# Summarly for Claude

Ask about your books from your own Claude chats. This plugin connects Claude to [Summarly](https://summarly.com), the back office for small businesses, and adds four workflows Claude follows when you ask for them.

## What's inside

- **The Summarly connector** (`https://summarly.com/api/mcp`). Read-only: Claude can find and total transactions, list your accounts and balances, your categories and your vendors. It can't change anything in Summarly.
- **Skills:**
  - **month-review**: how a month went against the one before, and what's left before it can be closed.
  - **missing-receipts**: payments that need a receipt and don't have one, by vendor, biggest first.
  - **cash-position**: balances across accounts and how money in and out has moved.
  - **supplier-spend**: who you pay most, what changed, likely subscriptions, and duplicate supplier names.

## Getting started

1. Install the plugin, then open its **Connectors** tab and connect **Summarly**.
2. Sign in to Summarly and tick the workspaces Claude may read.
3. Ask, for example: "Review September", "Which receipts am I missing this year?", "What's my cash position?", "Who are my biggest suppliers?"

You need a Summarly account on Premium (every feature is open during early access). The workspace's owner can turn AI apps off, or disconnect anyone, under Settings → Members. You can disconnect any time under Settings → Connected apps.

More: [summarly.com/mcp](https://summarly.com/mcp). Questions: founders@summarly.com.
