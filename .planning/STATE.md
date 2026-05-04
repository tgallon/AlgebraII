---
gsd_state_version: 1.0
milestone: v1.0
milestone_name: milestone
status: in_progress
stopped_at: "Fase 4 — Pulido y Entrega: pendiente (Fases 2 y 3 completas)"
last_updated: "2026-05-04T00:00:00.000Z"
progress:
  total_phases: 4
  completed_phases: 2
  total_plans: 2
  completed_plans: 2
---

# Estado del Proyecto

**Proyecto:** Práctica 1 — Álgebra Computacional EAFIT 2026-1
**Última actualización:** 2026-05-04

## Referencia del proyecto

Ver: .planning/PROJECT.md (actualizado 2026-04-28)

**Lo que importa:** Implementar bien qr_mgs y qr_householder desde cero, demostrar el colapso numérico de las ecuaciones normales, y que ambos problemas queden bien restaurados con QR.
**Foco actual:** Fase 4 — Pulido y Entrega

## Fase actual

**Fase 4:** Pulido y Entrega
- Estado: Pendiente (notebook ejecutado, falta PDF + códigos de estudiante)
- Deadline: 2026-05-05 23:59

## Estado por fase

| Fase | Estado | Notas |
|------|--------|-------|
| 1 — Setup | ✓ Completa | Esqueleto del notebook creado |
| 2 — Parte 1 | ✓ Completa | qr_mgs, qr_householder, back_substitution, análisis en español |
| 3 — Parte 2 | ✓ Completa | mgs_qr, householder_qr, datos NASA, análisis macroclimático |
| 4 — Entrega | ◆ Pendiente | Deadline: 2026-05-05 23:59 |

## Outputs verificados (2026-05-04)

- κ(A^T A) Parte 1: 2.8182e+13 (13.4 dígitos perdidos)
- κ(A^T A) Parte 2: 1.5922e+17 (colapso garantizado)
- ‖Q^T Q − I‖₂ MGS (Parte 1): 6.5064e-10
- ‖Q^T Q − I‖₂ Householder (Parte 1): 1.5972e-14 (ratio 40735x mejor)
- ‖Q^T Q − I‖_F MGS (Parte 2): 1.3475e-08
- ‖Q^T Q − I‖_F Householder (Parte 2): 3.7815e-15 (ratio 3563275x mejor)
- Figuras de restauración generadas (celdas 10, 19)
- Figuras de clima generadas
- Sin errores en ninguna celda

## Bloqueantes

Ninguno.

## Decisiones tomadas

- Fase 02-01: `back_substitution` manual definida inline en celda 18 (no como celda separada), según el plan
- Fase 02-01: Convención de barra invertida simple en LaTeX mantenida — coincide con el contenido existente del notebook
- Fase 02-01: Edge case del signo en Householder corregido con `(np.sign(x[0]) + (x[0] == 0))` en las dos celdas 16 y 32
- Fase 02-02: Celda integrantes insertada en posición 0 con TODO de códigos de estudiante

## Última sesión

- **Completado:** Fases 2 y 3 — notebook ejecutado sin errores, todos los outputs presentes
- **Pendiente:** Fase 4 — códigos de estudiante (manual) + exportar PDF
- **Timestamp:** 2026-05-04

## Notas

- Nombre del archivo: Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb (el enunciado dice "Practica3" aunque la práctica es la #1)
- Integrantes: Tomás Gallón, Sebastian Montoya, Miguel Gomez — los códigos de estudiante hay que añadirlos manualmente (TODO visible en celda 0)
- scipy.linalg.solve_triangular está permitida en Parte 2
