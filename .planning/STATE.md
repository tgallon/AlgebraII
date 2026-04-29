# Project State

**Project:** Práctica 1 — Álgebra Computacional EAFIT 2026-1
**Last updated:** 2026-04-29

## Project Reference

See: .planning/PROJECT.md (updated 2026-04-28)

**Core value:** Implementar correctamente qr_mgs y qr_householder desde cero, demostrar el colapso numérico de las ecuaciones normales, y restaurar satisfactoriamente ambos problemas con QR.
**Current focus:** Phase 2 — Parte 1: Rescate del Patrimonio Documental

## Current Phase

**Phase 2:** Parte 1 — Rescate del Patrimonio Documental
- Status: In Progress (plan 01 complete, plan 02 pending)
- Current Plan: 1 of 2
- Requirements: P1-02, P1-04, P1-05 (completed)

## Phase Status

| Phase | Status | Notes |
|-------|--------|-------|
| 1 — Setup | ✓ Complete | Notebook skeleton created |
| 2 — Parte 1 | ◆ In Progress | Plan 01 done: surgical edits applied |
| 3 — Parte 2 | ○ Pending | |
| 4 — Entrega | ○ Pending | Deadline: 2026-05-05 23:59 |

## Blockers

None.

## Decisions

- Phase 02-01: Manual back_substitution defined inline in cell 18 (not as a separate cell), consistent with plan spec
- Phase 02-01: Single-backslash LaTeX convention maintained in notebook — matches existing cell content
- Phase 02-01: Householder sign edge case fixed with `(np.sign(x[0]) + (x[0] == 0))` in both cells 16 and 32

## Last Session

- **Stopped at:** Completed 02-01-PLAN.md (surgical corrections to Parte 1 notebook)
- **Timestamp:** 2026-04-29T14:28:06Z

## Notes

- Nombre de archivo: Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb (el enunciado dice "Practica3" aunque la práctica es la #1)
- Integrantes: Tomás Gallón, Sebastian Montoya, Miguel Gomez — los códigos de estudiante deben añadirse manualmente
- scipy.linalg.solve_triangular está permitida en Parte 2
