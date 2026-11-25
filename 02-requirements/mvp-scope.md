# Alcance del MVP

Construible en la ventana de QuiJAM (≈19 h 30 min de construcción efectiva y 5 personas; ver `00-quijam/plan-48h.md`).

## P0 — Imprescindible para la demo

1. Modo demo con 2 perfiles semilla (Valentina, Andrés) y reinicio.
2. Onboarding corto (intereses, materias, ruta).
3. Test de 24 ítems, motor determinista, top 3 explicado más 1 fuera de zona.
4. Catálogo de 4 carreras: Enfermería, Ingeniería de Sistemas, Derecho y Tecnología en Gestión Logística (SENA).
5. Simulación con IA de 4 escenas para **Enfermería e Ingeniería de Sistemas**, con fallback estático. Las otras dos carreras tienen al menos el guion estático.
6. Ficha Contrastar completa para las 4 carreras (con fuente o "por verificar").
7. Agenda (8 eventos de ejemplo) y mentores (4 de ejemplo) con preguntas moderadas.
8. Bitácora, comparador, mi decisión y resumen compartible.
9. Pantalla de consentimiento del acudiente (envío simulado).
10. Guardas de IA: sin cifras, sin PII en prompts, señales de riesgo.

## P1 — Si sobra tiempo o justo después del evento

1. Simulación con IA para Derecho y Logística.
2. Panel del orientador (agregado y anónimo).
3. Sesiones grupales con mentores y recordatorios.
4. Repetir el test e historial.
5. Rutas de continuidad y financiación.
6. Retomar una simulación.

## P2 — Posterior

1. Ingesta automática de SNIES y Observatorio Laboral.
2. Más de 20 carreras, con contenido validado por las universidades y el SENA.
3. Consentimiento real del acudiente (OTP por SMS o correo) y verificación de mentores por la institución.
4. Despliegue multi-colegio con la Secretaría de Educación.
5. Canal WhatsApp o modo offline (PWA).
6. Evaluación de impacto (permanencia en el primer año).

## Real frente a simulado en la demo

| Componente | En la demo | Nota para el jurado |
|------------|-----------|---------------------|
| Test y motor de recomendación | **Real** | Determinista y explicable |
| Simulación con LLM (2 carreras) | **Real** | Con caché de respaldo para el guion de la demo |
| Guiones de escenas | **Real**, escritos por el equipo | Revisar con profesionales después del evento |
| Datos de la ficha (pensum, salario, empleabilidad) | **Real si están verificados**; si no, se muestra "por verificar" | Curados a mano desde las fuentes oficiales; nunca inventados |
| Instituciones donde se estudia | Real (nombres públicos) | Confirmar la oferta vigente en SNIES |
| Eventos de la agenda | **Simulado** (datos de ejemplo) | Las fechas reales de Descubre y otros eventos `[POR VERIFICAR con cada institución]` |
| Mentores | **Simulado** (perfiles ficticios rotulados "ejemplo") | P2: verificados por la institución |
| Respuestas de mentores | **Simulado** (precargadas) | Una pregunta nueva queda en moderación |
| Consentimiento del acudiente | **Simulado** (no se envía el mensaje) | El flujo y el bloqueo en la API sí son reales |
| Panel del orientador | No (P1); como mucho una captura | |
| Bitácora, comparador y resumen | **Real** | |

## Regla de alcance

No entra al MVP nada que no mejore directamente el loop:

**Explorar → Vivir → Contrastar → Conectar → Decidir con fundamento.**
