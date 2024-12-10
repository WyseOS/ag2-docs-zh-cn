---
myst:
  html_meta:
    "description lang=zh-cn": |
      AutoGen Core 用户指南，一个用于构建多智能体应用的框架。
    "charset": "utf-8"
---

# Core

```{toctree}
:maxdepth: 1
:hidden:

quickstart
core-concepts/index
framework/index
design-patterns/index
cookbook/index
extensions-user-guide/index
faqs
```

```{warning}
这个项目和文档还在开发中。如果您有任何问题或需要帮助，请在 GitHub 上联系我们。
```

AutoGen Core 提供了一种简单的方法来快速构建事件驱动的、分布式的、可扩展的、有弹性的 AI 智能体系统。智能体是使用 [Actor 模型](https://en.wikipedia.org/wiki/Actor_model) 开发的。您可以在本地构建和运行您的智能体系统，并在准备好时轻松迁移到云中的分布式系统。

AutoGen Core 的主要功能包括：

```{gallery-grid}
:grid-columns: 1 2 2 3

- header: "{fas}`network-wired;pst-color-primary` 异步消息传递"
  content: "智能体通过异步消息传递进行通信，支持事件驱动和请求/响应通信模型。"
- header: "{fas}`cube;pst-color-primary` 可扩展和分布式"
  content: "支持跨组织边界的复杂场景。"
- header: "{fas}`code;pst-color-primary` Multi-Language Support"
  content: "Python & Dotnet 智能体今天就可以互操作，更多语言即将到来。"
- header: "{fas}`globe;pst-color-primary` 模块化和可扩展"
  content: "高度可定制，具有自定义智能体、内存即服务、工具注册表和模型库等功能。"
- header: "{fas}`puzzle-piece;pst-color-primary` 可观察和可调试"
  content: "Easily trace and debug your agent systems."
- header: "{fas}`project-diagram;pst-color-primary` 事件驱动架构"
  content: "构建事件驱动的、分布式的、可扩展的、有弹性的 AI 智能体系统。"
```
