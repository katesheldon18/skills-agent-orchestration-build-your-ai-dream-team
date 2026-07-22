# Agent team

To build Mona's Project Pulse dashboard, I'm using a four-agent custom team defined under `.github/agents/`, orchestrated with GitHub Copilot CLI running in a Codespace.

## Orchestrator

- **Model:** Claude Opus 4.7 (copilot)
- **Responsibility:** Coordinates the Planner, Coder, and Designer. Breaks the request into phases, assigns non-overlapping file scopes, decides what can run in parallel vs. sequentially, and reports final results to the learner. Does not implement work itself.
- **Definition:** `.github/agents/orchestrator.agent.md`

## Planner

- **Model:** Claude Opus 4.7 (copilot)
- **Responsibility:** Researches the repository and relevant docs/APIs, then produces an implementation plan with ordered steps, file assignments, dependencies, parallelizable work, edge cases, and validation expectations. Does not write code.
- **Definition:** `.github/agents/planner.agent.md`

## Coder

- **Model:** GPT-5.5 (copilot)
- **Responsibility:** Implements code within the file scope assigned by the Orchestrator — clear structure, explicit errors, testable behavior. For Project Pulse, also creates supporting files like `.vscode/launch.json` (with `cwd` set to `${workspaceFolder}/app` and `index.html` opened) when assigned.
- **Definition:** `.github/agents/coder.agent.md`

## Designer

- **Model:** Gemini 3.1 Pro (copilot)
- **Responsibility:** Owns UI/UX, accessibility, information architecture, and visual design within its assigned scope. For Project Pulse, builds a polished dashboard with project cards, status badges, priority treatment, and deterministic CSS hooks (e.g., `.dashboard`, `.project-card`).
- **Definition:** `.github/agents/designer.agent.md`

All four agents avoid staging, committing, or pushing changes — git operations remain under my control via Copilot CLI prompts.
