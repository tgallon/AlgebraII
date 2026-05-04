# Fase 2: Parte 1 — Rescate del Patrimonio Documental - Investigación

**Investigado:** 2026-04-28
**Dominio:** Álgebra lineal numérica — factorización QR, sustitución hacia atrás, números de condición
**Confianza:** ALTA

---

<user_constraints>
## Lo que ya está decidido (de CONTEXT.md)

### Decisiones bloqueadas

#### solve_triangular en Parte 1
- **NO** usar `scipy.linalg.solve_triangular` en Parte 1
- Implementar la sustitución hacia atrás manualmente para resolver Rĥc = Qĥᵀb
- Parte 2 puede conservar `scipy.linalg.solve_triangular` (el enunciado lo permite explícitamente allí)

#### Corrección del edge case en Householder (convención del signo)
- Cuando `x[0] == 0`, `np.sign(0) = 0` deja `v[0] = 0`, rompiendo el reflector
- Corrección: `np.sign(x[0]) + (x[0] == 0)` en lugar de `np.sign(x[0])` puro
- Esta corrección aplica a **las dos** funciones: `qr_householder` (Parte 1) y `householder_qr` (Parte 2)
- Fórmula corregida: `v[0] += (np.sign(x[0]) + (x[0] == 0)) * np.linalg.norm(x)`

#### Análisis Markdown — Inciso 2 (Ecuaciones Normales)
- Ampliar la celda del inciso 2 para incluir:
  - La relación κ(AᵀA) = [κ(A)]² (el cuadrado del número de condición)
  - Cuántos dígitos se pierden: si κ(AᵀA) ~ 10^30 en precisión doble (~16 dígitos), queda 0 dígitos significativos
- El análisis del inciso 4 (conclusión Householder) está bien — no cambiar

#### Análisis Markdown — Inciso 4 (Conclusión)
- Dejar el análisis actual — explica correctamente por qué Householder es el estándar industrial

#### Códigos de estudiante
- La celda de integrantes tiene `*(código)*` como placeholders
- El plan incluye un TODO explícito: los tres (Tomás Gallón, Sebastian Montoya, Miguel Gomez) deben agregar sus códigos antes de la entrega

### A criterio del agente
- Formato de la back-substitution manual (función separada o inline)
- Nombre y estilo de la función si se crea por separado

### Ideas diferidas (FUERA DE ALCANCE)
Ninguna — la discusión se mantuvo dentro del alcance de la fase.
</user_constraints>

---

<phase_requirements>
## Requisitos de la fase

| ID | Descripción | Estado de investigación |
|----|-------------|------------------------|
| P1-01 | Matriz de diseño A con monomios x^j y^k con j+k ≤ 9 (d=9); dimensiones impresas; número de condición de AᵀA calculado e interpretado | Celda 5 construye A correctamente (m=16384, n=55). Celda 6 calcula cond(AᵀA). El análisis de celda 7 necesita la mención de κ(AᵀA)=[κ(A)]² y la cuantificación de pérdida de dígitos. |
| P1-02 | Ecuaciones normales con np.linalg.inv en try-except; imagen mostrada; explicación del colapso | Celdas 9–11 ya implementan esto. La celda 11 necesita ampliar κ(AᵀA)=[κ(A)]² con cuenta explícita de dígitos. |
| P1-03 | `qr_mgs(A)` desde cero con comentarios sobre el proyector ortogonal de Gram-Schmidt Modificado | Celda 14 implementa qr_mgs correctamente. No hay nada que cambiar. |
| P1-04 | `qr_householder(A)` desde cero con comentarios sobre v = sign(x₁)‖x‖e₁ + x | Celda 16 implementa qr_householder pero tiene el bug del signo. Hay que aplicar: `(np.sign(x[0]) + (x[0] == 0))`. |
| P1-05 | Restauración vía QR (MGS y Householder) con truco (+1.0 y np.clip); imágenes mostradas | Celda 18 usa solve_triangular — hay que reemplazarlo con back-substitution manual. La visualización de celda 19 está bien. |
| P1-06 | ‖Q̂ᵀQ̂ − I‖₂ calculada para MGS y Householder; comparación y conclusión sobre Householder | Celda 20 calcula las normas correctamente. El análisis de celda 21 está bien — no tocar. |
</phase_requirements>

---

## Resumen

