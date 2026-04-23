# Tasks — [Project Name]

<!-- Decomposed work. Agent handles one at a time, validates, advances. -->

## Status: ⬜ Pending · 🔄 In Progress · ✅ Done · ⏸️ Blocked

### T-01: Project setup and tooling
- **Status:** ⬜
- **Depends on:** —
- **Description:** Create `<project-name>/` subdirectory (§31), scaffold the project inside it, install deps, run `git init` inside `<project-name>/`. Configure RTK + Caveman + MemPalace (CLI + hooks) + linter + hooks. Configure MemPalace hooks in `.claude/settings.json` (SessionStart → wake-up, Stop → auto-save, PreCompact → emergency save). Verify native Auto Memory active. Meta artifacts (SPEC, PLAN, TASKS, AGENTS, docs/) stay in the workspace — never copied into `<project-name>/`.
- **Acceptance criteria:** `<project-name>/` exists with scaffolded project, `git rev-parse --git-dir` inside it resolves to `<project-name>/.git`, project's `README.md` has no AI/framework references, RTK intercepting (`rtk gain`), Caveman available, `mempalace status` returns initialized palace, MemPalace hooks registered, Auto Memory active
- **Files:** `<project-name>/[stack manifest]`, `<project-name>/.gitignore`, `<project-name>/README.md`, AGENTS.md (workspace), RTK config, .claude/settings.json

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
