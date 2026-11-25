# Límites de la IA

## Principio

> La IA orienta; nunca decide por el estudiante. (ADR-002)

## Dónde se usa la IA

| Uso | Modelo | Fallback |
|-----|--------|----------|
| Narrar escenas de la simulación y responder preguntas dentro del guion | Gemini, clase Flash (ADR-006) | `staticNarration` / caché |
| Reescribir en tono natural la explicación de la recomendación | Gemini, clase Flash | Plantilla determinista |
| Clasificar la intención del texto libre (story, data_request, off_topic, personal_health, risk_signal) | Gemini más reglas de palabras clave | Solo reglas |
| Prefiltro de moderación de preguntas a mentores (P1) | Gemini | Reglas más moderación humana |
| Apoyo al equipo para redactar borradores de contenido (fuera de runtime) | Cualquiera | Revisión humana obligatoria |

## La IA puede

- Narrar en segunda persona dentro de una escena curada.
- Explicar con otras palabras razones que ya se calcularon.
- Responder preguntas cualitativas usando los `groundingFacts` de la carrera.
- Decir "no lo sé" y remitir a la ficha o a un mentor.
- Reflejar los rasgos que mostraron las decisiones del estudiante, sin juzgarlos.

## La IA no puede

- Calcular o cambiar la afinidad ni el orden de las recomendaciones.
- Decir qué carrera debe estudiar el estudiante, ni que una carrera "no es para él o ella".
- Dar cifras (salario, empleabilidad, costos, duración, estadísticas).
- Nombrar instituciones, hospitales o empresas reales que no estén en el guion.
- Inferir o mencionar el género, el estrato, la etnia, la religión o la orientación del estudiante.
- Hacer consejería psicológica, diagnosticar o manejar crisis por su cuenta (solo activa el protocolo).
- Dar consejo médico: ni diagnósticos, ni medicamentos, ni dosis, ni sobre la salud del estudiante ni como indicación clínica en la simulación (FR-047).
- Recibir datos personales (alias, colegio, contactos) en el prompt.
- Publicar nada a los mentores ni al acudiente sin pasar por las reglas y la moderación.

## Arquitectura de control

```
Entrada del estudiante
  → Prefiltro determinista (longitud, PII, palabras de riesgo y de salud personal)
  → Gemini API (prompt versionado + escena + groundingFacts)
  → Validación de esquema (Zod)
  → Guardas deterministas (cifras, imperativos, consejo médico, riesgo, longitud)
  → UI    |   si falla cualquier paso → texto estático del guion
  → AiTurnLog (sin PII)
```

La seguridad no depende de que el modelo obedezca: las guardas deterministas son la última palabra.
