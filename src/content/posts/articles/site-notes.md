---
title: "网站维护备忘"
description: "记录如何发布博客，以及修改主页、About 页面和站点信息。"
pubDatetime: 2026-07-18T00:00:00+08:00
tags:
  - 备忘
---

## 写一篇新博客

在 `src/content/posts/articles/` 中新建一个 Markdown 文件，例如 `my-new-post.md`：

```md
---
title: "文章标题"
description: "一两句话的文章摘要。"
pubDatetime: 2026-07-18T12:00:00+08:00
tags:
  - 学习
featured: false
draft: false
---

从这里开始写正文。
```

- `title` 是文章标题。
- `description` 会显示在首页与文章列表的卡片中。
- `tags` 可以写一个或多个标签。
- `featured: true` 会让文章出现在首页的 Featured 区域。
- `draft: true` 表示草稿，不会被发布。

## 修改主页内容

主页文件是 `src/pages/index.astro`。

这里主要控制首屏的姓名、简介，以及 Featured 和 Recent Posts 的展示方式。一般不需要改动卡片样式；新增博客后，首页会自动读取文章的标题、日期和摘要。

## 修改 About 页面

About 内容位于 `src/content/pages/about.md`。

直接编辑其中的 Markdown 即可，例如补充教育经历、个人简介、研究兴趣或获奖信息。修改后会自动显示在 `/about/` 页面。

## 修改站点信息与社交链接

站点名称、描述、GitHub、邮箱和微信链接都在 `astro-paper.config.ts` 中。

修改配置时请保留原有格式。社交链接的图标名称需要对应 `src/assets/icons/socials/` 中的 SVG 文件名。

## 本地预览与发布

在项目根目录运行：

```powershell
pnpm.cmd dev
```

确认无误后，依次执行：

```powershell
pnpm.cmd build
git add .
git commit -m "Update site content"
git push origin main
```

推送到 GitHub 后，GitHub Pages 会自动重新部署。
