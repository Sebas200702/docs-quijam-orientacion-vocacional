# PRD — Rumbo

## 1. Resumen

Rumbo es una herramienta web mobile-first de orientación vocacional para grados 10 y 11. Combina cuatro experiencias (test explicado, simulación con IA, información realista y conexión con profesionales) en un solo loop que termina en una decisión registrada por el estudiante.

## 2. Problema

Elegir carrera a los 16 o 17 años con poca exposición real a las profesiones. Los espacios de exploración de las universidades son cortos y esporádicos, y la información oficial no está escrita para el estudiante. El resultado son decisiones con arrepentimiento, deserción y cambio de carrera (magnitud `[DATO POR VERIFICAR — fuente sugerida: SPADIES/MEN]`).

## 3. Oportunidad

- Las universidades aliadas de QuiJAM ya producen experiencias vocacionales (por ejemplo, Descubre de la CUC); falta continuidad.
- Los LLM permiten simular escenas interactivas a bajo costo, siempre que estén acotadas por un guion curado.
- Existen fuentes públicas (SNIES, Observatorio Laboral para la Educación) que se pueden traducir a lenguaje joven.

## 4. Visión

Que cada estudiante de colegio en Barranquilla pueda vivir, contrastar y conversar sobre al menos tres caminos antes de inscribirse en uno.

## 5. Objetivos

| ID | Objetivo | Cómo se verifica en el MVP |
|----|----------|----------------------------|
| O1 | Acceso todo el año | Todas las experiencias funcionan sin depender de un evento |
| O2 | Experiencia vivida | Simulación de 4 escenas con decisiones para al menos 2 carreras |
| O3 | Datos honestos | El 100 % de las cifras en pantalla tiene fuente o marca "por verificar" |
| O4 | Autonomía del estudiante | Ninguna pantalla dice "deberías estudiar X"; la decisión la escribe el estudiante |
| O5 | Puente a lo real | Agenda de eventos y preguntas a mentores accesibles desde cada carrera (en el MVP, con datos de ejemplo rotulados) |
| O6 | Seguridad de menores | Consentimiento, minimización de datos y conexión moderada |
| O7 | Datos para la ciudad | Panel de ciudad agregado y anónimo que compara intereses de los jóvenes con la demanda laboral de Barranquilla (datos sintéticos rotulados en la demo) |

## 6. Usuarios

Ver `personas.md`: Valentina (grado 11, colegio oficial), Andrés (grado 10, presión familiar), Luz Marina (orientadora), Carlos (mentor), Rosa (acudiente) y Diana (Secretaría de Educación, cliente del panel de ciudad).

## 7. Propuesta de valor

> Vive la carrera antes de elegirla.

## 8. Alcance funcional

| Módulo | Contenido | Prioridad |
|--------|-----------|-----------|
| Acceso y consentimiento | Modo invitado, perfil con alias, autorización del acudiente (simulada en el MVP), borrar datos | P0 |
| Onboarding | Grado, intereses, materias, preferencias opcionales; elegir ruta | P0 |
| Explorar | Test de 24 ítems, perfil de intereses, top 3 explicado más 1 fuera de zona | P0 |
| Vivir | Simulación de 4 escenas por carrera: texto narrado por IA con una ilustración estática por escena, y fallback estático | P0 |
| Vivir — voz | Voz del profesional virtual con Gemini Live, opcional y apagable; el texto sigue siendo la base | P1 (solo si el P0 está verde) |
| Contrastar | Ficha: pensum, salario, empleabilidad, duración, costo, mitos, dónde estudiar | P0 |
| Conectar | Agenda de eventos, mentores y preguntas moderadas, todo con datos rotulados "Ejemplo"; se presenta como visión | P0 (datos de ejemplo) |
| Decidir | Bitácora, comparador, mi decisión, resumen compartible | P0 |
| Panel de ciudad | Vista agregada y anónima para la Secretaría de Educación: intereses vocacionales frente a demanda laboral por sector (datos sintéticos rotulados en la demo; k ≥ 20) | P0 (cierre de la demo) |
| Orientador | Panel agregado y anónimo por colegio | P1 |
| Recordatorios | Aviso de eventos | P1 |

Detalle en `02-requirements/`.

## 9. Catálogo del MVP

Cuatro carreras con contenido curado, elegidas para cubrir áreas distintas y una ruta tecnológica:

1. Ingeniería de Sistemas (tecnología) — simulación completa con IA, demo.
2. Medicina (salud) — simulación completa con IA, demo.
3. Derecho (ciencias sociales) — ficha, info realista y guion estático.
4. Tecnología en Gestión Logística (SENA; logística y puerto) — ficha, info realista y guion estático.

Las dos simulaciones son dos extremos a propósito: una carrera que el equipo domina (realista y fácil de curar) y una lejana a la tecnología (muestra que el formato sirve para cualquier carrera). Ver `05-experiencias/simulacion-dia-en-la-carrera.md`.

