# QuantumultX 简约配置（MageGojo）

一份精简、可读、带统一图标的 Quantumult X 配置：**订阅解析 + AI 分流 + 常用业务分流 + 地区筛选**（自动排除不支持地区与垃圾节点）。策略组无 emoji，使用统一风格图标。

## 快速开始
1. Quantumult X →「设置 / 配置」→ 引用 / 下载下面的链接（走 jsDelivr，大陆可直连，避免冷启动回环）：
   `https://testingcf.jsdelivr.net/gh/MageGojo/QuantumultX@main/MageGojo.conf`
   > 备用（已有可用代理 / GitHub 能直连时再用）：`https://raw.githubusercontent.com/MageGojo/QuantumultX/main/MageGojo.conf`
   > 为什么主链接不用 `raw.githubusercontent.com`：该域名大陆直连常被墙，手机冷启动时还没有可用节点 →「拉配置得先有节点、有节点得先拉到配置」形成**回环**。jsDelivr(testingcf) 大陆可直连，从根上规避。
2. 打开 `MageGojo.conf`，把 `[server_remote]` 里的示例链接替换为你的**机场订阅链接**（可多条）。
3. 重启 Quantumult X，订阅节点与策略组图标会自动加载。

> 订阅 / 规则 / 图标偶发拉取失败时：Quantumult X →「设置 → 其他 → 资源解析使用代理」打开，让它们走节点更新，进一步免疫冷启动回环。

> **jsDelivr 缓存说明（重要）**：`@main` 分支链接有约 12h 的 CDN 缓存，**刚 push 完不会立刻刷新**。想立即拿到最新配置，二选一：
> 1. 用 **commit 锁定链接**（不可变、秒生效）：`https://testingcf.jsdelivr.net/gh/MageGojo/QuantumultX@<最新commit短哈希>/MageGojo.conf`，例如当前最新：`@8adf211`。
> 2. 访问一次刷新接口再等几分钟：`https://purge.jsdelivr.net/gh/MageGojo/QuantumultX@main/MageGojo.conf`。
> 日常自动更新用 `@main` 即可（约 12h 内自动同步到最新）。

## 策略组一览
| 策略组 | 说明 |
|---|---|
| OpenAI / Claude / GoogleAI | AI 对话 / 接口，封 港澳俄中(走 `AI自动`)。默认 `AI自动`(总有节点不黑洞)；有住宅 / 家宽节点时可手动切 `AI住宅`(住宅优先测速) 或 `AI故障转移`(住宅池按序故障转移)，住宅 IP 基本能过 ChatGPT 风控。详见 `docs/设计.md` |
| Gemini / GoogleSearch | Gemini 网页版放行港澳(走 `Gemini自动`)；谷歌搜索仅封中国大陆(走 `Google自动`)。均追加 `全局自动 / direct` 兜底防黑洞 |
| GitHub / YouTube / TikTok / 国际媒体 | 常用代理业务（国际媒体含 Netflix / Disney+ / HBO / Spotify 等），走 `代理` 或 `全局自动` |
| 微软服务 / 苹果服务 / 国内服务 | 默认直连，可切代理 |
| 广告拦截 | 默认 `reject` |
| 漏网之鱼 | 兜底分流 |
| 代理 | 手动总组（含全部节点手动池）|
| 全局自动 / AI自动 / AI住宅 / AI故障转移 / Gemini自动 / Google自动 | 自动测速 / 住宅 / 故障转移基础组（按各平台支持地区筛选）|

> **AI 可达性说明**：QX 不支持给单个策略组设独立健康检查 URL（只能用全局 `server_check_url`），无法像 Shadowrocket 那样用 `chatgpt.com/cdn-cgi/trace` 探测 OpenAI 风控。故用「住宅优先 + 故障转移」逼近：`AI住宅` / `AI故障转移` 只挑订阅里名字含 家宽 / 原生 / 住宅 / 解锁 / 流媒体 的节点，这类住宅 IP 基本能过 OpenAI / Claude 风控；若订阅无此类节点，两组会空，主组自动回退 `AI自动`，不黑洞。
> **GoogleAI vs GoogleSearch vs Gemini** 的精确分流（AI Studio / Gemini API → GoogleAI；gemini.google.com → Gemini；www.google.com → GoogleSearch）在 `[filter_local]` 手写完成——blackmatrix7 的 Gemini / Google 列表会把三者混为一谈，故不引用。

## 图标
- AI 区：[lobehub/lobe-icons](https://github.com/lobehub/lobe-icons)
- 功能 / 地区区：[Koolson/Qure](https://github.com/Koolson/Qure)（Color）
- 均通过 jsDelivr 加载，同类风格统一、无 emoji。

## 地区 / 垃圾节点过滤
通过 `server-tag-regex` 在策略组层面动态筛选，**统一用「纯排除」正则（含 emoji 国旗）**，比白名单更稳——只要节点名「不含」关键词就入选，连纯 🇯🇵🇺🇸 emoji 命名的节点也不会被漏掉：
- 垃圾节点：`剩余 / 流量 / 到期 / 过期 / 官网 / 订阅 / 客服 / 群组 / 测速 / Expire / Traffic / Reset` 等。
- 中国大陆（所有代理组都排）：`🇨🇳 / 大陆 / 回国`。
- 港澳俄（OpenAI / Claude / GoogleAI 额外排）：`🇭🇰 香港 HK / 🇲🇴 澳门 Macau / 🇷🇺 俄罗斯 Russia`。

可在 `MageGojo.conf` 的 `[policy]` 中自行增删关键词。

## 致谢
- 分流规则：[blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)
- 图标：[Koolson/Qure](https://github.com/Koolson/Qure)、[lobehub/lobe-icons](https://github.com/lobehub/lobe-icons)

> 详细设计见 [`docs/设计.md`](docs/设计.md)，进度见 [`docs/进度.md`](docs/进度.md)。
