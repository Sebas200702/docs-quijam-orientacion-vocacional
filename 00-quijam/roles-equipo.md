# Roles del equipo — QuiJAM 2026

Los roles **no** salen de la lista teórica de QuiJAM. Salen de **lo que el proyecto necesita para ganar**: primero se definen los frentes de trabajo que exige el producto y después se asigna cada frente a quien más rinde en él. Los 5 roles oficiales se usan solo como etiqueta formal (ver la tabla del final).

## 1. Frentes de trabajo que exige el proyecto

Una demo ganadora en ~30 horas necesita estos frentes, sea cual sea la idea:

| # | Frente | Qué produce | Idea 2 (Orientación Vocacional) | Idea 1 (Copiloto Financiero) |
|---|---|---|---|---|
| F1 | **Núcleo inteligente** | El "cerebro" del producto, confiable y sin inventar | Simulación "un día en la carrera", test vocacional y recomendación explicada, todo anclado a contenido curado | Motor de recomendaciones con reglas que protegen al usuario |
| F2 | **Datos y contenido** | Información real que sostiene el producto | Pensum, salarios y empleabilidad (SNIES, Observatorio Laboral), fichas de carreras, eventos y mentores semilla | Escenarios financieros, categorías, ledger simulado y datos agregados para la ciudad |
| F3 | **Experiencia inmersiva** | El momento "wow" de la demo | Profesional virtual con voz y avatar, escenas del día a día | Visualización de metas, progreso y distribución del dinero |
| F4 | **Producto y diseño** | Que se entienda en 5 segundos y se vea profesional | Recorrido del estudiante, sistema de diseño y diapositivas | Igual |
| F5 | **Validación, narrativa y calidad** | Pruebas de que el problema es real y de que la demo no falla | Testimonios de estudiantes de 10.º y 11.º, datos verificados, guion y QA | Testimonios de universitarios y aprendices, datos verificados, guion y QA |

Transversal a todos: **dirección**, es decir, decidir el alcance, cuidar los tiempos e integrar todo.

## 2. Roles propios

| Rol propio | Persona | Frentes | Responsabilidades | Por qué esa persona |
|---|---|---|---|---|
| **Arquitecto de IA y capitán** | **Sebastián Torregroza** | F1 + dirección | Arquitectura y contratos en la primera hora. Construye el núcleo inteligente con respuestas ancladas y cacheadas para el golden path. Decide el congelamiento. Responde las preguntas técnicas. | RAG en producción (Manglara), pruebas contra respuestas inventadas y orquestación de modelos (Nexus IA). En la idea 2 suma su experiencia orientando aspirantes en la Beca Talento de la CUC y el proyecto Amelia. |
| **Ingeniero de datos y plataforma** | **Ángel Castro** | F2 | Base de datos, API, carga y limpieza de datos reales, datos semilla, script de reinicio de la demo y despliegue. | Modelado relacional, Node/Express y Supabase, Pandas y NumPy (Talento Tech) y despliegue en Vercel con Gemini (Alpine-Translate). |
| **Ingeniero de experiencias inmersivas** | **Esteban M.** | F3 | Pantallas interactivas del corazón de la demo: la simulación, con avatar o 3D si aplica. **Opera la demo en vivo.** | React, TypeScript y Next, Blender (modelado y rigging 3D) y dos hackatones encima (Barranqui-IA, DataBridge). |
| **Diseñador de producto** | **Santiago Torregroza** | F4 (y frontend del resto de pantallas) | Recorrido del usuario y sistema de diseño en Figma antes del evento. Construye las pantallas que no son la simulación. Hace las diapositivas. Responde las preguntas de usuario y experiencia. | Figma de alta fidelidad, sistemas de diseño y WCAG. Diseñó Amelia para preuniversitarios y la interfaz del avatar de Manglara, y él mismo lleva sus diseños a React. |
| **Líder de validación y pitch** | **Mateo Cantillo** | F5 | Rúbrica y reglas a las 08:00. 3 datos verificados y 3–5 testimonios reales. Guion, ensayos y cronómetro. QA del golden path cada 2 horas como usuario. Responde las preguntas de impacto y viabilidad. | Es el perfil con menos carga técnica, así que se dedica al 100% a lo que suma puntos fuera del código. Su hoja de vida destaca responsabilidad e iniciativa. |

### Respaldos

Cada frente crítico tiene un segundo responsable:

| Frente | Titular | Respaldo |
|---|---|---|
| F1 Núcleo inteligente | Sebastián | Ángel (ya integró Gemini) |
| F2 Datos y plataforma | Ángel | Sebastián |
| F3 Experiencia inmersiva | Esteban | Santiago (ya trabajó la UI del avatar de Manglara) |
| F4 Producto y diseño | Santiago | Esteban |
| F5 Validación y pitch | Mateo | Sebastián (narra el dominio, sobre todo en la idea 2) |

## 3. Supuesto a confirmar

Mateo como voz principal del pitch supone que se siente cómodo frente al jurado. Si no es así:
- Sebastián narra.
- Mateo sigue a cargo de la validación, los datos y el QA.
- La dirección técnica pasa a Ángel durante los ensayos.

## 4. Turnos de sueño, noche del día 1

| Franja | Duermen | Siguen |
|---|---|---|
| 22:00–01:00 | Mateo | Sebastián, Ángel, Esteban, Santiago |
| 01:00–03:30 | Ángel, Santiago | Sebastián, Esteban, Mateo (QA y ensayo) |
| 03:30–06:00 | Sebastián, Esteban | Ángel, Santiago, Mateo |
| 06:00–08:30 | Nadie: video de respaldo, congelamiento a las 08:30 y ensayos | Todos |

Nunca duermen a la vez el titular y el respaldo de un mismo frente.

## 5. Equivalencia formal con QuiJAM (solo para la inscripción y el jurado)

| Rol oficial QuiJAM | Lo cubre |
|---|---|
| AI Specialist | Sebastián (Arquitecto de IA) |
| Backend | Ángel (Datos y plataforma) |
| Frontend | Esteban (Experiencias inmersivas) |
| UI/UX Designer | Santiago (Diseñador de producto) |
| Pitch Lead | Mateo (Validación y pitch) |
