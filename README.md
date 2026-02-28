# AI Workflow Template

A reusable, governance-driven workflow scaffold for AI-assisted software development.

This template is architecture-first, ADR-first, phase-based, and designed for deterministic delivery.

## What You Get

- `workflow/`: source-of-truth operating model, product vision, roadmap, phases, decisions, journal, milestones, and templates
- `.github/`: issue templates, PR template, CODEOWNERS, and CI/phase-guard workflows
- `GITHUB_SETUP.md`: detailed `.github` setup and validation guide
- `claude.md`: repository-level Claude operating instructions
- `instructions.md`: setup and usage guide for initializing a new project from this template

## Core Rules

- Product intent captured in `workflow/PRODUCT.md`
- Product-level decisions captured as PDRs in `workflow/pdr/`
- ADR-before-implementation for architectural changes
- Single active feature (`workflow/planning/active/`)
- Explicit scope and non-scope for each feature
- Supersession traceability (`Supersedes` / `Superseded by`)
- Deterministic PR and CI enforcement

## Quick Start

1. Copy this template into a new repository.
2. Update owners and defaults:
   - `.github/CODEOWNERS`
   - `workflow/PRODUCT.md`
   - `workflow/phases/PHASE-*.md` front matter
   - `workflow/ROADMAP.md`
3. Add any initial product decisions from `workflow/templates/PDR.md` to `workflow/pdr/`.
4. Create your first feature from `workflow/templates/FEATURE.md` in `workflow/planning/backlog/`.
5. Activate one feature by moving it to `workflow/planning/active/`.
6. Execute only against the active feature and log progress via `workflow/templates/CHECKPOINT.md` in `workflow/journal/`.

## How To Adopt This Template

You can use this in two ways:

1. Start from this repository:
   - Create a new repo from this template (or clone/fork it).
   - Add your application code into this repo.
   - Keep `workflow/`, `.github/`, and root governance docs as your operating system.
2. Add into an existing repository:
   - Copy these paths into your existing project root:
     - `workflow/`
     - `.github/`
     - `claude.md`
     - `instructions.md`
     - `WORKFLOW_DIAGRAM.md`
     - `GITHUB_SETUP.md`
   - Commit them as an onboarding baseline.
   - Run the setup sequence in `instructions.md`.

## Governance Sources

- Feature contract: `workflow/decisions/governance/FEATURE_GOVERNANCE_CONTRACT.md`
- Operating model: `workflow/AI_OPERATING_MODEL.md`
- Git process: `workflow/GIT_WORKFLOW.md`

## Next

Read `instructions.md` for full setup, customization checklist, and starter prompts.
Use `GITHUB_SETUP.md` for detailed GitHub governance/CI configuration.
