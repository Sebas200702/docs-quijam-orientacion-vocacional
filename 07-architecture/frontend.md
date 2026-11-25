# Frontend

## Rutas

| Ruta | Pantalla | FR |
|------|----------|----|
| `/` | Bienvenida | FR-001 |
| `/onboarding` | Pasos 1–6 | FR-002, FR-003, FR-010, FR-011 |
| `/test` | Test (una pregunta por pantalla) | FR-020 |
| `/resultados/:assessmentId` | Top 3 más fuera de zona | FR-022…FR-024 |
| `/carreras` | Catálogo | FR-030 |
| `/carreras/:slug` | Hub de carrera (Vivir / Contrastar / Conectar) | FR-031 |
| `/carreras/:slug/vivir` | Simulación | FR-040…FR-045 |
| `/carreras/:slug/contrastar#salario` | Ficha | FR-050…FR-054 |
| `/carreras/:slug/conectar` | Eventos, mentores y preguntas | FR-060…FR-064 |
| `/agenda` | Agenda general | FR-060 |
| `/bitacora` | Bitácora, comparador y mi decisión | FR-070…FR-073 |
| `/r/:token` | Resumen compartido (público, solo lectura) | FR-073 |
| `/perfil` | Privacidad y borrado | FR-004 |
| `/admin/moderacion` | Cola de moderación (protegida por clave del equipo) | FR-092 |

## Componentes clave

- `DataBadge` — cifra con fuente o "por verificar" (única forma permitida de mostrar números de la ficha).
- `SceneCard` — hora, lugar, narración y decisiones.
- `AffinityCard` — afinidad, razones y CTA *Vívela*.
- `ConsentGate` — envuelve las acciones de escritura y abre el modal.
- `LoopProgress` — Explorar · Vivir · Contrastar · Conectar por carrera.

## Estado

- TanStack Query para los datos del servidor.
- Sin consentimiento: el recorrido se guarda en `sessionStorage` (no persiste en el servidor).

## Accesibilidad y rendimiento

Tailwind con tokens de contraste AA, `prefers-reduced-motion`, imágenes livianas (ilustraciones SVG) y división de código por ruta (NFR-002, NFR-004).
