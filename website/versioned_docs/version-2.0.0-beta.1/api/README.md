---
sidebar_position: 1
id: index
slug: /api
---

# NoneBot 模块

## 快捷导入

为方便使用，`nonebot` 模块从子模块导入了部分内容

- `on_message` => `nonebot.plugin.on_message`

- `on_notice` => `nonebot.plugin.on_notice`

- `on_request` => `nonebot.plugin.on_request`

- `on_metaevent` => `nonebot.plugin.on_metaevent`

- `on_startswith` => `nonebot.plugin.on_startswith`

- `on_endswith` => `nonebot.plugin.on_endswith`

- `on_keyword` => `nonebot.plugin.on_keyword`

- `on_command` => `nonebot.plugin.on_command`

- `on_shell_command` => `nonebot.plugin.on_shell_command`

- `on_regex` => `nonebot.plugin.on_regex`

- `CommandGroup` => `nonebot.plugin.CommandGroup`

- `Matchergroup` => `nonebot.plugin.MatcherGroup`

- `load_plugin` => `nonebot.plugin.load_plugin`

- `load_plugins` => `nonebot.plugin.load_plugins`

- `load_all_plugins` => `nonebot.plugin.load_all_plugins`

- `load_from_json` => `nonebot.plugin.load_from_json`

- `load_from_toml` => `nonebot.plugin.load_from_toml`

- `load_builtin_plugins` => `nonebot.plugin.load_builtin_plugins`

- `get_plugin` => `nonebot.plugin.get_plugin`

- `get_loaded_plugins` => `nonebot.plugin.get_loaded_plugins`

- `export` => `nonebot.plugin.export`

- `require` => `nonebot.plugin.require`

## `get_driver()`

- **说明**

  获取全局 Driver 对象。可用于在计划任务的回调中获取当前 Driver 对象。

- **返回**

  - `Driver`: 全局 Driver 对象

- **异常**

  - `ValueError`: 全局 Driver 对象尚未初始化 (nonebot.init 尚未调用)

- **用法**

```python
driver = nonebot.get_driver()
```

## `get_app()`

- **说明**

  获取全局 Driver 对应 Server App 对象。

- **返回**

  - `Any`: Server App 对象

- **异常**

  - `ValueError`: 全局 Driver 对象尚未初始化 (nonebot.init 尚未调用)

- **用法**

```python
app = nonebot.get_app()
```

## `get_asgi()`

- **说明**

  获取全局 Driver 对应 Asgi 对象。

- **返回**

  - `Any`: Asgi 对象

- **异常**

  - `ValueError`: 全局 Driver 对象尚未初始化 (nonebot.init 尚未调用)

- **用法**

```python
asgi = nonebot.get_asgi()
```

## `get_bot(self_id=None)`

- **说明**

  当提供 self_id 时，此函数是 get_bots()[self_id] 的简写；当不提供时，返回一个 Bot。

- **参数**

  - `self_id: Optional[str]`: 用来识别 Bot 的 ID

- **返回**

  - `Bot`: Bot 对象

- **异常**

  - `KeyError`: 对应 ID 的 Bot 不存在

  - `ValueError`: 全局 Driver 对象尚未初始化 (nonebot.init 尚未调用)

  - `ValueError`: 没有传入 ID 且没有 Bot 可用

- **用法**

```python
assert nonebot.get_bot('12345') == nonebot.get_bots()['12345']

another_unspecified_bot = nonebot.get_bot()
```

## `get_bots()`

- **说明**

  获取所有通过 ws 连接 NoneBot 的 Bot 对象。

- **返回**

  - `Dict[str, Bot]`: 一个以字符串 ID 为键，Bot 对象为值的字典

- **异常**

  - `ValueError`: 全局 Driver 对象尚未初始化 (nonebot.init 尚未调用)

- **用法**

```python
bots = nonebot.get_bots()
```

## `init(*, _env_file=None, **kwargs)`

- **说明**

  初始化 NoneBot 以及 全局 Driver 对象。

  NoneBot 将会从 .env 文件中读取环境信息，并使用相应的 env 文件配置。

  你也可以传入自定义的 \_env_file 来指定 NoneBot 从该文件读取配置。

- **参数**

  - `_env_file: Optional[str]`: 配置文件名，默认从 .env.{env_name} 中读取配置

  - `**kwargs`: 任意变量，将会存储到 Config 对象里

- **返回**

  - `None`

- **用法**

```python
nonebot.init(database=Database(...))
```

## `run(*args, **kwargs)`

- **说明**

  启动 NoneBot，即运行全局 Driver 对象。

- **参数**

  - `*args`: 传入 Driver.run 的位置参数

  - `**kwargs`: 传入 Driver.run 的命名参数

- **返回**

  - `None`

- **用法**

```python
nonebot.run(host="127.0.0.1", port=8080)
```
