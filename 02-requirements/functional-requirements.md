# Requisitos funcionales

Prioridad entre corchetes. Los criterios verificables están en `acceptance-criteria.md`.

## Acceso y consentimiento

- FR-001 [P0]: Permitir explorar el catálogo y las fichas sin cuenta (modo invitado).
- FR-002 [P0]: Crear un perfil con alias, grado (10 u 11), año de nacimiento y colegio (opcional, de una lista). No pedir nombre completo, documento, género, estrato ni etnia.
- FR-003 [P0]: Si el estudiante tiene menos de 18 años, exigir la autorización registrada del acudiente antes de guardar resultados, enviar preguntas a mentores o compartir el resumen. En el MVP el envío al acudiente es simulado.
- FR-004 [P0]: Permitir al estudiante borrar su perfil y todos sus datos con una sola acción confirmada.
- FR-005 [P0]: Ofrecer un modo demo con perfiles semilla y un reinicio (`POST /demo/reset`).

## Onboarding

- FR-010 [P0]: Capturar intereses (selección de etiquetas), materias favoritas y, opcionalmente, preferencias: duración máxima, modalidad y si quiere ver opciones de financiación.
- FR-011 [P0]: Ofrecer dos rutas: "No tengo idea" (va al test) y "Tengo opciones en mente" (va al catálogo).

## Explorar — test vocacional

- FR-020 [P0]: Presentar un test de 24 ítems (4 por dimensión de intereses) con escala de 1 a 4, más el resultado del onboarding.
- FR-021 [P0]: Calcular un perfil de intereses de 6 dimensiones (`04-domain/matching-model.md`).
- FR-022 [P0]: Recomendar las 3 carreras del catálogo con mayor afinidad y mostrar el porqué de cada una (dimensiones y respuestas que más pesaron).
- FR-023 [P0]: Mostrar siempre una carrera "fuera de tu zona", la de mayor afinidad fuera del top 3 que pertenezca a otra área.
- FR-024 [P0]: Mostrar el aviso: "Este test es una herramienta de exploración, no un diagnóstico".
- FR-025 [P1]: Permitir repetir el test y ver el historial de perfiles.

## Catálogo

- FR-030 [P0]: Listar las carreras con área, nivel (técnico, tecnólogo o profesional) y duración, y filtrar por área y nivel.
- FR-031 [P0]: Desde cada carrera, acceder a Vivir, Contrastar y Conectar.

## Vivir — simulación "un día en la carrera"

- FR-040 [P0]: Iniciar la simulación de una carrera con guion curado de 4 escenas.
- FR-041 [P0]: En cada escena, la IA narra en segunda persona y ofrece 2 o 3 decisiones; el estudiante elige o escribe una respuesta libre corta (máximo 280 caracteres).
- FR-042 [P0]: La IA responde a la decisión con la consecuencia indicada en el guion y puede contestar preguntas libres usando solo el contenido de esa carrera.
- FR-043 [P0]: Si el estudiante pregunta por cifras (salario, empleabilidad, costo, duración), la IA no da números y ofrece el enlace a la sección correspondiente de la ficha.
- FR-044 [P0]: Al terminar, pedir una reflexión: "¿Te viste haciendo esto?" (escala de 1 a 5), qué le gustó y qué no.
- FR-045 [P0]: Si el LLM falla o tarda más de 8 s, continuar con el texto estático del guion sin perder el progreso.
- FR-046 [P1]: Retomar una simulación interrumpida.
- FR-047 [P0]: Si el estudiante pregunta por su propia salud o la de alguien cercano, no responder el contenido: mostrar un texto fijo que remite a un profesional de salud o a la línea de emergencias, sin diagnóstico, medicamentos ni dosis (los casos clínicos de la simulación son ficticios y educativos).

## Contrastar — información realista

- FR-050 [P0]: Mostrar el pensum resumido por áreas y por ciclos (por ejemplo, semestres 1 a 4 y 5 a 8).
- FR-051 [P0]: Mostrar salario de enganche, vinculación laboral, duración, costo aproximado por semestre y título otorgado, cada uno con fuente, año y estado.
- FR-052 [P0]: Si un dato no está verificado, mostrar "Dato por verificar" con la fuente sugerida y sin número.
- FR-053 [P0]: Mostrar 3 mitos y realidades por carrera.
- FR-054 [P0]: Listar dónde estudiarla en Barranquilla y el área metropolitana (institución, modalidad y nivel), incluyendo el SENA si aplica.
- FR-055 [P1]: Mostrar rutas de continuidad (técnico → tecnólogo → profesional) y opciones de financiación (por ejemplo ICETEX o becas) solo si el estudiante lo pidió.

## Conectar — profesionales y universidades

- FR-060 [P0]: Mostrar una agenda de eventos (puertas abiertas, Descubre u otros, ferias, charlas SENA) filtrable por carrera y fecha, disponible todo el año.
- FR-061 [P0]: Permitir marcar "me interesa" en un evento; queda en la bitácora.
- FR-062 [P0]: Listar mentores verificados por carrera (nombre de pila, cargo, institución que lo verifica y una frase).
- FR-063 [P0]: Permitir enviar preguntas a un mentor. Las preguntas entran en moderación y solo se publican la pregunta y la respuesta aprobadas, visibles para todos y de forma anónima.
- FR-064 [P0]: No ofrecer chat privado ni intercambio de datos de contacto entre estudiantes y mentores.
- FR-065 [P1]: Solicitar cupo en una sesión grupal con mentores.
- FR-066 [P1]: Recordatorio del evento por correo del acudiente.

## Decidir — bitácora

- FR-070 [P0]: Bitácora con las carreras exploradas, simulaciones completadas, reflexiones, eventos marcados y preguntas enviadas.
- FR-071 [P0]: Comparador lado a lado de 2 o 3 carreras con: afinidad, reflexión de la simulación, duración, costo, salario y vinculación (con sus estados de verificación).
- FR-072 [P0]: "Mi decisión": el estudiante escribe su opción preferida (o "aún no sé"), su nivel de seguridad (1 a 5) y su porqué. El sistema no la prellena.
- FR-073 [P0]: Resumen compartible para el acudiente o el orientador: vista de solo lectura con enlace que expira en 7 días, imprimible.

## Orientador (P1)

- FR-080 [P1]: Panel por colegio con agregados anónimos: estudiantes activos, carreras más exploradas y % de estudiantes con loop completo. Solo muestra grupos de 5 estudiantes o más.
- FR-081 [P1]: El orientador ve el resumen individual solo si el estudiante lo comparte.

## Contenido y moderación

- FR-090 [P0]: Cargar carreras, escenas, fichas, eventos y mentores desde archivos semilla JSON validados.
- FR-091 [P0]: Cada dato tiene estado `draft` o `verified`; en producción no se muestra contenido `draft`, excepto la marca "por verificar".
- FR-092 [P0]: Cola de moderación de preguntas a mentores (aprobar o rechazar con motivo). En el MVP la usa el equipo.
