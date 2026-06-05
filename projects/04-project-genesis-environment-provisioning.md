# Project Genesis: New Client Environment Provisioning & Process Hardening

**Role:** Sr. Site Reliability Engineer, Oracle America, Inc.  
**Timeline:** 2024 – Present  
**Tools:** Oracle RDBMS, OCI Object Storage, internal provisioning tooling, Confluence

---

## The Problem

The standard path for creating new client environments relied on a replicate process that was not supported for new-footprint provisioning. The alternative — a from-scratch environment creation process — had been abandoned after a platform version transition because it was no longer seen as worth maintaining.

That left a real operational gap: when a net-new client environment was needed and the replicate path was not viable, there was no supported method to fall back on. Institutional knowledge of the older process was fragmented across a small number of engineers, none of it documented.

---

## What I Did

### Process Recovery & Adaptation

- Identified that the capability gap was solvable rather than accepting it as a fixed constraint
- Partnered with internal teams that retained partial knowledge of the legacy process to reconstruct what was still viable
- Adapted the recovered approach to current platform and tooling requirements — the old process could not be used as-is after the version transition

### Pilot Execution

- Served as the **initial pilot operator** through the reconstructed process — not just coordinating or documenting, but executing the full workflow end to end
- Identified edge cases, undocumented dependencies, and execution gaps that only surface when actually running the process, not when describing it
- Built and improved working instructions in real time based on what the pilot exposed

### Runbook Development & Hardening

- Converted fragmented institutional knowledge and pilot findings into a structured, reusable runbook
- Documented operational nuances, decision points, and failure modes so future operators could execute with less risk
- Established this as the supported method for new-footprint provisioning when the replicate path is not available

### Next-Phase Design (In Progress)

- Contributing to a disconnected replicate model as the next evolution of the process
- The goal: stage required backend artifacts and a database copy in OCI Object Storage, removing dependency on a live source environment for each new build
- This design would meaningfully reduce turnaround time and improve viability for network-constrained client environments, including Federal deployments

---

## Impact

- **Closed an operational capability gap** that had no supported solution
- Reduced reliance on tribal knowledge by converting a partially remembered legacy process into working, current documentation
- Lowered delivery risk for future operators by piloting the process first and exposing gaps before broader reuse
- Created a path toward **faster, more portable environment creation** — reducing repeated coordination overhead with partner teams for each new request
- Advanced viability for Federal client environments where stricter network constraints make live-source-connected approaches impractical

---

## Skills Demonstrated

- Operational process recovery and adaptation
- Discovery-first execution (pilot before documentation)
- Runbook design and operational hardening
- Cross-team knowledge extraction and formalization
- Architecture contribution for next-phase disconnected replicate model
- Documentation calibrated for future operators, not just current context