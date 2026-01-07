# Contributing

## Git Flow Branching Model

This repository follows the [Git Flow](https://nvie.com/posts/a-successful-git-branching-model/) branching model.

### Branch Structure

| Branch | Purpose |
|--------|---------|
| `main` | Production-ready releases. Tagged with semantic versions. |
| `develop` | Integration branch for features. Next release candidate. |
| `feature/*` | New features and enhancements |
| `release/*` | Release preparation and final testing |
| `hotfix/*` | Emergency fixes for production |

### Workflow

#### Starting a New Feature

```bash
git checkout develop
git pull origin develop
git checkout -b feature/my-feature
# ... make changes ...
git push -u origin feature/my-feature
# Create PR to develop
```

#### Creating a Release

```bash
git checkout develop
git pull origin develop
git checkout -b release/v1.1.0

# Update CHANGELOG.md:
# - Move [Unreleased] items to new version section
# - Add release date
# - Update comparison links at bottom

git commit -am "Prepare release v1.1.0"
git push -u origin release/v1.1.0
# Create PR to main
```

After PR is merged to main:

```bash
git checkout main
git pull origin main
git tag -a v1.1.0 -m "v1.1.0 - Release description"
git push origin v1.1.0

# Merge back to develop
git checkout develop
git merge main
git push origin develop
```

#### Hotfix Process

```bash
git checkout main
git pull origin main
git checkout -b hotfix/v1.0.1

# Fix the issue
# Update CHANGELOG.md

git commit -am "Fix critical issue"
git push -u origin hotfix/v1.0.1
# Create PR to main
```

After PR is merged:

```bash
git checkout main
git pull origin main
git tag -a v1.0.1 -m "v1.0.1 - Hotfix description"
git push origin v1.0.1

# Merge to develop
git checkout develop
git merge main
git push origin develop
```

## Versioning

We use [Semantic Versioning](https://semver.org/):

- **MAJOR** (x.0.0): Breaking changes to module interface
- **MINOR** (0.x.0): New features, backward compatible
- **PATCH** (0.0.x): Bug fixes, backward compatible

### What Constitutes a Breaking Change?

- Removing or renaming variables
- Changing variable types
- Removing outputs
- Changing default behavior in incompatible ways
- Minimum provider version increases

## Pull Request Guidelines

1. Create feature branches from `develop`
2. Keep changes focused and atomic
3. Update CHANGELOG.md under `[Unreleased]`
4. Ensure `terraform fmt` passes
5. Ensure `terraform validate` passes
6. Update README.md if adding/changing variables or outputs

## Testing

Before submitting a PR:

```bash
terraform fmt -check -recursive
terraform init
terraform validate
```
