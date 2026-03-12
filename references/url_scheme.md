# iCost URL Scheme Reference

iCost registers `iCost://` and supports X-Callback-URL protocol.

## Add Expense
```
iCost://expense?[params]
```

## Add Income
```
iCost://income?[params]
```

## Add Transfer
```
iCost://transfer?[params]
```

## Common Parameters (expense / income)

| Param    | Required | Format                  | Notes                        |
|----------|----------|-------------------------|------------------------------|
| amount   | ✅       | 500 / 35.9              |                              |
| category | ✅       | 餐饮 / 交通              | Must exist in user's iCost   |
| currency | ❌       | CNY / USD               | Defaults to base currency    |
| account  | ❌       | 支付宝 / 微信钱包         | **MUST match exactly** — omit if unsure; validation fails if not found |
| date     | ❌       | 2019.10.10              |                              |
| time     | ❌       | 12:00 (24h)             |                              |
| remark   | ❌       | free text               |                              |
| tag      | ❌       | 标签1#标签2              |                              |
| discount | ❌       | 0.5 / 1                 | Discount amount              |
| claim    | ❌       | 0 / 1                   | Reimbursable                 |
| noBudget | ❌       | 0 / 1                   | Exclude from budget          |
| noCount  | ❌       | 0 / 1                   | Exclude from stats           |
| book     | ❌       | 宝宝账本                 | Defaults to default ledger   |

## Transfer Parameters

| Param        | Required | Notes                    |
|--------------|----------|--------------------------|
| amount       | ✅       |                          |
| from_account | ✅       | Must exist in iCost      |
| to_account   | ✅       | Must exist in iCost      |
| date         | ❌       | 2019.10.10               |
| remark       | ❌       |                          |
| fee          | ❌       | Transfer fee             |

## ⚠️ Key Rules

1. **Never include `account` unless you are certain it exists in the user's iCost** — validation is strict, wrong name = silent failure.
2. URL-encode all Chinese characters.
3. On macOS: trigger with `open "iCost://..."` in shell.
4. On iOS: send as tappable link; user taps to open iCost.

## Examples

```bash
# Expense (safe — no account)
open "iCost://expense?amount=22.55&currency=CNY&category=%E8%B4%AD%E7%89%A9&date=2026.03.12&remark=%E6%8B%BC%E5%A4%9A%E5%A4%9A%E8%AE%A2%E5%8D%95"

# Income
open "iCost://income?amount=100&currency=CNY&category=%E7%BA%A2%E5%8C%85&date=2026.03.12&remark=%E5%BE%97%E5%88%B0%E7%BA%A2%E5%8C%85"
```
