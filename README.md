# Copilot Agent Spec-Driven Harness Reference Architecture

This repository defines a reference architecture for a spec-driven Copilot issue workflow.

## Workflow

1. Copilot is assigned to a GitHub issue.
2. The issue orchestrator delegates refinement to the spec refinement subagent.
3. The refinement subagent reads `requirements.md`, `design.md`, and `tasks.md` and returns a plan plus any blocking questions.
4. The orchestrator updates the issue, or returns the exact Markdown comment to post when GitHub issue updates are unavailable.
5. When the issue is labeled `ready`, the orchestrator delegates implementation to the software development subagent.

## Files

- `.github/copilot-instructions.md`: repository-wide Copilot behavior.
- `.github/instructions/spec-driven-workflow.instructions.md`: discoverable workflow guidance for issue/spec work.
- `.github/agents/issue-orchestrator.agent.md`: main issue lifecycle coordinator.
- `.github/agents/spec-refinement.agent.md`: read-only refinement subagent.
- `.github/agents/software-development.agent.md`: implementation subagent for ready issues.
- `requirements.md`: structure-only requirements template populated by refined issues.
- `design.md`: structure-only design template populated by refined issues.
- `tasks.md`: structure-only task template populated by refined issues.