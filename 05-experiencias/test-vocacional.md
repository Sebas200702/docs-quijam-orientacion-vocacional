# Test vocacional y recomendación explicada

## Propósito

Dar un punto de partida rápido y explicable, no un veredicto. El cálculo está en `04-domain/matching-model.md`.

## Diseño del test

- 24 ítems (4 por dimensión), intercalados para que no se agrupen por dimensión.
- Escala: Nada (1) · Poco (2) · Bastante (3) · Mucho (4).
- Redacción: actividades concretas y cotidianas, no profesiones ("Me gusta explicarle a un compañero algo que no entendió", no "Me gustaría ser profesor").
- Neutros en género: sin ejemplos que asocien actividades a un género.
- Duración objetivo: unos 6 minutos.

## Ítems de ejemplo (2 por dimensión)

| Dim | Ítem |
|-----|------|
| R | Me gusta armar, reparar o manejar equipos. / Prefiero aprender haciendo que leyendo. |
| I | Me gusta entender por qué pasan las cosas. / Me engancho resolviendo acertijos o problemas de lógica. |
| A | Me gusta diseñar, escribir o expresar ideas de forma original. / Me fijo en cómo se ven y se sienten las cosas. |
| S | Me gusta ayudar a personas cuando están enfermas o tienen un problema. / Me gusta explicarle a un compañero algo que no entendió. |
| E | Me gusta defender una idea frente a otros. / Me animo a organizar a un grupo para lograr algo. |
| C | Me gusta que las cosas sigan un orden y un plan. / Llevo bien cuentas, listas o registros. |

El banco completo de 24 ítems se escribe el jueves en la ideación y queda en `seed/assessment-items.json`.

## Resultado

1. **Tu mapa de intereses:** gráfico de 6 barras con nombres amigables (no las letras R–C).
2. **Top 3:** afinidad (0–100) y 2 razones trazables por carrera.
3. **Fuera de tu zona:** una carrera de otra área.
4. **Aviso:** "Esto es para explorar, no un diagnóstico. Tú decides."
5. **Siguiente paso:** *Vívela* en cada tarjeta.

## Ejemplo de tarjeta (Valentina)

> **Enfermería — afinidad 98**
> Te la mostramos porque te interesa **Ayudar** e **Investigar**, que son centrales en Enfermería.
> · Marcaste *Mucho* en "Me gusta ayudar a personas cuando están enfermas o tienen un problema".
> · Marcaste *Mucho* en "Me gusta entender por qué pasan las cosas".
> [Vívela]

## Lo que el test no hace

- No usa notas, Saber 11, género, estrato ni colegio.
- No descarta carreras por duración ni costo; solo avisa.
- No se presenta como validado científicamente.
