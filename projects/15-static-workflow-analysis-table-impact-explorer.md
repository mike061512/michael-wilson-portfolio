# Static Workflow Analysis & Table-Impact Explorer

**Role:** Site Reliability Engineer  
**Timeline:** 2026  
**Tools:** HTML, JavaScript, Python, static source analysis, CSV export

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

## Impact

- Consolidated workflow, scenario, evidence, and table-impact review into one portable local artifact for demos and design discussions
- Made conditional behavior easier to explain than a linear procedure document by showing route-specific stages, decisions, and stop conditions
- Gave reviewers a practical way to examine potential cleanup effects at table level while retaining the distinction between source-backed candidates and observed execution results
- Established a reusable pattern for converting complex technical workflows into evidence-aware review tools without exposing sensitive implementation or deployment details

---

## Skills Demonstrated

- Static workflow analysis and technical process modeling
- Interactive HTML and JavaScript artifact design
- Conditional-path and checkpoint visualization
- Table-level impact analysis with predicates and evidence references
- Evidence classification, uncertainty communication, and safe documentation boundaries
- Portable technical-demo design and CSV-based review support