El notebook de Parte 1 está básicamente completo. La estructura y la matemática son correctas. Hacen falta tres cambios puntuales antes de cerrar la fase: (1) reemplazar `scipy.linalg.solve_triangular` en celda 18 con un bucle de sustitución hacia atrás manual, (2) arreglar el edge case del signo en `qr_householder` (celda 16) para que `x[0] == 0` dé signo +1 en lugar de 0, y (3) ampliar el análisis Markdown del Inciso 2 (celda 11) con la relación κ(AᵀA) = [κ(A)]² y cuantificar cuántos dígitos eso consume.

Todo lo demás — construcción de la matriz (celdas 5–6), ecuaciones normales con try-except (celdas 9–10), qr_mgs (celda 14), visualización (celda 19), norma de ortogonalidad (celda 20) y la conclusión del Inciso 4 (celda 21) — está correcto y no se toca.

**Recomendación:** Hacer las tres ediciones puntuales (back-substitution, fix del signo, expansión del análisis) con el mínimo de cambios posibles, dejando todo lo que ya funciona intacto.

---

## Stack estándar

### Lo que ya está en el notebook
| Librería | Para qué | Estado |
|----------|---------|--------|
| numpy | Construcción de matrices, normas, linalg.inv, linalg.cond | En uso, correcto |
| matplotlib | Visualización de imágenes, subplots | En uso, correcto |
| skimage | Carga y redimensionado de imágenes (celdas de setup) | En uso, correcto |
| scipy.linalg.solve_triangular | Resolución triangular — **SOLO en Parte 2** | Hay que eliminarlo de celda 18 en Parte 1 |

No hay que instalar librerías nuevas para esta fase.

---

## Patrones de arquitectura

### Mapa de celdas del notebook (Parte 1)

```
celda-0   Markdown — Integrantes (TODO: llenar códigos de estudiante)
celda-1   Markdown — Encabezado Parte 1
celda-2   Markdown — Encabezado Preparación
celda-3   Código — Setup: carga de imagen, grilla de coordenadas, daño, visualización
celda-4   Markdown — Teoría Inciso 1
celda-5   Código — Construir matriz A, imprimir dimensiones          [P1-01] CORRECTO
celda-6   Código — Calcular cond(AᵀA), imprimir análisis de dígitos  [P1-01] CORRECTO
celda-7   Markdown — Análisis Inciso 1                               [P1-01] CORRECTO
celda-8   Markdown — Encabezado Inciso 2
celda-9   Código — try-except ecuaciones normales                    [P1-02] CORRECTO
celda-10  Código — Visualizar colapso de ecuaciones normales          [P1-02] CORRECTO
celda-11  Markdown — Análisis Inciso 2                               [P1-02] NECESITA EXPANSIÓN
celda-12  Markdown — Encabezado Inciso 3
celda-13  Markdown — Teoría MGS
celda-14  Código — qr_mgs(A)                                         [P1-03] CORRECTO
celda-15  Markdown — Teoría Householder
celda-16  Código — qr_householder(A)                                 [P1-04] NECESITA ARREGLO DEL SIGNO
celda-17  Markdown — Encabezado Inciso 4
celda-18  Código — Resolver vía QR (usa solve_triangular)             [P1-05] NECESITA REEMPLAZO CON BACK-SUB
celda-19  Código — Visualización 4 paneles                            [P1-05] CORRECTO
celda-20  Código — Normas de ortogonalidad                            [P1-06] CORRECTO
celda-21  Markdown — Conclusión Inciso 4                              [P1-06] CORRECTO — NO TOCAR
```

### Patrón: Sustitución hacia atrás manual

La back-substitution resuelve Rx = b donde R es n×n triangular superior:

```python
def back_substitution(R, b):
    """Sustitución hacia atrás para sistema triangular superior Rx = b."""
    n = len(b)
    x = np.zeros(n)
    for i in range(n - 1, -1, -1):
        x[i] = (b[i] - R[i, i+1:] @ x[i+1:]) / R[i, i]
    return x
```

Es un bucle numpy puro, sin dependencia de scipy. Puede ir como función auxiliar antes de celda 18 o inline. Para un notebook académico, lo más limpio es una función con nombre propio.

### Patrón: Corrección del edge case del signo en Householder

Línea actual (con bug) en celda 16:
```python
v[0] += np.sign(x[0]) * np.linalg.norm(x)
```

Línea corregida:
```python
v[0] += (np.sign(x[0]) + (x[0] == 0)) * np.linalg.norm(x)
```

