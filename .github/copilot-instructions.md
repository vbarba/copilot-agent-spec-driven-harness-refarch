# Copilot Repository Instructions

This repository defines a spec-driven Copilot agent harness. Treat GitHub issues as the entry point for work and use the repository specs as the source of truth:

- `requirements.md` describes user needs, constraints, acceptance criteria, and unresolved questions.
- `design.md` describes architecture, workflows, data flow, agent responsibilities, and integration assumptions.
- `tasks.md` describes implementation tasks, status, dependencies, and verification steps.

## Issue Workflow

- When Copilot is assigned to a GitHub issue, route the issue through the issue orchestration workflow before implementing anything.
- Delegate requirement clarification and planning to the spec refinement subagent.
- The refinement subagent must propose a plan for changing `requirements.md`, `design.md`, and `tasks.md`; it must not modify those files directly in this first version of the workflow.
- If clarification is needed, ask it as a GitHub issue comment. When no GitHub issue commenting tool is available, return the exact comment text that should be posted.
- Do not treat an issue as ready for development while open refinement questions remain.
- When an issue has the `ready` label, delegate implementation to the software development subagent.
- If `ready` is present but no refinement plan exists, run refinement before development.

## Development Rules

- Keep changes scoped to the refined issue plan and the canonical specs.
- Prefer existing repository conventions over new abstractions.
- Update specs only when explicitly requested by the issue plan or by the user.
- Run relevant verification commands when implementation changes code or documentation structure.
- Report verification results and any unresolved risks in the issue response.