# Despliegue

## Objetivo

Web, API y PostgreSQL accesibles por HTTPS para la demo, más un plan B local.

## Flujo

Git → Build (Dockerfile por app) → Dokploy (VPS) → migración → seed → health check → verificación del recorrido de la demo.

Alternativa para el frontend: Vercel, si el VPS falla (la API sigue en Dokploy).

## Checklist (viernes, después del congelamiento de las 08:30 y antes de la revisión técnica de las 09:30)

- [ ] Variables configuradas (sin `DEMO_KEY` por defecto; `GEMINI_API_KEY` y `GEMINI_MODEL` solo en el servidor; `CITY_PANEL_KEY` definida; `DEMO_MODE` decidido: `off`, `cache` o `static` según `contingency.md`).
- [ ] Migraciones aplicadas.
- [ ] `bun run seed` sin errores del linter.
- [ ] `GET /health` → `db: ok`, `llm: ok` y `demoMode` con el valor decidido.
- [ ] `POST /demo/reset` y el login de Valentina funcionan.
- [ ] Batería de IA: los casos bloqueantes pasan.
- [ ] Recorrido de la demo completo en el celular del presentador con datos móviles (no solo con el wifi del evento).
- [ ] Caché de la demo precalentada.
- [ ] Video de respaldo grabado (listo antes de las 07:00).
- [ ] Las 8 ilustraciones de escena cargan desde `/scenes/` en el celular del presentador.
- [ ] Panel de ciudad: carga con la clave y muestra "Datos sintéticos de demostración".
- [ ] Conectar: la etiqueta "Ejemplo" se ve en eventos, mentores y respuestas.
- [ ] `DataBadge`: revisar que no se vea ninguna cifra sin fuente.
