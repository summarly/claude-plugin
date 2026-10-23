---
name: supplier-spend
description: Show who a business pays most in Summarly, how that spend has changed, and which supplier names look like the same company. Use when the user asks about suppliers, vendors, who they pay most, subscriptions, where money goes, or cutting costs.
---

# Supplier spend

1. **Period and company.** Default to the current year to date. With more than one workspace (`list_workspaces`), ask which and pass `workspace` on every call.
2. **Top suppliers.** Call `query_vendors` with the period and `limit: 20`. List the vendors by amount paid.
3. **Change against last year.** Call `aggregate` with `groupBy: "vendor"`, `direction: "expense"`, the period, and `compareTo` set to the same dates a year earlier. Name the biggest increases and decreases from `comparison.rows`, using each row's `change` and `changePercent`. Expenses are negative, so a negative change means more was spent.
4. **Recurring costs.** From the `aggregate` rows, point out vendors paid in most months (`months`) with a steady `perMonth`: these are likely subscriptions.
5. **Duplicates.** Compare the vendor names and `unlinkedPayees` from `query_vendors`; list any that look like the same supplier, so the user can link them on Summarly's Vendors page.

To see the payments behind a vendor, call `query_transactions` with `vendor` and the same period, and link each row with its `link`.
