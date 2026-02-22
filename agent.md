# AGENT.md - Implementing Fixes & Features

This guide explains how to implement and contribute fixes/features to ansible-role-app.

## Workflow Overview

1. Create a feature/fix branch from `main`
2. Make changes
3. Test locally with molecule
4. Push and open PR
5. CI runs molecule tests + lint
6. Merge to main

## Branches

- `main` - Stable branch, only merge via PR
- `fix/*` - Fix branches
- `feature/*` - Feature branches

## Making Changes

### 1. Create a Branch

```bash
git checkout main
git pull origin main
git checkout -b fix/your-fix-name
```

### 2. Run Tests Locally

```bash
# Install dependencies
pip install molecule molecule-docker ansible-core==2.16.0

# Run molecule test
molecule test

# Or just converge (faster for dev)
molecule converge
```

### 3. Add Tests for New Platforms

Edit `.github/workflows/molecule.yml` to add distros:

```yaml
matrix:
  include:
    - distro: ubuntu2204
      image: geerlingguy/docker-ubuntu2204-ansible:latest
    - distro: alma9
      image: docker.io/robinwalterfit/docker-almalinux9-ansible:latest
```

Also update `molecule/default/molecule.yml` comments to document supported platforms.

### 4. Update Tasks

Edit `tasks/main.yml` for role tasks.

### 5. Commit & Push

```bash
git add .
git commit -m "fix: description of change"
git push origin fix/your-fix-name
```

### 6. Open Pull Request

- Create PR on GitHub targeting `main`
- CI will run: lint → molecule converge → molecule destroy
- Review and merge

## Release Process

1. Merge to main
2. Create git tag:
   ```bash
   git tag v1.0.1
   git push origin v1.0.1
   ```
3. Release workflow runs automatically on tag push

## Common Issues

### Molecule "return code 2"
- Check ANSIBLE_ROLES_PATH in molecule.yml
- Ensure role name matches namespace in meta/main.yml
- Use dynamic role name in converge.yml

### Test Failures
- Run `molecule converge` locally to debug
- Check HOME and XDG_CONFIG_HOME env vars
- Ensure Docker is running
