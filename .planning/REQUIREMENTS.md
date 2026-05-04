# Requirements: Práctica 1 — Álgebra Computacional EAFIT 2026-1

**Definido:** 2026-04-28
**Lo que importa:** Implementar bien qr_mgs y qr_householder desde cero, demostrar el colapso numérico de las ecuaciones normales, y que ambos problemas queden bien restaurados con QR.

## Requisitos v1

### Setup

- [ ] **SETUP-01**: El repositorio git está inicializado y el notebook tiene el nombre correcto (`Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb`)
- [ ] **SETUP-02**: La primera celda Markdown tiene los nombres completos, apellidos y códigos de los tres integrantes
- [ ] **SETUP-03**: El código base del enunciado corre sin problemas y muestra la imagen original y la dañada

### Parte 1 — Rescate del Patrimonio Documental

- [ ] **P1-01**: Matriz de diseño A con todos los monomios x^j y^k con j+k ≤ 9 (d=9); dimensiones impresas; número de condición de AᵀA calculado y comentado (tiene que evidenciar el colapso)
- [x] **P1-02**: Ecuaciones normales intentadas con np.linalg.inv en try-except; imagen resultante mostrada; explicación del fenómeno de cancelación catastrófica
- [ ] **P1-03**: `qr_mgs(A)` desde cero con comentarios que conectan el código con el proyector ortogonal de Gram-Schmidt Modificado
- [x] **P1-04**: `qr_householder(A)` desde cero con comentarios sobre el vector estable v = sign(x₁)‖x‖e₁ + x
- [x] **P1-05**: Restauración vía QR (MGS y Householder) con el truco (+1.0 y np.clip); imágenes restauradas mostradas
- [ ] **P1-06**: ‖Q̂ᵀQ̂ − I‖₂ calculada para MGS y Householder; comparación y conclusión sobre por qué Householder es el estándar industrial

### Parte 2 — Modelación Climática

- [ ] **P2-01**: Datos NASA GISTEMP cargados con pandas desde URL; columnas Year y J-D extraídas; filas con `***` eliminadas; años escalados a [0,1]
- [ ] **P2-02**: Vandermonde de grado 12 construida; número de condición de AᵀA calculado; colapso evidenciado con gráfica de años reales (1880-actualidad)
- [ ] **P2-03**: `mgs_qr(A)` desde cero retornando Q̂ y R̂ con comentarios teóricos
- [ ] **P2-04**: `householder_qr(A)` desde cero con manejo correcto del signo para evitar cancelación catastrófica
- [ ] **P2-05**: Sistema resuelto con Householder usando scipy.linalg.solve_triangular; polinomio graficado sobre datos reales con años originales en eje x; comparación visual vs colapso
- [ ] **P2-06**: ‖QᵀQ − I‖_F calculada para MGS y Householder; discusión de cuál conserva mejor la ortogonalidad

### Entrega

- [ ] **ENTREGA-01**: Notebook completamente ejecutado (todas las celdas de código tienen output visible)
- [ ] **ENTREGA-02**: Exportación directa a PDF con la misma información
- [ ] **ENTREGA-03**: Archivos exactamente nombrados `Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb` y `Practica3-AlgComp-Gallon-Montoya-Gomez.pdf`

## Requisitos v2

*(Ninguno — el alcance está completamente definido por el enunciado)*

## Fuera del alcance

| Cosa | Por qué no entra |
|------|-----------------|
| np.linalg.qr / scipy.linalg.qr | Prohibido explícitamente en el enunciado |
| Implementación compartida de QR entre partes | El enunciado pide implementaciones separadas con nombres distintos |
| Funcionalidades extra | No las pide el enunciado |

## Trazabilidad

| Requirement | Fase | Estado |
|-------------|------|--------|
| SETUP-01 | Fase 1 | Pendiente |
| SETUP-02 | Fase 1 | Pendiente |
| SETUP-03 | Fase 1 | Pendiente |
| P1-01 | Fase 2 | Pendiente |
| P1-02 | Fase 2 | Completo (02-01) |
| P1-03 | Fase 2 | Pendiente |
| P1-04 | Fase 2 | Completo (02-01) |
| P1-05 | Fase 2 | Completo (02-01) |
| P1-06 | Fase 2 | Pendiente |
| P2-01 | Fase 3 | Pendiente |
| P2-02 | Fase 3 | Pendiente |
| P2-03 | Fase 3 | Pendiente |
| P2-04 | Fase 3 | Pendiente |
| P2-05 | Fase 3 | Pendiente |
| P2-06 | Fase 3 | Pendiente |
| ENTREGA-01 | Fase 4 | Pendiente |
| ENTREGA-02 | Fase 4 | Pendiente |
| ENTREGA-03 | Fase 4 | Pendiente |

**Cobertura:**
- Requisitos v1: 18 en total
- Mapeados a fases: 18
- Sin mapear: 0 ✓

---
*Requisitos definidos: 2026-04-28*
*Última actualización: 2026-04-28*
