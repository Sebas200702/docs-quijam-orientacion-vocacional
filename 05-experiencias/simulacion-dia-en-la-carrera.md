# Simulación "un día en la carrera" con IA

## Idea

El estudiante vive cuatro momentos de un día profesional como protagonista. No es un chat libre: es un **guion curado** (escenas, decisiones y consecuencias) que la IA narra y adapta a lo que el estudiante elige o pregunta. Así es vivo y a la vez controlado.

## Estructura de un guion

- **Protagonista:** nombre, rol y lugar (por ejemplo, "Daniela, enfermera de urgencias en un hospital de Barranquilla"). No se nombra un hospital ni una empresa real.
- **4 escenas** que cubren: rutina, reto técnico, lado humano o difícil, y cierre o crecimiento.
- **Por escena:** `timeLabel`, `setting`, `situation`, 2–3 `choices` (cada una con su `consequence` y el `trait` que revela), `groundingFacts` (3–6 hechos cualitativos que la IA puede usar) y `staticNarration` (fallback completo).

## Guion de ejemplo — Enfermería (P0, demo)

| # | Hora | Situación | Decisiones (rasgo que revela) |
|---|------|-----------|-------------------------------|
| 1 | 6:00 a. m. | Entrega de turno en urgencias: recibes 6 pacientes y las notas del turno de la noche. | Revisar primero al paciente más grave (priorizar) · Leer todas las notas antes de moverte (organizar) · Preguntar a la compañera saliente (trabajo en equipo) |
| 2 | 9:30 a. m. | Un adulto mayor tiene que recibir un medicamento, pero la orden médica parece tener un error. | Verificar con el médico antes de aplicarlo (seguridad) · Consultar el protocolo (rigor) |
| 3 | 1:00 p. m. | La hija del paciente está asustada y te pide explicaciones mientras suena otro llamado. | Explicarle con calma en 2 minutos y pedir apoyo (empatía + priorización) · Atender el llamado y volver después (priorización) |
| 4 | 5:30 p. m. | Cierre del turno: registras en la historia clínica y entregas a tu relevo. | Entrega detallada (rigor) · Entrega rápida y quedarte a ayudar (compromiso) |

`groundingFacts` (escena 1): "Los turnos pueden ser de mañana, tarde o noche", "La entrega de turno es un momento clave de seguridad del paciente", "Enfermería coordina con médicos, auxiliares y familias". Sin cifras.

## Guion de ejemplo — Ingeniería de Sistemas (P0, demo)

| # | Hora | Situación | Decisiones |
|---|------|-----------|------------|
| 1 | 8:30 a. m. | Reunión diaria de 15 min con tu equipo de una empresa de software de Barranquilla. | Contar en qué te bloqueaste · Decir que todo va bien y resolverlo solo |
| 2 | 10:00 a. m. | Una app de domicilios local falla al pagar. Los usuarios se quejan. | Revisar los registros (logs) del error · Reproducir el error en tu computador |
| 3 | 2:00 p. m. | La clienta no entiende por qué el arreglo toma un día. | Explicarle sin tecnicismos · Mostrarle el problema en pantalla |
| 4 | 5:00 p. m. | Code review: un compañero te señala que tu código es difícil de leer. | Aceptar y reescribir · Defender tu solución con argumentos |

## Contrato de la IA en cada turno

**Entrada al LLM** (sin PII): prompt de sistema con versión, guion de la carrera, escena actual, decisión elegida o texto libre (280 caracteres como máximo) y las 2 últimas salidas.

**Salida esperada** (JSON validado con Zod):

```json
{
  "narration": "Llegas al puesto de enfermería. La compañera de la noche te entrega...",
  "intent": "story | question_answered | data_request | off_topic | risk_signal",
  "choicesShown": ["c1", "c2", "c3"],
  "linkToFicha": null
}
```

**Reglas del prompt de sistema** (resumen; texto completo en el repo de código, versionado):

1. Narra en segunda persona, en español neutro con calidez caribeña, en 120 palabras como máximo.
2. Usa solo `situation`, `consequence` y `groundingFacts`. Si te preguntan algo fuera de eso, di que no lo sabes y sugiere preguntarle a un mentor.
3. Nunca des cifras (dinero, porcentajes, años, cantidades de empleo). Si te las piden, usa `intent: data_request`.
4. No juzgues la decisión como correcta o incorrecta; muestra su consecuencia y lo que revela.
5. No digas al estudiante qué carrera estudiar ni si "sirve" para ella.
6. No asumas el género del estudiante; el protagonista es el personaje del guion.
7. Ante señales de angustia, autolesión, abuso o riesgo, usa `intent: risk_signal` y no continúes la historia.

## Guardas posteriores (deterministas, `06-ai/grounding-y-alucinaciones.md`)

Validación del esquema → detector de cifras → detector de imperativos de decisión ("deberías estudiar") → longitud. Si alguna falla, se usa `staticNarration` o la `consequence` del guion. Se registra en `AiTurnLog`.

## Fallback y caché

- **Timeout de 8 s o error** → texto estático (FR-045).
- **Demo:** las respuestas del recorrido exacto de la demo se precalculan y se guardan en caché por `hash(escena, decisión)`; si el LLM falla en el escenario, se sirven desde caché (`source: cache`).

## Reflexión final

"¿Te viste haciendo esto?" (1–5) · "Lo que más me gustó" (chips: ayudar, resolver, el ritmo, el equipo, aprender) · "Lo que no me gustó" (chips: la presión, los horarios, la rutina, estar sentado, lidiar con conflictos) · nota opcional. Los rasgos (`trait`) de sus decisiones se muestran como un espejo: "En tus decisiones priorizaste la seguridad y la empatía". Son una observación y no se usan para recalcular la afinidad.

## Producción de guiones

UI/UX y AI Specialist redactan con ayuda de IA y el Pitch Lead revisa. Después del evento, cada guion lo valida un profesional de la carrera (`reviewedBy`). Tiempo estimado de un guion: 1 h de redacción más 30 min de revisión (estimación del equipo).
