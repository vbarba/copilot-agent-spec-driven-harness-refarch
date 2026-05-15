# Copilot Agent Spec-Driven Harness Reference Architecture

This repository defines a reference architecture for a spec-driven Copilot issue workflow.

## Workflow

1. Copilot is assigned to a GitHub issue.
2. The issue orchestrator delegates refinement to the spec refinement subagent.
3. The refinement subagent reads `requirements.md`, `design.md`, and `tasks.md` and returns a plan plus any blocking questions.
4. The orchestrator updates the issue when GitHub issue write tools are available, or returns the exact Markdown comment/body to post when they are unavailable.
5. When the issue is labeled `ready`, the orchestrator delegates implementation to the software development subagent.

## GitHub Issue Write Access

The `Spec Refinement` subagent is intentionally read-only. It returns exact Markdown for either a clarification comment or a replacement issue body.

The `Issue Orchestrator` is responsible for publishing that Markdown. To comment on or edit issues directly, it needs one of these write paths:

- A dedicated GitHub issue tool in its runtime and allowlist.
- An authenticated GitHub CLI (`gh`) available in the workspace shell.

For the `gh` path, verify the environment before relying on direct issue updates:

```sh
gh auth status
gh issue view <issue-number>
```

When no write path is available, the orchestrator returns the exact Markdown that should be posted manually or by an external workflow.

### Cloud Environments

Cloud agents do not inherit a developer's local `gh` login. To let the orchestrator comment on or edit issues in cloud, provide one of these capabilities in the cloud runtime:

- A native GitHub issue tool with permission to read issues, create issue comments, and edit issue bodies.
- `gh` plus `GH_TOKEN` or `GITHUB_TOKEN` with issue write permission.

For GitHub Actions-based runs, the workflow needs issue write permission, for example:

```yaml
permissions:
  contents: read
  issues: write
```

Before attempting issue writes in cloud, the orchestrator should be able to pass these checks:

```sh
gh auth status
gh issue view <issue-number>
```

For hosted Copilot coding agent runs, verify that the GitHub App or agent integration is enabled for the repository and allowed to read and write issues. If the runtime only exposes repository file tools and no issue write API, the expected behavior is still to return the exact Markdown for an external workflow or user to post.

## Files

- `.github/copilot-instructions.md`: repository-wide Copilot behavior.
- `.github/instructions/spec-driven-workflow.instructions.md`: discoverable workflow guidance for issue/spec work.
- `.github/agents/issue-orchestrator.agent.md`: main issue lifecycle coordinator.
- `.github/agents/spec-refinement.agent.md`: read-only refinement subagent.
- `.github/agents/software-development.agent.md`: implementation subagent for ready issues.
- `requirements.md`: structure-only requirements template populated by refined issues.
- `design.md`: structure-only design template populated by refined issues.
- `tasks.md`: structure-only task template populated by refined issues.