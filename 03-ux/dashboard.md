# UX — Bitácora vocacional (dashboard y perfil)

## Objetivo

Que el estudiante vea su recorrido y llegue a una decisión propia y explicada.

## Estructura

1. **Tu recorrido** (progreso del loop por carrera):

   | Carrera | Explorar | Vivir | Contrastar | Conectar |
   |---------|----------|-------|------------|----------|
   | Medicina | ✔ afinidad 98 | ✔ "Me vi" 4/5 | ✔ | ✔ 1 evento, 1 pregunta |
   | Ing. de Sistemas | ✔ afinidad 82 | ✔ 3/5 | — | — |

   (Valores de afinidad de la persona de demo, calculados en `04-domain/matching-model.md`; no son estadísticas.)

2. **Siguiente paso sugerido** (una sola acción): por ejemplo, "Te falta contrastar Ing. de Sistemas". Es una sugerencia de proceso, nunca de carrera.

3. **Comparador** (FR-071): elegir 2 o 3 carreras → tabla con afinidad, reflexión (lo que le gustó y lo que no), duración, costo, salario y vinculación (con `DataBadge`), y eventos próximos.

4. **Mi decisión** (FR-072): selector vacío más "Aún no sé", seguridad de 1 a 5 y "¿Por qué?" (texto). Microcopy: "Puedes cambiarla cuando quieras. Decidir también es descartar."

5. **Compartir** (FR-073): *Generar resumen para mi acudiente/orientador* → enlace de 7 días más la opción *Imprimir*.

6. **Mi perfil y privacidad:** alias, grado, estado de la autorización, *Descargar mis datos* (P1) y *Borrar mis datos* (FR-004).

## Resumen compartible (contenido)

- Carreras exploradas y la afinidad (sin respuestas ítem por ítem).
- Reflexiones de la simulación.
- Comparador.
- Mi decisión y mi porqué (solo si el estudiante la incluye).
- Próximos eventos marcados.
- Pie: "Este resumen es una herramienta de conversación. Las cifras indican su fuente o están marcadas como por verificar."

## Lo que no hay

Rankings entre estudiantes, puntos por elegir una carrera ni notificaciones insistentes. La gamificación se limita a mostrar el progreso del loop.
