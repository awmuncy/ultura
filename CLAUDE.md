# Ultura

Monorepo-style umbrella containing two independent git repos:

- `frontend/` — Expo (React Native) app (repo: awmuncy/ai-nki-expo)
- `etc-api/` — Express API backend (repo: awmuncy/etc-api)

## Working across repos

- Each subdirectory is its own git repo — commit and push separately.
- Run frontend commands from `frontend/`, API commands from `etc-api/`.

## API-to-frontend workflow

The `etc-api` exposes an OpenAPI spec at `/openapi.json`. The frontend consumes it to generate typed API clients. When making changes that touch both repos:

1. Make API changes in `etc-api/` first.
2. Run the API locally (`npm run dev` from `etc-api/`, runs on port 3000).
3. Run `npm run gen-api:local` from `frontend/` to regenerate the client from the local API.
4. Make frontend changes using the updated generated types.
5. Before deploying/merging, switch back to `npm run gen-api` (points to production) if needed.
