# Modelo de contenido de carreras

Cada carrera es un paquete JSON en `seed/careers/{slug}.json`, validado con Zod (`08-technical/contracts.md`). Un paquete solo se publica si todos sus bloques obligatorios existen; las cifras pueden ir en `draft` (se mostrarán como "por verificar").

## Estructura del paquete

```jsonc
{
  "id": "medicina",
  "name": "Medicina",
  "area": "salud",
  "level": "profesional",
  "durationLabel": "[DATO POR VERIFICAR — fuente sugerida: SNIES]",
  "riasecProfile": { "R": 0.5, "I": 0.9, "A": 0.1, "S": 1, "E": 0.3, "C": 0.6 },
  "summary": "Previenes, diagnosticas y tratas enfermedades en urgencias, consulta, hospitalización y comunidades, con turnos y trabajo en equipo.",
  "curriculum": [
    { "cycle": "básico", "areaTags": ["ciencias básicas", "anatomía", "fisiología", "bioquímica"],
      "highlights": ["Laboratorios y primeros contactos con pacientes"], "surprising": ["Mucha bioquímica, ética e investigación"] },
    { "cycle": "clínico", "areaTags": ["rotaciones clínicas", "medicina interna", "pediatría", "cirugía"],
      "highlights": ["Rotaciones por servicios de hospitales"], "surprising": ["Comunicar malas noticias también se estudia"] },
    { "cycle": "internado", "areaTags": ["práctica hospitalaria supervisada"],
      "highlights": ["Turnos reales bajo supervisión"], "surprising": ["Después viene el Servicio Social Obligatorio (año rural)"] }
  ],
  "dataPoints": [
    { "kind": "salario_enganche", "unit": "COP/mes", "value": null, "status": "draft",
      "suggestedSource": "Observatorio Laboral para la Educación (MEN)" },
    { "kind": "vinculacion", "unit": "%", "value": null, "status": "draft",
      "suggestedSource": "Observatorio Laboral para la Educación (MEN)" },
    { "kind": "costo_semestre", "segment": "privada", "unit": "COP", "value": null, "status": "draft",
      "suggestedSource": "SNIES / sitio oficial de cada institución" },
    { "kind": "servicio_social_obligatorio", "unit": "meses", "value": null, "status": "draft",
      "suggestedSource": "Ministerio de Salud" }
  ],
  "myths": [
    { "myth": "En Medicina todo es salvar vidas como en las series.",
      "reality": "Buena parte del día es escuchar, examinar, escribir la historia clínica, explicar a las familias y coordinar con el equipo; las emergencias son una parte." }
  ],
  "studyOptions": [
    { "institution": "[institución de Barranquilla]", "programName": "Medicina", "level": "profesional",
      "modality": "presencial", "sniesCode": null, "status": "draft" }
  ],
  "simulation": { "...": "ver 05-experiencias/simulacion-dia-en-la-carrera.md" },
  "interestChips": ["cuidar personas", "ciencias"],
  "contentVersion": "2026-11-26.1",
  "reviewedBy": []
}
```

## Reglas de contenido

1. **Cifras solo en `dataPoints`.** Ningún texto libre (summary, myths, escenas) puede contener cifras de salario, % o costos. Un linter del seed rechaza dígitos seguidos de `%`, `$`, "millones" o "salario mínimo" en esos campos.
2. **Fuente obligatoria para `verified`:** `sourceName`, `sourceYear` y, preferiblemente, `sourceUrl`.
3. **Fuentes aceptadas** (por tipo de dato):
   - Programas, duración, modalidad y registro: **SNIES** (MEN).
   - Salario de enganche y vinculación de recién graduados: **Observatorio Laboral para la Educación** (MEN).
   - Deserción y permanencia: **SPADIES** (MEN).
   - Mercado laboral local: **DANE** (GEIH, área metropolitana de Barranquilla).
   - Resultados Saber 11 (si se llegan a usar): **ICFES**.
   - Pensum y costos: sitio oficial de la institución, con la fecha de consulta.
   - Oferta SENA: **SENA** (portal oficial de oferta educativa).
4. **Diversidad:** los protagonistas de las 4 carreras del MVP alternan géneros y ninguno refuerza el estereotipo de su carrera (por ejemplo: un médico de urgencias y una ingeniera; lo que no se hace es "Medicina o Sistemas = hombre" ni poner siempre a las mujeres en el rol de apoyo).
5. **Lenguaje:** máximo 2 líneas por highlight, sin jerga sin explicar.
6. **Revisión:** `reviewedBy` lista quién verificó (rol, no nombre personal de estudiantes). En el MVP: Pitch Lead más un segundo miembro del equipo.

## Catálogo del MVP

| Slug | Nombre | Nivel | Área | Simulación con IA en P0 |
|------|--------|-------|------|-------------------------|
| `ingenieria-sistemas` | Ingeniería de Sistemas | profesional | tecnología | Sí (la que el equipo domina) |
| `medicina` | Medicina | profesional | salud | Sí (el otro extremo) |
| `derecho` | Derecho | profesional | sociales | Guion estático (IA en P1) |
| `tecnologia-gestion-logistica` | Tecnología en Gestión Logística | tecnólogo (SENA y otras) | logística | Guion estático (IA en P1) |

La oferta de cada programa en Barranquilla se confirma en SNIES y en la oferta del SENA antes de marcarla `verified`.
