---
myst:
  html_meta:
    "description lang=zh-cn": |
      对AutoGen 提供的编程模型、消息订阅、代理通信协议和多代理系统架构的详细设计。
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

# 设计

:::{card} {fas}`code;pst-color-primary` 编程模型
:class-title: card-title
:shadow: none

了解 AutoGen 的核心编程模型，包括事件驱动架构和代理通信机制。

[{fas}`book;pst-color-primary` 查看详情](01%20-%20Programming%20Model.md)
:::

:::{card} {fas}`sitemap;pst-color-primary` 主题系统
:class-title: card-title
:shadow: none

探索 AutoGen 的主题发布订阅系统，实现灵活的代理间通信。

[{fas}`book;pst-color-primary` 查看详情](02%20-%20Topics.md)
:::

:::{card} {fas}`exchange;pst-color-primary` 代理通信协议
:class-title: card-title
:shadow: none

深入了解代理间通信的协议规范和实现细节。

[{fas}`book;pst-color-primary` 查看详情](03%20-%20Agent%20Worker%20Protocol.md)
:::

:::{card} {fas}`fingerprint;pst-color-primary` 代理和主题 ID 规范
:class-title: card-title
:shadow: none

了解系统中代理和主题的标识符规范。

[{fas}`book;pst-color-primary` 查看详情](04%20-%20Agent%20and%20Topic%20ID%20Specs.md)
:::

:::{card} {fas}`cogs;pst-color-primary` 服务
:class-title: card-title
:shadow: none

AutoGen 提供的核心服务和功能。

[{fas}`book;pst-color-primary` 查看详情](05%20-%20Services.md)
:::

```{toctree}
:maxdepth: 2
:hidden:

01 - Programming Model
02 - Topics
03 - Agent Worker Protocol
04 - Agent and Topic ID Specs
05 - Services
```