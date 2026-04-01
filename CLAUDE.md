# Release Strategy

## Branch / Environment Mapping

| Branch              | Environment | Short name |
|---------------------|-------------|------------|
| `main`              | Production  | prod       |
| `quality-assurance` | QA          | qa         |
| `development`       | Development | dev        |

## Promotion Flow

```
feature branches → dev → qa → prod
```

- Feature branches merge into `dev` via **squash merge**
- Promotions between environment branches (`dev → qa → prod`) use **merge commits**

## Merge Methods

| PR type                | Merge method |
|------------------------|-------------|
| Feature branch → `dev` | Squash      |
| `dev` → `qa`           | Merge       |
| `qa` → `prod`          | Merge       |

## Version Bump Automation (planned)

GitHub Action that triggers when a PR from `dev` → `qa` is merged:

1. Bumps version on `dev` (defaults to patch if not specified)
2. Cherry-picks/merges the same commit into `qa`
3. Both branches end up with the identical version commit

Auth: GitHub App with scoped permissions to bypass branch protection.
