# QuantumultX 简约配置（MageGojo）

一份精简、可读、带统一图标的 Quantumult X 配置：**订阅解析 + AI 分流 + 常用业务分流 + 地区筛选**（自动排除不支持地区与垃圾节点）。策略组无 emoji，使用统一风格图标。

## 快速开始
1. Quantumult X →「设置 / 配置」→ 引用 / 下载下面任一链接：
   - 直连：`https://raw.githubusercontent.com/MageGojo/QuantumultX/main/MageGojo.conf`
   - jsDelivr 加速：`https://cdn.jsdelivr.net/gh/MageGojo/QuantumultX@main/MageGojo.conf`
2. 打开 `MageGojo.conf`，把 `[server_remote]` 里的示例链接替换为你的**机场订阅链接**（可多条）。
3. 重启 Quantumult X，订阅节点与策略组图标会自动加载。

## 策略组一览
| 策略组 | 说明 |
|---|---|
| OpenAI / Gemini / Claude / Google | AI 平台。默认 `AI自动`（自动测速，已排除香港 / 回国 / 垃圾节点），也可手动选地区或具体节点 |
| GitHub / YouTube / 国际媒体 | 常用代理业务（国际媒体含 Netflix / Disney+ / HBO / Spotify 等）|
| TikTok | 仅 日本 / 台湾 / 美国 / 新加坡 / 韩国（排除香港、大陆）|
| 微软服务 / 苹果服务 / 国内服务 | 默认直连，可切代理 |
| 广告拦截 | 默认 `reject` |
| 漏网之鱼 | 兜底分流 |
| 代理 | 手动总组（含全部节点手动池）|
| 全局自动 / AI自动 / 香港·台湾·日本·新加坡·美国·韩国 | 自动测速基础组 |

## 图标
- AI 区：[lobehub/lobe-icons](https://github.com/lobehub/lobe-icons)
- 功能 / 地区区：[Koolson/Qure](https://github.com/Koolson/Qure)（Color）
- 均通过 jsDelivr 加载，同类风格统一、无 emoji。

## 地区 / 垃圾节点过滤
通过 `server-tag-regex` 在策略组层面动态筛选：统一排除 `剩余 / 过期 / 官网 / 流量 / 游戏 / 倍率 / 网址 / 测试` 等垃圾信息节点；AI 组额外排除 `香港 / 回国 / 中国`。可在 `MageGojo.conf` 的 `[policy]` 中自行增删关键词。若某地区你没有节点，可删除对应地区组。

## 致谢
- 分流规则：[blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script)
- 图标：[Koolson/Qure](https://github.com/Koolson/Qure)、[lobehub/lobe-icons](https://github.com/lobehub/lobe-icons)

> 详细设计见 [`docs/设计.md`](docs/设计.md)，进度见 [`docs/进度.md`](docs/进度.md)。
