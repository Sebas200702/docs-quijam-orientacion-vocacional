# ADR-001 — Alcance del producto

## Estado
Aceptada (2026-11-24).

## Contexto
La idea surge del valor de eventos como Descubre (CUC) y de su límite: son cortos y esporádicos. El equipo eligió los cuatro formatos de experiencia: simulación con IA, test con recomendación explicada, conexión con profesionales y universidades, e info realista. Hay unas 19,5 h de construcción efectiva.

## Decisión
Un solo producto con el loop **Explorar → Vivir → Contrastar → Conectar → Decidir** para estudiantes de grado 10 y 11 de Barranquilla. Las cuatro experiencias son de primera clase. El MVP usa 4 carreras curadas (2 con simulación por IA, presentadas como texto con escenas ilustradas) y Conectar con datos de ejemplo presentado como visión. Afinado del 2026-11-24: el modelo es B2G (licencia de la Secretaría de Educación para los colegios oficiales, gratis para el estudiante) y la demo cierra con un panel de ciudad agregado y anónimo con datos sintéticos rotulados (`01-product/prd.md` §13, `03-ux/panel-ciudad.md`).

## Alternativas descartadas
- Solo test vocacional: ya existe y no resuelve "no sé cómo es un día real".
- Solo simulación: sin datos reales, refuerza impresiones y no da fundamento.
- Plataforma de mentoría en vivo: riesgo para menores y dependencia de la disponibilidad humana.

## Consecuencias
- La regla de alcance (`02-requirements/mvp-scope.md`) filtra todo lo que no mejora el loop.
- El contenido curado pasa a ser parte del producto (`10-operations/curacion-contenido.md`).
