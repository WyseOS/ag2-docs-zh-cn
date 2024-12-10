---
myst:
  html_meta:
    "description lang=zh-cn": |
      AgentChat 的用户指南，一个用于 AutoGen 的高级 API
    "charset": "utf-8"
---

# AgentChat

AgentChat 是一个用于构建多代理应用程序的高级 API。
它建立在 [`autogen-core`](../core-user-guide/index.md) 包之上。
对于初学者用户，AgentChat 是推荐的起点。
对于高级用户，[`autogen-core`](../core-user-guide/index.md) 的事件驱动编程模型提供了更多的灵活性和对底层组件的控制。

AgentChat 旨在提供直观的默认值，例如具有预设行为的 **Agents** 和具有预定义 [多代理设计模式](../core-user-guide/design-patterns/index.md) 的 **Teams**，以简化多代理应用程序的构建。

```{include} warning.md

```

```{tip}
如果您对实现复杂的代理交互行为、定义自定义消息协议或编排机制感兴趣，请考虑使用 [`autogen-core`](../core-user-guide/index.md) 包。

```

::::{grid} 2 2 2 2
:gutter: 3

:::{grid-item-card} {fas}`download;pst-color-primary` 安装
:link: ./installation.html

如何安装 AgentChat
:::

:::{grid-item-card} {fas}`rocket;pst-color-primary` 快速开始
:link: ./quickstart.html

构建您的第一个代理
:::

:::{grid-item-card} {fas}`graduation-cap;pst-color-primary` 教程
:link: ./tutorial/index.html

逐步指南，使用 AgentChat
:::

:::{grid-item-card} {fas}`code;pst-color-primary` 示例
:link: ./examples/index.html

示例代码和用例
:::
::::

```{toctree}
:maxdepth: 1
:hidden:

installation
quickstart
tutorial/index
examples/index
```
