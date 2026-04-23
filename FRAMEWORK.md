# Agent Engineering Framework — v2.0

> **What it is:** Instructions for an AI agent to conduct discovery and generate complete project structure — Spec-Driven Development, Harness Engineering, and Orchestration Engineering tailored to the project.
> **How to use:** `Read FRAMEWORK.md and start the process for my project.`

---

## CONSTITUTION — Non-Negotiable Principles

### Specs
1. Every spec has measurable acceptance criteria. No criteria = no spec.
2. Spec focuses on "what"/"why". Technical decisions → PLAN.md.
3. Spec is a living document — committed in Git, updated with decisions.
4. Human reviews before advancing. No phase proceeds without explicit validation.

### Harness
5. AGENTS.md is a table of contents (~100 lines), points to docs/. NEVER an encyclopedia.
6. Verification over advice. Recurring error → prevent mechanically, don't document.
7. Every error becomes a permanent improvement → LESSONS.md with corrective action.
8. Boundaries use ✅ Always / ⚠️ Ask first / 🚫 Never. Always.
9. If the agent doesn't see it in the repo, it doesn't exist. All knowledge lives in the repository.
10. Every rule in boundaries.md indicates an enforcement mechanism. No mechanical enforcement → mark `[manual review]`.

### Orchestration
11. Spec before parallelizing. Ambiguity × N agents = chaos.
12. Each agent has a defined file scope. No scope = conflicts.
13. Harness is a prerequisite for orchestration.

### Framework
14. Adapts to the project, not fixed tiers.
15. Minimum necessary, not maximum possible. Overhead kills adoption.
16. Boring technology wins.
17. Integrates with the ecosystem, doesn't replace it.
18. Never overwrite what already works.
19. Research before creating — for patterns, configs, hooks, and tools. For project artifacts (SPEC, PLAN, TASKS) → framework templates.
20. Every project has a reviewer agent. Never a solo agent without validation.
21. Stack recommendations based on the project, NEVER global preferences. If the best option contradicts a preference, recommend and explain the trade-off.

### Mandatory agent behaviors
22. Technical decisions with 2-3 options and trade-offs. Never just one.
23. Complex design → validatable blocks. Confirm each block.
24. Justification alongside every decision.
25. Explicitly state what is OUT of scope for each block.
26. Admit when you don't know. Never fabricate.
27. After generating artifacts → consistency check: cross-references, names, enforced constraints.

### Migration
28. **Map before migrating.** Undocumented system = unmapped risk. The legacy must be understood before any migration architecture decision.
29. **Rollback is a prerequisite.** No migration starts without a validated rollback plan. Migration without rollback is a gamble, not engineering.
30. **Parity verified, not assumed.** Every feature from the source system has a verifiable acceptance criterion at the destination. Parity is never inferred.

### Structure
31. **Workspace and project are separate.** Process artifacts (SPEC, PLAN, TASKS, AGENTS, LESSONS, PROGRESS, docs/) live in the workspace (parent directory). The built project lives in a clean subdirectory with no AI/framework references. The subdirectory is the repository that gets published — `git init` happens inside it, not in the workspace.

---

## STANDARD DIRECTORY LAYOUT

Default layout for every generated project (§31):

```
<workspace>/                         ← Agent workspace (meta artifacts)
├── SPEC.md   PLAN.md   TASKS.md
├── AGENTS.md (or CLAUDE.md)
├── LESSONS.md   PROGRESS.md
├── MIGRATION.md                     (MIGRATE mode only)
├── docs/
│   ├── architecture.md   golden-principles.md
│   ├── boundaries.md     patterns/
│   └── agents-roster.md  task-routing.md  (multi-agent only)
└── <project-name>/                  ← The actual project repo
    ├── src/ ...
    ├── package.json (or equivalent)
    ├── README.md                    (clean — no AI/framework references)
    ├── .gitignore
    └── [stack-specific files]
```

**Rules:**
- `git init` runs **inside `<project-name>/`**, never in the workspace.
- The project's `README.md` is for end users — no mention of AGENTS.md, SPEC.md, framework, or AI assistance.
- AGENTS.md references (Build & Test commands, file paths) point into `<project-name>/` since that's where the code lives, but AGENTS.md itself stays in the workspace.
- The workspace may have its own `.git` for tracking meta artifacts, but it is separate from the published project repo.
- RETROFIT: if the existing repo already mixes artifacts and code, propose migrating to this layout before generating anything new.

---

## OPERATION MODE

Ask: **"Starting from scratch, applying to an existing project, or evolving a project already using the framework?"**

| Mode | When | Action |
|------|------|--------|
| BOOTSTRAP | New | Full discovery, generates everything (workspace + `<project-name>/` subdir) |
| RETROFIT | Existing | Analyzes repo, generates what's missing. If artifacts/code are mixed → propose splitting into workspace + subdir |
| EVOLVE | Already uses framework | Re-reads artifacts, updates |
| MIGRATE | Existing system needs to be migrated | Analyzes legacy, defines strategy, generates structure + MIGRATION.md |

