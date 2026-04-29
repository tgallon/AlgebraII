# Roadmap: Práctica 1 — Álgebra Computacional EAFIT 2026-1

**Milestone:** v1.0 — Entrega 2026-05-05
**Phases:** 4 | **Requirements:** 18 | **All v1 requirements covered ✓**

---

## Phase Summary

| # | Phase | Goal | Requirements | Success Criteria |
|---|-------|------|--------------|-----------------|
| 1 | Setup y Estructura | Notebook creado, integrantes, código base | SETUP-01..03 | 3 |
| 2 | 1/2 | In Progress|  | 4 |
| 3 | Parte 2 — Modelación Climática | Todos los incisos de Parte 2 completos | P2-01..06 | 4 |
| 4 | Pulido y Entrega | Notebook ejecutado, PDF exportado, archivos nombrados | ENTREGA-01..03 | 4 |

---

## Phase 1: Setup y Estructura del Notebook

**Goal:** Repositorio inicializado, notebook creado con nombre correcto, celda de integrantes y código base ejecutado.

**Requirements:** SETUP-01, SETUP-02, SETUP-03

**Success Criteria:**
1. `Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb` existe en C:\AlgebraII y abre sin errores
2. Primera celda Markdown contiene nombres completos: Tomás Gallón, Sebastian Montoya, Miguel Gomez (con códigos de estudiante)
3. Código base corre sin errores y muestra imagen original + imagen dañada en subplot

---

## Phase 2: Parte 1 — Rescate del Patrimonio Documental

**Goal:** Los cuatro incisos de Parte 1 implementados, ejecutados y con análisis en español.

**Requirements:** P1-01, P1-02, P1-03, P1-04, P1-05, P1-06

**Success Criteria:**
1. Matriz A construida con monomios j+k≤9; m=16384, n=55 impresos; número de condición de AᵀA impreso y comentado (debe ser >10^15 evidenciando colapso)
2. Ecuaciones normales intentadas con try-except; imagen con colapso mostrada; explicación de cancelación catastrófica basada en teoría
3. `qr_mgs(A)` y `qr_householder(A)` implementadas desde cero — qr_householder usa sign(x[0])*‖x‖*e₁ + x para estabilidad
4. Imagen restaurada con ambos algoritmos es legible; ‖Q̂ᵀQ̂ − I‖₂ calculada y Householder muestra valor mucho menor que MGS
**Plans:** 1/2 plans executed
- [x] 02-01-PLAN.md — Surgical edits: Householder sign fix (cells 16, 32), back_substitution manual en cell 18, expansión κ² en cell 11
- [ ] 02-02-PLAN.md — TODO de códigos en cell 0, Restart & Run All headless, human-verify de outputs Parte 1


---

## Phase 3: Parte 2 — Modelación Climática

**Goal:** Los cuatro incisos de Parte 2 implementados, ejecutados y con análisis en español.

**Requirements:** P2-01, P2-02, P2-03, P2-04, P2-05, P2-06

**Success Criteria:**
1. Datos NASA cargados correctamente; filas con `***` eliminadas; años escalados a [0,1] para cálculos numéricos
2. Vandermonde grado 12 construida; número de condición de AᵀA impreso; gráfica del colapso muestra oscilaciones incoherentes con años 1880-actualidad en eje x
3. `mgs_qr(A)` y `householder_qr(A)` implementadas desde cero con comentarios teóricos
4. Polinomio de Householder graficado sobre datos reales captura tendencia macroclimática; ‖QᵀQ−I‖_F de Householder < MGS y se interpreta

---

## Phase 4: Pulido y Entrega

**Goal:** Notebook completamente ejecutado, PDF exportado, archivos con nombre correcto listos para subir a EAFIT Interactiva.

**Requirements:** ENTREGA-01, ENTREGA-02, ENTREGA-03

**Success Criteria:**
1. `Kernel → Restart & Run All` completa sin errores; todas las celdas tienen output
2. PDF exportado contiene la misma información que el .ipynb
3. Ambos archivos nombrados `Practica3-AlgComp-Gallon-Montoya-Gomez.{ipynb,pdf}`
4. Todo el código tiene comentarios concisos; cada sección tiene celda Markdown con análisis e interpretación de resultados

---

## Milestone Completion Criteria

- [ ] 18/18 requirements complete
- [ ] Notebook ejecutado sin errores
- [ ] Archivos subidos a EAFIT Interactiva antes del 2026-05-05 23:59
