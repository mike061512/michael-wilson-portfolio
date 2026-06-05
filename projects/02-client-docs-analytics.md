# Client Documentation Analytics & OAC Workbook Suite

**Role:** Sr. Site Reliability Engineer, Oracle America, Inc.  
**Timeline:** 2025 (multi-month delivery)  
**Tools:** Python, Oracle Analytics Cloud (OAC), SQL, Confluence, Git

---

## The Problem

The team maintained several hundred client-specific operational runbook pages in Confluence. The corpus was large, inconsistent across pages, and impossible to assess at scale through manual review. There was no structured way to:

- Identify which instruction patterns were standardized vs. one-off
- Surface cleanup candidates or documentation gaps
- Present coverage and quality data to leadership or SMEs
- Track the state of the corpus across refreshes without re-reviewing from scratch

---

## What I Did

### Data Extraction & Normalization

- Established the corpus boundary at **312 pages** (direct child pages); scoped active pages to **311**
- Extracted and normalized **1,536 row-level instructions** across active pages, preserving traceability back to source pages
- Identified **1,204 distinct instruction families** within the active scope
- Generated a structured analysis pack and OAC-ready CSV export pack for downstream reporting

### Dimensional Data Modeling

- Designed the OAC semantic model from scratch: fact tables, dimension tables, helper datasets, and marts
- Documented safe join logic and dataset grain explicitly to prevent reporting errors and overcounting
- Built a workbook playbook and build checklist so the model could be extended or rebuilt by others safely

### Dashboard & Workbook Delivery

Delivered a first-release set of **six stakeholder-facing workbooks**:

| Workbook | Purpose |
|---|---|
| Executive Summary | High-level corpus health and coverage overview |
| Family Prioritization | Ranked instruction families by frequency and standardization opportunity |
| Standard Coverage | Coverage analysis by instruction type across the client base |
| Page Cleanup | Surfaced pages with gaps, inconsistencies, or cleanup candidates |
| Cooccurrence | Identified instruction pairs that frequently appear together — useful for standardization planning |
| Operational Drilldown | Row-level drill view for SME review and audit |

### Pipeline Reliability

- Added **contract validation** on generated artifacts: schema drift is caught at generation time, not after workbook build
- Built a **one-command refresh workflow** so the full analysis pipeline can be re-run without manual intervention
- Authored workbook appendices explaining metric definitions and grain rules to prevent misinterpretation of mixed-grain outputs

---

## Impact

- Created the **first credible, structured reporting layer** over a documentation corpus that was previously unquantifiable at scale
- Shifted leadership and SME review from ad hoc, page-by-page effort to **data-driven prioritization**
- Established a maintainable, contract-checked refresh pipeline — the reporting layer does not degrade silently between runs
- Produced practical prioritization insight: cleanup candidates, standard-coverage opportunities, high-risk instruction families, and repeated family pairings that support automation planning

---

## Skills Demonstrated

- Dimensional data modeling (fact tables, dimension tables, datasets, mart design)
- BI dashboard design and delivery in Oracle Analytics Cloud
- Data normalization pipeline design in Python
- Schema contract design and refresh pipeline automation
- Documentation and stakeholder communication for non-technical audiences
- Audit trail maintenance and reproducibility standards