---
title: Hello-Hexo-Cloudflare
date: 2026-01-28 12:00:00
tags: [Hexo, Cloudflare]
---

正文开始，支持 **Markdown** 全部语法。


<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Hexo + GitHub + Cloudflare 免费博客搭建指南

## 前提准备

需要 GitHub 账号、Node.js（版本 16+）、Git，以及一个免费域名（可选，从 Freenom 或 Cloudflare Registrar 获取）。[^1][^2]
确保电脑安装 Node.js 和 Git，通过命令 `node -v` 和 `git --version` 验证。
Cloudflare 账号用于 CDN 和免费 SSL 加速。[^2][^4]

## 步骤1: 创建 GitHub 仓库

登录 GitHub，创建名为 `username.github.io` 的仓库（username 为你的用户名），设为 Public。
克隆仓库：`git clone https://github.com/username/username.github.io.git`。[^3][^2]
等待审核通过（首次约 10 分钟），访问 `https://username.github.io` 测试 GitHub Pages。[^3]

## 步骤2: 安装 Hexo

全局安装 Hexo CLI：`npm install -g hexo-cli`。[^5]
创建博客项目：`hexo init myblog && cd myblog && npm install`。[^5]
本地预览：`hexo g && hexo s`，浏览器打开 `http://localhost:4000`。[^4][^5]

## 步骤3: 配置 Hexo 站点

编辑根目录 `_config.yml`：

- 设置 `title`、`subtitle`、`description`、`author`。
- `url: https://username.github.io`（替换 username）。
- 保存后运行 `hexo clean && hexo g && hexo s` 测试。[^1][^5]


## 步骤4: 安装并配置主题

推荐 Fluid 或 NexT 主题。
克隆主题：`git clone https://github.com/fluid-dev/hexo-theme-fluid.git themes/fluid`（替换为目标主题）。[^9][^5]
在 `_config.yml` 中设 `theme: fluid`，启用主题配置文件 `_config.fluid.yml`。[^5]
运行 `hexo g && hexo s` 预览。

## 步骤5: 安装部署插件

运行 `npm install hexo-deployer-git --save`。[^9][^1]
编辑 `_config.yml` 部署部分：

```
deploy:
  type: git
  repo: https://github.com/username/username.github.io.git
  branch: main
```

使用 GitHub Personal Access Token（Settings > Developer settings > Personal access tokens）替换密码。[^5]

## 步骤6: 首次部署到 GitHub Pages

运行 `hexo clean && hexo g -d`（`-d` 自动部署）。[^1][^9]
浏览器访问 `https://username.github.io`，确认博客上线。

## 步骤7: 集成 Cloudflare

注册 Cloudflare，添加站点（输入你的域名或 `username.github.io`）。[^2][^4]
添加 DNS 记录：CNAME `@` → `username.github.io`，Proxy 开启（橙色云）。[^2]
在域名商处将 Nameservers 改为 Cloudflare 提供的 NS 记录（生效 24 小时内）。[^2]
启用 SSL/TLS 为 Full（严格），自动 HTTPS。[^4][^2]

## 步骤8: 自定义域名（可选）

在 GitHub 仓库 Settings > Pages > Custom domain 输入域名，保存。
仓库根目录新建 `CNAME` 文件（无后缀），内容为你的域名。
重新部署 `hexo d`，Cloudflare 接管流量。[^2]

## 步骤9: 写作与更新

新建文章：`hexo new post "标题"`，编辑 `source/_posts/` 下 Markdown 文件。
发布：`hexo clean && hexo g -d`。[^1]
添加评论（如 Gitalk 或 utterances）：在主题配置中集成 GitHub App。[^9][^1]

## 常见问题排查

- 部署失败：检查 Token 和 SSH 密钥（可选 `ssh-keygen` 生成）。[^5]
- 域名不生效：验证 DNS 传播（`dig @`）。
- 主题样式错乱：确认 `theme` 配置并清理缓存。[^5]
<span style="display:none">[^10][^6][^7][^8]</span>

<div align="center">⁂</div>

[^1]: https://kdsunset.top/hxpghblog/index.html

[^2]: https://tiger.fail/archives/hexo-setup-guide.html

[^3]: https://wsgzao.github.io/post/hexo/

[^4]: https://www.bilibili.com/read/cv32465194/

[^5]: https://blog.csdn.net/yaorongke/article/details/119089190

[^6]: https://blog.csdn.net/etrospect/article/details/147783798

[^7]: https://cloud.tencent.com/developer/article/2235973

[^8]: https://rockway.blog/post/hexo-guide

[^9]: https://www.youtube.com/watch?v=IeGJFOlClxc

[^10]: https://cloud.tencent.com/developer/article/2149937

