---
description: "Use when working with GitHub issues, assigned issues, refinement, requirements.md, design.md, tasks.md, ready label, or spec-driven software development in this repository."
---

# Spec-Driven Workflow

Use this workflow whenever a task starts from a GitHub issue or changes the repository specs.

## Canonical Specs

- Read `requirements.md`, `design.md`, and `tasks.md` before planning issue work.
- The initial expected state is structure-only spec files with placeholders; the first refined issue should start filling them.
- If a spec file is missing, say so explicitly and propose the smallest useful initial structure.
- Treat populated spec content as canonical context, but do not invent missing requirements or hidden approvals from empty placeholders.
- Keep proposed changes mapped to the affected spec file and section.

## Refinement Phase

- Refinement produces a plan, not direct file edits, unless the user explicitly changes that rule.
- The refinement output must include the user need, affected requirements, design impacts, task impacts, open questions, and readiness criteria.
- Any blocking uncertainty must become a GitHub issue comment question.
- If a GitHub commenting tool is unavailable, return a ready-to-post comment instead.

## Ready Phase

- A GitHub issue can move to development only when it has the `ready` label and no blocking refinement questions remain.
- If `ready` appears without an existing refinement plan, run refinement first.
- Development must stay inside the issue scope, the refinement plan, and the canonical specs.