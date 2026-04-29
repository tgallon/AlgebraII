# Phase 2: Parte 1 — Rescate del Patrimonio Documental - Context

**Gathered:** 2026-04-28
**Status:** Ready for planning

<domain>
## Phase Boundary

Implementar los cuatro incisos de Parte 1 completamente en el notebook:
1. Construir la matriz de diseño A con monomios bidimensionales (j+k≤9)
2. Demostrar el colapso de las ecuaciones normales con análisis en español
3. Implementar `qr_mgs(A)` desde cero
4. Implementar `qr_householder(A)` desde cero, restaurar la imagen y analizar ortogonalidad

La implementación ya existe en el notebook; el plan debe verificar correctitud, aplicar correcciones decididas y refinar los análisis Markdown.

</domain>

<decisions>
## Implementation Decisions

### solve_triangular en Parte 1
- **NO** usar `scipy.linalg.solve_triangular` en Parte 1
- Implementar sustitución hacia atrás (back-substitution) manualmente para resolver Rĥc = Qĥᵀb
- Parte 2 puede conservar `scipy.linalg.solve_triangular` (el enunciado lo permite explícitamente allí)

### Corrección del edge case en Householder (sign convention)
- Cuando `x[0] == 0`, `np.sign(0) = 0` deja `v[0] = 0`, haciendo el reflector incorrecto
- Corregir usando: `np.sign(x[0]) + (x[0] == 0)` en lugar de `np.sign(x[0])` puro
- Esta corrección aplica a **ambas** funciones: `qr_householder` (Parte 1) y `householder_qr` (Parte 2)
- Fórmula corregida: `v[0] += (np.sign(x[0]) + (x[0] == 0)) * np.linalg.norm(x)`

### Análisis Markdown — Inciso 2 (Ecuaciones Normales)
- Ampliar la celda de análisis del inciso 2 para incluir:
  - La relación κ(AᵀA) = [κ(A)]² (el número de condición se eleva al cuadrado)
  - Cuantificación de dígitos perdidos: si κ(AᵀA) ~ 10^30 en precisión doble (~16 dígitos), quedan 0 dígitos significativos
- Los análisis del inciso 4 (conclusión Householder) están bien — no cambiar

### Análisis Markdown — Inciso 4 (Conclusión)
- Conservar el análisis actual — cubre correctamente por qué Householder es el estándar industrial

### Códigos de estudiante
- La celda de integrantes tiene `*(código)*` como placeholders
- El plan debe incluir un TODO explícito: los tres integrantes (Tomás Gallón, Sebastian Montoya, Miguel Gomez) deben agregar sus códigos/cédulas manualmente antes de la entrega

### Claude's Discretion
- Formato de la back-substitution manual (puede ser función separada o inline)
- Estilo y nombre de la función de back-substitution si se crea por separado

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

No external specs — requirements are fully captured in decisions above and en REQUIREMENTS.md.

### Requisitos académicos
- `.planning/REQUIREMENTS.md` — Requirements P1-01 a P1-06 con criterios de aceptación exactos
- `.planning/ROADMAP.md` — Success criteria de Phase 2 con las verificaciones esperadas

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- `qr_mgs(A)` (celda 14): Implementada, retorna Q (m×n) y R (n×n). Lista para uso.
- `qr_householder(A)` (celda 16): Implementada, retorna Q_hat (m×n) y R_hat (n×n). Necesita corrección del sign edge case.
- Código base (celda 3): `imagen_original`, `imagen_danada`, `X`, `Y`, `A`, `b_p1` definidos globalmente.

### Established Patterns
- Todos los comentarios y análisis en español (consistente en todo el notebook)
- Truco de restauración: `np.clip(imagen_danada - superficie + 1.0, 0, 1)` — patrón establecido
- Visualización con matplotlib subplots con títulos descriptivos en español

### Integration Points
- Cell 18 usa `solve_triangular` para ambos métodos — debe reemplazarse con back-substitution manual
- Cell 20 calcula ‖Q̂ᵀQ̂ − I‖₂ — está correcto, no tocar
- Cell 11 tiene el análisis de cancelación catastrófica — ampliar con κ(AᵀA) = [κ(A)]²

</code_context>

<specifics>
## Specific Ideas

- La back-substitution manual en Parte 1 debe implementarse con un bucle estándar (no solve_triangular)
- La corrección del sign: `(np.sign(x[0]) + (x[0] == 0))` garantiza signo +1 cuando x[0]=0
- El análisis del inciso 2 debe mencionar explícitamente los ~16 dígitos de precisión doble y cuántos consume κ(AᵀA)

</specifics>

<deferred>
## Deferred Ideas

None — discussion stayed within phase scope.

</deferred>

---

*Phase: 02-parte-1-rescate-del-patrimonio-documental*
*Context gathered: 2026-04-28*
