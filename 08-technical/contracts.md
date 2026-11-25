# Contratos

Esquemas Zod compartidos entre frontend y backend (`packages/contracts`). Extracto:

```ts
export const Dimension = z.enum(["R", "I", "A", "S", "E", "C"]);

export const AssessmentInput = z.object({
  answers: z.record(z.string(), z.number().int().min(1).max(4))
    .refine((a) => Object.keys(a).length === 24, "Se requieren 24 respuestas"),
});

export const Recommendation = z.object({
  rank: z.union([z.literal(1), z.literal(2), z.literal(3), z.literal("out_of_zone")]),
  careerId: z.string(),
  affinity: z.number().int().min(0).max(100),
  reasons: z.array(z.object({ dimension: Dimension, itemId: z.string(), answer: z.number().int() })).min(2),
  explanation: z.string().max(400),
});

export const DataPointView = z.discriminatedUnion("status", [
  z.object({ status: z.literal("verified"), kind: z.string(), value: z.union([z.number(), z.string()]),
             unit: z.string(), sourceName: z.string(), sourceYear: z.number().int(), stale: z.boolean() }),
  z.object({ status: z.literal("draft"), kind: z.string(), value: z.null(), display: z.string() }),
]);

export const TurnInput = z.union([
  z.object({ choiceId: z.string() }),
  z.object({ freeText: z.string().trim().min(1).max(280) }),
]);

export const Intent = z.enum(["story", "question_answered", "data_request", "off_topic", "personal_health", "risk_signal"]);
export const DataKind = z.enum(["pensum", "duracion", "costo", "salario", "empleabilidad", "donde_estudiar"]);

export const SimulationTurnOutput = z.object({        // salida de Gemini (no confiable)
  narration: z.string().min(1).max(1200),
  intent: Intent,
  choicesShown: z.array(z.string()).max(3),
  dataKind: DataKind.nullable(),                     // solo un tema; nunca una URL
}).strict();                                          // un linkToFicha u otro campo extra → falla → texto estático

// Lista blanca de anclas de la ficha (BR-026). El servidor arma el enlace; la IA no.
export const FICHA_ANCHORS: Record<z.infer<typeof DataKind>, string> = {
  pensum: "pensum", duracion: "duracion", costo: "costo",
  salario: "salario", empleabilidad: "empleabilidad", donde_estudiar: "donde-estudiar",
};
export const fichaLink = (slug: string, kind: z.infer<typeof DataKind> | null) =>
  `/carreras/${slug}/contrastar${kind ? `#${FICHA_ANCHORS[kind]}` : ""}`;  // slug viene de la simulación en BD

export const TurnResponse = z.object({               // respuesta de la API al frontend
  narration: z.string(),
  intent: Intent,
  linkToFicha: z.string().regex(/^\/carreras\/[a-z0-9-]+\/contrastar(#(pensum|duracion|costo|salario|empleabilidad|donde-estudiar))?$/).nullable(),
  source: z.enum(["llm", "cache", "static", "fixed"]),
  guardFlags: z.array(z.string()),
});

export const SceneView = z.object({
  order: z.number().int().min(1).max(4), timeLabel: z.string(), setting: z.string(),
  illustration: z.object({ src: z.string().startsWith("/scenes/"), alt: z.string().min(10) }),
});

export const CityInsights = z.object({
  dataOrigin: z.enum(["synthetic", "real"]),
  label: z.string(),                                  // obligatorio si synthetic
  period: z.string(), grade: z.enum(["10", "11", "all"]), minGroupSize: z.literal(20),
  studentsCounted: z.number().int(),
  sectors: z.array(z.object({
    sectorId: z.string(), name: z.string(),
    studentsInSector: z.number().int().min(20).nullable(),   // null si suppressed
    interestShare: z.number().min(0).max(1).nullable(),
    suppressed: z.boolean(),
    demand: z.object({ demandIndex: z.number().min(0).max(1).nullable(),
                       status: z.enum(["synthetic", "verified", "draft"]), suggestedSource: z.string() }),
    gap: z.enum(["low_interest", "balanced", "high_interest"]).nullable(),
    relatedCareers: z.array(z.string()),
  }).strict()),                                        // sin campos de estudiante o colegio
  suppressedCells: z.number().int(),
});

export const QuestionInput = z.object({
  careerId: z.string(), mentorId: z.string().optional(),
  text: z.string().trim().min(10).max(400),
});

export const DecisionInput = z.object({
  careerId: z.string().nullable(), confidence: z.number().int().min(1).max(5),
  why: z.string().trim().min(5).max(600),
});

export const CareerPackage = z.object({ /* ver 04-domain/career-content-model.md */ });
```

## Errores

```json
{ "error": { "code": "CONSENT_REQUIRED", "message": "Necesitamos la autorización de tu acudiente.", "requestId": "…" } }
```

| Código | HTTP | Cuándo |
|--------|------|--------|
| `VALIDATION_ERROR` | 400 | Zod falla |
| `UNAUTHENTICATED` | 401 | Sin sesión o sin clave del panel de ciudad |
| `CONSENT_REQUIRED` | 403 | Menor sin autorización en una acción ✍ |
| `NOT_FOUND` | 404 | |
| `SHARE_EXPIRED` | 410 | Enlace vencido o revocado |
| `CONTACT_INFO_DETECTED` | 422 | Pregunta con datos de contacto |
| `SIMULATION_NOT_AVAILABLE` | 409 | Guion no verificado |
| `RATE_LIMITED` | 429 | |
| `INTERNAL` | 500 | Sin detalles internos |

Nota: un fallo del LLM **no** es un error HTTP; la respuesta es 200 con `source: "static"`.

## Versionado

- `contentVersion` en cada paquete de carrera.
- `promptVersion` en `ai_turn_logs` (`simulation.v1`, …).
- `modelVersion` del motor de recomendación en `assessments` (`matching.v1`).
