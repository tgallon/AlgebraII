# Requirements: Práctica 1 — Álgebra Computacional EAFIT 2026-1

**Defined:** 2026-04-28
**Core Value:** Implementar correctamente qr_mgs y qr_householder desde cero, demostrar el colapso numérico de las ecuaciones normales, y restaurar satisfactoriamente ambos problemas con QR.

## v1 Requirements

### Setup

- [ ] **SETUP-01**: Repositorio git inicializado y notebook creado con nombre correcto (`Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb`)
- [ ] **SETUP-02**: Primera celda Markdown con nombres completos, apellidos y códigos de los tres integrantes
- [ ] **SETUP-03**: Código base de preparación (provisto en el enunciado) ejecutado correctamente, mostrando imagen original y dañada

### Parte 1 — Rescate del Patrimonio Documental

- [ ] **P1-01**: Matriz de diseño A construida con todos los monomios bidimensionales x^j y^k con j+k ≤ 9 (d=9); dimensiones exactas impresas; número de condición de AᵀA calculado e interpretado
- [ ] **P1-02**: Ecuaciones normales intentadas con np.linalg.inv en bloque try-except; imagen resultante mostrada; explicación del fenómeno de cancelación catastrófica
- [ ] **P1-03**: Función `qr_mgs(A)` implementada desde cero con comentarios que relacionan el código con el proyector ortogonal de Gram-Schmidt Modificado
- [ ] **P1-04**: Función `qr_householder(A)` implementada desde cero con comentarios sobre el vector estable de reflexión v = sign(x₁)‖x‖e₁ + x
- [ ] **P1-05**: Restauración via QR (MGS y Householder) con truco de visualización (+1.0 y np.clip); imágenes restauradas mostradas
- [ ] **P1-06**: Norma ‖Q̂ᵀQ̂ − I‖₂ calculada para MGS y Householder; comparación y conclusión sobre por qué Householder es el estándar industrial

### Parte 2 — Modelación Climática

- [ ] **P2-01**: Datos NASA GISTEMP cargados vía pandas desde URL; columnas Year y J-D extraídas; filas con `***` eliminadas; años escalados a [0,1] para cálculos
- [ ] **P2-02**: Matriz de Vandermonde de grado 12 construida; número de condición de AᵀA calculado; colapso evidenciado con gráfica que muestra años reales (1880-actualidad) en eje x
- [ ] **P2-03**: Función `mgs_qr(A)` implementada desde cero retornando Q̂ y R̂ con comentarios teóricos
- [ ] **P2-04**: Función `householder_qr(A)` implementada desde cero retornando Q y R con gestión correcta del signo para evitar cancelación catastrófica
- [ ] **P2-05**: Sistema resuelto con Householder usando scipy.linalg.solve_triangular; polinomio graficado sobre datos reales con años originales en eje x; comparación visual vs colapso
- [ ] **P2-06**: Norma de Frobenius ‖QᵀQ − I‖_F calculada para MGS y Householder; discusión de cuál conserva mejor la ortogonalidad

### Entrega

- [ ] **ENTREGA-01**: Notebook completamente ejecutado (todas las celdas de código tienen output visible)
- [ ] **ENTREGA-02**: Exportación directa a PDF con la misma información
- [ ] **ENTREGA-03**: Archivos nombrados exactamente `Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb` y `Practica3-AlgComp-Gallon-Montoya-Gomez.pdf`

## v2 Requirements

*(Ninguno — el alcance está completamente definido por el enunciado)*

## Out of Scope

| Feature | Reason |
|---------|--------|
| np.linalg.qr / scipy.linalg.qr | Prohibido explícitamente por el enunciado |
| Implementación compartida de QR entre partes | El enunciado pide implementaciones separadas con nombres distintos |
| Funcionalidades adicionales al enunciado | Fuera del alcance académico |

## Traceability

| Requirement | Phase | Status |
|-------------|-------|--------|
| SETUP-01 | Phase 1 | Pending |
| SETUP-02 | Phase 1 | Pending |
| SETUP-03 | Phase 1 | Pending |
| P1-01 | Phase 2 | Pending |
| P1-02 | Phase 2 | Pending |
| P1-03 | Phase 2 | Pending |
| P1-04 | Phase 2 | Pending |
| P1-05 | Phase 2 | Pending |
| P1-06 | Phase 2 | Pending |
| P2-01 | Phase 3 | Pending |
| P2-02 | Phase 3 | Pending |
| P2-03 | Phase 3 | Pending |
| P2-04 | Phase 3 | Pending |
| P2-05 | Phase 3 | Pending |
| P2-06 | Phase 3 | Pending |
| ENTREGA-01 | Phase 4 | Pending |
| ENTREGA-02 | Phase 4 | Pending |
| ENTREGA-03 | Phase 4 | Pending |

**Coverage:**
- v1 requirements: 18 total
- Mapped to phases: 18
- Unmapped: 0 ✓

---
*Requirements defined: 2026-04-28*
*Last updated: 2026-04-28 after initial definition*
