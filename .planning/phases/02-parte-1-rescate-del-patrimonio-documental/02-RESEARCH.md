# Phase 2: Parte 1 — Rescate del Patrimonio Documental - Research

**Researched:** 2026-04-28
**Domain:** Numerical linear algebra — QR factorization, back-substitution, condition numbers
**Confidence:** HIGH

---

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions

#### solve_triangular en Parte 1
- **NO** usar `scipy.linalg.solve_triangular` en Parte 1
- Implementar sustitución hacia atrás (back-substitution) manualmente para resolver Rĥc = Qĥᵀb
- Parte 2 puede conservar `scipy.linalg.solve_triangular` (el enunciado lo permite explícitamente allí)

#### Corrección del edge case en Householder (sign convention)
- Cuando `x[0] == 0`, `np.sign(0) = 0` deja `v[0] = 0`, haciendo el reflector incorrecto
- Corregir usando: `np.sign(x[0]) + (x[0] == 0)` en lugar de `np.sign(x[0])` puro
- Esta corrección aplica a **ambas** funciones: `qr_householder` (Parte 1) y `householder_qr` (Parte 2)
- Fórmula corregida: `v[0] += (np.sign(x[0]) + (x[0] == 0)) * np.linalg.norm(x)`

#### Análisis Markdown — Inciso 2 (Ecuaciones Normales)
- Ampliar la celda de análisis del inciso 2 para incluir:
  - La relación κ(AᵀA) = [κ(A)]² (el número de condición se eleva al cuadrado)
  - Cuantificación de dígitos perdidos: si κ(AᵀA) ~ 10^30 en precisión doble (~16 dígitos), quedan 0 dígitos significativos
- Los análisis del inciso 4 (conclusión Householder) están bien — no cambiar

#### Análisis Markdown — Inciso 4 (Conclusión)
- Conservar el análisis actual — cubre correctamente por qué Householder es el estándar industrial

#### Códigos de estudiante
- La celda de integrantes tiene `*(código)*` como placeholders
- El plan debe incluir un TODO explícito: los tres integrantes (Tomás Gallón, Sebastian Montoya, Miguel Gomez) deben agregar sus códigos/cédulas manualmente antes de la entrega

### Claude's Discretion
- Formato de la back-substitution manual (puede ser función separada o inline)
- Estilo y nombre de la función de back-substitution si se crea por separado

### Deferred Ideas (OUT OF SCOPE)
None — discussion stayed within phase scope.
</user_constraints>

---

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|-----------------|
| P1-01 | Matriz de diseño A construida con todos los monomios bidimensionales x^j y^k con j+k ≤ 9 (d=9); dimensiones exactas impresas; número de condición de AᵀA calculado e interpretado | Cell 5 builds A correctly (m=16384, n=55). Cell 6 computes cond(AᵀA). Cell 7 analysis needs the κ(AᵀA)=[κ(A)]² mention and digit-loss quantification. |
| P1-02 | Ecuaciones normales intentadas con np.linalg.inv en bloque try-except; imagen resultante mostrada; explicación del fenómeno de cancelación catastrófica | Cells 9–11 already implement this. Cell 11 analysis needs amplification of κ(AᵀA)=[κ(A)]² and explicit digit count. |
| P1-03 | Función `qr_mgs(A)` implementada desde cero con comentarios que relacionan el código con el proyector ortogonal de Gram-Schmidt Modificado | Cell 14 implements qr_mgs correctly. No changes needed. |
| P1-04 | Función `qr_householder(A)` implementada desde cero con comentarios sobre el vector estable de reflexión v = sign(x₁)‖x‖e₁ + x | Cell 16 implements qr_householder but has the sign edge-case bug. Must apply correction: `(np.sign(x[0]) + (x[0] == 0))`. |
| P1-05 | Restauración via QR (MGS y Householder) con truco de visualización (+1.0 y np.clip); imágenes restauradas mostradas | Cell 18 uses solve_triangular — must replace with manual back-substitution. Cells 19 visualization is correct. |
| P1-06 | Norma ‖Q̂ᵀQ̂ − I‖₂ calculada para MGS y Householder; comparación y conclusión sobre por qué Householder es el estándar industrial | Cell 20 computes norms correctly. Cell 21 analysis is correct — do not change. |
</phase_requirements>

---

## Summary

