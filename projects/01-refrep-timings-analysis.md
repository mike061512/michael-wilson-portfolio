# RepRef Timings Report & Error Code Proof of Concept

**Role:** Sr. Site Reliability Engineer, Oracle America, Inc.  
**Analysis Window:** 154 days (Jan 2024 – Jun 2024)  
**Tools:** Python, SQL, Oracle RDBMS, Excel

---

## The Problem

A core operational workflow — the replicate and refresh (rep/ref) process — was generating frequent failures with no structured way to understand them. Engineers handled each failure in isolation: no standard error codes, no shared catalog, no way to analyze which failure types were consuming the most time or occurring most frequently.

The result was repeated rediscovery of known problems, siloed remediation knowledge, and no data to support prioritization conversations with engineering or leadership.

---

## What I Did

### Data Collection & Analysis

- Collected timing and event data across **447 process runs** and **8,157 events** over a 154-day window
- Analyzed event outcomes, durations, and failure rates to produce the first quantified picture of process health
- Mapped **3,911 failure events** to structured error codes, enabling frequency analysis and time attribution by error type

### Error Code Proof of Concept

- Demonstrated a method for mapping raw error messages to unique, categorized error codes at scale
- Designed a proposed error catalog structure: error-to-code mapping, grouping and reporting capabilities, per-error reference pages, and ticketing system integration
- Authored a formal PoC document outlining implementation approach, cross-team benefits, and next steps

### Reporting & KPI Design

- Produced a timing summary report with findings organized for both engineering and leadership audiences
- Proposed an OKR/KPI framework for ongoing rep/ref health tracking (error rate, lead time, MTTR by error category)
- Outlined a path toward repeatable monthly and quarterly analysis runs

---

## Key Findings

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
- Established a **repeatable analysis approach** that could be executed on a monthly or quarterly cadence without rebuilding from scratch
- Created the foundation for cross-team engagement with engineering on error prioritization and catalog development

---

## Skills Demonstrated

- Operational data collection and analysis at scale
- Structured error classification and cataloging design
- Quantitative problem framing for engineering and leadership audiences
- KPI and OKR definition for service health tracking
- Proof-of-concept documentation and cross-team stakeholder communication