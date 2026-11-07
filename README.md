# fenliu-rulesets

代理工具分流规则集远程托管仓库 —— 用于 **Surge / Clash / Loon / Quantumult X / sing-box** 等工具的规则订阅。

## 目录结构

```
fenliu-rulesets/
├── README.md
├── Surge/                 # Surge 规则集
│   └── Muse.list          # Meta Muse（muse.ai）分流规则集
```

## 规则集列表

| 规则集 | 类型 | 说明 | Raw 地址 |
|---|---|---|---|
| `Surge/Muse.list` | `#!type=domain` | Meta Muse（muse.ai）及其 API / 鉴权 / CDN | [直链](https://raw.githubusercontent.com/CjSalute/fenliu-rulesets/main/Surge/Muse.list) |

## Surge 使用方法

### 方式一：RULE-SET（推荐）

在 `[Rule]` 段添加：

```
RULE-SET, https://raw.githubusercontent.com/CjSalute/fenliu-rulesets/main/Surge/Muse.list, US
```

> 请把规则放在 `GEOIP,CN,DIRECT` 之前、`FINAL` 之前，否则不会命中。

### 方式二：直接引用域名规则

把各 `.list` 文件中的 `DOMAIN` / `DOMAIN-SUFFIX` 行复制进 `[Rule]` 段，并补上策略名即可。

## Muse 规则集说明

域名来源：抓取 `muse.ai` 官网及其 Next.js 前端 bundle 中硬编码的生产域名列表：

```
production: ["hatch.ecto1.ai","hatch.club","hatch.meta.ai","agent.meta.ai","muse.ai","production.museai.com"]
voice:      ["voice.museai.com"]
auth:       auth.meta.com / accountscenter.meta.com
cdn:        nest-static.fbcdn.net
```

已覆盖：

- **主站与 API**：`muse.ai`、`museai.com`、`api.muse.ai`、`voice.museai.com`
- **Agent 域名**：`agent.meta.ai`、`hatch.meta.ai`、`hatch.club`、`ecto1.ai`
- **登录鉴权**：`auth.meta.com`、`accountscenter.meta.com`
- **静态资源**：`nest-static.fbcdn.net`

注意事项：

- 未整体拦截 `meta.ai` 与 `*.fbcdn.net`，避免误伤 Instagram 等正常流量。
- 若使用语音功能感觉卡顿，可将 `voice.museai.com` 单独指向低延迟策略组。

## 更新日志

- 新增 Muse (Meta) 分流规则集

---

> 规则仅供个人学习与网络配置使用，请遵守当地法律法规。
