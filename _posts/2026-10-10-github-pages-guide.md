---
layout: post
title: 用 GitHub Pages 免费搭建个人博客的完整流程
date: 2026-10-10
excerpt: 从零开始，只用 Git 和 GitHub CLI，把一个 Jekyll 模板变成你的博客。
tags:
  - 教程
---

如果你也想搭一个自己的博客，但不打算装一堆前端工具，这篇文章记录了我用 GitHub Pages 做这件事的完整流程。

## 前提条件

只需要两样东西：

1. **Git** — 版本控制工具
2. **GitHub CLI (gh)** — 用来在命令行里操作 GitHub

不需要安装 Node.js、npm、Ruby 或 Jekyll。构建过程在 GitHub 的服务器上完成。

## 核心流程

```
本地写 Markdown 文章
      ↓
git push 到 GitHub 仓库
      ↓
GitHub Actions 自动运行 Jekyll
      ↓
Markdown 被编译成 HTML
      ↓
发布到 GitHub Pages URL
```

## 关键步骤

### 1. 克隆模板

找一个 Jekyll 模板仓库，克隆到本地。模板里已经配好了 Jekyll 需要的 `_config.yml`、`_layouts/` 和 GitHub Actions workflow。

### 2. 修改个人信息

编辑 `_config.yml` 改标题和描述，编辑 `index.html` 改首页内容，编辑 `about.md` 改关于页。配色在 `assets/style.css` 的 `:root` 变量里。

### 3. 写文章

在 `_posts/` 文件夹里新建文件，文件名格式是 `YYYY-MM-DD-title.md`。开头保留 Front Matter：

```yaml
---
layout: post
title: 文章标题
date: 2026-10-10
excerpt: 一句话摘要
tags:
  - 标签
---
```

下面直接写 Markdown 正文。

### 4. 创建仓库并推送

用 GitHub CLI 创建远程仓库，然后把代码推上去：

```bash
gh repo create 你的用户名.github.io --public --source=. --push
```

### 5. 启用 GitHub Pages

进入仓库的 Settings → Pages，把 Source 设为 GitHub Actions。之后每次 push 到 main 分支，网站都会自动重新生成。

## 为什么不用其他方案

| 方案 | 需要安装 | 费用 |
|------|---------|------|
| GitHub Pages + Jekyll | Git + gh | 免费 |
| Hexo | Node.js + npm | 免费 |
| Next.js | Node.js + npm | 需要 Vercel |
| WordPress | PHP + MySQL | 需要服务器 |

GitHub Pages 的优势是：零安装、零费用、零维护。你只需要写 Markdown，剩下的事情 GitHub 帮你做。
