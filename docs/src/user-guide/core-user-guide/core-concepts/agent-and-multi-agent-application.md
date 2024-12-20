# 代理和多代理应用

**代理**是一个通过消息进行通信、维护自身状态，并根据接收到的消息或状态变化执行操作的软件实体。这些操作可能会修改代理的状态并产生外部效果，如更新消息日志、发送新消息、执行代码或进行 API 调用。

许多软件系统可以被建模为相互交互的独立代理的集合。例如：

- 工厂车间的传感器
- 支持 Web 应用程序的分布式服务
- 涉及多个利益相关者的业务工作流
- AI 代理，如由语言模型（例如 GPT-4）驱动的代理，可以编写代码、与外部系统交互并与其他代理通信。

这些由多个交互代理组成的系统被称为**多代理应用**。

> **注意：**  
> AI 代理通常使用语言模型作为其软件栈的一部分来解释消息、执行推理和执行操作。

## 多代理应用的特点

在多代理应用中，代理可能：

- 在同一进程或同一机器上运行
- 跨不同机器或组织边界运行
- 使用不同的编程语言实现，并使用不同的 AI 模型或指令
- 通过消息传递协调行动，共同实现共同目标

每个代理都是一个可以独立开发、测试和部署的自包含单元。这种模块化设计允许代理在不同场景中重复使用，并组合成更复杂的系统。

代理本质上是**可组合的**：简单的代理可以组合形成复杂的、适应性强的应用程序，其中每个代理为整个系统贡献特定的功能或服务。