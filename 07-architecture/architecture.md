# Arquitectura

## Capas

| Capa | Tecnología | Responsabilidad |
|------|-----------|-----------------|
| Frontend | React + Vite + Tailwind + TypeScript | SPA mobile-first; estado del recorrido; render de `DataBadge` |
| API | Bun + Hono + TypeScript + Zod | Endpoints REST, validación, consentimiento, rate limit |
| Dominio | TypeScript puro | Motor de recomendación, reglas BR, guardas |
| IA | `SimulationProvider` (Gemini más guardas) | Narración, intención, explicaciones; fallback estático y caché según `DEMO_MODE` |
| Contenido | JSON semilla más Zod → PostgreSQL; ilustraciones como archivos estáticos del frontend | Carreras, guiones, DataPoints, eventos, mentores, sectores, agregados sintéticos del panel de ciudad |
| Panel de ciudad | `CityInsightsService` (dominio puro + SQL de agregados) | Agregados por sector con k-anonimato; sin IA |
| Persistencia | PostgreSQL + Drizzle | Recorrido del estudiante, contenido, logs |
| Observabilidad | Logs estructurados sin PII y `ai_turn_log` | Auditoría y depuración de la demo |

Coherente con el stack de la idea 1 (`docs-hackathon`, ADR-006) para reutilizar conocimiento del equipo.

## Diagrama

```
[Navegador móvil]
     │ HTTPS
[Frontend React/Vite] ──► [API Hono]
                              ├─► Domain: matching · rules · guards
                              ├─► SimulationProvider ──► Gemini API
                              │        └─ fallback: staticNarration / cache
                              ├─► ContentRepository (read-only)
                              ├─► CityInsightsService ──► k-anonymity (k ≥ 20)
                              └─► PostgreSQL (Drizzle)
[Ilustraciones /scenes/*] ── archivos estáticos servidos con el frontend (sin servicio de imágenes)
```

## Flujo de un turno de simulación

```
POST /simulations/:id/turns
 → auth + consent check (si persiste)
 → load scene (ContentRepository)
 → prefilter (PII, longitud, riesgo, salud personal)
     └ si marca risk_signal | personal_health → texto fijo, sin llamar a Gemini ─┐
 → SimulationProvider.narrate(scene, choice|text)   [según DEMO_MODE; timeout 8 s] │
 → schema (estricto) + guards                                                  │
     └ si Gemini devuelve risk_signal | personal_health → texto fijo ──────────┤
 → derive linkToFicha (servidor: slug + lista blanca de anclas, BR-026)        │
 → persist SimulationTurn + AiTurnLog  ◄────────────────────────────────────────────┘
     └ en turnos risk_signal | personal_health: free_text = NULL,
       ai_output = clave del texto fijo, source = fixed, + safety_events (sin texto)
 → respuesta { narration, intent, choices, linkToFicha, scene.illustration, source }
```

El texto libre de un turno de riesgo o de salud personal no se escribe en ninguna tabla ni log (BR-024, BR-025, NFR-018). Si la detección viene de Gemini y no del prefiltro, el texto ya se envió al modelo (sin PII, NFR-007), pero tampoco se persiste.

## `DEMO_MODE`

Una sola variable con tres valores (`10-operations/development.md`):

| Valor | Cadena del `SimulationProvider` | Cuándo |
|-------|-------------------------------|--------|
| `off` (por defecto) | Gemini → caché de la demo → estático | Desarrollo y demo con Gemini estable |
| `cache` | Caché de la demo → estático (no llama a Gemini; la intención se clasifica solo con reglas) | Si un ensayo del viernes o la batería bloqueante fallan (`10-operations/contingency.md`) |
| `static` | Solo `staticNarration` y textos fijos | Sin red o caché incompleta |

Las guardas de riesgo y salud personal y el texto fijo aplican en los tres modos. `GET /health` informa el modo activo.

## Decisiones clave

- Recomendación determinista fuera de la IA (ADR-004).
- Contenido curado como única fuente de la IA (ADR-003).
- Consentimiento y conexión moderada (ADR-005).
- Respuestas sin streaming en el fallback; streaming SSE opcional en el camino feliz (si no da tiempo, una respuesta completa con un indicador de "escribiendo…").
