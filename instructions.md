# Template Setup and Usage Instructions

This guide is written for a human setting up this template in a new repository.

Visual map: [WORKFLOW_DIAGRAM.md](./WORKFLOW_DIAGRAM.md)

## 0. Choose Adoption Path

### Path A - New Repository from Template

1. Create a new repo from this template (or clone/fork this repo).
2. Add your project code into the repo.
3. Keep workflow/governance files in place and continue with setup steps below.

### Path B - Existing Repository Integration

Copy these into your existing project root:

- `workflow/`
- `.github/`
- `claude.md`
- `instructions.md`
- `WORKFLOW_DIAGRAM.md`
- `GITHUB_SETUP.md`

Then:

1. Commit this baseline.
2. Continue with setup steps below.

## 1. Human-First Setup Order (Do This in Sequence)

1. Setup `claude.md` (AI operating contract)
2. Setup `.github/` governance and CI details
3. Add project context (`workflow/PRODUCT.md`, `workflow/ROADMAP.md`)
4. Set phase statuses (`workflow/phases/PHASE-*.md`)
5. Draft initial ADRs/PDRs needed for direction
6. Create first feature (`F001`) in backlog
7. Activate exactly one feature
8. Start execution and log checkpoints

## 2. Step-by-Step Setup

### Step A - Setup `claude.md` First

Update:

- Project name/title
- Optional project-specific section (boundaries, dependency direction, naming, testing, build order)
- Domain/compliance constraints
- Explicit non-scope guardrails

Prompt:

"Review `claude.md` and customize it for a [project type] repository. Keep governance rules intact, and only update project-specific constraints."

### Step B - Setup `.github` Governance

Reference: [GITHUB_SETUP.md](./GITHUB_SETUP.md)

Update and verify:

- `.github/CODEOWNERS` (real owners/teams)
- `.github/PULL_REQUEST_TEMPLATE.md` (required fields remain `Phase:` and `Feature:`)
- `.github/ISSUE_TEMPLATE/*.yml` (labels and required fields)
- `.github/workflows/ci.yml` (stack/tooling assumptions)
- `.github/workflows/phase-guard.yml` (required PR field enforcement)

Prompt:

"Audit `.github` templates and workflows for this repository stack and update only owner/tooling details while preserving governance checks."

#### `.github` file-by-file setup checklist

1. `.github/CODEOWNERS`
- Replace placeholder owners:
  - `* @repo-owner`
  - `/workflow/ @architecture-owners`
  - `/.github/ @platform-owners`
- Use real GitHub handles or teams (for example `@org/team-name`).

2. `.github/PULL_REQUEST_TEMPLATE.md`
- Keep required keys exactly:
  - `Phase:`
  - `Feature:`
- Keep sections for:
  - Related ADRs
  - Scope
  - Non-Scope
  - Acceptance Criteria
  - Drift Review
  - Supersession Traceability
  - Completion Gate

3. `.github/ISSUE_TEMPLATE/feature.yml`
- Confirm required fields:
  - Phase
  - Feature ID
  - Scope
  - Explicit Non-Scope
- Confirm label is `feature`.

4. `.github/ISSUE_TEMPLATE/adr.yml`
- Confirm required fields:
  - Context
  - Decision
  - Consequences
- Confirm label is `adr`.

5. `.github/ISSUE_TEMPLATE/bug.yml`
- Confirm required fields:
  - Steps to Reproduce
  - Expected vs Actual
- Confirm label is `bug`.

6. `.github/ISSUE_TEMPLATE/chore.yml`
- Confirm required fields:
  - Scope
  - Architectural impact confirmation
- Confirm label is `chore`.

7. `.github/workflows/ci.yml`
- Keep trigger:
  - Pull requests to `main`
- Verify Node setup:
  - Node `20`
- Verify steps:
  - Install dependencies
  - Lint if present
  - Typecheck if present
  - Build if present
- Adjust package manager commands only if your stack is not npm.

8. `.github/workflows/phase-guard.yml`
- Keep pull request trigger.
- Keep required PR body checks:
  - `Phase:`
  - `Feature:`
- Keep failure on missing required fields.

9. `.github/workflows/README.md`
- Update notes if you change policy or required PR fields.

#### `.github` validation prompts

"Validate `.github` for consistency: PR template keys, phase guard checks, issue template required fields, CODEOWNERS placeholders, and CI assumptions. Return exact mismatches."

