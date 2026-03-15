---
name: new-feature
description: Structure and plan a modeling or pipeline feature request. Use when the user asks to build a new model, transformation, data quality check, or small ingestion/pipeline change, or says "I want to add X".
---

# New Feature Skill (Data Modeling)

## Step 1 — Parse the request
If the user's request is missing any of the following, ask ONE clarifying question before proceeding:
- What the change does (e.g. new model, transformation, test, or pipeline step)
- Where it lives (which domain, layer, or folder)
- Acceptance criteria (how to know data and behaviour are correct)

Do not ask more than one question at a time.

## Step 2 — State a plan
Before writing any code, output a numbered plan (3–8 steps). Example:

```
Plan for: <modeling or pipeline change name>

1. Create/modify staging models for <source>
2. Add/adjust core or mart model <model_name> at grain <grain>
3. Add or update data tests (e.g. uniqueness, not-null, relationships)
4. (Optional) Adjust orchestration or configs if needed
5. Run data tests and verify results
6. Update SPEC.md and DECISIONS.md if needed

Confirm to proceed, or adjust the plan.
```

Wait for the human to say "go" or modify the plan.

## Step 3 — Execute step by step
Work through the plan one step at a time. After each step:
- Run the appropriate lint/type/data checks on changed files or models
- Commit with a Conventional Commit message (see `.claude/rules/commit-rules.md`)

Prefer additive, backward-compatible changes unless explicitly told otherwise.

## Step 4 — Run tests
After all steps are complete, run the configured data and/or unit tests. Report results. Do not proceed if tests fail.

## Step 5 — Check Definition of Done
Go through `.claude/rules/definition-of-done.md` item by item. Confirm each is satisfied.

## Step 6 — Sync docs
Run the doc sync procedure from `.claude/rules/doc-sync.md`.

---

## Prompt Template (give this to the human on request)

When the human asks "how do I request a modeling change?" or "give me the template", output this:

```
## Modeling Request

**What:** <one sentence — what model / pipeline / check you want>

**Why:** <business or analytics reason; which metric or use case this supports>

**Acceptance criteria:**
- [ ] <testable outcome 1, e.g. "orders_fct has one row per order">
- [ ] <testable outcome 2, e.g. "customer_dim exposes current and historical attributes">

**Scope:**
- In: <what to build or change (models, tests, docs, etc.)>
- Out: <what NOT to touch (upstreams, other domains, prod env, etc.)>

**Notes:** <edge cases, important joins, privacy constraints, SLAs, contracts>
```

