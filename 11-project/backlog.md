# Backlog del MVP

Estimaciones en horas (h) por persona, propias del equipo. Rol: FE, BE, AI, UX, PL.

## P0

| ID | Ítem | Rol | h | FR |
|----|------|-----|---|----|
| B-01 | Monorepo, CI local, Docker Postgres, deploy inicial en Dokploy | BE | 2 | — |
| B-02 | Esquema Drizzle y migraciones | BE | 1,5 | — |
| B-03 | Contratos Zod (`packages/contracts`) | BE | 1 | — |
| B-04 | Loader y linter del seed | BE | 1,5 | FR-090, FR-091 |
| B-05 | Perfil, sesión, consentimiento (simulado), borrado y demo login/reset | BE | 2,5 | FR-002…FR-005 |
| B-06 | Motor de recomendación y explicación con plantilla y tests | BE | 2 | FR-021…FR-023 |
| B-07 | Endpoints de carreras y ficha con data-visibility | BE | 1,5 | FR-030, FR-050…FR-054 |
| B-08 | Eventos, mentores, preguntas, filtro de contactos y moderación | BE | 2,5 | FR-060…FR-064, FR-092 |
| B-09 | Bitácora, comparador, decisiones y enlaces para compartir | BE | 2 | FR-070…FR-073 |
| B-10 | SimulationProvider: LLM, guardas, caché y estático | AI | 4 | FR-040…FR-045 |
| B-11 | Prompt `simulation.v1` y batería AI-01…AI-12 | AI | 3 | — |
| B-12 | Explicación del test con IA más validación | AI | 1 | FR-022 |
| B-13 | Detector de riesgo y protocolo | AI | 1 | BR-024 |
| B-14 | Layout, navegación, onboarding y ConsentGate | FE | 3 | FR-001…FR-011 |
| B-15 | Test y resultados | FE | 2,5 | FR-020…FR-024 |
| B-16 | Simulación (SceneCard, decisiones, texto libre, reflexión) | FE | 3,5 | FR-040…FR-044 |
| B-17 | Ficha con DataBadge | FE | 2 | FR-050…FR-054 |
| B-18 | Conectar (agenda, mentores, preguntas) | FE | 2 | FR-060…FR-064 |
| B-19 | Bitácora, comparador, mi decisión y resumen /r/:token | FE | 3 | FR-070…FR-073 |
| B-20 | Wireframes y sistema visual (tokens, componentes) | UX | 3 | — |
| B-21 | Guiones: Enfermería y Sistemas (4 escenas cada uno, con estático) | UX + AI | 3 | — |
| B-22 | Guiones estáticos: Derecho y Logística | UX | 2 | — |
| B-23 | Ítems del test (24) | UX + PL | 1,5 | FR-020 |
| B-24 | Fichas de las 4 carreras: pensum, mitos, dónde estudiar | PL | 4 | — |
| B-25 | Verificación de cifras en las fuentes oficiales | PL | 3 | NFR-009 |
| B-26 | Seed de eventos (8) y mentores (4) con preguntas y respuestas precargadas | PL | 1 | — |
| B-27 | Pitch, guion de demo, ensayos y video de respaldo | PL | 4 | — |
| B-28 | Revisión de accesibilidad y textos | UX | 1,5 | NFR-004, NFR-005 |

Total P0 por rol (estimado): BE ≈ 16,5 h · AI ≈ 9 h (más B-21 compartido) · FE ≈ 16 h · UX ≈ 6,5 h (más B-21 y B-23 compartidos) · PL ≈ 12 h (más B-23 compartido). Cabe en la ventana de ≈19,5 h si se respetan los descansos por turnos; FE y BE son el camino crítico.

## P1

| ID | Ítem | FR |
|----|------|----|
| B-30 | Simulación con IA para Derecho y Logística | FR-040 |
| B-31 | Panel del orientador (k ≥ 5) | FR-080, FR-081 |
| B-32 | Sesiones grupales y recordatorios | FR-065, FR-066 |
| B-33 | Repetir el test e historial | FR-025 |
| B-34 | Rutas y financiación | FR-055 |
| B-35 | Retomar una simulación | FR-046 |
| B-36 | Streaming SSE de la narración | NFR-003 |
