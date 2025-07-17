---
abbrlink: BookNav
ai: null
aplayer: null
aside: null
background: '#fff'
categories:
- - GitHub
- - 个人项目
- - telegram
- - cloudflare
comments: null
copyright: null
copyright_author: null
copyright_author_href: null
copyright_info: null
copyright_url: null
cover: https://tc-212.pages.dev/1744458795826.png
date: '2025-04-25T23:16:59.007959+08:00'
description: 让虚拟主机“物尽其用”，一劳永逸！防止吃灰。
highlight_shrink: null
katex: null
keywords: 书签导航,书签,导航,虚拟主机,防止吃灰,阿伟,阿伟,阿伟博客,阿伟个人,阿伟主页,cf,cloudflare,tg,telegram,私聊,机器人,tg双向机器人,
mathjax: null
share: true
swiper_index: 10
tags:
- GitHub
- 个人项目
- telegram
- cloudflare
- BookNav
- 书签导航
- 导航站
title: BookNav - 轻量级导航类似OneNav，避免免费虚拟主机吃灰
toc: null
toc_number: null
toc_style_simple: null
top: null
top_group_index: 10
top_img: null
updated: '2025-04-25T23:16:59.779+08:00'
url_name: BookNav
---
# BookNav - 网页收藏夹，随时随地访问

---

🔗 **项目地址**: [BookNav](https://github.com/iawooo/BookNav)
-------------------------------------------------------------

# 项目截图

![BookNav](https://tc-212.pages.dev/1744458795826.png)

# 项目演示站 https://cc.ct8.pl/  密码：admin）（数据库设置了只读）

## ✨ 前言：为什么选择 BookNav？

市面上虽有许多免费虚拟主机，但它们往往伴随着各种限制：空间不足、数据库受限、带宽瓶颈、点击量上限，甚至强制插入广告。如果您想部署个人网站或博客，稍有流量便可能不堪重负。这时，部署一个轻量级的导航工具作为您的网页收藏夹，不仅能满足日常需求，还能让虚拟主机“物尽其用”，一劳永逸！

许多免费虚拟主机以稳定性著称，例如：

- 🌐 [Freehostia](https://www.freehostia.com/)（据称已稳定运行超20年）
- 🌐 [InfinityFree](https://www.infinityfree.com/)（稳定运营十余年）
- 🌐 serv00和ct8
  BookNav 完美适配这些平台，部署后即可作为您的私人收藏夹，免去频繁维护的烦恼。当然，您也可以选择 Vercel 部署，或者将其打造为一个开放式导航站——简单灵活，支持 VPS，满足多样化需求。

---

## 🚀 部署教程：三步打造您的专属收藏夹

### 1. 下载源代码

从 [GitHub 项目地址](https://github.com/iawooo/BookNav) 下载 BookNav 的最新源代码。

### 2. 上传到虚拟主机

文件结构一览：

```
public_html/
  ├── add.php              # 添加书签的入口
  ├── backup.php           # 备份与恢复功能
  ├── config.php           # 核心配置文件
  ├── delete.php           # 删除书签脚本
  ├── delete_category.php  # 删除分类脚本
  ├── edit.php             # 编辑书签页面
  ├── edit_category.php    # 编辑分类页面
  ├── index.php            # 主页入口
  ├── install.php          # 一键安装页面
  ├── login.php            # 登录页面
  ├── script.js            # 前端交互（拖拽、樱花特效等）
  ├── style.css            # 样式文件
  ├── images/              # 默认图标与 favicon
  │   ├── default-bookmark.png
  │   └── favicon.ico


```

2. 上传：
   - 使用 FTP 工具（如 FileZilla）将整个文件夹上传到虚拟主机的 public_html 或指定目录。
   - 例如，上传到 /public_html/

### 3. 访问站点

- 在浏览器中访问：
  http://yourdomain.com/
- 填写配置数据库信息，绑定数据库
- 点击“安装”，系统会自动创建 config.inc.php 和 bookmarks 表。
- 登录后即可开始添加和管理书签！
-

## 亮点

- **超轻量级**：源代码不到 100KB，占用空间小，加载快。
- **简单部署**：只需 PHP 和 MySQL，无需额外依赖，虚拟主机即可运行。
- **灵感来源 OneNav**：继承了 OneNav 的简洁设计，同时优化了功能和用户体验。
- **高级图标抓取**：自动从网页提取最佳图标（支持 `favicon.ico`、HTML 链接、Manifest 等）。
- **书签管理**：添加、编辑、删除书签，支持名称、URL、分类、图标和备注。
- **拖拽排序**：支持多级分类，分类权重可调，拖拽调整书签顺序。
- **明暗主题**：内置炫酷的渐变背景，支持一键切换明暗模式。
- **樱花特效**：动态樱花飘落效果，提升视觉体验。
- **备份与恢复**：导出书签数据为 JSON 文件，或从备份文件导入，支持清空现有数据。
- **密码保护**：简单登录机制，确保书签隐私。
- **响应式设计**：适配桌面和移动端，随时随地管理书签。
- **搜索功能**：快速搜索书签名称、URL、分类或备注。

## 主要功能

1. **书签管理**：

   - 添加、编辑、删除书签。
   - 支持分类管理（新建、修改、删除分类）。
   - 可添加备注，方便记录额外信息。
   - 权重调整，实时保存，多端访问
2. **图标自动抓取**：

   - 优先检查默认 `favicon.ico`。
   - 解析 HTML 中的 `<link>` 标签（如 `rel="icon"` 或 `apple-touch-icon`）。
   - 支持 Web App Manifest 和 Microsoft `browserconfig.xml`。
   - 使用 CORS 代理（如 `api.allorigins.win`）确保跨域抓取成功。
   - 回退到 Google FaviconV2 服务。
3. **用户体验**：

   - 拖拽排序书签，实时保存顺序。
   - 右键或长按书签显示编辑/删除选项。
   - 动态调整书签文本大小，确保显示完整。
4. **视觉设计**：

   - 渐变背景（明暗主题可选）。
   - 半透明容器和阴影效果。
   - 樱花飘落动画，提升趣味性。
5. **备份与恢复**：

   - 一键将所有书签和分类数据导出为 JSON 文件，文件名包含日期（如 bookmarks_backup_2025-03-19.json）。
   - 上传 JSON 文件恢复数据，可选择清空现有数据后再导入。
6. **密码保护**：

   - 可选密码：安装时可设置网站访问密码，留空则无需密码。
   - 安全登录：使用 Session 和安全的 Cookie（HttpOnly）管理登录状态，30 天有效。
   - 自动登录：若未设置密码，系统默认允许直接访问。

## 🌸 让收藏更美好

BookNav 不仅仅是一个工具，更是一种体验。无论是作为私人收藏夹，还是开放式导航站，它都能为您带来高效、优雅的管理方式。现在就试试 BookNav，让您的网页收藏之旅更加精彩！
