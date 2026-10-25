# MCP 接入说明

本项目通过麦当劳官方 MCP Server（Streamable HTTP）接入麦当劳核心能力，实现「以巨无霸为锚定货币」的实时购买力换算。

## 一、申请 Token

1. 打开麦当劳 MCP 开放平台：https://open.mcd.cn/mcp
2. 手机号 / 扫码登录
3. 右上角进入「控制台」→ 激活申请 Token → 同意服务协议 → 复制 Token

> 限流：每个 Token 每分钟最多 600 次请求，超限返回 429。本 Skill 每次运行只调用 2~3 个工具，远低于限额。

## 二、MCP Server 配置

接入地址：`https://mcp.mcd.cn`
传输协议：Streamable HTTP
认证方式：请求头 `Authorization: Bearer <YOUR_MCP_TOKEN>`

完整配置见 [mcp-config.example.json](mcp-config.example.json)。**请勿在仓库中提交真实 Token**，推荐通过环境变量注入：

```json
{
  "mcpServers": {
    "mcd-mcp": {
      "type": "streamablehttp",
      "url": "https://mcp.mcd.cn",
      "headers": {
        "Authorization": "Bearer ${MCD_MCP_TOKEN}"
      }
    }
  }
}
```

## 三、本 Skill 实际调用的工具

| 步骤 | 工具 | 参数 | 说明 |
|---|---|---|---|
| 1 | `query-nearby-stores` | `searchType=2, city, keyword, beType=1` | 按城市/位置关键词查附近到店门店，取 `storeCode` |
| 2 | `query-meals` | `storeCode, orderType=1, beType=1` | 拉取门店在售菜单，定位「巨无霸」及价格 |
| 3 | `query-meal-detail` | `code, storeCode` | （可选）套餐歧义时确认单点价 |
| 4 | `calculate-price` | `storeCode, orderType, beType, items[{productCode, quantity:1}]` | （兜底）精确计算单点总价 |

不调用下单、领券、积分等写入类工具，Skill 为纯只读查询。

## 四、调用流程

```
用户输入城市/薪资
      │
      ▼
query-nearby-stores ──► storeCode
      │
      ▼
query-meals ──► 巨无霸 BIGMAC_PRICE（实时价）
      │        （歧义时 query-meal-detail / calculate-price 兜底）
      ▼
本地计算：
  BIGMAC_PER_HOUR  = 时薪 ÷ BIGMAC_PRICE
  BIGMAC_PER_MONTH = 月薪 ÷ BIGMAC_PRICE
  WORK_MINUTES     = BIGMAC_PRICE ÷ 时薪 × 60
      │
      ▼
称号评级 + 生成麦门汇率卡
```

## 五、错误处理

| code | 含义 | Skill 行为 |
|---|---|---|
| 401 | Token 无效/过期/未携带 | 提示用户重新检查 Token 配置 |
| 429 | 超过限流 | 提示稍后重试 |
| 门店/餐品查询失败 | 非营业时间、城市无覆盖 | 允许用户手输价格，标注「非实时价」 |

## 六、数据与隐私

- Skill 不存储、不上传用户薪资数据，仅在本对话内完成换算
- Token 通过环境变量注入，仓库内不含任何真实凭证
- 价格数据以麦当劳官方渠道实时返回为准
