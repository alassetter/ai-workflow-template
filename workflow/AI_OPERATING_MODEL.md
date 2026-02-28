# AI Operating Model

## Purpose

This repository uses AI assistance under structured workflow governance.

Authoritative feature lifecycle and enforcement policy:
`workflow/decisions/governance/FEATURE_GOVERNANCE_CONTRACT.md`

AI supports:

* Architectural validation
* Feature refinement
* Task breakdown
* Drift detection
* Review and constraint enforcement

AI does **not**:

* Author architecture without ADRs
* Modify accepted ADRs
* Expand scope beyond the active phase
* Skip defined workflow layers

---

## Execution Hierarchy

All work must follow this order:

1. Product Vision (`workflow/PRODUCT.md`)
2. Product Decision Record (PDR) when direction changes
3. ADR (Architecture Decision Record) when architecture changes
4. Phase Plan
5. Feature Specification
6. Implementation
7. Validation
8. Checkpoint Log

AI must never skip levels.

If an architectural change is required, a new ADR must be created before implementation proceeds.
If product direction changes materially, a PDR should be created before feature execution.

---

## Phases

Only one phase may be active at a time.

No feature from a future phase may move to `workflow/planning/active/` while a prior phase is incomplete.

Phase definitions are authoritative in:

`workflow/ROADMAP.md`
`workflow/phases/`

---

## AI Operation Modes

All AI sessions must declare one of the following modes:

### Architecture Mode

* Operates only on ADRs.
* No feature planning.

### Feature Mode

* Operates on a single feature file.
* No multi-feature reasoning.

### Task Planning Mode

* Breaks one feature into ordered tasks.
* No architectural modifications.

### Code Mode

* Operates on one file at a time.
* Must not modify unrelated areas.

### Drift Review Mode

* Compares implementation against:

  * Feature spec
  * Related ADRs
  * Phase constraints
* Identifies violations or hidden coupling.

---

## Scope Declaration Requirement

Every AI session must begin with:

* Current Phase (`PHASE-X`)
* Current Feature (`FXXX`)
* Relevant PDRs (`PDR-XXX` or `None`)
* Relevant ADRs (`ADR-XXX` or `None (justification)`)
* Explicit non-scope items

Example:

Phase: PHASE-1
Feature: F002
Related PDRs: PDR-001
Related ADRs: ADR-003, ADR-015
Non-scope (explicit):

* @axr/theme
* Component layer
* Documentation

---

## Supersession Discipline

If a feature or ADR becomes outdated:

* Mark the prior artifact as Superseded.
* Link replacement via `Superseded by`.
* Do not silently modify historical documents.
* Create a replacement artifact.

AI must not reference superseded artifacts unless performing historical analysis.

---

## Drift Prevention Rules

AI must not:

* Introduce new architectural patterns without ADR.
* Expand feature scope beyond specification.
* Propose future-phase work during active-phase execution.

---

## Review Gate

Before marking a feature complete:

1. Validate against Acceptance Criteria.
2. Validate against related PDRs and ADRs.
3. Confirm no scope expansion occurred.
4. Log a checkpoint using `workflow/templates/CHECKPOINT.md`.
5. Fill `Completed:` date in the feature file.
6. Move feature artifact to `workflow/planning/archive/`.
7. Log milestone in `workflow/milestones/`.

---

## Long-Term Integrity Principle

The repository prioritizes:

* Determinism
* Traceability
* Supersession clarity
* Phase discipline

AI is a reasoning assistant — not a source of truth.
The repository documents are the source of truth.
