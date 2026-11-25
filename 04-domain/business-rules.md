# Reglas de negocio

## Consentimiento y datos (BR-001…BR-009)

- BR-001: Un estudiante es menor si `año actual − birthYear < 18`. Ante la duda (cumple 18 este año), se trata como menor.
- BR-002: Un menor sin `GuardianConsent.status = granted` puede navegar, hacer el test y simular, pero no se persiste nada (todo queda en la sesión del cliente) ni se envían preguntas ni se comparte el resumen.
- BR-003: Revocar la autorización equivale a borrar los datos (FR-004).
- BR-004: Nunca se almacena género, estrato, etnia, documento ni nombre completo.
- BR-005: El alias, el colegio y cualquier identificador nunca forman parte de un prompt.

## Recomendación (BR-010…BR-014)

- BR-010: La afinidad se calcula de forma determinista (`matching-model.md`). La IA no participa en el cálculo.
- BR-011: Siempre se muestran 3 carreras del top más 1 "fuera de zona" (si el catálogo lo permite).
- BR-012: Las preferencias (duración, modalidad) no excluyen carreras: solo agregan avisos ("Dura más de lo que marcaste").
- BR-013: Toda recomendación lleva al menos 2 razones trazables a respuestas del estudiante.
- BR-014: Ninguna institución puede pagar ni influir para aparecer en las recomendaciones.

## Simulación (BR-020…BR-024)

- BR-020: Solo se simulan carreras con `SimulationScript.status = verified`.
- BR-021: La IA solo narra usando la escena actual y sus `groundingFacts`; las consecuencias de las decisiones salen del guion.
- BR-022: Respuesta de la IA con cifras (dinero, %, años) → se descarta y se usa el texto estático más el enlace a la ficha.
- BR-023: Máximo 6 turnos de IA por escena y 280 caracteres por entrada libre; si se excede, solo quedan los botones.
- BR-024: Detección de señal de riesgo → se pausa la simulación y se muestra el protocolo de apoyo (`06-ai/sesgos-y-seguridad-menores.md`).

## Datos de contraste (BR-030…BR-033)

- BR-030: Un `DataPoint` solo muestra su valor si `status = verified` y tiene `sourceName` y `sourceYear`.
- BR-031: Un dato `draft` se muestra como "Dato por verificar — fuente sugerida: {suggestedSource}".
- BR-032: Si un dato verificado tiene más de 3 años desde `sourceYear`, se muestra con la nota "puede estar desactualizado".
- BR-033: Los costos se muestran como rango por tipo de institución, nunca como precio de una institución concreta, salvo que la institución lo haya validado.

## Conexión (BR-040…BR-045)

- BR-040: No existe mensajería privada entre estudiante y mentor.
- BR-041: Toda pregunta pasa por moderación antes de que la vea un mentor.
- BR-042: El filtro automático rechaza teléfonos, correos, @usuarios, URLs y direcciones con el motivo "No compartas datos de contacto".
- BR-043: Las preguntas y respuestas publicadas son anónimas y visibles para todos los estudiantes de esa carrera.
- BR-044: Los mentores solo se publican si los verifica una institución aliada (en el MVP: perfiles de ejemplo rotulados).
- BR-045: Los eventos muestran el enlace oficial de inscripción; Rumbo no gestiona inscripciones.

## Decisión y compartir (BR-050…BR-053)

- BR-050: "Mi decisión" nunca se prellena ni se sugiere.
- BR-051: La decisión es histórica: cada cambio crea un registro nuevo.
- BR-052: El enlace de resumen expira a los 7 días y se puede revocar.
- BR-053: El resumen no incluye las respuestas ítem por ítem ni el colegio.
