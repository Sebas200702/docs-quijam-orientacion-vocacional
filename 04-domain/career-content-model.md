# Modelo de contenido de carreras

Cada carrera es un paquete JSON en `seed/careers/{slug}.json`, validado con Zod (`08-technical/contracts.md`). Un paquete solo se publica si todos sus bloques obligatorios existen; las cifras pueden ir en `draft` (se mostrarán como "por verificar").

## Estructura del paquete

```jsonc
{
  "id": "enfermeria",
  "name": "Enfermería",
  "area": "salud",
  "level": "profesional",
  "durationLabel": "[DATO POR VERIFICAR — fuente sugerida: SNIES]",
  "riasecProfile": { "R": 0.5, "I": 0.6, "A": 0.1, "S": 1, "E": 0.3, "C": 0.6 },
  "summary": "Cuidas la salud de las personas en hospitales, centros de salud y comunidades, con turnos y trabajo en equipo.",
  "curriculum": [
    { "cycle": "1–4", "areaTags": ["ciencias básicas", "anatomía", "cuidado básico"],
      "highlights": ["Prácticas desde los primeros semestres"], "surprising": ["Mucha química y farmacología"] }
  ],
  "dataPoints": [
    { "kind": "salario_enganche", "unit": "COP/mes", "value": null, "status": "draft",
      "suggestedSource": "Observatorio Laboral para la Educación (MEN)" },
    { "kind": "vinculacion", "unit": "%", "value": null, "status": "draft",
      "suggestedSource": "Observatorio Laboral para la Educación (MEN)" },
    { "kind": "costo_semestre", "segment": "privada", "unit": "COP", "value": null, "status": "draft",
      "suggestedSource": "SNIES / sitio oficial de cada institución" }
  ],
  "myths": [
    { "myth": "Enfermería es solo poner inyecciones.",
      "reality": "Incluye valorar pacientes, coordinar cuidados, educar familias y gestionar servicios." }
  ],
  "studyOptions": [
    { "institution": "[institución de Barranquilla]", "programName": "Enfermería", "level": "profesional",
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
4. **Diversidad:** los protagonistas de las 4 carreras del MVP alternan géneros y ninguno refuerza el estereotipo de su carrera (por ejemplo: un enfermero o una ingeniera son válidos; lo que no se hace es "Enfermería = mujer" en todas).
5. **Lenguaje:** máximo 2 líneas por highlight, sin jerga sin explicar.
6. **Revisión:** `reviewedBy` lista quién verificó (rol, no nombre personal de estudiantes). En el MVP: Pitch Lead más un segundo miembro del equipo.

## Catálogo del MVP

| Slug | Nombre | Nivel | Área | Simulación con IA en P0 |
|------|--------|-------|------|-------------------------|
| `enfermeria` | Enfermería | profesional | salud | Sí |
| `ingenieria-sistemas` | Ingeniería de Sistemas | profesional | tecnología | Sí |
| `derecho` | Derecho | profesional | sociales | Guion estático (IA en P1) |
| `tecnologia-gestion-logistica` | Tecnología en Gestión Logística | tecnólogo (SENA y otras) | logística | Guion estático (IA en P1) |

La oferta de cada programa en Barranquilla se confirma en SNIES y en la oferta del SENA antes de marcarla `verified`.
