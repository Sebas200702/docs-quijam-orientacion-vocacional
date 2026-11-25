# UX — Panel de ciudad (Secretaría de Educación)

## Objetivo

Que la Secretaría de Educación de Barranquilla vea, en una sola pantalla y sin datos personales, **qué quieren estudiar los jóvenes de 10 y 11 frente a lo que demanda la ciudad**, para decidir dónde reforzar la orientación, las becas y los convenios con universidades y el SENA. Responde al eje QuiJAM "Transforma datos en mejores decisiones".

Es el **cierre de la demo** (`11-project/demo-script.md`, tramo final): "esto es lo que ve la Alcaldía". FR-085…FR-088, AC-16, AC-17, BR-060…BR-064.

## Usuaria

Diana, profesional de la Secretaría de Educación (`01-product/personas.md`, P6). En el MVP entra con la clave del panel (`CITY_PANEL_KEY`); en P2, con un rol institucional.

## Pantalla (`/ciudad`, escritorio y proyector; usable en móvil)

1. **Rótulo fijo** arriba, en ámbar y sin opción de ocultarlo: **"Datos sintéticos de demostración — no representan estudiantes reales"**.
2. **Encabezado:** "Intereses de los jóvenes frente a la demanda laboral de Barranquilla", periodo y filtros: grado (10 / 11 / ambos) y periodo. No hay filtro por colegio.
3. **Gráfico principal:** barras horizontales pareadas por sector:
   - Barra azul: **interés** (% de estudiantes cuya carrera preferida pertenece al sector).
   - Barra gris: **demanda** (participación del sector en la demanda laboral, índice de 0 a 1).
   - Etiqueta de **brecha** a la derecha: "Poco interés frente a la demanda" o "Mucho interés frente a la demanda", sin cifras de más.
   - Sectores del MVP: puerto y logística, tecnología, salud, servicios jurídicos y públicos, otros.
4. **Tarjeta "Brecha principal"** (una sola): por ejemplo, "Puerto y logística: poco interés frente a la demanda. Carreras del catálogo: Tecnología en Gestión Logística (SENA)". Es una observación, no una orden.
5. **Celdas suprimidas:** un sector con menos de 20 estudiantes muestra "Grupo muy pequeño para mostrar" y no muestra la barra de interés. Pie: "k ≥ 20: ningún grupo de menos de 20 estudiantes se muestra".
6. **Fuentes:** cada barra de demanda lleva su `DataBadge`. En la demo: "Sintético — fuente real sugerida: Observatorio Laboral para la Educación / DANE GEIH Barranquilla AM / Servicio Público de Empleo".
7. **Pie legal:** "Agregados anónimos. Sin datos personales ni por colegio. Ley 1581 de 2012."

Boceto:

```
┌ Datos sintéticos de demostración — no representan estudiantes reales ┐
Intereses de los jóvenes vs. demanda laboral · 2026-2 · Grado: ambos
Puerto y logística   ██ interés          ████████ demanda   ▲ poco interés
Tecnología           ██████ interés      ███████ demanda
Salud                ██████████ interés  █████ demanda      ▼ mucho interés
Servicios jurídicos  ████ interés        ███ demanda
Otros                Grupo muy pequeño para mostrar
Brecha principal: Puerto y logística · ver Tecnología en Gestión Logística (SENA)
```

## Cómo se calcula (resumen; detalle en `04-domain/business-rules.md` BR-060…BR-064)

- **Carrera preferida** de un estudiante: la de su `Decision` más reciente; si eligió "aún no sé", la carrera con mayor `fitScore` en sus reflexiones; si no tiene ninguna, no cuenta.
- **Interés del sector** = estudiantes con carrera preferida en el sector ÷ estudiantes que cuentan, por grado y periodo.
- **Demanda del sector:** índice desde fuentes oficiales (piloto) o sintético (demo).
- **Brecha** = interés − demanda; se muestra como texto ("poco/mucho interés"), no como un número nuevo.
- La demanda laboral **nunca** entra en la recomendación del estudiante (BR-063).

## Datos en la demo

- Seed `seed/city-panel-synthetic.json` con **agregados sintéticos** (porcentajes y conteos por sector), no con estudiantes ficticios: no hay filas falsas en `students`.
- Los valores son ilustrativos y los elige el equipo para que la historia sea legible; no se presentan como hallazgos.
- Los sectores estratégicos de la ciudad se citan como `[DATO POR VERIFICAR — fuente sugerida: Plan de Desarrollo Distrital de Barranquilla / Cámara de Comercio de Barranquilla]`.

## Microcopy

- Vacío: "Aún no hay suficientes estudiantes en este periodo para mostrar datos sin poner en riesgo su privacidad."
- Tooltip de interés: "Porcentaje de estudiantes cuya carrera preferida está en este sector."
- Tooltip de demanda: "Peso del sector en la demanda laboral de la ciudad. En esta demo es sintético."

## Lo que no hay

Rankings de colegios, listas de estudiantes, alertas individuales, exportación de microdatos ni recomendaciones de qué deben estudiar los jóvenes.

## Relación con el panel del orientador

El panel por colegio (FR-080, P1) es otra vista, para el orientador de cada colegio, con k ≥ 5 dentro de su colegio. El panel de ciudad no baja al nivel de colegio.
