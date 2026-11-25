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
| `/ciudad` | Panel de ciudad de la Secretaría (clave del panel; rótulo de datos sintéticos) | FR-085…FR-088 |

## Componentes clave

- `DataBadge` — cifra con fuente o "por verificar" (única forma permitida de mostrar números de la ficha).
- `SceneCard` — ilustración estática de la escena (con `alt` y carga diferida), hora, lugar, narración en texto y decisiones. Botón de voz solo si FR-049 (P1) está activo.
- `CityGapChart` — barras pareadas interés/demanda por sector, celdas suprimidas y rótulo `SyntheticDataBanner`.
- `SampleBadge` — etiqueta "Ejemplo" para eventos, mentores y respuestas de ejemplo.
- `AffinityCard` — afinidad, razones y CTA *Vívela*.
- `ConsentGate` — envuelve las acciones de escritura y abre el modal.
- `LoopProgress` — Explorar · Vivir · Contrastar · Conectar por carrera.

## Estado

- TanStack Query para los datos del servidor.
- Sin consentimiento: el recorrido se guarda en `sessionStorage` (no persiste en el servidor).

## Accesibilidad y rendimiento

Tailwind con tokens de contraste AA, `prefers-reduced-motion`, ilustraciones de escena como archivos estáticos en `public/scenes/` (SVG o WebP, 100 KB o menos, carga diferida; NFR-017) y división de código por ruta (NFR-002, NFR-004).
