Example of a finished PR written with this template. Match its level of detail and tone. Do not copy its content.

---

**Title:** Fix invoice total when a percentage discount is applied

## Why

Invoices with a percentage discount could show a total off by 0.01 €, for example 99.99 € instead of 100.00 €. The code rounded the discount on each line, then added the rounded lines together. Fixes #42.

## What changed

- `computeInvoiceTotal()` applies the discount to the subtotal and rounds once, at the end.
- Added unit tests for 0 %, 10 % and 33 % discounts, including the 0.01 € case from the issue.

**Intentionally left unchanged**

- The PDF still prints a rounded amount on each line. Changing it would alter invoices already sent to clients. Tracked in #43.
- `formatCurrency()`, which has its own refactor open in #39.

## Validation and proof

- [x] Focused tests pass (`npm test -- invoice`: 12 passed)
- [x] Existing behavior is covered (no regression): full suite (`npm test`: 58 passed), including the 9 existing invoice tests, unchanged
- [ ] UI proof is attached (screenshot or recording), when relevant: N/A, no UI change
- [ ] A fresh reviewer or agent reviewed the diff: not yet, waiting for review

**Rollback:** easy. No schema or data change; reverting restores the old rounding for new invoices.
