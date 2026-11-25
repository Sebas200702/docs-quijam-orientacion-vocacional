# Sesgos, estereotipos y seguridad de menores

## Sesgos y estereotipos

### Riesgos concretos
- Recomendar carreras de cuidado a mujeres e Ingeniería a hombres, o presentar Medicina (sobre todo la cirugía) como "de hombres".
- Mostrar carreras "caras" solo a quien parece tener recursos, o rutas SENA solo a estudiantes de colegio oficial.
- Narraciones con protagonistas que confirman estereotipos.
- Tratar las rutas técnicas y tecnológicas como de "segunda".

### Controles
| Control | Dónde |
|---------|-------|
| No se recolectan género, estrato, barrio ni etnia | Onboarding, BD (BR-004) |
| El motor de recomendación es determinista y solo usa intereses | `04-domain/matching-model.md` |
| Ítems del test neutros en género y redactados como actividades | `05-experiencias/test-vocacional.md` |
| Protagonistas diversos (Julián, médico general en Medicina, y Andrea, desarrolladora en Sistemas; en P1: una abogada de barrio popular, etc.). En Medicina la especialista de apoyo es una mujer y el interno un hombre, para no repetir jerarquías por género | Guiones |
| Prompt: no asumir el género del estudiante y usar lenguaje neutro (tú) | Prompt de sistema |
| SENA y tecnologías en el mismo catálogo y con el mismo diseño de tarjeta | UX |
| Financiación mostrada a quien la pida, sin preguntar estrato | BR-012, FR-055 |
| Prueba de equidad: el mismo perfil con distintos alias produce el mismo resultado | AC-14, `09-testing/safety-menores.md` |

## Seguridad de menores

### Marco legal (a validar con asesoría jurídica)
- **Ley 1581 de 2012** (protección de datos personales / habeas data), que prohíbe el tratamiento de datos de niños, niñas y adolescentes salvo los de naturaleza pública y bajo el respeto de su interés superior.
- Reglamentación de la Ley 1581 (Decreto 1377 de 2013, compilado en el Decreto 1074 de 2015) sobre el tratamiento de datos de menores: debe responder a su interés superior, asegurar el respeto de sus derechos y contar con la autorización del representante legal, previo ejercicio del derecho del menor a ser escuchado.
- **Ley 1098 de 2006** (Código de la Infancia y la Adolescencia): interés superior del menor.

Las referencias normativas las debe revisar un abogado antes de cualquier piloto con estudiantes reales. La demo no usa datos de menores reales.

### Controles de producto
1. **Minimización:** alias, grado, año de nacimiento y colegio opcional (NFR-006).
2. **Autorización del acudiente** antes de persistir datos (FR-003, BR-002) y **asentimiento del estudiante** (pantalla en lenguaje claro: qué guardamos, para qué y cómo borrarlo).
3. **Sin contacto privado con adultos** (BR-040…BR-043).
4. **IA sin PII** (BR-005, NFR-007).
5. **Borrado fácil** (FR-004) y retención limitada (NFR-015).
6. **Sin publicidad ni perfilamiento comercial.** Los datos no se venden ni se comparten con universidades.

### Protocolo de señales de riesgo (F5)
- **Detección:** palabras clave (autolesión, suicidio, abuso, violencia en casa, "no quiero vivir", etc.) más el `intent: risk_signal` de Gemini. Ante la duda, se activa el protocolo.
- **Respuesta fija (no generada por la IA):** "Lo que escribiste es importante. No estás solo/a. Puedes hablar ahora con una línea de ayuda gratuita o con tu orientador o un adulto de confianza." Más las líneas oficiales vigentes: `[DATO POR VERIFICAR — fuente sugerida: Ministerio de Salud / Secretaría de Salud de Barranquilla / ICBF (Línea 141)]`.
- No se guarda el texto: el turno queda en `simulation_turns` con `free_text` nulo y solo se registra el evento `risk_signal_shown` (sin contenido).
- La IA no intenta aconsejar.
- P2: acuerdo con los colegios para que el orientador reciba una alerta, solo si existe un protocolo institucional y la autorización correspondiente.

### Preguntas de salud personal (simulación de Medicina)
- Los casos clínicos de la simulación son **ficticios y educativos**. La IA no da diagnósticos, medicamentos ni dosis, ni a los personajes como indicación ni al estudiante sobre sí mismo.
- **Detección:** palabras clave ("me duele", "tengo fiebre", "¿qué me tomo?", "mis síntomas", "¿será que tengo…?") más el `intent: personal_health` de Gemini.
- **Respuesta fija (no generada por la IA):** ver el texto en `05-experiencias/simulacion-dia-en-la-carrera.md` (remite a un adulto de confianza, a un profesional de salud y a la línea de emergencias). El turno queda con `free_text` nulo y se registra solo el evento `health_redirect_shown`, sin texto.
- Si también hay señal de riesgo, manda el protocolo F5.
