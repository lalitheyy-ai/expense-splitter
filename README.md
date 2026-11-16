# KitKat — Expense Splitter

A browser-based group expense splitter built by Team 7. It helps a group record shared expenses, understand who owes whom, and find a compact set of payments to settle balances.

> **Project status:** Hackathon prototype. This repository currently contains a single-file, client-side implementation. The documentation below describes the code currently present and identifies future improvements separately.

## Features in the current implementation

- Add participants and record expenses.
- Split expenses equally, by exact amounts, by percentage, or by weighted shares.
- Calculate participant totals: amount paid, fair share, and net balance.
- Generate settlement suggestions by matching debtors with creditors.
- Record settlement payments.
- Search the expense timeline.
- Export expenses as CSV.
- Copy a text summary or shareable group link.
- Print the summary.
- Switch between light and dark themes.
- Save data in browser local storage.

## Run locally

The current implementation does not require a build system or package installation.

1. Clone this repository.
2. Open `index (2).html` in a modern browser.

The source filename is retained as it currently exists in the repository. A future cleanup may rename it to `index.html`, after checking any deployment references.

## Implementation notes

- Monetary calculations use integer minor units (cents/paise-style units) to reduce floating-point rounding errors.
- The application is client-side and uses browser local storage. The current code does not implement user accounts, a backend, or cloud synchronization.
- The share-link feature Base64-encodes serialized group data. **Base64 is not encryption**; anyone with the link can decode its contents. Do not use the link for sensitive financial or personal information.
- The current UI, styles, application state, and business logic are contained in one HTML file.

## Documentation

- [Architecture and proposed refactoring](docs/ARCHITECTURE.md)
- [Test plan](docs/TEST_PLAN.md)

These documents distinguish the current implementation from proposed future work. The test plan is a plan, not a claim that an automated test suite already exists.

## Roadmap

1. Extract split, balance, and settlement logic into independent modules.
2. Add automated tests for monetary rounding and split invariants.
3. Validate data imported from share links before using it.
4. Improve accessibility and browser coverage.
5. Add continuous integration once the test runner is in place.

## Team and attribution

This project was developed in a team context. Add the verified names and contributions of each team member before presenting individual ownership or inviting external contributions.

## Licence

No licence is declared in this repository yet. All rights are reserved by default until the project owners choose and add a licence.
