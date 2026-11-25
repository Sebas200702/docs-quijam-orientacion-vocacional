# Contingencia

Horarios del día 2 alineados con `00-quijam/estrategia-para-ganar.md` §4–§5 y `00-quijam/plan-48h.md`: **video de respaldo listo antes de las 07:00**, **congelamiento de código a las 08:30** y **≥5 ensayos cronometrados** (2 la noche del día 1 y 3 la mañana del día 2).

`DEMO_MODE` es una sola variable con tres valores: `off | cache | static` (definición en `10-operations/development.md`).

| Falla | Señal | Plan |
|-------|-------|------|
| LLM caído o lento | `health.llm = degraded` o latencia mayor a 8 s | Automático con `DEMO_MODE=off`: Gemini → caché → estático. El presentador no lo menciona salvo que pregunten; si preguntan, es una virtud: "el sistema nunca deja al estudiante sin respuesta". |
| LLM inventa algo en vivo | Pasa una guarda por error | Presentar con `DEMO_MODE=cache` si en cualquiera de los ensayos del viernes o en la batería bloqueante (AI-01, AI-04, AI-06, AI-08, AI-13) hubo un fallo. Se decide justo después del congelamiento de las 08:30 y se verifica en `GET /health` (`demoMode`). |
| Caché incompleta o sin red hacia Gemini | Una pregunta del guion no está en caché | `DEMO_MODE=static`: solo textos del guion y textos fijos; el recorrido de la demo sigue igual |
| Wifi del evento | Sin conexión | Datos móviles del presentador; si falla, despliegue local en el portátil (`bun run dev` con Postgres en Docker, `DEMO_MODE=static`) |
| VPS caído | Health no responde | Local en el portátil y frontend en Vercel apuntando a la API local por túnel |
| Ilustración que no carga | Imagen rota en una escena | Se muestra la ilustración genérica de la carrera (FR-048); las ilustraciones son archivos estáticos, no dependen de ningún servicio |
| Panel de ciudad no responde | Error en `/ciudad` | Captura del panel rotulada "Datos sintéticos de demostración" en la última diapositiva; el Pitch Lead narra igual el cierre |
| Todo cae | — | Video de respaldo de 3 min, **listo antes de las 07:00 del viernes** (`00-quijam/plan-48h.md`) |
| Un dato no se pudo verificar | `status: draft` | Se muestra "por verificar" y se cuenta como ejemplo de honestidad del producto |
| La CUC no autoriza mencionar "Descubre" | — | Renombrar el evento del seed a "Experiencia vocacional (ejemplo)" y en el pitch hablar de "eventos como los que hacen las universidades" |
| Pregunta del jurado fuera de la preparación | — | Responder con la tabla de lo real frente a lo simulado y la honestidad: "no lo hemos validado aún" |
