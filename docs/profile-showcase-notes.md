# Profile 展示方案维护笔记

这份文档记录 `README.md` 中当前使用的展示组件，方便后续替换、排查裂图、或继续调研更稳定的方案。

## 首屏入口卡片

当前方案：使用 `shields.io` 静态徽章作为入口卡片。

保留 4 个入口：

- `Portfolio`：作品集与主页，指向 Netlify 作品集。
- `Demo Gallery`：演示作品与实验，指向 README 内的 `#演示-demo`。
- `Share Stack`：技术文章与工作流，指向 GitHub Pages 分享站。
- `Learning Stack`：学习路线与项目复盘，指向学习仓库。

维护建议：

- 优先使用静态徽章作为关键入口，稳定性高于动态卡片。
- 入口不要在 README 中重复出现，避免首屏、快速入口、Demo 区域互相抢重点。
- `shields.io` 的中文文案可以直接放在 badge path 中；复杂符号建议 URL encode。

## Typing SVG

当前方案：使用 `readme-typing-svg.herokuapp.com` 展示首屏动态短句。

当前文案方向：

- 作品集 / 交互 / Demo
- 分享站 / 笔记 / 复盘
- 学习仓库 / 路线 / 实践

维护建议：

- Typing SVG 只负责氛围，不承载关键导航。
- 文案尽量短，避免移动端溢出。
- 如果服务不稳定，可以直接删除这一行，不影响 README 信息结构。

## 演示 Demo 图片

当前方案：使用 `raw.githubusercontent.com` 读取 `learning_stack` 中已有图片。

维护建议：

- 图片已统一 `width="48%" height="220"`，并通过 `object-fit: cover` 保持网格整齐。
- 更稳定的长期方案是在 profile 仓库中维护 `assets/demo-*.png`，避免学习仓库路径调整导致裂图。
- 每张图外层使用 `<a>`，点击跳到对应 Demo 或源码目录。

## 贪吃蛇热力图

当前方案：使用 `Platane/snk` GitHub Action 生成贡献图 SVG，并发布到 `output` 分支。

README 引用：

- 浅色：`https://raw.githubusercontent.com/juemuel/juemuel/output/github-contribution-grid-snake.svg`
- 深色：`https://raw.githubusercontent.com/juemuel/juemuel/output/github-contribution-grid-snake-dark.svg`

Workflow：`.github/workflows/snake.yml`

维护建议：

- Push 后可以在 GitHub Actions 手动运行 `Generate contribution snake` 立即刷新。
- 日常由 schedule 自动刷新。
- 如果图片裂开，优先检查 `output` 分支是否存在、SVG 是否生成成功、Actions 是否有权限写入 `contents: write`。

## GitHub 动态统计

当前 README 仍使用：

- `github-readme-stats.vercel.app/api`
- `github-readme-stats.vercel.app/api/top-langs`
- `github-readme-activity-graph.vercel.app/graph`

维护建议：

- `github-readme-stats` 的公开 Vercel 服务可能因限流或维护状态不稳定。关键入口不要依赖它。
- 如果统计图也开始裂图，可考虑：
  - 删除统计卡片，仅保留蛇形热力图和 Activity Graph。
  - 自部署 stats 服务。
  - 改成 `shields.io` 静态徽章或 GitHub Actions 生成静态 SVG。