# Simulación "un día en la carrera" con IA

## Idea

El estudiante vive cuatro momentos de un día profesional como protagonista. No es un chat libre: es un **guion curado** (escenas, decisiones y consecuencias) que la IA narra y adapta a lo que el estudiante elige o pregunta. Así es vivo y a la vez controlado.

## Estructura de un guion

- **Protagonista:** nombre, rol y lugar (por ejemplo, "Julián, médico general de urgencias en una clínica de Barranquilla"). No se nombra un hospital ni una empresa real.
- **4 escenas** que cubren: rutina, reto técnico, lado humano o difícil, y cierre o crecimiento.
- **Por escena:** `timeLabel`, `setting`, `situation`, 2–3 `choices` (cada una con su `consequence` y el `trait` que revela), `groundingFacts` (3–6 hechos cualitativos que la IA puede usar), `staticNarration` (fallback completo) e `illustration` (archivo estático con `alt`).

## Presentación: texto con escenas ilustradas (P0) y voz opcional (P1)

Decisión del equipo (2026-11-24): "Texto con escenas ilustradas + voz opcional".

- **P0, base de la demo:** cada escena muestra una ilustración estática y la narración en texto. Son 8 ilustraciones (4 de Sistemas y 4 de Medicina) más una genérica por carrera.
- **Las ilustraciones se preparan antes**, no en vivo: se pueden pregenerar con IA, una persona las revisa (diversidad, sin marcas ni lugares reales, sin escenas clínicas explícitas) y se sirven como archivos estáticos desde `apps/web/public/scenes/`. Ningún paso del golden path depende de un servicio de generación de imágenes (FR-048, BR-027).
- **La ilustración no cambia con el fallback:** si Gemini falla, cambia solo la fuente del texto (`static` o `cache`).
- **P1, solo si el P0 está verde:** voz del profesional virtual con Gemini Live (FR-049), apagada por defecto y con el texto siempre en pantalla. Si falla, la escena sigue en texto. El guion de demo no la necesita.

## Por qué Ingeniería de Sistemas y Medicina

Solo dos carreras tienen simulación completa con IA en el MVP; Derecho y Tecnología en Gestión Logística tienen ficha, info realista y guion estático (IA en P1). Decisión del equipo: "hagámoslo con la carrera que todos dominamos que sería ingeniería de sistema pero también llévemonos a otro extremo ... medicina".

- **Ingeniería de Sistemas, la que conocemos a fondo.** Todo el equipo la vive: el guion sale realista y fácil de curar en pocas horas.
- **Medicina, el otro extremo.** Está lejos de la tecnología, es una de las carreras que más sueñan los estudiantes de 10 y 11 y es de las que más cuesta en tiempo y dinero si no era lo que se pensaba. Si Rumbo funciona con Medicina, el jurado ve que el formato sirve para cualquier carrera, no solo para la nuestra.

## Guion de ejemplo — Medicina (P0, demo)

Protagonista: **Julián, médico general del servicio de urgencias** de una clínica de Barranquilla (ficticia). Lo acompañan Samuel, interno de último año, y la doctora Peña, internista de turno. Se reparten los géneros para no repetir jerarquías por género (`06-ai/sesgos-y-seguridad-menores.md`).

| # | Hora | Situación | Decisiones (rasgo que revela) |
|---|------|-----------|-------------------------------|
| 1 | 7:00 a. m. | **Triage en urgencias.** Recibes el turno y llegan tres pacientes casi al tiempo: don Ernesto, con dolor en el pecho; una niña con fiebre que llora en brazos de su papá; una señora con una cortada en la mano. | Ver primero a quien el triage marcó como más urgente (priorizar) · Leer rápido las notas del turno de la noche antes de moverte (organizar) · Ir con don Ernesto y pedirle a Samuel que tome los datos de los otros dos (trabajo en equipo) |
| 2 | 10:30 a. m. | **Ronda y consulta.** En la ronda con Samuel encuentras a una señora con diabetes que vuelve por tercera vez en el mes. No sigue el tratamiento: dice que no entiende las indicaciones y que no le alcanza para ir hasta la farmacia. | Explicarle con palabras sencillas y pedir apoyo a trabajo social (empatía + recursividad) · Revisar con Samuel la historia clínica para entender qué falló (rigor + enseñar) |
| 3 | 2:00 p. m. | **Una noticia difícil.** La familia de don Ernesto pregunta en el pasillo. Tienes que decirles que se queda hospitalizado, que hay que esperar exámenes y que todavía no hay certezas. | Buscar un lugar tranquilo y explicarlo sin tecnicismos (comunicación) · Pedir que la doctora Peña te acompañe (prudencia + trabajo en equipo) · Primero escuchar qué entendieron y qué temen (escucha) |
| 4 | 7:00 p. m. | **Cierre del turno.** Te quedan dos historias clínicas por completar y un paciente esperando resultados. Tu relevo ya llegó. | Entregar paciente por paciente con detalle (rigor) · Terminar las notas antes de irte aunque salgas tarde (compromiso) |

