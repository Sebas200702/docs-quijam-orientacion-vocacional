# ADR-002 — La IA orienta, no decide

## Estado
Aceptada (2026-11-24).

## Contexto
Elegir carrera es una decisión de vida de un menor de edad. Un LLM puede sonar convincente aunque se equivoque, reproducir estereotipos o inventar datos. El jurado y las familias van a preguntar "¿la IA le dice qué estudiar?".

## Decisión
1. La recomendación la calcula un motor determinista y explicable (ADR-004); la IA no participa en el cálculo.
2. La IA solo narra simulaciones dentro de guiones curados y explica razones ya calculadas.
3. Ninguna pantalla ni respuesta de la IA dice qué carrera debe estudiar el estudiante; las guardas bloquean los imperativos de decisión.
4. Siempre se muestran varias opciones, incluida una fuera de zona.
5. "Mi decisión" la escribe el estudiante, sin prellenado, y admite "aún no sé".

## Consecuencias
- La experiencia es menos "mágica" que un chatbot oráculo, pero confiable y defendible ante el jurado, las familias y los colegios.
- Hacen falta guardas deterministas y pruebas (AI-04, AC-01, AC-10).
- Principio rector: *La IA orienta; los datos verificados informan; los profesionales acercan; el estudiante decide; el sistema registra el porqué.*
