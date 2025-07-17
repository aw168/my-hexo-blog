---
abbrlink: cftc
ai: null
aplayer: null
aside: null
background: '#fff'
categories:
- - 个人项目
- - 图床搭建
- - telegram
- - GitHub
- - cloudflare
comments: null
copyright: null
copyright_author: null
copyright_author_href: null
copyright_info: null
copyright_url: null
cover: https://awtc.pages.dev/web.png
date: '2025-04-16T23:05:45.403380+08:00'
description: 阿伟,阿伟,阿伟博客,阿伟个人,阿伟主页,cf,cloudflare,tg,telegram,私聊,机器人,tg双向机器人,
highlight_shrink: null
katex: null
keywords: 图床，图床搭建，cloudflare图床，telegram图床，免费图床，阿伟,阿伟,阿伟博客,阿伟个人,阿伟主页,cf,cloudflare,tg,telegram,私聊,机器人,tg双向机器人,
mathjax: null
share: true
swiper_index: 10
tags:
- 图床搭建
- 图床
- 个人项目
- GitHub
- telegram
- cloudflare
title: '[cftc]-基于cloudflare图床,支持tg机器人面板和网页管理,上传,自定义后缀等'
toc: null
toc_number: null
toc_style_simple: null
top: null
top_group_index: 10
top_img: null
updated: '2025-07-17T23:16:16.786+08:00'
url_name: cftc
---
# [cftc](https://github.com/iawooo/cftc/) 支持telegram机器人管理和网页管理文件（包括上传，删除，分类，修改后缀等功能）

## [cftc](https://github.com/iawooo/cftc/) 支持R2 telegram存储，多多star后期可能会跟进B2 S3等存储

# 项目地址：https://github.com/iawooo/cftc/ 感谢你们的star助力孩子圆梦论坛鸡

## 📸 截图


