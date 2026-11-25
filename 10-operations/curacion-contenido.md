# Curaduría de contenido

El valor de Rumbo depende de la calidad del contenido. Este es el proceso para cada carrera.

## Pipeline

1. **Borrador** (UI/UX o AI Specialist; se puede usar IA): summary, pensum por ciclos, mitos y realidades, guion de 4 escenas y `groundingFacts`. Estado `draft`.
2. **Cifras** (Pitch Lead): consultar la fuente oficial (`04-domain/career-content-model.md` §Fuentes), copiar el valor, la fuente, la URL y el año. Solo entonces `verified`. Si no se encuentra el dato, se queda en `draft` con `suggestedSource`.
3. **Linter** (`bun run seed`): rechaza cifras en el texto libre, `verified` sin fuente y escenas sin `staticNarration`.
4. **Revisión cruzada** (otra persona del equipo): lenguaje, estereotipos y coherencia con la carrera. Se registra en `reviewedBy`.
5. **Revisión profesional** (después del evento): un profesional de la carrera valida el guion y los mitos; la institución aliada valida el pensum y la oferta.

## Checklist por carrera (antes de la demo)

- [ ] Resumen sin cifras.
- [ ] Pensum: 2 ciclos con 3 o más áreas cada uno; fuente institucional con fecha de consulta.
- [ ] DataPoints: salario de enganche, vinculación, duración y costo (verified o draft con sugerencia).
- [ ] 3 mitos y realidades.
- [ ] Dónde estudiar: 2 o más opciones en Barranquilla y el área metropolitana (código SNIES si se verificó).
- [ ] Guion: 4 escenas, 2–3 decisiones cada una, `staticNarration` completa, protagonista según la regla de diversidad.
- [ ] Ilustraciones (carreras con simulación): una por escena más una genérica, archivo estático con `alt`, revisadas por una persona (regla 7 de `04-domain/career-content-model.md`).
- [ ] `sectorId` asignado para el panel de ciudad.
- [ ] Revisión cruzada hecha.

## Actualización

- Las cifras con más de 3 años desde `sourceYear` se marcan `stale` (BR-032).
- Revisión semestral del catálogo con las instituciones (P2).
