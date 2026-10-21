# 顽石智护网站 · 项目操作注意事项

## 源码与发布

- **网站源码根目录**：`E:\顽石智护网站`
- **公开站点**：`https://wanshizhihu.com/`
- **预览站**：`https://wanshizhihu.pages.dev/`
- **部署方式**：GitHub `main` 分支推送后，Cloudflare Pages 自动部署。不要为普通内容发布重新创建站点或修改域名。
- **原始素材目录**：通常在 `F:\素材库\AI素材\`；网站内只放为网页发布准备的副本，绝不改动这里的原始视频。

## 重要结构

- 视频文件：`assets/uploads/`
- 文章正文：`experience/posts/<slug>.md`
- 文章列表：`experience/posts/list.json`（新文章必须添加在数组顶部）
- 文章页模板：`experience/post.html`
- 内容后台：`/admin` 会由根目录 `_redirects` 转到 Netlify Identity 后台。不要删除或覆盖 `_redirects` 中的三条 `/admin` 跳转规则。

## 发布视频文章的固定流程

1. 根据视频主题确定清晰、简短的中文标题与英文 `slug`。
2. 检查原始视频的时长、分辨率与文件大小；保留原始素材不动。
3. Cloudflare Pages 单个静态文件最多 **25 MiB**。超过时，使用 H.264/AAC 生成网页副本（通常 1280×720、两遍压缩），将网页副本控制在 25 MiB 以下。
4. 将网页视频放在 `assets/uploads/<slug>.mp4`。
5. 新建 `experience/posts/<slug>.md`，使用现有文章的 YAML front matter 格式，并用 `<video controls>` 引用 `/assets/uploads/<slug>.mp4`。
6. 在 `experience/posts/list.json` 顶部添加 `slug`、`title`、`date`、`excerpt`、`type: 视频`。
7. 先用 JSON 解析验证列表、检查视频文件存在和大小；仅暂存本次新增或修改的文件，**不要使用 `git add .`**。
8. 提交并推送 `main`，然后核验：
   - `https://wanshizhihu.pages.dev/experience/posts/list.json`
   - `https://wanshizhihu.com/experience/posts/list.json`
   - `https://wanshizhihu.com/experience/post.html?slug=<slug>`
   - 视频资源的 HTTP 状态与 `video/mp4` 内容类型。

## 内容与安全

- 医疗、设备、照护内容应使用科普/经验分享语气；涉及具体方案时提醒结合专业人士评估，不做个体化医疗结论。
- 发布前不要擅自删除现有页面、视频、文章、重定向、域名或部署配置。
- 工作区可能有用户未提交的文件；无论是否相关，都不要暂存、覆盖或删除它们。
- 不要把密码、访问令牌、Cookie、远程地址中的凭据或任何私密配置写入源码、文档、提交信息或对话回复。

## 用户交付格式

每次网站上新并验证成功后，必须额外提供一个可一键复制的代码块，内容严格为两行：

```text
中文标题
https://wanshizhihu.com/experience/post.html?slug=<slug>
```

微信不识别 Markdown 超链接；分享文案使用“中文文字 + 中文标题 + 纯网址链接”，不要输出 `[标题](链接)` 作为最终分享格式。
