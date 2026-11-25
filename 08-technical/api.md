# API

Base: `/api/v1`. JSON. Errores según `contracts.md`. 🔒 = requiere sesión; ✍ = requiere consentimiento si el estudiante es menor (BR-002).

## Resumen

| Método | Ruta | Auth | FR |
|--------|------|------|----|
| GET | `/health` | — | — |
| POST | `/demo/login` | — | FR-005 |
| POST | `/demo/reset` | clave demo | FR-005 |
| POST | `/students` | — | FR-002 |
| GET | `/me` | 🔒 | — |
| DELETE | `/me` | 🔒 | FR-004 |
| POST | `/me/consent` | 🔒 | FR-003 |
| POST | `/me/consent/simulate-grant` | 🔒 (solo demo) | FR-003 |
| GET | `/assessment/items` | — | FR-020 |
| POST | `/assessments` | 🔒 (persiste solo con ✍) | FR-020…FR-024 |
| GET | `/careers` | — | FR-030 |
| GET | `/careers/:slug` | — | FR-031, FR-050…FR-054 |
| POST | `/simulations` | 🔒 | FR-040 |
| POST | `/simulations/:id/turns` | 🔒 | FR-041…FR-045 |
| POST | `/simulations/:id/reflection` | 🔒 ✍ | FR-044 |
| GET | `/events?career=&from=` | — | FR-060 |
| POST | `/events/:id/interest` | 🔒 ✍ | FR-061 |
| GET | `/careers/:slug/mentors` | — | FR-062 |
| GET | `/careers/:slug/questions` | — | FR-063 |
| POST | `/questions` | 🔒 ✍ | FR-063, FR-064 |
| GET | `/journal` | 🔒 | FR-070 |
| GET | `/journal/compare?careers=a,b` | 🔒 | FR-071 |
| POST | `/decisions` | 🔒 ✍ | FR-072 |
| POST | `/share-links` | 🔒 ✍ | FR-073 |
| GET | `/share/:token` | — | FR-073 |
| GET | `/admin/questions?status=pending` | clave admin | FR-092 |
| POST | `/admin/questions/:id/moderate` | clave admin | FR-092 |

## Ejemplos

### POST /students
```json
// request
{ "alias": "Vale", "grade": 11, "birthYear": 2010, "schoolId": null,
  "interests": ["cuidar personas", "ciencias"], "favoriteSubjects": ["biología", "química"],
  "preferences": { "maxDuration": "any", "modality": "presencial", "wantsFinancing": true } }
// 201
{ "id": "7b1e…", "alias": "Vale", "isMinor": true, "consent": { "status": "pending" } }
```

### POST /me/consent
```json
// request
{ "guardianContact": "acudiente@example.com", "studentAssent": true, "policyVersion": "2026-11-v1" }
// 202
{ "status": "pending", "method": "demo", "message": "Solicitud enviada (simulada en demo)." }
```

### POST /assessments
```json
// request
{ "answers": { "R1": 2, "R2": 1, "I1": 4, "I2": 3, "S1": 4, "...": 0 } }
// 201
{
  "assessmentId": "a91c…",
  "persisted": true,
  "profile": { "R": 0.33, "I": 0.75, "A": 0.25, "S": 1.0, "E": 0.42, "C": 0.58 },
  "recommendations": [
    { "rank": 1, "careerId": "enfermeria", "affinity": 98,
      "reasons": [ { "dimension": "S", "itemId": "S1", "answer": 4 },
                   { "dimension": "I", "itemId": "I1", "answer": 4 } ],
      "explanation": "Te la mostramos porque te interesa Ayudar e Investigar…" },
    { "rank": 2, "careerId": "derecho", "affinity": 87, "reasons": [ … ] },
    { "rank": 3, "careerId": "ingenieria-sistemas", "affinity": 82, "reasons": [ … ] },
    { "rank": "out_of_zone", "careerId": "tecnologia-gestion-logistica", "affinity": 79, "reasons": [ … ] }
  ],
  "disclaimer": "Esto es para explorar, no un diagnóstico. Tú decides."
}
```