The notebook for Parte 1 is substantially complete. The implementation skeleton is correct in structure and mathematics. Three targeted changes are required before the phase is done: (1) replace `scipy.linalg.solve_triangular` in cell 18 with a manual back-substitution loop, (2) fix the sign edge-case in `qr_householder` (cell 16) so `x[0] == 0` maps to sign +1 rather than 0, and (3) expand the Markdown analysis cell for Inciso 2 (cell 11) to explicitly state the κ(AᵀA) = [κ(A)]² squaring relationship and to quantify how many decimal digits that consumes.

Everything else — matrix construction (cells 5–6), try-except normal equations (cells 9–10), qr_mgs (cell 14), visualization (cell 19), orthogonality norm (cell 20), and the Inciso 4 conclusion (cell 21) — is correct and must not be disturbed.

**Primary recommendation:** Make the three targeted edits (back-substitution, sign fix, analysis expansion) in the minimum number of cell modifications, leaving all correct code untouched.

---

## Standard Stack

### Core (already present in notebook)
| Library | Purpose | Status |
|---------|---------|--------|
| numpy | Matrix construction, norms, linalg.inv, linalg.cond | In use, correct |
| matplotlib | Image visualization, subplots | In use, correct |
| skimage | Image loading and resize (setup cells) | In use, correct |
| scipy.linalg.solve_triangular | Triangular solve — **ONLY in Parte 2** | Must be removed from Parte 1 cell 18 |

No new libraries need to be installed for this phase.

---

## Architecture Patterns

### Notebook Cell Map (Parte 1)

```
cell-0   Markdown — Integrantes (TODO: fill student codes)
cell-1   Markdown — Parte 1 header
cell-2   Markdown — Preparación header
cell-3   Code — Setup: image load, coordinate grid, damage, visualization
cell-4   Markdown — Inciso 1 theory
cell-5   Code — Build matrix A, print dimensions          [P1-01] CORRECT
cell-6   Code — Compute cond(AᵀA), print digit analysis   [P1-01] CORRECT
cell-7   Markdown — Inciso 1 analysis                     [P1-01] CORRECT
cell-8   Markdown — Inciso 2 header
cell-9   Code — try-except normal equations               [P1-02] CORRECT
cell-10  Code — Visualize normal-equations collapse        [P1-02] CORRECT
cell-11  Markdown — Inciso 2 analysis                     [P1-02] NEEDS EXPANSION
cell-12  Markdown — Inciso 3 header
cell-13  Markdown — MGS theory
cell-14  Code — qr_mgs(A)                                 [P1-03] CORRECT
cell-15  Markdown — Householder theory
cell-16  Code — qr_householder(A)                         [P1-04] NEEDS SIGN FIX
cell-17  Markdown — Inciso 4 header
cell-18  Code — Solve via QR (uses solve_triangular)       [P1-05] NEEDS BACK-SUB REPLACEMENT
cell-19  Code — 4-panel visualization                      [P1-05] CORRECT
cell-20  Code — Orthogonality norms                        [P1-06] CORRECT
cell-21  Markdown — Inciso 4 conclusion                    [P1-06] CORRECT — DO NOT CHANGE
```

### Pattern: Manual Back-Substitution

Back-substitution solves Rx = b where R is n×n upper triangular:

```python
def back_substitution(R, b):
    """Sustitución hacia atrás para sistema triangular superior Rx = b."""
    n = len(b)
    x = np.zeros(n)
    for i in range(n - 1, -1, -1):
        x[i] = (b[i] - R[i, i+1:] @ x[i+1:]) / R[i, i]
    return x
```

This is a pure numpy loop — no scipy dependency. Can be implemented as a helper function above cell 18, or inline. Per Claude's discretion, a named helper function is cleaner and more legible for a notebook being submitted for academic evaluation.

### Pattern: Sign Edge-Case Fix for Householder

Current (buggy) line in cell 16:
```python
v[0] += np.sign(x[0]) * np.linalg.norm(x)
```

Corrected line:
```python
v[0] += (np.sign(x[0]) + (x[0] == 0)) * np.linalg.norm(x)
```

**Why this works:** `np.sign(0)` returns `0.0` in NumPy. Adding `(x[0] == 0)` — which evaluates to `1` (int, auto-promoted to float) when True — ensures the sign is +1 when `x[0]` is exactly zero, making the reflector well-defined. The same fix applies to `householder_qr` in cell 32 (Parte 2), but that cell is out of scope for this phase.

