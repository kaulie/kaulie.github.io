# TravelTalker

浏览器 PTT 对讲机 —— 直接用两台手机打开网页即可互相通话（半双工，按住说话）。

**入口（地址永久固定）：**

```
https://kaulie.github.io/traveltalker/?channel=trip&name=A
```

把 `name` 换成不同的值（如 `A` / `B`）分给不同手机，`channel` 保持一致即可。

## 这里是什么

- `index.html` —— 对讲机页面（从 `endpoint.json` 读取当前后端地址，所以本页地址永不变）
- `endpoint.json` —— 当前后端（wss）地址，由 GitHub Actions 定时从服务器拉取更新，**请勿手工编辑**

后端代码与部署说明见仓库 `kaulie/travel_talker`。

## 为什么需要这层转发

后端跑在国内云服务器上。云厂商对**未备案域名**会按 SNI 拦截（80/443/8443 都一样），
所以后端实际通过 Cloudflare 隧道对外提供服务，而隧道地址在重启后会变。
本页面所在域名固定，Actions 每 5 分钟同步一次最新的后端地址，因此**二维码永远不用换**。
