---
myst:
  html_meta:
    "description lang=zh-cn": |
      AutoGen 包提供了一套用于构建多代理应用程序的 AI 代理功能。
    "charset": "utf-8"
---

<style>
.card-title {
  font-size: 1.2rem;
  font-weight: bold;
}

.card-title svg {
  font-size: 2rem;
  vertical-align: bottom;
  margin-right: 5px;
}
</style>

# 代码库

## 0.4

(pkg-info-autogen-agentchat)=

:::{card} {fas}`people-group;pst-color-primary` AutoGen AgentChat
:class-title: card-title
:shadow: none

库与 AutoGen 0.2 类似，包括默认代理和群聊。

```sh
pip install 'autogen-agentchat==0.4.0.dev6'
```

[{fas}`circle-info;pst-color-primary` User Guide](/user-guide/agentchat-user-guide/index.md) | [{fas}`file-code;pst-color-primary` API Reference](/reference/python/autogen_agentchat/autogen_agentchat.rst) | [{fab}`python;pst-color-primary` PyPI](https://pypi.org/project/autogen-agentchat/0.4.0.dev6/) | [{fab}`github;pst-color-primary` Source](https://github.com/microsoft/autogen/tree/main/python/packages/autogen-agentchat)
:::

(pkg-info-autogen-core)=

:::{card} {fas}`cube;pst-color-primary` AutoGen Core
:class-title: card-title
:shadow: none

实现了 AutoGen 框架的核心功能，提供了创建多代理系统的基本构建块。

```sh
pip install 'autogen-core==0.4.0.dev6'
```

[{fas}`circle-info;pst-color-primary` User Guide](/user-guide/core-user-guide/index.md) | [{fas}`file-code;pst-color-primary` API Reference](/reference/python/autogen_core/autogen_core.rst) | [{fab}`python;pst-color-primary` PyPI](https://pypi.org/project/autogen-core/0.4.0.dev6/) | [{fab}`github;pst-color-primary` Source](https://github.com/microsoft/autogen/tree/main/python/packages/autogen-core)
:::

(pkg-info-autogen-ext)=

:::{card} {fas}`puzzle-piece;pst-color-primary` AutoGen Extensions
:class-title: card-title
:shadow: none

实现了与外部服务接口的组件，或使用额外依赖的组件。例如，基于 Docker 的代码执行。

```sh
pip install 'autogen-ext==0.4.0.dev6'
```

Extras:

- `langchain` needed for {py:class}`~autogen_ext.tools.LangChainToolAdapter`
- `azure` needed for {py:class}`~autogen_ext.code_executors.ACADynamicSessionsCodeExecutor`
- `docker` needed for {py:class}`~autogen_ext.code_executors.DockerCommandLineCodeExecutor`
- `openai` needed for {py:class}`~autogen_ext.models.OpenAIChatCompletionClient`

[{fas}`circle-info;pst-color-primary` User Guide](/user-guide/extensions-user-guide/index.md) | [{fas}`file-code;pst-color-primary` API Reference](/reference/python/autogen_ext/autogen_ext.rst) | [{fab}`python;pst-color-primary` PyPI](https://pypi.org/project/autogen-ext/0.4.0.dev6/) | [{fab}`github;pst-color-primary` Source](https://github.com/microsoft/autogen/tree/main/python/packages/autogen-ext)
:::

(pkg-info-autogen-magentic-one)=

:::{card} {fas}`users;pst-color-primary` Magentic One
:class-title: card-title
:shadow: none

一个通用的多代理机器人，利用五个代理来解决涉及多步骤规划和现实世界行动的复杂任务。

```{note}
Not yet available on PyPI.
```

[{fab}`github;pst-color-primary` Source](https://github.com/microsoft/autogen/tree/main/python/packages/autogen-magentic-one)
:::

## 0.2

(pkg-info-autogen-02)=

:::{card} {fas}`robot;pst-color-primary` AutoGen
:class-title: card-title
:shadow: none
现有的 AutoGen 库，提供了一个用于构建多代理系统的抽象。

```sh
pip install 'autogen-agentchat~=0.2'
```

[{fas}`circle-info;pst-color-primary` Documentation](https://microsoft.github.io/autogen/0.2/) | [{fab}`python;pst-color-primary` PyPI](https://pypi.org/project/autogen-agentchat/0.2.38/) | [{fab}`github;pst-color-primary` Source](https://github.com/microsoft/autogen/tree/0.2/)
:::

## 其他

(pkg-info-autogenbench)=

:::{card} {fas}`chart-bar;pst-color-primary` AutoGen Bench
:class-title: card-title
:shadow: none

AutoGenBench 是一个用于重复运行预定义的 AutoGen 任务的工具，在严格控制的初始条件下。

```sh
pip install autogenbench
```

[{fab}`python;pst-color-primary` PyPI](https://pypi.org/project/autogenbench/) | [{fab}`github;pst-color-primary` Source](https://github.com/microsoft/autogen/tree/main/python/packages/agbench)
:::
