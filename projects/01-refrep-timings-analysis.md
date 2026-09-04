# RefRep Timings Report: From Manual PoC to Automated V1 Pipeline

**Role:** Sr. Site Reliability Engineer, Oracle America, Inc.
**Timeline:** 2024 – Present
**Tools:** Python, SQL, Oracle RDBMS, Excel, Vertica, MCP (Model Context Protocol), PyTest

---

## The Problem

A core operational workflow — the replicate and refresh (rep/ref) process — was generating frequent failures with no structured way to understand them. Engineers handled each failure in isolation: no standard error codes, no shared catalog, no way to analyze which failure types were consuming the most time or occurring most frequently.

The result was repeated rediscovery of known problems, siloed remediation knowledge, and no data to support prioritization conversations with engineering or leadership. The first version of this work (2024) was a manual, one-off proof of concept — it proved the value of the analysis but had to be rebuilt from scratch every time it ran.

---

## What I Did

### 2024: Data Collection & Analysis (Proof of Concept)

- Collected timing and event data across **447 process runs** and **8,157 events** over a 154-day window
- Analyzed event outcomes, durations, and failure rates to produce the first quantified picture of process health
- Mapped **3,911 failure events** to structured error codes, enabling frequency analysis and time attribution by error type
- Demonstrated a method for mapping raw error messages to unique, categorized error codes at scale, and authored a formal PoC document outlining a proposed error catalog and next steps
- Produced a timing summary report and proposed an OKR/KPI framework for ongoing rep/ref health tracking

### 2026: Automated V1 Pipeline Uplift

Rebuilding the manual PoC into a repeatable, operator-run pipeline, built on the [Vertica read-only MCP server](13-vertica-mcp-server.md) I had already built:

- **Automated export:** the MCP server performs the data export for a provided date range directly against Vertica — fixed export datasets, parameterized half-open date bounds, named approved exclusion profiles — replacing the manual one-off SQL pulls from the 2024 PoC
- **Automated validation:** export receipts, CSV schema, checksums, row counts, and date-interval contracts are validated before any analysis runs
- **Automated classification:** lifecycle state, workflow path and deviations, diagnostic evidence, and error-taxonomy categorization now run automatically — closing the biggest manual gap from the 2024 PoC, where error-to-code mapping was done by hand
- **Atomic, fail-safe publish:** artifacts are staged before atomically replacing the local `latest` output, so a failed or partial run never overwrites a good one; found and fixed an Excel-only edge case where source text containing XML-forbidden control characters could break the workbook export
- **Tested and proven:** 161 report-repository tests and 36 MCP-repository tests passing; validated end to end against an approved, read-only six-month production data run (2026-03-03 through 2026-09-03)

**Still in progress:** the visualization/reporting layer. Data collection, validation, and error categorization are automated and proven end to end — the presentation layer on top of the Markdown/Excel output is still being built out.

---

## Key Findings (2024 PoC Baseline)

| Metric | Value |
|---|---|
| Total processes analyzed | 447 across 154 days |
| Total events tracked | 8,157 |
| Failure events mapped | 3,911 (48% of all events) |
| Failure share of per-process tracked time | **59%** (151,980 minutes / 2,533 hours) |
| Failure share of total 154-day observation window | **69%** |
| Average process duration | 576 minutes (~10 hours) |
| Average failure time per process | 340 minutes (~6 hours) |
| Top error category (by time) | CREATE COPY OF DATABASE — 874 errors, 1,835 hours, **72% of all error time** |
| Single highest-impact error code | RR-1056 (372 occurrences) — 49% of time in that category |
| Second highest-impact error code | RR-1090 (150 occurrences) — 363 hours, 14% of total error time |

---

## Impact

- **First structured, quantified view** of how much time was lost to failures in this process — previously unmeasured
- Gave leadership a concrete figure (69% of operational time consumed by failures) to anchor investment conversations about error reduction
- Demonstrated that a small number of high-frequency error types drove a disproportionate share of lost time — creating a clear, defensible prioritization target
- Converted the one-off 2024 PoC into a repeatable, automated pipeline: what previously required manual SQL, manual error mapping, and manual report assembly now runs on demand against a validated, read-only data boundary
- Extended the Vertica MCP server — originally built for ad hoc self-service queries — into a second, proven production use case
- Eliminated a class of report-corruption risk through staged, atomic publication with automatic fallback to the last good output

---

## Skills Demonstrated

- Operational data collection and analysis at scale
- Structured error classification and cataloging design
- Quantitative problem framing for engineering and leadership audiences
- KPI and OKR definition for service health tracking
- Pipeline design: automated extract → validate → classify → report
- Safe, boundary-first production data-access design (building on prior MCP server work)
- Defensive data handling: receipt/schema/checksum validation, atomic fail-safe publication
- Automated test discipline across two coordinated repositories (197 total passing tests)
