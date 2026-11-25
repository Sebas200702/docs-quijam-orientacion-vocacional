# Integraciones

| Integración | MVP | Después |
|-------------|-----|---------|
| **Gemini API** (Google AI Studio; llave solo en el servidor; ADR-006) | Real, modelo de clase Flash, con timeout de 8 s, límite de tokens y fallback | Afinar el prompt por carrera; evaluación continua |
| **Gemini Live API** (voz en tiempo real) | Opcional P1, solo si el P0 está verde; la demo no depende de ella | Voz del profesional virtual; el equipo ya la usó en producción en Manglara |
| **Generación de imágenes** | Ninguna en runtime: ilustraciones pregeneradas y revisadas antes del evento, servidas como archivos estáticos | — |
| **SNIES** (MEN) | Consulta manual; datos copiados al seed con fuente y año | Ingesta periódica del listado de programas (P2) |
| **Observatorio Laboral para la Educación** | Consulta manual | Ingesta de los indicadores de vinculación y salario de enganche (P2) |
| **SPADIES** | Solo para el pitch (contexto de deserción), marcado por verificar | Panel de impacto (P2) |
| **DANE GEIH / Servicio Público de Empleo** | Contexto local, marcado por verificar; en el panel de ciudad la demanda es sintética | Demanda laboral por sector para el panel de ciudad (piloto) |
| **Calendarios de las universidades y el SENA** | Seed de ejemplo | Formulario o feed para que cada institución publique (P1/P2) |
| **Correo/SMS al acudiente** | Simulado | Proveedor transaccional con OTP (P2) |
| **Secretaría de Educación** | Panel de ciudad con datos sintéticos (sin integración) | Cliente B2G: lista oficial de colegios, despliegue por colegio y panel con datos reales agregados (piloto/P2) |

## Regla

Ninguna integración externa es crítica para la demo: si una falla, el producto sigue con el seed y el fallback estático.
