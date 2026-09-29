# Vertica Read-Only MCP Server

**Role:** Sr. Site Reliability Engineer, Oracle America, Inc.
**Timeline:** July 2026
**Tools:** Python, MCP (Model Context Protocol), Vertica, Codex, Git

---

## The Problem

Our team lands an enormous amount of operational and client data in Vertica, but getting at it required either writing ad hoc SQL by hand or asking someone else to run a one-off lookup. Managers and engineers who wanted to explore the data self-service had no safe, low-friction way to do it — and any solution had to avoid distributing shared credentials or opening the door to unreviewed writes.

Leadership asked me to build a way for the team to use Codex to connect to and query Vertica directly.

---

## What I Did

Designed and built `vertica-readonly-mcp`, a local STDIO MCP server that gives Codex controlled, read-only access to Vertica:

- **Defined a safe operating boundary first:** each user connects with their own already-approved, read-only Vertica account through local environment variables — no shared credentials, no elevated access.
- **Built only the retrieval surface needed:** four tools — `list_schemas`, `list_tables`, `describe_table`, `query_readonly` — covering catalog discovery and bounded ad hoc queries.
- **Layered in defense in depth:** SQL validation permits exactly one comment-free `SELECT` statement, results are capped at 500 rows, catalog lookups are parameterized, and every MCP tool is marked read-only. Errors are handled generically so driver details and connection internals never leak back through MCP responses.
- **Made it reproducible:** a single cross-platform Python bootstrap script (Windows, Intel macOS, Apple Silicon) creates the virtual environment, installs dependencies, and runs the test suite.
- **Made it manager-ready:** wrote credential-free Codex configuration examples, onboarding steps, and troubleshooting guidance so non-engineers could set it up without help.

---

## Current State

Shipped as a working local MCP integration: Python 3.11+ packaging with a `vertica-readonly-mcp` console command, Windows and macOS setup paths, and a growing automated test suite — 15 tests at initial delivery, now at **36 passing tests** as the tool has matured. No credentials, `.env` files, or query data are committed to the repository.

Deliberately scoped as a small pilot rather than a shared service — the next step is a small manager pilot (individual read-only accounts, over VPN) before any broader rollout or centrally managed packaging is considered.

---

## Impact

- Gave managers a self-service way to ask plain-language questions ("what schemas can I access?", "show me the columns in this table") without waiting on an engineer to run a lookup.
- Shortened the path from question to evidence for engineers: discover schema, inspect structure, run a narrow query — all in one Codex session.
- Individual accounts preserve accountability and keep database permissions as the ultimate enforcement point, so the tool adds convenience without adding risk.
- Proved out as a reusable data-access boundary beyond its original self-service use case: it now also powers the automated export step in the [RefRep timings reporting pipeline](01-refrep-timings-analysis.md).

---

## Skills Demonstrated

- MCP server design and implementation (STDIO transport, tool boundary design)
- Secure-by-design data access: read-only enforcement, SQL validation, credential isolation, generic error handling
- Cross-platform Python packaging and reproducible setup tooling
- Automated testing as part of initial delivery, not an afterthought — grown from 15 tests at launch to 36 passing tests today
- Translating a leadership ask into a scoped, safe pilot rather than an over-built service
