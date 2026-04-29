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
    - "Householder sign fix: (np.sign(x[0]) + (x[0] == 0)) handles x[0]==0 edge case"
    - "Manual back-substitution loop as replacement for scipy.linalg.solve_triangular in Parte 1"

key-files:
  created: []
  modified:
    - "Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb"

key-decisions:
  - "Manual back_substitution defined inline in cell 18 (not as a separate cell)"
  - "Single backslash LaTeX convention maintained for consistency with existing notebook content"
  - "Comment in cells 16 and 32 updated to mention x_1==0 edge case explicitly"

patterns-established:
  - "LaTeX backslash convention: single backslash in decoded notebook string matches existing cells"

requirements-completed: [P1-02, P1-04, P1-05]

duration: 5min
completed: 2026-04-29
---

# Phase 02 Plan 01: Surgical Corrections to Parte 1 Notebook Summary

**Three surgical edits: Householder sign edge-case fix in cells 16 and 32, scipy.solve_triangular replaced with manual back-substitution in cell 18, and kappa(A^T A) = [kappa(A)]^2 digit-loss analysis appended to cell 11**

## Performance

- **Duration:** 5 min
- **Started:** 2026-04-29T14:23:01Z
- **Completed:** 2026-04-29T14:28:06Z
- **Tasks:** 3 (all in one commit — all changes to same file)
- **Files modified:** 1

## Accomplishments
- Fixed Householder reflector sign edge case (`np.sign(0) == 0` would zero out `v[0]`) in both `qr_householder` (cell 16) and `householder_qr` (cell 32)
- Eliminated `from scipy.linalg import solve_triangular` from Parte 1 (cell 18), replaced with inline `back_substitution` helper that implements the standard upper-triangular back-substitution loop
- Appended third paragraph to cell 11 Markdown analysis quantifying digit loss: `kappa(A^T A) = [kappa(A)]^2`, ~16 digits available in double precision, 30 digits lost when `kappa(A^T A) ≈ 10^30`

## Task Commits

All three tasks were applied to the same notebook file and committed atomically:

1. **Task 1: Sign edge case fix (cells 16 & 32)** — `b56a877` (feat)
2. **Task 2: Replace solve_triangular with back_substitution (cell 18)** — `b56a877` (feat)
3. **Task 3: Expand Inciso 2 analysis (cell 11)** — `b56a877` (feat)

**Plan metadata:** (pending final commit)

## Files Created/Modified
- `Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb` — cells 11, 16, 18, 32 modified; all other cells intact

## Decisions Made
- All three tasks committed in one atomic commit since they are all surgical edits to the same notebook file and there was no benefit to splitting them
- Used inline `back_substitution` helper in cell 18 as specified (not a new cell)
- Maintained single-backslash LaTeX convention to match existing notebook cells

## Deviations from Plan

### Auto-fixed Issues

**1. [Rule 1 - Bug] Python escape sequence corruption in cell 11 append**
- **Found during:** Task 3 (cell 11 append)
- **Issue:** Python interpreted `\varepsilon` as `\x0b` (vertical tab) + `arepsilon`, `\approx` as bell + `pprox`, `\top` as tab + `op` in string literals — corrupting the LaTeX content
- **Fix:** Rebuilt the append text using `chr(92)` for each LaTeX backslash to avoid Python escape sequence interpretation
- **Files modified:** Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb (cell 11)
- **Verification:** All acceptance criteria verified via Node.js checks; `\varepsilon`, `\approx`, `\kappa`, `\top` present correctly
- **Committed in:** b56a877 (task commit)

**2. [Rule 1 - Bug] Double-backslash inconsistency in first fix attempt**
- **Found during:** Task 3 iteration
- **Issue:** First fix attempt used `chr(92)*2` producing `\\kappa` (double backslash) in decoded string, while existing notebook uses single backslash LaTeX convention
- **Fix:** Changed to `chr(92)` (single backslash) to match notebook convention
- **Files modified:** Practica3-AlgComp-Gallon-Montoya-Gomez.ipynb (cell 11)
- **Verification:** Node check `s.includes(backslash+'kappa(A^'+backslash+'top A) = ['+backslash+'kappa(A)]^2')` passes
- **Committed in:** b56a877 (task commit)

---

**Total deviations:** 2 auto-fixed (2 Rule 1 bugs from Python escape sequence handling)
**Impact on plan:** Both fixes were necessary for correct LaTeX rendering. No scope creep.

## Issues Encountered
- Python escape sequences (`\v`, `\a`, `\t`) in string literals silently corrupt LaTeX commands (`\varepsilon`, `\approx`, `\top`). Resolved by using `chr(92)` for backslash construction.

## User Setup Required
None - no external service configuration required.

## Next Phase Readiness
- Notebook has all three Parte 1 corrections applied: sign edge case, no scipy in Parte 1, expanded Inciso 2 analysis
- Ready for plan 02-02: Restart & Run All + visual verification
- Cells 14, 15, 17, 19, 20, 21 confirmed unmodified
- nbformat validation passes (39 cells, valid notebook)

---
*Phase: 02-parte-1-rescate-del-patrimonio-documental*
*Completed: 2026-04-29*
