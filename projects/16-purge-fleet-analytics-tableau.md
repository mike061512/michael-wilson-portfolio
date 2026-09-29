# Fleet Performance Analytics: Purge Instrumentation & Cross-Client Benchmarking

**Role:** Software Engineer III, Cerner Corporation
**Timeline:** 2020 – 2022
**Tools:** Tableau, Vertica, Oracle RDBMS, PL/SQL, Oracle GoldenGate, Linux

---

## The Problem

The product was a clinical downtime continuity system: a replicated copy of production patient data maintained on client-hosted infrastructure so hospitals and clinics could continue delivering care when their connection to production was severed or taken down for maintenance. Keeping that copy current depended on a nightly purge process that removed aged data across more than 90 tables, and on replication processes that were sensitive to how long that purge held locks.

The purge ran linearly across every table and took 9 to 12 hours on average. That runtime was a problem on its own, but the larger problem was that nobody could see it. There was no execution telemetry, no way to compare one client's performance to another, and no way to tell a healthy deployment from a struggling one. Database growth and tablespace consumption surfaced only when Operations filed a support request, which meant the team learned about capacity problems after they had already become incidents.

Support engineers were troubleshooting individual client complaints with no baseline for what normal looked like. Operations had no evidence to support pushing clients onto newer releases. Both were working from anecdote.

---

## What I Did

### Redesigned the purge process

- Converted the nightly purge from a single linear pass across 90+ tables into three parallel job streams followed by a smaller set of final linear tables
- Total runtime became a function of the longest of the three streams rather than the sum of all tables, reducing average execution from 9 to 12 hours down to roughly 3
- Reduced the window during which the purge could contend with replication processes for row locks

### Instrumented the process to emit telemetry

The analysis was only possible because the redesign included capturing execution data that did not previously exist:

- Purging ran in batches of 20,000 rows, with a commit and a telemetry write after each batch
- Each record captured the purge process identifier, the table being purged, the elapsed time for that batch, and the actual row count where a batch completed with fewer than 20,000 rows
- The result was a per-batch event stream across the client install base, gathered nightly

Defining what to capture came before any analysis was possible. The process had no structured execution data until this work created it.

### Built the reporting and benchmarking layer

Sourced the resulting data into Vertica in partnership with an adjacent team, then built Tableau reporting on top of it across three analytical layers:

- **Server against peers within a client.** Clients running multiple servers were charted side by side, so a server operating differently from its siblings was visible immediately rather than being discovered through a support ticket.
- **Client against a cross-client average.** Built a baseline from the full install base and calculated each client's deviation from it, which made "slow" a measurable quantity rather than a subjective complaint.
- **Drill-down by application version.** Treated release version as an analytical dimension, isolating performance differences attributable to the software rather than to the environment.

### Turned the reporting into decisions

The reporting was built to be consumed by two teams outside my own, and it was:

- **Operations** used the version-level analysis as evidence for driving client adoption of the release containing the purge redesign
- **Support** used it as client-facing evidence when explaining that an upgrade would relieve replication lag and stability problems

---

## Findings

The benchmarking surfaced four classes of problem that were invisible before it existed:

**Internal process deviation.** The data showed support engineers terminating purge jobs prematurely as a workaround for replication row-lock contention. This was an undocumented internal practice that no one had reported, visible only as a pattern in execution telemetry.

**Unsupported client configuration changes.** Row counts that did not match expected purge behavior identified clients who had altered purge settings directly, which was not a supported configuration. The configuration itself was not visible to us; the change was inferred entirely from the output signal.

**Version-attributable performance differences.** Drill-down by release established which performance and replication-lag problems were addressed by the newer version, converting an upgrade recommendation from an assertion into evidence.

**Undersized and incorrectly provisioned hardware.** Worst-performing clients identified through deviation analysis were escalated to Operations and Support for investigation. In some cases the root cause turned out to be physical: the wrong hardware had been shipped, and the servers were substantially undersized for the workload they were carrying. This was not discoverable by examining the software, and would not have been visible without a cross-client baseline to measure against.

---

## Impact

- Cut average nightly purge runtime from 9 to 12 hours to roughly 3, reducing both the maintenance window and the period of contention with replication processes
- Replaced ticket-driven discovery of database growth and tablespace consumption with direct measurement, so capacity trends were observable rather than reported after the fact
- Gave Support a baseline for what normal performance looked like across the install base, changing client troubleshooting from anecdotal to comparative
- Gave Operations quantified, version-attributable evidence to support release adoption
- Surfaced an internal workaround, unsupported client configuration drift, and physical hardware provisioning errors, none of which were visible through existing tooling
- Established a measurement pattern applied repeatedly in later work: instrument the process first, define the structured data, then build the reporting that makes prioritization possible

---

## Follow-On Work

The parallelization approach developed here was subsequently scaled down and applied at single-table granularity as a self-managing PL/SQL purge function, which batched rows to a target size and then removed itself. That finer-grained version was reused for client-specific and edge-case tables where the fleet-wide nightly process was not the right fit.

---

## Current State

The Tableau reports were deprecated and removed when the Tableau license was retired; they were not migrated to a successor platform. The underlying purge redesign and the telemetry it emitted remained in the product.

---

## Skills Demonstrated

- Process instrumentation: defining and capturing structured execution data where none existed
- Comparative and benchmark analysis across a multi-tenant install base
- Anomaly detection through deviation from a computed baseline
- Tableau report design for cross-team, non-authoring consumers
- Vertica and Oracle SQL for analytical workloads
- Cross-team data sourcing and partnership
- PL/SQL development and parallel execution design over large tables
- Translating analytical findings into adoption decisions and client-facing evidence
