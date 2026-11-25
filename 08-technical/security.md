# Seguridad y protección de datos de menores

## Marco normativo (validar con asesoría jurídica antes de un piloto real)

- **Ley 1581 de 2012** (Régimen general de protección de datos personales, habeas data). Principios aplicados: finalidad, libertad (autorización previa, expresa e informada), veracidad, transparencia, acceso y circulación restringida, seguridad y confidencialidad.
- **Tratamiento de datos de niños, niñas y adolescentes:** prohibido salvo datos de naturaleza pública, y según la reglamentación (Decreto 1377 de 2013, compilado en el Decreto 1074 de 2015) solo si responde a su interés superior, respeta sus derechos fundamentales y cuenta con la autorización del representante legal, previo ejercicio del derecho del menor a ser escuchado.
- **Ley 1098 de 2006** (Código de la Infancia y la Adolescencia).
- **Política de tratamiento de datos:** documento público, en lenguaje claro, versionado (`policyVersion`), con el responsable, la finalidad, los derechos y el canal de consultas. Responsable en el piloto: `[POR DEFINIR — persona o entidad responsable]`.

## Medidas

### Consentimiento
- Asentimiento del estudiante (pantalla clara) más autorización del acudiente antes de persistir datos (BR-002).
- Se registran `policy_version`, `method` y la fecha. Se guarda un hash del contacto del acudiente, no el contacto en claro (salvo que P2 requiera reenvíos: entonces se cifra en reposo).
- Revocar = borrar.
- En la demo: método `demo`, sin envío real; solo perfiles semilla ficticios.

### Minimización y finalidad
- Solo alias, grado, año de nacimiento, colegio opcional y el recorrido.
- Finalidad única: orientación vocacional del propio estudiante. Sin uso comercial, sin venta y sin compartir con instituciones.
- Los agregados para orientadores y la Secretaría son solo grupales (k ≥ 5).

### Autenticación y autorización
- Sesión con cookie `httpOnly`, `Secure` y `SameSite=Lax`; rotación al crear el perfil.
- Un estudiante solo accede a su propio recorrido (filtro por `student_id` de la sesión en cada consulta).
- Admin/moderación: clave del equipo en una variable de entorno (MVP) → roles en P2.
- Enlaces para compartir: token aleatorio de 128 bits, guardado como hash, que expira a los 7 días y se puede revocar.

### IA
- Sin PII en los prompts (NFR-007): el prompt se construye solo con el contenido de la carrera y el texto del turno; el prefiltro elimina correos y teléfonos del texto libre.
- Revisar los términos vigentes de la Gemini API sobre uso y retención de datos: en el nivel gratuito el contenido podría usarse para mejorar los productos de Google `[POR VERIFICAR en los términos de la Gemini API]`. Por eso el prompt nunca lleva PII; para un piloto con menores, evaluar el nivel de pago.
- `GEMINI_API_KEY` solo en el servidor: nunca en el frontend, en el repo ni en los logs.
- Rate limit en los endpoints de IA y tope diario de tokens.

### API e infraestructura
- Validación con Zod en todas las entradas; límite del tamaño del body.
- TLS terminado en el proxy de Dokploy (Traefik).
- Secretos en variables de entorno de Dokploy, nunca en el repositorio.
- Logs estructurados sin alias, texto libre ni IP completa (IP truncada para el rate limit).
- CORS restringido al dominio del frontend.
- Cabeceras: CSP básica, `X-Content-Type-Options` y `Referrer-Policy: no-referrer` (para no filtrar el token del resumen).

### Conexión con adultos
- Sin mensajería privada; filtro de contactos; moderación previa; mentores verificados (P2); código de conducta (`05-experiencias/conexion-profesionales.md`).

### Derechos del titular
- Acceso: `GET /journal` más la descarga (P1).
- Supresión: `DELETE /me`.
- Consultas y reclamos: canal en la política de datos `[POR DEFINIR]`.
