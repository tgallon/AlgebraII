---
gsd_state_version: 1.0
milestone: v1.0
milestone_name: milestone
status: unknown
stopped_at: "Checkpoint 02-02: Tasks 1-2 complete, awaiting human-verify Task 3"
last_updated: "2026-04-29T14:37:21.440Z"
progress:
  total_phases: 4
  completed_phases: 0
  total_plans: 2
  completed_plans: 1
---

# Estado del Proyecto

**Proyecto:** Práctica 1 — Álgebra Computacional EAFIT 2026-1
**Última actualización:** 2026-04-29

## Referencia del proyecto

Ver: .planning/PROJECT.md (actualizado 2026-04-28)

**Lo que importa:** Implementar bien qr_mgs y qr_householder desde cero, demostrar el colapso numérico de las ecuaciones normales, y que ambos problemas queden bien restaurados con QR.
**Foco actual:** Fase 2 — Parte 1: Rescate del Patrimonio Documental

## Fase actual

**Fase 2:** Parte 1 — Rescate del Patrimonio Documental
- Estado: En progreso (plan 01 completo, plan 02 pendiente)
- Plan actual: 1 de 2
- Requisitos: P1-02, P1-04, P1-05 (completados)

## Estado por fase

| Fase | Estado | Notas |
|------|--------|-------|
| 1 — Setup | ✓ Completa | Esqueleto del notebook creado |
| 2 — Parte 1 | ◆ En progreso | Plan 01 listo: correcciones quirúrgicas aplicadas |
| 3 — Parte 2 | ○ Pendiente | |
| 4 — Entrega | ○ Pendiente | Deadline: 2026-05-05 23:59 |

## Bloqueantes

Ninguno.

## Decisiones tomadas

- Fase 02-01: `back_substitution` manual definida inline en celda 18 (no como celda separada), según el plan
- Fase 02-01: Convención de barra invertida simple en LaTeX mantenida — coincide con el contenido existente del notebook
- Fase 02-01: Edge case del signo en Householder corregido con `(np.sign(x[0]) + (x[0] == 0))` en las dos celdas 16 y 32

## Última sesión

- **Detenido en:** Checkpoint 02-02: Tasks 1-2 completas, esperando verificación visual (Task 3)
- **Timestamp:** 2026-04-29T14:28:06Z

## Notas

- Nombre del archivo: Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb (el enunciado dice "Practica3" aunque la práctica es la #1)
- Integrantes: Tomás Gallón, Sebastian Montoya, Miguel Gomez — los códigos de estudiante hay que añadirlos manualmente
- scipy.linalg.solve_triangular está permitida en Parte 2