| Telegram 交互                                    | 网页管理                                    |
| ------------------------------------------------ | ------------------------------------------- |
| ![Telegram 交互](https://awtc.pages.dev/bot.png) | ![网页管理](https://awtc.pages.dev/web.png) |

## ✨ 核心特性

- **与 [CTT](https://github.com/iawooo/ctt) 项目协同，实现一举两得**

  - **提升整体效率**：与  [CTT](https://github.com/iawooo/ctt)  项目无缝协作，共享 Telegram 生态的优势。群组中用户既能享受 CTT 的消息转发功能，又能把群组当存储，最大化 Telegram 群组的价值。（不能共用一个机器人）
- **Telegram 机器人驱动的智能管理**

  - **随时随地操作**：内置 Telegram 机器人提供直观的菜单面板，支持上传、修改后缀、管理和分类文件等功能。用户通过简单按钮即可完成复杂操作，无需专业技能，管理文件如同聊天般轻松。
- **永久直链的革命性体验**

  - **提升用户体验**：通过先删除旧文件、上传新文件并修改直链后缀为旧后缀。用户可以在不更改链接的情况下频繁更新文件内容（如替换照片或文档），特别适合博客、电商或需要稳定链接的场景。
- **Cloudflare workers/pages部署**

  - **快速上手**：代码简单，部署代码，填写变量便能使用。
  - **免费永久稳定的图床服务**  Cloudflare 的业界领先稳定性，一旦部署，文件托管长期可靠，无需担心服务中断或数据丢失，一劳永逸，节省维护精力。
- **Cloudflare D1 数据库**

  - **高效存储**：使用Cloudflare D1这个根本用不完的数据库存储用户设置和文件元数据，避免用kv这个少得可怜还造成动不动扣费的现象。
- **利用 Telegram 群组的无限免费存储**

  - **零成本存储**：利用 Telegram 群组作为免费存储后端，空间近乎无限，成本为零。用户无需额外付费即可托管图片、视频和文档，轻松实现高性价比的图床。
- **灵活的双存储模式**

  - **灵活适配，覆盖广泛**：支持 Telegram 存储和 Cloudflare R2 存储两种模式，用户可根据需求自由切换。Telegram 模式适合轻量文件，R2 模式支持大文件和高性能，满足从个人分享到企业托管的多种场景。
- **动态直链后缀修改**

  - **直链可复用**：cftc 允许用户随时修改文件直链的后缀，无需更改文件内容即可生成新链接。改变了传统图床“修改内容必须更换直链”的限制，实现动态化管理。

## 部署教程

大佬部署可以直接看变量表

#### 准备工作

**创建Telegram Bot**（获取`TG_BOT_TOKEN`变量）：

- 在Telegram中找到`@BotFather`，发送`/newbot`创建新机器人。
- 按照提示设置机器人名称和用户名，获取Bot Token（例如`123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`）。
  **创建后台群组**（获取`TG_STORAGE_CHAT_ID`变量）：
  **可与[CTT](https://github.com/iawooo/ctt) 项目共用群组如果部署过[CTT](https://github.com/iawooo/ctt) 项目，此步骤省略**
- 创建一个Telegram群组（按需设置是否公开），
- 添加机器人为管理员。
- 获取群组的Chat ID（例如`-100123456789`），可以通过`@getidsbot`获取（拉它进群）。
  ![step 1](https://awtc.pages.dev/1.png)
  ![step 2](https://awtc.pages.dev/2.png)

#### 创建D1 SQL数据库（获取`DATABASE`变量）

1. 登录[Cloudflare仪表板](https://dash.cloudflare.com/)。
2. 导航到 **存储和数据库 > D1 SQL数据库**，输入一个名称（例如`cftc`），点击 **创建**。
   ![step 3](https://awtc.pages.dev/3.png)
   ![step 4](https://awtc.pages.dev/4.png)

#### 创建R2存储桶（获取`BUCKET`变量）<可选>

- 绑卡后，创建创建一个存储桶

### 部署到Cloudflare pages (推荐：pages.dev域名中国也能访问)

### *点个star，frok[本项目](https://github.com/iawooo/cftc/)**

#### 创建pages项目

1. 登录[Cloudflare仪表板](https://dash.cloudflare.com/)。
2. 导航到 **Workers和Pages > Workers和Pages**，点击 **创建**。
   ![step 5](https://awtc.pages.dev/5.png)
3. 点击 **Pages**，再点击 **连接到Git**
   ![step 6](https://awtc.pages.dev/6.png)
4. 选择 **cftc** 存储库，点击**开始设置**，输入项目名称（例如`cftc`）
   ![step 7](https://awtc.pages.dev/7.png)
   ![step 8](https://awtc.pages.dev/8.png)
5. 点击 **保存并部署**，等待20秒左右，点击 **继续处理项目**
6. 点击**设置**，根据**变量表**添加或绑定变量，确保变量正确。
   ![step 9](https://awtc.pages.dev/9.png)
   以下是项目中需要在 Cloudflare 环境中绑定的变量及其说明：
   - **`TG_STORAGE_CHAT_ID`说明：如果你部署过[CTT](https://github.com/iawooo/ctt) 项目则`TG_STORAGE_CHAT_ID`可与[CTT](https://github.com/iawooo/ctt) 项目中的`GROUP_ID_ENV`相同，有且只有群组id变量能相同，共用群组，不影响[CTT](https://github.com/iawooo/ctt) 项目的双向机器人。**
   - **`DOMAIN`说明：推荐填写cloud flare给你项目的域名如：`yourdomain.pages.dev`这样的图床直链做到“人走图还在”（cf不倒闭）**


| **变量名**           | **类型** | **描述**                                                                                | **默认值/示例**                |
| -------------------- | -------- | --------------------------------------------------------------------------------------- | ------------------------------ |
| `DATABASE`           | D1 绑定  | **(必需)** Cloudflare D1 数据库绑定名称，用于存储文件元数据、用户设置和分类信息。       | `cftc-db`                      |
| `DOMAIN`             | 环境变量 | **(必需)** Cloudflare Workers/pages 部署域名，用于生成文件直链和设置 Telegram Webhook。 | `yourdomain.workers/pages.dev` |
| `TG_BOT_TOKEN`       | 环境变量 | **(必需)** Telegram 机器人 Token，用于与 Telegram API 通信以处理文件上传和交互。        | `123456:ABC-DEF1234ghIkl`      |
| `TG_STORAGE_CHAT_ID` | 环境变量 | **(必需，如果使用 Telegram 存储)** 用于存储文件的 Telegram 群组或频道 ID。              | `-100123456789`                |
| `USERNAME`           | 环境变量 | **(必需，如果 `ENABLE_AUTH` 为 `true`)** 管理面板的登录用户名。                         | `admin`                        |
| `PASSWORD`           | 环境变量 | **(必需，如果 `ENABLE_AUTH` 为 `true`)** 管理面板的登录密码。                           | `your_secure_password`         |
| `MAX_SIZE_MB`        | 环境变量 | **(可选)** 单个文件的最大大小限制（单位 MB），防止上传过大文件。                        | `20`                           |
| `BUCKET`             | R2 绑定  | **(可选)** Cloudflare R2 存储桶绑定名称，用于 R2 存储模式（若启用）。                   | `cftc-bucket`                  |
| `COOKIE`             | 环境变量 | **(可选)** 网页认证 Cookie 的有效期（单位天），控制登录会话时长。                       | `7`                            |
| `TG_CHAT_ID`         | 环境变量 | **(可选)** 允许使用机器人的 Telegram 用户（英文逗号分隔），限制访问权限。               | `123456789,987654321`          |
| `ENABLE_AUTH`        | 环境变量 | **(可选)** 是否启用网页管理界面的用户名/密码认证（`true` 或 `false`）。                 | `true`                         |

7. 点击**部署**，找到**重试部署**，点击**重试部署**
   ![step 10](https://awtc.pages.dev/10.png)

### 部署到Cloudflare Workers （替换代码填变量）

这里不做说明详细请移步https://github.com/iawooo/cftc

## 🛠️ 使用说明

* **网页界面**:
  * 访问 Worker/pages 的 URL (例如 `https://cftc.workers/pages.dev/` 或你的自定义域名)。
  * `https://cftc.workers/pages.dev/admin`: 文件管理后台，可查看、搜索、筛选、分享、删除文件和管理分类。
* **Telegram Bot**:
  * 私聊你的 Bot 发送 `/start` 开始交互。
  * 直接发送图片、视频、文档等文件给 Bot 进行上传。
  * 使用 Bot 提供的内联键盘按钮进行各种操作（切换存储、管理分类、查看文件、修改后缀、删除文件等）。
  * 按照 Bot 的提示回复消息以完成特定操作（如输入新分类名称、要删除的文件名、新后缀等）。

## 🤝 贡献

### 欢迎到[GitHub](https://github.com/iawooo/cftc)提交 Issue 或 Pull Request！如果您有任何改进建议或新功能需求，请随时联系我。

## 🌟 致谢

### 感谢所有测试者、贡献者和社区支持！

### [cloud flare](https://www.cloudflare.com/) - 提供强大的基础设施支持。

### [telegram](https://telegram.org/) - 便捷的 Bot API。

### 感谢 [xAI](https://x.ai/)   [claude](https://claude.ai/) 帮助我完成了本项目的开发和优化

## 声明

- **尊重原创，转载须知**
  如需转载，请务必注明出处，感谢支持！严禁将本项目用于任何违法犯罪行为。
- **二次修改与发布**
  欢迎基于本项目进行二次开发，但请在发布时注明原始出处，共同维护开源社区的良好氛围。
