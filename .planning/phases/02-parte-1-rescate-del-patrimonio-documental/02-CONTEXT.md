# Fase 2: Parte 1 — Rescate del Patrimonio Documental - Contexto

**Reunido:** 2026-04-28
**Estado:** Listo para planear

<domain>
## Límites de la fase

Lo que hay que implementar en el notebook son los cuatro incisos de Parte 1:
1. Construir la matriz de diseño A con monomios bidimensionales (j+k≤9)
2. Demostrar el colapso de las ecuaciones normales con análisis en español
3. Implementar `qr_mgs(A)` desde cero
4. Implementar `qr_householder(A)` desde cero, restaurar la imagen y analizar la ortogonalidad

La implementación ya existe en el notebook; el plan es verificar que esté correcta, aplicar las correcciones que decidimos y mejorar los análisis Markdown.

</domain>

<decisions>
## Decisiones de implementación

### solve_triangular en Parte 1
- **NO** usar `scipy.linalg.solve_triangular` en Parte 1
- Implementar la sustitución hacia atrás manualmente para resolver Rĥc = Qĥᵀb
- Parte 2 puede conservar `scipy.linalg.solve_triangular` (el enunciado lo permite explícitamente allí)

### Corrección del edge case en Householder (convención del signo)
- Cuando `x[0] == 0`, `np.sign(0) = 0` deja `v[0] = 0`, lo que rompe el reflector
- Corrección: `np.sign(x[0]) + (x[0] == 0)` en lugar de `np.sign(x[0])` puro
- Esta corrección aplica a **las dos** funciones: `qr_householder` (Parte 1) y `householder_qr` (Parte 2)
- Fórmula corregida: `v[0] += (np.sign(x[0]) + (x[0] == 0)) * np.linalg.norm(x)`

### Análisis Markdown — Inciso 2 (Ecuaciones Normales)
- Ampliar la celda del inciso 2 para incluir:
  - La relación κ(AᵀA) = [κ(A)]² (el cuadrado del número de condición)
  - Cuántos dígitos se pierden: si κ(AᵀA) ~ 10^30 en precisión doble (~16 dígitos), queda 0 dígitos significativos
- El análisis del inciso 4 (conclusión Householder) está bien — no tocar

### Análisis Markdown — Inciso 4 (Conclusión)
- Dejar el análisis actual — explica correctamente por qué Householder es el estándar industrial

### Códigos de estudiante
- La celda de integrantes tiene `*(código)*` como placeholders
- El plan incluye un TODO explícito: Tomás Gallón, Sebastian Montoya y Miguel Gomez tienen que agregar sus códigos/cédulas manualmente antes de la entrega

### A criterio del agente
- Formato de la back-substitution manual (función separada o inline)
- Nombre y estilo de la función si se crea por separado

</decisions>

<canonical_refs>
## Referencias canónicas

**Los agentes que planeen o implementen deben leer esto primero.**

No hay specs externas — los requisitos están capturados arriba y en REQUIREMENTS.md.

### Requisitos académicos
- `.planning/REQUIREMENTS.md` — Requisitos P1-01 a P1-06 con criterios de aceptación exactos
- `.planning/ROADMAP.md` — Criterios de éxito de la Fase 2 con las verificaciones esperadas

</canonical_refs>

<code_context>
## Lo que ya existe en el notebook

### Cosas reutilizables
- `qr_mgs(A)` (celda 14): Implementada, retorna Q (m×n) y R (n×n). Lista para usar.
- `qr_householder(A)` (celda 16): Implementada, retorna Q_hat (m×n) y R_hat (n×n). Necesita la corrección del signo.
- Código base (celda 3): `imagen_original`, `imagen_danada`, `X`, `Y`, `A`, `b_p1` definidos globalmente.

### Patrones establecidos
- Todos los comentarios y análisis en español (consistente en todo el notebook)
- Truco de restauración: `np.clip(imagen_danada - superficie + 1.0, 0, 1)` — patrón ya establecido
- Visualización con matplotlib subplots con títulos descriptivos en español

### Puntos de integración
- Celda 18 usa `solve_triangular` para los dos métodos — hay que reemplazarlo con back-substitution manual
- Celda 20 calcula ‖Q̂ᵀQ̂ − I‖₂ — está correcto, no tocar
- Celda 11 tiene el análisis de cancelación catastrófica — ampliar con κ(AᵀA) = [κ(A)]²

</code_context>

<specifics>
## Ideas específicas

- La back-substitution manual en Parte 1 va con un bucle estándar (no solve_triangular)
- La corrección del signo: `(np.sign(x[0]) + (x[0] == 0))` garantiza signo +1 cuando x[0]=0
- El análisis del inciso 2 debe mencionar explícitamente los ~16 dígitos de precisión doble y cuántos consume κ(AᵀA)

</specifics>

<deferred>
## Ideas diferidas

Ninguna — la discusión se mantuvo dentro del alcance de la fase.

</deferred>

---

*Fase: 02-parte-1-rescate-del-patrimonio-documental*
*Contexto reunido: 2026-04-28*
