# FAQs

## 如何获取底层的智能体实例？

智能体可能分布在多台机器上，因此不鼓励访问底层的智能体实例。如果智能体肯定在同一台机器上运行，您可以通过调用 {py:meth}`autogen_core.base.AgentRuntime.try_get_underlying_agent_instance` 访问智能体实例。如果智能体不可用，这将抛出异常。

## 如何调用智能体上的函数？

由于实例本身不可访问，您不能直接调用智能体上的函数。相反，您应该创建一个类型来表示函数调用及其参数，然后将该消息发送给智能体。然后在智能体中为该消息类型创建一个处理程序并实现所需的逻辑。这也支持返回响应给调用者。

这使得智能体可以在分布式环境中工作，也可以在本地环境中工作。

## 为什么需要使用工厂来注册智能体？

一个 {py:class}`autogen_core.base.AgentId` 由一个 `type` 和一个 `key` 组成。类型对应于创建智能体的工厂，而键是此实例的运行时、数据依赖的键。

键可以对应于用户 id、会话 id，或者如果您不需要区分实例，则可以只是 "default"。每个唯一的键将基于提供的工厂创建智能体的新实例。这使得系统可以自动扩展到同一智能体的不同实例，并根据您在应用程序中选择如何处理键来独立管理每个实例的生命周期。

## 如何增加 GRPC 消息大小？

如果您需要提供自定义的 gRPC 选项，例如覆盖 `max_send_message_length` 和 `max_receive_message_length`，您可以定义一个 `extra_grpc_config` 变量，并将其传递给 `WorkerAgentRuntimeHost` 和 `WorkerAgentRuntime` 实例。

```python
# Define custom gRPC options
extra_grpc_config = [
    ("grpc.max_send_message_length", new_max_size),
    ("grpc.max_receive_message_length", new_max_size),
]

# Create instances of WorkerAgentRuntimeHost and WorkerAgentRuntime with the custom gRPC options

host = WorkerAgentRuntimeHost(address=host_address, extra_grpc_config=extra_grpc_config)
worker1 = WorkerAgentRuntime(host_address=host_address, extra_grpc_config=extra_grpc_config)
```

**注意**：当 `WorkerAgentRuntime` 为客户端创建主机连接时，它使用来自 `HostConnection` 类的 `DEFAULT_GRPC_CONFIG` 作为默认值集，如果您使用 `extra_grpc_config` 传递同名参数，这些默认值可以被覆盖。
