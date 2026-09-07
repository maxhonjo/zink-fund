# Plan 0001: Blank Express Server Deployed on Railway

**Decisions locked in:** JavaScript (no TypeScript), npm, npm workspaces (root `package.json` linking `client/` and `server/`), Vite + React for the frontend.

**Goal:** A single Railway service that builds the React/Vite client into static assets, serves them from an Express server, and exposes a working health-check API route — all deployed and verified live. No spending-tracker functionality yet.

## Phase 1: Repository Scaffolding
- Step 1: Initialize git repo at project root; add `.gitignore` (`node_modules/`, `client/dist/`, `.env`, `.railway/`)
- Step 2: Create root `package.json` declaring npm workspaces: `["client", "server"]`
- Step 3: Confirm `docs/sessions/` exists for this plan/handoff pair

## Phase 2: Backend Setup (Express)
- Step 1: Create `server/` workspace, `npm init` inside it
- Step 2: Install `express` as a dependency of `server/`
- Step 3: Write `server/index.js` — minimal Express app with `GET /api/health` returning `{ status: "ok" }`, listening on `process.env.PORT`
- Step 4: Add `"start": "node index.js"` script to `server/package.json`
- Step 5: Run locally and confirm `/api/health` responds

## Phase 3: Frontend Setup (Vite + React)
- Step 1: Scaffold `client/` with `npm create vite@latest client -- --template react`
- Step 2: Run the Vite dev server locally and confirm the default React starter page loads
- Step 3: Confirm `npm run build -w client` produces `client/dist`

## Phase 4: Wire Frontend + Backend Into One Service
- Step 1: Update `server/index.js` to serve `client/dist` via `express.static` in production
- Step 2: Add a catch-all GET fallback to `index.html` for non-`/api` routes (SPA-friendly, even though there's no routing yet)
- Step 3: Add root `package.json` scripts: `"build": "npm run build -w client"`, `"start": "npm run start -w server"`
- Step 4: Locally run `npm run build` then `npm run start` from root and confirm one server on one port serves both the React page and `/api/health`

## Phase 5: Railway Configuration
- Step 1: Create a new Railway project and service
- Step 2: Confirm Railway's Nixpacks auto-detection picks up root `build`/`start` scripts (fallback: add explicit `railway.json` if needed)
- Step 3: Confirm Railway injects `PORT` and the server reads it correctly
- Step 4: Set `NODE_ENV=production` as a Railway environment variable

## Phase 6: Deploy & Verify
- Step 1: Push repo to GitHub
- Step 2: Connect Railway service to the GitHub repo (or deploy via Railway CLI)
- Step 3: Trigger a deploy and review build logs for errors
- Step 4: Visit the deployed URL — confirm the React starter page loads
- Step 5: Hit `<deployed-url>/api/health` — confirm it responds correctly
- Step 6: Confirm this is a single Railway service (not split frontend/backend services)

## Phase 7: Session Wrap-up
- Step 1: Write `docs/sessions/handoff_0001.md` capturing implementation decisions — exact Railway build/start commands used, any deviations from this plan, static-serving approach in Express
