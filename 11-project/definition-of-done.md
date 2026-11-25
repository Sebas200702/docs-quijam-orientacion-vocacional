# Definición de terminado

## Un ítem de código está terminado cuando

- [ ] Cumple sus criterios de aceptación (AC-xx) y los FR referenciados.
- [ ] Tiene tests unitarios si toca el dominio (matching, reglas, guardas) y pasan.
- [ ] Valida entradas con los contratos Zod.
- [ ] No registra PII en los logs ni la envía al LLM.
- [ ] Funciona a 360 px y con el LLM caído (si aplica).
- [ ] Lo revisó otra persona del equipo y está en `main` desplegado.

## Un paquete de contenido (carrera) está terminado cuando

- [ ] Pasa el linter del seed.
- [ ] Cumple el checklist de `10-operations/curacion-contenido.md`.
- [ ] Toda cifra está `verified` con fuente y año o es `draft` con fuente sugerida.

## El MVP está terminado cuando

- [ ] El guion de demo (`demo-script.md`) se ejecuta completo 3 veces seguidas sin intervención técnica.
- [ ] Los casos bloqueantes de IA (AI-01, AI-04, AI-06, AI-08, AI-13) pasan.
- [ ] SM-01…SM-12 pasan.
- [ ] El panel de ciudad muestra el rótulo de datos sintéticos y Conectar la etiqueta "Ejemplo".
- [ ] La tabla de lo real frente a lo simulado coincide con lo que se muestra.
- [ ] El video de respaldo está grabado antes de las 07:00 del día 2.
