---
phase: 02-parte-1-rescate-del-patrimonio-documental
plan: 01
subsystem: notebook
tags: [numpy, householder, qr, back-substitution, numerical-analysis]

requires: []
provides:
  - "qr_householder (cell 16) with corrected sign edge case for x[0]==0"
  - "householder_qr (cell 32, Parte 2) with same sign correction"
  - "back_substitution helper in cell 18 replacing scipy.linalg.solve_triangular"
  - "cell 11 analysis expanded with kappa(A^T A) = [kappa(A)]^2 and digit loss quantification"
affects: [02-02-verification]

tech-stack:
  added: []
  patterns:
    - "Arreglo del signo en Householder: (np.sign(x[0]) + (x[0] == 0)) maneja el caso x[0]==0"
    - "Bucle manual de back-substitution como reemplazo de scipy.linalg.solve_triangular en Parte 1"

key-files:
  created: []
  modified:
    - "Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb"

key-decisions:
  - "back_substitution manual definida inline en celda 18 (no como celda separada)"
  - "Convención de barra invertida simple en LaTeX mantenida para coherencia con el resto del notebook"
  - "Comentario en celdas 16 y 32 actualizado para mencionar explícitamente el caso borde x_1==0"

patterns-established:
  - "Convención LaTeX: barra invertida simple en el string decodificado del notebook, coincide con las celdas existentes"

requirements-completed: [P1-02, P1-04, P1-05]

duration: 5min
completed: 2026-04-29
---

# Plan 02-01: Correcciones Quirúrgicas al Notebook de Parte 1

**Tres ediciones puntuales: arreglo del signo en Householder (celdas 16 y 32), reemplazo de scipy.solve_triangular con back-substitution manual en celda 18, y expansión del análisis kappa(A^T A) = [kappa(A)]^2 en celda 11**

## Desempeño

- **Duración:** 5 min
- **Inicio:** 2026-04-29T14:23:01Z
- **Fin:** 2026-04-29T14:28:06Z
- **Tareas:** 3 (en un solo commit — todos los cambios en el mismo archivo)
- **Archivos modificados:** 1

## Lo que se hizo
- Corregido el edge case del signo en el reflector Householder (`np.sign(0) == 0` dejaba `v[0]` en cero) en las dos funciones: `qr_householder` (celda 16) y `householder_qr` (celda 32)
- Eliminado `from scipy.linalg import solve_triangular` de Parte 1 (celda 18), reemplazado con un helper `back_substitution` inline que implementa el bucle estándar de sustitución hacia atrás triangular superior
- Añadido tercer párrafo a la celda 11 de análisis Markdown cuantificando la pérdida de dígitos: `kappa(A^T A) = [kappa(A)]^2`, ~16 dígitos disponibles en doble precisión, 30 dígitos perdidos cuando `kappa(A^T A) ≈ 10^30`

## Commits de las tareas

Las tres tareas se aplicaron al mismo archivo notebook y se commitearon atómicamente:

1. **Tarea 1: Arreglo del edge case del signo (celdas 16 & 32)** — `b56a877` (feat)
2. **Tarea 2: Reemplazar solve_triangular con back_substitution (celda 18)** — `b56a877` (feat)
3. **Tarea 3: Ampliar análisis Inciso 2 (celda 11)** — `b56a877` (feat)

**Metadatos del plan:** (commit final pendiente)

## Archivos creados/modificados
- `Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb` — celdas 11, 16, 18, 32 modificadas; todas las demás intactas

## Decisiones tomadas
- Las tres tareas en un solo commit atómico ya que son ediciones quirúrgicas al mismo archivo y no había beneficio en separarlas
- Helper `back_substitution` inline en celda 18 según lo especificado (no como celda nueva)
- Convención de barra invertida simple en LaTeX para coincidir con las celdas existentes del notebook

## Desviaciones del plan

### Problemas auto-corregidos

**1. [Regla 1 - Bug] Corrupción de secuencias de escape de Python en el append de celda 11**
- **Detectado en:** Tarea 3 (append de celda 11)
- **El problema:** Python interpretó `\varepsilon` como `\x0b` (tab vertical) + `arepsilon`, `\approx` como campana + `pprox`, `\top` como tab + `op` en literales de cadena — corrompiendo el contenido LaTeX
- **Solución:** Se reconstruyó el texto del append usando `chr(92)` para cada barra invertida LaTeX para evitar la interpretación de secuencias de escape de Python
- **Archivos modificados:** Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb (celda 11)
- **Verificación:** Todos los criterios de aceptación verificados vía chequeos de Node.js; `\varepsilon`, `\approx`, `\kappa`, `\top` presentes correctamente
- **Commiteado en:** b56a877

**2. [Regla 1 - Bug] Inconsistencia de doble barra invertida en el primer intento de corrección**
- **Detectado en:** Iteración de Tarea 3
- **El problema:** El primer intento usó `chr(92)*2` produciendo `\\kappa` (doble barra) en el string decodificado, mientras que el notebook existente usa la convención de barra simple
- **Solución:** Cambiado a `chr(92)` (barra simple) para coincidir con la convención del notebook
- **Archivos modificados:** Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb (celda 11)
- **Verificación:** Chequeo Node.js `s.includes(backslash+'kappa(A^'+backslash+'top A) = ['+backslash+'kappa(A)]^2')` pasa
- **Commiteado en:** b56a877

---

**Total de desviaciones:** 2 auto-corregidas (2 bugs de Regla 1 por manejo de secuencias de escape de Python)
**Impacto en el plan:** Las dos correcciones eran necesarias para el renderizado correcto del LaTeX. Sin scope creep.

## Problemas encontrados
- Las secuencias de escape de Python (`\v`, `\a`, `\t`) en literales de cadena corrompen silenciosamente comandos LaTeX (`\varepsilon`, `\approx`, `\top`). Se resolvió usando `chr(92)` para construir las barras invertidas.

## Setup requerido del usuario
Ninguno — no se requiere configuración de servicio externo.

## Preparación para la siguiente fase
- El notebook tiene las tres correcciones de Parte 1 aplicadas: arreglo del signo, sin scipy en Parte 1, análisis del Inciso 2 expandido
- Listo para plan 02-02: Restart & Run All + verificación visual
- Celdas 14, 15, 17, 19, 20, 21 confirmadas sin modificar
- Validación nbformat pasa (39 celdas, notebook válido)

---
*Fase: 02-parte-1-rescate-del-patrimonio-documental*
*Completado: 2026-04-29*
