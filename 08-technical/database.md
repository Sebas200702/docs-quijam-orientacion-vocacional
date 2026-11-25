# Base de datos

PostgreSQL + Drizzle. Nombres en snake_case. Los campos detallados están en `04-domain/domain-model.md`.

## Tablas

### Contenido (cargado desde el seed, solo lectura en runtime)
- `careers` (id text PK, name, area, level, duration_label, riasec jsonb, summary, status, content_version)
- `curriculum_blocks` (id, career_id FK, cycle, area_tags text[], highlights text[], surprising text[])
- `data_points` (id, career_id FK, kind, value numeric NULL, unit, segment, source_name, source_url, source_year, suggested_source, status, verified_by, verified_at)
  - CHECK: `status = 'verified' → value IS NOT NULL AND source_name IS NOT NULL AND source_year IS NOT NULL`
- `myths` (id, career_id FK, myth, reality, data_point_id NULL)
- `institutions` (id, name, type, city, is_quijam_ally)
- `study_options` (id, career_id FK, institution_id FK, program_name, level, modality, snies_code, status)
- `simulation_scripts` (id, career_id FK UNIQUE, protagonist jsonb, version, status)
- `simulation_scenes` (id, script_id FK, order smallint, time_label, setting, situation, choices jsonb, grounding_facts text[], static_narration) — UNIQUE(script_id, order)
- `assessment_items` (id text PK, dimension char(1), text, order)
- `events` (id, institution_id FK, title, type, career_ids text[], starts_at, ends_at, location, is_virtual, cost, official_url, is_sample)
- `mentors` (id, first_name, role, career_id FK, verified_by_institution_id FK, bio, is_sample)
- `schools` (id, name, type, city)

### Recorrido del estudiante
- `students` (id uuid PK, alias, grade, birth_year, school_id NULL, interests text[], favorite_subjects text[], preferences jsonb, is_demo, created_at, last_active_at)
- `guardian_consents` (id, student_id FK UNIQUE ON DELETE CASCADE, guardian_contact_hash, status, method, policy_version, granted_at, revoked_at)
- `assessments` (id, student_id FK CASCADE, answers jsonb, profile jsonb, model_version, created_at)
- `recommendations` (id, assessment_id FK CASCADE, career_id FK, rank text, affinity smallint, reasons jsonb)
- `simulations` (id, student_id FK CASCADE, career_id, script_version, current_scene, status, started_at, completed_at)
- `simulation_turns` (id, simulation_id FK CASCADE, scene_order, choice_id, free_text varchar(280), ai_output text, source, guard_flags text[], latency_ms)
- `reflections` (id, simulation_id FK UNIQUE CASCADE, fit_score smallint, liked text[], disliked text[], note)
- `event_interests` (student_id FK CASCADE, event_id FK, created_at) PK(student_id, event_id)
- `mentor_questions` (id, student_id FK NULL ON DELETE SET NULL, career_id, mentor_id NULL, text, status, reject_reason, answer, answered_at, created_at)
- `decisions` (id, student_id FK CASCADE, career_id NULL, confidence smallint, why, created_at)
- `share_links` (id, student_id FK CASCADE, token_hash UNIQUE, includes_decision, expires_at, revoked_at)

### Auditoría
- `ai_turn_logs` (id, simulation_turn_id FK SET NULL, prompt_version, model, input_tokens, output_tokens, guard_results jsonb, created_at) — sin texto del estudiante.
- `safety_events` (id, type ['risk_signal_shown','health_redirect_shown','contact_blocked'], career_id, created_at) — sin student_id ni texto.

## Índices
- `events(starts_at)`, GIN `events(career_ids)`
- `mentor_questions(career_id, status)`
- `simulations(student_id, career_id)`
- `share_links(token_hash)`

## Borrado (FR-004)
`DELETE FROM students WHERE id = $1` → cascada en todo el recorrido; `mentor_questions.student_id → NULL` (las preguntas publicadas quedan anónimas; las `pending` se borran antes con una transacción).

## Seed
`bun run seed` → `content/loader.ts` valida con Zod y el linter de cifras, y luego hace un upsert idempotente por `id`. `POST /demo/reset` borra los estudiantes con `is_demo = true` y recarga `demo-students.json`.
