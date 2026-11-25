# UX — Las cuatro experiencias

Diseño funcional y de contenido en `05-experiencias/`. Aquí: pantallas, componentes y microcopy.

## 1. Explorar — test y resultados

- **Test:** una pregunta por pantalla, escala de 4 caritas o textos ("Nada / Poco / Bastante / Mucho"), barra de progreso, botón *Atrás*. 24 ítems, ≈6 min.
- **Resultados:** tarjeta por carrera con su afinidad (barra 0–100, sin decimales) y "Por qué te la mostramos" (2 razones citando sus respuestas). Una cuarta tarjeta en otro color: **Fuera de tu zona** ("No salió primero, pero comparte cosas contigo: …").
- Aviso fijo: "Esto es para explorar, no un diagnóstico. Tú decides."
- Llamado a la acción en cada tarjeta: **Vívela** (simulación).

## 2. Vivir — "un día en la carrera"

- Pantalla tipo historia: cabecera con la hora del día de la escena ("7:00 a. m. — Triage en urgencias"), lugar y protagonista ("Eres Julián, médico general de urgencias").
- Narración con streaming. Debajo, 2–3 botones de decisión y un campo opcional "Escribe tu pregunta" (280 caracteres).
- Indicador de escena (1/4 … 4/4). Botón *Salir* que guarda el progreso (P1: retomar).
- Si se activa el fallback, no se avisa del error; el texto aparece completo sin streaming.
- Al final, la **reflexión**: "¿Te viste haciendo esto?" (1–5), "Lo que más me gustó" y "Lo que no me gustó" (chips más texto opcional). Botones: *Contrastar con datos reales* y *Vivir otra carrera*.

## 3. Contrastar — ficha realista

Secciones ancladas (navegación por pestañas):

1. **En pocas palabras** (2 líneas, sin cifras).
2. **Qué vas a estudiar:** pensum por ciclos con áreas (chips) y "materias que sorprenden".
3. **Cuánto dura y cuánto cuesta:** duración y costo aproximado por semestre por tipo de institución (pública / privada / SENA).
4. **Trabajo y salario:** salario de enganche y vinculación laboral.
5. **Mitos y realidades:** 3 tarjetas que se voltean.
6. **Dónde estudiarla en Barranquilla:** lista de instituciones con nivel y modalidad.

**Componente `DataBadge`:** cada cifra muestra la fuente y el año ("Observatorio Laboral, 2024"). Si el estado es `draft`: chip ámbar "Dato por verificar — fuente sugerida: …" sin número. Al tocar el chip: "Preferimos no mostrarte un número que no hemos confirmado."

## 4. Conectar — agenda y mentores

- **Agenda:** lista por mes, filtro por carrera, tarjeta de evento (institución, tipo, fecha, lugar o virtual, gratis o con costo, enlace oficial). Botón *Me interesa*. Etiqueta "Ejemplo" en el MVP.
- **Mentores:** tarjeta con nombre de pila, cargo, institución que lo verifica y la frase "Lo que nadie te cuenta de mi carrera". Etiqueta "Perfil de ejemplo" en el MVP.
- **Preguntas:** lista pública de preguntas y respuestas aprobadas. Botón *Pregúntale*: textarea con el aviso "No compartas tu nombre, teléfono ni redes. Tu pregunta será revisada antes de publicarse." Estado: "En revisión".

## 5. Decidir

Ver `dashboard.md`.
