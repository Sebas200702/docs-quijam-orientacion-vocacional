# ADR-003 — Contenido curado como única fuente de la IA

## Estado
Aceptada (2026-11-24).

## Contexto
La simulación necesita sonar real sin inventar. Las cifras de salario y empleabilidad son las más sensibles y las más fáciles de alucinar.

## Decisión
- La IA recibe solo el guion de la carrera (escena, consecuencias y `groundingFacts` cualitativos). Sin web ni RAG abierto en el MVP.
- Las cifras viven solo en `DataPoint`, con fuente, año y estado; la IA nunca las recibe ni las emite.
- Si el estudiante pide datos, se redirige a la ficha (`intent: data_request`).
- Un dato no verificado se muestra como "Dato por verificar" con fuente sugerida.

## Consecuencias
- Cada carrera nueva cuesta trabajo de curaduría; se acepta, porque ese contenido es el activo del producto.
- La honestidad del dato se vuelve un diferenciador visible en la demo.
