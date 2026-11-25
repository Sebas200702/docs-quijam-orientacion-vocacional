# Arquitectura

## Capas

| Capa | Tecnología | Responsabilidad |
|------|-----------|-----------------|
| Frontend | React + Vite + Tailwind + TypeScript | SPA mobile-first; estado del recorrido; render de `DataBadge` |
| API | Bun + Hono + TypeScript + Zod | Endpoints REST, validación, consentimiento, rate limit |
| Dominio | TypeScript puro | Motor de recomendación, reglas BR, guardas |
| IA | `SimulationProvider` (LLM más guardas) | Narración, intención, explicaciones; fallback estático y caché |
| Contenido | JSON semilla más Zod → PostgreSQL | Carreras, guiones, DataPoints, eventos, mentores |
| Persistencia | PostgreSQL + Drizzle | Recorrido del estudiante, contenido, logs |
| Observabilidad | Logs estructurados sin PII y `ai_turn_log` | Auditoría y depuración de la demo |

Coherente con el stack de la idea 1 (`docs-hackathon`, ADR-006) para reutilizar conocimiento del equipo.

## Diagrama

```
[Navegador móvil]
     │ HTTPS
[Frontend React/Vite] ──► [API Hono]
                              ├─► Domain: matching · rules · guards
                              ├─► SimulationProvider ──► LLM API
                              │        └─ fallback: staticNarration / cache
                              ├─► ContentRepository (read-only)
                              └─► PostgreSQL (Drizzle)
```

## Flujo de un turno de simulación

```
POST /simulations/:id/turns
 → auth + consent check (si persiste)
 → load scene (ContentRepository)
 → prefilter (PII, longitud, riesgo)
 → SimulationProvider.narrate(scene, choice|text)   [timeout 8 s]
 → schema + guards
 → persist SimulationTurn + AiTurnLog
 → respuesta { narration, intent, choices, linkToFicha, source }
```

## Decisiones clave

- Recomendación determinista fuera de la IA (ADR-004).
- Contenido curado como única fuente de la IA (ADR-003).
- Consentimiento y conexión moderada (ADR-005).
- Respuestas sin streaming en el fallback; streaming SSE opcional en el camino feliz (si no da tiempo, una respuesta completa con un indicador de "escribiendo…").
