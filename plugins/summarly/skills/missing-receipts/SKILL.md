---
name: missing-receipts
description: Find payments in Summarly that need a receipt and don't have one, grouped by vendor with the biggest first, and say how to close the gaps. Use when the user asks about missing receipts, what receipts to chase, documents their accountant needs, or why a month isn't ready.
---

# Chase missing receipts

1. **Period and company.** Default to the current year to date. With more than one workspace (`list_workspaces`), ask which and pass `workspace` on every call.
2. **The gaps.** Call `query_transactions` with `receipt: "missing"`, the period, `sort: "largest"` and `limit: 100`. Report `summary.matched` and, from `summary.byCurrency`, the total they add up to. If `summary.shown` is less than `summary.matched`, say you're showing the largest `shown`.
3. **By vendor.** Group the rows you were given by `vendor` and list each vendor with how many payments and the dates, biggest first, linking each payment with its `link`. If the user wants only larger payments, use `minAmount` rather than filtering yourself.
4. **Waiting to be confirmed.** Call `query_transactions` with `receipt: "suggested"` for the same period: these already have a receipt proposed and only need confirming in Summarly's Review tab.

Then tell the user how to close the gaps: forward the receipt to the workspace's receipt email, snap it with the phone, or upload it in Summarly; Summarly matches it to the payment. A category that never needs a receipt can be marked so in Summarly. This connection is read-only, so you can't attach anything yourself.
