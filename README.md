# 同花顺策略导航合集

这是从原始 `导航合集.html` 改造出的 Cloudflare Pages 静态站点项目。

## 项目结构

```text
ths-navigation-page/
  public/
    index.html
    _headers
    _redirects
  package.json
  wrangler.toml
```

## Cloudflare Pages 部署

1. 将本目录提交到 Git 仓库。
2. 在 Cloudflare Pages 创建项目并连接仓库。
3. 构建配置填写：
   - Framework preset: `None`
   - Build command: `npm run build`
   - Build output directory: `public`
   - Deploy command: 留空
4. 保存并部署。

不要在 Cloudflare Pages 中使用 `wrangler deploy`。这是 Workers 的部署命令，会要求 Worker 入口文件或 assets 配置，并触发 `Missing entry-point to Worker script or to assets directory` 错误。

也不要在 Cloudflare Pages 的 Git 构建中使用 `wrangler pages deploy` 或 `npm run pages:deploy`。Git 集成部署会自动上传 `public` 目录；在构建容器里手动跑 Wrangler 需要额外的 `CLOUDFLARE_API_TOKEN` 权限，容易触发 `Authentication error [code: 10000]`。

## Cloudflare Workers 部署

如果 Cloudflare 控制台页面里出现必填的“部署命令”，并且默认值类似 `npx wrangler versions upload`，说明当前创建的是 Workers 项目，不是 Pages 项目。此时填写：

- 构建命令：`npm run build`
- 部署命令：`npm run deploy`
- 非生产分支部署命令：`npm run deploy`
- 路径：`/`

`wrangler.toml` 已配置 `[assets] directory = "./public"`，Workers 会把 `public/index.html` 作为静态资源发布。

## Wrangler 部署

```bash
npm run pages:deploy
```

本地预览：

```bash
npm run preview
```

## 注意事项

页面内有多个外部 iframe 链接，其中部分是 `http://` 地址。Cloudflare Pages 会通过 HTTPS 访问，现代浏览器可能会拦截 HTTPS 页面中的 HTTP iframe；这属于浏览器混合内容限制，不是 Pages 构建错误。若目标站点支持 HTTPS，可以把对应链接改成 `https://`。
