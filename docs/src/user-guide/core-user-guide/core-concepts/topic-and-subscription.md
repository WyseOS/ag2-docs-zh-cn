# 主题和订阅

运行时有两种传递消息的方式：直接消息传递或广播。直接消息传递是一对一的：发送者必须提供接收者的代理 ID。另一方面，广播是一对多的，发送者不提供接收者的代理 ID。

许多场景适合使用广播。例如，在事件驱动的工作流中，代理并不总是知道谁将处理它们的消息，而且工作流可以由没有相互依赖关系的代理组成。本节重点介绍广播中的核心概念：主题和订阅。

## Topic

Topic定义了广播消息的范围。本质上，代理运行时通过其广播 API 实现了一个发布-订阅模型：在发布消息时，必须指定主题。它是代理 ID 的一个间接层。

主题由两个组成部分：主题类型和主题来源。

```{note}
Topic = (Topic Type, Topic Source)
```

与 [agent ID](./agent-identity-and-lifecycle.md#agent-id)类似，主题类型也有两个组成部分，通常由应用程序代码定义，用于标记主题所针对的消息类型。例如，GitHub 代理在发布关于新问题的消息时可能使用 `"GitHub_Issues"` 作为主题类型。

主题来源是主题类型内的唯一标识符。它通常由应用程序数据定义。例如，GitHub 代理可能使用 `"github.com/{repo_name}/issues/{issue_number}"` 作为主题来源来唯一标识主题。主题来源允许发布者限制消息的范围并创建隔离区。

主题 ID 可以与字符串相互转换。字符串的格式是：

```{note}
Topic_Type/Topic_Source
```

类型在 UTF8 中且仅包含字母数字字符（a-z）和（0-9）或下划线（_）时被视为有效。有效标识符不能以数字开头，也不能包含任何空格。
来源在 UTF8 中且仅包含 ascii 32（空格）到 126（~）之间（包含）的字符时被视为有效。

## 订阅

订阅将主题映射到代理 ID。

![Subscription](subscription.svg)

上图显示了主题和订阅之间的关系。代理运行时跟踪订阅并使用它们将消息传递给代理。

如果主题没有订阅，发布到该主题的消息将不会传递给任何代理。如果主题有多个订阅，消息将按照所有订阅只向每个接收代理传递一次。应用程序可以使用代理运行时的 API 添加或删除订阅。

## 基于类型的订阅

基于类型的订阅将主题类型映射到代理类型
(见 [agent ID](./agent-identity-and-lifecycle.md#agent-id))。

它声明了一个从主题到代理 ID 的无界映射，而无需知道确切的主题来源和代理密钥。机制很简单：任何匹配基于类型订阅的主题类型的主题都将映射到具有订阅代理类型的代理 ID，并将代理密钥分配给主题来源的值。对于 Python API，使用 {py:class}`~autogen_core.components.TypeSubscription`。

```{note}
基于类型的订阅 = 主题类型 --> 代理类型
```

一般来说，基于类型的订阅是声明订阅的首选方式。它是可移植的和数据独立的：开发人员不需要编写依赖于特定代理 ID 的应用程序代码。

### 基于类型订阅的场景

当确切的主题或代理 ID 依赖于数据时，基于类型的订阅可以应用于许多场景。这些场景可以根据两个考虑因素来分解：
(1) 是单租户还是多租户，以及
(2) 每个租户是单个主题还是多个主题。
租户通常指处理特定用户会话或特定请求的一组代理。

#### 单租户，单Topic

在这种场景中，整个应用程序只有一个租户和一个Topic。
这是最简单的场景，可以用于许多情况，如命令行工具或单用户应用程序。

要对这种场景应用基于类型的订阅，为每个代理类型创建一个基于类型的订阅，并为所有基于类型的订阅使用相同的Topic类型。
在发布时，始终使用相同的Topic，即相同的Topic类型和Topic来源。

例如，假设有三种代理类型：`"triage_agent"`、`"coder_agent"` 和 `"reviewer_agent"`，Topic类型是 `"default"`，创建以下基于类型的订阅：

```python
# Type-based Subscriptions for single-tenant, single topic scenario
TypeSubscription(topic_type="default", agent_type="triage_agent")
TypeSubscription(topic_type="default", agent_type="coder_agent")
TypeSubscription(topic_type="default", agent_type="reviewer_agent")
```

使用上述基于类型的订阅，对所有消息使用相同的主题来源 `"default"`。因此主题始终是 `("default", "default")`。发布到此主题的消息将传递给上述所有类型的所有代理。具体来说，消息将发送到以下代理 ID：

```python
# The agent IDs created based on the topic source
AgentID("triage_agent", "default")
AgentID("coder_agent", "default")
AgentID("reviewer_agent", "default")
```

下图显示了在此示例中基于类型的订阅是如何工作的。

![Type-Based Subscription Single-Tenant, Single Topic Scenario Example](type-subscription-single-tenant-single-topic.svg)

如果具有该 ID 的代理不存在，运行时将创建它。

#### 单租户，多主题

在这种场景中，只有一个租户，但您想控制哪个代理处理哪个主题。当您想创建隔离区并让不同的代理专门处理不同的主题时，这很有用。

要对这种场景应用基于类型的订阅，为每个代理类型创建一个基于类型的订阅，但使用不同的主题类型。如果您希望这些代理类型共享相同的主题，可以将相同的主题类型映射到多个代理类型。对于主题来源，在发布时仍然对所有消息使用相同的值。

继续上面的示例，使用相同的代理类型，创建以下基于类型的订阅：

```python
# Type-based Subscriptions for single-tenant, multiple topics scenario
TypeSubscription(topic_type="triage", agent_type="triage_agent")
TypeSubscription(topic_type="coding", agent_type="coder_agent")
TypeSubscription(topic_type="coding", agent_type="reviewer_agent")
```

使用上述基于类型的订阅，发布到主题 `("triage", "default")` 的任何消息都将传递给类型为 `"triage_agent"` 的代理，而发布到主题 `("coding", "default")` 的任何消息都将传递给类型为 `"coder_agent"` 和 `"reviewer_agent"` 的代理。

下图显示了在此示例中基于类型的订阅是如何工作的。

![Type-Based Subscription Single-Tenant, Multiple Topics Scenario Example](type-subscription-single-tenant-multiple-topics.svg)

#### 多租户场景

在单租户场景中，主题来源始终相同（例如 `"default"`）—— 它在应用程序代码中是硬编码的。当转向多租户场景时，主题来源变得依赖于数据。

```{note}
表明您处于多租户场景的一个好迹象是您需要同一代理类型的多个实例。例如，您可能希望有不同的代理实例来处理不同的用户会话以保持私有数据隔离，或者，您可能希望将繁重的工作负载分配给同一代理类型的多个实例，让它们同时处理。
```

继续上面的示例，如果您想要专门的代理实例来处理特定的 GitHub 问题，您需要将主题来源设置为该问题的唯一标识符。

例如，假设有一个代理类型 `"triage_agent"` 的基于类型的订阅：

```python
TypeSubscription(topic_type="github_issues", agent_type="triage_agent")
```

当消息发布到主题 `("github_issues", "github.com/microsoft/autogen/issues/1")` 时，运行时将把消息传递给 ID 为 `("triage_agent", "github.com/microsoft/autogen/issues/1")` 的代理。当消息发布到主题 `("github_issues", "github.com/microsoft/autogen/issues/9")` 时，运行时将把消息传递给 ID 为 `("triage_agent", "github.com/microsoft/autogen/issues/9")` 的代理。

下图显示了在此示例中基于类型的订阅是如何工作的。

![Type-Based Subscription Multi-Tenant Scenario Example](type-subscription-multi-tenant.svg)

注意代理 ID 是依赖于数据的，如果代理不存在，运行时将创建该代理的新实例。

要支持每个租户的多个主题，您可以使用不同的主题类型，就像单租户、多主题场景一样。