### Pattern: Inciso 2 Analysis Expansion

The current cell 11 already mentions κ(AᵀA) = [κ(A)]² but does not quantify the digit loss. The expansion must add:

- Explicit statement: "Si κ(AᵀA) ≈ 10^30 en precisión doble (~16 dígitos disponibles), se pierden 30 dígitos — quedando literalmente cero dígitos significativos."
- Reference to the cell 6 output: the printed value of κ(AᵀA) should be cited as evidence.
- The relationship κ(AᵀA) = [κ(A)]² must be stated as a theorem (it already appears but can be made more prominent).

---

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Upper triangular solve | Custom Gaussian elimination | Simple back-substitution loop (5 lines) | The problem is already triangular — full elimination would be overkill |
| Matrix-vector products in back-sub | Manual nested loops | `R[i, i+1:] @ x[i+1:]` numpy dot | NumPy slice-dot is O(n) and numerically equivalent |
| Orthogonality verification | Custom norm | `np.linalg.norm(..., ord=2)` | Already used correctly in cell 20 |

**Key insight:** The back-substitution is the one component that must be written from scratch (per the locked decision). Everything else that exists in numpy/scipy can and should be used.

---

## Common Pitfalls

### Pitfall 1: Disturbing Correct Cells
**What goes wrong:** Editing cells 14, 19, 20, 21 while targeting cells 11, 16, 18 introduces regressions.
**Why it happens:** "While I'm here" impulse to clean up or refactor adjacent code.
**How to avoid:** The plan must enumerate exactly which cells change and which are read-only. Cells 14, 19, 20, 21 are explicitly frozen.
**Warning signs:** Any modification to qr_mgs, the visualization logic, the orthogonality norm computation, or the Inciso 4 Markdown conclusion.

### Pitfall 2: Incomplete Sign Fix (only fixing one function)
**What goes wrong:** Fixing `qr_householder` (cell 16) but forgetting `householder_qr` (cell 32).
**Why it happens:** The phase description focuses on Parte 1; Parte 2 cells feel out of scope.
**How to avoid:** Per CONTEXT.md, the sign fix applies to BOTH functions. The plan must explicitly mention cell 32 even though it is formally in Phase 3's territory. Apply the fix now since both functions live in the same notebook execution context.
**Warning signs:** If cell 32 still has the original `np.sign(x[0])` line after the phase is done.

### Pitfall 3: Back-Substitution Breaking for n=1 or Degenerate R
**What goes wrong:** The loop `range(n-1, -1, -1)` with `R[i, i+1:]` fails silently when `i = n-1` (empty slice is fine in NumPy — evaluates to 0.0).
**Why it happens:** Off-by-one anxiety leads to adding an unnecessary special case.
**How to avoid:** The standard loop is correct as-is. `R[n-1, n:]` returns an empty array, and `empty_array @ x[n:]` returns `0.0`. No special case needed.

### Pitfall 4: Analysis Expansion Over-Writing
**What goes wrong:** Rewriting cell 11 from scratch removes the existing correct content.
**Why it happens:** It feels easier to rewrite than to append.
**How to avoid:** The expansion is additive. The existing paragraph stays. Two new sentences are appended: the κ(AᵀA) = [κ(A)]² quantification and the digit-loss count.

### Pitfall 5: solve_triangular Left in Cell 18 Header Import
**What goes wrong:** The `from scipy.linalg import solve_triangular` import at the top of cell 18 is left even after replacing the calls.
**Why it happens:** The import is on line 1, the calls are later — easy to miss.
**How to avoid:** When replacing cell 18, remove the scipy import line from that cell. (The import will still exist in Parte 2 cells if needed there.)

---

## Code Examples

### Back-Substitution (canonical implementation)
```python
# Sustitución hacia atrás para resolver R @ c = rhs
# R: matriz triangular superior (n × n), rhs: vector (n,)
def back_substitution(R, b):
    """Sustitución hacia atrás para sistema triangular superior Rx = b."""
    n = len(b)
    x = np.zeros(n)
    for i in range(n - 1, -1, -1):
        x[i] = (b[i] - R[i, i+1:] @ x[i+1:]) / R[i, i]
    return x
```

