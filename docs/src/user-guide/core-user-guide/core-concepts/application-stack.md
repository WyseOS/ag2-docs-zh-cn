# 应用程序栈

AutoGen core 被设计为一个无偏见的框架，可用于构建各种多代理应用程序。它不与任何特定的代理抽象或多代理模式绑定。

下图显示了应用程序栈。

![Application Stack](application-stack.svg)

在栈的底层是基础消息传递和路由设施，使代理能够相互通信。这些由代理运行时管理，对于大多数应用程序来说，开发人员只需要与运行时提供的高级 API 交互。 (见 [Agent and Agent Runtime](../framework/agent-and-agent-runtime.ipynb)).

在栈的顶层，开发人员需要定义代理交换的消息类型。这组消息类型形成了代理必须遵守的行为契约，而契约的实现决定了代理如何处理消息。行为契约有时也被称为消息协议。实现行为契约是开发人员的责任。多代理模式从这些行为契约中产生。
(见 [Multi-Agent Design Patterns](../design-patterns/index.md)).

## 示例应用

让我们考虑一个用于代码生成的多代理应用程序的具体示例。该应用程序由三个代理组成：
编码代理（Coder Agent）、执行代理（Executor Agent）和审查代理（Reviewer Agent）。
下图显示了代理之间的数据流和它们之间交换的消息类型。

![Code Generation Example](code-gen-example.svg)

在这个例子中，行为契约包含以下内容：

- 从应用程序到编码代理的 `CodingTaskMsg` 消息
- 从编码代理到执行代理的 `CodeGenMsg` 
- 从执行代理到审查代理的 `ExecutionResultMsg`
- 从审查代理到编码代理的 `ReviewMsg`
- 从审查代理到应用程序的 `CodingResultMsg`

行为契约通过代理对这些消息的处理来实现。例如，审查代理监听 `ExecutionResultMsg` 并评估代码执行结果以决定是否批准或拒绝，如果批准，它会向应用程序发送 `CodingResultMsg`，否则，它会向编码代理发送 `ReviewMsg` 进行另一轮代码生成。

这个行为契约是一个称为_反思_的多代理模式的案例，其中生成结果通过另一轮生成进行审查，以提高整体质量。