**Por qué funciona:** `np.sign(0)` devuelve `0.0` en NumPy. Sumar `(x[0] == 0)` — que vale `1` cuando es True — garantiza signo +1 cuando `x[0]` es exactamente cero, haciendo el reflector bien definido. El mismo arreglo va en `householder_qr` en celda 32 (Parte 2), aunque sea de otra fase.

### Patrón: Expansión del análisis del Inciso 2

La celda 11 actual ya menciona κ(AᵀA) = [κ(A)]² pero no cuantifica la pérdida de dígitos. Hay que añadir:

- Declaración explícita: "Si κ(AᵀA) ≈ 10^30 en precisión doble (~16 dígitos disponibles), se pierden 30 dígitos — queda literalmente cero dígitos significativos."
- Referencia al output de celda 6: el valor impreso de κ(AᵀA) como evidencia numérica.
- La relación κ(AᵀA) = [κ(A)]² como teorema (ya aparece pero puede destacarse más).

---

## Lo que NO hay que reinventar

| Problema | No construir | Usar esto | Por qué |
|---------|-------------|-----------|---------|
| Resolver triangular superior | Eliminación Gaussiana propia | Bucle de back-substitution (5 líneas) | El sistema ya es triangular — la eliminación completa sería un exceso |
| Productos matriz-vector en back-sub | Bucles anidados manuales | `R[i, i+1:] @ x[i+1:]` con numpy | El slice-dot de NumPy es O(n) y numéricamente equivalente |
| Verificación de ortogonalidad | Norma propia | `np.linalg.norm(..., ord=2)` | Ya se usa correctamente en celda 20 |

**Punto clave:** La back-substitution es lo único que hay que implementar desde cero (así lo decidimos). Todo lo demás que ya existe en numpy/scipy puede y debe usarse.

---

## Errores comunes a evitar

### Error 1: Tocar celdas que ya están bien
**Qué sale mal:** Editar celdas 14, 19, 20, 21 mientras se apunta a celdas 11, 16, 18 introduce regresiones.
**Por qué pasa:** El impulso de "ya que estoy aquí" para limpiar código adyacente.
**Cómo evitarlo:** El plan enumera exactamente qué celdas cambian y cuáles son de solo lectura. Las celdas 14, 19, 20, 21 están explícitamente congeladas.
**Señal de alerta:** Cualquier modificación a qr_mgs, la lógica de visualización, el cálculo de la norma de ortogonalidad, o la conclusión Markdown del Inciso 4.

### Error 2: Arreglar solo una de las dos funciones Householder
**Qué sale mal:** Arreglar `qr_householder` (celda 16) y olvidar `householder_qr` (celda 32).
**Por qué pasa:** La fase se enfoca en Parte 1; las celdas de Parte 2 se sienten fuera de alcance.
**Cómo evitarlo:** Según CONTEXT.md, el arreglo del signo aplica a LAS DOS funciones. El plan menciona celda 32 explícitamente aunque sea territorio de Fase 3.
**Señal de alerta:** Si celda 32 todavía tiene la línea original `np.sign(x[0])` al terminar la fase.

### Error 3: Back-substitution que falla para n=1 o R degenerada
**Qué sale mal:** El bucle `range(n-1, -1, -1)` con `R[i, i+1:]` cuando `i = n-1` da slice vacío — en NumPy eso evalúa a 0.0, lo cual está bien.
**Por qué pasa:** Ansiedad de off-by-one que lleva a agregar un caso especial innecesario.
**Cómo evitarlo:** El bucle estándar está bien como está. No hace falta caso especial.

### Error 4: Reescribir celda 11 desde cero y perder el contenido original
**Qué sale mal:** Reescribir celda 11 completamente borra los párrafos correctos.
**Por qué pasa:** Parece más fácil reescribir que añadir.
**Cómo evitarlo:** La expansión es aditiva. Los párrafos existentes se quedan. Solo se añaden dos oraciones nuevas al final.

### Error 5: Dejar el import de solve_triangular en celda 18
**Qué sale mal:** El `from scipy.linalg import solve_triangular` en la primera línea de celda 18 se queda aunque se reemplacen las llamadas.
**Por qué pasa:** El import está en la línea 1, las llamadas están más abajo — fácil de pasar por alto.
**Cómo evitarlo:** Al reemplazar celda 18, eliminar también esa línea de import.

---

## Ejemplos de código

### Back-substitution (implementación canónica)
```python
# Sustitución hacia atrás para resolver R @ c = rhs
# R: matriz triangular superior (n × n), rhs: vector (n,)
def back_substitution(R, b):
    """Sustitución hacia atrás para sistema triangular superior Rx = b."""
    n = len(b)
    x = np.zeros(n)
    for i in range(n - 1, -1, -1):
        x[i] = (b[i] - R[i, i + 1:] @ x[i + 1:]) / R[i, i]
    return x
```

