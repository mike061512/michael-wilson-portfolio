# OLAM Modernization: RefRep Validation & Evidence-Collection Framework

**Role:** Sr. Site Reliability Engineer, Oracle America, Inc.
**Timeline:** 2026 (discovery and planning phase)
**Tools:** Oracle Linux Automation Manager (OLAM), Jira, Bash/KSH/PowerShell (legacy script review)

---

## The Problem

RefRep operational readiness depends on a large set of pre-change and post-change checks, comparisons, and evidence captures. The legacy automation implementing them — a `refrep_checks.sh` wrapper and its related scripts — mixes unrelated responsibilities in the same execution path: validation, evidence capture, credential access, notifications, Jira updates, and remediation all run together. That coupling makes failures hard to isolate, prevents checks from being scheduled or delegated independently, and means a change to one script carries the regression and security risk of the entire wrapper.

---

## What I Did

### Discovery-first inventory

Completed a static, execution-free review of the legacy automation surface — reconciling the `refrep_checks.sh` wrapper family, the RefRep application's own prerequisite-check archive, and the team's manual pre-work/post-work runbook — without running any source script or creating any OLAM configuration.

### Decomposed monolithic scripts into atomic units

- Broke a single node-validation wrapper into **23 separable checks** spanning OS/kernel state, capacity, service and process health, and connectivity
- Catalogued additional module areas for decomposition: package/version compatibility comparison, application URL/endpoint validation, LDAP/security-hosting validation, paired pre/post evidence capture (e.g., instance-count comparison), and TNS configuration-file validation
- Flagged **38 candidate legacy prerequisite scripts** as unproven-active until certified against the RefRep application's external prerequisite contract — treating "referenced in an old script" as a hypothesis to verify, not a fact to migrate

### Designed the governance model before any implementation

- Defined a least-privilege role model (operator, maintainer, auditor, approver) and a non-secret credential-reference model so no job needs to expose or handle raw credentials
- Specified a shared result/severity contract (PASS/FAIL/WARN/UNKNOWN/BLOCKED) and an artifact redaction/retention policy so every future job's output is sanitized and auditable by construction
- Established that validation, evidence capture, notification, Jira integration, credential retrieval, and remediation each require **separate tasks and separate permissions** — no future job can silently accumulate scope
- Explicitly excluded state-changing and high-risk actions (credential retrieval, database mutation, source-to-target restore/copy, package installation) from the initial adoption wave, routing them instead to a future change-workflow with its own approval and rollback controls

### Designed a task-allocation framework with built-in management visibility

Translated the discovery findings into a structured Jira Epic skeleton — not just a backlog dump, but a three-tier framework built so the same artifact serves engineers, team leads, and leadership at once:

- **Epic** — the single objective and status leadership tracks without needing module-level detail
- **Parent work packages** (e.g., node validation, compatibility comparison, LDAP/security-hosting, TNS validation) — the unit team leads assign to an engineer or sub-team, each with its own scope and boundary
- **Atomic leaf tasks** (roughly 109 of them across seven module areas — foundation, atomic checks, controlled evidence capture, prerequisite certification, manual-runbook mining, and sensitive-output/remediation decisions) — small enough that any engineer can pick one up independently, with its own notes and completion evidence, without blocking on the rest of the module

Every task carries an explicit rule set (one job, one purpose, one result contract, stated non-responsibilities) so an engineer picking up any leaf task — regardless of who scoped it — produces work that fits the same governance model. Framed explicitly as a planning skeleton for team review, not authorization to create Jira issues or configure OLAM.

---

## Current State

The project is in discovery and planning: no OLAM job templates, credentials, schedules, or Jira issues have been created. The next gating step is team review of the governance foundations and certification of the legacy prerequisite scripts' actual active status — the control plane needed before the first read-only OLAM jobs can be designed safely.

---

## Impact

- Converted a fragile, high-risk automation surface — where checks, secrets, and remediation were entangled in the same scripts — into a scoped, reviewable modernization backlog
- Established a separation-of-duties model that isolates credential handling and state-changing actions from routine, low-risk validation work
- Prevented premature migration of unproven legacy scripts by requiring explicit certification against the application's real prerequisite contract first
- Created a durable, evidence-based planning artifact that lets the team adopt the new model incrementally, with governance decisions made once and reused across every future check
- Gave the effort a shared structure that scales across the organization: engineers get independently assignable atomic tasks, team leads get parent-level work packages to distribute, and leadership gets Epic-level progress — without anyone needing to track 109 individual line items to see whether the initiative is moving

---

## Skills Demonstrated

- Legacy system reverse engineering and discovery-first methodology (static analysis without execution risk)
- Automation architecture: single-purpose job design, least-privilege access, safe workflow composition
- Security-conscious systems design: credential isolation, output redaction, artifact retention policy
- Large-scale backlog decomposition and Epic/task planning for cross-team review
- Governance design: explicit approval boundaries, ownership assignment, and scope exclusions for high-risk work
- Multi-level program framework design: structuring one artifact to serve engineer task allocation, team-lead work distribution, and leadership visibility simultaneously
