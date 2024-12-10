# 日志记录

AutoGen 使用 Python 内置的 [`logging`](https://docs.python.org/3/library/logging.html) 模块。

有两种类型的日志记录：

- **跟踪日志**：这用于调试，是人类可读的消息，用于指示正在发生什么。这旨在帮助开发人员理解代码中发生的事情。其他系统不应依赖这些日志的内容和格式。
    - 名称：{py:attr}`~autogen_core.application.logging.TRACE_LOGGER_NAME`。
- **结构化日志**：此记录器发出可被其他系统使用的结构化事件。其他系统可以依赖这些日志的内容和格式。
    - 名称：{py:attr}`~autogen_core.application.logging.EVENT_LOGGER_NAME`。
    - 查看模块 {py:mod}`autogen_core.application.logging.events` 以了解可用的事件。
- {py:attr}`~autogen_core.application.logging.ROOT_LOGGER` 可用于启用或禁用所有日志。

## 启用日志输出

要启用跟踪日志，您可以使用以下代码：

```python
import logging

from autogen_core.application.logging import TRACE_LOGGER_NAME

logging.basicConfig(level=logging.WARNING)
logger = logging.getLogger(TRACE_LOGGER_NAME)
logger.setLevel(logging.DEBUG)
```

### 结构化日志

结构化日志允许您编写处理逻辑，处理包含所有字段的实际事件，而不仅仅是格式化的字符串。

例如，如果您定义了这个自定义事件并正在发出它，那么您可以编写以下处理程序来接收它。

```python
import logging
from dataclasses import dataclass

@dataclass
class MyEvent:
    timestamp: str
    message: str

class MyHandler(logging.Handler):
    def __init__(self) -> None:
        super().__init__()

    def emit(self, record: logging.LogRecord) -> None:
        try:
            # Use the StructuredMessage if the message is an instance of it
            if isinstance(record.msg, MyEvent):
                print(f"Timestamp: {record.msg.timestamp}, Message: {record.msg.message}")
        except Exception:
            self.handleError(record)
```

以下是如何使用它：

```python
logger = logging.getLogger(EVENT_LOGGER_NAME)
logger.setLevel(logging.INFO)
my_handler = MyHandler()
logger.handlers = [my_handler]
```

## 发出日志

这两个名称是这些类型的根记录器。发出日志的代码应该使用这些记录器的子记录器。例如，如果您正在编写一个模块 `my_module` 并且想要发出跟踪日志，您应该使用以下名称的记录器：

```python
import logging

from autogen_core.application.logging import TRACE_LOGGER_NAME
logger = logging.getLogger(f"{TRACE_LOGGER_NAME}.my_module")
```

### 发出结构化日志

如果您的事件看起来像：

```python
from dataclasses import dataclass

@dataclass
class MyEvent:
    timestamp: str
    message: str
```

那么它可以在代码中这样发出：

```python
from autogen_core.application.logging import EVENT_LOGGER_NAME

logger = logging.getLogger(EVENT_LOGGER_NAME + ".my_module")
logger.info(MyEvent("timestamp", "message"))
```
