# Git Workflow

- Never commit directly to `main`. Create a branch for every change -- feature, fix, or chore -- open a PR, and merge only after CI passes.
- Branch naming: `type/short-kebab-description`.
  - `feat/` -- new feature
  - `fix/` -- bug fix
  - `hotfix/` -- urgent production fix
  - `refactor/` -- restructuring without behavior change
  - `chore/` -- maintenance, dependencies, config
  - `docs/` -- documentation only
  - `test/` -- tests only
  - `perf/` -- performance improvement
- `main` is protected: no direct pushes. PRs require the CI workflow (`.github/workflows/ci.yml`: rspec, rubocop, brakeman, importmap audit) to pass before merge.
- New Brakeman findings must be fixed, not silenced. Only add an entry to `.brakeman.ignore` for a finding that's been reviewed and is a confirmed false positive or an accepted risk -- always with a `note` explaining why.
- Deploys still run off `main` via `bin/kamal deploy`. Merging to `main` is what makes a change deployable, not what deploys it -- deploying stays a separate, explicit step.
