# ADR-005 — Datos de menores y conexión moderada

## Estado
Aceptada (2026-11-24). Requiere revisión jurídica antes de un piloto real.

## Contexto
Los usuarios son, en su mayoría, menores de 18 años. La Ley 1581 de 2012 y su reglamentación restringen el tratamiento de sus datos y exigen la autorización del representante legal y el respeto de su interés superior. La conexión con adultos (mentores) implica riesgos de contacto indebido.

## Decisión
- Minimización: alias, grado, año de nacimiento y colegio opcional. No se recolectan género, estrato, etnia ni documento.
- Exploración sin persistencia para todos; persistencia solo con asentimiento del estudiante más autorización del acudiente.
- Sin mensajería privada. Las preguntas a mentores pasan por un filtro de contactos y moderación previa y se publican de forma anónima.
- Borrado en un clic; enlaces para compartir que expiran.
- La IA no recibe PII.
- La demo usa solo perfiles ficticios; el consentimiento está simulado y rotulado.

## Consecuencias
- Hay más fricción para guardar el progreso; se mitiga permitiendo explorar sin cuenta.
- La conexión es menos inmediata que un chat, pero segura y escalable (una respuesta sirve a muchos).
