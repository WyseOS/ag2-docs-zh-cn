# 主题

本文档描述了发布消息和订阅主题的语义和组件。

## 概述

主题被用作管理哪些代理接收给定已发布消息的基本单位。代理订阅主题。主题到代理实例的映射由应用程序定义。

这些概念有意映射到 [CloudEvents](https://cloudevents.io/) 规范。这允许与现有系统和工具轻松集成。

### 非目标

本文档不规定 RPC/直接消息传递

## 标识符

主题由两个组件标识（称为 `TopicId`）：

- [`type`](https://github.com/cloudevents/spec/blob/v1.0.2/cloudevents/spec.md#type) - 表示发生的事件类型，这在代码中是静态定义的
    - 应该使用反向域名表示法以避免命名冲突。例如：`com.example.my-topic`。
- [`source`](https://github.com/cloudevents/spec/blob/v1.0.2/cloudevents/spec.md#source-1) - 表示事件的起源，这是动态的，基于消息本身
    - 应该是一个 URI

代理实例由两个组件标识（称为 `AgentId`）：

- `type` - 表示代理类型，这在代码中是静态定义的
    - 必须是[此处](https://docs.python.org/3/reference/lexical_analysis.html#identifiers)定义的有效标识符，但只允许 ASCII 范围
- `key` - 表示该类型代理的实例的键
    - 应该是一个 URI

例如：`GraphicDesigner:1234`

## 订阅

订阅定义了哪些代理接收发布到主题的消息。订阅是动态的，可以随时添加或删除。

订阅定义了两件事：

- 匹配函数，类型为 `TopicId -> bool`，告诉我们"此订阅是否匹配此主题"
- 映射函数，类型为 `TopicId -> AgentId`，告诉我们"给定此订阅匹配此主题，它映射到哪个代理"

这些函数必须没有副作用，以便可以缓存评估结果。

### 代理实例创建

如果在主题上收到映射到尚不存在的代理的消息，运行时将实例化一个代理来满足请求。

## 消息类型

代理能够处理某些类型的消息。这是代理实现的内部细节。通道中的所有代理都将接收所有消息，但会忽略它无法处理的消息。

> [!注意]
> 基于扩展性和性能考虑，这一点可能会被重新审视。