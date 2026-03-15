# Commit Rules
> Follow Conventional Commits on every commit without exception.

## Format
```
<type>(<scope>): <short description>

[optional body]

[optional footer]
```

## Types
| Type | Use for |
|---|---|
| `feat` | New user-facing feature or modeling capability |
| `fix` | Bug fix or correction to models, migrations, or checks |
| `docs` | Documentation only |
| `refactor` | No behaviour change |
| `test` | Adding or fixing tests or data checks |
| `chore` | Tooling, deps, config |
| `style` | Formatting only |

## Rules
- Subject line ≤ 72 chars, imperative mood ("add dimension model", not "added dimension model")
- Scope = the area changed, e.g. `models`, `api`, `warehouse`, `etl`
- Never commit: `.env` files, secrets, build artifacts, `node_modules`
- Never force-push to a protected branch
- One logical change per commit — do not batch unrelated work
- No `TODO`, `FIXME`, or `console.log` in committed code

## Example
```
feat(models): add customer dimension and fact orders

- Introduce slowly changing dimension for customers
- Add fact table for orders with grain order_id
```

