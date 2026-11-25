# ADR-006 — Stack

## Estado
Aceptada (2026-11-24).

## Contexto
Equipo de 5 personas, unas 19,5 h de construcción. La idea 1 (`docs-hackathon`, ADR-006) ya definió un stack conocido por el equipo; reutilizarlo reduce el riesgo y permite cambiar de idea sin cambiar de herramientas.

## Decisión
- **Frontend:** React + Vite + Tailwind + TypeScript; TanStack Query.
- **Backend:** Bun + Hono + TypeScript; Zod para los contratos compartidos.
- **Datos:** PostgreSQL + Drizzle.
- **IA:** Gemini vía la **Gemini API**, con llave de Google AI Studio guardada solo en el servidor (`GEMINI_API_KEY`). Un modelo de clase Flash para la narración de la simulación, la clasificación de intención y las explicaciones del test; la versión exacta la fija el Arquitecto de IA en el evento (`GEMINI_MODEL`). Interfaz `SimulationProvider` con implementaciones Gemini, caché y estática: cambiar de proveedor no toca el dominio.
- **Voz (P1/P2, opcional):** Gemini Live API (voz en tiempo real) para el profesional virtual, solo si el P0 está verde.
- **Tests:** Vitest.
- **Despliegue:** Docker + Dokploy en VPS; Vercel como alternativa para el frontend.

## Razón de Gemini
- Es lo más sencillo de aplicar (decisión del equipo, 2026-11-24: "El más sencillo y más fácil de aplicar pues sería Gemini").
- Tiene nivel gratuito: no depende de créditos para la demo.
- Todo el equipo ya lo usó: Sebastián, Gemini Live en Manglara (en producción); Ángel, Gemini API en Alpine-Translate; Esteban, Gemini en UltraCem.
- Es el mismo proveedor de la idea 1 (`docs-hackathon`, ADR-006): una sola llave y una sola curva de aprendizaje.

## Alternativas consideradas
- Otros proveedores de LLM: posibles detrás de `SimulationProvider`, pero exigen créditos y el equipo tiene menos experiencia con ellos.
- Astro + React (stack general del equipo): mejor para sitios con contenido, pero la idea 1 ya usa SPA + Hono y la app es interactiva; se puede migrar después.
- Un no-code o low-code para la demo: más rápido para pantallas, pero no permite las guardas de IA ni las reglas de consentimiento reales.

## Consecuencias
- Contratos Zod compartidos entre web y api.
- Si Gemini falla o se agota la cuota del nivel gratuito, el producto sigue funcionando con caché y fallback estático (NFR-010).
- Revisar los términos de datos de la Gemini API antes de un piloto con menores (`08-technical/security.md`).
