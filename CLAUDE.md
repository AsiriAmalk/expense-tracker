# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev      # Start dev server at http://localhost:5173
npm run build    # Production build
npm run lint     # Run ESLint
npm run preview  # Preview production build
```

**Note:** Requires Node.js 20.19+ or 22.12+. If using nvm: `nvm use 22`.

## Architecture

React app with no routing or state management libraries. `transactions` state lives in `App` and is passed down as props. There are no shared utilities or context.

- `src/App.jsx` — root component; owns `transactions` state and `handleAdd`, composes child components
- `src/Summary.jsx` — receives `transactions`, calculates and displays `totalIncome`, `totalExpenses`, and `balance`
- `src/AddTransaction.jsx` — owns its own form state (`description`, `amount`, `type`, `category`), calls `onAdd` prop with new transaction
- `src/TransactionList.jsx` — receives `transactions`, owns its own filter state (`filterType`, `filterCategory`), renders filtered table
- `src/App.css` — component styles
- `src/index.css` — global styles
- `src/main.jsx` — React root mount

The `categories` array is duplicated in `AddTransaction` and `TransactionList` — a candidate for future extraction to a shared constants file.

### Data flow for deletion
`App` passes `handleDelete` as `onDelete` to `TransactionList`. Each row has a Delete button that triggers `window.confirm` before calling `onDelete(t.id)`, which filters the transaction out of state. Summary totals update automatically since `Summary` derives its values from the same `transactions` prop.
