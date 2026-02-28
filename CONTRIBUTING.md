# Contributing Guide

## Workflow First

All non-trivial work must follow `workflow/` governance.

Before coding:

1. Confirm exactly one active feature in `workflow/planning/active/`.
2. Confirm phase alignment in `workflow/phases/` and `workflow/ROADMAP.md`.
3. Confirm ADR requirements (`workflow/decisions/adr/`) for architectural changes.

## Pull Requests

Use `.github/PULL_REQUEST_TEMPLATE.md` and include:

- `Phase:`
- `Feature:`
- Related ADRs
- Scope and explicit non-scope

PRs are validated by CI and phase guard workflows.

## Required Practices

- Keep changes within active feature scope.
- Keep non-scope untouched.
- Document supersession explicitly.
- Add/update checkpoint in `workflow/journal/` for session continuity.

## Governance References

- `workflow/decisions/governance/FEATURE_GOVERNANCE_CONTRACT.md`
- `workflow/AI_OPERATING_MODEL.md`
- `workflow/GIT_WORKFLOW.md`
