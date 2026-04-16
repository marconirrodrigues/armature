# Armature — Agent Engineering Framework

A framework that interviews you about your project and generates a complete structure — Spec-Driven Development, Harness Engineering, and Orchestration Engineering.

## How it works

```
Discovery → Ecosystem → Decision → Generation → Review
(4-5 qs)   (research)  (tailored)  (files)     (approve)
```

### Key features
- **Stack-agnostic** — recommends based on the project, not preferences
- **Research before creating** — battle-tested patterns as a foundation
- **Reviewer agent by default** — validation by a second agent
- **Explicit enforcement** — every rule indicates how it's enforced
- **Token-optimized** — RTK + Caveman integrated by default
- **4 modes** — Bootstrap, Retrofit, Evolve, Migrate

## Quick Start

```bash
# Claude Code
claude "Read FRAMEWORK.md and start the process for my project"

# Any agent — open FRAMEWORK.md as context
# Chat — paste FRAMEWORK.md and ask to start
```

## Structure

```
├── FRAMEWORK.md          ← Discovery + decision + generation
├── templates/            ← Base templates (on demand)
│   ├── SPEC.md  PLAN.md  TASKS.md  AGENTS.md
│   ├── BOUNDARIES.md  LESSONS.md  PROGRESS.md
│   ├── ARCHITECTURE.md  GOLDEN-PRINCIPLES.md
│   ├── PATTERNS.md  AGENTS-ROSTER.md  TASK-ROUTING.md
│   ├── MIGRATION.md
│   └── README.md
├── guia-completo.html    ← Full reference guide (HTML)
└── README.md
```

## v2.0 — Changelog

- **MIGRATE mode** — 4th operation mode for system migrations (stack, database, cloud, architecture). Specific M1–M4 discovery, dedicated MIGRATION.md template.
- **MIGRATION.md template** — MIGRATE mode artifact: origin→destination mapping, strategy, rollback, feature parity checklist, cutover plan, success criteria.
- **Principles §28–§30** — Expanded Constitution with 3 migration principles: map before migrating, rollback as prerequisite, verified parity.
- **Agnostic P3** — Discovery P3 with generic terms (plugins, automations, integrations) — works with any provider/IDE/model.
- **Explicit quality criteria** — Phase 1.5 "Proactive research" with 5 objective criteria.
- **Improved SPEC.md** — New Assumptions and Open Questions sections.
- **Multica removal** — Framework 100% agnostic of project management tooling.

## v1.4.1 — Changelog

- **Native persistent memory** — MemPalace integrated via CLI + hooks (no MCP, zero schema overhead). Auto-save hooks, automatic wake-up (~170 tokens), on-demand search via bash.
- **Native Auto Memory** — Verification and activation of Claude Code's built-in system as a complement.
- **Native token optimization** — RTK + Caveman as standard tools in Phase 1.5.
- Lean CLAUDE.md (<500 tokens) as best practice.
- Model routing and CLI > MCP as default recommendations.
- FRAMEWORK.md compressed ~40% without semantic loss.

## Integrated concepts

| Concept | Solves | Source |
|---------|--------|--------|
| Spec-Driven | "What to build" | Spec Kit, Osmani, Thoughtworks |
| Harness | "How the agent operates" | OpenAI, Hashimoto, Anthropic |
| Orchestration | "Who does what" | Osmani, O'Reilly, LangChain |

## License

MIT
