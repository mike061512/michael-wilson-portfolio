# Project STC: AI-Assisted Engineering Continuity Framework

**Type:** Self-Initiated Work Initiative  
**Timeline:** May 2026  
**Tools:** Tool-agnostic framework design; applied across Claude Code, Cline, Codex, Jira, Confluence, Git

---

## The Problem

Engineering organizations are generally good at preserving code. They are poor at preserving *understanding*.

Context fragments across Jira tickets, Confluence pages, chat threads, AI sessions, and individual contributors. As projects age, teams rediscover previously known information, repeat past investigations, and reconstruct decisions whose rationale was never preserved. The cost is real: slower onboarding, recurring investigation overhead, and engineering drift where teams make decisions that contradict earlier conclusions they no longer remember.

AI-assisted development introduced a new dimension of this problem. Individual AI sessions can be highly productive — but discoveries, decision rationale, and scoped instructions are lost when sessions end. The next session starts cold. Over time, the gap between what was figured out and what is accessible compounds.

No existing framework at the team level addressed this directly. Jira tracks tickets. Confluence stores documentation. Neither preserves the reasoning and operational context that makes engineering work maintainable over time.

---

## What I Did

### Framework Design

Designed Project STC (named as a nod to the Standard Template Construct from Warhammer 40k — a repository of preserved engineering knowledge) as a lightweight, tool-agnostic framework with four core components:

**Memory Bank**  
Structured preservation of active context, decisions, research findings, and troubleshooting history. Separates durable knowledge (decisions, findings, constraints) from transient working state (current task, next steps). Designed to survive session boundaries and contributor turnover.

**Project Context Layer**  
Local project understanding decoupled from org-wide policies. Each project preserves its own context — architecture decisions, known constraints, prior investigation results — without requiring modification of shared guidance documents. Projects can be handed off or resumed without re-explanation.

**AI Instruction Layer**  
Formalized, reusable instructions that improve AI reasoning consistency, scope discipline, and uncertainty handling across sessions and contributors. Reduces the variance between what a skilled engineer gets from an AI session versus what a junior engineer or new contributor gets.

**Anti-Drift Mechanisms**  
Explicit constructs that treat context drift as a manageable engineering problem rather than an inevitable one:
- Mission definitions that anchor project scope
- Phase boundaries that mark decision points and completed work
- Decision logs that preserve rationale alongside outcomes
- Scope controls that prevent gradual expansion from eroding project focus

### Implementation & Reception

- Framework philosophy and conceptual design are mature; implementation is early-stage and actively evolving
- Applied components of the framework across active Oracle projects — the cross-agent baton model in the MCP/AI enablement work is a direct application of the Memory Bank and AI Instruction Layer concepts
- Initial reactions from colleagues have been strongly positive; no similar initiative existed at Oracle prior to this work

---

## Impact

- Identified a systemic gap in engineering effectiveness that applies across teams, tools, and roles — not specific to any one project or platform
- Created a practical, low-overhead framework designed to be adopted at the engineering level rather than mandated through process
- Reduced context loss in AI-assisted workflows — measurably so in projects where the framework components were actively applied
- Established a reusable pattern for onboarding, handoff, and long-running project maintainability that other engineers can adopt without heavy tooling investment

---

## Skills Demonstrated

- Systems thinking and organizational problem framing
- Framework design for engineering effectiveness
- AI workflow architecture and cross-session context management
- Knowledge management and engineering process improvement
- Documentation designed for adoption, not just comprehensiveness