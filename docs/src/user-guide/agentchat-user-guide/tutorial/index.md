---
myst:
  html_meta:
    "description lang=zh-cn": |
      AutoGen AgentChat 教程，一个用于构建多智能体应用的框架。
    "charset": "utf-8"
---

# 教程

AutoGen AgentChat 教程，一个用于构建多智能体应用的框架。

```{include} ../warning.md

```

::::{grid} 2 2 2 3
:gutter: 3

:::{grid-item-card} {fas}`book-open;pst-color-primary` Models
:link: ./models.html

设置用于代理和团队的模型客户端。
:::

:::{grid-item-card} {fas}`users;pst-color-primary` Agents
:link: ./agents.html

构建使用模型、工具和代码执行器的代理。
:::

:::{grid-item-card} {fas}`users;pst-color-primary` Teams Intro
:link: ./teams.html

介绍团队和任务终止。
:::

:::{grid-item-card} {fas}`users;pst-color-primary` Selector Group Chat
:link: ./selector-group-chat.html

一个使用模型策略和自定义选择器的智能团队。
:::

:::{grid-item-card} {fas}`users;pst-color-primary` Swarm
:link: ./swarm.html

一个使用传递任务在代理之间传递任务的动态团队。
:::

:::{grid-item-card} {fas}`users;pst-color-primary` Custom Agents
:link: ./custom-agents.html

如何构建自定义代理。
:::

::::

```{toctree}
:maxdepth: 1
:hidden:

models
agents
teams
selector-group-chat
swarm
termination
custom-agents
```
