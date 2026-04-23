# Boundaries — [Project Name]

<!-- Agent permissions. Update when agent does something it shouldn't. -->

## ✅ Always

- Run tests before committing
- Follow conventions in AGENTS.md
- Keep imports organized
- [project rule]

## ⚠️ Ask First

- Add dependencies
- Modify database schema
- Modify CI/CD
- Create public endpoints
- [project rule]

## 🚫 Never

- Commit secrets/tokens/credentials
- Remove/disable linter rules
- Modify production config
- Delete tests to make build pass
- Add AI/framework/agent references to the project's `README.md` or any end-user-facing doc (§31 — workspace artifacts stay in the workspace)
- Run `git init` in the workspace — it belongs inside `<project-name>/`
- Move meta artifacts (SPEC, PLAN, TASKS, AGENTS, LESSONS, PROGRESS, docs/) into `<project-name>/`
- [project rule]
