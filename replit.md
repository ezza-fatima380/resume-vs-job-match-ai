# Resume vs Job Match AI

A focused web app that compares a resume with a job description using Google Gemini and returns a match score, skill overlap, gaps, and practical improvement tips.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `GEMINI_API_KEY` — Google Gemini API key for resume analysis (stored as a Replit Secret)

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/resume-job-match-ai/src/App.tsx` — single-page resume/job input and results UI
- `artifacts/resume-job-match-ai/src/index.css` — app theme, typography, responsive layout, and motion
- `artifacts/resume-job-match-ai/server/app.py` — Flask API and Gemini request/JSON normalization
- `lib/api-spec/openapi.yaml` — source-of-truth contract for `POST /api/analyze-match`
- `artifacts/api-server/src/routes/match.ts` — same-origin bridge from `/api` to the Flask service

## Architecture decisions

- The AI request lives in Flask to honor the requested Python backend; the shared API server proxies the browser-facing `/api` route.
- Gemini’s JSON response mode is requested explicitly, then the Flask layer validates and normalizes the response. The requested `gemini-1.5-flash` model currently returns 404 from Google’s model catalog, so the service retries with the supported `gemini-flash-lite-latest` alias and transient-error backoff.
- Resume and job text are kept in React state for the session and are not persisted.

## Product

- Paste a resume and job description, then analyze the fit with Gemini.
- See a percentage score, matching skills, missing skills, and short resume improvement suggestions.
- Load an example, retry an analysis, clear the form, and copy the report.

## User preferences

- Keep the design clean and simple.

## Gotchas

- `GEMINI_API_KEY` must be present for analysis; without it the API intentionally returns a clear configuration error.
- The Flask service uses the artifact's `/resume-api` route for health access, while the browser uses `/api/analyze-match` through the shared bridge.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
