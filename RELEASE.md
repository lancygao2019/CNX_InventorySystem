# Release and Versioning Guide

This project uses Semantic Versioning with the format `MAJOR.MINOR.PATCH` (example: `1.1.55`).

The current version is stored in the root `VERSION` file.

## Version Rules

- `PATCH` (`1.1.55` -> `1.1.56`)
  - Bug fixes
  - UI tweaks
  - Small behavior adjustments with no breaking changes
- `MINOR` (`1.1.55` -> `1.2.0`)
  - New features
  - New endpoints/pages/capabilities that are backward compatible
- `MAJOR` (`1.1.55` -> `2.0.0`)
  - Breaking changes
  - Incompatible data/API/behavior changes

## Branch and Commit Conventions

- Main branch: `ims-app`
- Feature branch naming:
  - `feature/<short-name>`
  - `fix/<short-name>`
  - `chore/<short-name>`
- Commit message style:
  - `feat: ...`
  - `fix: ...`
  - `refactor: ...`
  - `docs: ...`
  - `test: ...`

Examples:
- `feat: add inventory pagination controls`
- `fix: sort inventory list by barcode desc`
- `docs: add release workflow guide`

## Standard Release Flow

1. Sync latest code and create/update your working branch.
2. Complete changes and verify tests:
   - `python3 -m pytest tests/ -v`
3. Update `VERSION` based on rules above.
4. Commit changes (include `VERSION` update).
5. Merge into `ims-app`.
6. Create a Git tag for the release:
   - `git tag -a v$(cat VERSION) -m "Release v$(cat VERSION)"`
7. Push branch and tags:
   - `git push origin ims-app --tags`
8. Build and validate distributables:
   - macOS: `./scripts/build_exe.sh`
   - Windows: `scripts\build_exe.bat`

## Pre-Release Checklist

- App starts from source: `./scripts/start.sh` or `python app.py`
- Dev mode sanity: `./scripts/start-dev.sh`
- Tests pass: `python3 -m pytest tests/ -v`
- Login works (`admin/admin` or updated credentials)
- Device CRUD + barcode scan path sanity checked
- Import/export sanity checked (CSV/XLSX)
- Backup create/restore sanity checked
- `VERSION` is updated correctly

## Hotfix Flow

For urgent production fixes:

1. Branch from latest `ims-app`: `fix/hotfix-<short-name>`
2. Implement minimal fix and run targeted tests first, then full tests.
3. Bump `PATCH` only (for hotfix releases).
4. Merge to `ims-app`, tag, and publish.

## Rollback Guidance

If a release is bad:

1. Identify the last known good tag (example: `v1.1.54`).
2. Rebuild and redeploy from that tag.
3. Open a hotfix branch for corrective changes.
4. Publish a new `PATCH` version (do not reuse an existing tag/version).

## Notes for This Repository

- CI may auto-bump versions in some workflows.
- Always verify the final `VERSION` value before tagging.
- Keep release notes focused on:
  - User-visible changes
  - Bug fixes
  - Upgrade/rollback notes