### RETROFIT
1. **Analyze repo** — AGENTS.md, CLAUDE.md, .cursorrules, docs, tests, linter?
2. **Diagnose** — ✅ has it, ⬜ missing, 🔌 detected, ⚠️ conflict. Confirm.
3. **Focused interview** — ONLY questions that cannot be inferred from the code.
4. **Generate missing artifacts** — Only what's missing. Different format → "Migrate or keep?"

### EVOLVE
1. **Re-read** — Does SPEC still hold? Obsolete TASKS? New patterns? Tools?
2. **Ask** — "What changed? New tools? Pain points? Useless artifact?"
3. **Propose** — 📝 update, ➕ add, 🗑️ remove, 🔌 tools. Confirm.

### MIGRATE
1. **Understand the legacy** — Is there documentation? Tests? Technical owner available? What's the health status?
2. **Assess risk** — Zero-downtime mandatory? Maintenance window available? Impact of an outage?
3. **Adapted discovery** — P1–P4 standard + migration-specific questions:

**M1 — Legacy:** "What exists today? Current stack, documentation status, are there tests, is there a technical owner available for consultation?"
→ Infer: legacy complexity, hidden risks, depth of mapping required.

**M2 — Risk and continuity:** "Is zero-downtime mandatory? Is there an available maintenance window? What's the impact of an outage?"
→ Infer: cutover strategy, level of caution, need for parallel systems.

**M3 — Strategy:** "Do you prefer to migrate everything at once (big bang), replace gradually (strangler fig), or would you like a recommendation based on context?"
→ Infer: plan complexity, required phases, timeline.

**M4 — Data (conditional — if data migration is involved):** "What is the volume, criticality, and is consistency during migration mandatory?"

**MIGRATE summary includes additional fields:**
```
Source system: [stack/platform] | State: [documented|partial|legacy]
Strategy: [big bang|strangler fig|parallel|TBD]
Zero-downtime: [yes|no|window: X]
Data: [yes|no|volume: X]
```

4. **Mandatory additional artifact** — `MIGRATION.md` (template at `templates/MIGRATION.md`)

---

## PHASE 1 — DISCOVERY

**4-5 dense questions.** Extract the maximum from each answer. Infer from context. Only ask back if something critical is ambiguous. Offer A/B/C options in 1 line.

**P1 — Project:** "What is it, for whom, and what does it need to do in the first delivery?"
→ Infer: type, scope, priorities, stage.

**P2 — Environment:** "Stack (preferred, already in use, or want a recommendation?), AI agent, solo or team, budget?"
→ Infer: technical constraints, tools, scale. §21: stack based on the project.

**P3 — Ecosystem:** "Does your agent/IDE support extensions or integrations? (e.g.: plugins, automations, persistent memory) Want recommendations?"
→ Infer: existing ecosystem, integration opportunities, compatibility with standard tools.

**P4 — Concerns:** "What worries you most? Anything the system should NEVER do?"
→ Infer: priorities, boundaries.

**P5 (conditional — multi-agent/complex):** "Do you plan to run agents in parallel? Have you used subagents before?"

### Finalization — Structured summary:

```
═══════════════════════════════════════
📋 DISCOVERY SUMMARY
═══════════════════════════════════════
Project: [name] | Type: [POC|MVP|Product|Refactor]
Stack: [based on project] | Agent: [tool]
Scale: [Solo|Team|Multi-agent]
Ecosystem: [existing/desired]
Concern: [main] | Constraints: [never]
Artifacts: [list] | Workspace: [normal|split]
═══════════════════════════════════════
```

Confirm. Complex projects → deepen design in blocks before generating.

---

## PHASE 1.5 — ECOSYSTEM AND CONSISTENCY

After discovery is approved, before deciding on artifacts.

### Standard tools (always)
- **Spec creation skill** (Superpower Skills or equivalent)
- **Reviewer agent** — research best option for stack/agent (§20, mandatory)

### Token optimization (always recommend)
- **RTK** (rtk-ai/rtk) — CLI proxy that compresses command outputs by 60-90%. Install with `rtk init -g` (Claude Code) or the agent's flag.
- **Caveman skill** (JuliusBrussee/caveman) — skill that reduces output tokens by ~75% via ultra-concise responses. Install with `claude install-skill JuliusBrussee/caveman`.
- **Lean CLAUDE.md** — keep <500 tokens, use references to sub-docs instead of a monolith.
- **Model routing** — Opus for architecture, Sonnet for day-to-day, Haiku for lookups.
- **CLI > MCP** — prefer native CLIs (gh, etc.) over MCP servers when available.

