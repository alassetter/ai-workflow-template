# Template Setup and Usage Instructions

This guide walks you through setting up and running this workflow template in a new project.

Visual map: [WORKFLOW_DIAGRAM.md](./WORKFLOW_DIAGRAM.md)

## 1. Setup Goal

Initialize governance, define the first executable feature, and begin work in single-flight mode.

You will produce:

- One ACTIVE phase
- One first feature (`F001`)
- One first ADR (`ADR-001`) if architecture is involved
- One initial checkpoint in `workflow/journal/`

## 2. Setup Draft Workspace

Use setup drafts in `workflow/setup/`:

- `workflow/setup/SETUP_PHASES.md`
- `workflow/setup/SETUP_FEATURE_F001.md`
- `workflow/setup/SETUP_ADR_001.md`
- `workflow/setup/SETUP_CHECKPOINT.md`

Finalize outputs into authoritative folders:

- Phases -> `workflow/phases/`
- Feature -> `workflow/planning/backlog/` then `workflow/planning/active/`
- ADR -> `workflow/decisions/adr/`
- Checkpoint -> `workflow/journal/`

## 3. Prompt-Driven Setup (Recommended)

Use these prompts in order.

### Prompt A - Initialize Phases

"Review `workflow/phases/PHASE-*.md` and set front matter for a new [project type] repository. Keep exactly one phase ACTIVE and the rest BACKLOG. Return a short rationale for the active phase."

Expected result:

- Updated phase front matter with `status`, `owner`, and dates.

### Prompt B - Draft First Feature

"Create `workflow/planning/backlog/F001-[slug].md` from `workflow/templates/FEATURE.md` for [first deliverable]. Include explicit scope and non-scope, and keep implementation to <= 5 major steps."

Expected result:

- New backlog feature ready for activation.

### Prompt C - Draft ADR (If Needed)

"Create `workflow/decisions/adr/ADR-001-[slug].md` from `workflow/templates/ADR.md` for the architecture decision needed by F001. Include alternatives and consequences."

Expected result:

- ADR draft linked from feature metadata.

### Prompt D - Activate and Validate Single-Flight

"Move `F001` into `workflow/planning/active/`, verify it is the only active feature, and summarize the first 3 execution steps."

Expected result:

- Single active feature with immediate execution plan.

### Prompt E - Log Setup Checkpoint

"Create a checkpoint in `workflow/journal/YYYY-MM-DD-setup-baseline.md` from `workflow/templates/CHECKPOINT.md` with setup summary, decisions, open questions, and next steps."

Expected result:

- Session continuity artifact for the next run.

## 4. Day-to-Day Execution Loop

1. Confirm exactly one file exists in `workflow/planning/active/`.
2. Read the active feature and related ADRs.
3. Execute scoped work only.
4. Update checkpoint in `workflow/journal/`.
5. If complete, set `Completed:` date and move feature to `workflow/planning/archive/`.
6. Activate next feature from backlog.

## 5. Required Updates for New Projects

- `.github/CODEOWNERS` owners/teams
- `workflow/phases/PHASE-*.md` front matter values
- `workflow/ROADMAP.md` priorities and success criteria
- `claude.md` optional project-specific constraints
- CI assumptions if not using Node/npm scripts

## 6. Governance Rules You Must Preserve

- ADR-before-implementation for architecture changes
- Single active feature rule
- Explicit scope and non-scope for features
- Supersession traceability (`Supersedes` / `Superseded by`)
- Deterministic PR checks (`Phase:` and `Feature:`)

Authoritative policy:
`workflow/decisions/governance/FEATURE_GOVERNANCE_CONTRACT.md`

## 7. Troubleshooting Prompts

"Audit this repository for workflow drift against `FEATURE_GOVERNANCE_CONTRACT.md` and list violations by severity."

"Validate that PR template, phase guard workflow, and feature template use consistent required fields."

"Given the active feature and related ADRs, propose the smallest next implementation step and explicit non-scope guardrails."

See also: [WORKFLOW_DIAGRAM.md](./WORKFLOW_DIAGRAM.md)
