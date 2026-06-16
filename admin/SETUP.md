# Decap CMS 使用与上线说明

后台地址：本地 `http://localhost:4000/admin/`，上线后 `https://yli000.github.io/admin/`。

---

## 1. 本地免登录测试（现在就能用，不碰 GitHub）

需要两个进程同时开着：

```bash
# 终端 A：博客本体
bundle exec jekyll serve --livereload

# 终端 B：Decap 的本地后端（第一次会自动下载）
npx decap-server
```

然后浏览器打开 **http://localhost:4000/admin/** ，直接就能新建/编辑文章、左写右预览、点「Publish」。
此模式下「发布」= 写入本机 `_posts/` 文件，**不会**推到 GitHub（要上线还得 `git push`，或配好下面第 2 步）。

> `config.yml` 里的 `local_backend: true` 就是这个开关，只在 localhost 生效，留着不影响线上。

---

## 2. 让线上 /admin 能直接发布（一次性配置，需要你的 GitHub/Cloudflare 账号）

GitHub Pages 是纯静态站，没法自己做登录，所以要挂一个免费的 OAuth 代理。推荐用 Cloudflare Worker。

**(a) 建一个 GitHub OAuth App**
GitHub → Settings → Developer settings → OAuth Apps → New OAuth App
- Homepage URL：`https://yli000.github.io`
- Authorization callback URL：`https://<你的worker域名>/callback`（worker 建好后再回填）
- 创建后记下 **Client ID**，并 Generate 一个 **Client Secret**。

**(b) 部署 OAuth 代理（Cloudflare Worker）**
用现成模板 `sveltia/sveltia-cms-auth`（与 Decap 协议兼容）一键部署到 Cloudflare Workers，设置环境变量：
- `GITHUB_CLIENT_ID` = 上一步的 Client ID
- `GITHUB_CLIENT_SECRET` = 上一步的 Client Secret
- `ALLOWED_DOMAINS` = `yli000.github.io`

部署后拿到 worker 域名（形如 `https://xxx.workers.dev`），回到 (a) 把 callback 填成 `https://xxx.workers.dev/callback`。

**(c) 回填本仓库配置**
编辑 `admin/config.yml`，把 `backend` 下被注释的那行打开并改成你的 worker 域名：
```yaml
backend:
  name: github
  repo: yli000/yli000.github.io
  branch: main
  base_url: https://xxx.workers.dev
```
推送上线后，打开 `https://yli000.github.io/admin/` → 用 GitHub 登录 → 写文章 → Publish，会直接 commit 到仓库、约 1 分钟后线上更新。

参考官方清单：https://decapcms.org/docs/external-oauth-clients/

---

## 3. 注意：正文里的 `<details>` 折叠块

Decap 的「正文」用的是富文本/Markdown 混合编辑器，富文本模式可能会破坏 `<details markdown="1">` 这类原生 HTML。
**写带折叠块的文章时，点编辑器右上角的 `</>`（Markdown 源码）按钮切到源码模式再写**，就不会被改坏。
