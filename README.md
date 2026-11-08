# Sentinel

Sentinel is a full-stack **study and work tracker** for recording focus sessions, organizing projects and tasks, planning work, and reviewing activity over time.

The project started as a Web Programming assignment at the University of Catania and was expanded independently into a substantially larger application. This repository contains a reviewed source snapshot of that later work. It is distinct from the [original course repository](https://github.com/UniCT-WebDevelopment/Sentinel) and is not an official university project.

## Features

- Free-form focus sessions with recorded history and per-project statistics
- Hierarchical projects and an unscheduled task backlog
- Daily planning, scheduled sessions, and task management
- Activity charts, exports, and weekly reports
- Email/password accounts, personal API tokens, and a versioned REST API
- Responsive interface with drag-and-drop planning and accessible UI primitives

## Architecture

- **Application:** Next.js App Router, React, TypeScript and Tailwind CSS
- **Persistence:** SQLite for local development, libSQL/Turso when configured for hosted environments
- **Backend:** Same-origin Next.js route handlers, account-scoped queries, schema migrations
- **Verification:** Vitest, ESLint, TypeScript, production build, and GitHub Actions

The app and its `/api/v1/*` endpoints run in one Next.js process. Client-side caching and optimistic updates are used for some reversible interactions; the server remains authoritative.

## Run locally

Requirements: Node.js 22 or newer and pnpm 10.30.3.

```sh
corepack enable
pnpm install --frozen-lockfile
cp .env.example .env.local
pnpm dev
```

Open `http://localhost:3000`. Without Turso environment values, local development uses an ignored `local.db` SQLite file.

To populate a **disposable local development database**:

```sh
pnpm seed:local
```

This creates a fictional sample account, accessible through `/demo-login`, with example-only credentials (`demo@example.com` / `LocalExampleOnly123`). The seed script resets that local account and must never be run against real or production data.

For remote databases, configure `TURSO_DATABASE_URL` and `TURSO_AUTH_TOKEN` through secure server-side environment variables. The `.env.example` file contains placeholders only.

## Validate

```sh
pnpm test
pnpm lint
pnpm typecheck
pnpm build
```

## Scope and limitations

This is a clean-history source snapshot. It does not include the private development repository's commit history, internal discussions, user accounts, or production data. It is not connected to or automatically synchronized with any hosted deployment. The local sample login is not a secure shared public sandbox.

The software is shared for inspection, learning, and contribution, not as a security-audited hosted service. No support, uptime, or ongoing security maintenance is promised.

## License

[MIT](LICENSE). Copyright and third-party notices must be retained.
