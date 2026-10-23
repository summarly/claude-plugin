---
name: cash-position
description: Report a business's cash position from Summarly — the balance in each bank account, card and cash pot, the total, and how money in and out has moved over recent months. Use when the user asks how much money they have, about cash, balances, burn, runway or whether they can afford something.
---

# Cash position

1. **Company.** With more than one workspace (`list_workspaces`), ask which and pass `workspace` on every call.
2. **Balances.** Call `query_accounts`. List each account with its `balance` (and `balanceInBaseCurrency` when it is in another currency), then `summary.cashBalance`. Credit cards are a liability, totalled separately as `cardBalance`; never add them to cash. If `summary.accountsConvertedAtTodaysRate` is above zero, say the total includes balances converted at today's rate. An account whose `includedInTotals` is false is quoted in its own currency and left out of the total — say so.
3. **The trend.** Call `aggregate` with `groupBy: "month"` over the last three full months plus this month so far. Give income, expenses and net for each month from the rows, and `summary.perMonth` for the average. Say plainly that the current month is partial and isn't a trend.
4. **If they ask about runway or affording something,** use only those figures: cash today against the average monthly net outflow. If the business is cash-positive on average, say so instead of computing a runway.

Every number comes from a tool result. Don't forecast invoices or bills: this connection can't read them.
