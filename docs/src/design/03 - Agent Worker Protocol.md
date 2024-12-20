# 代理工作器协议

## 系统架构

系统由多个进程组成，每个进程要么是_服务_进程，要么是_工作器_进程。
工作器进程托管应用程序代码（代理）并连接到服务进程。
工作器向服务通告它们支持的代理，以便服务可以决定将代理放置在哪个工作器上。
服务进程协调代理在工作器进程上的放置，并促进代理之间的通信。

代理实例由元组 `(namespace: str, name: str)` 标识。
_namespace_ 和 _name_ 都由应用程序定义。
系统不对 _namespace_ 施加任何语义：它是自由格式的，任何语义都由应用程序代码实现。
_name_ 用于将请求路由到支持该名称的代理的工作器。
工作器向服务通告它们能够托管的代理名称集合。
工作器根据从服务接收的消息激活代理。
服务使用 _name_ 来确定当前非活动代理的放置位置，维护从代理名称到支持该代理的工作器集合的映射。
服务维护一个_目录_，将活动代理 ID 映射到托管该代理的工作器进程。

### 代理生命周期

代理永远不会被显式创建或销毁。当收到针对当前非活动代理的请求时，服务负责选择一个能够托管该代理的工作器，并将请求路由到该工作器。

## 工作器协议流程

工作器协议有三个阶段，遵循工作器的生命周期：初始化、运行和终止。

### 初始化

当工作器进程启动时，它启动与服务进程的连接，建立一个双向通信通道，用于传递消息。
接下来，工作器发出零个或多个 `RegisterAgentType(name: str)` 消息，告诉服务它能够托管的代理的名称。

* 待办：工作器应该向服务提供哪些其他元数据？
* 待办：我们是否应该给工作器一个唯一的 ID，可以用来在其生命周期内识别它？我们是否应该允许这个 ID 由工作器进程本身指定？

### 运行

一旦建立连接，并且服务知道工作器能够托管哪些代理，工作器就可以开始接收它必须托管的代理的请求。
代理的放置是响应 `Event(...)` 或 `RpcRequest(...)` 消息而发生的。
工作器维护一个本地活动代理的_目录_：从代理 ID 到代理实例的映射。
如果收到针对目录中没有对应条目的代理的消息，工作器会激活该代理的新实例并将其插入目录。
工作器将消息分发给代理：

* 对于 `Event`，代理处理消息，不生成响应。
* 对于 `RpcRequest` 消息，代理处理消息并生成 `RpcResponse` 类型的响应。工作器将响应路由回原始发送者。

工作器维护一个未完成请求的映射，通过 `RpcRequest.id` 标识，映射到未来 `RpcResponse` 的承诺。
当收到 `RpcResponse` 时，工作器找到相应的请求 ID 并使用该响应实现承诺。
如果在指定的时间范围内（例如，30秒）没有收到响应，工作器会以超时错误中断承诺。

### 终止

当工作器准备关闭时，它关闭与服务的连接并终止。服务注销工作器和所有托管在其上的代理实例。