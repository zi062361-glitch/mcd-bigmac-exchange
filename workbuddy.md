# WorkBuddy 开发记录

本项目使用腾讯 WorkBuddy 进行开发，本文件为开发过程记录，用于申报 WorkBuddy 3000 积分专项奖励。

## 项目信息

- 项目名称：麦门汇率 M-Currency Exchange
- 开发工具：腾讯 WorkBuddy（Agent 模式）
- 开发周期：2026-10-25（半天，程序员节当天赶 DDL 的作品）
- 作品类型：基于麦当劳 MCP 的 WorkBuddy Skill + 网页版演示

## 开发过程

### 1. 选题阶段

通过 WorkBuddy 联网调研赛事信息与麦当劳 MCP 能力清单（38 个工具），对比了 4 个候选方向（麦门汇率 / Bug 修复奖励机 / 加班续命决策器 / 积分操盘手），综合「差异化 × 可落地 × 传播性」选定「麦门汇率」：只需 2~3 个只读 MCP 工具即可跑通，且 Big Mac Index 的梗自带传播属性。

### 2. Skill 开发

由 WorkBuddy 编写 `SKILL.md`：定义了从「查附近门店 → 取实时巨无霸价 → 收入换算 → 称号评级 → 输出汇率卡」的完整流程，以及错误兜底（401/429/门店不可用）和隐私准则。

### 3. 网页版演示

由 WorkBuddy 生成 `assets/exchange-card.html`：单文件零依赖网页版汇率卡生成器，让没有 MCP Token 的用户也能体验。

### 4. 参赛材料

由 WorkBuddy 整理 README.md、MCP_INTEGRATION.md、mcp-config.example.json，并原样引用官方 CONTEST_DECLARATION.md。

## 开发对话记录

> 按赛事要求附上使用 WorkBuddy 开发的完整对话记录（Markdown 导出）。

<!-- TODO（提交前替换）：在此处粘贴 WorkBuddy 完整开发对话的导出内容，
     或附上对话记录文件链接（如 conversation-2026-10-25.md） -->

## 一致性声明

本仓库中的 Skill 逻辑、MCP 调用流程与上述开发对话记录一致，未使用其他生成工具替代 WorkBuddy 完成核心开发。
