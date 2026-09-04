# RefRep Process Timings V1: Automated Reporting Pipeline

**Role:** Sr. Site Reliability Engineer, Oracle America, Inc.
**Timeline:** 2026 (building on the 2024 timings PoC)
**Tools:** Python, Vertica, MCP (Model Context Protocol), PyTest, Excel/Markdown reporting, Windows CLI

---

## The Problem

The [2024 RefRep timings analysis](01-refrep-timings-analysis.md) proved that structured, quantified reporting on the replicate/refresh (rep/ref) process was valuable — but it was a one-off, manually assembled proof of concept. There was no repeatable path to rerun that analysis safely on a recurring basis: no validated data-access boundary, no standardized artifact format, and no automated safeguards against publishing a bad or partial report.

---

## What I Did

### Built on a safe data-access boundary

Used the [Vertica read-only MCP server](13-vertica-mcp-server.md) I had already built as the sole data-access path for this workflow — fixed export datasets, parameterized half-open date bounds, named approved exclusion profiles, and server-controlled output paths. No ad hoc SQL, no broad table access, no credentials stored in the repository.

### Designed a validate-before-trust pipeline

- Validated export receipts, CSV schema, checksums, row counts, and date-interval contracts before any analysis ran
- Classified each process run's lifecycle state, workflow path and deviations, diagnostic evidence, and taxonomy-backed error categories
- Preserved observed event chronology and distinguished directly observed facts from workflow expectations, rather than inferring missing context

### Built an atomic, fail-safe publish model

- Staged all four output artifacts (aggregate findings and timing events, each in Markdown and Excel) before atomically replacing the local `latest` output
- Guaranteed the prior successful output is preserved if staging or publication fails, so a bad run never overwrites a good one
- Found and fixed an Excel-only edge case where source text containing XML-forbidden control characters would break the workbook — added boundary-level encoding so a source-text anomaly can't produce an unhandled export error
- Repaired the generic MCP table-listing query so it requests only the Vertica catalog columns the target environment actually supports

### Validated end to end

Ran an approved, read-only six-month production proof (2026-03-03 through 2026-09-03) that published all four expected artifacts successfully after the Excel fix, with a sanitized full test suite passing across both repositories — 161 report-repository tests and 36 MCP-repository tests.

---

## Current State

V1 is implemented, tested, and proven against real production data end to end. It is deliberately scoped as a local, operator-run tool — not a scheduler, dashboard, or email delivery system, and not a broader options-analysis solution. Those are separate, explicitly deferred investment decisions (scheduled execution, Power BI/Grafana presentation, Linux/Jenkins execution), not unfinished parts of the current capability.

Per the project's own data-handling standard, no credentials, source rows, or report contents are retained in project documentation — including here. The value demonstrated is the repeatable *process*: validated extraction, safe classification, and atomic publication.

---

## Impact

- Converted a one-off analysis into a repeatable, operator-led reporting workflow that can be rerun on demand without rebuilding anything from scratch
- Extended the Vertica MCP server from a single ad hoc use case into a proven second production workflow, validating the read-only boundary design under real operational load
- Eliminated a class of report-corruption risk (partial writes, bad Excel exports) through staged, atomic publication with automatic fallback to the last good output
- Kept the entire workflow inside strict data-handling controls — read-only access, credential isolation, allowlisted context — while still delivering full lifecycle, deviation, and failure-taxonomy reporting

---

## Skills Demonstrated

- End-to-end pipeline design: extract → validate → classify → report → atomically publish
- Safe, boundary-first production data-access design (building on prior MCP server work)
- Defensive data handling: receipt/schema/checksum validation, control-character edge cases, fail-safe publication
- Dual-format (Excel + Markdown) automated reporting
- Automated test discipline across two coordinated repositories (197 total passing tests)
- Honest scoping — clearly separating delivered capability from deferred future investment
