---
sidebar_position: 1
description: 通过脚手架, pip 安装驱动器
---

# 安装驱动器

NoneBot 在默认安装情况下内置了 `fastapi` 服务端驱动器，其他驱动器如 `httpx`, `aiohttp` 则需要额外安装。

## 查看

前往 [商店](/store) 即可查看所有驱动器。

或者使用 `nb-cli` 命令行查看：

```bash
nb driver list
```

## 安装

前往 [商店](/store) 点击复制 `nb-cli` 安装命令至命令行执行即可安装。

或者自行输入命令安装：

```bash
nb driver install <driver-name>
```

或者使用交互模式安装：

```bash
nb driver install
```

也可以使用 `pip` 安装

```bash
pip install <driver-name>
```

<!-- TODO: asciinema for install driver -->
