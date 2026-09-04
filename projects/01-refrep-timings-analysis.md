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
- **Now producing a richer KPI set for leadership on every run:** beyond the original error-code frequency/time attribution, the pipeline now automatically computes taxonomy coverage, elapsed-time percentiles (median/P90), a failure-runtime-to-total-elapsed ratio, and a workflow-deviation rate — metrics the manual 2024 PoC had no repeatable way to produce

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

## Key Findings (Current Automated Run — 12-Month Window)

The most recent automated run covers a full 12-month window (2025-09-04 through 2026-09-04) and produces a materially richer KPI set than the 2024 PoC could — this is the current picture leadership sees:

| Metric | Value |
|---|---|
| Projects analyzed | 670 |
| Timing events processed | 8,580 |
| Failed events | 3,164 (36.9% failed-event rate) |
| Automated taxonomy coverage | **94.4%** (2,986 of 3,164 failed events auto-classified; only 178 need manual review) |
| Total failed-step runtime | ~3,507 hours |
| Unclassified inter-step elapsed time | ~60,196 hours |
| Median completed-project elapsed time | 61h 12m |
| P90 completed-project elapsed time | 217h 31m |
| Failed-step runtime as share of completed-project elapsed | 6.6% |
| Workflow-deviation rate | **94.7%** of assessed projects show at least one deviation from the expected step path |

**What the new metrics reveal that the 2024 PoC couldn't:**

- **Automation now does the categorization work.** 94.4% of failed events are auto-classified against the error taxonomy on every run — versus a one-time manual mapping exercise in 2024 — with only 178 events left for analyst review.
- **The prioritization story has shifted.** Explicit failures account for only 6.6% of completed-project elapsed time, but unclassified inter-step elapsed time is more than 17x larger than total failed-step runtime. The biggest lever for shortening the process isn't failure remediation alone — it's instrumenting the large, currently-unclassified gaps between steps.
- **Workflow deviation is now visible, and it's pervasive.** 94.7% of assessed projects deviate from the expected step path (a missing required step, an out-of-order step, or a repeated non-repeatable step) — a finding the 2024 PoC had no mechanism to surface at all.
- **The same failure-concentration pattern from 2024 still holds**, but is now recalculated automatically every run instead of once by hand: a small number of error categories (remote export/import errors, DDL execution errors, missing table/view references) account for the majority of failed-step runtime.

---

## Impact

- **First structured, quantified view** of how much time was lost to failures in this process — previously unmeasured
- Converted the one-off 2024 PoC into a repeatable, automated pipeline that now runs over a full 12-month window and re-derives its findings on every execution, instead of a single hand-built snapshot
- Delivered a materially richer, leadership-facing KPI set — elapsed-time percentiles, a workflow-deviation rate, and automated taxonomy coverage — that the manual PoC had no repeatable way to produce
- Surfaced a new, higher-value prioritization insight: unclassified inter-step time now dwarfs explicit failure time, redirecting the conversation from "reduce failures" toward "instrument the gaps between steps"
- Demonstrated that a small number of high-frequency error types continue to drive a disproportionate share of lost time — a durable, defensible prioritization target reconfirmed automatically rather than re-derived by hand
- Extended the Vertica MCP server — originally built for ad hoc self-service queries — into a second, proven production use case
- Eliminated a class of report-corruption risk through staged, atomic publication with automatic fallback to the last good output

---

## Skills Demonstrated

- Operational data collection and analysis at scale
- Structured error classification and cataloging design
- Quantitative problem framing for engineering and leadership audiences
- KPI and OKR definition for service health tracking, including percentile-based (median/P90) elapsed-time and workflow-deviation metrics
- Pipeline design: automated extract → validate → classify → report
- Safe, boundary-first production data-access design (building on prior MCP server work)
- Defensive data handling: receipt/schema/checksum validation, atomic fail-safe publication
- Automated test discipline across two coordinated repositories (197 total passing tests)
