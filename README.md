# MyDesk

A fullstack todo management app built with [Nuxt 4](https://nuxt.com/docs/4.x/getting-started/introduction).

## Tech Stack

| Layer | Technology |
| --- | --- |
| Framework | [Nuxt 4](https://nuxt.com) (Vue 3 + Nitro server) |
| Language | TypeScript |
| UI Components | [shadcn-vue](https://www.shadcn-vue.com) (built on [Reka UI](https://reka-ui.com)) |
| Styling | [Tailwind CSS](https://tailwindcss.com) |
| Database | [PostgreSQL](https://www.postgresql.org) |
| ORM / Query Builder | [Drizzle ORM](https://orm.drizzle.team) + [Drizzle Kit](https://orm.drizzle.team/docs/kit-overview) for migrations |
| Package Manager | pnpm |

## Setup

Install dependencies:

```bash
pnpm install
```

Copy the environment file and adjust its values:

```bash
cp .env.example .env
```

## Development Server

Start the development server on `http://localhost:3000`:

```bash
pnpm dev
```

## Production

Build the application for production:

```bash
pnpm build
```

Locally preview the production build:

```bash
pnpm preview
```

Check out the [deployment documentation](https://nuxt.com/docs/getting-started/deployment) for more information.

## Folder Structure

The project follows the [Nuxt 4 directory structure conventions](https://nuxt.com/docs/4.x/directory-structure).

```
mydesk/
├── app/
│   ├── assets/
│   │   └── css/main.css
│   ├── components/
│   ├── composables/
│   ├── layouts/
│   │   └── default.vue
│   ├── middleware/
│   ├── pages/
│   │   └── index.vue
│   ├── plugins/
│   ├── utils/
│   ├── app.config.ts
│   ├── app.vue
│   └── error.vue
├── server/
│   ├── api/
│   ├── middleware/
│   ├── plugins/
│   ├── routes/
│   └── utils/
├── shared/
│   ├── types/
│   │   └── todo.ts
│   └── utils/
├── public/
├── .env.example
├── nuxt.config.ts
└── tsconfig.json
```

### `app/` — Frontend

All code that runs on the client (and during SSR). This is the `srcDir` in Nuxt 4, so the `~/` and `@/` aliases point here.

| Folder / File | Purpose |
| --- | --- |
| `assets/` | Assets processed by the build tool (Vite): CSS, fonts, and images imported from code. `css/main.css` is the global stylesheet registered in `nuxt.config.ts`. |
| `components/` | Reusable Vue components. **Auto-imported**: no `import` needed, just use them in templates. Components in subfolders are prefixed with the folder name, e.g. `components/todo/Item.vue` → `<TodoItem />`. |
| `composables/` | Reusable Composition API functions (state & logic), e.g. `useTodos()` for fetching and mutating todo data. **Auto-imported** (top-level files only). |
| `layouts/` | Page shells (header, sidebar, footer) that wrap pages. `default.vue` is applied automatically; other layouts are selected with `definePageMeta({ layout: 'name' })`. |
| `middleware/` | Route middleware that runs before navigating to a page, e.g. an auth check (`auth.ts`) that redirects unauthenticated users. Files ending in `.global.ts` run on every route. |
| `pages/` | Application pages with **file-based routing**. `pages/index.vue` → `/`, `pages/todos/[id].vue` → `/todos/:id`. |
| `plugins/` | Code that runs once when the Vue app is created, e.g. registering third-party libraries or providing global helpers. Use the `.client.ts` / `.server.ts` suffix to limit a plugin to one side. |
| `utils/` | Pure (non-composable) frontend helper functions, e.g. date formatting. **Auto-imported**. |
| `app.config.ts` | Public config available at runtime via `useAppConfig()`, e.g. app name or theme. Never store secrets here. |
| `app.vue` | The root component. Renders `<NuxtLayout>` and `<NuxtPage>`. |
| `error.vue` | The page shown when an error occurs (404, 500, etc.). |

### `server/` — Backend

Backend code run by Nuxt's server engine (Nitro). Code here is **never** shipped to the browser, so it's safe for database access and secrets.

| Folder | Purpose |
| --- | --- |
| `api/` | REST API endpoints, automatically prefixed with `/api`. The HTTP method comes from the file name, e.g. `api/todos/index.get.ts` → `GET /api/todos`, `api/todos/index.post.ts` → `POST /api/todos`, `api/todos/[id].patch.ts` → `PATCH /api/todos/:id`. |
| `middleware/` | Server middleware that runs on **every** request before the handler, e.g. logging or parsing a session/token. Don't return a response here unless you intend to stop the request. |
| `plugins/` | Nitro plugins that run once on server start, e.g. initializing a database connection or registering lifecycle hooks. |
| `routes/` | Server routes **without** the `/api` prefix, e.g. `routes/sitemap.xml.ts` → `/sitemap.xml`. |
| `utils/` | Server-only helpers, e.g. the database instance, validation, auth helpers. **Auto-imported** throughout `server/`. |

### `shared/` — Shared Code

Code used by **both the frontend and the backend**. Don't import anything Vue-specific or server-specific here.

| Folder | Purpose |
| --- | --- |
| `types/` | Shared TypeScript types, e.g. `todo.ts` with the `Todo` interface used in API responses and components. **Auto-imported** (top-level files only). |
| `utils/` | Helpers used on both sides, e.g. todo input validation. **Auto-imported**. |

### Root Files & Folders

| File / Folder | Purpose |
| --- | --- |
| `public/` | Static files served as-is at the root URL, e.g. `public/favicon.ico` → `/favicon.ico`. Not processed by the build tool. |
| `.env.example` | Example environment variables. Copy it to `.env` (which is not committed). `NUXT_*` variables automatically override `runtimeConfig`. |
| `nuxt.config.ts` | Main Nuxt config: modules, global CSS, `runtimeConfig`, etc. |
| `tsconfig.json` | TypeScript config, referencing the tsconfigs Nuxt generates in `.nuxt/`. |

> Empty folders contain a `.gitkeep` so they're tracked by git. Delete it once the folder has real files.