Usage in cell 18:
```python
# ── MGS ─────────────────────────────────────────────────────────────────────
print('Factorizando A con MGS...')
Q_mgs, R_mgs = qr_mgs(A)
c_mgs = back_substitution(R_mgs, Q_mgs.T @ b_p1)
superficie_mgs = (A @ c_mgs).reshape(alto, ancho)
restaurada_mgs = np.clip(imagen_danada - superficie_mgs + 1.0, 0, 1)

# ── Householder ──────────────────────────────────────────────────────────────
print('Factorizando A con Householder...')
Q_hh, R_hh = qr_householder(A)
c_hh = back_substitution(R_hh, Q_hh.T @ b_p1)
superficie_hh = (A @ c_hh).reshape(alto, ancho)
restaurada_hh = np.clip(imagen_danada - superficie_hh + 1.0, 0, 1)

print('Listo.')
```

### Householder Sign Fix (cell 16, the one changed line)
```python
# Before (buggy when x[0] == 0):
v[0] += np.sign(x[0]) * np.linalg.norm(x)

# After (correct):
v[0] += (np.sign(x[0]) + (x[0] == 0)) * np.linalg.norm(x)
```

### Inciso 2 Analysis Expansion (text to append to cell 11)
The following Spanish paragraph must be appended to the existing Markdown in cell 11:

```markdown
La relación $\kappa(A^\top A) = [\kappa(A)]^2$ explica por qué el método es computacionalmente catastrófico incluso cuando funciona algebraicamente: elevar al cuadrado el número de condición duplica la cantidad de dígitos significativos consumidos. En precisión doble disponemos de aproximadamente $-\log_{10}(\varepsilon_\text{máq}) \approx 16$ dígitos. Si $\kappa(A^\top A) \approx 10^{30}$, se pierden 30 dígitos — es decir, la solución no tiene **ningún** dígito correcto. La impresión en la celda anterior lo confirma numéricamente.
```

---

## State of the Art

| Old Approach | Current Approach | Impact |
|--------------|------------------|--------|
| `scipy.linalg.solve_triangular` in Parte 1 | Manual back-substitution loop | Required by assignment; demonstrates the algorithm explicitly |
| `np.sign(x[0])` in Householder sign convention | `np.sign(x[0]) + (x[0] == 0)` | Correct behavior when first element is exactly zero |
| Inciso 2 analysis without digit quantification | Analysis with explicit κ²= digit-loss count | Required by academic rubric (P1-02 criteria) |

---

## Open Questions

1. **Does the sign edge-case actually trigger in practice for this matrix A?**
   - What we know: The edge case `x[0] == 0` occurs only when the first element of a Householder subvector is exactly zero, which is rare with floating-point monomials evaluated at non-degenerate grid points.
   - What's unclear: Whether the bug would cause visible degradation on this specific (16384×55) matrix.
   - Recommendation: Apply the fix unconditionally — it is mathematically correct and costs nothing. The CONTEXT.md decision is locked.

2. **Where to define `back_substitution` in the notebook?**
   - What we know: Claude's discretion determines whether it is a separate function or inline.
   - What's unclear: The grader's preference for code organization.
   - Recommendation: Define as a named helper function in a new code cell immediately before cell 18 (or at the top of cell 18 itself). A named function is more readable, matches the style of `qr_mgs` and `qr_householder`, and makes the academic intent clear.

---

## Sources

### Primary (HIGH confidence)
- Notebook cells 0–21 read directly — all findings about current implementation state are verified by direct inspection
- REQUIREMENTS.md P1-01 through P1-06 — acceptance criteria verified
- CONTEXT.md locked decisions — constraints verified

### Secondary (MEDIUM confidence)
- NumPy documentation behavior: `np.sign(0)` returns `0.0` — standard IEEE 754 behavior, consistent with NumPy docs
- Back-substitution algorithm: standard numerical methods textbook (Trefethen & Bau, "Numerical Linear Algebra") — algorithm is well-established

---

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH — all libraries already in use, no new dependencies
- Architecture (what to change vs not change): HIGH — verified by direct cell-by-cell inspection
- Back-substitution implementation: HIGH — standard algorithm, no ambiguity
- Sign fix: HIGH — locked decision with exact formula provided
- Analysis expansion: HIGH — exact text specified in CONTEXT.md decisions

**Research date:** 2026-04-28
**Valid until:** 2026-05-05 (submission deadline — no external dependencies)
