# 部署指南（Cloudflare Pages / GitHub Pages）

## 目录
- `index.html`：最终页面（已内置点击卡片复制模型名 + Toast 提示）
- `_headers`：Cloudflare Pages 响应头（允许被嵌入到 iframe 中文档）

---

## 方式 A：Cloudflare Pages（最简单）

### 1. 直接上传文件
1. 打开 Cloudflare Dashboard → **Pages** → **Create a project** → 选择 **Upload assets**。
2. 拖拽本目录下的 **index.html** 和 **_headers** 两个文件到上传框。
3. 点击部署，完成后会得到一个 `https://xxx.pages.dev` 域名。

### 2. 连接 Git 仓库（方便以后改动）
1. 把本目录作为一个仓库推送到 GitHub/GitLab（仓库根目录包含 `index.html` 和 `_headers`）。
2. Cloudflare Pages → **Create a project** → 连接该仓库。
3. Framework 选择 **None**，Build Command 留空，Output directory 写 `/`（根目录）。
4. 部署完成。以后你只要 push 代码，Pages 会自动重新部署。

### 3. 嵌入到你的后台首页（iframe）
- 在你的后台「首页内容」输入框里直接填入 Cloudflare Pages 的链接（例如 `https://xxx.pages.dev/`）。
- 若你后台限制 iframe 嵌入，可以把 `_headers` 里 `frame-ancestors *;` 改为你的后台域名，例如：
  ```
  /*
    Content-Security-Policy: frame-ancestors https://admin.yourdomain.com;
  ```

---

## 方式 B：GitHub Pages（备选）
1. 在 GitHub 新建一个仓库，把 `index.html` 推上去（根目录）。
2. 仓库 Settings → **Pages** → Source 选择 **Deploy from a branch**；Branch 选 `main`/`master`，Root 选 `/`。
3. 保存后等待几分钟，GitHub 会生成一个 `https://你的用户名.github.io/仓库名/` 的页面链接。

> 注：GitHub Pages 不支持 `_headers`；若需要被 iframe 嵌入，请改用 Cloudflare Pages。

---

## 验证复制功能
- 打开页面，点击任意模型卡片；
- 底部会弹出 “已复制：模型名” 提示；
- 在输入框或聊天框粘贴，看看是否复制成功。

祝你使用愉快！
