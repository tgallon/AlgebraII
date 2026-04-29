# Práctica 1 — Álgebra Computacional EAFIT 2026-1

## What This Is

Implementación en Jupyter Notebook de algoritmos de factorización QR desde cero para resolver
dos problemas de mínimos cuadrados mal condicionados: restauración de imágenes históricas y
ajuste de datos climáticos de la NASA. Entrega académica para el curso Álgebra Computacional,
Ingeniería Matemática, EAFIT.

## Core Value

Implementar correctamente qr_mgs y qr_householder desde cero, demostrar el colapso numérico
de las ecuaciones normales, y restaurar satisfactoriamente ambos problemas con QR.

## Requirements

### Validated

(None yet — ship to validate)

### Active

- [ ] Notebook completamente ejecutado con todas las celdas corridas
- [ ] Primera celda Markdown con nombres, apellidos y códigos de los integrantes
- [ ] Parte 1: Matriz de diseño con monomios bidimensionales, grado d=9
- [ ] Parte 1: Demostración del colapso con ecuaciones normales (np.linalg.inv)
- [ ] Parte 1: Implementación `qr_mgs(A)` desde cero con comentarios
- [ ] Parte 1: Implementación `qr_householder(A)` desde cero con comentarios
- [ ] Parte 1: Restauración de imagen y comparación visual
- [ ] Parte 1: Análisis de ortogonalidad ||Q̂ᵀQ̂ − I||₂
- [ ] Parte 2: Carga y limpieza de datos CSV de la NASA GISTEMP
- [ ] Parte 2: Escalamiento de años a [0,1], construcción de Vandermonde grado 12
- [ ] Parte 2: Demostración del colapso con ecuaciones normales
- [ ] Parte 2: Implementación `mgs_qr(A)` desde cero
- [ ] Parte 2: Implementación `householder_qr(A)` desde cero
- [ ] Parte 2: Solución estable vía QR de Householder, gráfica con años reales
- [ ] Parte 2: Comparación ||QᵀQ − I||_F para MGS vs Householder
- [ ] Exportación a PDF con la misma información que el .ipynb
- [ ] Archivos nombrados: Practica3-AlgComp-Gallon-Montoya-Gomez.{ipynb,pdf}

### Out of Scope

- Uso de np.linalg.qr o scipy.linalg.qr — prohibido por el enunciado
- scipy.linalg.solve_triangular para Parte 2 está **permitida** (sustitución hacia atrás)
- Funcionalidades no pedidas en el enunciado

## Context

- Universidad EAFIT, Pregrado Ingeniería Matemática
- Profesor: Diego Fonseca
- Integrantes: Tomás Gallón, Sebastian Montoya, Miguel Gomez
- El enunciado usa "Practica3" en el nombre de archivo (aunque el título dice Práctica 1)
- Coordenadas en [0,1] fuerzan inestabilidad tipo Hilbert intencionalmente
- Implementaciones QR separadas por parte (no compartidas), según el enunciado

## Constraints

- **Stack**: Python, NumPy, Matplotlib, scikit-image, pandas, scipy (solo solve_triangular)
- **QR**: Implementar desde cero — NO usar np.linalg.qr ni scipy.linalg.qr
- **Timeline**: Entrega 2026-05-05 23:59
- **Format**: .ipynb completamente ejecutado + exportación directa a .pdf

## Key Decisions

| Decision | Rationale | Outcome |
|----------|-----------|---------|
| Implementaciones QR separadas por parte | El enunciado las pide en cada sección y los nombres difieren | — Pending |
| Idioma español para comentarios y análisis | Contexto académico EAFIT | — Pending |
| scipy.linalg.solve_triangular en Parte 2 | El enunciado lo permite explícitamente | — Pending |

---
*Last updated: 2026-04-28 after initialization*
