# docs-quijam-orientacion-vocacional

## Rumbo — Vive la carrera antes de elegirla (nombre de trabajo)

Herramienta de orientación vocacional para estudiantes de grado 10 y 11 de Barranquilla. Lleva a cualquier momento del año lo que hoy solo ocurre en espacios cortos y esporádicos (como el evento "Descubre" de la Universidad de la Costa): vivir un día simulado en la carrera, contrastarlo con datos reales de pensum, salario y empleabilidad, y conectar con profesionales y universidades. El estudiante decide con fundamento y sin el "esto no era lo que yo quería".

Idea 2 del equipo para QuiJAM 2026 (26–27 nov 2026, Barranquilla). La idea 1, Copiloto Financiero, vive en `docs-hackathon`.

## Loop central

**Explorar → Vivir → Contrastar → Conectar → Decidir con fundamento**

| Paso | Experiencia (S3) | Documento |
|------|------------------|-----------|
| Explorar | Test vocacional + recomendación explicada | `05-experiencias/test-vocacional.md` |
| Vivir | Simulación "un día en la carrera" con IA | `05-experiencias/simulacion-dia-en-la-carrera.md` |
| Contrastar | Info realista: pensum, salario, empleabilidad | `05-experiencias/info-realista.md` |
| Conectar | Conexión con profesionales/universidades | `05-experiencias/conexion-profesionales.md` |
| Decidir | Bitácora vocacional y comparador | `03-ux/dashboard.md` |

## Mapa

- `00-quijam/` — reto, alineación, pitch, plan de 48 h, preguntas del jurado, [estrategia para ganar](00-quijam/estrategia-para-ganar.md), [roles del equipo](00-quijam/roles-equipo.md) y [comparativa de ideas](00-quijam/comparativa-ideas.md).
- `01-product/` — brief, PRD, personas y principios.
- `02-requirements/` — requisitos con ID, historias, criterios de aceptación y alcance MVP.
- `03-ux/` — onboarding, flujos, experiencias y bitácora.
- `04-domain/` — modelo de dominio, reglas, modelo de recomendación y modelo de contenido de carreras.
- `05-experiencias/` — diseño de las cuatro experiencias (reemplaza la sección Open Payments de la idea 1).
- `06-ai/` — límites de la IA, grounding y control de sesgos y seguridad de menores.
- `07-architecture/` — arquitectura del sistema.
- `08-technical/` — API, base de datos, contratos y seguridad (Ley 1581 de 2012).
- `09-testing/` — estrategia, fallos de IA y seguridad de menores.
- `10-operations/` — desarrollo, despliegue, contingencia y curaduría de contenido.
- `11-project/` — roadmap, backlog, definición de terminado y guion de demo.
- `12-decisions/` — ADRs.

## Principio rector

> La IA orienta; los datos verificados informan; los profesionales acercan; el estudiante decide; el sistema registra el porqué.

## Regla de datos

Ninguna cifra se inventa. Toda estadística, salario o tasa que no esté verificada se escribe como `[DATO POR VERIFICAR — fuente sugerida: X]`, en la documentación y en el producto.

## Trazabilidad

Problema → Objetivo → Experiencia → Requisito (FR/NFR) → Regla (BR) → Dominio → API → Implementación → Test.

Ejemplo: "los espacios de exploración son cortos y esporádicos" → "acceso a la experiencia todo el año" → Simulación → FR-040…FR-047 → BR-020…BR-025 → `Simulation`, `SimulationScene` → `POST /simulations` → `simulation-service` → `09-testing/ai-failures.md` casos AI-01…AI-15.

## Decisiones (ADR)

- ADR-001 Alcance del producto · ADR-002 La IA orienta, no decide · ADR-003 Contenido curado como única fuente de la IA · ADR-004 Recomendación determinista · ADR-005 Datos de menores y conexión moderada · ADR-006 Stack.
