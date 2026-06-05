# AI Agent & MCP Workflow Enablement

**Role:** Sr. Site Reliability Engineer, Oracle America, Inc.  
**Timeline:** 2024 – Present  
**Tools:** Cline, Codex, Oracle Code Assist, Claude, MCP (Model Context Protocol), Jira/Confluence via mcp-atlassian, Git

---

## The Problem

AI coding and analysis tools are increasingly capable, but most teams use them in an isolated, session-by-session way: start a session, get some output, lose the context when the session ends. Each new session rediscovers the same project state, re-explains the same constraints, and produces inconsistent results because the tool has no durable understanding of the work.

The second problem is coordination: when multiple AI agents or tools are working against the same repository, there is no standard way to hand off context, avoid conflicts, or preserve decisions made in one session for the next.

---

## What I Did

### MCP Workflow Configuration

- Configured MCP-backed AI workflows connecting agent tools (Cline, Codex) to internal Atlassian systems (Jira, Confluence) via `mcp-atlassian`
- Enabled agents to query, inspect, and act on real internal knowledge stores and project artifacts — not just public documentation or synthetic examples
- Applied these connections directly to live delivery work: the Client Special Instructions corpus analysis, documentation generation, and reporting support

### Cross-Agent Coordination Model

- Partnered with a colleague (Hanley) to develop a repeatable **baton-passing model** for multi-agent collaboration against the same repository
- Built supporting repo patterns: shared handoff notes, durable memory context files, and explicit coordination rules that survive session boundaries
- The model allows Cline and Codex to work against the same codebase in sequence without losing context or duplicating effort

### Practical Delivery Application

- Applied AI-assisted workflows directly to production delivery work — not as demos, but as tools that accelerated real projects
- Used agent-assisted analysis to support the Client Special Instructions corpus normalization and OAC workbook delivery
- Used MCP-connected Jira workflows to manage project tracking and issue state during active delivery

---

## Impact

- Moved AI tool usage from isolated experimentation to **repeatable, production-applied delivery workflows**
- Reduced context loss between sessions by building durable handoff and memory structures — the single biggest usability gap in AI-assisted development at the team level
- Created reusable patterns for future AI-assisted work against internal systems and repositories
- Supported measurably faster delivery on adjacent projects by removing the overhead of re-establishing context on each session

---

## Skills Demonstrated

- MCP server configuration and integration (mcp-atlassian, Jira/Confluence)
- Multi-agent workflow design and coordination (Cline, Codex, Claude)
- Cross-agent context management and baton-passing model design
- Prompt engineering for consistent, scoped AI behavior across sessions
- AI-assisted delivery applied to real operational work (not demos or prototypes)
- Repository pattern design for AI collaboration: memory banks, handoff notes, coordination rules