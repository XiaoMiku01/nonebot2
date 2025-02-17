---
sidebar_position: 2
---

# NoneBot.config 模块

## 配置

NoneBot 使用 [pydantic](https://pydantic-docs.helpmanual.io/) 以及 [python-dotenv](https://saurabh-kumar.com/python-dotenv/) 来读取配置。

配置项需符合特殊格式或 json 序列化格式。详情见 [pydantic Field Type](https://pydantic-docs.helpmanual.io/usage/types/) 文档。

## _class_ `Env`

基类：`nonebot.config.BaseConfig`

运行环境配置。大小写不敏感。

将会从 `nonebot.init 参数` > `环境变量` > `.env 环境配置文件` 的优先级读取配置。

### `environment`

- **类型**: `str`

- **默认值**: `"prod"`

- **说明**

  当前环境名。 NoneBot 将从 `.env.{environment}` 文件中加载配置。

## _class_ `Config`

基类：`nonebot.config.BaseConfig`

NoneBot 主要配置。大小写不敏感。

除了 NoneBot 的配置项外，还可以自行添加配置项到 `.env.{environment}` 文件中。
这些配置将会在 json 反序列化后一起带入 `Config` 类中。

### `driver`

- **类型**: `str`

- **默认值**: `"~fastapi"`

- **说明**

  NoneBot 运行所使用的 `Driver` 。继承自 `nonebot.drivers.Driver` 。

  配置格式为 `<module>[:<Driver>][+<module>[:<Mixin>]]*`。

  `~` 为 `nonebot.drivers.` 的缩写。

### `host`

- **类型**: `IPvAnyAddress`

- **默认值**: `127.0.0.1`

- **说明**

  NoneBot 的 HTTP 和 WebSocket 服务端监听的 IP/主机名。

### `port`

- **类型**: `int`

- **默认值**: `8080`

- **说明**

  NoneBot 的 HTTP 和 WebSocket 服务端监听的端口。

### `log_level`

- **类型**: `Union[int, str]`

- **默认值**: `INFO`

- **说明**

  配置 NoneBot 日志输出等级，可以为 `int` 类型等级或等级名称，参考 [loguru 日志等级](https://loguru.readthedocs.io/en/stable/api/logger.html#levels)。

- **示例**

```default
LOG_LEVEL=25
LOG_LEVEL=INFO
```

### `api_timeout`

- **类型**: `Optional[float]`

- **默认值**: `30.`

- **说明**

  API 请求超时时间，单位: 秒。

### `superusers`

- **类型**: `Set[str]`

- **默认值**: `set()`

- **说明**

  机器人超级用户。

- **示例**

```default
SUPERUSERS=["12345789"]
```

### `nickname`

- **类型**: `Set[str]`

- **默认值**: `set()`

- **说明**

  机器人昵称。

### `command_start`

- **类型**: `Set[str]`

- **默认值**: `{"/"}`

- **说明**

  命令的起始标记，用于判断一条消息是不是命令。

### `command_sep`

- **类型**: `Set[str]`

- **默认值**: `{"."}`

- **说明**

  命令的分隔标记，用于将文本形式的命令切分为元组（实际的命令名）。

### `session_expire_timeout`

- **类型**: `timedelta`

- **默认值**: `timedelta(minutes=2)`

- **说明**

  等待用户回复的超时时间。

- **示例**

```default
SESSION_EXPIRE_TIMEOUT=120  # 单位: 秒
SESSION_EXPIRE_TIMEOUT=[DD ][HH:MM]SS[.ffffff]
SESSION_EXPIRE_TIMEOUT=P[DD]DT[HH]H[MM]M[SS]S  # ISO 8601
```
