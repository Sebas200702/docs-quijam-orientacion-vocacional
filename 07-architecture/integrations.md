# Integraciones

| Integración | MVP | Después |
|-------------|-----|---------|
| **Gemini API** (Google AI Studio; llave solo en el servidor; ADR-006) | Real, modelo de clase Flash, con timeout de 8 s, límite de tokens y fallback | Afinar el prompt por carrera; evaluación continua |
| **Gemini Live API** (voz en tiempo real) | — | Voz del profesional virtual (P1/P2); el equipo ya la usó en producción en Manglara |
| **SNIES** (MEN) | Consulta manual; datos copiados al seed con fuente y año | Ingesta periódica del listado de programas (P2) |
| **Observatorio Laboral para la Educación** | Consulta manual | Ingesta de los indicadores de vinculación y salario de enganche (P2) |
| **SPADIES** | Solo para el pitch (contexto de deserción), marcado por verificar | Panel de impacto (P2) |
| **DANE GEIH** | Contexto local, marcado por verificar | Indicadores de mercado laboral local |
| **Calendarios de las universidades y el SENA** | Seed de ejemplo | Formulario o feed para que cada institución publique (P1/P2) |
| **Correo/SMS al acudiente** | Simulado | Proveedor transaccional con OTP (P2) |
| **Secretaría de Educación** | — | Lista oficial de colegios; despliegue por colegio (P2) |

## Regla

Ninguna integración externa es crítica para la demo: si una falla, el producto sigue con el seed y el fallback estático.
