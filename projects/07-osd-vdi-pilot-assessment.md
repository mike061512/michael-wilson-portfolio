# OSD VDI Pilot Assessment: Operational Requirements & Impact Analysis

**Role:** Sr. Site Reliability Engineer, Oracle America, Inc.  
**Timeline:** 2025  
**Tools:** Jira, written assessment documentation, cross-team stakeholder engagement

---

## The Problem

The team relied on a dual-access VPN model that allowed simultaneous connectivity to two network contexts — enabling engineers to work across on-prem client environments, hosted tooling, cloud environments, and internal tools without repeatedly swapping VPN sessions during the day. This was operationally important for SRE work, where context switching between environments happens constantly.

When the networking team moved away from allowing the dual VPN approach, Oracle Secure Desktops (OSD) — a Windows VDI — was introduced as the replacement path. The VDI would allow access to one network context while the local machine remained on the other.

The pilot was positioned as a straightforward replacement. The engineering team needed to verify whether it actually was.

---

## What I Did

### Requirements Definition

- Defined the functional baseline that any viable replacement solution would need to meet before accepting a forced migration
- Requirements included: concurrent environment access, access to core hosted and cloud tools, source-control availability across both contexts, file transfer capability, and session reliability under normal SRE workload

### Structured Pilot Evaluation

- Tested the OSD VDI against **real SRE usage patterns**, not synthetic or simplified scenarios
- Documented findings systematically: critical blockers, high-impact usability gaps, and sustained productivity risks — categorized by severity and operational consequence

### Critical Blockers Identified

- Lack of concurrent environment access — the core requirement the VDI was supposed to address
- VM persistence risk — sessions and state were not reliably preserved
- File transfer limitations — moving files between VDI and local contexts was constrained

### Sustained Productivity Risks Documented

- Repeated MFA friction under normal usage patterns
- Session instability and timeout behavior during longer operational tasks
- Missing access to shared tools (SharePoint, OneDrive) inside the VDI environment

### Written Impact Assessment

- Produced a detailed written assessment translating each technical gap into business and operational impact: context-switching cost, time-to-access overhead, authentication friction, and incident-response risk
- Delivered findings in a format usable by leadership and the owning team for decision-making, not just as an engineer complaint log

---

## Impact

- **Prevented the team from accepting a replacement that did not deliver functional parity** — the default outcome if the pilot had been treated as a formality
- Made engineering requirements explicit and documented, shifting the conversation from a security-and-networking decision to a question of whether the solution preserved operational capability
- Contributed to follow-up concessions from the owning team, including active investigation into restoring access to previously blocked tools inside the VDI environment
- Established a model for **structured engineering evaluation of infrastructure changes** before forced adoption

---

## Skills Demonstrated

- Functional requirements definition for platform and tooling changes
- Structured pilot evaluation against real operational usage patterns
- Technical finding documentation with business and operational impact framing
- Cross-team stakeholder communication and influence
- Advocacy for engineering team capability during externally driven platform changes