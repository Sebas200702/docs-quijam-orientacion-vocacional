# Preguntas probables del jurado

**1. ¿En qué se diferencia de los test vocacionales que ya existen en internet?**
Un test te da una etiqueta. Rumbo te hace vivir la carrera (simulación), te muestra la realidad con fuente (pensum, salario, empleabilidad), te conecta con personas y deja registrado tu porqué. El test es solo la puerta de entrada.

**2. ¿La IA le dice al estudiante qué estudiar?**
No. Las recomendaciones salen de un cálculo determinista y explicable (afinidad de intereses frente al perfil de la carrera). La IA solo narra la simulación y explica en lenguaje sencillo. Siempre mostramos tres opciones más una fuera de su zona, y la decisión la escribe el estudiante. Ver ADR-002.

**3. ¿Qué pasa si la IA inventa un salario o dice algo falso?**
La IA no tiene permiso de dar cifras. Si el estudiante pregunta por salarios, la IA remite a la ficha, donde cada dato tiene fuente y fecha. Si el dato no está verificado, la pantalla dice "dato por verificar". Lo mostramos en vivo en la demo. Ver `06-ai/grounding-y-alucinaciones.md`.

**4. Son menores de edad. ¿Cómo manejan sus datos?**
Aplicamos la Ley 1581 de 2012 y su reglamentación sobre datos de niños, niñas y adolescentes. Se puede explorar sin cuenta. Para guardar resultados hace falta la autorización del acudiente, se pide lo mínimo (alias, grado, colegio opcional) y no se pide género, estrato ni etnia. Nada de chat privado con adultos. En la demo, el consentimiento está simulado. Ver `08-technical/security.md`.

**5. ¿Cómo evitan sesgos de género o de estrato?**
El motor de recomendación no recibe género ni estrato: no los pedimos. Las simulaciones y las fichas usan protagonistas de distintos géneros. Tenemos pruebas que verifican que el mismo perfil de intereses produce las mismas recomendaciones cuando se cambian nombres o pronombres. Ver `06-ai/sesgos-y-seguridad-menores.md`.

**6. ¿De dónde salen los datos de salario y empleabilidad?**
De fuentes oficiales: Observatorio Laboral para la Educación (MEN) para vinculación y salario de enganche, SNIES para programas y duración, y las universidades para el pensum. En el MVP están curados a mano para cuatro carreras. Integrarlos automáticamente queda para después.

**7. ¿Esto compite con "Descubre" de la CUC?**
Lo complementa. Descubre dura pocos días al año; Rumbo prepara al estudiante antes y lo acompaña después. La agenda de Descubre aparece dentro de Rumbo. Para la CUC es un canal para llegar con estudiantes mejor preparados.

**8. ¿Quién mantiene el contenido? ¿No es caro?**
Las universidades y el SENA publican eventos y validan los pensums de sus programas. Los datos oficiales se actualizan cuando el Observatorio publica. El formato del guion de simulación permite que un orientador o un profesional revise una carrera en poco tiempo, porque son cuatro escenas estructuradas, no un libro.

**9. ¿Por qué un estudiante lo usaría?**
Porque es corto, desde el celular y se parece más a un juego de decisiones que a un formulario. Pensamos validarlo con estudiantes reales después del evento. Hoy no tenemos métricas de uso y no las inventamos.

**10. ¿Cómo escala con la Alcaldía?**
A través de las clases de orientación de grado 10 y 11 de los colegios oficiales. El orientador recibe un panel agregado y anónimo (P1) con las carreras que exploran sus estudiantes. El costo de la IA por estudiante se controla con guiones y caché. Ver `11-project/roadmap.md`.

**11. ¿Qué parte del prototipo es real y qué es simulado?**
Real: test, motor de recomendación, simulación con IA, fichas con fuentes verificadas, bitácora y comparador. Simulado: los mentores y los eventos son datos de ejemplo, el consentimiento del acudiente no envía un mensaje real y las preguntas a mentores tienen respuestas precargadas. Tabla completa en `02-requirements/mvp-scope.md`.

**12. ¿Y los estudiantes sin datos móviles o sin celular?**
La app es liviana y funciona en navegador. El resumen se puede imprimir. En la fase con colegios, se usa en la sala de sistemas durante la clase de orientación.

**13. ¿Qué pasa si un estudiante expresa angustia o algo grave en la simulación?**
Hay guardas: la IA detecta señales de riesgo, no hace terapia, muestra un mensaje de apoyo y las líneas de ayuda oficiales, y sugiere hablar con el orientador. Ver `06-ai/sesgos-y-seguridad-menores.md`.

**14. ¿Modelo de sostenibilidad?**
Gratis para el estudiante siempre. Posibles fuentes de financiación: convenio con la Secretaría de Educación, aportes de las universidades por publicar eventos y verificar sus programas (sin pagar por aparecer en las recomendaciones) y alianzas con el SENA. Es una hipótesis que no validamos en el evento.
