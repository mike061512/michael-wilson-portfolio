# Static Workflow Analysis & Table-Impact Explorer

**Role:** Sr. Site Reliability Engineer, Oracle America, Inc.
**Timeline:** 2026 - Present (discovery and continued development)
**Tools:** Python, Codex (AI-assisted analysis and artifact generation), HTML/JavaScript (generated interactive explorer), CSV export

---

## The Problem

Complex operational workflows are often documented across procedure guides, source files, generated artifacts, and team knowledge. That makes them difficult to review consistently: people can see the broad sequence but not the conditions that change the route, the evidence behind a step, or the potential effects of cleanup activities on individual tables.

The challenge was to turn a large static-review record into a clear, safe explorable artifact for technical and leadership conversations without presenting source presence as deployed behavior or an executable instruction set.

---

## What I Did

### Unified Workflow Explorer

- Built a single self-contained HTML briefing that combines a high-level workflow view, route selection, detailed stage descriptions, source references, and a table-impact explorer
- Modeled alternative paths explicitly so a reviewer can select an operation and copy method, then see only the applicable major stages and decision points
- Added clear checkpoints for prerequisites, handoffs, recovery boundaries, and acceptance conditions

### Table-Impact Review

- Created a filterable table-level catalog that explains each identified cleanup action, affected table or columns, row-selection condition, applicability gate, and supporting source reference
- Kept the display explicit about uncertainty: entries are static candidate effects, not proof that a specific run changed rows
- Added CSV export for review, evidence sharing, and offline comparison

### Evidence and Safety Boundaries

- Separated static source observations from runtime behavior, supported configurations, and operational instructions
- Preserved the limits of the available evidence, including unknown table membership, environment-specific rules, and unverified final-state effects
- Designed the briefing for demonstration and review without embedding credentials, sensitive data, environment identifiers, or executable operational commands

---

## Review Findings & Questions

### Questions for Developers and Process Owners

The explorer turns broad review concerns into practical questions that can be answered with a bounded evidence request:

- Which inputs choose a route, and which are configuration versus runtime discovery?
- What confirms completion, what blocks continuation, and where is the safe restart boundary for each phase?
- Which generated or externally owned artifacts are required for the selected route?
- What table-level rules, predicates, exclusions, and preservation groups are active for a given run?
- Which source observations remain unverified until the deployed version, effective configuration, and one representative result are reconciled?

### Paths, Risks, and Evidence Gaps Identified

- Conditional branches can change the order, applicability, and recovery path of major workflow stages; a single linear checklist can conceal those differences
- Generated artifacts and external handoffs can be essential to a route even when their implementation is outside the reviewed source set
- A successful configuration-generation step does not prove downstream acceptance, execution, validation, or final cleanup
- Table-impact rules can identify candidate actions, but row counts, actual membership, and final target state require run-specific evidence
- Completion, cleanup, retention, and acceptance are separate outcomes and should not be reported as one status

---

## Improvement Opportunities

- **Explicit route contracts:** define inputs, prerequisites, outputs, success criteria, failure handling, and escalation ownership for each major stage
- **Evidence-aware completion:** report generation, readiness, execution, validation, cleanup, and acceptance as distinct states instead of one generic success signal
- **Reusable configuration profiles:** capture proven configuration choices in a controlled form so recurring routes can be reviewed consistently without copying sensitive values
- **Focused recovery design:** identify safe restart points and the evidence required before a phase can be repeated or handed off
- **Table-impact reconciliation:** pair candidate source rules with approved, run-specific metadata and result summaries before making final-state claims
- **Reduced manual rediscovery:** use the explorer to show conditional paths, dependencies, and unresolved ownership at the point of review rather than reconstructing them from scattered documents

---

## Relationship to the RefRep Response Generator

This explorer is a companion to the RefRep Response Generator (internal repo name: macro-exterminatus). The Response Generator produces and validates response-file configurations, while this project maps how those selections influence downstream workflow paths, checkpoints, and review questions.

The relationship is deliberately iterative:

1. A response-file path is validated and proven in macro-exterminatus.
2. Its sanitized configuration shape becomes a seeded selection for this explorer.
3. The explorer adds the applicable route, stages, potential table impacts, dependencies, and evidence questions to a full operational review.
4. Findings from that review identify the next response-file path, validation boundary, or configuration rule worth proving upstream.

This creates a controlled feedback loop: configuration evidence sharpens workflow discovery, and workflow discovery identifies the most valuable configuration evidence to validate next. It does not imply that configuration generation alone proves operational execution or support.

---

## How the Analysis Was Derived

- Used AI-assisted analysis to organize and cross-reference static source material, response-file behavior, generated-artifact references, and written procedure plans
- Correlated documented sequence and conditional instructions with source-level dispatch, validation, and cleanup logic to build a complete review picture
- Connected the workflow review to upstream response-file work so proven selections can seed future route exploration without embedding sensitive values
- Produced interactive views from the resulting evidence model: high-level flow, route-specific stages, developer questions, improvement opportunities, and table-impact candidates
- Applied explicit evidence labels and limitations throughout: static source presence, documented instruction, proposed improvement, and runtime behavior are separate categories

---

## Current State

In progress. The explorer has been reviewed and demonstrated in limited early sessions while under active development, with positive initial reception. A first walkthrough for development teams and management is the next step. Table-impact entries remain static candidate effects until reconciled against run-specific evidence.

---

## Impact

- Consolidated workflow, scenario, evidence, developer questions, improvement opportunities, and table-impact review into one portable local artifact for demos and design discussions
- Made conditional behavior easier to explain than a linear procedure document by showing route-specific stages, decisions, and stop conditions
- Gave reviewers a practical way to examine potential cleanup effects at table level while retaining the distinction between source-backed candidates and observed execution results
- Established a reusable pattern for converting complex technical workflows into evidence-aware review tools without exposing sensitive implementation or deployment details
- Created a clear feedback loop between upstream configuration validation and downstream operational-review discovery

---

## Skills Demonstrated

- Static workflow analysis and technical process modeling
- AI-assisted evidence synthesis and cross-artifact correlation
- Interactive review-artifact design and specification (AI-assisted build with Codex, human-reviewed)
- Conditional-path and checkpoint visualization
- Table-level impact analysis with predicates and evidence references
- Configuration-to-workflow traceability design
- Evidence classification, uncertainty communication, and safe documentation boundaries
- Portable technical-demo design and CSV-based review support
