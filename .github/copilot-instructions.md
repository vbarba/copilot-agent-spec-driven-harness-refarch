# Copilot Repository Instructions

This repository defines a spec-driven Copilot agent harness. Treat GitHub issues as the entry point for work and use the repository specs as the source of truth:

- `requirements.md` describes user needs, constraints, acceptance criteria, and unresolved questions.
- `design.md` describes architecture, workflows, data flow, agent responsibilities, and integration assumptions.
- `tasks.md` describes implementation tasks, status, dependencies, and verification steps.

## Issue Workflow

- When Copilot is assigned to a GitHub issue, route the issue through the issue orchestration workflow before implementing anything.
- Delegate requirement clarification and planning to the spec refinement subagent.
- The refinement subagent must produce GitHub issue content documenting spec impact; it must never modify, commit, push, or open pull requests for `requirements.md`, `design.md`, or `tasks.md`.
- If clarification is needed, produce an exact GitHub issue comment. When the plan is clear, produce a replacement issue body with the refinement plan and readiness criteria.
- The orchestrator should publish that comment or body update only when a GitHub issue write tool is available; otherwise it must return the exact text to post.
- In cloud environments, do not rely on local developer authentication; publish only when the runtime exposes a GitHub issue write tool or `gh` is authenticated with `GH_TOKEN`/`GITHUB_TOKEN` that can write issues.
- When no GitHub issue update tool is available, return the exact comment text or replacement issue body that should be posted.
- Do not treat an issue as ready for development while open refinement questions remain.
- When an issue has the `ready` label, delegate implementation to the software development subagent.
- If `ready` is present but no refinement plan exists, run refinement before development.

## Development Rules

- Keep changes scoped to the refined issue plan and the canonical specs.
- Prefer existing repository conventions over new abstractions.
- Update specs only during development or a dedicated spec update task, and only when explicitly requested by the issue plan or by the user.
- Run relevant verification commands when implementation changes code or documentation structure.
- Report verification results and any unresolved risks in the issue response.