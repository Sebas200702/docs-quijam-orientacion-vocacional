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
| `rules/consent` | Menor sin consentimiento → bloqueo; regla del cumpleaños (BR-001) |
| `content/linter` | Seed con cifras en el texto libre → falla |

## Integration (API + DB)

- `POST /assessments` con y sin consentimiento (`persisted: false`).
- Ciclo de simulación completo con `StaticProvider` (4 escenas → reflexión).
- `POST /simulations/:id/turns` con un `LlmProvider` mock que devuelve: cifra, JSON inválido, timeout → `source: static` (AC-05, AC-06).
- Payload enviado a la Gemini API sin alias ni colegio (NFR-007).
- `DELETE /me` borra en cascada (AC-12).
- Enlace compartido vencido → 410 (AC-11).
- Acción ✍ sin consentimiento → 403 sin escritura en la BD (AC-08).

## Contrato

- Toda respuesta de `/careers/:slug` valida contra `DataPointView`; no existe un `value` no nulo con `status: draft` (NFR-009).

## Evaluación de IA

Ver `ai-failures.md`: batería con LLM real, corrida antes de la demo.

## Manual / usabilidad

- Flujo de la demo de punta a punta en un Android real (NFR-001).
- Tres personas externas al equipo completan el loop sin ayuda (si hay jóvenes en el evento, mejor; sin recoger datos personales).
- Ensayo con `GEMINI_API_KEY` inválida (NFR-010).
