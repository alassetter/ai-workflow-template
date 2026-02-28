# Feature Governance Contract

This repository operates under a strict workflow operating system located in `workflow/`.

All meaningful work must be tracked as an `FXXX` Feature.

Governance is mandatory.

---

## Lifecycle Model

Features move through exactly three states:

BACKLOG -> ACTIVE -> COMPLETE

Folder mapping:

| Status | Folder |
| --- | --- |
| BACKLOG | `workflow/planning/backlog/` |
| ACTIVE | `workflow/planning/active/` |
| COMPLETE | `workflow/planning/archive/` |

No feature may skip a state.

---

## Single Active Feature Rule

At any given time, there must be exactly ONE feature in:

`workflow/planning/active/`

Rules:

- A second feature may not move to ACTIVE until the current ACTIVE feature is COMPLETE and archived.
- If new work is requested while a feature is ACTIVE:
  - It must be added to BACKLOG.
  - It cannot be activated yet.
- Context switching is not allowed.
- Parallel feature execution is prohibited.

This repository operates in single-flight mode.

---

## Feature Requirements

Each Feature must:

- Use `FXXX` identifier (sequential, never reused)
- Include:
  - Status
  - Created date
  - Completed date (`null` until complete)
  - Related ADRs
- Define:
  - Objective
  - Scope (Included / Excluded)
  - Implementation Plan (checklist)
  - Deliverables
  - Acceptance Criteria

A feature may only be marked COMPLETE if:

- All checklist items are checked
- All deliverables exist
- Completion date is filled
- File is moved to archive

---

## Activation Rules

Before work begins:

1. Feature must exist in BACKLOG.
2. User must explicitly activate it.
3. Feature must be moved to ACTIVE.
4. Only then may execution begin.

No execution without ACTIVE status.

---

## Feature Size Discipline

If a feature exceeds ~5-7 major implementation steps:

It should be split into multiple `FXXX` features.

Small features prevent:

- Context overflow
- Partial execution states
- Governance drift

---

## Architectural Decisions (ADR)

Architectural changes require an ADR.

Location:
`workflow/decisions/adr/`

ADR statuses:

- Proposed
- Accepted
- Rejected
- Superseded

Rules:

- Accepted ADRs are immutable in meaning.
- If replacing an ADR, mark it Superseded and create a new ADR.
- Features introducing structural change must reference related ADRs.

No silent architecture changes.

---

## Golden Conversations

Golden Conversations preserve institutional insight.

Location:
`workflow/decisions/golden/`

They are required when:

- Governance shifts
- Architectural philosophy changes
- Major strategic direction is set
- AI collaboration rules are modified

Golden Conversations must:

- Capture Core Insight
- Be curated (not raw transcripts)
- Be rare and high-signal

They do not replace ADRs.

---

## Checkpoints

Location:
`workflow/journal/`

Purpose:

- Preserve session continuity
- Capture decisions and next steps
- Prevent context loss

Checkpoints are not lifecycle artifacts.
They are execution breadcrumbs.

---

## Supersession Traceability

If an artifact is replaced:

- Mark the old artifact as Superseded.
- Add forward reference (`Superseded by`) and back reference (`Supersedes`) where applicable.
- Preserve historical artifacts.

---

## Enforcement Principle

If work is not tracked as a Feature, it does not exist.

If a Feature is not ACTIVE, work must not proceed.

Long-term coherence is prioritized over short-term convenience.
