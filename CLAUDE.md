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

## Version Bump Automation

GitHub Action (`.github/workflows/bump-version.yml`) triggers when a PR from `dev` → `qa` is merged:

1. Generates a short-lived token from the GitHub App (`fddao-version-bumper`)
2. Bumps the patch version in `version.txt` on `dev`
3. Cherry-picks the same commit onto `qa`
4. Both branches end up with the identical version commit

Auth: GitHub App (`fddao-version-bumper`) with Contents: Read & Write, added to branch protection bypass list for `dev` and `qa`. Credentials stored as repo secrets `APP_ID` and `APP_PRIVATE_KEY`.
