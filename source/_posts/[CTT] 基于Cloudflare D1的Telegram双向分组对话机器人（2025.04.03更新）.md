---
abbrlink: CTT
categories:
- - GitHub
- - 个人项目
- - telegram
- - cloudflare
date: '2025-03-25T14:44:55.269722+08:00'
description: 阿伟,阿伟,阿伟博客,阿伟个人,阿伟主页,cf,cloudflare,tg,telegram,私聊,机器人,tg双向机器人,
tags:
- GitHub
- 个人项目
- telegram
- cloudflare
title: '[CTT] 基于Cloudflare D1的Telegram双向分组对话机器人（2025.04.03更新）'
updated: '2025-03-25T14:44:55.830+08:00'
share: true
---
# CFTeleTrans (CTT) - 基于 Cloudflare 的 Telegram 消息转发分组对话机器人 本项目地址：[CFTeleTrans](https://github.com/iawooo/ctt) 欢迎fork 期待star

# 部署双向机器人的好处：隐私保护，避免封号，任何人能联系你（不受双向限制）

## 04.03更新：修复bug，结合反馈添加功能，添加面板，优化响应速度。

## 项目截图

以下是 CFTeleTrans 项目的截图：
![CFTeleTrans 截图](https://tc-212.pages.dev/1743001600418.png)
一款强大、灵活、低成本的 Telegram 机器人解决方案，助你轻松管理消息互动！以下是它的核心亮点：

- **完全自部署，掌控在你手中**
  部署在自己的 Cloudflare 账户下，避免被第三方操控或推送流氓广告，安全可靠，隐私无忧。
- **分组对话，清晰高效**
  每个给你发消息的人自动分配独立分组，查找记录一目了然，回复无需“@”提及，直接在对应分组操作，省时省力。
- **好友式聊天体验，随时畅聊**
  用户发消息就像添加了你的好友，随时随地想聊就聊。即使多人同时发消息，也井然有序，绝不混乱。
- **纯 Cloudflare 驱动，零服务器成本**
  完全基于 Cloudflare 平台，利用其免费额度（每天10万次请求）实现高性能运行，无需额外服务器，轻松上手。
- **D1 数据库存储，容量无忧**
  使用 Cloudflare D1 存储用户状态和数据，免费额度高达每天10万次读写，远超传统 KV 空间限制，稳定又实用。
- **智能防护与管理功能**
  配备高效的用户验证机制、消息频率限制（防止恶意刷消息）以及管理员功能，确保机器人安全稳定运行。
- **更多功能，等你探索**
  想了解更多 欢迎访问 GitHub 项目地址：[https://github.com/iawooo/ctt](https://github.com/iawooo/ctt)，完整功能一览无余！

---

# 部署教程

## 准备工作

1. **创建Telegram Bot**：

   - 在Telegram中找到 `@BotFather`，发送 `/newbot`创建新机器人。
   - 按照提示设置机器人名称和用户名，获取Bot Token（例如 `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`）。
   - 发送 `/setinline`切换内联模式。
     ![image](https://tc-212.pages.dev/1742897391924.png)
2. **创建后台群组**：

   - 创建一个Telegram群组（按需设置是否公开），
   - 群组的“话题功能”打开。
   - 添加机器人为管理员，建议权限全给（消息管理，话题管理）
     ![image](https://tc-212.pages.dev/1742897456559.png)
   - 获取群组的Chat ID（例如 `-100123456789`），可以通过 `@getidsbot`获取（拉它进群）。
     ![image](https://tc-212.pages.dev/1742897487893.png)

## 部署到Cloudflare Workers

### 步骤 1：创建D1 SQL数据库

1. 登录[Cloudflare仪表板](https://dash.cloudflare.com/)。
2. 导航到 **存储和数据库 > D1 SQL数据库**，输入一个名称（例如 `cfteletrans-db`），点击 **创建**。
   ![image](https://tc-212.pages.dev/1742897504981.png)
   ![image](https://tc-212.pages.dev/1742897530332.png)

### 步骤 2：创建Workers项目

1. 登录[Cloudflare仪表板](https://dash.cloudflare.com/)。
2. 导航到 **Workers和Pages > Workers和Pages**，点击 **创建**。
   ![image](https://tc-212.pages.dev/1742897572684.png)
3. 点击 **Hello world**，输入一个名称（例如 `cfteletrans`），再点击 **部署**
4. 点击 **继续处理项目**，（先填写变量再替换项目代码）

### 步骤 3：配置环境变量

1. 在创建的Workers项目 **设置 > 变量和机密** 中，添加以下变量：

- `BOT_TOKEN_ENV`：您的Telegram Bot Token（例如 `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`）。
- `GROUP_ID_ENV`：后台群组的Chat ID（例如 `-100123456789`）。
- `MAX_MESSAGES_PER_MINUTE_ENV`：消息频率限制（例如 `40`）。

### 步骤 4：绑定D1 SQL数据库

1. 在创建的Workers项目 **设置 > 绑定** 中，绑定数据库：

- 添加-选择D1数据库
- 变量名称 `D1`
- D1 数据库 选择刚建的数据库（例如 `cfteletrans-db`），
- 点击 **编辑代码**，把原来的代码用[本项目](https://github.com/iawooo/ctt)中的_worker.js代码替换后部署

| **变量名**                | **类型** | **描述**                                                   | **默认值/示例**       |
| ------------------------------- | -------------- | ---------------------------------------------------------------- | --------------------------- |
| `BOT_TOKEN_ENV`               | 环境变量       | Telegram Bot 的 Token，用于与 Telegram API 通信。                | `your-telegram-bot-token` |
| `GROUP_ID_ENV`                | 环境变量       | Telegram 群组的 ID，用于消息转发和客服回复。                     | `-123456789`              |
| `MAX_MESSAGES_PER_MINUTE_ENV` | 环境变量       | 每分钟允许的最大消息数，用于限制用户发送频率。                   | `40`                      |
| `D1`                          | D1 绑定        | Cloudflare D1 数据库绑定，用于存储用户状态、消息频率和群组映射。 | `cfteletrans-db`          |

![image](https://tc-212.pages.dev/1742897645328.png)

### 步骤 5：测试

1. 在Telegram中找到您的机器人，发送 `/start`。
2. 确认收到“你好，欢迎使用私聊机器人！”并触发验证码。
3. 完成验证，确认收到合并消息，例如：
4. 发送消息，确认消息转发到后台群组的子论坛。

## 部署到Cloudflare pages（可选）

### **首先fork[本项目](https://github.com/iawooo/ctt)**！！！

### 步骤 1：创建pages项目

1. 登录[Cloudflare仪表板](https://dash.cloudflare.com/)。
2. 导航到 **Workers和Pages > Workers和Pages**，选择pages，点击 **创建**。
3. 连接GitHub部署（或者下载本项目zip部署）

### 步骤 2：填写变量后重试部署

![image](https://tc-212.pages.dev/1742897645328.png)

## 说明

- 本项目首次公测，可能有bug，
- bug和改进建议联系我

## 致谢

- 特别感谢 [xAI](https://x.ai/) 提供的支持，帮助我完成了本项目的开发和优化
- 特别感谢 [cloud flare](https://www.cloudflare.com/) 大善人

## 声明

- **尊重原创，转载须知**
  如需转载，请务必注明出处，感谢支持！严禁将本项目用于任何违法犯罪行为。
- **二次修改与发布**
  欢迎基于本项目进行二次开发，但请在发布时注明原始出处，共同维护开源社区的良好氛围。
