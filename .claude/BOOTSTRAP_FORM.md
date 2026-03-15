# BOOTSTRAP FORM
> Fill in this file before running `/project:bootstrap`.
> The agent will read your answers and scaffold the project accordingly.
> Leave any field as `~` if you want the agent to recommend a default.

---

## 1. Project Identity

```
Project name:       Agentic Data Modeling Starter Kit
Short description:  A toolkit and reference implementation for building agentic, AI-assisted data modeling and data transformation workflows.
Primary language:   ~        # e.g. Python, SQL, TypeScript
Primary use case:   ~        # e.g. analytics warehouse, feature store, reporting mart, lakehouse curation
```

---

## 2. Data Domains & Sources

```
Core domains:       ~        # e.g. sales, marketing, product-analytics, finance

Source systems:     ~        # e.g. Postgres OLTP, Stripe, Salesforce, Snowplow, S3, BigQuery, CSV dumps
Source freshness:   ~        # e.g. batch-daily, batch-hourly, streaming, ad-hoc

Data volume:        ~        # e.g. small (<10GB), medium (10GB–1TB), large (1TB+)
PII present:        ~        # yes | no | unknown
```

---

## 3. Storage & Compute Stack

```
Warehouse / DB:     ~        # e.g. Snowflake, BigQuery, Redshift, Postgres, DuckDB, SQLite
Data lake:          ~        # e.g. S3, GCS, Azure Data Lake, none
File formats:       ~        # e.g. parquet, delta, iceberg, csv, json

Execution engine:   ~        # e.g. dbt, Spark, Snowflake SQL, BigQuery SQL, Pandas, Polars
Orchestration:      ~        # e.g. Airflow, Dagster, Prefect, dbt Cloud, GitHub Actions, none
```

---

## 4. Modeling Conventions

```
Modeling framework: ~        # e.g. dbt, custom-SQL, Python-pipelines, metrics-layer, semantic-layer

Layering pattern:   ~        # e.g. staging → core → marts, bronze → silver → gold, flat models only
Grain conventions:  ~        # e.g. one-row-per-event, one-row-per-entity, mixed

Slowly changing:    ~        # e.g. SCD1 only, SCD2 for dimensions, none
Time zones:         ~        # e.g. UTC, source-local, mixed
```

---

## 5. Data Quality & Validation

```
Testing framework:  ~        # e.g. dbt tests, Great Expectations, Soda, custom Python tests, none
Critical checks:    ~        # e.g. non-null ids, uniqueness, referential integrity, freshness thresholds

Data contracts:     ~        # yes | no | planned   (explicit schemas that upstreams must follow)
Backfills allowed:  ~        # yes | no | case-by-case
```

---

## 6. Runtime & Tooling

```
Runtime env:        ~        # e.g. Python 3.11, Node 20, system-SQL-only
Package manager:    ~        # e.g. pip, uv, poetry, npm, pnpm

Code style:         ~        # e.g. Ruff+Black, ESLint+Prettier, none
Type checking:      ~        # e.g. mypy, pyright, TypeScript, none
Git hooks:          ~        # e.g. pre-commit, Husky + lint-staged, none
Commit convention:  ~        # Conventional Commits | none
```

---

## 7. Infrastructure & Environments

```
Execution context:  ~        # local-only | local+cloud | cloud-only
Containerize:       ~        # yes | no  (generates Dockerfile + docker-compose)

Environments:       ~        # e.g. dev, staging, prod
Env config:         ~        # e.g. .env files, Vault, AWS Secrets Manager, Doppler
CI/CD:              ~        # e.g. GitHub Actions, GitLab CI, none
```

---

## 8. Agent Behaviour Preferences

```
Auto-commit:        ~        # yes | no  (agent commits after every completed task)
Doc sync:           ~        # yes | no  (agent updates SPEC.md and DECISIONS.md when code changes)

Safety mode:        ~        # read-only | dry-run | apply   (how aggressively the agent can change data code)
Notify on:          ~        # commit | pr | never  (when agent should pause for human review)
Allowed scopes:     ~        # e.g. models only, tests+docs, orchestration configs, all of the above
```

---

## 9. Team & Governance

```
Solo or team:       ~        # solo | team
Main branch:        ~        # main | master
Protected branches: ~        # e.g. main, staging

Code review:        ~        # required | optional | none
Approval for:       ~        # e.g. schema changes, prod pipelines, dependency changes
```

---

## 10. Anything Else

```
Notes for agent:    ~
# Add anything that doesn't fit above — special constraints, privacy requirements, SLAs, external tools,
# non-standard folder conventions, or existing modeling patterns to respect.
```