`groundingFacts` (escena 1): "El triage ordena a los pacientes por gravedad, no por orden de llegada", "En urgencias el médico general trabaja con enfermería, auxiliares, especialistas y familias", "Los turnos pueden ser de día, de noche, fines de semana o festivos", "Buena parte del día se va en escuchar, examinar y escribir la historia clínica". Sin cifras.

`groundingFacts` (escena 3): "Dar malas noticias se aprende y se practica durante la carrera", "Se explica en lenguaje sencillo, en un lugar privado y dejando espacio para preguntas", "Cuando no hay certezas se dice con honestidad". Sin cifras.

### Seguridad del guion de Medicina

- **Todos los casos son ficticios y educativos.** Ningún paciente, clínica ni médico es real.
- **No hay consejo médico.** La narración no nombra medicamentos ni dosis ni da indicaciones de tratamiento; las decisiones del estudiante son de comunicación, prioridad y trabajo en equipo, no clínicas. La consecuencia de cada decisión ya está escrita en el guion.
- **Nada sobre la salud del estudiante.** Si pregunta por su propia salud o la de alguien cercano ("me duele el pecho, ¿qué me tomo?", "¿será que tengo lo mismo?"), la IA no responde el contenido: se clasifica como `personal_health` y se muestra un texto fijo, no generado: "Esto es una simulación educativa y no puedo darte consejos médicos ni decirte qué tienes. Si te sientes mal, cuéntaselo a un adulto de confianza y consulta a un profesional de salud. Si es una emergencia, llama a la línea de emergencias `[DATO POR VERIFICAR — fuente sugerida: Secretaría de Salud de Barranquilla / Ministerio de Salud (Línea 123)]`." Después puede seguir con la simulación (FR-047, AC-15).
- Si la pregunta muestra riesgo (por ejemplo, sobre hacerse daño), manda el protocolo `risk_signal` (F5), que tiene prioridad.

### Ruta real de Medicina (va en la ficha, nunca en la IA)

La simulación no da estos datos; si el estudiante los pide, `intent: data_request` lo lleva a la ficha:

| Dato | Estado |
|------|--------|
| Duración del programa | `[DATO POR VERIFICAR — fuente sugerida: SNIES]` |
| Internado (último año de práctica en hospitales) | Duración y condiciones: `[DATO POR VERIFICAR — fuente sugerida: SNIES / pensum oficial de cada institución]` |
| Servicio Social Obligatorio ("año rural") | Duración, modalidades y exoneraciones: `[DATO POR VERIFICAR — fuente sugerida: Ministerio de Salud]` |
| Costo por semestre (pública / privada) | `[DATO POR VERIFICAR — fuente sugerida: SNIES / sitio oficial de cada institución]` |
| Salario de enganche del médico general | `[DATO POR VERIFICAR — fuente sugerida: Observatorio Laboral para la Educación]` |
| Vinculación laboral | `[DATO POR VERIFICAR — fuente sugerida: Observatorio Laboral para la Educación]` |
| Especialización | Cualitativo: es un estudio aparte, posterior y con cupos limitados; cifras `[DATO POR VERIFICAR — fuente sugerida: SNIES]` |

## Guion de ejemplo — Ingeniería de Sistemas (P0, demo)

Protagonista: **Andrea, desarrolladora** en una empresa de software de Barranquilla (ficticia).

| # | Hora | Situación | Decisiones |
|---|------|-----------|------------|
| 1 | 8:30 a. m. | Reunión diaria de 15 min con tu equipo de una empresa de software de Barranquilla. | Contar en qué te bloqueaste · Decir que todo va bien y resolverlo solo |
| 2 | 10:00 a. m. | Una app de domicilios local falla al pagar. Los usuarios se quejan. | Revisar los registros (logs) del error · Reproducir el error en tu computador |
| 3 | 2:00 p. m. | La clienta no entiende por qué el arreglo toma un día. | Explicarle sin tecnicismos · Mostrarle el problema en pantalla |
| 4 | 5:00 p. m. | Code review: un compañero te señala que tu código es difícil de leer. | Aceptar y reescribir · Defender tu solución con argumentos |