"Update `.github/CODEOWNERS` with these owners: [list], preserving separate rules for `workflow/` and `/.github/`."

"Adapt `.github/workflows/ci.yml` for [npm/pnpm/yarn], keeping deterministic failure behavior and optional lint/typecheck/build execution."

### Step C - Add Project Context

Update:

- `workflow/PRODUCT.md` (vision, outcomes, non-goals, metrics)
- `workflow/ROADMAP.md` (priorities and sequencing)

Prompt:

"Draft `workflow/PRODUCT.md` and update `workflow/ROADMAP.md` for a new [project/domain], with clear outcomes and measurable success criteria."

### Step D - Initialize Phases

Update front matter in:

- `workflow/phases/PHASE-0.md`
- `workflow/phases/PHASE-1.md`
- `workflow/phases/PHASE-2.md`
- `workflow/phases/PHASE-3.md`

Rules:

- Exactly one phase is `ACTIVE`
- Remaining phases are `BACKLOG`

Prompt:

"Set phase front matter for `workflow/phases/PHASE-*.md`, keep exactly one ACTIVE phase, and provide rationale."

### Step E - Plan ADRs and PDRs

Use templates:

- ADR template: `workflow/templates/ADR.md`
- PDR template: `workflow/templates/PDR.md`

Create drafts in:

- `workflow/decisions/adr/`
- `workflow/pdr/`

Prompts:

"Create `ADR-001` for the first architecture decision required by the roadmap."

"Create `PDR-001` for the first product-direction decision required before feature execution."

"Review current ADR drafts and extract product-level decisions that should become PDRs. Propose `PDR-XXX` candidates with rationale."

### Step F - Create and Activate First Feature

Create first feature from template:

- Source: `workflow/templates/FEATURE.md`
- Target: `workflow/planning/backlog/F001-[slug].md`

Then activate:

- Move to `workflow/planning/active/`
- Ensure it is the only active file

Prompt:

"Create `F001` from feature template, then activate it and verify single-flight compliance."

### Step G - Start Execution and Log Checkpoints

Before ending each working session:

- Create a checkpoint in `workflow/journal/` using `workflow/templates/CHECKPOINT.md`

Prompt:

"Create `workflow/journal/YYYY-MM-DD-[slug].md` checkpoint with summary, decisions, progress, open questions, and next steps."

## 3. Setup Draft Workspace (Optional)

Use drafts in `workflow/setup/` if you prefer staged editing before final placement:

- `workflow/setup/SETUP_PHASES.md`
- `workflow/setup/SETUP_PDR_001.md`
- `workflow/setup/SETUP_FEATURE_F001.md`
- `workflow/setup/SETUP_ADR_001.md`
- `workflow/setup/SETUP_CHECKPOINT.md`

## 4. Daily Execution Loop

1. Confirm exactly one file exists in `workflow/planning/active/`.
2. Read the active feature, related PDRs, and related ADRs.
3. Execute scoped work only.
4. Update checkpoint in `workflow/journal/`.
5. If complete, set `Completed:` date and move feature to `workflow/planning/archive/`.
6. Activate next feature from backlog.

## 5. Required Updates for New Projects

- `.github/CODEOWNERS` owners/teams
- `claude.md` project-specific constraints
- `workflow/PRODUCT.md` product baseline
- `workflow/ROADMAP.md` priorities and milestones
- `workflow/phases/PHASE-*.md` front matter values
- Initial ADRs in `workflow/decisions/adr/`
- Initial PDRs in `workflow/pdr/`
- CI assumptions if not using Node/npm scripts

## 6. Governance Rules You Must Preserve

- ADR-before-implementation for architecture changes
- PDR before major product-direction changes
- Single active feature rule
- Explicit scope and non-scope for features
- Supersession traceability (`Supersedes` / `Superseded by`)
- Deterministic PR checks (`Phase:` and `Feature:`)

Authoritative policy:
`workflow/decisions/governance/FEATURE_GOVERNANCE_CONTRACT.md`

## 7. Quick Validation Prompts

"Audit repository governance drift against `FEATURE_GOVERNANCE_CONTRACT.md` and list violations by severity."

"Validate `claude.md`, `.github` templates, phase guard workflow, feature template, ADR/PDR templates, and active feature for field consistency."

"Given active feature + related PDRs + related ADRs, propose the smallest safe next step and explicit non-scope guardrails."

See also: [WORKFLOW_DIAGRAM.md](./WORKFLOW_DIAGRAM.md)
