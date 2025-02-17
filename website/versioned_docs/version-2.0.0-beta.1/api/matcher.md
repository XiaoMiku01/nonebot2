---
sidebar_position: 5
---

# NoneBot.matcher 模块

## 事件响应器

该模块实现事件响应器的创建与运行，并提供一些快捷方法来帮助用户更好的与机器人进行对话 。

## `matchers`

- **类型**

  `Dict[int, List[Type[Matcher]]]`

- **说明**

  用于存储当前所有的事件响应器

## _class_ `Matcher`

基类：`object`

事件响应器类

### `plugin`

- **类型**

  `Optional[Plugin]`

- **说明**

  事件响应器所在插件

### `module`

- **类型**

  `Optional[ModuleType]`

- **说明**

  事件响应器所在插件模块

### `plugin_name`

- **类型**

  `Optional[str]`

- **说明**

  事件响应器所在插件名

### `module_name`

- **类型**

  `Optional[str]`

- **说明**

  事件响应器所在点分割插件模块路径

### `type`

- **类型**

  `str`

- **说明**

  事件响应器类型

### `rule`

- **类型**

  `Rule`

- **说明**

  事件响应器匹配规则

### `permission`

- **类型**

  `Permission`

- **说明**

  事件响应器触发权限

### `priority`

- **类型**

  `int`

- **说明**

  事件响应器优先级

### `block`

- **类型**

  `bool`

- **说明**

  事件响应器是否阻止事件传播

### `temp`

- **类型**

  `bool`

- **说明**

  事件响应器是否为临时

### `expire_time`

- **类型**

  `Optional[datetime]`

- **说明**

  事件响应器过期时间点

### `_default_state`

- **类型**

  `T_State`

- **说明**

  事件响应器默认状态

### `_default_type_updater`

- **类型**

  `Optional[Dependent]`

- **说明**

  事件响应器类型更新函数

### `_default_permission_updater`

- **类型**

  `Optional[Dependent]`

- **说明**

  事件响应器权限更新函数

### `__init__()`

实例化 Matcher 以便运行

### `handlers`

- **类型**

  `List[Handler]`

- **说明**

  事件响应器拥有的事件处理函数列表

### _classmethod_ `new(type_='', rule=None, permission=None, handlers=None, temp=False, priority=1, block=False, *, plugin=None, module=None, expire_time=None, default_state=None, default_type_updater=None, default_permission_updater=None)`

