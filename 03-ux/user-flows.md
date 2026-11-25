# Flujos de usuario

## F1 — Loop completo (flujo de la demo)

```
Bienvenida → Onboarding → Test (24 ítems) → Resultados (top 3 + fuera de zona)
  → Carrera: Enfermería
      → Vivir: 4 escenas → Reflexión (1–5)
      → Contrastar: ficha (pensum, salario, empleabilidad, mitos, dónde)
      → Conectar: evento ("Me interesa") + pregunta a mentora (moderación)
  → Carrera: Ing. de Sistemas → Vivir → Reflexión
  → Bitácora → Comparador (Enfermería frente a Sistemas) → Mi decisión → Compartir resumen
```

## F2 — "Tengo opciones en mente"

Onboarding → Catálogo (filtro por área y nivel) → Carrera → Vivir / Contrastar / Conectar → Bitácora. El test se ofrece como sugerencia ("¿Quieres ver qué otras carreras encajan contigo?").

## F3 — Invitado

Bienvenida → *Solo quiero mirar* → Catálogo → Ficha Contrastar y agenda (lectura). Al intentar simular o guardar: "Crea tu perfil para vivir la carrera" (la simulación requiere perfil para controlar el costo y la seguridad).

## F4 — Pregunta de cifras dentro de la simulación

Escena → el estudiante escribe "¿cuánto gana?" → la guarda detecta la intención `data_request` → respuesta: "Ese dato lo tenemos con fuente en la ficha" → botón *Ver salario con fuente* → ficha anclada en la sección Salario → *Volver a la simulación* (conserva la escena).

## F5 — Señal de riesgo

El estudiante escribe algo que indica angustia o riesgo → la guarda `risk_signal` pausa la simulación → mensaje de apoyo, líneas oficiales de ayuda y "habla con tu orientador o un adulto de confianza" → opción de seguir o salir. No se guarda el texto (solo el evento `risk_signal_shown`).

## F6 — Consentimiento

Perfil de un menor sin autorización → acción que guarda → modal de autorización → *Simular autorización* (demo) → `consent.status = granted` → la acción continúa.

## F7 — Mentor (P0 simulado)

El equipo (moderador) abre la cola → aprueba o rechaza la pregunta → el mentor de ejemplo responde (precargado o escrito en vivo por el equipo) → la pregunta y la respuesta aparecen en la carrera, sin autor.

## F8 — Acudiente

Recibe el enlace del resumen → ve las carreras exploradas, las reflexiones, el comparador y la decisión → (P1) opciones de financiación y rutas SENA.
