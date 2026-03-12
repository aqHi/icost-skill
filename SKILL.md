---
name: icost
description: Record expenses in iCost via URL scheme or import file. Use when: (1) user sends a payment screenshot (WeChat Pay, Alipay, Pinduoduo, etc.) and wants to log it in iCost, (2) user says something like "帮我记一笔账" / "把这笔账记进iCost" / "记账", (3) user provides a WeChat Pay or Alipay bill export (.xlsx) for bulk import to iCost, (4) user asks to open iCost or add an entry. NOT for: generic expense tracking without iCost, CSV to other formats, bank statement analysis.
---

# iCost Skill

Record individual expenses via URL scheme, or bulk-import WeChat/Alipay bill exports.

## Workflow: Single Entry (screenshot or text)

1. Extract from screenshot or user message: **amount**, **date**, **merchant/product**
2. Determine category (see `references/categories.md`)
3. Build URL and trigger:

```bash
# macOS — triggers iCost directly
open "iCost://expense?amount=22.55&currency=CNY&category=购物&date=2026.03.12&remark=拼多多订单"
```

On iOS: send as a tappable `iCost://...` link; user taps to open iCost.

**⚠️ Never include `account` parameter unless you are 100% certain it exists in the user's iCost** — wrong name causes silent failure. See `references/url_scheme.md` for all parameters.

## Workflow: Bulk Import (WeChat bill export)

WeChat Pay exports `.xlsx` with 16 metadata rows + header on row 17, data from row 18.

```bash
python3 scripts/wechat_to_icost.py input.xlsx output_icost.xlsx
```

Requires `openpyxl`. Install via: `pip install openpyxl` (or use a venv).

Output is an iCost-compatible `.xlsx`. Import in iCost: **设置 → 数据导入**.

After conversion, review any rows labeled `待分类` and fix their categories manually.

## Category Rules

See `references/categories.md` for keyword→category mapping.

Default categories used (adjust to match user's actual iCost setup):
`餐饮` `购物` `交通` `居家` `运动` `医疗` `娱乐` `金融` `通讯` `教育` `个护` `转账` `其他`

## URL Scheme Quick Reference

| Action   | URL prefix          |
|----------|---------------------|
| Expense  | `iCost://expense?`  |
| Income   | `iCost://income?`   |
| Transfer | `iCost://transfer?` |

Required: `amount` + `category` (expense/income); `amount` + `from_account` + `to_account` (transfer).  
Date format: `2019.10.10` · Time: `12:00` (24h)  
Full reference: `references/url_scheme.md`

## Tips

- **先用后付** orders: record when payment actually clears, or note in remark
- **Refunds** (`退款`): record as `收入 / 其他 / 退款`
- **Personal transfers** (`转账`): use `iCost://transfer` with `from_account` + `to_account` when accounts are known
- URL-encode Chinese in shell: use Python `urllib.parse.quote()` or pre-encode manually
