# AGENTS.md — [Project Name]

<!-- ~100 LINES MAX. Point to docs/. Update when agent makes mistakes. -->

## Build & Test

- Build: `[command]`
- Test: `[command]`
- Lint: `[command]`
- Dev: `[command]`

## Structure

```
[level 1-2 only]
```

## Conventions

- [e.g.: "Functional components, never class"]
- [e.g.: "Variables in English, comments in English"]
- [e.g.: "Absolute imports @/"]

## Token Optimization

- **RTK:** installed (`rtk init -g`). Command outputs compressed automatically.
- **Caveman:** active. Use `/caveman` for ultra-concise responses.
- **Model routing:** Opus → architecture/complex debug. Sonnet → day-to-day. Haiku → lookups.
- **CLI > MCP:** prefer `gh`, `aws`, native CLIs over MCP servers.
- **Session:** `/compact` between tasks. New sessions every ~80k context tokens.

## Persistent Memory

- **MemPalace (CLI):** context from previous sessions automatically injected via hook at session start (~170 tokens). Before responding about past decisions, search: `mempalace search "relevant query"`. Do NOT use via MCP — use via bash to avoid schema overhead in context.
- **Auto Memory:** active (native Claude Code). Learnings saved automatically in `~/.claude/projects/`.
- **PROGRESS.md:** update at end of each session as fallback and bridging between sessions.

## References

- Architecture: `docs/architecture.md`
- Principles: `docs/golden-principles.md`
- Boundaries: `docs/boundaries.md`
- Patterns: `docs/patterns/`

## Boundaries (Summary)

- ✅ **Always:** [mandatory actions]
- ⚠️ **Ask first:** [actions that need approval]
- 🚫 **Never:** [prohibited actions]
