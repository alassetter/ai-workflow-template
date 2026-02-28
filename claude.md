# Repository Claude Instructions Template

> This file governs how Claude operates in this project. Read it fully before doing any work.

This repository operates under a strict workflow operating system located in `workflow/`.

Governance is mandatory.

Authoritative feature governance policy:
`workflow/decisions/governance/FEATURE_GOVERNANCE_CONTRACT.md`

---

## Workflow Governance (FXXX)

All non-trivial work must be tracked as an **FXXX Feature**.

Lifecycle:

BACKLOG -> ACTIVE -> COMPLETE

Folder mapping:

- BACKLOG -> `workflow/planning/backlog/`
- ACTIVE -> `workflow/planning/active/`
- COMPLETE -> `workflow/planning/archive/`

### Single Active Feature Rule

There may be **exactly ONE ACTIVE feature** at a time.

Before doing any work:

1. Check `workflow/planning/active/`
2. If there are **0** files -> ask the user which BACKLOG feature to activate
3. If there are **2+** files -> stop and ask the user to resolve (single-flight violation)
4. If there is **1** file -> read it fully and follow it

Execution is not allowed unless it is tied to the single ACTIVE feature.

### Golden Conversations

Golden conversations preserve institutional insight and must be stored in:

`workflow/decisions/golden/`

Create a Golden Conversation when a session produces:

- Governance shifts
- Architectural philosophy changes
- Major strategic direction
- AI collaboration rules modifications

Golden Conversations are curated, not raw transcripts.

Use: `workflow/templates/GOLDEN_CONVERSATION.md`

---

## Session Protocol

### Starting a New Session

1. Check `workflow/planning/active/` and confirm the single ACTIVE feature (or ask which BACKLOG item to activate).
2. Check `workflow/journal/` and locate the most recent checkpoint by date.
3. Confirm current phase and completed checklist items.
4. Do not start implementation until the user confirms where to resume.

### Checkpoints

- Before ending any session or when requested, create a checkpoint file.
- Location: `workflow/journal/`
- Naming: `YYYY-MM-DD-short-description.md`
- Template: `workflow/templates/CHECKPOINT.md`
- Content: summary, changes made, decisions, feature progress, open questions, next steps.
- Checkpoints are cumulative and should be self-contained enough for resumption.

### Pace of Work

- Do not skip ahead. Follow the ACTIVE feature implementation plan.
- Each significant step should be reviewed before the next major step.
- When in doubt, ask.
- Prefer small, verifiable increments.
- If a feature exceeds ~5-7 major steps, propose splitting into multiple FXXX features.

---

## Architecture-First Rule

ADR-before-implementation is mandatory.

If implementation introduces or changes architecture:

1. Create or update an ADR first.
2. Resolve ADR review status.
3. Proceed with implementation only after ADR alignment.

ADR artifacts live in:

`workflow/decisions/adr/`

Use: `workflow/templates/ADR.md`

### Supersession Traceability

If an artifact is replaced:

- Mark prior artifact as superseded.
- Add forward link (`Superseded by`) and backward link (`Supersedes`) where applicable.
- Preserve historical artifacts; do not silently rewrite intent.

---

## Phase Discipline

Only one phase may be active at a time, as defined in:

- `workflow/ROADMAP.md`
- `workflow/phases/`

Rules:

- Work must align to the active phase.
- Future-phase work is out of scope unless explicitly approved.
- If cross-phase dependency appears, pause and resolve via ADR or roadmap update.

Use: `workflow/templates/PHASE.md`

---

## Feature Governance

Every feature should have:

- Explicit Feature ID (`FXXX`)
- Explicit phase (`PHASE-X`)
- Scope and explicit non-scope
- Related ADRs (`ADR-XXX` or `None (justification)`)
- Acceptance criteria and completion gates

Use: `workflow/templates/FEATURE.md`

Feature completion requires at minimum:

- Implementation plan checklist completed
- Deliverables present and reviewable
- CI checks green (where applicable)
- Related ADR requirements satisfied
- Drift review confirms non-scope remained unchanged
- `Completed:` date populated
- Feature moved to `workflow/planning/archive/`

For normative lifecycle and enforcement rules, follow:
`workflow/decisions/governance/FEATURE_GOVERNANCE_CONTRACT.md`

---

## Deterministic CI and PR Requirements

All PRs must include:

- `Phase:`
- `Feature:`
- Related ADR references
- Scope statement
- Explicit non-scope statement

CI must be deterministic and fail on missing required checks.

---

## Repository Workflow Structure

Authoritative structure is under `workflow/`:

workflow/
|- AI_OPERATING_MODEL.md
|- ROADMAP.md
|- phases/
|- planning/
|  |- active/
|  |- backlog/
|  |- archive/
|  `- superseded/
|- decisions/
|  |- adr/
|  |- governance/
|  `- golden/
|- journal/
|- milestones/
`- templates/
   |- ADR.md
   |- FEATURE.md
   |- PHASE.md
   |- GOLDEN_CONVERSATION.md
   `- CHECKPOINT.md

---

## Operating Constraints for Claude

- Stay within the active feature scope unless user explicitly changes scope.
- Do not modify accepted ADR semantics.
- Do not proceed when governance invariants are broken (for example, multiple active features).
- Prefer explicit, auditable changes over implicit behavior.
- Treat workflow documents as source of truth.

---

## Optional Project-Specific Section

Use this section only if the repository defines concrete architecture/package conventions.

- Package boundaries:
- Dependency direction:
- Naming conventions:
- Testing standards:
- Build order:
