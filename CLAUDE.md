# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install       # Install dependencies
npm run dev       # Start dev server at http://localhost:3000
npm run build     # Production build
npm run lint      # Run ESLint
npm run preview   # Preview production build
```

## Architecture

React 19 app built with Vite. `App.jsx` is the single stateful root; all UI is split into components under `src/components/`.

**Component structure:**
- `App.jsx` — holds the `transactions` array state and passes data/callbacks down. No UI of its own beyond the page shell.
- `components/Summary.jsx` — receives `transactions`, computes `totalIncome`, `totalExpenses`, and `balance` internally.
- `components/TransactionForm.jsx` — owns its own form state (`description`, `amount`, `type`, `category`). Calls `onAdd(transaction)` prop when submitted.
- `components/TransactionList.jsx` — receives `transactions`, owns its own `filterType` / `filterCategory` state internally.

**Transaction shape:** `{ id, description, amount (number), type ("income"|"expense"), category, date (YYYY-MM-DD) }`

**Data flow:** `App` owns the source-of-truth list. `TransactionForm` creates new entries via `onAdd`. There is no persistence; data resets on page refresh.

**Shared constant:** `categories` array is currently duplicated in `TransactionForm` and `TransactionList`.
