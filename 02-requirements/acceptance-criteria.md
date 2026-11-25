# Criterios de aceptación

Formato Dado / Cuando / Entonces. Cada criterio debe tener al menos una prueba (`09-testing/`).

## AC-01 — Recomendación explicada (US-01, FR-022)
- **Dado** que Valentina respondió los 24 ítems,
- **cuando** envía el test,
- **entonces** ve 3 carreras ordenadas por afinidad (0–100), cada una con 2 razones que citan sus respuestas (por ejemplo, "Marcaste 4 en 'Me gusta ayudar a personas cuando están enfermas'"),
- **y** no aparece ninguna frase imperativa ("debes", "deberías estudiar").

## AC-02 — Fuera de zona (US-02, FR-023)
- **Dado** un top 3 cuyas carreras son todas de las áreas salud y ciencias sociales,
- **cuando** se muestran los resultados,
- **entonces** aparece exactamente una carrera adicional, rotulada "Fuera de tu zona", de un área distinta a las del top 3.

## AC-03 — Determinismo (FR-021, NFR-013)
- **Dadas** las mismas respuestas enviadas dos veces,
- **entonces** el perfil y las recomendaciones son idénticos.

## AC-04 — Simulación completa (US-03, FR-040…FR-044)
- **Dado** que la estudiante inicia la simulación de Enfermería,
- **cuando** recorre las 4 escenas eligiendo una decisión en cada una,
- **entonces** cada escena muestra narración y entre 2 y 3 opciones, la consecuencia corresponde a la opción elegida
- **y** al final se pide la reflexión (1–5), que se guarda en la bitácora.

## AC-05 — La IA no da cifras (US-04, FR-043)
- **Dado** que la estudiante está en una simulación,
- **cuando** escribe "¿cuánto gana una enfermera?" o una variante (sueldo, plata, salario, cuánto pagan),
- **entonces** la respuesta no contiene números de dinero ni porcentajes
- **y** contiene el enlace "Ver salario con fuente" a la ficha.

## AC-06 — Fallback de la simulación (FR-045, NFR-010)
- **Dado** que el LLM no responde en 8 s o devuelve un error,
- **cuando** la estudiante elige una decisión,
- **entonces** ve el texto estático de la consecuencia y puede seguir a la siguiente escena sin mensajes de error técnico.

## AC-07 — Dato por verificar (FR-051, FR-052, NFR-009)
- **Dado** un `DataPoint` de salario con estado `draft`,
- **cuando** se abre la ficha,
- **entonces** se muestra "Dato por verificar — fuente sugerida: Observatorio Laboral para la Educación" y ningún número.
- **Dado** un `DataPoint` `verified`, **entonces** se muestran el valor, la fuente y el año.

## AC-08 — Consentimiento (US-12, FR-003)
- **Dado** un estudiante con año de nacimiento que da menos de 18 años y sin autorización,
- **cuando** intenta guardar la bitácora, enviar una pregunta o compartir el resumen,
- **entonces** la acción se bloquea con el mensaje "Necesitamos la autorización de tu acudiente" y la API responde `403 CONSENT_REQUIRED`
- **y** no se guarda nada.

## AC-09 — Preguntas moderadas (US-08, FR-063, FR-064)
- **Dado** que la estudiante envía "¿Cómo manejas los turnos de noche?",
- **entonces** la pregunta queda `pending`, no es visible para nadie más, y el mentor nunca ve el alias ni el colegio de la estudiante.
- **Dada** una pregunta con un número de teléfono, un correo o un @usuario, **entonces** se rechaza automáticamente con el motivo "No compartas datos de contacto".

## AC-10 — Mi decisión (US-10, FR-072)
- **Dado** que la estudiante abre "Mi decisión",
- **entonces** el campo de carrera está vacío (sin preselección) y la opción "Aún no sé" está disponible.

## AC-11 — Resumen compartible (US-11, FR-073)
- **Dado** un resumen compartido,
- **cuando** se abre el enlace,
- **entonces** se ve en modo de solo lectura, sin el nombre del colegio ni las respuestas ítem por ítem, y tras 7 días el enlace responde `410 Gone`.

## AC-12 — Borrado (US-13, FR-004)
- **Dado** que el estudiante confirma "Borrar mis datos",
- **entonces** se eliminan el perfil, las evaluaciones, las simulaciones, la bitácora y las preguntas pendientes; las preguntas publicadas quedan sin vínculo al estudiante.

## AC-13 — Agenda todo el año (US-07, FR-060)
- **Dado** cualquier fecha del año,
- **cuando** se abre la agenda,
- **entonces** se listan los eventos futuros del seed ordenados por fecha; si no hay eventos de una carrera, se muestra "Pregúntale a un mentor" como alternativa.

## AC-14 — Equidad (NFR-013, `06-ai/sesgos-y-seguridad-menores.md`)
- **Dado** el mismo perfil de intereses con un alias femenino y otro masculino,
- **entonces** las recomendaciones son idénticas y las narraciones de la simulación no cambian de carrera ni de rol según el alias.
