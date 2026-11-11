# Project Pulse implementation plan

## Goal

Build a lightweight, static Project Pulse dashboard that lets contributors see active projects, owners, status, recent activity, priority or risk, and contributor-friendly summaries. The result must be polished, accessible, and runnable through the VS Code **Run Project Pulse Dashboard** launch configuration.

## File assignments and responsibilities

| File | Owner | Responsibility |
| --- | --- | --- |
| `app/project-data.json` | Coder | Define a valid top-level `projects` array. Every project will provide `name`, `owner`, `status`, `recentActivity`, and `priority`, with a contributor-friendly summary for display. |
| `app/index.html` | Coder | Build the semantic dashboard structure, exact `Project Pulse` title, data-loading/rendering behavior, project-card markup, and empty or error state. |
| `app/styles.css` | Designer | Define the responsive visual system and accessible layout: information hierarchy, readable spacing, project cards, status badges, priority treatment, contrast, focus states, and mobile behavior. The Coder integrates these styles with the HTML hooks. |
| `.vscode/launch.json` | Coder | Add a strict JSON configuration named **Run Project Pulse Dashboard** that serves `app/`, uses `${workspaceFolder}/app` as its working directory, and opens `index.html` rather than a directory listing. |

The Designer is responsible for the UI/UX decisions and CSS implementation within `app/styles.css`. The Coder is responsible for the static HTML, data contract, rendering behavior, and launch configuration. The Orchestrator assigns these scopes, resolves any cross-file contract questions, and reviews the integrated dashboard.

## Phases, dependencies, and parallel work

1. **Establish the data and interface contract.** The Coder defines representative project records in `app/project-data.json` and the fields that `app/index.html` will consume. This is a dependency for final data rendering.
2. **Design and structure the dashboard.** The Designer can create `app/styles.css` in **parallel** with the Coder's initial `app/index.html` structure because their file scopes do not overlap. They coordinate on stable class hooks such as `.dashboard` and `.project-card`.
3. **Integrate rendering and styling.** The Coder implements data loading and project-card rendering in `app/index.html`, using the agreed data schema and Designer's CSS hooks. This work depends on the data contract; final styling review depends on the integrated markup.
4. **Configure and verify launch behavior.** The Coder creates `.vscode/launch.json` after the app path is confirmed. It is independent of the dashboard content, so it may run in **parallel** with Phase 2, but browser validation must wait until `app/index.html` exists.
5. **Review the completed experience.** The Designer reviews the rendered dashboard for hierarchy, responsive behavior, accessibility, and visual clarity. The Orchestrator checks that all files work together before handoff.

## Validation expectations

- Confirm `app/project-data.json` is valid JSON with a top-level `projects` array and all required fields for each record.
- Open `app/index.html` through **Run Project Pulse Dashboard** and verify it displays the Project Pulse UI, not a server directory listing.
- Confirm each project card presents its name, owner, status, recent activity, priority, and summary.
- Verify `app/index.html` references `app/styles.css` and loads `app/project-data.json` successfully.
- Review the dashboard at desktop and narrow viewport widths for readable layout, visible status and priority treatment, sufficient contrast, and keyboard focus visibility.
- Confirm `.vscode/launch.json` is valid strict JSON, serves from `${workspaceFolder}/app`, and opens `index.html`.
