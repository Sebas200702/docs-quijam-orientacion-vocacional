# Despliegue

## Objetivo

Web, API y PostgreSQL accesibles por HTTPS para la demo, más un plan B local.

## Flujo

Git → Build (Dockerfile por app) → Dokploy (VPS) → migración → seed → health check → verificación del recorrido de la demo.

Alternativa para el frontend: Vercel, si el VPS falla (la API sigue en Dokploy).

## Checklist (viernes 09:00)

- [ ] Variables configuradas (sin `DEMO_KEY` por defecto; `GEMINI_API_KEY` y `GEMINI_MODEL` solo en el servidor).
- [ ] Migraciones aplicadas.
- [ ] `bun run seed` sin errores del linter.
- [ ] `GET /health` → `db: ok`, `llm: ok`.
- [ ] `POST /demo/reset` y el login de Valentina funcionan.
- [ ] Batería de IA: los casos bloqueantes pasan.
- [ ] Recorrido de la demo completo en el celular del presentador con datos móviles (no solo con el wifi del evento).
- [ ] Caché de la demo precalentada.
- [ ] Video de respaldo grabado.
- [ ] `DataBadge`: revisar que no se vea ninguna cifra sin fuente.