Se puede cambiar cualquiera, siempre que se mantengan una ruta técnica o tecnológica y la diversidad de áreas.

## 10. Fuera de alcance

- Diagnóstico psicológico o psicométrico clínico. El test no es un instrumento validado y la pantalla lo dice.
- Inscripción o pagos a universidades.
- Chat privado entre adultos y menores.
- Ranking de universidades o publicidad pagada en las recomendaciones.
- Integración automática con SNIES u Observatorio en el MVP (los datos se curan a mano).
- App nativa.

## 11. Éxito del MVP

En la demo, una estudiante pasa de "no sé qué estudiar" a comparar dos carreras que vivió y contrastó, con una pregunta enviada a una mentora de ejemplo y una decisión escrita por ella, y la Alcaldía ve en el panel de ciudad cómo esas decisiones, sumadas, se comparan con la demanda laboral de Barranquilla. Todo en menos de 5 minutos y sin que la IA invente una cifra.

## 12. Riesgos

| Riesgo | Mitigación |
|--------|------------|
| La IA inventa datos | Grounding en contenido curado, prohibición de cifras y redirección a la ficha (`06-ai/`) |
| La IA refuerza estereotipos | Sin género ni estrato en los datos, protagonistas diversos, pruebas de sesgo |
| Contenido mal verificado | Estados `draft`/`verified`; en pantalla solo se muestra `verified` o la marca "por verificar" |
| Alcance excesivo en 2 días | P0 estricto; Conectar con datos de ejemplo; ilustraciones pregeneradas (sin generar imágenes en runtime); voz solo P1; panel de ciudad sobre un seed sintético |
| Panel de ciudad leído como datos reales | Rótulo fijo "Datos sintéticos de demostración" en cada vista y en el payload; el pitch lo dice en voz alta |
| Exposición de menores | Ley 1581, consentimiento, sin chat privado, minimización |
| LLM caído en la demo | Guion estático y caché de la demo |
| Conflicto con la marca Descubre | Pedir permiso a la CUC; si no lo da, usar un evento genérico |
| Dependencia de un solo cliente público | Convenio por vigencias con piloto evaluado; contenido y código reutilizables por otras secretarías del Caribe |

## 13. Modelo de sostenibilidad (B2G)

**Quién paga:** la Alcaldía de Barranquilla, a través de la Secretaría de Educación Distrital, licencia Rumbo para los colegios oficiales (convenio o licencia anual). **El estudiante nunca paga.**

**Qué recibe la Secretaría:**

| Componente | Para quién | Estado |
|------------|-----------|--------|
| Plataforma completa (test, simulaciones, fichas, agenda, bitácora) | Estudiantes de 10 y 11 de los colegios oficiales | MVP P0 |
| Panel de ciudad agregado y anónimo (intereses frente a demanda laboral) | Secretaría de Educación | P0 en la demo con datos sintéticos; datos reales solo en el piloto |
| Panel de orientación por colegio | Orientadores de cada colegio | P1 |
| Curaduría y actualización del catálogo de carreras | Todos | Servicio continuo |
| Inducción a orientadores | Colegios del piloto | Fase de piloto |

**Qué cuesta operarlo (impulsores de costo):**

| Impulsor | De qué depende | Control |
|----------|---------------|---------|
| Uso de Gemini | Simulaciones por estudiante × turnos × tokens (NFR-011) | Guiones cortos, caché, tope diario de tokens |
| Hosting | VPS, base de datos, almacenamiento de ilustraciones | Arquitectura sencilla (un VPS con Dokploy) |
| Curaduría de contenido | Horas de redacción y verificación por carrera (`10-operations/curacion-contenido.md`) | Formato de 4 escenas; universidades y SENA validan su información |
| Soporte e inducción | Número de colegios | Material autoguiado para orientadores |

Costo anual por estudiante y precio de la licencia: `[DATO POR VERIFICAR — se calcula con el consumo real de tokens y hosting del piloto]`. Cualquier cifra que se diga en el pitch debe decir que es ilustrativa.

**Camino de piloto:** piloto en N colegios oficiales durante un semestre (N `[POR DEFINIR con la Secretaría de Educación]`) → evaluación con métricas acordadas (loop completo, seguridad de la decisión, uso por los orientadores) → escala a los colegios oficiales del Distrito.

**Universidades y SENA:** participan gratis como aliados de contenido (publican eventos y validan pensums y oferta). **Nunca pagan por aparecer en las recomendaciones** (BR-014): la recomendación sale solo del perfil del estudiante.

**Lo que no es fuente de ingreso:** venta de datos, publicidad o perfilamiento comercial de estudiantes.

## 14. Definición del producto

> Rumbo es una herramienta de orientación vocacional para estudiantes de grado 10 y 11 de Barranquilla que les permite, en cualquier momento del año, explorar sus intereses, vivir un día simulado en una carrera, contrastarlo con datos reales y conectar con profesionales y universidades. La IA orienta; el estudiante decide.
