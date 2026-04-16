# Migration — [Project Name]

<!-- Mandatory artifact in MIGRATE mode. Maps source → destination, defines strategy, and ensures rollback and parity. Principles §28, §29, §30. -->

## Source System

- **Current stack:** [language, framework, database, infra]
- **Documentation state:** [complete | partial | absent | undocumented legacy]
- **Test coverage:** [% or "no tests"]
- **Main modules:** [list existing modules/services]
- **Critical dependencies:** [external integrations, services that depend on this system]
- **Technical owner:** [who knows the current system and can be consulted]

## Migration Scope

- **What migrates:** [what will be moved to the destination system]
- **What stays:** [what remains in the source system after migration]
- **What is discarded:** [features that will not be migrated and why]

## Strategy

<!-- §28: map before migrating. Choice based on project context. -->

**Chosen approach:** [Big bang | Strangler fig | Parallel execution | Phased migration]

**Justification:** [why this approach given the context: risk, deadline, zero-downtime, data volume]

**Discarded alternative:** [X, because Y]

## Source → Destination Mapping

| Module/Component (Source) | Equivalent (Destination) | Notes |
|---------------------------|--------------------------|-------|
| [module] | [new module] | [changes, simplifications, breaking changes] |
| [module] | [new module] | |

### Data Mapping (fill in if there is data migration)

| Table/Entity (Source) | Table/Entity (Destination) | Required Transformations |
|-----------------------|---------------------------|--------------------------|
| [table] | [table] | [e.g.: normalization, renaming, split] |

## Rollback Plan

<!-- §29: rollback is a prerequisite. This plan must be validated BEFORE starting the migration. -->

**Rollback trigger:** [criterion that activates rollback — e.g.: error rate > X%, response time > Xms, corrupted data detected]

**Rollback steps:**
1. [concrete step — e.g.: redirect traffic back to source system]
2. [concrete step — e.g.: restore database snapshot from [date]]
3. [concrete step — e.g.: notify stakeholders]

**Responsible:** [who executes the rollback]
**Estimated reversal time:** [e.g.: "< 15 minutes"]
**Rollback window:** [e.g.: "first 48h after cutover"]

## Feature Parity Checklist

<!-- §30: parity verified, not assumed. One line per feature from the source system. -->

| Feature | Acceptance criterion in destination | Verified? |
|---------|-------------------------------------|-----------|
| [feature] | [how to test that the equivalent works] | ⬜ |
| [feature] | [how to test] | ⬜ |

## Cutover Plan

**Cutover strategy:** [big bang in maintenance window | gradual by % of traffic | by user segment]

**Go/No-go criteria:**
- [ ] [e.g.: all parity tests passing]
- [ ] [e.g.: destination system performance validated under load]
- [ ] [e.g.: rollback plan tested in staging]
- [ ] [e.g.: stakeholders notified]

**Phase 1 — Pre-cutover:**
- [concrete action, responsible, deadline]

**Phase 2 — Cutover:**
- [concrete action, responsible, time window]

**Phase 3 — Post-cutover (monitoring):**
- [what to monitor, for how long, success criterion]

## Success Criteria

<!-- Measurable. Compare against source system baseline. -->

| Metric | Baseline (Source) | Target (Destination) | Deadline |
|--------|-------------------|----------------------|----------|
| [e.g.: p95 response time] | [current value] | [target value] | [date] |
| [e.g.: error rate] | [current value] | [target value] | [date] |
| [e.g.: test coverage] | [current value] | [target value] | [date] |

**Definition of "migration complete":** [objective and verifiable criterion]
