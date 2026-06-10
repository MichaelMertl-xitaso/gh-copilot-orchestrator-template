# Copilot Instructions — <...>

## Project Context

<...>

### Key Dependencies

<...>

## App Structure

<...>

## Available Agents

Use `.github/agents/` agents via `run_subagent` for specialized tasks:

| Agent | When to use |
|---|---|
| `orchestrator` | Complex multi-step features touching multiple files/concerns |
| `plan` | Understanding impact before starting; large refactors |
| `feature-implementer` | Creating or modifying <...> |
| `tester` | Writing or fixing unit tests |
| `style-checker` | Reviewing <...> for <...> |
| `code-reviewer` | Code quality review after implementation |