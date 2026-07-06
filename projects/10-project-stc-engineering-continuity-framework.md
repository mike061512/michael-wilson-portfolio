# Project STC: AI-Assisted Engineering Continuity Framework

**Type:** Self-Initiated Work Initiative (Public Open-Source Release)  
**Timeline:** May 2026 – Present (public release: June 30, 2026; v1.1.0: July 2, 2026)  
**Tools:** Python, Git, Markdown, GitHub; tool-agnostic framework applied across Claude Code, Cursor, Cline, Codex, GitHub Copilot  
**Repository:** [github.com/mike061512/project-stc](https://github.com/mike061512/project-stc) (MIT License)

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

### Public Release

Took the framework from internal concept to a public, versioned open-source project in roughly five weeks:

- Published the repository publicly on GitHub under the MIT License, with a full public-facing rewrite of all docs to remove internal/company-specific framing
- Shipped two tagged releases: **v1.0.0** (initial public release, June 30, 2026) and **v1.1.0** (tiered context model and Memory Bank lifecycle guidance, July 2, 2026)
- Built two adoption paths: `starters/tiny-stc/` (5-file minimal starter, fills in under 10 minutes) and `starters/minimum-stc/` (15-file starter for team/long-running projects), plus a guided AI-assisted initialization prompt
- Delivered two fully filled-in reference examples (legacy CLI modernization, greenfield REST API) so adopters can see the framework applied at a realistic mid-work state rather than a blank template
- Wrote a `docs/comparison.md` positioning STC against single-instruction-file approaches (CLAUDE.md/AGENTS.md/.cursorrules) and heavier memory/orchestration frameworks, and `docs/tool-adapters.md` with integration snippets for Claude Code, Cursor, Cline, Copilot, and Codex
- Built `scripts/validate-stc.py`, a lightweight Python validator that checks a project's required files and flags broken local links
- Authored `CONTRIBUTING.md` and `SECURITY.md` to support external contribution and responsible disclosure

### Community Reception

- Announced the release publicly via [LinkedIn](https://www.linkedin.com/posts/michael-wilson-ohh-sre_github-mike061512project-stc-a-lightweight-activity-7477810544922632192-iHgV) and several Reddit developer communities
- Received and merged the project's **first external contribution** (PR #1: tiered context model and Memory Bank lifecycle guidance), validating that the framework's structure was clear enough for an outside contributor to extend it correctly
- Framework philosophy and design are mature; the public release is early — honest framing given it's under two weeks old as of this writing, with adoption still to be proven at scale
- Applied components of the framework internally across active Oracle projects prior to the public release — the cross-agent baton model in the [MCP/AI enablement work](08-ai-agent-mcp-workflow-enablement.md) is a direct application of the Memory Bank and AI Instruction Layer concepts

---

## Impact

- Identified a systemic gap in engineering effectiveness that applies across teams, tools, and roles — not specific to any one project or platform
- Took a framework from internal concept to a public, versioned, MIT-licensed open-source release in about five weeks — including documentation, starters, working examples, a validator, and contribution/security policies
- Proved the framework's clarity externally: an outside contributor was able to extend it correctly on the first pull request
- Created a practical, low-overhead framework designed to be adopted at the engineering level rather than mandated through process
- Reduced context loss in AI-assisted workflows — measurably so in projects where the framework components were actively applied prior to public release
- Established a reusable pattern for onboarding, handoff, and long-running project maintainability that other engineers can adopt without heavy tooling investment

---

## Skills Demonstrated

- Systems thinking and organizational problem framing
- Framework design for engineering effectiveness
- Open-source project delivery: versioning/release tagging, contribution governance, security policy, public documentation
- AI workflow architecture and cross-session context management
- Knowledge management and engineering process improvement
- Documentation designed for adoption, not just comprehensiveness