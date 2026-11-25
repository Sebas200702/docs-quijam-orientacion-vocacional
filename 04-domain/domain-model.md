# Modelo de dominio

## Entidades principales

### Student
| Campo | Tipo | Nota |
|-------|------|------|
| id | uuid | |
| alias | text (2–30) | Nunca se envía al LLM |
| grade | enum `10` \| `11` | |
| birthYear | int | Para determinar si es menor |
| schoolId | uuid? | Opcional |
| interests | text[] (máx. 5) | Chips del onboarding |
| favoriteSubjects | text[] (máx. 3) | |
| preferences | jsonb | `{maxDuration, modality, wantsFinancing}` |
| isDemo | bool | |
| createdAt, lastActiveAt | timestamptz | Retención (NFR-015) |

### GuardianConsent
`id, studentId, guardianContactHash (sha256), status (pending|granted|revoked), method (demo|email|sms), grantedAt, revokedAt, policyVersion`

### School
`id, name, type (oficial|privado), city` — catálogo cerrado.

### Career
`id (slug), name, area (salud|tecnologia|sociales|ingenieria|negocios|artes|logistica), level (tecnico|tecnologo|profesional), durationLabel, riasecProfile {R,I,A,S,E,C} (0–1), sectorId, summary, status (draft|verified), contentVersion`

### CurriculumBlock
`id, careerId, cycle ("1–4", "5–8"), areaTags[], highlights[], surprising[]`

### DataPoint (cifra con fuente)
| Campo | Tipo | Nota |
|-------|------|------|
| id | uuid | |
| careerId | text | |
| kind | enum `salario_enganche` \| `vinculacion` \| `duracion` \| `costo_semestre` \| `otro` | |
| value | numeric? | Null si está en `draft` |
| unit | text | `COP/mes`, `%`, `semestres` |
| segment | text? | `publica`, `privada`, `sena` |
| sourceName | text | "Observatorio Laboral para la Educación" |
| sourceUrl | text? | |
| sourceYear | int? | |
| suggestedSource | text | Para mostrar en "por verificar" |
| status | enum `draft` \| `verified` | |
| verifiedBy, verifiedAt | text, date | |

### MythReality
`id, careerId, myth, reality, dataPointId?`

### StudyOption
`id, careerId, institutionId, programName, level, modality, sniesCode?, status`

### Institution
`id, name, type (universidad|sena|institucion_tecnica), city, isQuiJamAlly`

### SimulationScript / SimulationScene
- Script: `id, careerId, protagonist {name, role, place}, version, status`
- Script: `genericIllustration {src, alt}` — respaldo si una escena no tiene ilustración.
- Scene: `id, scriptId, order (1–4), timeLabel, setting, situation, choices[{id, label, consequence, trait}], groundingFacts[], staticNarration, illustration {src, alt}` — `src` es un archivo estático de `apps/web/public/scenes/` (BR-027).

### Assessment
`id, studentId, answers jsonb ({itemId: 1–4}), profile {R..C}, createdAt, modelVersion`

### Recommendation
`id, assessmentId, careerId, rank (1–3 | 'out_of_zone'), affinity (0–100), reasons jsonb [{dimension, itemId, answer}]`

### Simulation
`id, studentId, careerId, scriptVersion, currentScene, status (active|completed|abandoned), startedAt, completedAt`

### SimulationTurn
`id, simulationId, sceneOrder, choiceId?, freeText? (máx. 280), aiOutput, source (llm|static|cache|fixed), guardFlags[], latencyMs`

Invariante: si `guardFlags` contiene `risk_signal` o `personal_health`, `freeText` es `null` y `aiOutput` guarda solo la clave del texto fijo (`fixed:risk_support.v1`, `fixed:health_redirect.v1`) (BR-024, BR-025).

### Reflection
`id, simulationId, fitScore (1–5), liked[], disliked[], note?`

### Event
`id, institutionId, title, type (puertas_abiertas|descubre|feria|charla|taller), careerIds[], startsAt, endsAt, location, isVirtual, cost (gratis|pago), officialUrl, isSample`

### EventInterest
`studentId, eventId, createdAt`

### Mentor
`id, firstName, role, careerId, verifiedByInstitutionId, bio, isSample` — sin datos de contacto almacenados en el modelo visible.

### MentorQuestion
`id, studentId?, careerId, mentorId?, text, status (pending|approved|rejected|answered), rejectReason?, answer?, answeredAt` — `studentId` se anula al publicar o al borrar.

### Decision
`id, studentId, careerId? (null = "aún no sé"), confidence (1–5), why, createdAt` — histórico (una por cambio).

### ShareLink
`id, studentId, tokenHash, includesDecision, expiresAt, revokedAt`

### AiTurnLog (auditoría, sin PII)
`id, simulationTurnId, promptVersion, model, inputTokens, outputTokens, guardResults jsonb, createdAt`

### Sector (panel de ciudad)
`id (slug: puerto-logistica | tecnologia | salud | servicios-juridicos | otros), name, isStrategic, strategicSource` — `isStrategic` con fuente `[DATO POR VERIFICAR — fuente sugerida: Plan de Desarrollo Distrital / Cámara de Comercio de Barranquilla]`.

### LaborDemandPoint
`id, sectorId, period, demandIndex (0–1)?, sourceName, sourceYear?, suggestedSource, status (draft|verified), dataOrigin (synthetic|official)` — misma regla de visibilidad que `DataPoint` (BR-030).

### CityInsightCell (agregado, nunca por estudiante)
`period, grade (10|11|all), sectorId, studentsCounted, studentsInSector, interestShare, suppressed, dataOrigin (synthetic|real)` — en la demo se carga desde el seed sintético; en el piloto, una vista SQL sobre `decisions` y `reflections` de estudiantes con autorización (BR-064).

## Relaciones

```
Student 1─1 GuardianConsent
Student 1─* Assessment 1─* Recommendation *─1 Career
Student 1─* Simulation 1─* SimulationTurn ; Simulation 1─1 Reflection
Career 1─1 SimulationScript 1─4 SimulationScene
Career 1─* CurriculumBlock, DataPoint, MythReality, StudyOption, Mentor
Event *─* Career ; Student *─* Event (EventInterest)
Student 1─* MentorQuestion *─1 Career
Student 1─* Decision ; Student 1─* ShareLink
Sector 1─* Career ; Sector 1─* LaborDemandPoint ; Sector 1─* CityInsightCell
```

## Agregados

- **Contenido de carrera** (Career + Curriculum + DataPoint + Myth + StudyOption + Script): de solo lectura en runtime; se carga desde el seed.
- **Recorrido del estudiante** (Assessment, Simulation, Reflection, EventInterest, MentorQuestion, Decision): la bitácora es una vista sobre este agregado.
- **Panel de ciudad** (Sector, LaborDemandPoint, CityInsightCell): de solo lectura; nunca expone ni guarda referencias a estudiantes.
