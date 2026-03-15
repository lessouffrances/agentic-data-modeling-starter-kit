---
name: bootstrap
description: Scaffold a new data modeling project from BOOTSTRAP_FORM.md. Use when the user says "bootstrap the project", "set up the project", or runs /bootstrap for the first time.
---

# Bootstrap Skill (Data Modeling)

## Step 1 — Validate the form
Read `.claude/BOOTSTRAP_FORM.md`. Check that these fields are filled (not `~`):
- Project name
- Primary use case
- Warehouse / DB (or primary storage)
- Modeling framework / execution engine

If any required field is missing, list them and stop. Do not guess or use defaults without asking.

## Step 2 — Generate directory structure
Based on the filled form and conventions:

**dbt-style project (or SQL-first modeling):**
```
models/
  staging/
  core/
  marts/
tests/
seeds/            ← optional sample data
data/             ← optional raw/demo files
```

**Python/Notebook-centric project:**
```
src/
  pipelines/
  models/
  io/            ← connectors, readers/writers
  quality/       ← tests, expectations, contracts
notebooks/
data/
```

If the form clearly indicates another pattern (e.g. lakehouse bronze/silver/gold), adapt the folder names accordingly but keep it simple and well-documented in `SPEC.md`.

## Step 3 — Generate config files
Create starter config files matching the chosen stack. Examples:
- `pyproject.toml` / `requirements.txt` / `environment.yml` for Python tooling
- `dbt_project.yml` and `profiles` stub if using dbt
- `.env.example` with placeholder connection details (never real secrets)
- `Dockerfile` + `docker-compose.yml` if containerize: yes
- CI config (e.g. `.github/workflows/ci.yml`) if CI/CD: GitHub Actions or similar

Always keep secrets out of version control and use placeholders instead.

## Step 4 — Generate SPEC.md
Create `SPEC.md` using this template:

```markdown
# Data Modeling Spec: <Project Name>

_Last updated: <date>_

## Overview
<Short description and primary use case from BOOTSTRAP_FORM.md>

## Data Stack
- Warehouse / DB: <from BOOTSTRAP_FORM.md>
- Data lake: <if any>
- Execution engine / framework: <dbt / SQL / Python / Spark / etc.>
- Orchestration: <if any>

## Domains & Sources
- Domains: <from BOOTSTRAP_FORM.md>
- Source systems: <from BOOTSTRAP_FORM.md>

## Modeling Layers
Describe the intended layers (e.g. staging, core, marts) and their roles.

## Backlog
_Fill this in as development progresses._

- [ ] <First modeling or pipeline task>

## Changelog
| Date | Commit | Change |
|------|--------|--------|
| <date> | — | Initial scaffold |
```

## Step 5 — Generate docs/DECISIONS.md
Log the initial tech choices using ADR format (see `.claude/rules/doc-sync.md`).
Start with ADR-001 for repository structure, ADR-002 for storage/compute stack, ADR-003 for modeling framework.

## Step 6 — Init git and commit
If git is not initialised yet:
```bash
git init
git add .
git commit -m "chore: initial data modeling scaffold"
```

## Step 7 — Print summary
List what was created and tell the human what to do next:
1. Fill in `SPEC.md` with their first modeling and data tasks
2. Connect to real or sample data as described in the README
3. Run `/new-feature` when ready to build something

