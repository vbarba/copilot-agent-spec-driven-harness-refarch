---
description: "Use when working with GitHub issues, assigned issues, refinement, requirements.md, design.md, tasks.md, ready label, or spec-driven software development in this repository."
---

# Spec-Driven Workflow

Use this workflow whenever a task starts from a GitHub issue or uses the repository specs as planning context.

## Canonical Specs

- Read `requirements.md`, `design.md`, and `tasks.md` before planning issue work.
- The initial expected state is structure-only spec files with placeholders; the first refined issue should start filling them.
- If a spec file is missing, say so explicitly and propose the smallest useful initial structure.
- Treat populated spec content as canonical context, but do not invent missing requirements or hidden approvals from empty placeholders.
- Keep proposed spec impact mapped to the affected spec file and section, but document it in the issue during refinement.

## Refinement Phase

- Refinement produces issue updates, not repository file edits.
- The refinement subagent must never modify, commit, push, or open pull requests for `requirements.md`, `design.md`, or `tasks.md`.
- The refinement output must include the user need, affected requirements, design impacts, task impacts, open questions, and readiness criteria as GitHub issue content.
- Any blocking uncertainty must become a GitHub issue comment question.
- When there are no blocking questions, the refinement output must be a complete issue body update with the plan and readiness criteria.
- If GitHub issue tools are unavailable, return a ready-to-post comment or replacement issue body instead.

## Ready Phase

- A GitHub issue can move to development only when it has the `ready` label and no blocking refinement questions remain.
- If `ready` appears without an existing refinement plan, run refinement first.
- Development must stay inside the issue scope, the refinement plan, and the canonical specs.