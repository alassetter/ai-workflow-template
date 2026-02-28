# AI Workflow Template

A reusable, governance-driven workflow scaffold for AI-assisted software development.

This template is architecture-first, ADR-first, phase-based, and designed for deterministic delivery.

## What You Get

- `workflow/`: source-of-truth operating model, roadmap, phases, decisions, journal, milestones, and templates
- `.github/`: issue templates, PR template, CODEOWNERS, and CI/phase-guard workflows
- `claude.md`: repository-level Claude operating instructions
- `instructions.md`: setup and usage guide for initializing a new project from this template

## Core Rules

- ADR-before-implementation for architectural changes
- Single active feature (`workflow/planning/active/`)
- Explicit scope and non-scope for each feature
- Supersession traceability (`Supersedes` / `Superseded by`)
- Deterministic PR and CI enforcement

## Quick Start

1. Copy this template into a new repository.
2. Update owners and defaults:
   - `.github/CODEOWNERS`
   - `workflow/phases/PHASE-*.md` front matter
   - `workflow/ROADMAP.md`
3. Create your first feature from `workflow/templates/FEATURE.md` in `workflow/planning/backlog/`.
4. Activate one feature by moving it to `workflow/planning/active/`.
5. Execute only against the active feature and log progress via `workflow/templates/CHECKPOINT.md` in `workflow/journal/`.

## Governance Sources

- Feature contract: `workflow/decisions/governance/FEATURE_GOVERNANCE_CONTRACT.md`
- Operating model: `workflow/AI_OPERATING_MODEL.md`
- Git process: `workflow/GIT_WORKFLOW.md`

## Next

Read `instructions.md` for full setup, customization checklist, and starter prompts.
