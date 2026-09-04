# OLAM Modernization: RefRep Validation and Evidence Collection

## Executive summary

This project is establishing a structured path to modernize the RefRep validation and evidence-collection processes that support Refresh and Replicate work. The current process relies on large, brittle script wrappers that combine unrelated responsibilities such as validation, evidence capture, credential access, notifications, Jira updates, and remediation. That model is difficult to scale, audit, secure, test, or safely change.

Our target is a modular Oracle Linux Automation Manager (OLAM) framework in which each approved job has one operational purpose, explicit inputs, a defined result, least-privilege access, and independently managed scheduling. This will let the SRE team improve reliability and visibility while keeping sensitive and state-changing work behind separate governance and approval boundaries.

The project is currently in discovery and planning. No OLAM job templates, playbooks, credentials, schedules, operational script executions, or Jira issues have been created as part of this work.

## Why this project is needed

RefRep operational readiness depends on a broad set of checks, comparisons, and evidence captures performed before and after environment changes. Static review of the current automation showed that the legacy wrapper model mixes many concerns in the same execution path. Some scripts that appear to be checks also create files, access sensitive data, send email, update Jira, modify access or packages, or perform restoration and remediation actions.

That coupling creates several operational challenges:

- A failure is harder to isolate because a single wrapper can run multiple checks and side effects together.
- Checks cannot be safely scheduled or delegated independently when they have different privilege, credential, and target-impact requirements.
- Outputs and retained artifacts do not consistently have a defined sanitization, ownership, retention, or rerun contract.
- The active RefRep prerequisite check set cannot yet be fully inferred from archived scripts alone because the application invokes an external `refrep_prereq` executable.
- Changes to a broad wrapper carry more regression and security risk than changes to a small, well-defined validation unit.

The modernization effort addresses these issues by moving away from monolithic pre-check and post-check wrappers toward an industry-aligned automation model: small composable jobs, explicit interfaces, separation of duties, least-privilege access, auditable results, and controlled workflow composition.

## Project objectives

The project will provide a sustainable framework for RefRep-related operational validation and evidence collection.

| Objective | Intended outcome |
| --- | --- |
| Improve reliability | Individual failures can be identified, rerun, and remediated without rerunning unrelated activities. |
| Strengthen security | Credential handling, sensitive output, external writes, and target-changing actions are separated from routine validation. |
| Increase operational visibility | Each approved check produces a structured, sanitized result with a clear target scope and severity. |
| Enable scale | Reusable jobs can be composed into workflows only where dependencies are verified. |
| Improve governance | Ownership, approvals, artifact retention, audit expectations, and scheduling decisions are explicit. |
| Create a durable backlog | Discovery findings are translated into reviewable Epic work packages and atomic future implementation tasks. |

## Discovery completed to date

The team completed a discovery-first inventory without executing the source scripts or creating OLAM configuration. The work reconciled several sources:

- Legacy OHMRR automation, including the `refrep_checks.sh` wrapper and its related scripts.
- RefRep application artifacts, including the controller, parser, and archive of potential prerequisite check scripts.
- The Refresh/Replicate pre-work and post-work runbook.
- Relevant response-input and target-discovery work that may inform a later, opt-in data-collection stream.

The resulting discovery catalog identifies confirmed candidates, controlled captures, blocked sensitive-output work, and excluded state-changing or external-write actions. It also documents the dependencies and decisions that must be resolved before an individual candidate can become an OLAM implementation task.

### Key findings

- The legacy `refrep_checks.sh` wrapper is a mixed orchestrator and must not be migrated as a single OLAM job.
- `node_checks.sh` contains at least 23 separable platform and node-validation components, including operating-system, capacity, service, process, and connectivity observations.
- Read-only or comparison-oriented candidates include node validation, package/version comparison, instance-count capture and comparison, MPage URL validation, LDAP/security-hosting validation, QC reporting, and TNS file validation.
- Several apparent checks require redesign before adoption because they may access credentials, create sensitive artifacts, send email, modify systems, or integrate with Jira.
- The RefRep archive contains 38 potential prerequisite scripts, but their current active status remains unproven until the external `refrep_prereq` executable and its emitted result set are recovered and mapped.

## Target operating model

The future OLAM framework will use the following operating principles.

| Principle | Application |
| --- | --- |
| Single-purpose jobs | A job validates one condition or captures one defined evidence set. It does not combine validation, notification, remediation, and external updates. |
| Explicit contracts | Each job documents inputs, authorized inventory, result schema, severity rules, retained evidence, and non-responsibilities. |
| Least privilege | Access is limited to the system, data, and actions required for the job. Secret values are not exposed in documentation or routine job output. |
| Safe composition | Workflows connect jobs only when a real dependency is evidenced, such as comparing a post-change capture with an immutable pre-change capture. |
| Controlled evidence | Artifacts have a defined storage location, sanitization standard, access model, retention period, capacity expectation, and rerun policy. |
| Independent governance | Validation, capture, notification, Jira integration, credential retrieval, remediation, restoration, and target-changing actions have separate approval and permission boundaries. |

