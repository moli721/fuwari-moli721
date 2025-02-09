---
title: Nonebot2——QQ机器人搭建教程-Linux篇
published: 2025-02-09
description: '本文详细介绍如何在 Linux 系统（以 Ubuntu 为例）上搭建 Nonebot2 QQ机器人，包括环境配置、依赖安装和常见问题解决方案。'
image: ''
tags: ['Nonebot2', 'Linux', 'QQ机器人', 'Ubuntu']
category: 'QQ机器人'
draft: false 
lang: 'zh-CN'
---

# Linux 环境下的 Nonebot2 QQ机器人搭建指南

> 本文是 Nonebot2 教程系列的 Linux 篇，主要介绍如何在 Linux 系统上配置和部署 QQ 机器人。

## 一、框架安装

### 1. 安装 NapCat
推荐使用 Docker 方式安装 NapCat，具体步骤请参考[官方文档](https://napneko.github.io/)。安装完成后，按照[框架接入指南](https://napneko.github.io/use/integration)完成配置。

### 2. 环境迁移准备
如果你已在本地环境调试好机器人，可以通过复制以下文件到服务器来快速部署：
- `src` 文件夹
- `pyproject.toml`
- `poetry.lock`

## 二、Python 环境配置

在 Ubuntu 系统上安装 Python 3.10.11 的详细步骤：

### 1. 系统更新
   先更新一下包管理器的包列表，确保系统是最新的：
   ```bash
   sudo apt update
   ```

### 2. 安装必要依赖
   安装编译 Python 需要的一些工具和库：
   ```bash
   sudo apt install -y software-properties-common
   sudo apt install -y build-essential libssl-dev zlib1g-dev libbz2-dev \
   libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev \
   libffi-dev liblzma-dev python3-openssl git
   ```

### 3. 添加 Python PPA
   使用 Python 官方的 PPA 仓库来安装特定版本的 Python：
   ```bash
   sudo add-apt-repository ppa:deadsnakes/ppa
   sudo apt update
   ```

### 4. 安装 Python 3.10
   安装 Python 3.10.12：
   ```bash
   sudo apt install python3.10
   ```

### 5. 配置 pip
   安装 Python 包管理工具 `pip`：
   ```bash
   sudo apt install python3.10-distutils
   wget https://bootstrap.pypa.io/get-pip.py
   sudo python3.10 get-pip.py
   ```

### 6. 验证安装
   最后，检查 Python 版本，确保安装成功：
   ```bash
   python3.10 --version
   ```


> 💡 如果显示 `Python 3.10.11`，则表示安装成功。

## 三、项目依赖管理

完成 Python 安装后，需要创建项目结构并安装依赖：

1. 创建 Nonebot 项目目录
2. 复制之前准备的文件到相应位置
3. 创建并激活虚拟环境
4. 使用 Poetry 安装依赖

> ⚠️ 如果在安装依赖时遇到超时问题，可以考虑配置代理。

## 四、配置网络代理

### 1. 安装和配置 Clash
推荐参考[详细教程](https://www.fuxi.info/archives/273)配置 Clash 代理。配置完成后，可以使用以下命令控制 Clash：

```bash
systemctl start clash # 启动代理
systemctl stop clash # 停止代理
```

### 2. 代理相关命令
```bash
查看当前代理设置
echo $http_proxy
echo $https_proxy

临时关闭代理
unset http_proxy https_proxy all_proxy
```

### 3. SSL 错误解决
如果遇到 SSL 错误：`error:0a000126:ssl routines::unexpected eof while reading`，可以参考[这篇文章](https://blog.csdn.net/youcharming/article/details/140181774)解决。

## 常见问题与解决方案

1. Poetry 安装超时
   - 配置国内镜像源
   - 使用代理
   - 增加超时时间

2. 依赖安装失败
   - 检查 Python 版本兼容性
   - 确认系统依赖是否完整
   - 查看错误日志定位具体问题

3. 网络连接问题
   - 验证代理配置
   - 检查防火墙设置
   - 确认端口是否开放

> 🔍 遇到问题时，建议先查看 Nonebot2 的[官方文档](https://v2.nonebot.dev/)和[问题解答](https://v2.nonebot.dev/docs/tutorial/troubleshooting)。

