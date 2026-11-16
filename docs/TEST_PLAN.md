# Test Plan

> This is a proposed test plan. It has not yet been executed as an automated suite against this repository.

## Monetary values and rounding

- Convert decimal input such as `99.99` to an integer representation of 9999 minor units.
- Reject empty, non-numeric, zero, and negative expense amounts.
- Split a total that is not evenly divisible (for example, 100 minor units among 3 people) and verify that the shares sum exactly to the total.
- Verify very small totals and large supported totals.

## Split modes

### Equal
- Selected participants receive equal or remainder-adjusted shares.
- Unselected participants receive no share.
- Allocations sum exactly to the expense total.

### Exact amounts
- Accept allocations whose sum equals the expense total.
- Reject totals that are too small or too large.
- Reject negative and non-numeric values.

### Percentages
- Accept percentages totalling 100% within the documented tolerance.
- Reject invalid totals and negative values.
- Verify deterministic handling of rounding remainders.

### Weighted shares
- Verify proportional allocation for weights such as 2:1.
- Reject zero, negative, and non-numeric weights.
- Verify that allocated minor units sum exactly to the original expense.

## Balances and settlement

- The payer receives credit for the amount paid.
- Participants receive debits equal to their allocated shares.
- Net balances sum to zero.
- Settlement output clears all positive and negative balances.
- A settled group produces no additional transfers.
- Recording a payment updates balances correctly.

## Persistence and share links

- Valid saved state reloads correctly.
- Malformed JSON and malformed encoded data are rejected safely.
- Unknown participant IDs are rejected or handled without corrupting balances.
- Oversized payloads are rejected.
- Documentation clearly states that Base64 is encoding, not encryption.

## Browser and accessibility checks

- Test current desktop and mobile browser layouts.
- Test keyboard-only navigation and visible focus.
- Verify form labels and accessible names.
- Test CSV export with commas, quotes, and non-ASCII names.
- Verify graceful behaviour when local storage is unavailable.
