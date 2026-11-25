# Plan de construcción sobre la agenda oficial

> Roles: los 5 oficiales se usan solo como etiqueta formal. El reparto real del equipo está en [`roles-equipo.md`](./roles-equipo.md) y la estrategia en [`estrategia-para-ganar.md`](./estrategia-para-ganar.md).

## Supuestos

- Ventana de construcción efectiva: jue 14:00 → vie 09:30 (≈19 h 30 min de reloj, con la noche de construcción). Antes de las 14:00 la agenda tiene reto, ideación e impulso técnico.
- Hitos del día 2, iguales a `estrategia-para-ganar.md` §4–§5: **video de respaldo listo antes de las 07:00**, **congelamiento de código a las 08:30** y **≥5 ensayos cronometrados** (2 la noche del día 1 y 3 la mañana del día 2).
- Antes del evento solo preparamos documentación, guiones de contenido en borrador y la verificación de fuentes. Hay que confirmar con la organización si se permite código previo (plantilla de repo, configuración). Si no se permite, todo el código arranca el jueves.
- Se usan agentes de IA para acelerar (código, contenido en borrador). Todo contenido generado lo revisa una persona antes de marcarse `verified` (`10-operations/curacion-contenido.md`).

## Roles (los 5 obligatorios)

| Rol | Dueño de | Entregable clave |
|-----|----------|------------------|
| **Frontend** | App React mobile-first: onboarding, test, simulación (texto con escena ilustrada), ficha, agenda, bitácora, panel de ciudad | Flujo de demo navegable de punta a punta |
| **Backend** | API Hono, Postgres/Drizzle, seed, motor de recomendación determinista, consentimiento, moderación, panel de ciudad (seed sintético y k-anonimato) | Endpoints de `08-technical/api.md` P0, seed cargado, `/health` |
| **AI Specialist** | Motor de simulación (prompts, guion, grounding, guardas), explicaciones del test, fallback estático, pruebas AI-01…AI-16 | Simulación de 2 carreras estable y una que no invente cifras |
| **UI/UX Designer** | Flujos, componentes, tono para 15–17 años, accesibilidad, guiones de escenas con el AI Specialist, ilustraciones estáticas por escena | Figma/maqueta + guiones e ilustraciones de 4 escenas por carrera |
| **Pitch Lead** | Narrativa, verificación de datos con fuentes oficiales, contenido de las fichas, demo y preguntas del jurado | Fichas con fuente, demo ensayada ≥5 veces, respuestas |

## Jueves 26

| Hora oficial | Bloque | Frontend | Backend | AI Specialist | UI/UX | Pitch Lead |
|---|---|---|---|---|---|---|
| 08:00 Registro / 08:30 Apertura | — | Entorno listo | Entorno listo | Llaves de API probadas | — | Confirmar duración del pitch y las reglas sobre código previo |
| 09:00 Conformación de equipos | — | Confirmar roles | | | | |
| 09:45 Comprender el reto | Validar el encaje con el eje | Escuchan | Escuchan | Escuchan | Escuchan | Toma nota de los criterios del jurado; ajusta `reto-y-alineacion.md` |
| 11:00 Ideación | Congelar alcance | Revisa P0 | Congela el modelo de datos | Congela el formato del guion de escenas | Wireframes de 6 pantallas | Confirma las 4 carreras (Sistemas y Medicina con simulación de IA) |
| 12:30 Almuerzo | | | | | | |
| 13:30 Impulso técnico | Preguntas a mentores técnicos | | Consulta sobre el despliegue | Consulta sobre cuotas de la Gemini API (nivel gratuito) | | |
| 14:00–16:00 Construcción | Esqueleto | Rutas, layout, onboarding | Esquema, migración, seed vacío, `/health`, deploy inicial | Prompt de simulación v1 con 1 carrera | Componentes base, paleta y estilo de las ilustraciones | Ficha de Medicina con fuentes |
| 16:00–18:00 | Primer loop | Test y resultados | `POST /assessments`, motor de recomendación | Explicación del test (IA + plantilla) | Pantalla de simulación | Fichas restantes; guion de demo v1 |
| **18:00 Punto de control** | Demo interna | Mostrar: onboarding → test → top 3 | | | | Cronometrar |
| 18:30–22:00 Noche | Vivir + Contrastar | Simulación con ilustración por escena, ficha | `POST /simulations`, turnos, guardas | Grounding, rechazo de cifras, fallback estático | Ilustraciones de las 8 escenas (pregeneradas, archivos estáticos) | Verificación de datos, mitos y realidades |
| 22:00–01:00 | Conectar + Decidir + Ciudad | Agenda, mentores, bitácora, comparador | Eventos, preguntas moderadas, bitácora, resumen, `GET /city/insights` con seed sintético | Pruebas AI-01…AI-16 | Pantalla del panel de ciudad; resumen compartible imprimible | Pitch v2; **ensayos 1 y 2** con cronómetro |
| 01:00–05:00 | Turnos de descanso | Duermen dos personas por turno; siempre queda alguien de backend o de IA despierto (detalle en `roles-equipo.md` §4) | | | | |
| 05:00–07:00 | Estabilizar | Bugs de la demo | Seed de la demo, `POST /demo/reset` | Caché de respuestas de la demo | Accesibilidad y textos | **Video de respaldo grabado antes de las 07:00** |
| 07:00–08:00 | Ensayar | Solo bugs del golden path | | Batería bloqueante de IA | | **Ensayo 3** |

## Viernes 27

| Hora oficial | Bloque | Todo el equipo |
|---|---|---|
| 08:00 Construcción final | **Congelamiento de código a las 08:30** | Antes de las 08:30, solo arreglos del golden path. Después, nada nuevo: desplegar, correr el checklist de `10-operations/deployment.md` y decidir `DEMO_MODE` (`10-operations/contingency.md`). **Ensayo 4.** |
| 09:30 Revisión técnica | | Backend y AI Specialist explican la arquitectura y los límites de la IA. **Ensayo 5** antes de las 10:00. |
| 10:00 Día de demostraciones | | Pitch Lead presenta, Frontend maneja la pantalla y los demás responden preguntas por área. |
| 12:30 Evaluación | | Tener a mano `preguntas-jurado.md` y la tabla de lo real frente a lo simulado. |

## Puntos de corte (si vamos atrasados)

1. 18:00: si el test no funciona, se usa un perfil precalculado y todo el esfuerzo va a la simulación.
2. 01:00: si la simulación con Gemini no es estable, la demo usa el guion estático y la IA solo responde preguntas libres.
3. 01:00: si el panel de ciudad no está, se cierra la demo con una captura del diseño rotulada "datos sintéticos" y la narración del panel.
4. 05:00: si Conectar no está, se muestra la agenda como lista estática del seed.
5. 08:30: congelamiento. Lo que no funciona sale del guion.
