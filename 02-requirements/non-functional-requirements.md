# Requisitos no funcionales

| ID | Categoría | Requisito | Verificación |
|----|-----------|-----------|--------------|
| NFR-001 | Dispositivo | Mobile-first; usable a 360 px de ancho en un Android de gama media | Prueba manual en un dispositivo del equipo |
| NFR-002 | Rendimiento | Carga inicial de menos de 3 s en 4G con bundle JS inicial de 250 KB gzip o menos | Lighthouse móvil y tamaño del build |
| NFR-003 | Rendimiento IA | Primer token de la simulación en menos de 3 s (p50); tiempo máximo de 8 s antes del fallback | Log de latencias en la demo |
| NFR-004 | Accesibilidad | Contraste WCAG AA, navegable con teclado, botones táctiles de al menos 44 px y texto escalable | Revisión con axe y manual |
| NFR-005 | Lenguaje | Textos legibles para 15 años, en segunda persona y sin jerga técnica sin explicar | Revisión del UI/UX y del Pitch Lead |
| NFR-006 | Privacidad | Minimización: solo alias, grado, año de nacimiento, colegio opcional y respuestas. Sin género, estrato, etnia ni documento | Revisión del esquema de BD |
| NFR-007 | Privacidad | Los prompts al LLM no incluyen el alias, el colegio ni otro identificador; solo el contenido de la carrera y el texto del turno | Prueba de integración que inspecciona el payload |
| NFR-008 | Seguridad | TLS en tránsito, secretos fuera del repositorio, rate limit por IP y por sesión en los endpoints de IA | Checklist de despliegue |
| NFR-009 | Veracidad | El 100 % de las cifras visibles proviene de `DataPoint` con estado `verified` o se muestra como "por verificar" | Test de contrato sobre el render de la ficha |
| NFR-010 | Disponibilidad demo | La demo completa funciona con el LLM caído (guion estático y caché) | Ensayo con `GEMINI_API_KEY` inválida |
| NFR-011 | Costo | Tope de tokens por simulación (≈6 turnos × respuesta de 250 tokens o menos) y tope diario configurable | Config y métrica |
| NFR-012 | Trazabilidad | Cada respuesta de la IA se registra con versión del prompt, carrera, escena y resultado de las guardas (sin PII) | Tabla `ai_turn_log` |
| NFR-013 | Equidad | Mismas respuestas del test producen las mismas recomendaciones (determinismo) | Test unitario |
| NFR-014 | Mantenibilidad | Contenido separado del código (JSON semilla validado con Zod) | Revisión |
| NFR-015 | Retención | Los datos de los estudiantes se borran tras 12 meses de inactividad o a petición | Política documentada; job en P2 |
| NFR-016 | Privacidad | Panel de ciudad: solo agregados con k ≥ 20 por celda, sin desglose por colegio ni por estudiante; la demo usa solo agregados sintéticos | Test unitario de k-anonimato (AC-17) y revisión del payload (SM-12) |
| NFR-017 | Rendimiento | Ilustraciones de escena como archivos estáticos (SVG o WebP) de 100 KB o menos cada una, con carga diferida y fuera del bundle JS inicial | Tamaño del build y Lighthouse móvil |
| NFR-018 | Privacidad | Los turnos con `risk_signal` o `personal_health` no persisten el texto libre del estudiante en ninguna tabla ni log | Test de integración SM-11 |
