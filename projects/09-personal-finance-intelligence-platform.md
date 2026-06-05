# Personal Finance Intelligence Platform

**Type:** Personal Side Project  
**Timeline:** May 2026  
**Tools:** Python, Power BI, DAX, openpyxl, PyYAML, PyInstaller, Git, Claude Code (Anthropic)

---

## Overview

Built an end-to-end personal finance data platform from scratch — a Python ETL pipeline combined with a multi-page Power BI analytics report. The system ingests CSV exports from two financial institutions, normalizes and categorizes transaction data, merges it into a structured Excel ledger, and surfaces actionable insights through a suite of purpose-built dashboards.

Built iteratively using AI-assisted development (Claude Code), treating it as a real engineering engagement: requirements gathering, architecture design, implementation, live data testing, and incremental feature delivery.

---

## System Architecture

```
Bank CSV Exports
      │
      ▼
Python ETL Pipeline
  ├── importer.py     → parse + clean per institution
  ├── categorizer.py  → apply YAML category rules
  ├── merger.py       → idempotent dedup + merge
  └── workbook.py     → read/write structured Excel ledger
      │
      ▼
ledger.xlsx (per-account tabs + Summary)
      │
      ▼
Power BI Report (9 pages, DAX measures, calculated columns)
```

---

## Python ETL Pipeline

### Data Ingestion & Normalization
- Parses CSV exports from two institutions with different column schemas, date formats, and encoding conventions
- Two-stage description cleaning: YAML-driven override map for known merchants, then heuristic cleaner for routing numbers, processor prefixes, store numbers, and city/state segments
- Handles 3-row metadata headers, negative debit conventions, internal transfer resolution, and check number extraction

### Merge & Deduplication
- **Idempotent pipeline**: re-running on already-imported data produces no duplicates
- Dedup key: `(date, debit_amount, credit_amount)` — description excluded so user-edited descriptions survive re-imports
- Counter-based deduplication correctly handles N identical transactions on the same date as N distinct events
- Manually entered rows (pending expenses, forecasts, opening balances) are preserved across every run

### Configuration-Driven Design
- `config/categories.yaml` — 27 spending categories, order-sensitive keyword rules
- `config/descriptions.yaml` — 186 merchant override entries
- No code changes required to add merchants or adjust categorization — edit YAML and re-run

### Packaging
- Packaged as a Windows `.exe` via PyInstaller — zero Python installation required for end users

---

## Power BI Analytics Layer

Nine-page report with custom DAX measures and calculated columns:

| Page | Purpose |
|---|---|
| Overview | Cross-account summary: spend by category, credit/debit tables, month-to-month trend |
| Monthly Breakdown | Month selector with totals, category bar chart, current vs. prior month |
| Bills | KPI cards for Bills, Utilities, Insurance, Subscriptions; month-to-month charts per sub-category |
| Gas & Groceries | Focused spend tracking with average and combined trend line |
| Transaction Metrics | Full debit drill-down with five slicers for ad-hoc analysis |
| Account Balances | Ending monthly balance per account + total across all accounts (cumulative DAX) |
| Monthly Recurring | Recurring charge audit: items active in 2+ consecutive months with avg, most recent, YTD |
| Uncategorized Items | QA page: flags transactions the pipeline could not categorize |
| Kids Gaming | Pivot table tracking per-child gaming spend (Playstation, Roblox) |

### Key DAX Engineering
- **Recurring charge detection**: `SUMMARIZE` over Account + Description, counts distinct Year+Month occurrences, surfaces items active in 2+ months
- **Cumulative account balance**: reconstructed from opening balance rows + cumulative transaction history — no dependency on Excel formula columns
- **Cross-year month counting**: `COUNTROWS(SUMMARIZE(..., Year, Month#))` to distinguish January 2025 from January 2026
- **HASONEVALUE pattern**: applied to all per-row measures to suppress meaningless total row aggregations

---

## Outcomes

- **Subscription audit**: recurring charge detection surfaced an unused sports club membership ($309 YTD) — immediately cancelled
- **Anomaly detection**: account balance chart surfaced a ~$33K single-month balance drop, prompting review of large one-time expenses
- **Spend visibility**: identified that a single merchant (Amazon, 99 transactions) represents ~5.8% of all YTD debit spend
- **Process efficiency**: what previously required manual CSV review now runs in seconds via a single Windows executable

---

## Skills Demonstrated

- Python ETL pipeline design (multi-source normalization, idempotent merge, configuration-driven architecture)
- DAX measure development (filter context management, cumulative calculations, recurring pattern detection)
- Power BI report design and data modeling
- openpyxl workbook generation with conditional formatting and formula strings
- PyInstaller packaging for non-technical end users
- AI-assisted development with iterative live-data testing (Claude Code)
- Financial data modeling and anomaly detection