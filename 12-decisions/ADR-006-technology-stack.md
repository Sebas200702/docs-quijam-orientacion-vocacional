# ADR-006 — Stack

## Estado
Aceptada (2026-11-24).

## Contexto
Equipo de 5 personas, unas 19,5 h de construcción. La idea 1 (`docs-hackathon`, ADR-006) ya definió un stack conocido por el equipo; reutilizarlo reduce el riesgo y permite cambiar de idea sin cambiar de herramientas.

## Decisión
- **Frontend:** React + Vite + Tailwind + TypeScript; TanStack Query.
- **Backend:** Bun + Hono + TypeScript; Zod para los contratos compartidos.
- **Datos:** PostgreSQL + Drizzle.
- **IA:** interfaz `SimulationProvider` con implementaciones LLM, caché y estática. Modelo por defecto: Claude Sonnet 5.5 (`claude-sonnet-5-5`) para la narración y Claude Haiku 5.5 (`claude-haiku-5-5`) para la clasificación de intención y como respaldo por latencia; configurable por `LLM_MODEL`. Elegir según la disponibilidad de créditos del equipo.
- **Tests:** Vitest.
- **Despliegue:** Docker + Dokploy en VPS; Vercel como alternativa para el frontend.

## Alternativas consideradas
- Astro + React (stack general del equipo): mejor para sitios con contenido, pero la idea 1 ya usa SPA + Hono y la app es interactiva; se puede migrar después.
- Un no-code o low-code para la demo: más rápido para pantallas, pero no permite las guardas de IA ni las reglas de consentimiento reales.

## Consecuencias
- Contratos Zod compartidos entre web y api.
- Si el proveedor de LLM falla, el producto sigue funcionando con el fallback estático (NFR-010).
