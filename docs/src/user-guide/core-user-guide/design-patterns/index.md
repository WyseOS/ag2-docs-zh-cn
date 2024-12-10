# 多代理设计模式

代理可以通过各种方式协同工作来解决问题。像 [AutoGen](https://aka.ms/autogen-paper)、[MetaGPT](https://arxiv.org/abs/2308.00352) 和 [ChatDev](https://arxiv.org/abs/2307.07924) 这样的研究工作已经表明，多代理系统在软件开发等复杂任务中的表现优于单代理系统。

多代理设计模式是从消息协议中产生的结构：它描述了代理如何相互交互来解决问题。例如，前一节中的[tool-equipped-agent](../framework/tools.ipynb#tool-equipped-agent)采用了一种称为 ReAct 的设计模式，该模式涉及代理与工具的交互。

您可以使用 AutoGen 代理实现任何多代理设计模式。在接下来的两节中，我们将讨论两种常见的设计模式：用于任务分解的群聊，以及用于增强稳健性的反思。

```{toctree}
:maxdepth: 1

group-chat
handoffs
mixture-of-agents
multi-agent-debate
reflection
```
