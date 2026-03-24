# Ultura

Monorepo-style umbrella containing two independent git repos:

- `fe/` — Expo (React Native) app (repo: awmuncy/ai-nki-expo)
- `api/` — Express API backend (repo: awmuncy/etc-api)

## Working across repos

- Each subdirectory is its own git repo — commit and push separately.
- Run frontend commands from `fe/`, API commands from `api/`.

## API-to-frontend workflow

The `api/` exposes an OpenAPI spec at `/openapi.json`. The frontend consumes it to generate typed API clients. When making changes that touch both repos:

1. Make API changes in `api/` first.
2. Run the API locally (`npm run dev` from `api/`, runs on port 3000).
3. Run `npm run gen-api:local` from `fe/` to regenerate the client from the local API.
4. Make frontend changes using the updated generated types.
5. Before deploying/merging, switch back to `npm run gen-api` (points to production) if needed.

## Roadmap

### Features
1. **Tasks page with deadline view** — Evolve the Routines tab into a "Tasks" page. Routines keep compact square icons (many per row); non-recurring tasks get full-width rows with title. May include projects/milestones later.
2. **In-app triage** — Triage tasks within the app instead of Linear. Per task: set due date (or "no due date"), create forfeit, select project (or none), move Triage → To-do. Possibly quick-action buttons.
3. **Deadline vs goal-line distinction** — Differentiate hard deadlines from soft targets in Linear. No solution decided yet.
4. **Routine interval distinction** — Visually differentiate daily/weekly/monthly routines (e.g. color shading). Blocked: interval data not yet in API.
5. **Project and initiative views** — Early-stage idea, no concrete design yet.
6. **Weight goal bar visualizer** — 14-day bar chart; green bars above and red bars below either next goal or current weight.

### UX improvements
7. **Prettier "More" page** — Current design needs polish.
8. **Stronger design opinions from LLM** — Better prompting or a pairing session for more opinionated UI suggestions.
