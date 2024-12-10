---
myst:
  html_meta:
    "description lang=zh-cn": |
      AutoGen 扩展用户指南，一个用于构建多代理应用程序的框架。
    "charset": "utf-8"
---

# 扩展

```{toctree}
:maxdepth: 3
:hidden:

azure-container-code-executor
```


## 发现社区项目:

::::{grid} 1 2 2 2
:margin: 4 4 0 0
:gutter: 1

:::{grid-item-card} {fas}`globe;pst-color-primary` <br> Ecosystem
:link: https://github.com/topics/autogen
:class-item: api-card
:columns: 12

查找与 AutoGen 配合使用的示例、服务和其他内容

:::

:::{grid-item-card} {fas}`puzzle-piece;pst-color-primary` <br> Community Extensions
:link: https://github.com/topics/autogen-extension
:class-item: api-card

查找用于3方工具、组件和服务的 AutoGen 扩展

:::

:::{grid-item-card} {fas}`vial;pst-color-primary` <br> Community Samples
:link: https://github.com/topics/autogen-sample
:class-item: api-card

查找与 AutoGen 配合使用的示例、服务和其他内容

:::

::::


### 社区项目列表

| 名称                                                                          | 包                                                       | 描述                                                                       |
| ----------------------------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------------------------- |
| [autogen-watsonx-client](https://github.com/tsinggggg/autogen-watsonx-client) | [PyPi](https://pypi.org/project/autogen-watsonx-client/) | Model client for [IBM watsonx.ai](https://www.ibm.com/products/watsonx-ai) |

<!-- Example -->
<!-- | [My Model Client](https://github.com/example)  | [PyPi](https://pypi.org/project/example) | Model client for my custom model service | -->
<!-- - Name should link to the project page or repo
- Package should link to the PyPi page
- Description should be a brief description of the project. 1 short sentence is ideal. -->


## 内置扩展

阅读内置扩展的文档:

```{note}
WIP
```

<!-- ::::{grid} 1 2 3 3
:margin: 4 4 0 0
:gutter: 1

:::{grid-item-card} LangChain Tools
:link: python/autogen_agentchat/autogen_agentchat
:link-type: doc
:::

:::{grid-item-card} ACA Dynamic Sessions Code Executor
:link: python/autogen_agentchat/autogen_agentchat
:link-type: doc
:::

:::: -->


## 创建自己的社区扩展

在 0.4 版本中，创建和发布自己的扩展比以往任何时候都更容易。本页面详细介绍了一些最佳实践，以确保您的扩展包与 AutoGen 生态系统无缝集成。

### 最佳实践

#### 命名

没有命名要求。但前缀包名称为 `autogen-` 会使其更容易被发现。

#### 常见接口

尽可能实现 `autogen_core` 包中提供的接口。这将使用户获得更一致的体验。

##### 依赖 AutoGen

为确保扩展与设计时使用的 AutoGen 版本兼容，建议在 `pyproject.toml` 的依赖项部分指定 AutoGen 的版本，并使用适当的约束。

```toml
[project]
# ...
dependencies = [
    "autogen-core>=0.4,<0.5"
]
```

#### 使用类型提示

AutoGen 拥抱使用类型提示来提供更好的开发体验。扩展应尽可能使用类型提示。

### Discovery

为使您的扩展、示例、服务或包更容易被用户发现，您可以 [添加主题](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/classifying-your-repository-with-topics) [`autogen`](https://github.com/topics/autogen) 到 GitHub 仓库。

更具体的话题也已可用：

- [`autogen-extension`](https://github.com/topics/autogen-extension) for extensions
- [`autogen-sample`](https://github.com/topics/autogen-sample) for samples

### 从 0.2 版本的变化

在 AutoGen 0.2 中，常见做法是将 3 方扩展和示例合并到主仓库中。我们非常感谢所有在 0.2 版本中为生态系统笔记本、模块和页面做出贡献的用户。然而，总体上我们正在远离这种模式，以允许更多的灵活性和减少维护负担。

有 `autogen-ext` 包用于 1 方支持的扩展，但我们希望选择性地管理维护负担。如果您想看看您的扩展是否适合添加到 `autogen-ext`，请打开一个 issue 并让我们讨论。否则，我们鼓励您将您的扩展作为单独的包发布，并遵循 [发现](#discovery) 下的指南，以便用户更容易发现。

