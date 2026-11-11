# Mona's Project Pulse agent team

I am using GitHub Copilot CLI in a Codespace to orchestrate a four-agent team for Mona's Project Pulse dashboard:

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 5.5 (copilot) | Coordinates the team: obtains a plan, assigns explicit and non-overlapping file scopes, sequences dependent work, and verifies the integrated result. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 5.5 (copilot) | Researches the repository and relevant documentation, then produces implementation phases, dependencies, file assignments, risks, edge cases, and validation expectations. | `.github/agents/planner.agent.md` |
| Coder | GPT-5.5 (copilot) | Implements assigned application logic and fixes with explicit errors, deterministic behavior, and validation; can add runnable-app support when assigned. | `.github/agents/coder.agent.md` |
| Designer | Gemini 3.7 Flash (copilot) | Owns the dashboard's UI/UX direction, accessibility, information hierarchy, responsive styling, and visual clarity. | `.github/agents/designer.agent.md` |

The workflow starts with the Planner, then the Orchestrator turns the plan into dependency-aware phases for the Coder and Designer. All agents keep to their assigned file scopes and leave staging, commits, and pushes under learner control through Copilot CLI.
