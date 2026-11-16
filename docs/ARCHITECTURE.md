# Architecture and Refactoring Plan

> This document describes the current implementation and a proposed target structure. The target structure is not yet implemented.

## Current implementation

The application currently lives in `index (2).html` and contains:

- HTML markup for the dashboard, forms, charts, timeline, and summary.
- CSS for layout, responsive behaviour, and themes.
- JavaScript state for participants, expenses, selections, and editing.
- Split calculations for equal, exact, percentage, and weighted modes.
- Balance aggregation and settlement suggestions.
- Browser local-storage persistence.
- CSV export, print, summary copy, and share-link generation.

## Proposed target structure

```text
expense-splitter/
├── index.html
├── assets/
│   └── styles.css
├── src/
│   ├── app.js
│   ├── domain/
│   │   ├── money.js
│   │   ├── split.js
│   │   ├── balances.js
│   │   └── settlement.js
│   ├── storage/
│   │   └── local-store.js
│   └── ui/
│       ├── people-view.js
│       ├── expense-form.js
│       └── dashboard.js
├── tests/
│   ├── money.test.js
│   ├── split.test.js
│   ├── balances.test.js
│   └── settlement.test.js
└── README.md
```

## Module responsibilities

- `money.js`: convert user-entered decimal amounts to integer minor units and format them for display.
- `split.js`: implement equal, exact, percentage, and weighted allocation.
- `balances.js`: aggregate paid amounts, allocated shares, and net balances.
- `settlement.js`: calculate transfers that clear the group's net balances.
- `local-store.js`: handle versioned persistence and validate data before loading.
- `ui/`: render the interface and handle user interaction without owning financial rules.

## Invariants

1. Allocations for each expense must sum exactly to its total in integer minor units.
2. The sum of participant net balances must be zero after valid expenses and payments.
3. Expense and payment records must refer only to existing participants.
4. Imported or shared data must be validated before being trusted.
5. Settlement transfers must not exceed outstanding debts or credits.
6. Display formatting must not mutate underlying monetary values.

## Privacy and security

- Share links currently encode data using Base64; they do not encrypt it.
- Avoid putting sensitive information in share URLs.
- Validate imported JSON, participant references, numeric ranges, and payload size.
- If cloud synchronization is introduced, design authentication, authorization, retention, and deletion controls before collecting user data.
