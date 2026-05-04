# Roadmap: Práctica 1 — Álgebra Computacional EAFIT 2026-1

**Hito:** v1.0 — Entrega 2026-05-05
**Fases:** 4 | **Requisitos:** 18 | **Todos los requisitos v1 cubiertos ✓**

---

## Resumen de fases

| # | Fase | Objetivo | Requisitos | Criterios de éxito |
|---|------|----------|------------|-------------------|
| 1 | Setup y Estructura | Notebook creado, integrantes, código base | SETUP-01..03 | 3 |
| 2 | Parte 1 | En progreso | | 4 |
| 3 | Parte 2 — Modelación Climática | Todos los incisos de Parte 2 completos | P2-01..06 | 4 |
| 4 | Pulido y Entrega | Notebook ejecutado, PDF exportado, archivos nombrados | ENTREGA-01..03 | 4 |

---

## Fase 1: Setup y Estructura del Notebook

**Objetivo:** Repositorio listo, notebook creado con el nombre correcto, celda de integrantes completa y código base corriendo.

**Requisitos:** SETUP-01, SETUP-02, SETUP-03

**Criterios de éxito:**
1. `Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb` existe en C:\AlgebraII y abre sin errores
2. Primera celda Markdown con los nombres completos: Tomás Gallón, Sebastian Montoya, Miguel Gomez (con códigos de estudiante)
3. El código base corre sin errores y muestra la imagen original + la imagen dañada en subplot

---

## Fase 2: Parte 1 — Rescate del Patrimonio Documental

**Objetivo:** Los cuatro incisos de Parte 1 implementados, corriendo y con análisis en español.

**Requisitos:** P1-01, P1-02, P1-03, P1-04, P1-05, P1-06

**Criterios de éxito:**
1. Matriz A con monomios j+k≤9; m=16384, n=55 impresos; número de condición de AᵀA comentado (tiene que ser >10^15 para evidenciar el colapso)
2. Ecuaciones normales con try-except; imagen con colapso visible; explicación de cancelación catastrófica basada en teoría
3. `qr_mgs(A)` y `qr_householder(A)` desde cero — Householder usa sign(x[0])*‖x‖*e₁ + x para estabilidad
4. La imagen restaurada con los dos algoritmos se puede leer; ‖Q̂ᵀQ̂ − I‖₂ calculada y Householder queda mucho mejor que MGS
**Planes:** 1/2 planes ejecutados
- [x] 02-01-PLAN.md — Correcciones quirúrgicas: arreglo del signo en Householder (celdas 16, 32), back_substitution manual en celda 18, expansión del análisis κ² en celda 11
- [ ] 02-02-PLAN.md — TODO de códigos en celda 0, Restart & Run All headless, verificación visual de los outputs de Parte 1


---

## Fase 3: Parte 2 — Modelación Climática

**Objetivo:** Los cuatro incisos de Parte 2 implementados, corriendo y con análisis en español.

**Requisitos:** P2-01, P2-02, P2-03, P2-04, P2-05, P2-06

**Criterios de éxito:**
1. Datos NASA cargados correctamente; filas con `***` eliminadas; años escalados a [0,1] para los cálculos numéricos
2. Vandermonde grado 12 construida; número de condición de AᵀA impreso; la gráfica del colapso muestra oscilaciones incoherentes con años 1880-actualidad en el eje x
3. `mgs_qr(A)` y `householder_qr(A)` desde cero con comentarios teóricos
4. El polinomio de Householder sobre los datos reales captura la tendencia macroclimática; ‖QᵀQ−I‖_F de Householder < MGS y se interpreta

---

## Fase 4: Pulido y Entrega

**Objetivo:** Notebook completamente ejecutado, PDF exportado y archivos con el nombre correcto listos para subir a EAFIT Interactiva.

**Requisitos:** ENTREGA-01, ENTREGA-02, ENTREGA-03

**Criterios de éxito:**
1. `Kernel → Restart & Run All` termina sin errores; todas las celdas tienen output
2. El PDF exportado tiene la misma información que el .ipynb
3. Ambos archivos nombrados `Practica3-AlgComp-Gallon-Montoya-Gomez.{ipynb,pdf}`
4. Todo el código tiene comentarios concisos; cada sección tiene celda Markdown con análisis e interpretación de resultados

---

## Criterios de completitud del hito

- [ ] 18/18 requisitos completos
- [ ] Notebook ejecutado sin errores
- [ ] Archivos subidos a EAFIT Interactiva antes del 2026-05-05 23:59
