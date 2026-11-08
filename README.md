# FOD 播放环境检测

一个纯前端、零后端的诊断页，用来判断「为什么打不开 / 播放不了 FOD」。

## 检测内容

- **出口 IP（多源）** — ipwho.is / ipapi.co / ipinfo.io / ip.sb 并发查询，任一可用即可，并做一致性比对
- **FOD 地区判定** — 直接调用 `geo.fod.j-stream.jp/api/check`，读取 `result: true|false`
- **域名连通性** — `fod` / `i.fod` / `waiting.id` / `geo` 四个关键域名
- **DRM 能力（EME）** — Widevine 硬件级/软件级、FairPlay、PlayReady、HDCP 2.2
- **设备与浏览器** — 平台识别，Android 引导下载原生 App

## 已知限制

- 手机浏览器（Android / iOS）打开 FOD 网页会被**强制跳转 App 或 App Store**，开「桌面版网站」多数情况也无效。本页在手机上只用于诊断，不能播放。
- 浏览器只能读到 EME 声明的能力，不等于服务端最终授权；Android 的真实 L1/L3、GMS、内购需要原生 App。
- FOD App 要求 iOS 15.0+，iPhone 6（最高 iOS 12.5.7）无法使用。

## 部署

任意静态托管均可，仓库根目录即网站根目录：

- **Cloudflare Pages**：连接本仓库 → 构建命令留空 → 输出目录 `/`
- **Vercel**：导入仓库 → Framework 选 Other → 无需构建
- **GitHub Pages**：Settings → Pages → Source 选 `main` / `root`

自定义域名建议用 `fod.` 子域，CNAME 指向托管商给出的目标；若域名在 Cloudflare 且用 Cloudflare Pages，控制台内直接绑定即可，无需手动改 DNS。

## 目录

```
index.html    诊断页（单文件，无外部依赖）
fod-diag.apk  Android 原生检测 App（可选，供上架下载）
```
