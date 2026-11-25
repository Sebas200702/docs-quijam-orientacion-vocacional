# Info realista: pensum, salario, empleabilidad

## Propósito

Contrastar lo vivido en la simulación con datos reales, con su fuente visible. Es la respuesta a "esto no era lo que yo pensaba".

## Contenido por carrera

| Bloque | Qué se muestra | Fuente | Estado en el MVP |
|--------|----------------|--------|------------------|
| Pensum | Áreas por ciclos, "materias que sorprenden" | Sitio oficial de 1 o 2 instituciones de Barranquilla (fecha de consulta) | Curado a mano |
| Duración y título | Semestres y título por nivel | SNIES | `[DATO POR VERIFICAR — fuente sugerida: SNIES]` hasta consultarlo |
| Costo | Rango por semestre: pública / privada / SENA | Sitios oficiales y SNIES | `[DATO POR VERIFICAR — fuente sugerida: sitios oficiales de las instituciones / SNIES]` |
| Salario de enganche | Promedio de recién graduados por nivel de formación | Observatorio Laboral para la Educación (MEN) | `[DATO POR VERIFICAR — fuente sugerida: Observatorio Laboral para la Educación]` |
| Vinculación laboral | % de graduados que cotizan a seguridad social | Observatorio Laboral para la Educación | `[DATO POR VERIFICAR — fuente sugerida: Observatorio Laboral para la Educación]` |
| Contexto local | Sectores con demanda en Barranquilla | DANE (GEIH) y fuentes del Distrito | `[DATO POR VERIFICAR — fuente sugerida: DANE GEIH área metropolitana de Barranquilla]` |
| Mitos y realidades | 3 por carrera, cualitativos | Equipo más un mentor (revisión) | Redactado por el equipo |
| Dónde estudiar | Instituciones de Barranquilla y el área metropolitana con el programa | SNIES y oferta del SENA | Verificar código SNIES vigente |

**Todas las cifras de la tabla siguen pendientes.** El Pitch Lead las consulta antes del día 2 a las 09:30 y cambia `status` a `verified` solo con fuente y año. Lo que no alcance a verificarse se muestra en la demo como "por verificar", y eso también se presenta como una virtud del producto.

## Presentación de una cifra

```
Salario de enganche (recién graduados)
$ ███ COP/mes      ← solo si verified
Fuente: Observatorio Laboral para la Educación · Año: ____ · Nivel: profesional
ⓘ Es un promedio nacional/regional; tu caso puede variar.
```

Si está en `draft`:

```
Salario de enganche
[Dato por verificar — fuente sugerida: Observatorio Laboral para la Educación]
Preferimos no mostrarte un número que no hemos confirmado.
```

## Mitos y realidades — ejemplos (cualitativos)

- **Medicina.** Mito: "Es salvar vidas todo el día, como en las series". Realidad: mucho del trabajo es escuchar, examinar, escribir la historia clínica, explicar a pacientes y familias y trabajar en equipo; antes de ejercer hay internado y Servicio Social Obligatorio (duraciones `[DATO POR VERIFICAR — fuente sugerida: SNIES / Ministerio de Salud]`).
- **Ingeniería de Sistemas.** Mito: "Es estar solo frente al computador todo el día". Realidad: gran parte del trabajo es en equipo: reuniones, explicarle a clientes y revisar el código de otros.
- **Derecho.** Mito: "Es estar en juicios como en las series". Realidad: mucho del trabajo es leer, redactar, negociar y asesorar; los juicios son una parte.
- **Tecnología en Gestión Logística.** Mito: "Es solo cargar cajas". Realidad: es planear inventarios, rutas, tiempos y costos; en una ciudad portuaria conecta con puertos, bodegas y comercio exterior.

## Rutas y financiación (P1)

- Rutas de continuidad (por ejemplo, tecnólogo → profesional por ciclos propedéuticos, donde exista): verificar en SNIES por programa.
- Financiación: solo si el estudiante la pidió en el onboarding. Se muestran enlaces oficiales (ICETEX, becas institucionales, programas distritales o nacionales vigentes) sin cifras no verificadas. Programas vigentes: `[DATO POR VERIFICAR — fuente sugerida: ICETEX / MEN / Alcaldía de Barranquilla]`.
