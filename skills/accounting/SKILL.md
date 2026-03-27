# Skill: accounting

## Purpose

Maintain plain-text books and generate financial statements from `main.ledger`.

## Repository Layout

- `main.ledger` - root file with include statements
- `imports/<YEAR>/` - normalized journal entries
- `transaction-imports/<YEAR>/` - raw exports
- `expenses/<YEAR>/` - invoices and receipts
- `reports/<YEAR>/` - generated report outputs

## Core Method

- Use double-entry postings only.
- Preserve source traceability in memos/payee text.
- Keep account naming stable over time.
- Record owner-funded business costs into an equity contribution account when applicable.

## Workflow

1. Review raw source files in `transaction-imports/<YEAR>/` and `expenses/<YEAR>/`.
2. Convert to normalized entries in `imports/<YEAR>/*.ledger`.
3. Update `main.ledger` include statements if needed.
4. Run ledger validation commands.
5. Generate financial reports into `reports/<YEAR>/`.

## Validation Commands

```bash
ledger -f main.ledger bal
ledger -f main.ledger reg
```

Books must balance to zero globally.

## Financial Statements

Profit and Loss:

```bash
ledger -f main.ledger bal Income Expenses --period "from <start> to <end>"
```

Balance Sheet:

```bash
ledger -f main.ledger bal Assets Liabilities Equity --period "to <as-of-date>"
```

## Output Contract

For a requested period/year, return:

1. files created or updated
2. validation outputs
3. P&L totals
4. balance sheet totals
5. unresolved classification assumptions
