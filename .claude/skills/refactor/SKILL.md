---
name: refactor
description: Plan and execute a refactor of models, SQL, or pipeline code with preserved behaviour. Use when the user asks to refactor, clean up, simplify, extract, or reorganise existing data logic without changing what the data means.
---

# Refactor Skill (Data Modeling)

## Step 1 — Parse the request
Identify:
- **Target:** Which model(s), file(s), schema(s), or pipeline(s)
- **Goal:** What kind of refactor (extract common CTEs, standardise naming, split large models, remove duplication, simplify joins, reorganise folders, etc.)
- **Constraint:** Data semantics and outputs must stay the same (no new features, no breaking contract changes)

If any of these are unclear, ask ONE clarifying question. Do not guess scope.

## Step 2 — State a plan
Before changing code, output a short plan. Include:

```
Plan for: <refactor name>

1. <first change — e.g. Extract shared CTE into reusable model or macro>
2. <second change — e.g. Standardise naming for key columns>
…
N. Run tests to confirm behaviour and outputs unchanged

- In scope: <what will change>
- Out of scope: <what will NOT change (schemas, contracts, SLAs, etc.)>
- Behaviour: preserved (existing tests must still pass)

Confirm to proceed, or adjust the plan.
```

Wait for the human to say "go" or modify the plan.

## Step 3 — Execute step by step
- Make small, logical changes. One commit per logical step where possible.
- After each step: run relevant checks (SQL compile, dbt run/test, unit tests, linters).
- Commit with Conventional Commits (see `.claude/rules/commit-rules.md`). Use type `refactor:` for refactor-only commits, e.g. `refactor(models): deduplicate customer join logic`.

## Step 4 — Verify behaviour
- Run the full data test suite or an appropriate subset that covers the changed models/pipelines.
- If no tests exist, describe how the human can verify that row counts, key distributions, and important metrics remain consistent.
- Do not proceed if tests fail; fix the cause (refactor or test) before committing.

## Step 5 — Check Definition of Done
Go through `.claude/rules/definition-of-done.md`. Ensure no new lint/type errors, no stray TODOs or console.logs, and commits follow the convention.

## Step 6 — Sync docs (if needed)
If the refactor changes architecture, folder layout, or public contracts, run the doc sync procedure from `.claude/rules/doc-sync.md` (e.g. update DECISIONS.md with an ADR). For purely internal cleanups, you can skip ADRs.

---

## Prompt Template (give this to the human on request)

When the user asks "how do I request a refactor?" or "give me the refactor template", output:

```
## Refactor Request

**Target:** <model(s), file(s), schema(s), or area — e.g. "models/staging/stripe", "customer_dim", "etl for orders">

**Goal:** <what to improve — e.g. extract repeated logic, rename for clarity, split large model, standardise keys>

**Constraint:** Data semantics unchanged. Existing tests (or agreed checks) must still pass.

**Out of scope:** <what NOT to change — e.g. table names, external contracts, SLAs>
```

