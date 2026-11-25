# Estrategia para ganar QuiJAM 2026

> No vamos a participar. Vamos a ganar. Cada decisión de estas 48 horas se mide con una pregunta: **¿esto sube nuestra nota frente al jurado?**

Este documento sirve para cualquiera de las dos ideas: Copiloto Financiero u Orientación Vocacional. La elección entre ellas está en [`comparativa-ideas.md`](./comparativa-ideas.md). El reparto de personas está en [`roles-equipo.md`](./roles-equipo.md).

---

## 1. Entender cómo se gana

**Quién evalúa.** Hay tres públicos:
- La Alcaldía de Barranquilla, dueña del reto.
- Las universidades y el SENA (CUC, Unisimón, UAC y otras).
- Las empresas del Draft, que buscan talento.

**Qué les importa** (inferido mientras no tengamos la rúbrica oficial):

| Criterio probable | Lo que el jurado necesita ver | Cómo lo demostramos |
|---|---|---|
| Pertinencia al reto | Un problema real de **ciudadanos de Barranquilla** | Personas barranqueras, datos locales verificados, testimonios reales |
| Impacto | A quién mejora la vida, cuántos y cómo se mide | 1 métrica de impacto clara y un escenario de escala con aliados |
| Innovación | Algo que hoy no existe o se hace mal | Diferenciador en una frase, sin jerga |
| Prototipo funcional | Que funcione de verdad, en vivo | Golden path completo y sin fallos (§4) |
| Viabilidad | Que se pueda continuar después del evento | Ruta con aliados reales (Alcaldía, CUC, SENA) y costo bajo |
| Pitch y equipo | Claridad, seguridad, trabajo en equipo | Pitch ensayado ≥5 veces y respuestas preparadas (`preguntas-jurado.md`) |

**Acción obligatoria a las 08:00 del día 1:** pedir a la organización la **rúbrica de evaluación con sus pesos**, la duración del pitch, si se permite código previo y si hay proyector. Con la rúbrica real se ajusta esta tabla en 15 minutos.

---

## 2. Antes del evento: el partido se gana acá

Tenemos ~2 días. Quien llega preparado le saca horas de ventaja a quien llega a "idear".

| # | Entregable previo | Responsable | Por qué gana puntos |
|---|---|---|---|
| 1 | **Elegir la idea principal** esta noche, con la otra como respaldo | Todo el equipo | Cero debate en el evento |
| 2 | **3 datos reales verificados**, con su fuente, para reemplazar los `[DATO POR VERIFICAR]` clave | Validación y pitch (Mateo) | Un número real vale más que diez supuestos |
| 3 | **3–5 conversaciones con usuarios reales** (estudiantes o bachilleres), con una cita textual o un audio corto | Mateo + Santiago | "Validamos con usuarios" es lo que más distingue de otros equipos |
| 4 | Diseño base: paleta, tipografía, componentes y las 5 pantallas del golden path en Figma | Diseñador de producto (Santiago) | El día 1 se construye, no se diseña desde cero |
| 5 | Plantilla del repo, stack probado, despliegue de prueba y llaves de LLM funcionando *(si las reglas permiten código previo)* | Datos y plataforma (Ángel) + Arquitecto (Sebastián) | Elimina el riesgo técnico de la primera hora |
| 6 | Prompts y contenido semilla (datos demo, respuestas cacheadas) | Arquitecto de IA (Sebastián) | La IA sale bien en la demo, no "a ver qué responde" |
| 7 | Primer borrador del pitch y del guion de demo | Validación y pitch (Mateo) | Se ensaya desde el día 1, no la mañana del día 2 |

Si la organización prohíbe el código previo, los puntos 4–7 se quedan en diseño, documentación y prompts. Eso sí está permitido y sigue siendo ventaja.

---

## 3. Día 1: comprender, congelar y construir

| Hora | Bloque oficial | Lo que hacemos nosotros |
|---|---|---|
| 08:00 | Registro | Pedir rúbrica y reglas (§1). Ubicar enchufes y wifi. |
| 08:30 | Apertura | Escuchar qué palabras usa la Alcaldía. **Esas palabras van al pitch.** |
| 09:00 | Conformación | Equipo ya formado. Confirmar roles y comunicar el plan. |
| 09:45 | Comprender el reto | Mapear nuestra idea al reto con el lenguaje oficial. Hablar con mentores y validar el enfoque. |
| 11:00 | Ideación | **Congelamiento de alcance a las 11:30.** Se escribe el golden path y lo que **no** se hace. Desde aquí, una idea nueva solo entra si reemplaza algo. |
| 12:30 | Almuerzo | En turnos: nunca se para todo el equipo a la vez. |
| 13:30 | Impulso técnico | Aprovechar mentores técnicos para los riesgos (LLM, despliegue). |
| 14:00 | Construcción | **Rebanada vertical primero:** el golden path de punta a punta, feo pero completo. |
| 18:00 | **Punto de control** | Tratarlo como **ensayo general**: mostrar el flujo completo y un pitch de 2 min. Anotar cada reacción del jurado o los mentores. |
| 18:30 | Noche | Pulir el golden path, hacer el diseño fino y grabar el video de respaldo. Dormir en turnos (§6). |

