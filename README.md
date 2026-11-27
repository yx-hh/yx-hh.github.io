# yx-hh.github.io

## 发一篇新博客

1. 复制 `_drafts/_TEMPLATE.md`（或改 `_drafts/` 里现成的草稿）
2. 改好后放进 `_posts/`，文件名必须是 `YYYY-MM-DD-英文短标题.md`，例如 `_posts/2026-12-01-idempotent-payout-path.md`
3. commit + push。GitHub Pages 约 1 分钟后自动生成，文章出现在 `/blog/`，首页 "Latest Writing" 显示最新 3 篇

- `_drafts/` 里的文件不会发布，可以放未写完的稿子
- 文章开头 `---` 之间的 front matter 必填 `title`；`description` 是列表页的一句话简介；`tags` 可选
- 日期取自文件名，列表按日期倒序排列
- 支持标准 Markdown：标题、列表、表格、代码块、引用、图片（图片放 `assets/img/`，用 `![说明](/assets/img/xx.png)` 引用）

## 目录

- `index.html` 首页（Skills / Projects / Experience / Latest Writing / Contact）
- `blog/index.html` 博客列表页
- `_layouts/` 页面模板，`assets/css/style.css` 全站样式
