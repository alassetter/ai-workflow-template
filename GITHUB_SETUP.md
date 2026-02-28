# GitHub Setup Guide

Use this guide to configure `.github/` for governance enforcement in a new repository.

## 1. CODEOWNERS

File: `.github/CODEOWNERS`

Replace placeholders with real owners:

- `* @repo-owner`
- `/workflow/ @architecture-owners`
- `/.github/ @platform-owners`

Use valid GitHub users or teams (for example `@org/team-name`).

## 2. Pull Request Template

File: `.github/PULL_REQUEST_TEMPLATE.md`

Required keys that must remain:

- `Phase:`
- `Feature:`

Required sections to keep:

- Related ADRs
- Scope
- Non-Scope
- Acceptance Criteria
- Drift Review
- Supersession Traceability
- Completion Gate

## 3. Issue Templates

Directory: `.github/ISSUE_TEMPLATE/`

### `feature.yml`

- Required fields:
  - Phase
  - Feature ID
  - Scope
  - Explicit Non-Scope
- Label: `feature`

### `adr.yml`

- Required fields:
  - Context
  - Decision
  - Consequences
- Label: `adr`

### `bug.yml`

- Required fields:
  - Steps to Reproduce
  - Expected vs Actual
- Label: `bug`

### `chore.yml`

- Required fields:
  - Scope
  - Architectural impact confirmation
- Label: `chore`

## 4. CI Workflow

File: `.github/workflows/ci.yml`

Keep:

- Trigger on pull requests to `main`
- Node 20 setup
- Dependency install
- Lint if present
- Typecheck if present
- Build if present
- Fail on error

Adjust package manager commands only if stack requires it (npm/pnpm/yarn).

## 5. Phase Guard Workflow

File: `.github/workflows/phase-guard.yml`

Keep:

- Pull request trigger
- PR body checks for:
  - `Phase:`
  - `Feature:`
- Fail when either key is missing

## 6. Workflow Notes

File: `.github/workflows/README.md`

Update this file whenever:

- Required PR fields change
- CI steps change
- Governance enforcement behavior changes

## 7. Validation Checklist

- CODEOWNERS has real owners
- PR template keys match phase guard checks
- Issue template required fields and labels are correct
- CI matches repository tooling
- Workflow notes are updated

## 8. Useful Prompts

"Validate `.github` consistency: CODEOWNERS, PR template keys, phase-guard checks, issue template required fields, and CI assumptions."

"Update `.github/CODEOWNERS` with these users/teams: [list], preserving separate ownership for `workflow/` and `/.github/`."

"Adapt `.github/workflows/ci.yml` for [npm/pnpm/yarn] while preserving deterministic failure and optional lint/typecheck/build behavior."
