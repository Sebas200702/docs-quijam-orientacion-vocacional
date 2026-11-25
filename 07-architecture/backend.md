# Backend

## Estructura

```
api/
  src/
    routes/        auth, students, consent, assessments, careers, simulations,
                   events, mentors, questions, journal, share, demo, health, admin, city
    domain/
      matching/    profile.ts, affinity.ts, explain.ts       (puro, testeado)
      rules/       consent.ts, contact-filter.ts, data-visibility.ts, k-anonymity.ts
      guards/      numbers.ts, urls.ts, entities.ts, imperatives.ts, risk.ts
      ficha-link.ts   (dataKind + slug → ancla de la lista blanca, BR-026)
      city/        insights.ts (interés por sector, brecha; puro, testeado)
    ai/
      simulation-provider.ts   (interfaz)
      llm-provider.ts          (cliente de la Gemini API, prompt versionado)
      static-provider.ts       (fallback)
      cache-provider.ts        (demo)
      prompts/simulation.v1.md
    content/
      loader.ts    (lee seed/*.json, valida con Zod, upsert)
      linter.ts    (rechaza cifras en texto libre)
    db/            schema.ts (Drizzle), migrations/
  seed/            careers/*.json, events.json, mentors.json, assessment-items.json, demo-students.json,
                   sectors.json, city-panel-synthetic.json
```

## Servicios

- **AssessmentService:** valida las 24 respuestas, calcula el perfil y las recomendaciones, y persiste si hay consentimiento.
- **SimulationService:** máquina de estados `active → completed | abandoned`; avanza la escena con la decisión; delega la narración en el `SimulationProvider` (cadena según `DEMO_MODE`: `off` = Gemini → caché → estático; `cache` = caché → estático; `static` = estático); construye `linkToFicha` con `ficha-link.ts`; en turnos `risk_signal`/`personal_health` persiste `free_text = NULL` y el evento de seguridad.
- **CityInsightsService:** lee `city-panel-synthetic.json` (demo) o la vista de agregados (piloto), aplica `k-anonymity` (k ≥ 20) y devuelve `dataOrigin`.
- **CareerService:** compone la ficha aplicando `data-visibility` (BR-030…BR-033).
- **QuestionService:** filtro de contactos → `pending` → moderación → `approved`/`answered`.
- **JournalService:** vista de la bitácora, comparador, decisiones y enlaces para compartir.
- **ConsentService:** estado del acudiente; middleware `requireConsentForWrite`.

## Middleware

`requestId` → `rateLimit` (IP + sesión; los endpoints de IA a 20 req/min por sesión) → `session` → `zodValidator` → handler → `errorHandler` (códigos de `contracts.md`). Las rutas `/city/*` usan `requirePanelKey` (cabecera `X-Panel-Key` = `CITY_PANEL_KEY`) en lugar de la sesión de estudiante.

## Autenticación

MVP: sesión por cookie httpOnly emitida al crear el perfil (sin contraseña) y los perfiles demo con `POST /demo/login`. P2: inicio de sesión con código por correo del acudiente o integración con la cuenta del colegio.
