# Agent Commit Guide

Quick reference for how Jarvis commits code.

## When to Commit

- After completing a logical unit of work
- Before merging to main
- When tests pass

## How to Commit

### Single change:
```bash
git add <files>
git commit -m "type(scope): description"
```

### Interactive staging:
```bash
git add -p  # review hunks interactively
git commit
```

## Commit Types

| Type | Use for |
|------|---------|
| `feat` | New functionality |
| `fix` | Bug fixes |
| `docs` | README, comments, docs |
| `style` | Formatting only |
| `refactor` | Restructuring code |
| `test` | Adding tests |
| `chore` | Deps, build, CI |

## Tips

- Write imperative mood ("add" not "added")
- Keep subject line under 50 chars
- Body wrapped at 72 chars
- Reference issues: `Closes #123`

## Example Workflow

```bash
# Make changes to files
git status
git add -A
git commit -m "feat(auth): implement login flow

- Add user model
- Create login endpoint
- Add session handling

Closes #45"
git push
```

---

# Release Process

This project uses **semantic-release** with GitHub Actions for automated releases.

## How Releases Work

1. **Push to `main`** — Triggers a full release (production)
2. **Push to prerelease branches** — Any branch that's not main creates prereleases
3. **Semantic-release** analyzes commits since last release to determine version bump
4. **Ansible role** is packaged and pushed to GHCR as a container image

## Branch Strategy

| Branch | Release Type |
|--------|--------------|
| `main` | Production release |
| `!main` | Prerelease (e.g., `pre-beta`) |

## Version Bumping

Semantic-release automatically determines the version bump based on commit messages:

| Commit Message | Version Bump |
|----------------|--------------|
| `fix:` | Patch (`1.0.0` → `1.0.1`) |
| `feat:` | Minor (`1.0.0` → `1.1.0`) |
| `feat!:`, `fix!:`, etc. | Major (`1.0.0` → `2.0.0`) |

## Triggering a Release

```bash
# For production release (main branch)
git checkout main
git merge your-feature-branch
git push origin main

# For prerelease (beta branch)
git checkout beta
git merge your-feature-branch
git push origin beta
```

## Release Outputs

- **GitHub Release** — Created automatically (title is version only, e.g., `v1.2.0`)
- **Ansible Role** — Available on GitHub Releases

## Important Notes

- **Don't specify versions** in commit messages — semantic-release determines the version
- All conventional commits are collected since the last release
- GitHub release title is just the version number (e.g., `v1.2.0`), no description
- Role can be installed via `ansible-galaxy install <owner>.<repo>`
