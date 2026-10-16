# AGENTS.md

devservices config for the shared Redis container in Sentry developer environments. [README.md](README.md) covers how other repos use it.

## Check

- Run `pip install -r requirements-dev.txt`, then `devservices up`, `devservices status`, and `devservices down`.
- CI (`.github/workflows/ci.yml`) runs `getsentry/action-validate-devservices-config` when `devservices/**`, `.github/workflows/ci.yml`, or `requirements-dev.txt` change.

## Invariants

- Consumers reference `repo_name: sentry-shared-redis` on `branch: main` and start its `default` mode. Renaming the repo or branch, or removing `redis` from `default`, breaks them.