**Regla de oro del día 1:** a las 18:00 tiene que existir algo que funcione de principio a fin. Un producto completo al 60% le gana a uno perfecto al 30%.

---

## 4. La demo que no puede fallar

- **Golden path único:** un usuario, un caso y un recorrido de 90–120 segundos que muestra el valor completo. Todo lo demás es secundario.
- **Datos semilla fijos:** la demo siempre parte del mismo estado y se reinicia con un botón o script.
- **IA sin sorpresas:** las respuestas del golden path quedan precalculadas o cacheadas, con el LLM en vivo solo como opcional. Si el wifi cae, la demo sigue.
- **Plan B en capas:**
  1. Demo en vivo, desplegada.
  2. Demo local en una laptop.
  3. Video grabado de la demo, listo antes de las 07:00 del día 2.
- **Congelamiento de código:** a las 08:30 del día 2. Después solo se corrigen bugs del golden path. Nada nuevo.
- **Revisión técnica (09:30):** llegamos con la checklist pasada: despliegue arriba, datos reiniciados, video listo, laptop cargada.

---

## 5. El pitch que gana

**Estructura** (ajustar a la duración oficial):

1. **Gancho (20 s):** una persona real con nombre y un momento concreto de Barranquilla. Nada de "en el mundo de hoy…".
2. **Problema (30 s):** un dato verificado y por qué importa para la ciudad.
3. **Solución (20 s):** qué es, en una frase.
4. **Demo en vivo (90–120 s):** el golden path. Un integrante opera y el líder de pitch narra.
5. **Impacto (30 s):** a quién, cuántos y con qué métrica. Conexión explícita con el reto de la Alcaldía.
6. **Viabilidad y escala (20 s):** aliados reales (Alcaldía, CUC, SENA), costo y siguiente paso concreto.
7. **Cierre (10 s):** una frase memorable, más el equipo y los roles.

**Reglas:**
- Ensayar **≥5 veces con cronómetro**: 2 la noche del día 1 y 3 la mañana del día 2.
- Hacer al menos un ensayo frente a alguien ajeno al equipo, como un mentor u otro equipo.
- Repartir las preguntas del jurado por frente: lo técnico lo responde el Arquitecto de IA o Datos y plataforma, lo de usuario el Diseñador de producto y lo de impacto o negocio el líder de validación y pitch.
- Nadie lee diapositivas. Máximo 6 diapositivas, con más imagen que texto.
- Mencionar los **roles propios** (ver `roles-equipo.md`) y el aporte de cada persona, porque el Draft de empresas está mirando.

---

## 6. Operación del equipo

- **Capitán o capitana:** tiene la última palabra en alcance y tiempos. Las decisiones se toman en 2 minutos, no en 20.
- **Standups de 5 minutos** a las 11:30, 14:00, 16:00, 18:00, 22:00, 02:00 y 07:00, con tres preguntas: qué terminé, qué sigue y qué me bloquea.
- **Tablero visible** (GitHub Projects o papel) con tres columnas: Por hacer / Haciendo / Hecho en demo.
- **Turnos de sueño** de 2–3 h, escalonados. Nunca duermen a la vez dos personas del mismo frente, y el líder de pitch **duerme sí o sí**, porque el día 2 es su día.
- **Multiagentes de IA:** cada rol trabaja con su agente sobre la documentación de este repo como especificación. La documentación existe para eso: se le pasa el archivo y el requisito (FR-xxx), no se improvisa el prompt.
- **Integración temprana y frecuente:** la experiencia y la plataforma se conectan desde la primera hora con contratos (`08-technical/contracts.md`), no al final.

---

## 7. Riesgos que hacen perder, y su antídoto

| Riesgo | Antídoto |
|---|---|
| Alcance que crece | Congelamiento a las 11:30 y regla "solo entra si reemplaza" |
| Demo que falla en vivo | Datos semilla, IA cacheada y video de respaldo |
| Wifi o LLM caído | Modo offline del golden path |
| Pitch genérico | Persona barranquera, dato verificado y palabras de la Alcaldía |
| Integración a última hora | Contratos primero y rebanada vertical a las 18:00 |
| Agotamiento | Turnos de sueño y líder de pitch descansado |
| No responder bien al jurado | `preguntas-jurado.md` ensayado y respuestas repartidas por rol |

---

## 8. Más allá del podio: el Draft

Las empresas eligen talento según lo que ven:
- Cada integrante lleva su CV actualizado (ya fue pedido en la inscripción) y su LinkedIn o GitHub a mano.
- El README del repo final lista los roles y el aporte de cada persona.
- Si alguien del jurado o de las empresas se acerca, se le muestra la demo y se le da contacto.
