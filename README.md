# react-supa

Minimal React + TypeScript + Vite starter wired up to Supabase (based on a
tutorial).

This repo is a small demo app that uses Supabase for authentication and a simple
message/post board. It was built with Vite, React + TypeScript and Tailwind CSS.
The project includes a local `supabase/` folder with migrations and helpful SQL
scripts.

## Contents

- `src/` — React + TypeScript source files
- `supabase/` — Supabase configuration, migrations and helper SQL (see
  `supabase/migrations` and `supabase/clear-db-data.sql`)
- `e2e/` — example Playwright end-to-end test(s)
- `package.json` — scripts and dependencies

## Prerequisites

- Node.js (16+ recommended)
- pnpm, npm or yarn (this repo contains a `pnpm-lock.yaml` but npm/yarn will
  also work)
- (Optional) Docker & Supabase CLI if you want to run the Supabase local Docker
  stack

## Environment variables

The app reads the Supabase configuration from Vite environment variables. Create
a `.env` or `.env.local` file in the project root with the following values
(these keys must start with `VITE_` so Vite exposes them to the client):

```
VITE_SUPABASE_API_URL=https://your-project-ref.supabase.co
VITE_SUPABASE_ANON_KEY=your-anon-public-key
```

To obtain those values:

- Create a project at https://app.supabase.io or use your existing Supabase
  project
- From the project dashboard go to Settings → API and copy the URL and anon key

If you prefer to run Supabase locally using the Supabase CLI and Docker, you can
use the `supabase/` folder in this repo which already contains migrations and a
`clear-db-data.sql` script. Installing the Supabase CLI and running
`supabase start` will bring up the local stack. See the Supabase docs for
details.

## Quick start

Install dependencies:

```bash
# using pnpm (recommended because of lockfile)
pnpm install

# or with npm
npm install
```

Run the dev server (Vite):

```bash
npm run dev
```

Build for production:

```bash
npm run build
```

Preview the production build locally:

```bash
npm run preview
```

Lint the project:

```bash
npm run lint
```

## Supabase and database migrations

- Migrations are stored in `supabase/migrations`. You can apply them using the
  Supabase CLI (`supabase db push` / `supabase db reset`) or by running SQL
  against your Supabase instance.
- A quick SQL helper to clear test/demo data is available at
  `supabase/clear-db-data.sql`.

If you run the Supabase local Docker stack (`supabase start`) and need the API
URL and anon key for that local instance, the CLI prints the values when the
stack is running. Use those values in your `.env` file.

## Tests / Playwright

This repo has a sample end-to-end test under `e2e/`. To run Playwright tests
(requires `@playwright/test`):

```bash
npx playwright test
```

Or using pnpm:

```bash
pnpm exec playwright test
```

## Useful files

- `src/supa-client.ts` — creates and exports the Supabase client. Important env
  vars used there are `VITE_SUPABASE_API_URL` and `VITE_SUPABASE_ANON_KEY`.
- `supabase/clear-db-data.sql` — SQL script to clean example data during
  development/testing.
- `supabase/migrations/` — SQL migrations that define the demo schema.

## Notes and next steps

- This repo is a small demo. If you ship a production app:
  - Don't expose any service_role keys to the client
  - Use stricter CORS and RLS policies in Supabase
  - Add tests and CI that run migrations against a disposable database

If you want, I can:

- add a sample `.env.example` file
- add a short script to automate local Supabase start + migrate
- wire up Github Actions to run lint/tests on push

---

Generated from a learning/demo project inspired by a Supabase + React tutorial.
