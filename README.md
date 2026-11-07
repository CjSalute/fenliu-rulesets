# fenliu-rulesets

代理工具分流规则集远程托管仓库 —— 所有规则集**自包含**，不依赖第三方仓库。

规则来源：从 `Smart-Config-Kit` 的 Surge 配置中提取 288 条外部引用，逐条下载合并、去重、清洗格式后重新分类生成。

## 目录结构

```
fenliu-rulesets/
├── README.md
└── Surge/
    ├── Muse.list                 # Meta Muse 分流规则集
    ├── Surge-template.conf       # 适配本仓库规则集的 Surge 完整配置模板
    └── Rulesets/
        ├── AI.list               # AI 服务
        ├── Advertising?          # 广告拦截（拆分为 AdBlock01~24）
        ├── Apple.list …          # 其余分类，见下表
```

## 规则集总览

共 **31 个分类**，**137,243 条**规则。广告拦截因单文件体积拆为 24 片（`AdBlock01.list` ~ `AdBlock24.list`，合计 103,677 条）。

| 规则集 | 规则数 | 对应策略组 |
|---|---:|---|
| `AdBlock01`~`AdBlock24` | 103,677 | 🛑 广告拦截 |
| `ChinaMedia.list` | 4,561 | 📺 国内流媒体 |
| `ChinaSite.list` | 12,731 | 🏠 国内网站 |
| `Restricted.list` | 6,469 | 🚫 受限网站 |
| `Netflix.list` | 1,219 | 🎥 Netflix |
| `Tools.list` | 1,334 | 🔧 工具与服务 |
| `SocialMedia.list` | 780 | 📱 社交媒体 |
| `GlobalMedia.list` | 777 | 🌐 其他国外流媒体 |
| `GlobalGame.list` | 737 | 🎮 国外游戏 |
| `GlobalSite.list` | 547 | 🌐 国外网站 |
| `Microsoft.list` | 683 | Ⓜ️ 微软服务 |
| `Financial.list` | 367 | 🏦 金融支付 |
| `AI.list` | 368 | 🤖 AI 服务 |
| `Apple.list` | 333 | 🍎 苹果服务 |
| `Crypto.list` | 295 | 💰 加密货币 |
| `Tracker.list` | 248 | 🛰️ BT/PT Tracker |
| `YouTube.list` | 190 | 📹 YouTube |
| `Disney.list` | 175 | 🎬 Disney+ |
| `InstantMessaging.list` | 144 | 💬 即时通讯 |
| `DirectExtra.list` | 142 | DIRECT |
| `Download.list` | 767 | 📥 下载更新 |
| `JPKRMedia.list` | 107 | 🇯🇵 日韩流媒体 |
| `EUMedia.list` | 104 | 🇪🇺 欧洲流媒体 |
| `Music.list` | 77 | 🎵 音乐流媒体 |
| `Meeting.list` | 70 | 🧑‍💼 会议协作 |
| `HKMedia.list` | 69 | 🇭🇰 香港流媒体 |
| `ChinaGame.list` | 68 | 🕹️ 国内游戏 |
| `Hulu.list` | 59 | 📺 Hulu |
| `HBO.list` | 50 | 📡 HBO/Max |
| `TWMedia.list` | 41 | 🇹🇼 台湾流媒体 |
| `TikTok.list` | 36 | 🎵 TikTok |
| `PrimeVideo.list` | 18 | 🎬 Prime Video |
| `Muse.list` | 11 | 🤖 AI 服务 |

## 使用方法

### 方式一：直接用配置模板（最省事）

```
https://raw.githubusercontent.com/CjSalute/fenliu-rulesets/main/Surge/Surge-template.conf
```

Surge → 配置 → ➕ → 从 URL 安装 → 粘贴上面的链接 → 下载 → 启用。

模板已含 `[General]` / `[DNS]` / `[Proxy Group]` / `[Rule]` / `[Host]` / `[URL Rewrite]` / `[MITM]`，56 条 `RULE-SET` 全部指向本仓库。

> 节点需另配：把机场订阅作为子配置导入，再在主配置里选为「节点来源」。

### 方式二：只取需要的规则集

在 `[Rule]` 段按需添加，例如：

```
RULE-SET, https://raw.githubusercontent.com/CjSalute/fenliu-rulesets/main/Surge/Rulesets/AI.list, 🤖 AI 服务
RULE-SET, https://raw.githubusercontent.com/CjSalute/fenliu-rulesets/main/Surge/Rulesets/Muse.list, 🤖 AI 服务
RULE-SET, https://raw.githubusercontent.com/CjSalute/fenliu-rulesets/main/Surge/Rulesets/Netflix.list, 🎥 Netflix
```

广告拦截需引 24 片：

```
RULE-SET, https://raw.githubusercontent.com/CjSalute/fenliu-rulesets/main/Surge/Rulesets/AdBlock01.list, 🛑 广告拦截
...（AdBlock02 ~ AdBlock24 同理）
```

> 规则顺序：具体业务规则在前，`GEOIP,CN,DIRECT` 和 `FINAL` 在最后。

### jsDelivr 镜像（国内更快）

把 `raw.githubusercontent.com` 换成 `cdn.jsdelivr.net`：

```
https://cdn.jsdelivr.net/gh/CjSalute/fenliu-rulesets@main/Surge/Rulesets/AI.list
```

## Muse (Meta) 规则集说明

域名来源：抓取 `muse.ai` 官网及其 Next.js 前端 bundle 中硬编码的生产域名列表。

已覆盖：主站 `muse.ai` / `museai.com`、API `api.muse.ai`、语音 `voice.museai.com`、Agent 域名 `agent.meta.ai` / `hatch.meta.ai` / `hatch.club` / `ecto1.ai`、登录鉴权 `auth.meta.com` / `accountscenter.meta.com`、静态资源 `nest-static.fbcdn.net`。

未整体拦截 `meta.ai` 与 `*.fbcdn.net`，避免误伤 Instagram 等正常流量。

## 已知限制

- 广告规则原始文件 3.4MB，受上传通道对单请求体积的限制（约 250KB 上限），拆为 24 个约 145KB 的分片。规则总数与原文件完全一致（103,677 条），无遗漏。
- 源配置中有 3 条规则集链接已失效（`hagezi` 的 surge 版、`blackmatrix7` 的 RemoteDesktop / BiliIntl），已跳过。

## 更新日志

- 初始化仓库
- 新增 31 个分类规则集（137,243 条）
- 新增 Muse (Meta) 分流规则集
- 新增 Surge 配置模板

---

> 规则仅供个人网络配置使用，请遵守当地法律法规。
