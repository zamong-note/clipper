# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Runtime

- This is **vinext**, not Next.js: Next-style App Router code (`app/`, `next/*` imports) built by Vite (`vite.config.ts`) and run on Cloudflare Workers. Don't add Next-only config or Node-only APIs; code runs in the Workers runtime.
- D1 is reached through `getDatabase()` in `lib/clipper/db.ts`, which reads the `DB` binding from `cloudflare:workers` `env`. Query with Drizzle; schema is `db/schema.ts`.
- After changing bindings in `wrangler.jsonc`, regenerate types with `npm run cf-typegen` (writes `worker-configuration.d.ts`).
- Timestamps are stored as integer milliseconds (`mode: "timestamp_ms"`), and prices as `priceCents`.

## Local database

- `npm run db:migrate:local` applies `drizzle/` migrations to the local D1 in `.wrangler/`.
- `npm run db:seed:local` **wipes all tables** (including appointments) before reseeding from `scripts/seed.sql`.

## Verification

- There are no tests. Verify with `npm run lint` and `npx tsc --noEmit`.

## Git

- Never create commits; the user commits manually.
