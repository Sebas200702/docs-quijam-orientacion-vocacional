# Estrategia de testing

Runner: Vitest (Bun). Prioridad: dominio puro y guardas, que son las que protegen al estudiante.

## Unit (obligatorio en el MVP)

| Módulo | Casos |
|--------|-------|
| `matching/profile` | Respuestas → perfil (todo 1 → ceros; todo 4 → unos) |
| `matching/affinity` | Caso de Valentina (`04-domain/matching-model.md`): orden Medicina 98, Derecho 87, Sistemas 82, Logística 79 (fuera de zona); empate → orden alfabético; determinismo (AC-03) |
| `matching/explain` | 2 razones trazables; sin imperativos (AC-01) |
| `guards/numbers` | Detecta "$2.500.000", "2,5 millones", "80 %", "ochenta por ciento", "un salario mínimo"; no marca "escena 2" ni "6:00 a. m." |
| `guards/imperatives` | Detecta "deberías estudiar", "esta carrera es para ti", "no sirves para" |
| `guards/medical-advice` | Detecta "500 mg", "cada 8 horas", "tómate", "te recomiendo tomar", "lo que tienes es"; no marca "triage", "historia clínica" ni "urgencias" |
| `guards/personal-health` | "me duele el pecho, ¿qué me tomo?" y "¿será que tengo lo mismo?" → `personal_health`; "¿qué hace un médico en urgencias?" → no (AC-15) |
| `rules/contact-filter` | Teléfono (300 123 4567), correo, @usuario, URL → rechazo (AC-09) |
| `rules/data-visibility` | `draft` → sin valor (AC-07); `verified` antiguo → `stale` |
| `ficha-link` | `dataKind: salario` + slug `medicina` → `/carreras/medicina/contrastar#salario`; `null` → ficha sin ancla; una salida de Gemini con `linkToFicha: "https://ejemplo.invalid"` o cualquier campo extra falla `SimulationTurnOutput.strict()` → texto estático (BR-026) |
| `guards/urls` | Detecta `http://`, `https://`, `www.` y rutas `/algo` en la narración; no marca "7:00 a. m." |
| `rules/k-anonymity` | Celda con 19 → suprimida; 20 → visible; total del grado menor de 20 → nada visible (AC-17) |
| `city/insights` | Interés por sector desde la carrera preferida (decisión más reciente o mejor `fitScore`); brecha `low_interest`/`high_interest`; la salida no cambia las recomendaciones (BR-063) |
| `rules/consent` | Menor sin consentimiento → bloqueo; regla del cumpleaños (BR-001) |
| `content/linter` | Seed con cifras en el texto libre → falla |

## Integration (API + DB)

- `POST /assessments` con y sin consentimiento (`persisted: false`).
- Ciclo de simulación completo con `StaticProvider` (4 escenas → reflexión).
- `POST /simulations/:id/turns` con un `LlmProvider` mock que devuelve: cifra, JSON inválido, timeout → `source: static` (AC-05, AC-06).
- **Turnos de riesgo y salud personal sin texto libre (SM-11):** con consentimiento, enviar `{ "freeText": "a veces siento que no quiero vivir" }` y `{ "freeText": "me duele el pecho desde ayer, ¿qué me tomo?" }`, y un mock de Gemini que devuelve `intent: risk_signal` para un texto que el prefiltro no detectó. Esperado en los tres: `SELECT free_text FROM simulation_turns WHERE simulation_id = $1 AND guard_flags && ARRAY['risk_signal','personal_health']` devuelve solo `NULL`; `ai_output` es la clave del texto fijo; `source = 'fixed'`; ningún registro de `ai_turn_logs`, `safety_events` ni del log de la API contiene el texto enviado. Un `INSERT` directo que viole el CHECK falla.
- `DEMO_MODE=cache`: ninguna llamada al cliente de Gemini; `DEMO_MODE=static`: todas las respuestas `source: static` o `fixed`; `GET /health` informa el modo.
- `GET /city/insights` sin `X-Panel-Key` → 401; con clave → valida contra `CityInsights`, `dataOrigin: "synthetic"` y `label` presentes (AC-16).
- Payload enviado a la Gemini API sin alias ni colegio (NFR-007).
- `DELETE /me` borra en cascada (AC-12).
- Enlace compartido vencido → 410 (AC-11).
- Acción ✍ sin consentimiento → 403 sin escritura en la BD (AC-08).

## Contrato

- Toda respuesta de `/careers/:slug` valida contra `DataPointView`; no existe un `value` no nulo con `status: draft` (NFR-009).
- Toda respuesta de `/simulations/:id/turns` valida contra `TurnResponse` (enlace solo de la lista blanca).
- Toda escena del seed tiene `illustration.src` bajo `/scenes/` o usa la genérica; ninguna apunta a un dominio externo (FR-048).

## Evaluación de IA

Ver `ai-failures.md`: batería con LLM real, corrida antes de la demo.

## Manual / usabilidad

- Flujo de la demo de punta a punta en un Android real (NFR-001).
- Tres personas externas al equipo completan el loop sin ayuda (si hay jóvenes en el evento, mejor; sin recoger datos personales).
- Ensayo con `GEMINI_API_KEY` inválida (NFR-010).
