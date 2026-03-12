# iCost Skill for OpenClaw

> 让 AI 助手直接帮你往 iCost 里记账 —— 发截图、说一句话，账就记好了。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Platform: macOS](https://img.shields.io/badge/Platform-macOS-blue.svg)]()
[![OpenClaw Skill](https://img.shields.io/badge/OpenClaw-Skill-green.svg)](https://clawhub.com)

---

## 功能

- 📸 **截图记账** — 发一张支付截图，AI 自动识别金额、商家、日期，一键写入 iCost
- 💬 **口语记账** — 说"刚花 50 吃饭"，AI 帮你分类并记录
- 📊 **批量导入** — 导出微信支付账单 `.xlsx`，自动转换为 iCost 导入格式，覆盖几个月的流水
- 🔗 **URL Scheme** — 直接唤起 iCost 记账界面，首次使用需手动点击确认，之后无需再次确认

---

## 前置条件

| 条件 | 说明 |
|------|------|
| **macOS** | 需要 macOS 系统（通过 `open` 命令触发 URL Scheme） |
| **iCost 应用** | 需要安装 iCost for Mac，官网：[icostapp.com](https://icostapp.com) |
| **OpenClaw** | 需要安装 [OpenClaw](https://openclaw.ai) AI 助手框架 |
| **Python 3 + openpyxl** | 批量导入功能需要（`pip install openpyxl`） |

> 💡 iCost 是一款优秀的个人/家庭记账应用，支持正版，欢迎前往 [icostapp.com](https://icostapp.com) 了解和购买。

---

## 安装

### 方式一：通过 ClawHub 安装（推荐）

```bash
clawhub install icost
```

### 方式二：手动安装

```bash
git clone git@github.com:aqHi/icost-skill.git
# 将目录复制到 OpenClaw skills 路径
cp -r icost-skill ~/.openclaw/workspace/skills/icost
```

---

## 使用方法

### 截图记账

在 iMessage / 微信 等渠道，直接发一张支付截图给 AI 助手：

```
[发送支付宝/微信支付/拼多多订单截图]
```

AI 会自动识别并调用：

```bash
open "iCost://expense?amount=22.55&currency=CNY&category=购物&date=2026.03.12&remark=拼多多订单"
```

> **首次使用提示：** macOS 第一次通过 `open` 命令打开 `iCost://` 链接时，系统会弹窗询问是否允许打开 iCost，点击「允许」即可。**后续使用无需再次确认。**

### 口语记账

直接告诉 AI 助手：

```
帮我记一笔，今天下午喝奶茶花了 28 块，用微信付的
刚在盒马买了菜，花了 156.8
记一下，马拉松报名费 150，运动类
```

### 批量导入微信账单

1. 在微信 → 「我」→「支付」→「钱包」→「账单」→「常见问题」→「下载账单」，导出 `.xlsx`
2. 发给 AI 助手，说「帮我转换成 iCost 格式」
3. AI 运行转换脚本，生成 `*_icost.xlsx`
4. 在 iCost → 「设置」→「数据导入」，选择生成的文件导入

---

## 自动分类规则

| 关键词 | 分类 |
|--------|------|
| 餐饮类商家（麦当劳、奶茶、烤肉…） | 餐饮 / 三餐 |
| 拼多多、京东、盒马、超市… | 购物 / 网购超市 |
| 骑行、健身、跑步、马拉松… | 运动 / 运动健身 |
| 电费、燃气、水费、电网… | 居家 / 水电燃气 |
| 滴滴、地铁、高铁、停车… | 交通 / 出行 |
| 保险 | 金融 / 保险 |
| 腾讯云、阿里云、服务器… | 数码 / 云服务 |
| 转账（个人） | 转账 / 个人转账 |

> 识别规则保存在 `references/categories.md`，可自行编辑扩展。

---

## 文件结构

```
icost-skill/
├── SKILL.md                    # OpenClaw 技能入口
├── README.md                   # 本文档
├── LICENSE                     # MIT 协议
├── references/
│   ├── url_scheme.md           # iCost URL Scheme 完整参数参考
│   └── categories.md           # 关键词→分类映射规则
└── scripts/
    └── wechat_to_icost.py      # 微信账单批量转换脚本
```

---

## 贡献

欢迎提交 PR 或 Issue：

- 增加支付宝账单支持
- 改进分类规则
- 支持更多记账 App

---

## 协议

[MIT License](LICENSE) © 2026 aqHi
