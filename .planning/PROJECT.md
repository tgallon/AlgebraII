# Práctica 1 — Álgebra Computacional EAFIT 2026-1

## De qué va esto

Básicamente tenemos que armar un Jupyter Notebook donde implementamos los algoritmos de
factorización QR desde cero para resolver dos problemas de mínimos cuadrados que están
intencionalmente mal condicionados: uno de restauración de imágenes históricas y otro con
datos climáticos de la NASA. Es la entrega del curso Álgebra Computacional,
Ingeniería Matemática, EAFIT.

## Lo que realmente importa

Que qr_mgs y qr_householder queden bien implementados desde cero, que demostremos claramente
por qué las ecuaciones normales colapsan numéricamente, y que ambos problemas se resuelvan bien con QR.

## Requirements

### Validados

(Ninguno todavía — hay que entregar primero)

### Activos

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

### Fuera del alcance

- Usar np.linalg.qr o scipy.linalg.qr — explícitamente prohibido por el enunciado
- scipy.linalg.solve_triangular para Parte 2 sí **está permitida** (sustitución hacia atrás)
- Cualquier funcionalidad que el enunciado no pida

## Contexto

- Universidad EAFIT, Pregrado Ingeniería Matemática
- Profesor: Diego Fonseca
- Integrantes: Tomás Gallón, Sebastian Montoya, Miguel Gomez
- El enunciado llama al archivo "Practica3" aunque la práctica se llama Práctica 1 — no pregunten por qué
- Las coordenadas en [0,1] generan inestabilidad tipo Hilbert a propósito
- Las implementaciones QR van separadas por parte (no se comparten), así lo pide el enunciado

## Restricciones

- **Stack**: Python, NumPy, Matplotlib, scikit-image, pandas, scipy (solo solve_triangular)
- **QR**: Desde cero — NO usar np.linalg.qr ni scipy.linalg.qr
- **Entrega**: 2026-05-05 23:59
- **Formato**: .ipynb completamente ejecutado + exportación directa a .pdf

## Decisiones clave

| Decisión | Por qué | Estado |
|----------|---------|--------|
| QR separado por parte | El enunciado las pide así y con nombres distintos | — Pendiente |
| Comentarios y análisis en español | Contexto académico EAFIT | — Pendiente |
| scipy.linalg.solve_triangular en Parte 2 | El enunciado lo permite explícitamente | — Pendiente |

---
*Última actualización: 2026-04-28 después de inicializar el proyecto*
