# Desarrollo

## Repositorio de código (separado de estos docs)

Monorepo Bun workspaces:

```
apps/web        React + Vite + Tailwind
apps/api        Hono
packages/contracts   Zod compartido
packages/domain      matching, rules, guards (sin dependencias de I/O)
seed/                contenido JSON
```

## Comandos

```
bun install
docker compose up -d db          # Postgres local
bun run db:migrate
bun run seed                     # valida y carga el contenido
bun run dev                      # web + api
bun test                         # Vitest
bun run ai:eval                  # batería AI-01…AI-15 (usa Gemini real)
bun run lint && bun run typecheck
```

## Variables de entorno

`DATABASE_URL`, `GEMINI_API_KEY`, `GEMINI_MODEL`, `LLM_TIMEOUT_MS=8000`, `LLM_DAILY_TOKEN_CAP`, `SESSION_SECRET`, `ADMIN_KEY`, `DEMO_KEY`, `DEMO_MODE=true|false`, `WEB_ORIGIN`.

Nota de Gemini: `GEMINI_API_KEY` es la llave de Google AI Studio y vive solo en el servidor (nunca en `apps/web`, en el repo ni en los logs). `GEMINI_MODEL` es un modelo de clase Flash; la versión exacta la fija el Arquitecto de IA en el evento.

## Flujo de trabajo en la hackatón

- Rama `main` protegida por convención; ramas cortas `feat/<área>`; merge rápido con revisión de otra persona (2 min).
- Conventional Commits.
- Contratos primero: el backend publica los tipos Zod el jueves a las 15:00 y el frontend los usa con mocks hasta que la API exista.
- El contenido (seed) lo editan UI/UX y el Pitch Lead; `bun run seed` ejecuta el linter de cifras.
- Uso de agentes de IA para generar código: se acepta solo con la prueba del módulo pasando.
