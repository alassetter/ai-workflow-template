# Workflow Automation Notes

## Included Workflows

- `ci.yml`: Runs on pull requests to `main`, sets up Node 20, installs dependencies, and runs lint/typecheck/build when available.
- `phase-guard.yml`: Runs on pull requests and fails when required PR fields are missing (`Phase:` and `Feature:`).

## Maintenance

When updating governance rules, keep these files aligned:

- `.github/PULL_REQUEST_TEMPLATE.md`
- `.github/workflows/phase-guard.yml`
- `workflow/decisions/governance/FEATURE_GOVERNANCE_CONTRACT.md`