### Persistent memory (always recommend)
- **MemPalace via CLI** — cross-session memory, 96.6% recall, 100% local, zero API.
  Install: `pip install mempalace && mempalace init ~/project`
  Use via CLI (NOT MCP — avoids overhead of 19 tool definitions in context):
  - Hook SessionStart: `mempalace wake-up > context.txt` (~170 injected tokens)
  - On-demand search: `mempalace search "query"` (bash, no MCP)
  - Hook Stop: auto-save hook saves every 15 messages
  - Hook PreCompact: emergency save before context compression
- **Native Auto Memory** — built-in in Claude Code v2.1.59+. Check if active (`/memory`). Saves learnings to `~/.claude/projects/<project>/memory/`.
- **Session handoff** — PROGRESS.md updated at the end of each session (already covered by the framework).

### Proactive research
Search GitHub for tools relevant to the project. Include only tools that meet **all** criteria:
- ⭐ Stars relevant to the niche (context matters — 500 stars in a specialized lib can be excellent)
- 📅 Recent commit (last 6 months)
- 🐛 Healthy open/closed issue ratio (not abandoned)
- 📖 Clear README and documentation
- 🔒 No known vulnerabilities in dependencies (check via repo's Dependabot alerts)

Categories: automations/plugins for the agent in use, stack quality gates, reviewer agent, workflow tools.

### Proposal to the user

```
═══════════════════════════════════════
🔌 RECOMMENDED ECOSYSTEM
═══════════════════════════════════════
Standard:
  ✅ [Specs skill] — [purpose]
  ✅ [Reviewer agent] — [purpose]
  ✅ RTK — command output compression (-60-90% tokens)
  ✅ Caveman — concise responses (-75% output tokens)
  ✅ MemPalace (CLI) — cross-session persistent memory (96.6% recall, local)

Recommended:
  📦 [Tool] — [purpose] (⭐ Xk, updated [date])

Upgrade path:
  🔮 [Tool] — [when to adopt]
═══════════════════════════════════════
```

If accepted → document in AGENTS.md, CLAUDE.md, PLAN.md. Actual installation → T-01.

---

## PHASE 2 — ARTIFACT DECISION

### Inclusion rules

Column **Location** indicates where the file lives — `workspace` (meta artifact) or `<project>/` (end-user visible, §31).

| Condition | Artifacts | Location |
|-----------|-----------|----------|
| Always | SPEC.md · PLAN.md · TASKS.md | workspace |
| Always | README.md | `<project>/` (clean, no AI refs) |
| Uses AI agent | AGENTS.md | workspace |
| MIGRATE mode | MIGRATION.md | workspace |
| Claude Code | CLAUDE.md | workspace |
| Has constraints | docs/boundaries.md | workspace |
| >1 session | LESSONS.md · PROGRESS.md | workspace |
| Production/existing | docs/architecture.md · docs/golden-principles.md · docs/patterns/ | workspace |
| Multi-agent | docs/agents-roster.md · docs/task-routing.md | workspace |

### Research before creating (§19)
- **patterns/, configs, hooks** → battle-tested GitHub → customize
- **SPEC, PLAN, TASKS, AGENTS** → templates at `templates/[NAME].md` + discovery

### Ecosystem adaptation
Tools accepted in 1.5 → do not duplicate functionality, reference/integrate, document in AGENTS.md.

---

## PHASE 3 — GENERATION

1. Pattern/config based on GitHub → customize
2. Otherwise → template `templates/[NAME].md` + discovery
3. Missing info → `[DEFINE: explanation]`

**Rules:** create complete structure at once; project-specific; keep template sections; concrete stack examples; RETROFIT: only what's missing; EVOLVE: only what changed.

**Directory setup (§31):** generate workspace artifacts at the root and create `<project-name>/` subdirectory for the actual project. Run `git init` inside `<project-name>/`, never in the workspace. The project's `README.md` describes the product — no mention of AGENTS.md, SPEC.md, framework, or AI assistance.

**Enforcement in boundaries.md (§10):**
```
- [Rule] → Enforced by: [tool/hook/linter]
  OR
- [Rule] → [manual review]
```

**Tools from Phase 1.5:** document installation in AGENTS.md, CLAUDE.md, PLAN.md. Execution → T-01.

**Consistency check (§27):**
- Do cross-references match?
- Do names match across artifacts?
- Are constraints enforced? Do patterns use the declared stack?
- Is enforcement indicated? Does the project README stay clean (§31)?
- Is the stack justified by the project (§21)?

---

## PHASE 4 — REVIEW AND DELIVERY

1. File tree with descriptions
2. Ecosystem tools documented
3. Reviewer agent configured
4. Inconsistencies corrected
5. "Want to review any file?"
6. Incorporate feedback → Approval:

```
═══════════════════════════════════════
✅ DONE — [Bootstrap|Retrofit|Evolve]
Files: [N] | Ecosystem: [tools]
Reviewer: [configured] | Fixes: [N]
→ Open TASKS.md, request T-01
→ Review output after each task
→ Errors → LESSONS.md → system improves
═══════════════════════════════════════
```
