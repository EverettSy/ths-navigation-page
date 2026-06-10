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

## Cloudflare Pages 控制台部署

1. 将本目录提交到 Git 仓库。
2. 在 Cloudflare Pages 创建项目并连接仓库。
3. 构建配置填写：
   - Framework preset: `None`
   - Build command: `npm run build`
   - Build output directory: `public`
4. 保存并部署。

## Wrangler 部署

```bash
npm run deploy
```

本地预览：

```bash
npm run preview
```

## 注意事项

页面内有多个外部 iframe 链接，其中部分是 `http://` 地址。Cloudflare Pages 会通过 HTTPS 访问，现代浏览器可能会拦截 HTTPS 页面中的 HTTP iframe；这属于浏览器混合内容限制，不是 Pages 构建错误。若目标站点支持 HTTPS，可以把对应链接改成 `https://`。