This design retains the operational value of pre-change and post-change readiness checks without retaining the fragile wrapper implementation. Pre-change and post-change are execution contexts, not reasons to group unrelated actions into one job.

## Planned delivery approach

The team will progress in controlled waves. A candidate will not move into implementation simply because it has been discovered or named in a runbook.

1. Establish OLAM foundations: governance, naming, inventories, execution environments, role-based access, credential-reference categories, result schemas, artifact controls, and notification policy.
2. Complete source certification: recover the current `refrep_prereq` result set and map each active result to its underlying behavior, target scope, input requirements, and pass/fail semantics.
3. Design and manually validate the first read-only candidates as independent OLAM jobs.
4. Introduce controlled evidence capture only after storage, retention, security, and restore-relationship decisions are accepted.
5. Keep sensitive, state-changing, or externally visible activities in separate future design streams with their own approval, rollback, and execution-ownership decisions.

The first read-only design wave is expected to focus on high-value candidates such as platform and node validation, package/version comparison, QC evidence, pre/post instance-count comparison, endpoint validation, LDAP/security-hosting validation, and TNS validation. The final release sequence will be selected by the SRE team after the foundation and certification work is complete.

## Team operating and decision model

This is a shared SRE modernization effort rather than a traditional project-manager-led initiative. The team will use lightweight, evidence-based governance:

- Jira will be the system of record for approved work, ownership, decisions, and implementation progress.
- The discovery catalog and Epic skeleton will remain the design sources that explain why a candidate is included, blocked, or excluded.
- Each candidate will receive peer review before it becomes an implementation task.
- One person will own each active backlog item, while technical decisions and check definitions remain reviewable by the broader SRE team.
- Security, artifact-management, and active-`refrep_prereq` ownership must be explicitly assigned before affected work can proceed.
- A failed check's downstream behavior, such as notification, workflow block, or both, will be agreed before scheduling is enabled.

## Tracking and readiness criteria

The proposed Epic is organized around foundation work, modular check design, controlled capture, prerequisite certification, manual-runbook mining, and future data-collection discovery. The detailed backlog includes 109 leaf-level placeholder tasks under seven module areas; these are planning placeholders, not created Jira issues.

Every future implementation task must demonstrate all of the following before it is considered ready to configure in OLAM:

- Source behavior and current applicability are verified.
- The target inventory, owner, and authorized operator group are known.
- The activity is classified as read-only, controlled capture, remediation, or external action.
- Inputs, non-secret credential references, privilege boundary, and expected result are defined.
- Failure, severity, human-review, and rerun-safety rules are agreed.
- Output is sanitized, has an approved retained-artifact location, and meets retention and access requirements.
- The job has completed a manual-launch review before it is considered for scheduling.
- The job states its one purpose and its explicit non-responsibilities.

## Current boundaries and dependencies

The project deliberately excludes the following from its initial OLAM check-adoption wave: credential retrieval or disclosure, package installation, SSH key setup, email delivery, Jira creation or updates, database mutation, source-to-target copy or restore, process termination, and server-cycling actions. Those activities may be evaluated later, but only through separately approved change-workflow design with security, rollback, and ownership controls.

The most important near-term dependency is recovery of the current external `refrep_prereq` executable contract. Until that evidence is available, the 38 archived prerequisite scripts remain potential candidates rather than confirmed active checks.

## Measures of progress

Leadership and the SRE team can track progress through a small set of practical measures:

- Foundation decisions accepted: governance, inventory, access, result, artifact, and notification contracts.
- Candidates certified: confirmed source behavior, scope, safety classification, and owner.
- Modular jobs designed and manually validated: independent input/result and permission contracts accepted.
- Jobs eligible for scheduling: manual execution, failure behavior, retained evidence, and operational ownership accepted.
- Legacy wrapper responsibilities retired or isolated: validation and capture moved out of mixed orchestration without importing unsafe side effects.

## Project artifacts

The following working documents support the project and can be updated as the team makes decisions:

- [OLAM Check Discovery Catalog](olam-check-discovery-catalog.md): source inventory, candidate classifications, boundaries, and discovery evidence.
- [OLAM Jira Epic Plan](olam-jira-epic-plan.md): proposed Epic objective, work packages, sequencing, and implementation-readiness template.
- [OLAM Jira Epic Skeleton](olam-jira-epic-skeleton.md): detailed parent and leaf-level planning placeholders for backlog refinement.

## Next step

The next decision is to confirm the initial OLAM governance model and assign owners for artifact security, output retention, and recovery of the active `refrep_prereq` contract. That work provides the control plane needed to begin designing the first read-only jobs safely.
