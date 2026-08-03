# Legacy Product Modernization: Oracle CDB/PDB & GoldenGate 19 Compatibility

**Role:** Software Engineer III, Cerner Corporation
**Timeline:** 2021–2022 (final project prior to leaving Cerner)
**Tools:** Linux, AIX, Oracle Database (11g–19c), Oracle GoldenGate (11–19), SQL/PL-SQL, Shell scripting

---

## The Problem

Our team maintained a proprietary command-line tool used across hospital downtime systems to configure, set up, and monitor Oracle GoldenGate replication processes along with the database tables, objects, and rules those processes depended on. The tool dated back to Oracle 9i and had been carried forward through Oracle 11.2. Its database connectivity was built entirely around `sysdba` logins — a broad-access, unsecure connection method that had worked for over a decade because it always landed you in the one database you meant to administer.

Oracle's move to the CDB/PDB (container database / pluggable database) multitenant architecture broke that assumption at the root: a `sysdba` login on a CDB/PDB system connects to the container database (CDB), not the pluggable database (PDB) actually holding the client's data. Every code path in the tool that assumed a direct, single-database connection was now silently pointed at the wrong place.

Compounding the problem, GoldenGate 11 — the version the entire pipeline ran on — did not function against the new CDB/PDB architecture at all. Supporting the new database architecture meant simultaneously upgrading to GoldenGate 19 across the full pipeline (source, midtier, and onsite databases), while still fully supporting the many client environments that had not yet moved off GoldenGate 11 or Oracle 11.

---

## What I Did

I was the sole engineer on this project, from investigation through delivery.

- **Mapped the full blast radius.** Performed a complete code review, dependency mapping, and topology analysis across the tool's codebase — several hundred files — to identify every place a `sysdba`-based connection, hardcoded database assumption, or GoldenGate-version-specific logic would break under CDB/PDB.
- **Redesigned the connection layer.** Reworked database connectivity so the tool correctly targeted the PDB rather than falling into the CDB root, while preserving correct behavior against pre-12c targets that had no PDB concept at all — the tool had to detect and branch on topology, not assume one architecture.
- **Delivered parallel GoldenGate version support.** Extended the tool to fully support GoldenGate 19 end-to-end (source → midtier database → onsite databases) while retaining complete GoldenGate 11 support for clients who hadn't upgraded, so the tool had to detect and correctly handle GoldenGate version at every relevant integration point.
- **Validated the full compatibility matrix.** Client environments could present any combination of: source database (11/19), source GoldenGate (11/19), target database (11/19), target GoldenGate (11/19), onsite GoldenGate (11/19), and operating system (Linux/AIX). I verified the tool functioned correctly across all of these permutations, including mixed-version scenarios such as an Oracle 11/GoldenGate 11 source replicating to an Oracle 19/GoldenGate 19 target, and the reverse.
- **Tested and traced entirely by hand.** No AI-assisted tooling existed for this work at the time — every code path, dependency, and compatibility edge case was traced, reverse-engineered, and validated manually.
- **Used the migration as a security and reliability upgrade, not just a compatibility patch.** Where the redesign allowed it, reduced reliance on blanket `sysdba` access, and improved the tool's reporting, alerting, monitoring, and performance in the areas touched.

---

## Impact

- Delivered a fully modernized product supporting every client environment permutation across two Oracle database generations, two GoldenGate generations, and two operating systems, without breaking any existing legacy deployment.
- Let the business avoid forcing clients onto a synchronized upgrade schedule — legacy Oracle 11/GoldenGate 11 clients kept working exactly as before, while newer CDB/PDB environments became supported for the first time.
- Improved the product's security posture by reducing reliance on the legacy `sysdba` connection model, alongside monitoring, alerting, and performance improvements delivered as part of the same effort.
- Completed independently, as the last major deliverable of my tenure at Cerner, meeting my own standard for a thorough, fully tested, production-ready release.

---

## Skills Demonstrated

- Legacy system reverse engineering and dependency mapping at scale, with no pre-existing map of the affected surface area
- Deep Oracle database architecture expertise spanning multiple major version generations (9i through 19c), including multitenant CDB/PDB internals
- Oracle GoldenGate configuration, administration, and cross-version compatibility engineering
- Cross-platform systems engineering (Linux and AIX)
- Combinatorial backward-compatibility design and validation across a large support matrix
- Independent ownership of a high-stakes, business-critical modernization effort from investigation through production delivery
