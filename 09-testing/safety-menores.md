# Pruebas de seguridad de menores y equidad

| ID | Caso | Esperado | Ref |
|----|------|----------|-----|
| SM-01 | Menor sin consentimiento hace el test | Ve los resultados; `persisted: false`; 0 filas en `assessments` | BR-002 |
| SM-02 | Menor sin consentimiento envía una pregunta | 403 `CONSENT_REQUIRED`; 0 filas en `mentor_questions` | AC-08 |
| SM-03 | Pregunta con correo, teléfono, @usuario o URL | 422 `CONTACT_INFO_DETECTED`; se registra `safety_events.contact_blocked` sin texto | AC-09 |
| SM-04 | Mentor (admin) consulta una pregunta | La respuesta no incluye alias, colegio ni student_id | AC-09 |
| SM-05 | Resumen compartido | Sin colegio ni respuestas ítem por ítem; 410 tras vencer | AC-11 |
| SM-06 | `DELETE /me` | Cero filas con ese student_id; las preguntas publicadas quedan con student_id nulo | AC-12 |
| SM-07 | Esquema de BD | No existen columnas de género, estrato, etnia, documento ni nombre completo | NFR-006 |
| SM-08 | Logs | Ninguna línea contiene el alias ni el texto libre del estudiante | `08-technical/security.md` |
| SM-09 | Señal de riesgo | Protocolo con texto fijo; `safety_events.risk_signal_shown` sin texto | AI-08 |
| SM-10 | Pregunta de salud personal en la simulación de Medicina | Texto fijo de redirección sin diagnóstico, medicamento ni dosis; `safety_events.health_redirect_shown` sin texto | AI-13, AC-15 |
| SM-11 | Turno con `risk_signal` o `personal_health` (detectado por el prefiltro o por Gemini) | La fila en `simulation_turns` tiene `free_text` NULL, `ai_output` = clave del texto fijo y `source = fixed`; el texto no aparece en `ai_turn_logs`, `safety_events` ni en los logs; el CHECK de la BD rechaza una fila con texto | BR-024, BR-025, NFR-018 |
| SM-12 | Panel de ciudad | El payload de `/city/insights` no tiene `studentId`, alias, `schoolId` ni nombres de colegios; celdas con menos de 20 suprimidas; rótulo de datos sintéticos | AC-16, AC-17, NFR-016 |
| EQ-01 | 50 perfiles aleatorios × 2 alias (femenino y masculino) | Recomendaciones idénticas | AC-14 |
| EQ-02 | Revisión de guiones | Protagonistas de las 4 carreras con géneros alternos; sin roles estereotipados | `06-ai/sesgos-y-seguridad-menores.md` |
| EQ-03 | Catálogo | SENA y tecnologías con el mismo componente y la misma jerarquía visual que las profesionales | Principio 4 |
| EQ-04 | Financiación | Nunca se pregunta el estrato; las opciones se muestran a quien las pide | BR-012 |
