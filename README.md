# gh-copilot-orchestrator-template

A drop-in template for implementing the **orchestrator pattern** with GitHub Copilot custom agents. The orchestrator plans and delegates work to specialized sub-agents (implementer, tester, reviewer, style-checker) instead of doing everything itself — leading to more reliable, multi-step results for non-trivial tasks.

## Getting Started

1. **Copy** the `.github/` folder into your own repository.
2. **Fill in the placeholders** — every spot marked with `<...>` is a hole for project-specific context (tech stack, conventions, file patterns, test commands, etc.). The more accurate and specific you are, the better the agents perform.
3. **Start using the agents** — open Copilot Chat in agent mode and either invoke the `orchestrator` directly for complex tasks, or let it be auto-selected based on the agent descriptions.

## What's Inside

```
.github/
├── copilot-instructions.md       # Project-wide context loaded into every Copilot session
└── agents/
    ├── orchestrator.agent.md     # Plans + delegates (the core of the pattern)
    ├── feature-implementer.agent.md  # Writes/refactors production code
    ├── tester.agent.md           # Writes/maintains unit tests
    ├── style-checker.agent.md    # Reviews styling/UI consistency
    └── code-reviewer.agent.md    # Reviews code quality, patterns, security
```

## Customization Tips

- **Models** — each agent specifies a `model:` in its frontmatter. Swap to whatever models you have access to (e.g. `Claude Sonnet 4.6 (copilot)`, `GPT-5.3-Codex (copilot)`). Heavier models for orchestration/review, faster models for implementation.
- **Tech-stack agnostic** — the templates use neutral language. Fill `<...>` with your stack: e.g. "Angular 18 + RxJS + Jasmine", "Next.js + React + Vitest", "FastAPI + pytest", "Rust + cargo test".
- **Remove what you don't need** — the `style-checker` agent is geared toward UI/CSS work. For backend, CLI, library, or infrastructure projects, you can either delete it or repurpose it (e.g. as a "docs-checker" or "schema-checker"). If you remove it, also drop it from the mandatory pipeline in `orchestrator.agent.md` and the agent table in `copilot-instructions.md`.
- **Add your own agents** — drop additional `*.agent.md` files into `.github/agents/` for project-specific roles (e.g. `db-migrator`, `api-designer`, `security-auditor`) and register them in the orchestrator's delegation table.
- **Mandatory pipeline** — the orchestrator enforces a `feature-implementer → tester → style-checker → code-reviewer` pipeline for every feature. Adjust this in `orchestrator.agent.md` if it doesn't fit your workflow.

## How the Pattern Works

```
User request
    ↓
orchestrator  ──→  plan          (optional: research & break down)
    ↓
    ├──→  feature-implementer    (write/modify code)
    ├──→  tester                 (write/update tests)
    ├──→  style-checker          (verify styling — optional for non-UI projects)
    └──→  code-reviewer          (final quality review)
    ↓
Verified result reported back to user
```
