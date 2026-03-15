# Agentic Data Modeling Starter Kit

A reusable starter kit for **agentic, AI-assisted data modeling and data transformation**. Drop it into any new analytics or data platform repo and get a structured agent workflow out of the box — with consistent commits, living docs, and clear rules for what the agent can do to your data models and pipelines versus what you decide.

---

## What's included

```
CLAUDE.md                        ← Agent's operating manual (read every session)
SPEC.md                          ← Living modeling spec (human + agent co-own)
docs/
  DECISIONS.md                   ← Architecture decision log (ADRs) for data + modeling
.claude/
  BOOTSTRAP_FORM.md              ← Fill this once to describe data stack, sources, and safety
  rules/
    approval-gates.md            ← Actions that require human sign-off (e.g. schema changes)
    commit-rules.md              ← Conventional Commits enforcement
    definition-of-done.md        ← Checklist the agent runs before every commit
    doc-sync.md                  ← How the agent keeps docs in sync with models and pipelines
  skills/
    bootstrap/SKILL.md           ← /bootstrap — scaffold a new data modeling project
    new-feature/SKILL.md         ← /new-feature — plan and build a new model or transformation
    refactor/SKILL.md            ← /refactor — plan and execute a refactor (semantics preserved)
    sync-docs/SKILL.md           ← /sync-docs — update spec and decision log
    commit/SKILL.md              ← /commit — guided Conventional Commit
```

---

## Getting started

**1. Fill in the bootstrap form**

Open `.claude/BOOTSTRAP_FORM.md` and fill in:

- **Data domains and sources** (e.g. sales, marketing, OLTP DBs, SaaS tools)
- **Storage and compute** (e.g. warehouse, lake, execution engine, orchestration)
- **Modeling conventions** (layers, grain, SCD rules, time zones)
- **Data quality and governance** (tests, contracts, backfill policy)
- **Agent behaviour** (safety mode, allowed scopes, review rules)

Every field you leave as `~` will be asked about interactively during bootstrap.

**2. Run bootstrap**

Open Claude Code in the project root and run:

```
/bootstrap
```

The agent will read your form, scaffold the directory structure, generate starter config files, initialise git (if needed), and populate `SPEC.md` and `docs/DECISIONS.md` with data-focused templates.

**3. Add your first modeling work to SPEC.md**

Open `SPEC.md` and add descriptions under a backlog section, for example:

- New staging models for a source system
- New core/mart models for a domain (e.g. orders, customers)
- New data quality checks or contracts

These are yours to write — the agent only updates status markers and the changelog.

**4. Start building**

Use `/new-feature` to kick off any modeling or pipeline feature. The agent will ask one clarifying question if needed, present a plan for your approval, then execute step by step with commits along the way.

**5. Connect and store data**

Depending on your answers in `BOOTSTRAP_FORM.md`, configure how real data is stored and accessed:

- For **warehouses/lakes**: point connection configs (e.g. profiles, connection strings, credentials) at a sandbox or dev environment first.
- For **local/demo work**: add small sample datasets (e.g. CSV/Parquet in a `data/` or `seeds/` folder) that the agent can use when building models and tests.
- For **data ingestion**: decide whether this repo owns extraction/landing or assumes upstream tables already exist, and document that in `SPEC.md`.

The agent will treat these locations as the source of truth when creating models, transformations, and data quality checks.

---

## Slash commands

| Command | What it does |
|---|---|
| `/bootstrap` | Scaffold a new data modeling project from `.claude/BOOTSTRAP_FORM.md` |
| `/new-feature` | Plan and build a new model, transformation, or data check |
| `/refactor` | Plan and execute a refactor while preserving data semantics |
| `/sync-docs` | Update `SPEC.md` and `docs/DECISIONS.md` after modeling/pipeline changes |
| `/commit` | Create a well-formed Conventional Commit with pre-commit checks |

---

## How ownership is divided

| Agent does autonomously | Human must approve |
|---|---|
| Write and edit data models, tests, and pipeline code | Choice of warehouse, lake, engines, and modeling frameworks |
| Run lint, type-check, and data tests | Destructive schema changes in production-like environments |
| Commit on non-protected branches | Merges to protected branches |
| Update `SPEC.md` status and changelog | Modeling requirements, SLAs, and governance policies |
| Log ADRs to `DECISIONS.md` | Decisions that contradict existing ADRs |
| Generate boilerplate and config | New dependencies or major architectural shifts |

A full list of approval gates is in `.claude/rules/approval-gates.md`.

---

## How to request a modeling change

Use this template when prompting the agent:

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

Or just run `/new-feature` and the agent will ask you the right questions.

---

## Design principles

**Lean context.** `CLAUDE.md` is kept short and acts as an index. Detail lives in `.claude/rules/` and `.claude/skills/`, loaded on demand rather than injected into every session.

**Rules vs skills.** Rules (`.claude/rules/`) are reference content the agent reads passively when relevant. Skills (`.claude/skills/`) are task workflows invoked explicitly with a slash command.

**Human owns decisions, agent owns execution.** The agent never chooses warehouses, changes governance policies, or merges to a protected branch on its own. `SPEC.md` has explicit ownership comments so neither side overwrites the other's work.

**Data safety first.** Approval gates cover destructive schema changes, infra changes, and external side effects. The agent should prefer additive and backward-compatible changes unless told otherwise.

**Commit discipline.** Every commit follows [Conventional Commits](https://www.conventionalcommits.org/). The `/commit` skill runs lint and type/data-checks before staging anything, and shows the commit message for confirmation before writing it.

---

## Reusing this kit

Copy the entire `.claude/` directory, `CLAUDE.md`, and `SPEC.md` into any new data project. Then:

1. Clear `SPEC.md` down to the template placeholders
2. Re-fill `.claude/BOOTSTRAP_FORM.md` for the new project's stack and data domains
3. Run `/bootstrap`

Everything else carries over unchanged.

---

## Contributing

Contributions welcome. Good places to start:

- Add rules for a workflow not yet covered (e.g. backfills, incident response, data contracts)
- Add example projects for different stacks (e.g. dbt+Snowflake, DuckDB+Python, BigQuery-only)
- Improve the wording of existing rules or skills for clarity and consistency

