---
name: init-takt-devcontainer
description: >-
  Initialize a minimal standalone devcontainer with TakT tooling
  (gh-aw, gh-insitu, gh-tt) for issues-and-docs repositories.
---

# Init TakT Devcontainer

Use this skill when a repository needs a standalone devcontainer with minimal
dependencies and TakT-compatible GitHub CLI tooling.

## Use when

- The repository is primarily issues/discussions/docs
- The repo should run standalone and not depend on another workspace's devcontainer
- TakT command support is needed via GitHub CLI extensions

## Files created or updated

- `.devcontainer/devcontainer.json`
- `.insitu.yml`
- `.gitignore` (append if it already exists)
- `.gitconfig`
- `.githooks/pre-commit`

## Implementation steps

1. Create `.devcontainer/devcontainer.json` using `templates/devcontainer.minimal.json`.
2. Create `.insitu.yml` using `templates/insitu.yml`.
3. Ensure `.insitu.yml` includes:
   - `post-create` wave for setup actions
   - `trunk-worthy` wave with `cspell`, `markdownlint-cli2`, and
     `prettier --check .`
   - `repo-gitconfig` inventory step to include `../.gitconfig` in local
     git config
   - lint tool verification checks (`command -v ...`) in post-create
4. Ensure the `post-create` wave installs these extensions if missing:
   - `github/gh-aw`
   - `devx-cafe/gh-insitu`
   - `devx-cafe/gh-tt`
5. Ensure `.githooks/pre-commit` runs at least
   `gh insitu run trunk-worthy`.
6. Set `postCreateCommand` to
   `gh ext install devx-cafe/gh-insitu && gh insitu run post-create`.
7. Validate setup:
   - `python3 -m json.tool .devcontainer/devcontainer.json`
   - `gh insitu run post-create`
   - `gh insitu run trunk-worthy`

## Notes

- Keep runtime minimal; avoid app-framework dependencies unless explicitly needed.
- Prefer markdown/doc quality tooling over build stacks for docs-first repos.
- Install lint tools through devcontainer features and verify them in insitu.
