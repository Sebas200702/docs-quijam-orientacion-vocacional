# Contingencia

| Falla | Señal | Plan |
|-------|-------|------|
| LLM caído o lento | `health.llm = degraded` o latencia mayor a 8 s | Automático: `cache` → `static`. El presentador no lo menciona salvo que pregunten; si preguntan, es una virtud: "el sistema nunca deja al estudiante sin respuesta". |
| LLM inventa algo en vivo | Pasa una guarda por error | Forzar `DEMO_MODE=cache` (variable o toggle de admin) antes de presentar si en el ensayo 3 hubo cualquier fallo |
| Wifi del evento | Sin conexión | Datos móviles del presentador; si falla, despliegue local en el portátil (`bun run dev` con Postgres en Docker) |
| VPS caído | Health no responde | Local en el portátil y frontend en Vercel apuntando a la API local por túnel |
| Todo cae | — | Video de respaldo de 3 min, grabado el viernes a las 08:30 |
| Un dato no se pudo verificar | `status: draft` | Se muestra "por verificar" y se cuenta como ejemplo de honestidad del producto |
| La CUC no autoriza mencionar "Descubre" | — | Renombrar el evento del seed a "Experiencia vocacional (ejemplo)" y en el pitch hablar de "eventos como los que hacen las universidades" |
| Pregunta del jurado fuera de la preparación | — | Responder con la tabla de lo real frente a lo simulado y la honestidad: "no lo hemos validado aún" |
