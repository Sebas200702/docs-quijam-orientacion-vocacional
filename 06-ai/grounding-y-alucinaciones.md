# Grounding y control de alucinaciones

## Riesgo

Un LLM puede inventar con seguridad salarios, tasas de empleo, materias o instituciones. Para un estudiante de 16 años, una cifra inventada puede decidir su carrera.

## Estrategia en cuatro capas

### 1. Contenido curado como única fuente
- La IA solo recibe el guion de la carrera: escena actual, `situation`, `consequence` y `groundingFacts`.
- No hay acceso a la web ni a RAG abierto en el MVP. El contexto es pequeño y controlado.
- Los `groundingFacts` son cualitativos; las cifras viven solo en `DataPoint`, que la IA nunca recibe.

### 2. Instrucciones explícitas (prompt de sistema versionado)
- "Si no está en los hechos de la escena, di que no lo sabes."
- "Nunca des números de dinero, porcentajes, duraciones ni estadísticas."
- Salida JSON con `intent` para enrutar las peticiones de datos.

### 3. Guardas deterministas posteriores
| Guarda | Regla | Acción si falla |
|--------|-------|-----------------|
| Esquema | JSON válido según `SimulationTurnOutput` | Texto estático |
| Cifras | Regex: dígitos junto a `%`, `$`, `COP`, "millones", "mil pesos", "salario mínimo", "por ciento", y números escritos en letras más esas unidades | Texto estático más enlace a la ficha |
| Entidades | Nombres de instituciones o empresas que no estén en la lista blanca del guion | Texto estático |
| Imperativo de decisión | "deberías estudiar", "esta carrera es para ti", "no sirves para" | Texto estático |
| Consejo médico | Dosis y unidades clínicas (mg, ml, gotas, "cada N horas"), "tómate", "te recomiendo tomar", "lo que tienes es" | Texto estático; si la entrada era de salud personal, texto fijo de redirección (FR-047) |
| Longitud | Más de 180 palabras | Truncar en la última oración completa |
| Riesgo | Clasificador más palabras clave | Protocolo de apoyo |

### 4. Redirección a datos con fuente
`intent: data_request` → la UI muestra "Ese dato lo tenemos con fuente" más el botón a la sección de la ficha. Así la pregunta del estudiante se responde con verdad verificable y no con la IA.

## Explicaciones del test
La IA recibe solo `{carrera, dim1, dim2, itemTexts}` y debe reescribir la plantilla. Validación: la salida debe mencionar ambas dimensiones y no puede agregar otras ni cifras distintas de la afinidad. Si falla, se usa la plantilla.

## Medición
- `AiTurnLog.guardResults` cuenta cuántas veces se activa cada guarda por versión de prompt.
- Antes de la demo: correr la batería de `09-testing/ai-failures.md` y que todos los casos pasen.
