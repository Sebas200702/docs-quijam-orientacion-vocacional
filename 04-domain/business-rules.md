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

## Simulación (BR-020…BR-025)

- BR-020: Solo se simulan carreras con `SimulationScript.status = verified`.
- BR-021: La IA solo narra usando la escena actual y sus `groundingFacts`; las consecuencias de las decisiones salen del guion.
- BR-022: Respuesta de la IA con cifras (dinero, %, años) → se descarta y se usa el texto estático más el enlace a la ficha.
- BR-023: Máximo 6 turnos de IA por escena y 280 caracteres por entrada libre; si se excede, solo quedan los botones.
- BR-024: Detección de señal de riesgo → se pausa la simulación y se muestra el protocolo de apoyo (`06-ai/sesgos-y-seguridad-menores.md`). El texto libre del estudiante **no se persiste**: el turno se guarda con `freeText = null` y `aiOutput` = clave del texto fijo, y se registra `safety_events.risk_signal_shown` sin texto.
- BR-025: Pregunta sobre la salud del propio estudiante o de alguien cercano (`personal_health`) → texto fijo de redirección a un profesional o a la línea de emergencias; la IA nunca da diagnósticos, medicamentos ni dosis. El texto libre **no se persiste** (igual que BR-024, con `health_redirect_shown`). Si además hay señal de riesgo, manda BR-024.
- BR-026: El enlace a la ficha (`linkToFicha`) lo construye el servidor con el `slug` de la simulación y una lista blanca de anclas (`#pensum`, `#duracion`, `#costo`, `#salario`, `#empleabilidad`, `#donde-estudiar`). La IA solo puede proponer el tema del dato (`dataKind`); cualquier URL o ruta en su salida se ignora.
- BR-027: La ilustración de cada escena es un archivo estático del contenido curado; nunca se genera en runtime ni la elige la IA.

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

## Panel de ciudad (BR-060…BR-064)

- BR-060: El panel de ciudad solo muestra agregados por sector, grado y periodo. Nunca muestra estudiantes, alias, colegios ni desgloses por colegio.
- BR-061: k-anonimato: una celda con menos de 20 estudiantes se suprime ("Grupo muy pequeño para mostrar"). Si el total del grado y periodo tiene menos de 20 estudiantes, no se muestra nada. (El panel del orientador, P1, usa k ≥ 5 dentro de su colegio.)
- BR-062: Si los datos no salen de estudiantes reales, el payload lleva `dataOrigin: "synthetic"` y la UI muestra "Datos sintéticos de demostración" sin opción de ocultarlo. Una cifra de demanda real solo se muestra con fuente y año (BR-030); si no, queda como `[DATO POR VERIFICAR]`.
- BR-063: La demanda laboral y el panel de ciudad nunca alteran la afinidad, el orden ni la explicación de las recomendaciones del estudiante (BR-010, BR-014).
- BR-064: Con datos reales (piloto), solo cuentan estudiantes con autorización del acudiente y con la finalidad estadística declarada en la política de datos vigente (`08-technical/security.md`).
