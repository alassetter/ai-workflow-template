# Git Workflow

## Purpose

This repository follows an architecture-first, phase-driven workflow.

Git is used to enforce:

* ADR-before-implementation discipline
* Phase sequencing
* Feature isolation
* Supersession clarity
* Deterministic change history

This workflow supports — and does not override — the rules defined in:

* `workflow/AI_OPERATING_MODEL.md`
* `workflow/ROADMAP.md`
* `workflow/phases/`

---

# Branching Strategy

## Protected Branch

### `main`

* Always deployable
* Must pass CI
* No direct commits allowed
* Changes merged via Pull Request only

---

## Branch Types

### Feature Branches

Format:

```
feature/FXXX-short-description
```

Rules:

* One feature per branch
* Must reference Feature ID
* Must reference Phase
* May not include unrelated changes

Example:

```
feature/F002-v2-token-build-pipeline
```

---

### ADR Branches

Format:

```
adr/XXX-short-title
```

Rules:

* Used when introducing or superseding an ADR
* Must not contain implementation changes
* Must merge before dependent feature branches

Example:

```
adr/017-build-cache-strategy
```

---

### Chore / Refactor Branches

Format:

```
chore/description
refactor/description
```

Rules:

* No architectural change
* No feature scope expansion
* Must not modify ADR intent

---

# Pull Request Rules

All changes require a Pull Request into `main`.

Each PR must include:

* Phase
* Feature ID (if applicable)
* Related ADR(s)
* Scope statement
* Explicit non-scope confirmation

Example PR description:

```
Phase: PHASE-1
Feature: F002
Related ADRs: ADR-003, ADR-015

Scope:
Implements token pipeline outputs.

Non-scope (explicit):
No changes to @axr/theme.
No component work.
No documentation updates.
```

---

# ADR Sequencing Rule

If a feature requires new architecture:

1. Create ADR branch.
2. Merge ADR.
3. Create feature branch.
4. Implement feature.

Implementation must never precede architectural decision.

---

# Phase Discipline

Only one phase may be active at a time.

Rules:

* No feature from a future phase may merge while a prior phase is incomplete.
* `workflow/ROADMAP.md` is authoritative.
* Feature PRs must align with active phase.

If a cross-phase dependency is discovered:

* Pause feature.
* Re-evaluate via ADR or roadmap update.

---

# Supersession Discipline

If a feature or ADR becomes obsolete:

* Move it to `workflow/planning/superseded/`
* Update `Supersedes` / `Superseded by` fields
* Do not modify historical artifacts
* Reference supersession in PR description

Example:

```
Supersedes: F002
```

History must remain traceable.

---

# Merge Strategy

* Squash and merge (recommended)
* Clean, atomic commits
* Commit message format:

```
[FXXX] Short description

Phase: X
Related ADRs: ADR-XXX | None (justification)
```

Example:

```
[F002] Implement token pipeline

Phase: PHASE-1
Related ADRs: ADR-003, ADR-015
```

---

# Completion Gate

A feature is complete when:

1. Acceptance Criteria satisfied
2. Related ADR constraints validated
3. No scope expansion occurred
4. Checkpoint logged from `workflow/templates/CHECKPOINT.md`
5. `Completed:` date filled in the feature file
6. Feature moved to `workflow/planning/archive/`
7. Milestone logged in `workflow/milestones/`

Only then may the next feature move to `workflow/planning/active/`.

---

# CI Expectations

CI must enforce:

* Linting
* Type checks (if applicable)
* Build integrity
* No direct pushes to `main`

Future enhancements (optional):

* Phase gate validation
* PR template enforcement
* ADR reference validation

---

# Long-Term Integrity Principles

* Architecture is versioned via ADRs.
* Features are versioned via branch history.
* Superseded artifacts remain preserved.
* No silent rewrites of history.

Git exists to reinforce architectural clarity — not bypass it.

The repository documents are the source of truth.
