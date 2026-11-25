# Modelo de recomendación (matching)

## Enfoque

Modelo de intereses de 6 dimensiones inspirado en la tipología RIASEC de Holland, de uso común en orientación vocacional. Los ítems los redacta el equipo en español del Caribe colombiano. **No es un instrumento psicométrico validado** y el producto lo dice (FR-024). P2: revisar con un psicólogo u orientador y, si se usa un instrumento existente, verificar su licencia.

| Dim | Nombre en la app | Ejemplo de ítem |
|-----|------------------|-----------------|
| R | Hacer con las manos | "Me gusta armar, reparar o manejar equipos." |
| I | Investigar | "Me gusta entender por qué pasan las cosas." |
| A | Crear | "Me gusta diseñar, escribir o expresar ideas de forma original." |
| S | Ayudar | "Me gusta ayudar a personas cuando están enfermas o tienen un problema." |
| E | Liderar y convencer | "Me gusta defender una idea frente a otros." |
| C | Organizar | "Me gusta que las cosas sigan un orden y un plan." |

24 ítems = 4 por dimensión, respuesta de 1 a 4.

## Cálculo

1. **Perfil del estudiante.** Para cada dimensión `d`: `p_d = (suma de sus 4 respuestas − 4) / 12` → valor entre 0 y 1.
2. **Perfil de la carrera.** `c_d` entre 0 y 1, asignado por el equipo de contenido para cada carrera (`Career.riasecProfile`) y revisado por un profesional cuando sea posible.
3. **Afinidad base.** Similitud coseno: `cos(p, c) = Σ p_d·c_d / (‖p‖·‖c‖)`. Si `‖p‖ = 0` (todo en 1), afinidad 0 para todas y mensaje: "Parece que nada te llamó la atención. Prueba con *Tengo opciones en mente*."
4. **Bono de intereses.** +0,05 por cada chip del onboarding mapeado a la carrera (máx. +0,10).
5. **Afinidad final.** `round(min(1, cos + bono) × 100)`.
6. **Orden y desempate.** Por afinidad descendente y, si hay empate, por `career.id` alfabético (determinismo, NFR-013).
7. **Fuera de zona.** La carrera de mayor afinidad fuera del top 3 cuya `area` no esté en el top 3; si no existe, la de mayor afinidad fuera del top 3. Con el catálogo de 4 carreras del MVP es siempre la cuarta; la regla cobra sentido al crecer el catálogo.

## Explicación (razones)

- Se toman las 2 dimensiones con mayor contribución `p_d·c_d`.
- Para cada una se cita el ítem con la respuesta más alta del estudiante: "Marcaste *Mucho* en 'Me gusta ayudar a personas…'".
- Plantilla determinista: "Te la mostramos porque te interesa **{dim1}** y **{dim2}**, que son centrales en {carrera}."
- La IA puede reescribir la plantilla en un tono más natural, pero sin agregar razones nuevas, y la salida se valida contra las razones calculadas. Si falla, se usa la plantilla.

## Entradas prohibidas

Género, estrato, colegio, barrio, rendimiento académico y alias. El motor recibe solo las respuestas, los chips y las preferencias.

## Ejemplo (persona de demo, no son datos medidos)

Valentina: `p = {R:0.33, I:0.75, A:0.25, S:1.0, E:0.42, C:0.58}`

Sin bono de chips, para simplificar:

| Carrera | c (R,I,A,S,E,C) | Coseno | Afinidad | Resultado |
|---------|-----------------|--------|----------|-----------|
| Medicina | .5,.9,.1,1,.3,.6 | 0,983 | 98 | Top 1 |
| Derecho | .1,.6,.4,.6,1,.6 | 0,868 | 87 | Top 2 |
| Ing. de Sistemas | .4,1,.4,.2,.3,.7 | 0,821 | 82 | Top 3 |
| Tecn. Gestión Logística | .5,.4,.1,.3,.6,1 | 0,791 | 79 | Fuera de zona |

Afinidades recalculadas con el perfil de Medicina (2026-11-24); Derecho, Sistemas y Logística no cambian. Este ejemplo sirve como caso de prueba de `matching.spec.ts`. Los perfiles de las carreras son supuestos de diseño del equipo, no datos empíricos.
