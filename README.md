# Forked GLPI dependencies

This folder is also published as the **gamut-deps** repo on GitHub: **https://github.com/randyyates/gamut-deps**

These directories are clones of GLPI project packages, used locally so we can maintain our own forks and avoid depending on upstream for builds.

| Directory | Upstream | Purpose |
|-----------|----------|---------|
| **inventory_format** | [glpi-project/inventory_format](https://github.com/glpi-project/inventory_format) | Inventory JSON schema and validation (PHP). Used by `gamut` via Composer path repo. |
| **phpstan-glpi** | [glpi-project/phpstan-glpi](https://github.com/glpi-project/phpstan-glpi) | PHPStan rules for GLPI. Used by `gamut` via Composer path repo. |
| **illustrations** | [glpi-project/illustrations](https://github.com/glpi-project/illustrations) | SVG illustrations. Used by `gamut` via npm `file:../deps/illustrations`. |

## Current state

- **inventory_format** is checked out at tag `1.2.3` (detached HEAD).
- **phpstan-glpi** is checked out at tag `1.1.1` (detached HEAD).
- **illustrations** is at default branch (no version tag; npm uses the local folder).

## Using your own forks

1. Fork each repo on GitHub (e.g. under your user or `gamutit` org).
2. In each directory, add your fork as a remote and push:
   ```bash
   cd deps/inventory_format
   git remote add myfork https://github.com/YOUR_USER/inventory_format.git
   git push myfork 1.2.3
   # Optional: create a branch for your changes
   git checkout -b gamut
   git push myfork gamut
   ```
3. To pull upstream changes later: `git fetch origin` then merge or rebase as needed.

## Wiring in the main app

- **gamut/composer.json** has `repositories` with `path` entries for `../deps/inventory_format` and `../deps/phpstan-glpi`. Composer installs from these paths when you run `composer install` from `gamut/`.
- **gamut/package.json** has `"@glpi-project/illustrations": "file:../deps/illustrations"`. Run `npm install` from `gamut/` to link the local package.

Running `composer install` or `npm install` from `gamut/` will use these local deps; no need to publish to Packagist or npm.

## Pushing to GitHub

This directory is a git repo with `origin` → `https://github.com/randyyates/gamut-deps.git`. To push (e.g. after adding the deps or updating the README):

```bash
cd deps
git add -A
git status   # then commit if needed
git push -u origin main
```

Use your usual GitHub auth (SSH key, token, or gh CLI).