### GET /careers/enfermeria (extracto)
```json
{
  "id": "enfermeria", "name": "Enfermería", "level": "profesional", "area": "salud",
  "summary": "Cuidas la salud de las personas…",
  "dataPoints": [
    { "kind": "salario_enganche", "status": "draft", "value": null,
      "display": "Dato por verificar — fuente sugerida: Observatorio Laboral para la Educación" },
    { "kind": "vinculacion", "status": "verified", "value": "<valor consultado>", "unit": "%",
      "sourceName": "Observatorio Laboral para la Educación", "sourceYear": "<año>", "stale": false }
  ],
  "myths": [ { "myth": "…", "reality": "…" } ],
  "studyOptions": [ { "institution": "…", "level": "profesional", "modality": "presencial" } ],
  "hasAiSimulation": true
}
```
Nota: `<valor consultado>` y `<año>` se llenan desde la fuente; ningún valor de ejemplo en esta documentación es un dato.

### POST /simulations
```json
// request
{ "careerId": "enfermeria" }
// 201
{ "simulationId": "s-42", "scene": { "order": 1, "timeLabel": "6:00 a. m.", "setting": "Urgencias",
  "narration": "Llegas al puesto de enfermería…", "choices": [
    { "id": "c1", "label": "Revisar primero al paciente más grave" },
    { "id": "c2", "label": "Leer todas las notas antes de moverte" },
    { "id": "c3", "label": "Preguntarle a la compañera saliente" } ] },
  "totalScenes": 4, "source": "llm" }
```

### POST /simulations/:id/turns
```json
// request (decisión)
{ "choiceId": "c1" }
// request (pregunta libre)
{ "freeText": "¿y cuánto gana una enfermera?" }
// 200 (pregunta de cifra)
{ "narration": "Buena pregunta. Ese dato lo tenemos con su fuente en la ficha.",
  "intent": "data_request", "linkToFicha": "/carreras/enfermeria/contrastar#salario",
  "scene": { "order": 1 }, "source": "llm", "guardFlags": [] }
// 200 (avance de escena)
{ "narration": "Revisas a don Ernesto…", "intent": "story",
  "nextScene": { "order": 2, "timeLabel": "9:30 a. m.", "choices": [ … ] }, "source": "static",
  "guardFlags": ["numbers_detected"] }
```

### POST /simulations/:id/reflection
```json
{ "fitScore": 4, "liked": ["ayudar", "el equipo"], "disliked": ["los horarios"], "note": "Me dio nervios la parte del medicamento" }
// 201 { "ok": true }
```

### POST /questions
```json
// request
{ "careerId": "enfermeria", "mentorId": "m-enf-1", "text": "¿Cómo manejas los turnos de noche?" }
// 202
{ "id": "q-9", "status": "pending" }
// 422 (contacto detectado)
{ "error": { "code": "CONTACT_INFO_DETECTED", "message": "No compartas datos de contacto." } }
```

### POST /decisions
```json
{ "careerId": null, "confidence": 3, "why": "Me gusta cuidar gente, pero quiero ver más de Sistemas antes de decidir." }
// 201 { "id": "d-3", "createdAt": "2026-11-27T10:12:00-05:00" }
```

### POST /share-links
```json
{ "includeDecision": true }
// 201 { "url": "https://<host>/r/9f3a…", "expiresAt": "2026-12-04T10:15:00-05:00" }
```

### POST /admin/questions/:id/moderate
```json
{ "action": "approve" }            // o { "action": "reject", "reason": "Fuera de tema" }
{ "action": "answer", "answer": "…" } // demo: el equipo carga la respuesta del mentor de ejemplo
```

### GET /health
```json
{ "status": "ok", "db": "ok", "llm": "ok | degraded", "contentVersion": "2026-11-26.1" }
```
