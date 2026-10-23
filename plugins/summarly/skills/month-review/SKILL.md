---
name: month-review
description: Review one month of a business's books in Summarly — what came in and went out, what changed against the month before, and what still needs doing before the month can be closed. Use when the user asks how a month went, to review or check a month, or what's left before handing a month to their accountant.
---

# Review a month

Work from Summarly's tools only. Every figure you state must come from a tool result; never add rows up yourself.

1. **Pick the month and the company.** Default to the last full month. If `list_workspaces` returns more than one workspace, ask which, and pass its id as `workspace` on every call.
2. **The month against the one before.** Call `aggregate` with `groupBy: "category"`, the month as `from`/`to`, and `compareTo` set to the previous month. Report `summary.income`, `summary.expenses` and the net, then, from `comparison.rows`, the three categories whose `change` is largest either way.
3. **What still needs doing.** Call `query_transactions` for the month three times:
   - `review: true` — still waiting in Summarly's Review tab;
   - `category: "Uncategorized"` — no category yet;
   - `receipt: "missing"` — payments that need a receipt and have none.
   For each, give `summary.matched` and the largest few rows, each linked with its `link`.
4. **Anything unusual.** Call `query_transactions` with `sort: "largest"` and `limit: 10`; mention any payment that is much larger than the month's others or to a vendor not seen before.
5. **Balances.** Call `query_accounts` and give `summary.cashBalance` (and `cardBalance` if there are cards).

Finish with a short checklist of what to fix in Summarly before the month is closed (Transactions → Review, then Monthly close). This connection is read-only: tell the user where to make a change, never offer to make it.
