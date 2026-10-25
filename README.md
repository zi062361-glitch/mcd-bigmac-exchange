# 🍔 麦门汇率 M-Currency Exchange

> Big Mac Index · 个人版。你的时薪不是 ¥40，是 **1.63 个巨无霸**。

用 [麦当劳官方 MCP](https://open.mcd.cn/mcp) 查实时巨无霸价格，把你的收入换算成「麦门货币」，生成一张可分享的**麦门汇率卡**——含专属麦门称号和梗语。

麦当劳程序员创意开发大赛参赛作品（基于 McDonald's China MCP 能力 + 腾讯 WorkBuddy 开发）。

## ✨ 它能干什么

- **实时锚定汇率**：调用麦当劳 MCP 的门店/菜单/算价工具，取你附近门店的巨无霸真实售价作为「麦门货币」锚点
- **购买力换算**：月薪 / 日薪 / 时薪 → 巨无霸/小时、巨无霸/月、吃一个巨无霸要打工几分钟
- **麦门称号评级**：从「巨无霸联邦储备银行行长」到「板烧挣扎者」，7 段位
- **彩蛋换算**：一杯咖啡、一次地铁、一顿伤心套餐 = 多少打工时间
- **网页版计算器**：不接 MCP 也能玩，打开 [assets/exchange-card.html](assets/exchange-card.html) 手输价格即可生成汇率卡

## 🚀 快速开始（WorkBuddy）

1. 去 [open.mcd.cn/mcp](https://open.mcd.cn/mcp) 申请 Token（手机号登录 → 控制台 → 激活申请）
2. 在 WorkBuddy 连接器管理中按 [mcp-config.example.json](mcp-config.example.json) 配置麦当劳 MCP Server（Token 放环境变量，别硬编码）
3. 安装本 Skill：把 `SKILL.md` 放入 `~/.workbuddy/skills/mcd-bigmac-exchange/`
4. 对 WorkBuddy 说：**「我的工资能买几个巨无霸？」** 或 **「算一下我的麦门汇率」**
5. 收下你的汇率卡，截图，转发，让同事破防

## 🖥️ 网页版（零配置）

不想申请 Token？直接用浏览器打开 `assets/exchange-card.html`，手输巨无霸价格和月薪，同样出卡——只是没有实时价加持的仪式感。

## 🧱 用了哪些 MCP 能力

| 工具 | 用途 |
|---|---|
| `query-nearby-stores` | 找附近门店 |
| `query-meals` / `query-meal-detail` | 定位巨无霸并取价 |
| `calculate-price` | 精确算单点价（兜底） |

详见 [MCP_INTEGRATION.md](MCP_INTEGRATION.md)。

## 📁 目录结构

```
mcd-bigmac-exchange/
├── SKILL.md                  # WorkBuddy Skill 本体（核心交付物）
├── assets/
│   └── exchange-card.html    # 网页版汇率卡生成器
├── README.md
├── MCP_INTEGRATION.md        # MCP 接入说明
├── mcp-config.example.json   # 脱敏 MCP 配置示例
├── CONTEST_DECLARATION.md    # 参赛声明（官方原文）
└── workbuddy.md              # WorkBuddy 开发记录
```

## 🏆 赛事信息

- 赛事：麦当劳程序员创意开发大赛（10.09–10.25）
- 主办：McDonald's China × WorkBuddy
- 规则仓库：[M-China/mcd-developer-innovation-challenge](https://github.com/M-China/mcd-developer-innovation-challenge)

## ⚠️ 免责声明

本项目为参赛者独立开发的娱乐性作品，非麦当劳官方产品。所有换算结果仅供参考，不构成任何理财建议（巨无霸也不构成）。餐品价格、供应状态以麦当劳官方渠道实时结果为准。