Uso en celda 18:
```python
# ── MGS ─────────────────────────────────────────────────────────────────────
print('Factorizando A con MGS...')
Q_mgs, R_mgs = qr_mgs(A)
# Resolver R_hat * c = Q_hat^T * b mediante sustitución hacia atrás manual
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

### Arreglo del signo en Householder (celda 16, la línea que cambia)
```python
# Antes (bug cuando x[0] == 0):
v[0] += np.sign(x[0]) * np.linalg.norm(x)

# Después (correcto):
v[0] += (np.sign(x[0]) + (x[0] == 0)) * np.linalg.norm(x)
```

### Expansión del análisis del Inciso 2 (texto para añadir al final de celda 11)

```markdown

La relación $\kappa(A^\top A) = [\kappa(A)]^2$ explica por qué el método es computacionalmente catastrófico incluso cuando funciona algebraicamente: elevar al cuadrado el número de condición duplica la cantidad de dígitos significativos consumidos. En precisión doble disponemos de aproximadamente $-\log_{10}(\varepsilon_\text{máq}) \approx 16$ dígitos. Si $\kappa(A^\top A) \approx 10^{30}$, se pierden 30 dígitos — es decir, la solución no tiene **ningún** dígito correcto. La impresión en la celda anterior lo confirma numéricamente.
```

---

## Estado del arte

| Antes | Ahora | Impacto |
|-------|-------|---------|
| `scipy.linalg.solve_triangular` en Parte 1 | Bucle de back-substitution manual | Requerido por el enunciado; demuestra el algoritmo explícitamente |
| `np.sign(x[0])` en la convención del signo de Householder | `np.sign(x[0]) + (x[0] == 0)` | Comportamiento correcto cuando el primer elemento es exactamente cero |
| Análisis del Inciso 2 sin cuantificar dígitos | Análisis con κ²= pérdida de dígitos explícita | Requerido por la rúbrica académica (criterios P1-02) |

---

## Preguntas abiertas

1. **¿El edge case del signo se dispara en práctica para esta matriz A?**
   - Lo que sabemos: El caso `x[0] == 0` solo ocurre cuando el primer elemento de un subvector de Householder es exactamente cero, lo cual es raro con monomios de punto flotante en una grilla no degenerada.
   - Lo que no está claro: Si el bug causaría degradación visible en esta matriz específica (16384×55).
   - Recomendación: Aplicar el arreglo de todas formas — es matemáticamente correcto y no cuesta nada. La decisión en CONTEXT.md está bloqueada.

2. **¿Dónde definir `back_substitution` en el notebook?**
   - Lo que sabemos: El agente decide si va como función separada o inline.
   - Lo que no está claro: La preferencia del evaluador sobre organización del código.
   - Recomendación: Definir como función auxiliar con nombre propio justo antes de celda 18 (o al principio de celda 18). Una función con nombre queda más legible y coincide con el estilo de `qr_mgs` y `qr_householder`.

---

## Fuentes

### Primarias (confianza ALTA)
- Celdas 0–21 del notebook leídas directamente — todos los hallazgos sobre el estado actual están verificados por inspección directa
- REQUIREMENTS.md P1-01 a P1-06 — criterios de aceptación verificados
- CONTEXT.md decisiones bloqueadas — restricciones verificadas

### Secundarias (confianza MEDIA)
- Comportamiento de NumPy: `np.sign(0)` retorna `0.0` — comportamiento estándar IEEE 754, consistente con la documentación de NumPy
- Algoritmo de back-substitution: método numérico estándar (Trefethen & Bau, "Numerical Linear Algebra") — el algoritmo está bien establecido

---

## Metadatos

**Desglose de confianza:**
- Stack estándar: ALTA — todas las librerías ya están en uso, sin dependencias nuevas
- Arquitectura (qué cambiar y qué no): ALTA — verificada por inspección celda a celda
- Implementación de back-substitution: ALTA — algoritmo estándar, sin ambigüedad
- Arreglo del signo: ALTA — decisión bloqueada con fórmula exacta
- Expansión del análisis: ALTA — texto exacto especificado en CONTEXT.md

**Fecha de investigación:** 2026-04-28
**Válido hasta:** 2026-05-05 (deadline de entrega — sin dependencias externas)
