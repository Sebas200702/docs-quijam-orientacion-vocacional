# ADR-004 — Recomendación determinista y explicable

## Estado
Aceptada (2026-11-24).

## Contexto
Hay que recomendar carreras de forma justa, reproducible y explicable a un menor y a su familia, y probarlo en dos días.

## Decisión
Perfil de intereses de 6 dimensiones (inspirado en RIASEC) con 24 ítems, similitud coseno frente al perfil curado de cada carrera, un bono acotado por intereses del onboarding, desempate alfabético y razones trazables a las respuestas. Entradas prohibidas: género, estrato, colegio, notas. Detalle en `04-domain/matching-model.md`.

## Alternativas descartadas
- Que el LLM elija las carreras: no reproducible, no auditable y con riesgo de sesgo.
- Un modelo entrenado con datos: no tenemos datos ni tiempo, y sería opaco.

## Consecuencias
- Tests exactos (AC-03, EQ-01).
- El test no es un instrumento validado; se declara así y se revisa con profesionales en la fase 1.
