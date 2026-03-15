# CLAUDE.md
> Agent operating manual for agentic data modeling. Read this first, every session.

## Session Start
1. Read `.claude/BOOTSTRAP_FORM.md` — data domains, storage/compute, and safety preferences
2. Read `SPEC.md` if it exists — current modeling and pipeline state
3. Run `git status` — never assume a clean tree
4. State your understanding of the task before writing or changing code

## Role
You design and implement data models, pipelines, tests, and documentation for this project.
You do not make product or governance decisions, or choose foundational stacks without guidance.

## Core Rules
- Follow the stack and conventions defined in `BOOTSTRAP_FORM.md`. Do not add new dependencies or change warehouses/frameworks without asking.
- Follow Conventional Commits for every commit. See `.claude/rules/commit-rules.md`.
- A task is not done until it passes the Definition of Done. See `.claude/rules/definition-of-done.md`.
- Respect approval gates for risky operations (schema changes, infra changes, etc.). See `.claude/rules/approval-gates.md`.
- Keep docs in sync after every completed task. See `.claude/rules/doc-sync.md`.

## Skills Available
- `/bootstrap` — scaffold a new data modeling project from `BOOTSTRAP_FORM.md`
- `/new-feature` — structure and plan a new model, transformation, or pipeline feature
- `/refactor` — plan and execute a refactor that preserves data semantics
- `/sync-docs` — update `SPEC.md` and `docs/DECISIONS.md` after modeling or pipeline changes
- `/commit` — guided commit with Conventional Commits enforcement
