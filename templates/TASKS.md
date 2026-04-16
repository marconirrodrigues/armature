# Tasks — [Project Name]

<!-- Decomposed work. Agent handles one at a time, validates, advances. -->

## Status: ⬜ Pending · 🔄 In Progress · ✅ Done · ⏸️ Blocked

### T-01: Project setup and tooling
- **Status:** ⬜
- **Depends on:** —
- **Description:** Initialize project, install deps, configure RTK + Caveman + MemPalace (CLI + hooks) + linter + hooks. Configure MemPalace hooks in `.claude/settings.json` (SessionStart → wake-up, Stop → auto-save, PreCompact → emergency save). Verify native Auto Memory active.
- **Acceptance criteria:** Project runs, RTK intercepting (`rtk gain`), Caveman available, `mempalace status` returns initialized palace, MemPalace hooks registered, Auto Memory active
- **Files:** package.json, .gitignore, AGENTS.md, RTK config, .claude/settings.json

### T-02: [Descriptive name]
- **Status:** ⬜
- **Depends on:** T-01
- **Description:** [what to do]
- **Acceptance criteria:** [how to know it's done]
- **Files:** [created/modified]

### T-03: [Descriptive name]
- **Status:** ⬜
- **Depends on:** T-02
- **Description:** [what to do]
- **Acceptance criteria:** [how to know it's done]
- **Files:** [created/modified]

<!-- Independent tasks → run in parallel (multi-agent). -->
