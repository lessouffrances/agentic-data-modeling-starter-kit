---
name: sync-docs
description: Update SPEC.md and docs/DECISIONS.md to reflect recent modeling and pipeline changes. Use after completing a feature, refactor with contract impact, or when the user says "sync docs", "update the spec", or "log this decision".
---

# Sync Docs Skill (Data Modeling)

## When called after a modeling or pipeline change
1. Read the most recent git log (`git log --oneline -10`) to identify what changed.
2. Open `SPEC.md` and:
   - Mark completed items `[x]` in the backlog or modeling sections.
   - Add or adjust any brief descriptions needed to reflect the new models/pipelines.
3. Add a changelog entry:
   ```
   | YYYY-MM-DD | <short hash> | <what changed> |
   ```
4. Commit:
   ```
   docs(spec): mark <modeling change> complete [<hash>]
   ```

## When called after an architectural or governance decision
Ask the human:
- What was decided? (e.g. new modeling framework, new contract policy, new environment strategy)
- Why?
- What does it affect? (domains, models, environments, SLAs)

Then add an ADR entry to `docs/DECISIONS.md`:
```markdown
## ADR-<N>: <Short title>
**Date:** YYYY-MM-DD
**Status:** Accepted
**Context:** <why>
**Decision:** <what>
**Consequences:** <impact>
```

Commit:
```
docs(decisions): add ADR-<N> <short title>
```

## Guardrails
- Never rewrite sections the human authored
- Never delete changelog entries
- Never change feature or modeling descriptions, only their status markers and brief summaries

