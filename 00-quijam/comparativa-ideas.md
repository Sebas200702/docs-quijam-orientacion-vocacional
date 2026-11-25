# Comparativa de ideas — QuiJAM 2026

Comparamos las dos ideas del equipo frente al reto oficial para decidir cuál es la **principal** y cuál el **respaldo**:

> "¿Cómo usar tecnología, innovación y talento joven para mejorar la calidad de vida de los ciudadanos de Barranquilla?"

| | Idea 1 | Idea 2 |
|---|---|---|
| Nombre | **Copiloto de Salud Financiera** | **Rumbo** (nombre de trabajo) — Orientación Vocacional |
| Repo | `docs-hackathon` | `docs-quijam-orientacion-vocacional` |
| En una frase | Gestiona tu dinero sin convertirlo en otra tarea | Vive la carrera antes de elegirla |
| Usuario | Universitarios y aprendices SENA con ingresos limitados | Estudiantes de grado 10.º y 11.º de Barranquilla |
| Eje QuiJAM | Economía y oportunidades | Economía y oportunidades + talento joven (y datos para decidir) |

## Matriz de evaluación

La escala va de 1 a 5. Es un **juicio del equipo**, no un dato, y se recalibra con la rúbrica oficial cuando la entreguen el día 1 a las 08:00.

| Criterio probable del jurado | Copiloto | Rumbo | Por qué |
|---|:-:|:-:|---|
| Pertinencia al reto de la Alcaldía | 3 | **5** | El reto pide explícitamente "talento joven". Rumbo actúa justo antes del primer gran paso hacia el empleo; el Copiloto habla de finanzas personales, un ángulo menos directo de ciudad. |
| Impacto en ciudadanos | 3 | **5** | Elegir mal una carrera tiene un costo alto y duradero en tiempo, dinero, deserción y frustración (`[DATO POR VERIFICAR — SPADIES/MEN]`). Rumbo llega a todos los colegios, mientras Descubre llega solo dos veces al año, por 2–3 días. |
| Innovación y efecto sorpresa en la demo | 3 | **5** | Rumbo puede mostrar la "simulación de un día en la carrera" con un profesional virtual, con voz y avatar si da el tiempo. El Copiloto compite con funciones que ya existen en apps como los "bolsillos" de Nequi. |
| Viabilidad y escala con aliados | 3 | **5** | La CUC, que creó Descubre, y la Alcaldía, que maneja los colegios oficiales, son **aliadas de QuiJAM**. Rumbo tiene una ruta de piloto natural; el Copiloto no tiene un aliado tan evidente. |
| Encaje con el equipo | 3 | **5** | Sebastián orienta aspirantes en la Beca Talento de la CUC. Sebastián y Santiago hicieron **Amelia**, un asistente para preuniversitarios, y **Manglara**, un avatar 3D con voz y RAG. Esteban modela en 3D. Es construir sobre experiencia propia. |
| Riesgo de construcción en ~20 h efectivas | **4** | 3 | El Copiloto es más acotado (reglas y ledger simulado). Rumbo exige contenido curado de 4 carreras y una simulación con IA, aunque se mitiga con 2 simulaciones completas y respuestas cacheadas. |
| Riesgo regulatorio o ético | **4** | 3 | Rumbo trata datos de **menores** (Ley 1581/2012, Ley 1098/2006). Se resuelve con datos mínimos, consentimiento del acudiente y conexión moderada, pero hay que defenderlo bien. |
| Madurez de la documentación | 4 | 4 | Las dos están completas tras la iteración de hoy. |
| **Total (sobre 40)** | **27** | **35** | |

## Recomendación

**Principal: Rumbo (Orientación Vocacional). Respaldo: Copiloto Financiero.**

Por qué:
1. Responde al reto con sus propias palabras: talento joven, oportunidades y calidad de vida.
2. Los aliados del evento son la ruta de escala, lo que convierte la pregunta de viabilidad en un punto a favor.
3. El equipo ya construyó piezas casi idénticas (Amelia, Manglara), así que en 20 horas se puede llegar más lejos que cualquier otro equipo.
4. La demo tiene un momento memorable: "habla con una enfermera en su turno de noche antes de elegir la carrera".

Cuándo usar el respaldo:
- Si en "Comprender el reto" (09:45) la Alcaldía enfoca el reto en algo que deja por fuera la educación.
- Si la organización prohíbe trabajar con menores o datos de colegios.

En cualquiera de los dos casos, se decide antes de las 11:30 (congelamiento de alcance) y no se vuelve a discutir.

## Riesgos de Rumbo que hay que cerrar antes del evento

| Riesgo | Acción | Responsable |
|---|---|---|
| "Es otro test vocacional más" | Abrir el pitch con la **simulación**, no con el test. El test es solo la puerta de entrada. | Mateo + Esteban |
| Cifras sin fuente | Verificar 3 cifras clave en SNIES, el Observatorio Laboral y SPADIES | Mateo |
| Uso del nombre "Descubre" o de instituciones | Preguntar a la CUC o hablar de "eventos tipo Descubre"; plan en `10-operations/contingency.md` | Sebastián |
| Simulación que alucina | Respuestas ancladas a contenido curado y cacheadas en el golden path (ADR-003) | Sebastián |
| Datos de menores | Defender el diseño con datos mínimos y consentimiento (ADR-005) en `preguntas-jurado.md` | Sebastián + Mateo |

## Decisiones pendientes del equipo

1. Confirmar si Rumbo es la principal.
2. Elegir el nombre: Rumbo, Ensaya, Un Día Como o Brújula Caribe.
3. Elegir qué 2 de las 4 carreras llevan simulación completa con IA.
4. Confirmar el proveedor de LLM y sus créditos.
