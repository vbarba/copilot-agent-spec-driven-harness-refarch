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

- Refinement produces issue-ready Markdown, not repository file edits.
- The refinement subagent must never modify, commit, push, or open pull requests for `requirements.md`, `design.md`, or `tasks.md`.
- The refinement output must include the user need, affected requirements, design impacts, task impacts, open questions, and readiness criteria as GitHub issue content.
- Any blocking uncertainty must become exact Markdown for a GitHub issue comment question.
- When there are no blocking questions, the refinement output must be a complete replacement issue body with the plan and readiness criteria.
- If GitHub issue write tools are unavailable, return the ready-to-post comment or replacement issue body instead.

## GitHub Issue Publishing

- The issue orchestrator is the only agent responsible for publishing refinement output to GitHub issues.
- Prefer a dedicated GitHub issue write tool when the runtime provides one.
- If using the GitHub CLI, verify `gh auth status` before posting or editing issues.
- In cloud environments, require a native GitHub issue write tool or `GH_TOKEN`/`GITHUB_TOKEN` with issue write permission; do not assume local developer credentials are present.
- If publishing cannot be verified, return the exact Markdown comment or replacement issue body instead of attempting a write.

## Ready Phase

- A GitHub issue can move to development only when it has the `ready` label and no blocking refinement questions remain.
- If `ready` appears without an existing refinement plan, run refinement first.
- Development must stay inside the issue scope, the refinement plan, and the canonical specs.