- **说明**

  创建一个新的事件响应器，并存储至 [matchers](#matchers)

- **参数**

  - `type_: str`: 事件响应器类型，与 `event.get_type()` 一致时触发，空字符串表示任意

  - `rule: Optional[Rule]`: 匹配规则

  - `permission: Optional[Permission]`: 权限

  - `handlers: Optional[List[T_Handler]]`: 事件处理函数列表

  - `temp: bool`: 是否为临时事件响应器，即触发一次后删除

  - `priority: int`: 响应优先级

  - `block: bool`: 是否阻止事件向更低优先级的响应器传播

  - `plugin: Optional[Plugin]`: 事件响应器所在插件

  - `module: Optional[ModuleType]`: 事件响应器所在模块

  - `default_state: Optional[T_State]`: 默认状态 `state`

  - `expire_time: Optional[datetime]`: 事件响应器最终有效时间点，过时即被删除

- **返回**

  - `Type[Matcher]`: 新的事件响应器类

### _async classmethod_ `check_perm(bot, event, stack=None, dependency_cache=None)`

- **说明**

  检查是否满足触发权限

- **参数**

  - `bot: Bot`: Bot 对象

  - `event: Event`: 上报事件

- **返回**

  - `bool`: 是否满足权限

### _async classmethod_ `check_rule(bot, event, state, stack=None, dependency_cache=None)`

- **说明**

  检查是否满足匹配规则

- **参数**

  - `bot: Bot`: Bot 对象

  - `event: Event`: 上报事件

  - `state: T_State`: 当前状态

- **返回**

  - `bool`: 是否满足匹配规则

### _classmethod_ `type_updater(func)`

- **说明**

  装饰一个函数来更改当前事件响应器的默认响应事件类型更新函数

- **参数**

  - `func: T_TypeUpdater`: 响应事件类型更新函数

### _classmethod_ `permission_updater(func)`

- **说明**

  装饰一个函数来更改当前事件响应器的默认会话权限更新函数

- **参数**

  - `func: T_PermissionUpdater`: 会话权限更新函数

### _classmethod_ `handle(parameterless=None)`

- **说明**

  装饰一个函数来向事件响应器直接添加一个处理函数

- **参数**

  - `parameterless: Optional[List[Any]]`: 非参数类型依赖列表

### _classmethod_ `receive(id='', parameterless=None)`

- **说明**

  装饰一个函数来指示 NoneBot 在接收用户新的一条消息后继续运行该函数

- **参数**

  - `id: str`: 消息 ID

  - `parameterless: Optional[List[Any]]`: 非参数类型依赖列表

### _classmethod_ `got(key, prompt=None, parameterless=None)`

- **说明**

  装饰一个函数来指示 NoneBot 当要获取的 `key` 不存在时接收用户新的一条消息并经过 `ArgsParser` 处理后再运行该函数，如果 `key` 已存在则直接继续运行

- **参数**

  - `key: str`: 参数名

  - `prompt: Optional[Union[str, Message, MessageSegment, MessageFormatter]]`: 在参数不存在时向用户发送的消息

  - `args_parser: Optional[T_ArgsParser]`: 可选参数解析函数，空则使用默认解析函数

  - `parameterless: Optional[List[Any]]`: 非参数类型依赖列表

### _async classmethod_ `send(message, **kwargs)`

- **说明**

  发送一条消息给当前交互用户

- **参数**

  - `message: Union[str, Message, MessageSegment]`: 消息内容

  - `**kwargs`: 其他传递给 `bot.send` 的参数，请参考对应 adapter 的 bot 对象 api

### _async classmethod_ `finish(message=None, **kwargs)`

- **说明**

  发送一条消息给当前交互用户并结束当前事件响应器

- **参数**

  - `message: Union[str, Message, MessageSegment, MessageTemplate]`: 消息内容

  - `**kwargs`: 其他传递给 `bot.send` 的参数，请参考对应 adapter 的 bot 对象 api

### _async classmethod_ `pause(prompt=None, **kwargs)`

- **说明**

  发送一条消息给当前交互用户并暂停事件响应器，在接收用户新的一条消息后继续下一个处理函数

- **参数**

  - `prompt: Union[str, Message, MessageSegment, MessageTemplate]`: 消息内容

  - `**kwargs`: 其他传递给 `bot.send` 的参数，请参考对应 adapter 的 bot 对象 api

### _async classmethod_ `reject(prompt=None, **kwargs)`

- **说明**

  最近使用 `got` / `receive` 接收的消息不符合预期，发送一条消息给当前交互用户并暂停事件响应器，
  在接收用户新的一条消息后继续当前处理函数

- **参数**

  - `prompt: Union[str, Message, MessageSegment, MessageTemplate]`: 消息内容

  - `**kwargs`: 其他传递给 `bot.send` 的参数，请参考对应 adapter 的 bot 对象 api

### _async classmethod_ `reject_arg(key, prompt=None, **kwargs)`

- **说明**

  最近使用 `got` 接收的消息不符合预期，发送一条消息给当前交互用户并暂停事件响应器，
  在接收用户新的一条消息后继续当前处理函数

- **参数**

  - `key: str`: 参数名

  - `prompt: Union[str, Message, MessageSegment, MessageTemplate]`: 消息内容

  - `**kwargs`: 其他传递给 `bot.send` 的参数，请参考对应 adapter 的 bot 对象 api

### _async classmethod_ `reject_receive(id='', prompt=None, **kwargs)`

- **说明**

  最近使用 `got` 接收的消息不符合预期，发送一条消息给当前交互用户并暂停事件响应器，
  在接收用户新的一条消息后继续当前处理函数

- **参数**

  - `id: str`: 消息 id

  - `prompt: Union[str, Message, MessageSegment, MessageTemplate]`: 消息内容

  - `**kwargs`: 其他传递给 `bot.send` 的参数，请参考对应 adapter 的 bot 对象 api

### `stop_propagation()`

- **说明**

  阻止事件传播