## Contrato de la IA en cada turno

**Entrada a Gemini** (sin PII; modelo de clase Flash, ver ADR-006): prompt de sistema con versión, guion de la carrera, escena actual, decisión elegida o texto libre (280 caracteres como máximo) y las 2 últimas salidas.

**Salida esperada** (JSON validado con Zod):

```json
{
  "narration": "Llegas a urgencias. El médico de la noche te entrega el turno...",
  "intent": "story | question_answered | data_request | off_topic | personal_health | risk_signal",
  "choicesShown": ["c1", "c2", "c3"],
  "dataKind": null
}
```

`dataKind` (`pensum | duracion | costo | salario | empleabilidad | donde_estudiar | null`) solo indica el tema cuando `intent` es `data_request`. **La IA no devuelve enlaces:** el servidor construye `linkToFicha` con el `slug` de la simulación y la lista blanca de anclas (BR-026). Un campo extra como `linkToFicha` o una URL dentro de la narración se descartan (Zod en modo estricto y guarda de URLs).

**Reglas del prompt de sistema** (resumen; texto completo en el repo de código, versionado):

1. Narra en segunda persona, en español neutro con calidez caribeña, en 120 palabras como máximo.
2. Usa solo `situation`, `consequence` y `groundingFacts`. Si te preguntan algo fuera de eso, di que no lo sabes y sugiere preguntarle a un mentor.
3. Nunca des cifras (dinero, porcentajes, años, cantidades de empleo). Si te las piden, usa `intent: data_request` y el `dataKind` del tema. No escribas enlaces ni URLs.
4. No juzgues la decisión como correcta o incorrecta; muestra su consecuencia y lo que revela.
5. No digas al estudiante qué carrera estudiar ni si "sirve" para ella.
6. No asumas el género del estudiante; el protagonista es el personaje del guion.
7. Ante señales de angustia, autolesión, abuso o riesgo, usa `intent: risk_signal` y no continúes la historia.
8. Los casos clínicos son ficticios y educativos: no nombres medicamentos ni dosis ni des indicaciones de tratamiento.
9. Si el estudiante pregunta por su propia salud o la de alguien cercano, usa `intent: personal_health` y no respondas el contenido.

## Guardas posteriores (deterministas, `06-ai/grounding-y-alucinaciones.md`)

Validación del esquema → detector de cifras → detector de URLs → detector de imperativos de decisión ("deberías estudiar") → detector de consejo médico (dosis, "tómate", "te recomiendo tomar") → longitud → derivación de `linkToFicha` en el servidor (BR-026). Si alguna falla, se usa `staticNarration` o la `consequence` del guion. Se registra en `AiTurnLog`.

**Turnos de riesgo o de salud personal:** si el prefiltro o la salida de Gemini marcan `risk_signal` o `personal_health`, se responde con el texto fijo, el turno se guarda con `freeText = null` y `source: fixed`, y solo queda el evento en `safety_events` (BR-024, BR-025).

## Fallback y caché

- **Timeout de 8 s o error** → texto estático (FR-045).
- **Demo:** las respuestas del recorrido exacto de la demo se precalculan y se guardan en caché por `hash(escena, decisión)`; si Gemini falla en el escenario, se sirven desde caché (`source: cache`).
- **`DEMO_MODE`** (`off | cache | static`, definido en `10-operations/development.md`) fija la cadena: `off` = Gemini → caché → estático; `cache` = caché → estático, sin llamar a Gemini; `static` = solo textos del guion. Los textos fijos de riesgo y salud aplican en los tres modos.

## Reflexión final

"¿Te viste haciendo esto?" (1–5) · "Lo que más me gustó" (chips: ayudar, resolver, el ritmo, el equipo, aprender) · "Lo que no me gustó" (chips: la presión, los horarios, la rutina, estar sentado, lidiar con conflictos) · nota opcional. Los rasgos (`trait`) de sus decisiones se muestran como un espejo: "En tus decisiones priorizaste la seguridad y la empatía". Son una observación y no se usan para recalcular la afinidad.

## Producción de guiones

UI/UX y AI Specialist redactan con ayuda de IA y el Pitch Lead revisa. Después del evento, cada guion lo valida un profesional de la carrera (`reviewedBy`). Tiempo estimado de un guion: 1 h de redacción más 30 min de revisión (estimación del equipo).
