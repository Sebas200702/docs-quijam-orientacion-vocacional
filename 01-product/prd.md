# PRD — Rumbo

## 1. Resumen

Rumbo es una herramienta web mobile-first de orientación vocacional para grados 10 y 11. Combina cuatro experiencias (test explicado, simulación con IA, información realista y conexión con profesionales) en un solo loop que termina en una decisión registrada por el estudiante.

## 2. Problema

Elegir carrera a los 16 o 17 años con poca exposición real a las profesiones. Los espacios de exploración de las universidades son cortos y esporádicos, y la información oficial no está escrita para el estudiante. El resultado son decisiones con arrepentimiento, deserción y cambio de carrera (magnitud `[DATO POR VERIFICAR — fuente sugerida: SPADIES/MEN]`).

## 3. Oportunidad

- Las universidades aliadas de QuiJAM ya producen experiencias vocacionales (por ejemplo, Descubre de la CUC); falta continuidad.
- Los LLM permiten simular escenas interactivas a bajo costo, siempre que estén acotadas por un guion curado.
- Existen fuentes públicas (SNIES, Observatorio Laboral para la Educación) que se pueden traducir a lenguaje joven.

## 4. Visión

Que cada estudiante de colegio en Barranquilla pueda vivir, contrastar y conversar sobre al menos tres caminos antes de inscribirse en uno.

## 5. Objetivos

| ID | Objetivo | Cómo se verifica en el MVP |
|----|----------|----------------------------|
| O1 | Acceso todo el año | Todas las experiencias funcionan sin depender de un evento |
| O2 | Experiencia vivida | Simulación de 4 escenas con decisiones para al menos 2 carreras |
| O3 | Datos honestos | El 100 % de las cifras en pantalla tiene fuente o marca "por verificar" |
| O4 | Autonomía del estudiante | Ninguna pantalla dice "deberías estudiar X"; la decisión la escribe el estudiante |
| O5 | Puente a lo real | Agenda de eventos y preguntas a mentores accesibles desde cada carrera |
| O6 | Seguridad de menores | Consentimiento, minimización de datos y conexión moderada |

## 6. Usuarios

Ver `personas.md`: Valentina (grado 11, colegio oficial), Andrés (grado 10, presión familiar), Luz Marina (orientadora), Carlos (mentor) y Rosa (acudiente).

## 7. Propuesta de valor

> Vive la carrera antes de elegirla.

## 8. Alcance funcional

| Módulo | Contenido | Prioridad |
|--------|-----------|-----------|
| Acceso y consentimiento | Modo invitado, perfil con alias, autorización del acudiente (simulada en el MVP), borrar datos | P0 |
| Onboarding | Grado, intereses, materias, preferencias opcionales; elegir ruta | P0 |
| Explorar | Test de 24 ítems, perfil de intereses, top 3 explicado más 1 fuera de zona | P0 |
| Vivir | Simulación de 4 escenas por carrera con IA y fallback estático | P0 |
| Contrastar | Ficha: pensum, salario, empleabilidad, duración, costo, mitos, dónde estudiar | P0 |
| Conectar | Agenda de eventos, mentores verificados, preguntas moderadas | P0 (datos de ejemplo) |
| Decidir | Bitácora, comparador, mi decisión, resumen compartible | P0 |
| Orientador | Panel agregado y anónimo por colegio | P1 |
| Recordatorios | Aviso de eventos | P1 |

Detalle en `02-requirements/`.

## 9. Catálogo del MVP

Cuatro carreras con contenido curado, elegidas para cubrir áreas distintas y una ruta tecnológica:

1. Enfermería (salud) — demo.
2. Ingeniería de Sistemas (tecnología) — demo.
3. Derecho (ciencias sociales).
4. Tecnología en Gestión Logística (SENA; logística y puerto).

Se puede cambiar cualquiera, siempre que se mantengan una ruta técnica o tecnológica y la diversidad de áreas.

## 10. Fuera de alcance

- Diagnóstico psicológico o psicométrico clínico. El test no es un instrumento validado y la pantalla lo dice.
- Inscripción o pagos a universidades.
- Chat privado entre adultos y menores.
- Ranking de universidades o publicidad pagada en las recomendaciones.
- Integración automática con SNIES u Observatorio en el MVP (los datos se curan a mano).
- App nativa.

## 11. Éxito del MVP

En la demo, una estudiante pasa de "no sé qué estudiar" a comparar dos carreras que vivió y contrastó, con una pregunta enviada a una mentora y una decisión escrita por ella, en menos de 5 minutos y sin que la IA invente una cifra.

## 12. Riesgos

| Riesgo | Mitigación |
|--------|------------|
| La IA inventa datos | Grounding en contenido curado, prohibición de cifras y redirección a la ficha (`06-ai/`) |
| La IA refuerza estereotipos | Sin género ni estrato en los datos, protagonistas diversos, pruebas de sesgo |
| Contenido mal verificado | Estados `draft`/`verified`; en pantalla solo se muestra `verified` o la marca "por verificar" |
| Alcance excesivo en 2 días | P0 estricto; Conectar con datos de ejemplo |
| Exposición de menores | Ley 1581, consentimiento, sin chat privado, minimización |
| LLM caído en la demo | Guion estático y caché de la demo |
| Conflicto con la marca Descubre | Pedir permiso a la CUC; si no lo da, usar un evento genérico |

## 13. Definición del producto

> Rumbo es una herramienta de orientación vocacional para estudiantes de grado 10 y 11 de Barranquilla que les permite, en cualquier momento del año, explorar sus intereses, vivir un día simulado en una carrera, contrastarlo con datos reales y conectar con profesionales y universidades. La IA orienta; el estudiante decide.
