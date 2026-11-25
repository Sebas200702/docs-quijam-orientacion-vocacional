# Reto y alineación — QuiJAM 2026

## El reto

QuiJAM 2026 (26 y 27 de noviembre de 2026, Barranquilla; organiza Tecnoparque SENA con la Alcaldía de Barranquilla) plantea un reto único:

> "¿Cómo usar tecnología, innovación y talento joven para mejorar la calidad de vida de los ciudadanos de Barranquilla?"

La entrega final debe "explicar el problema, presentar la solución y mostrar una prueba o prototipo de lo construido". Las bases aclaran que "no necesitan una aplicación" y que "lo esencial es mostrar cómo la solución responde a una necesidad real de la ciudad".

## Eje que atacamos

**Economía y oportunidades** — "Impulsa el talento y los negocios locales. Abre caminos hacia el empleo, el emprendimiento y la inclusión."

Rumbo abre el primer camino hacia el empleo: elegir bien qué estudiar. Un joven que elige con información real llega a una formación que termina y que conecta con un empleo posible en su ciudad.

Eje secundario: datos y tecnología ("Transforma datos en mejores decisiones. Conecta la tecnología con las necesidades de la ciudad."). Rumbo lo cumple en dos niveles:

- **Estudiante:** convierte datos oficiales dispersos (SNIES, Observatorio Laboral) en una decisión concreta de un joven de 16 años.
- **Ciudad:** el **panel de ciudad** (cierre de la demo) muestra a la Secretaría de Educación, en agregado y sin datos personales, los intereses vocacionales de los jóvenes frente a la demanda laboral de los sectores estratégicos de Barranquilla (puerto y logística, tecnología, salud…). En la demo usa datos sintéticos rotulados; ver `03-ux/panel-ciudad.md`.

## La necesidad real

| Hecho | Estado |
|-------|--------|
| Las universidades abren espacios de exploración vocacional, pero son cortos y esporádicos. Ejemplo: "Descubre" de la CUC, que según el equipo ocurre dos veces al año durante dos o tres días. | Testimonio del equipo; confirmar frecuencia y cupos con la CUC. |
| Proporción de estudiantes que abandonan o cambian de carrera en los primeros semestres | `[DATO POR VERIFICAR — fuente sugerida: SPADIES / Ministerio de Educación Nacional]` |
| Número de estudiantes de grado 10 y 11 en colegios oficiales de Barranquilla | `[DATO POR VERIFICAR — fuente sugerida: Secretaría de Educación Distrital de Barranquilla / SIMAT]` |
| Número de orientadores escolares por estudiante en colegios oficiales del Distrito | `[DATO POR VERIFICAR — fuente sugerida: Secretaría de Educación Distrital de Barranquilla]` |
| Tasa de tránsito inmediato de la media a la educación superior en el Atlántico | `[DATO POR VERIFICAR — fuente sugerida: MEN, indicadores de tránsito inmediato]` |

## Por qué mejora la calidad de vida de los barranquilleros

1. **Menos deserción, menos deuda y menos tiempo perdido.** Cada semestre que un estudiante cursa en una carrera equivocada cuesta matrícula, transporte y años de vida. Para una familia de colegio oficial ese costo pesa más.
2. **Igualdad de acceso a la orientación.** Hoy vive la experiencia quien logra un cupo en un evento de dos o tres días. Rumbo está abierto todo el año, desde un celular, para cualquier colegio.
3. **Talento alineado con la ciudad.** Mostrar rutas técnicas y tecnológicas (SENA) junto con las profesionales, y su empleabilidad real, conecta a los jóvenes con sectores con demanda en Barranquilla (logística y puerto, salud, servicios, tecnología). La demanda por sector va marcada como `[DATO POR VERIFICAR — fuente sugerida: Observatorio Laboral para la Educación / DANE GEIH Barranquilla AM]`.
4. **Familias que deciden juntas.** El resumen compartible lleva la conversación a la casa con datos y no con suposiciones.

## Aliados de QuiJAM como camino de escala

- **Universidad de la Costa (CUC)** creó "Descubre" y es institución de QuiJAM. Rumbo no compite con Descubre: lo extiende. Antes del evento, el estudiante llega con una carrera explorada; después del evento, sigue en contacto. La agenda de Descubre podría aparecer dentro de Rumbo (en el prototipo es un evento de ejemplo). Hay que preguntar a la CUC si podemos usar el nombre "Descubre" en la demo; si no, lo mencionamos solo como ejemplo.
- **Universidad Simón Bolívar, Universidad Autónoma del Caribe y la quinta institución** (logo "sergio", probablemente Sergio Arboleda, sin verificar) podrían publicar eventos y mentores en el mismo catálogo (en el prototipo, todos son datos de ejemplo).
- **SENA / Tecnoparque**, organizador, aporta las rutas técnicas y tecnológicas que el estudiante debe ver al mismo nivel que las universitarias.
- **Alcaldía de Barranquilla**, a cargo de los colegios oficiales, es el canal de escala y el cliente: la Secretaría de Educación licenciaría Rumbo para los colegios oficiales (B2G, gratis para el estudiante), lo llevaría a las clases de orientación de grado 10 y 11 y recibiría el panel de ciudad; cada orientador tendría su panel por colegio (P1). Camino: piloto en algunos colegios oficiales → evaluación → escala (`01-product/prd.md` §13). Rumbo no reemplaza al orientador; le da tiempo y datos. Hoy no existe ningún acuerdo con la Alcaldía.
- **Universidades y SENA** entrarían como aliados de contenido gratuitos: publican eventos y validan su información, sin pagar nunca por aparecer en las recomendaciones.

## Talento joven

- Lo construye un equipo joven con los cinco roles de QuiJAM.
- El usuario es talento joven antes de entrar al mercado laboral.
- Los mentores podrían ser egresados recientes de las universidades aliadas: talento joven que orienta a talento joven (visión; en el prototipo son perfiles de ejemplo).

## Lo que no es

- No es un test que dicta la carrera. La IA orienta; el estudiante decide (ADR-002).
- No es un directorio de publicidad universitaria. Las universidades aparecen por la carrera, no porque paguen.
- No es un sistema que vigile estudiantes. El panel de ciudad solo muestra agregados de 20 o más estudiantes y no influye en las recomendaciones.
- No es una plataforma de chat entre adultos y menores. La conexión es moderada y grupal (ADR-005).
