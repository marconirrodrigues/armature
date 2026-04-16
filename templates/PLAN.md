# Technical Plan — [Project Name]

<!-- HOW to build. Update when technical decisions change. -->

## Stack

| Layer | Technology | Justification |
|-------|-----------|---------------|
| Language | [DESCRIBE] | [why] |
| Framework | [DESCRIBE] | [why] |
| Database | [DESCRIBE] | [why] |
| Tests | [DESCRIBE] | [why] |

## Architecture

[how the system is organized, data flow, module boundaries]

## Technical Decisions

<!-- Decision → Reason → Discarded alternative -->

1. **[Decision]:** [Reason]. Discarded: [X, because Y].

## Directories

```
src/
├── [folder]/    ← [purpose]
├── [folder]/    ← [purpose]
└── [folder]/    ← [purpose]
```

## Dependencies

- [Dep]: [purpose, version]

## Token Optimization and Memory Tooling

- RTK: `rtk init -g [--gemini|--codex|--agent cursor]`
- Caveman: `claude install-skill JuliusBrussee/caveman`
- MemPalace (CLI): `pip install mempalace && mempalace init ~/project`
  - Hooks configured in `.claude/settings.json` (SessionStart, Stop, PreCompact)
  - Search via bash: `mempalace search "query"` (without MCP)
- Native Auto Memory: verify active via `/memory`
- Model routing configured in AGENTS.md
