# Jafjeer

Arabic RTL recipe website for discovering home cooking, matching recipes to pantry ingredients, and managing a shopping list.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server
- `pnpm --filter @workspace/jafjeer run dev` — run the Jafjeer web app
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string
- `JAFJEER_ADMIN_EMAILS` — comma-separated, verified email addresses allowed to manage recipes
- Google sign-in is configured in the Replit Auth pane for the Clerk app; development and production auth users are separate

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/jafjeer` — public website, pantry matcher, shopping list, moderator dashboard, and sign-in pages
- `artifacts/api-server` — recipe APIs, administrator checks, and image upload URLs
- `lib/api-spec/openapi.yaml` — API contract; regenerate clients after changes with the `api-spec` codegen command
- `lib/db/src/schema/recipes.ts` — persistent recipe data model

## Architecture decisions

- Recipe records live in PostgreSQL; uploaded recipe images live in App Storage.
- Clerk sessions authenticate users; the API enforces the configured administrator email allowlist.
- Pantry selections and shopping lists are kept in each visitor's browser storage.

## Product

- Search and filter Arabic recipes; view ingredients and preparation steps.
- Match recipes against ingredients selected in “ماذا في بيتي؟”.
- Build a shopping list manually or from recipe ingredients.
- Administrators can add, edit, and delete recipes, upload an image, and link a video.

## User preferences

- The product interface is Arabic and right-to-left.

## Gotchas

- A moderator must use a verified email listed in `JAFJEER_ADMIN_EMAILS`.
- Google SSO must be enabled in the Clerk Auth pane before Google sign-in is available.
- Keep public recipes and recipe image viewing accessible without sign-in; protect recipe writes and image upload URL creation.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
