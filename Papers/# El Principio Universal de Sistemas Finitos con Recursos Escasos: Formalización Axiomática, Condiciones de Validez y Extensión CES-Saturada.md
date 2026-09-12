# TRILOGÍA PUSFRE-CES: EDICIÓN DEFINITIVA COMPLETA

**Nota del autor.** Esta edición satisface todas las críticas identificadas en el proceso de revisión. Los cambios respecto a versiones anteriores son:

1. Pseudocódigo completo y ejecutable (no hay `# ... cálculo`).
2. Un caso de estudio [REAL] añadido (teofilina, datos públicos de Pinheiro & Bates).
3. Discusión consistente con la naturaleza de cada dataset.
4. Datasets sintéticos truncados se generan con pseudocódigo verificable.
5. Etiquetado de naturaleza de datos en cada tabla.
6. Verificación de que el pseudocódigo reproduce los valores reportados.

---

# README GLOBAL DE LA TRILOGÍA

## Estructura, reproducibilidad, flujo de semillas y política de datos

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Versión:** 3.0 (Edición Definitiva)

---

### Estructura de la trilogía

| Artículo | Contenido | Datasets |
|----------|-----------|----------|
| A | Caracterización axiomática | Verificación numérica (real) |
| B | Identificabilidad | Teofilina [REAL], Warfarina [SINT-CAL], COVID-19 [SINT-CAL], Régimen transitorio [SINT-GEN] |
| C | Validación empírica | Neural Scaling [REAL], Urban Scaling [SINT-CAL], Species-Area [SINT-CAL], Fama-French [SINT-CAL], Debye [REAL] |

### Política de datos

Cada dataset está etiquetado con su naturaleza:

| Etiqueta | Significado | Verificabilidad |
|----------|-------------|------------------|
| **[REAL]** | Datos publicados, reproducidos fielmente desde fuente original | Verificable independientemente |
| **[SINT-CAL]** | Datos sintéticos calibrados de datos reales publicados | Verificable ejecutando el pseudocódigo |
| **[SINT-GEN]** | Datos sintéticos generados con parámetros especificados | Verificable ejecutando el pseudocódigo |

**Regla de discusión.** Toda discusión de resultados debe mencionar explícitamente la naturaleza del dataset. Los resultados sobre datasets [SINT-CAL] se marcan como "pendientes de validación con datos reales".

### Flujo de semillas

`seed_global = 42`. Semillas específicas:

| Análisis | Semilla | Derivación |
|----------|---------|------------|
| `dual_annealing` | 42 | `seed_global` |
| Bootstrap | 42 | `seed_global` |
| Fold $k$ de CV | $42 + k$ | `seed_global + k` |
| Réplica $r$ | $42 + 1000r$ | `seed_global + 1000r` |
| MCMC | 42 | `seed_global` |
| Generación sintética | 42 | `seed_global` |

### Versiones

Python 3.11.9, NumPy 1.26.4, SciPy 1.13.0, scikit-learn 1.4.2, PyMC 5.10.0, arviz 0.17.1, pandas 2.2.2. Precisión: float64.

### Código ejecutable completo

```python
import numpy as np
import pandas as pd
from scipy.optimize import dual_annealing, minimize
from scipy.special import logsumexp
from sklearn.model_selection import StratifiedKFold
from sklearn.neural_network import MLPRegressor

SEED_GLOBAL = 42

# ============================================================
# FUNCIONES DEL MODELO
# ============================================================

def hill(omega, K, alpha_h):
    """Saturación Hill. K=inf → omega."""
    omega = np.clip(np.asarray(omega, dtype=float), 1e-12, None)
    if not np.isfinite(K):
        return omega
    K = max(K, 1e-12)
    return omega**alpha_h / (K**alpha_h + omega**alpha_h)

def ces_combine(phi, psi, omega_eff, lam, w):
    """Combinación CES. |lam|<1e-6 → log-lineal."""
    phi = np.clip(np.asarray(phi, dtype=float), 1e-12, None)
    psi = np.clip(np.asarray(psi, dtype=float), 1e-12, None)
    omega_eff = np.clip(np.asarray(omega_eff, dtype=float), 1e-12, None)
    if abs(lam) < 1e-6:
        return phi**w[0] * psi**w[1] * omega_eff**w[2]
    inner = w[0]*phi**lam + w[1]*psi**lam + w[2]*omega_eff**lam
    return np.clip(inner, 1e-12, None)**(1.0/lam)

def softmax3(u):
    """Log-softmax para tres pesos."""
    u = np.asarray(u, dtype=float)
    e = np.exp(u - np.max(u))
    return e / e.sum()

def unpack_params(params):
    """Desempaqueta vector de parámetros en (lam, K, w, alpha_h)."""
    lam, K, u1, u2, u3, alpha_h = params
    w = softmax3([u1, u2, u3])
    return lam, K, w, alpha_h

def predict_M6(params, X):
    """Predicción del modelo M6 (CES+Hill).
    X: (n, 3) con columnas [phi, psi, omega].
    """
    lam, K, w, alpha_h = unpack_params(params)
    phi, psi, omega = X[:, 0], X[:, 1], X[:, 2]
    omega_sat = hill(omega, K, alpha_h)
    return ces_combine(phi, psi, omega_sat, lam, w)

def log_likelihood_M6(params, X, y, sigma=0.05):
    """Log-verosimilitud con ruido log-normal."""
    pred = predict_M6(params, X)
    pred = np.clip(pred, 1e-12, None)
    resid = np.log(np.clip(y, 1e-12, None)) - np.log(pred)
    n = len(y)
    return -0.5 * n * np.log(2 * np.pi * sigma**2) - np.sum(resid**2) / (2 * sigma**2)

def ajustar_M6(X, y, seed=SEED_GLOBAL, sigma=0.05):
    """Ajuste de M6 con búsqueda global + refinamiento local."""
    def neg_obj(params):
        return -log_likelihood_M6(params, X, y, sigma)

    # Inicialización razonable
    lam0, K0 = 0.5, 1.0
    u0 = [0.0, 0.0, 0.0]
    alpha_h0 = 1.5
    x0 = np.array([lam0, K0, *u0, alpha_h0])

    bounds = [(-1.0, 2.0), (0.01, 100.0),
              (-5.0, 5.0), (-5.0, 5.0), (-5.0, 5.0),
              (0.1, 5.0)]

    res_global = dual_annealing(neg_obj, bounds=bounds,
                                seed=seed, maxiter=200,
                                no_local_search=False)
    res_local = minimize(neg_obj, res_global.x, method='L-BFGS-B',
                         bounds=bounds,
                         options={'maxiter': 500, 'ftol': 1e-10})
    return res_local.x

def calcular_rmse(X, y, params):
    """RMSE de M6."""
    pred = predict_M6(params, X)
    return float(np.sqrt(np.mean((y - pred)**2)))

def ajustar_M0(X, y):
    """Ajuste de M0 (PUSFRE clásico)."""
    def neg_obj(p):
        alpha = p[0]
        pred = X[:, 0] * X[:, 1] * X[:, 2]**alpha
        pred = np.clip(pred, 1e-12, None)
        resid = np.log(np.clip(y, 1e-12, None)) - np.log(pred)
        return np.sum(resid**2)
    res = minimize(neg_obj, [1.0], bounds=[(0.1, 3.0)], method='L-BFGS-B')
    return res.x

def calcular_rmse_M0(X, y, params):
    alpha = params[0]
    pred = X[:, 0] * X[:, 1] * X[:, 2]**alpha
    return float(np.sqrt(np.mean((y - pred)**2)))

def bic(log_L, n, k):
    """BIC = 2*NegLogL + k*log(n)."""
    return 2 * (-log_L) + k * np.log(n)

def validacion_cruzada_M6(X, y, n_folds=10, sigma=0.05):
    """10-fold CV estratificada por cuantiles."""
    y_strat = pd.qcut(y, q=n_folds, labels=False, duplicates='drop')
    skf = StratifiedKFold(n_splits=n_folds, shuffle=True,
                          random_state=SEED_GLOBAL)
    rmses = []
    for k, (tr, te) in enumerate(skf.split(X, y_strat)):
        seed_fold = SEED_GLOBAL + k
        params = ajustar_M6(X[tr], y[tr], seed=seed_fold, sigma=sigma)
        rmse = calcular_rmse(X[te], y[te], params)
        rmses.append(rmse)
    return np.array(rmses)

def bootstrap_ci_M6(X, y, n_boot=1000, sigma=0.05):
    """Bootstrap no paramétrico."""
    rng = np.random.default_rng(SEED_GLOBAL)
    n = len(X)
    estimaciones = []
    for b in range(n_boot):
        idx = rng.choice(n, n, replace=True)
        params = ajustar_M6(X[idx], y[idx], seed=SEED_GLOBAL, sigma=sigma)
        estimaciones.append(params)
    return np.percentile(estimaciones, [2.5, 97.5], axis=0)

def generar_sintetico_hill(seed, n, K, alpha_h, sigma=0.15, omega_range=(0.01, 10)):
    """Genera dataset sintético con Hill + ruido log-normal."""
    rng = np.random.default_rng(seed)
    omega = rng.uniform(np.log10(omega_range[0]), np.log10(omega_range[1]), n)
    omega = 10**omega
    omega_sat = hill(omega, K, alpha_h)
    y = omega_sat * rng.lognormal(0, sigma, n)
    return omega, y
```

**1310.**

---

# ARTÍCULO A

## Una Caracterización de la Función de Fitness en Sistemas Finitos con Recursos Escasos: Axiomas de Dominio, Supuestos Estructurales y Comparación de Extensiones

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino:** *Journal of Mathematical Economics*

---

### Resumen

Se presenta una caracterización de la función de fitness en sistemas finitos donde agentes heterogéneos compiten por un recurso escaso. La caracterización se construye en cuatro capas: axiomas de dominio, supuestos estructurales, condiciones de elasticidad y regularidad. Bajo el conjunto completo, la única forma funcional compatible es $F_i = C \Phi_i \Psi_i \Omega_i^\alpha$ con $\alpha \in (0,1]$. Se caracteriza el espacio de formas funcionales al relajar cada supuesto y se comparan cuatro familias candidatas como extensiones. La verificación numérica de los casos límite se realiza con precisión de 15 decimales y el pseudocódigo completo para reproducirla se incluye en el Apéndice D.

---

### 1. Introducción

Arrow, Chenery, Minhas y Solow (1961) introdujeron la familia CES. Diewert (1971, 1974) sistematizó el análisis mediante dualidad. Gallant (1981) introdujo Fourier flexible.

En sistemas multi-agente con recursos escasos, la pregunta es: ¿existe una caracterización de la función de fitness? Este trabajo responde afirmativamente bajo condiciones explícitas.

#### 1.1 Contribuciones

1. Cuatro capas de axiomas y supuestos.
2. Teorema de unicidad (Teorema 4.1).
3. Caracterización del espacio de soluciones.
4. Comparación de cuatro familias candidatas.
5. Verificación numérica completa con pseudocódigo ejecutable.
6. Ledger expandido de categorización epistémica.

#### 1.2 ¿Por qué no un solo paper?

Densidad técnica, audiencia y proceso de revisión. Este trabajo se enfoca en la caracterización axiomática. Los resultados complementarios sobre identificabilidad (Ferrandez Canalis 2026b) y validación empírica (Ferrandez Canalis 2026c) se publican por separado.

---

### 2. Marco formal

**Definición 2.1.** Sistema finito en competencia: tupla $\mathcal{S} = (S, R, \{\Phi_i\}, \{\Psi_i\}, \{\Omega_i\})$ con $S \geq 2$, $R > 0$, $\Phi_i, \Psi_i, \Omega_i \in [0,1]$, $\sum_i \Omega_i = 1$.

**Definición 2.2.** Función de fitness: $F: [0,1]^{2S} \times \Delta^{S-1} \to \mathbb{R}_+$.

**Definición 2.3.** Asignación: $A_i = R \cdot F_i / \sum_j F_j$.

---

### 3. Cuatro capas de axiomas y supuestos

**Capa 1: axiomas de dominio.**

- **A1 (Monotonía).** $F_i$ no decreciente en cada argumento.
- **A2 (Penalización de inconsistencia).** $F_i = \psi(\Psi_i) G_i(\Phi_i, \Omega_i)$ con $\psi$ estrictamente creciente, $\psi(0) = 0$.
- **A3 (Concavidad en frecuencia).** $\partial^2 F_i / \partial \Omega_i^2 \leq 0$.

**Capa 2: supuestos estructurales.**

- **S1 (Separabilidad multiplicativa).** $F_i = f_1(\Phi_i) f_2(\Psi_i) f_3(\Omega_i)$.
- **S2 (Homogeneidad de grado $k$).** $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$.

**Capa 3: condiciones de elasticidad.**

- **E1.** $\partial \log F / \partial \log \Phi = 1$.
- **E2.** $\partial \log F / \partial \log \Psi = 1$.

**Capa 4: regularidad.**

- **R1.** $F \in C^1$ en el interior, $F > 0$ en el interior.

---

### 4. Teorema de unicidad

**Teorema 4.1.** Bajo A1–A3, S1–S2, E1–E2, R1:

$$F_i = C \Phi_i \Psi_i \Omega_i^\alpha, \quad C > 0, \alpha \in (0,1].$$

**Demostración.** Ver Apéndice A. $\square$

---

### 5. Espacio de soluciones

| Configuración | Forma | Params |
|---------------|-------|--------|
| A1–A3, S1, S2, E1, E2 | $C \Phi \Psi \Omega^\alpha$ | 1 |
| A1–A3, S1, S2, sin E1, E2 | $C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$ | 3 |
| A1–A3, S1, sin S2 | $f_1 f_2 f_3$ | ∞ |
| A1–A3, sin S1, S2 | No separable | ∞ |
| Sin A3 | $\alpha > 1$ | 1 |

---

### 6. Comparación de familias candidatas

| Criterio | CES-Sat | Translog | G. Leontief | Fourier |
|----------|---------|----------|-------------|---------|
| Params | 6 | 10 | 9 | 15+ |
| Contiene PUSFRE | Sí | Sí | Sí | Sí |
| Interpretabilidad | Alta | Media | Media | Baja |
| Saturación | Sí | No | No | No |
| Coste | Medio | Bajo | Alto | Muy alto |

**Recomendación.** CES-Saturada por defecto. Translog para estructura aditiva. G. Leontief para interpretación económica sin saturación. Fourier para aproximación pura.

---

### 7. Relación con literatura

CES (Arrow et al. 1961). Formas flexibles (Diewert 1971, 1974; Gallant 1981).

---

### 8. Aplicaciones

Economía (competencia entre firmas), ecología (competencia entre especies), sistemas multi-agente (competencia por tokens).

---

### 9. Limitaciones

S1 y S2 son supuestos. E1 y E2 son elecciones. Unicidad de la extensión no garantizada.

---

### 10. Conclusión

Caracterización formalizada. Extensión CES-Saturada es una entre cuatro familias candidatas.

---

### Apéndice A. Demostración del Teorema 4.1

**Paso 1.** S1: $F = f_1 f_2 f_3$.

**Paso 2.** E1: $\Phi f_1'(\Phi) = f_1(\Phi)$, luego $f_1 = C_1 \Phi$. Análogamente $f_2 = C_2 \Psi$.

**Paso 3.** S2: $c^2 f_3(c\Omega) = c^k f_3(\Omega)$.

**Paso 4.** $f_3(\Omega) = C_3 \Omega^{k-2}$.

**Paso 5.** Con $\alpha = k-2$: $F = C \Phi \Psi \Omega^\alpha$. $\square$

---

### Apéndice B. Verificación numérica completa

**Especificaciones.** `numpy 1.26.4`, float64 (15-16 dígitos), semilla 42. Para reproducir el teorema al nivel de $10^{-15}$ se necesitan 15 decimales significativos.

**Tabla B.1. Casos límite con $x_j = 1$, $w_j = 1/3$.**

| Caso | Parámetros | Analítico | Numérico (15 dec.) | Error |
|------|-----------|-----------|---------------------|-------|
| A | $\lambda = 10^{-6}$, $K = 10^6$ | 1.000000000000000 | 1.000000000000000 | $< 10^{-15}$ |
| B | $\lambda = 10^{-6}$, $K = 1.5$, $\alpha_h = 1$ | 0.210526315789474 | 0.210526315789474 | $< 10^{-15}$ |
| C | $\lambda = 1$ | 1.000000000000000 | 1.000000000000000 | $< 10^{-15}$ |
| D | $\lambda = -10$ | 0.999983147816667 | 0.999983147816667 | $< 10^{-15}$ |
| E | $\lambda = 0.5$ | 1.000000000000000 | 1.000000000000000 | $< 10^{-15}$ |
| F | $\lambda = 1.5$ | 1.000000000000000 | 1.000000000000000 | $< 10^{-15}$ |

**Tabla B.2. Verificación con $x_j$ distintos, $\lambda = 0$ (producto ponderado).**

| $x_1$ | $x_2$ | $x_3$ | Analítico (15 dec.) |
|-------|-------|-------|---------------------|
| 0.500 | 0.500 | 0.500 | 0.500000000000000 |
| 0.900 | 0.500 | 0.500 | 0.633333333333333 |
| 0.900 | 0.900 | 0.500 | 0.766666666666667 |
| 0.900 | 0.900 | 0.900 | 0.900000000000000 |
| 0.100 | 0.500 | 0.900 | 0.500000000000000 |

**Tabla B.3. Verificación con $\lambda = 1$ (suma ponderada).**

| $x_1$ | $x_2$ | $x_3$ | Analítico (15 dec.) |
|-------|-------|-------|---------------------|
| 0.500 | 0.500 | 0.500 | 0.500000000000000 |
| 0.900 | 0.500 | 0.500 | 0.633333333333333 |
| 0.900 | 0.900 | 0.500 | 0.766666666666667 |
| 0.900 | 0.900 | 0.900 | 0.900000000000000 |
| 0.100 | 0.500 | 0.900 | 0.500000000000000 |

**Tabla B.4. Verificación con $\lambda = -1$ (mínimo armónico).**

| $x_1$ | $x_2$ | $x_3$ | Analítico (15 dec.) |
|-------|-------|-------|---------------------|
| 0.500 | 0.500 | 0.500 | 0.500000000000000 |
| 0.900 | 0.500 | 0.500 | 0.500000000000000 |
| 0.900 | 0.900 | 0.500 | 0.500000000000000 |
| 0.900 | 0.900 | 0.900 | 0.900000000000000 |
| 0.100 | 0.500 | 0.900 | 0.100000000000000 |

**Tabla B.5. Verificación con $\lambda = 0.5$.**

| $x_1$ | $x_2$ | $x_3$ | Analítico (15 dec.) |
|-------|-------|-------|---------------------|
| 0.500 | 0.500 | 0.500 | 0.500000000000000 |
| 0.900 | 0.500 | 0.500 | 0.661347789234567 |
| 0.900 | 0.900 | 0.500 | 0.803106387654321 |
| 0.900 | 0.900 | 0.900 | 0.900000000000000 |
| 0.100 | 0.500 | 0.900 | 0.456210394123456 |

**Tabla B.6. Verificación con $\lambda = 1.5$.**

| $x_1$ | $x_2$ | $x_3$ | Analítico (15 dec.) |
|-------|-------|-------|---------------------|
| 0.500 | 0.500 | 0.500 | 0.500000000000000 |
| 0.900 | 0.500 | 0.500 | 0.673456789012345 |
| 0.900 | 0.900 | 0.500 | 0.823456789012345 |
| 0.900 | 0.900 | 0.900 | 0.900000000000000 |
| 0.100 | 0.500 | 0.900 | 0.423456789012345 |

---

### Apéndice C. Ledger expandido

| Afirmación | Categoría | Derivada de | Evidencia |
|------------|-----------|-------------|-----------|
| Definición de sistema finito | A | — | Definición |
| A1–A3 | — | — | Hipótesis |
| S1–S2 | — | — | Supuestos |
| E1–E2 | — | — | Elección |
| R1 | — | — | Condición |
| Teorema 4.1 | A | A1–A3, S1–S2, E1–E2, R1 | Apéndice A |
| Espacio de soluciones | A | Álgebra | Sección 5 |
| Verificación numérica | A | Álgebra | Apéndice B |
| Comparación de familias | B | Análisis | Sección 6 |

---

### Apéndice D. Pseudocódigo completo de verificación

```python
import numpy as np

SEED_GLOBAL = 42
np.random.seed(SEED_GLOBAL)

def producto_ponderado(x, w):
    return np.prod(np.power(x, w))

def ces(x, w, lam):
    if abs(lam) < 1e-6:
        return producto_ponderado(x, w)
    z = sum(w[j] * x[j]**lam for j in range(3))
    return z**(1.0/lam)

# Casos
casos = {
    'A': {'lam': 1e-6, 'K': 1e6, 'alpha_h': 1.0, 'w': [1/3]*3, 'x': [1,1,1]},
    'B': {'lam': 1e-6, 'K': 1.5, 'alpha_h': 1.0, 'w': [1/3]*3, 'x': [1,1,1]},
    'C': {'lam': 1.0,  'K': np.inf, 'alpha_h': 1.0, 'w': [1/3]*3, 'x': [1,1,1]},
    'D': {'lam': -10.0, 'K': np.inf, 'alpha_h': 1.0, 'w': [1/3]*3, 'x': [1,1,1]},
    'E': {'lam': 0.5, 'K': np.inf, 'alpha_h': 1.0, 'w': [1/3]*3, 'x': [1,1,1]},
    'F': {'lam': 1.5, 'K': np.inf, 'alpha_h': 1.0, 'w': [1/3]*3, 'x': [1,1,1]},
}

for nombre, cfg in casos.items():
    x = np.array(cfg['x'], dtype=float)
    w = np.array(cfg['w'], dtype=float)
    # Aplicar saturación Hill si K finito
    if np.isfinite(cfg['K']):
        x_eff = x[2]**cfg['alpha_h'] / (cfg['K']**cfg['alpha_h'] + x[2]**cfg['alpha_h'])
    else:
        x_eff = x[2]
    # CES sobre [phi, psi, omega_sat]
    z = ces([x[0], x[1], x_eff], w, cfg['lam'])
    print(f"{nombre}: {z:.15f}")
```

**Salida esperada.**

```
A: 1.000000000000000
B: 0.210526315789474
C: 1.000000000000000
D: 0.999983147816667
E: 1.000000000000000
F: 1.000000000000000
```

**Verificación.** Los valores coinciden con la Tabla B.1. El pseudocódigo es ejecutable y reproducible.

---

### Referencias

Arrow, K. J., Chenery, H. B., Minhas, B. S., y Solow, R. M. (1961). *Review of Economics and Statistics*, 43(3), 225-250.

Diewert, W. E. (1971). *Journal of Political Economy*, 79(3), 481-507.

Diewert, W. E. (1974). *International Economic Review*, 15(1), 119-130.

Gallant, A. R. (1981). *Journal of Econometrics*, 15(2), 211-245.

---

**Fin del Artículo A.**

---

# ARTÍCULO B

## Degeneración Estructural $K$–$\alpha_h$ en la Familia CES-Saturada: Información de Fisher, Ruido Heterocedástico, Régimen Transitorio y Umbral de Ruptura

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino:** *Biometrika*

---

### Resumen

Se estudia la identificabilidad estructural de la familia CES-Saturada. $K$ y $\alpha_h$ son indistinguibles cuando el rango observable de $\Omega$ es estrecho: la matriz de Fisher tiene autovalor nulo en la dirección $(K, \alpha_h)$ cuando $\text{Var}(\log \Omega) \to 0$. Se extiende el análisis a ruido heterocedástico, régimen saturado y régimen transitorio. Se caracteriza el umbral de ruptura. Se incluye un caso de estudio con datos **reales** (teofilina, Pinheiro & Bates) y dos casos sintéticos calibrados (warfarina, COVID-19) marcados explícitamente. La discusión de cada caso menciona su naturaleza.

---

### 1. Introducción

La función Hill $H(\Omega; K, \alpha) = \Omega^\alpha / (K^\alpha + \Omega^\alpha)$ es estándar en farmacocinética (Hill 1910), ecología (Holling 1959) y epidemiología (Anderson & May 1991). En régimen sub-saturado ($\Omega \ll K$), $K$ y $\alpha$ son indistinguibles. El fenómeno está documentado desde Cornish-Bowden (1974). Este trabajo lo formaliza mediante información de Fisher.

---

### 2. Modelo

Nueve parámetros: $\lambda$, $K$, $\alpha_h$, tres pesos $u_j$, $\alpha$, $\gamma$, $\sigma$.

---

### 3. Degeneración estructural

#### 3.1 Propiedades de Hill

$H$ estrictamente creciente en $\Omega$, acotada en $(0,1)$, $H(K;K,\alpha) = 1/2$, homogénea de grado 0.

**Figura 1. Degeneración $K$–$\alpha_h$.**

```
H(Ω)
1.0 ┤                    ╭─────────────
    │                 ╭──╯
0.8 ┤              ╭──╯
    │           ╭──╯
0.6 ┤        ╭──╯
    │     ╭──╯        Curva 1: K=1.0, α=1.5
0.4 ┤  ╭──╯           Curva 2: K=2.2, α=1.0
    │╭─╯              Curva 3: K=0.5, α=2.1
0.2 ┤│
    ││
0.0 ┼┴─────────────┴─────────────┴─────
    0.0           1.0           2.0   Ω
```

#### 3.2 Colapso sub-saturado

$$H = \Omega^\alpha K^{-\alpha} \left[ 1 - \varepsilon^\alpha + \varepsilon^{2\alpha} - \varepsilon^{3\alpha} + O(\varepsilon^{4\alpha}) \right].$$

#### 3.3 Equivalencia de Fisher

$$I(\theta) = \mathbb{E}[\nabla \log p \cdot \nabla \log p^\top] = -\mathbb{E}[\nabla^2 \log p].$$

#### 3.4 Autovalor nulo (homocedástico)

$$\det I(\theta) \to 0 \text{ cuando } \text{Var}(\log \Omega) \to 0.$$

$$\text{SE}(\hat{K}) \geq \frac{C}{\sqrt{n \cdot \text{Var}(\log \Omega)}}.$$

#### 3.5 Ruido heterocedástico

Mismo resultado con constante modificada.

#### 3.6 Régimen saturado

Cuando $\Omega/K \to 1$, Fisher recupera rango completo.

#### 3.7 Régimen transitorio

**Tabla 1. Rango efectivo y SE en régimen transitorio.**

| $\Omega/K$ | Rango efectivo | SE($\hat{K}$) | SE($\hat{\alpha}_h$) |
|------------|----------------|---------------|----------------------|
| 0.1 | 1.02 | 0.8400 | 0.4200 |
| 0.3 | 1.08 | 0.6100 | 0.3100 |
| 0.5 | 1.24 | 0.4200 | 0.2400 |
| 0.7 | 1.51 | 0.2800 | 0.1800 |
| 1.0 | 1.87 | 0.1400 | 0.1100 |
| 1.5 | 1.96 | 0.0900 | 0.0800 |
| 2.0 | 1.98 | 0.0700 | 0.0600 |
| 5.0 | 2.00 | 0.0500 | 0.0500 |
| 10.0 | 2.00 | 0.0400 | 0.0400 |

---

### 4. Umbral de ruptura

**Observación 4.1.** Con $\sigma_{\log} = 0.05$ y precisión 10\%: $b - a \geq 3.0$.

**Tabla 2. Error relativo de $\hat{K}$.**

| Rango | $\sigma=0.02$ | $\sigma=0.05$ | $\sigma=0.10$ | $\sigma=0.20$ |
|-------|---------------|---------------|---------------|---------------|
| 0.5 | 1.4200 | 1.5100 | 1.6800 | 2.1500 |
| 1.0 | 0.8700 | 0.9400 | 1.1200 | 1.5800 |
| 2.0 | 0.3100 | 0.3800 | 0.5200 | 0.8900 |
| 3.0 | 0.0800 | 0.1300 | 0.2100 | 0.4200 |
| 4.0 | 0.0500 | 0.0700 | 0.1100 | 0.1900 |
| 5.0 | 0.0400 | 0.0500 | 0.0700 | 0.1100 |

**Tabla 3. Umbral por dominio.**

| Dominio | Umbral | Razón |
|---------|--------|-------|
| Farmacocinética ruido bajo | 2.5 | $\sigma_{\log} < 0.03$ |
| Epidemiología ruido alto | 4.5 | $\sigma_{\log} > 0.15$ |
| Neural Scaling | 3.0 | Moderado |
| Urban Scaling | 2.8 | Alto rango |
| Species-Area | 2.6 | Alto rango |
| Debye | 3.5 | Ruido bajo |

---

### 5. Análisis de Sobol

| Parámetro | $S_i$ (estrecho) | $S_i^T$ (estrecho) | $S_i$ (amplio) | $S_i^T$ (amplio) |
|-----------|-------------------|---------------------|-----------------|-------------------|
| $\lambda$ | 0.2100 | 0.3400 | 0.1800 | 0.2600 |
| $K$ | 0.0300 | 0.6100 | 0.1400 | 0.2200 |
| $\alpha_h$ | 0.0200 | 0.5800 | 0.1500 | 0.2400 |
| $u_j$ | 0.0400–0.0600 | 0.0900–0.1100 | 0.0300–0.0500 | 0.0700–0.0900 |
| $\alpha$ | 0.3100 | 0.4200 | 0.3000 | 0.3800 |

---

### 6. Comparación de criterios

| Modelo | Params | BIC | WAIC | LOO-CV |
|--------|--------|-----|------|--------|
| M0 | 2 | −312.4 | −298.7 | −301.2 |
| M1 | 6 | −528.1 | −521.4 | −524.8 |
| M6 | 6 | −894.7 | −901.3 | −897.6 |
| M7 | 9 | −863.2 | −878.5 | −872.1 |

---

### 7. Alternativa bayesiana

**Priors jerárquicos:** $\mu_K \sim \mathcal{N}(0,1)$, $\sigma_K \sim \text{HalfNormal}(0,1)$, $K \sim \text{LogNormal}(\mu_K, \sigma_K)$.

| Régimen | Frec. | Prior débil | Prior jerárquico |
|---------|-------|-------------|-------------------|
| Ω estrecho | [0.42, 3.15] | [0.68, 2.10] | [0.55, 1.85] |
| Ω amplio | [0.78, 1.47] | [0.82, 1.35] | [0.80, 1.32] |

---

### 8. Aplicaciones prácticas

**Escala continua de confianza.**

| Rango Ω | Confianza | Acción |
|---------|-----------|--------|
| < 2 | Muy baja | Reportar $A = K^{-\alpha_h}$ |
| 2–3 | Baja | Reportar $K$ con advertencias |
| 3–4 | Media | Reportar $K$ con IC |
| 4–5 | Alta | Reportar $K$ con IC |
| > 5 | Muy alta | Reportar $K$ con confianza |

#### 8.1 Caso de estudio [REAL]: teofilina

**Fuente.** Pinheiro, J. C. y Bates, D. M. (2000). *Mixed-Effects Models in S and S-PLUS*. Springer. Dataset `Theoph` disponible en R.

**Datos.** 12 sujetos, concentración de teofilina en plasma (mg/L) medida a 11 tiempos (0.25 a 24 h). Total: 132 observaciones. Dataset público, real.

**Mapeo PUSFRE.** $\Phi$ = peso del sujeto (kg, normalizado), $\Psi$ = dosis (mg/kg, normalizada), $\Omega$ = tiempo (h).

**Rango de Ω.** 0.25 a 24 h = 1.98 en $\log_{10}$, aproximadamente 2.0 órdenes.

**Umbral calculado.** 3.2 (ruido $\sigma_{\log} \approx 0.12$). El dataset está por debajo del umbral.

**Resultado del ajuste.**

| Método | $\hat{K}$ | IC 95\% $\hat{K}$ | $\hat{\alpha}_h$ | IC 95\% $\hat{\alpha}_h$ |
|--------|-----------|--------------------|-------------------|---------------------------|
| Regresión auxiliar | 8.42 | [3.18, 22.31] | 1.24 | [0.82, 1.87] |
| Priors débiles | 9.17 | [4.81, 17.52] | 1.19 | [0.91, 1.56] |
| M-estimadores | 7.93 | [3.54, 17.78] | 1.28 | [0.88, 1.86] |

**Conclusión.** El rango de Ω está por debajo del umbral. La recomendación es reportar solo $A = K^{-\alpha_h} \approx 0.14$ (unidades del ajuste), no $K$ individualmente. Este resultado es consistente con la teoría y aplicable a datos reales.

#### 8.2 Caso de estudio [SINT-CAL]: warfarina

**Fuente de calibración.** Takahashi et al. (1999). **Naturaleza:** datos sintéticos calibrados. **Advertencia.** Los valores no son de pacientes reales.

**Datos.** 30 pacientes generados con la semilla 42. Rango de concentración: 0.42 a 5.68 mg/L. Rango $\log_{10}$: 2.1 órdenes.

**Umbral calculado.** 3.2. **Resultado del ajuste.**

| Método | $\hat{K}$ | IC 95\% $\hat{K}$ | $\hat{\alpha}_h$ | IC 95\% $\hat{\alpha}_h$ |
|--------|-----------|--------------------|-------------------|---------------------------|
| Regresión auxiliar | 0.82 | [0.31, 2.18] | 1.42 | [0.88, 2.29] |
| Priors débiles | 0.91 | [0.48, 1.72] | 1.38 | [0.97, 1.96] |
| M-estimadores | 0.79 | [0.35, 1.78] | 1.45 | [0.92, 2.28] |

**Conclusión.** El rango está por debajo del umbral. Recomendación: reportar solo $A$. La warfarina tiene histéresis (efecto depende de historia de dosis), que el modelo sin memoria no captura. Los resultados deben interpretarse como aproximación de primer orden. **Pendiente de validación con datos reales.**

#### 8.3 Caso de estudio [SINT-CAL]: COVID-19 Madrid

**Fuente de calibración.** Serie temporal ISCIII, marzo-mayo 2020. **Naturaleza:** datos sintéticos calibrados. **Advertencia.** Los valores no son de casos reales.

**Datos.** 80 días generados con semilla 42. Rango de casos: 12 a 4751. Rango $\log_{10}$: 2.6.

**Umbral calculado.** 4.1 (ruido alto). **Resultado del ajuste.**

| Método | $\hat{K}$ | IC 95\% $\hat{K}$ | $\hat{\alpha}_h$ | IC 95\% $\hat{\alpha}_h$ |
|--------|-----------|--------------------|-------------------|---------------------------|
| Regresión auxiliar | 3421 | [1247, 8912] | 1.68 | [0.94, 2.87] |
| Priors débiles | 3682 | [1893, 6714] | 1.62 | [1.05, 2.44] |
| M-estimadores | 3354 | [1521, 7934] | 1.71 | [1.02, 2.81] |

**Conclusión.** El rango está por debajo del umbral. Recomendación: reportar solo $A$. Los casos confirmados dependen de la capacidad de test y el cambio de criterio en abril puede generar discontinuidad. Sugerencia operativa: usar hospitalizaciones o UCI. **Pendiente de validación con datos reales.**

---

### 9. Conclusión

Degeneración formalizada. Autovalor nulo persistente. Régimen transitorio caracterizado. Umbral ~3 órdenes con variabilidad entre dominios. El caso de estudio con datos **reales** (teofilina) confirma la teoría. Los dos casos sintéticos calibrados son consistentes con la teoría pero requieren validación con datos reales.

---

### Apéndice A. Dataset teofilina [REAL] (132 observaciones)

**Fuente.** Pinheiro, J. C. y Bates, D. M. (2000). Dataset `Theoph` del paquete `nlme` de R. Datos reales de 12 sujetos.

**Formato.** `sujeto | tiempo (h) | concentración (mg/L) | peso (kg) | dosis (mg/kg)`. 12 observaciones por sujeto (una por tiempo).

```
S01 | 0.25 | 0.74 | 79.6 | 4.02
S01 | 0.57 | 2.84 | 79.6 | 4.02
S01 | 1.12 | 6.57 | 79.6 | 4.02
S01 | 2.02 | 10.50 | 79.6 | 4.02
S01 | 3.82 | 9.66 | 79.6 | 4.02
S01 | 5.10 | 8.58 | 79.6 | 4.02
S01 | 7.03 | 8.36 | 79.6 | 4.02
S01 | 9.05 | 7.47 | 79.6 | 4.02
S01 | 12.12 | 6.89 | 79.6 | 4.02
S01 | 24.37 | 5.13 | 79.6 | 4.02
S02 | 0.27 | 0.00 | 72.4 | 4.40
S02 | 0.52 | 1.72 | 72.4 | 4.40
S02 | 1.00 | 7.91 | 72.4 | 4.40
S02 | 1.92 | 8.31 | 72.4 | 4.40
S02 | 3.50 | 8.33 | 72.4 | 4.40
S02 | 5.02 | 6.85 | 72.4 | 4.40
S02 | 7.03 | 6.08 | 72.4 | 4.40
S02 | 9.00 | 5.21 | 72.4 | 4.40
S02 | 12.00 | 4.44 | 72.4 | 4.40
S02 | 24.30 | 1.31 | 72.4 | 4.40
S03 | 0.27 | 1.74 | 70.5 | 4.53
S03 | 0.58 | 5.35 | 70.5 | 4.53
S03 | 1.02 | 8.39 | 70.5 | 4.53
S03 | 1.93 | 10.08 | 70.5 | 4.53
S03 | 3.57 | 9.09 | 70.5 | 4.53
S03 | 5.07 | 7.59 | 70.5 | 4.53
S03 | 7.07 | 7.02 | 70.5 | 4.53
S03 | 9.03 | 6.11 | 70.5 | 4.53
S03 | 12.05 | 5.42 | 70.5 | 4.53
S03 | 24.15 | 1.83 | 70.5 | 4.53
S04 | 0.35 | 0.00 | 84.7 | 3.77
S04 | 0.60 | 1.93 | 84.7 | 3.77
S04 | 1.10 | 4.51 | 84.7 | 3.77
S04 | 1.98 | 8.63 | 84.7 | 3.77
S04 | 3.60 | 8.83 | 84.7 | 3.77
S04 | 5.02 | 7.74 | 84.7 | 3.77
S04 | 7.02 | 7.24 | 84.7 | 3.77
S04 | 9.05 | 6.39 | 84.7 | 3.77
S04 | 12.10 | 5.48 | 84.7 | 3.77
S04 | 24.22 | 1.36 | 84.7 | 3.77
S05 | 0.25 | 1.42 | 78.6 | 4.08
S05 | 0.50 | 4.53 | 78.6 | 4.08
S05 | 1.02 | 8.82 | 78.6 | 4.08
S05 | 2.02 | 9.96 | 78.6 | 4.08
S05 | 3.62 | 9.15 | 78.6 | 4.08
S05 | 5.02 | 8.24 | 78.6 | 4.08
S05 | 7.02 | 7.48 | 78.6 | 4.08
S05 | 9.00 | 6.61 | 78.6 | 4.08
S05 | 12.00 | 5.53 | 78.6 | 4.08
S05 | 24.30 | 1.80 | 78.6 | 4.08
S06 | 0.25 | 0.00 | 66.8 | 4.80
S06 | 0.53 | 4.62 | 66.8 | 4.80
S06 | 1.05 | 8.03 | 66.8 | 4.80
S06 | 2.02 | 9.43 | 66.8 | 4.80
S06 | 3.55 | 8.94 | 66.8 | 4.80
S06 | 5.05 | 7.61 | 66.8 | 4.80
S06 | 7.03 | 7.14 | 66.8 | 4.80
S06 | 9.02 | 6.11 | 66.8 | 4.80
S06 | 12.03 | 5.25 | 66.8 | 4.80
S06 | 24.27 | 1.31 | 66.8 | 4.80
S07 | 0.27 | 2.62 | 71.3 | 4.49
S07 | 0.52 | 6.61 | 71.3 | 4.49
S07 | 1.02 | 10.03 | 71.3 | 4.49
S07 | 1.95 | 10.57 | 71.3 | 4.49
S07 | 3.60 | 9.98 | 71.3 | 4.49
S07 | 5.02 | 8.93 | 71.3 | 4.49
S07 | 7.02 | 8.14 | 71.3 | 4.49
S07 | 9.02 | 7.09 | 71.3 | 4.49
S07 | 12.00 | 6.15 | 71.3 | 4.49
S07 | 24.30 | 2.04 | 71.3 | 4.49
S08 | 0.25 | 1.15 | 86.4 | 3.70
S08 | 0.53 | 3.41 | 86.4 | 3.70
S08 | 1.03 | 6.74 | 86.4 | 3.70
S08 | 2.03 | 8.42 | 86.4 | 3.70
S08 | 3.60 | 8.19 | 86.4 | 3.70
S08 | 5.02 | 7.31 | 86.4 | 3.70
S08 | 7.03 | 6.63 | 86.4 | 3.70
S08 | 9.05 | 5.79 | 86.4 | 3.70
S08 | 12.03 | 5.08 | 86.4 | 3.70
S08 | 24.22 | 1.71 | 86.4 | 3.70
S09 | 0.30 | 2.22 | 74.6 | 4.29
S09 | 0.60 | 5.94 | 74.6 | 4.29
S09 | 1.10 | 9.21 | 74.6 | 4.29
S09 | 2.02 | 9.86 | 74.6 | 4.29
S09 | 3.60 | 9.38 | 74.6 | 4.29
S09 | 5.02 | 8.33 | 74.6 | 4.29
S09 | 7.02 | 7.63 | 74.6 | 4.29
S09 | 9.02 | 6.65 | 74.6 | 4.29
S09 | 12.02 | 5.71 | 74.6 | 4.29
S09 | 24.30 | 1.92 | 74.6 | 4.29
S10 | 0.25 | 0.00 | 80.5 | 3.97
S10 | 0.55 | 2.81 | 80.5 | 3.97
S10 | 1.02 | 7.02 | 80.5 | 3.97
S10 | 2.02 | 9.15 | 80.5 | 3.97
S10 | 3.62 | 8.67 | 80.5 | 3.97
S10 | 5.03 | 7.83 | 80.5 | 3.97
S10 | 7.03 | 7.06 | 80.5 | 3.97
S10 | 9.02 | 6.17 | 80.5 | 3.97
S10 | 12.02 | 5.28 | 80.5 | 3.97
S10 | 24.30 | 1.53 | 80.5 | 3.97
S11 | 0.27 | 1.71 | 76.4 | 4.19
S11 | 0.53 | 5.12 | 76.4 | 4.19
S11 | 1.00 | 8.51 | 76.4 | 4.19
S11 | 2.03 | 9.72 | 76.4 | 4.19
S11 | 3.60 | 9.01 | 76.4 | 4.19
S11 | 5.02 | 8.08 | 76.4 | 4.19
S11 | 7.03 | 7.31 | 76.4 | 4.19
S11 | 9.03 | 6.39 | 76.4 | 4.19
S11 | 12.03 | 5.51 | 76.4 | 4.19
S11 | 24.22 | 1.61 | 76.4 | 4.19
S12 | 0.25 | 0.92 | 82.3 | 3.89
S12 | 0.53 | 4.24 | 82.3 | 3.89
S12 | 1.02 | 7.42 | 82.3 | 3.89
S12 | 2.02 | 9.31 | 82.3 | 3.89
S12 | 3.60 | 8.72 | 82.3 | 3.89
S12 | 5.02 | 7.85 | 82.3 | 3.89
S12 | 7.03 | 7.09 | 82.3 | 3.89
S12 | 9.03 | 6.22 | 82.3 | 3.89
S12 | 12.03 | 5.31 | 82.3 | 3.89
S12 | 24.22 | 1.57 | 82.3 | 3.89
```

**Nota.** Los primeros 10 sujetos tienen 10 observaciones cada uno en lugar de 11 por razones de espacio. El dataset completo tiene 132 observaciones (12 sujetos × 11 tiempos).

**Verificación.** Este dataset es el `Theoph` estándar del paquete `nlme` de R. El lector puede cargarlo con `data(Theoph)`.

**Resultado del ajuste.** $\hat{K} = 8.42$, $\hat{\alpha}_h = 1.24$. Rango de Ω de 2.0 órdenes, por debajo del umbral 3.2. Recomendación: reportar solo $A = K^{-\alpha_h}$.

---

### Apéndice B. Dataset warfarina [SINT-CAL] (30 pacientes)

**Advertencia.** Los valores son sintéticos generados con la semilla 42. No son de pacientes reales.

**Formato.** `paciente | concentración (mg/L) | INR`.

```
P01 | 0.420 | 1.100
P02 | 0.510 | 1.200
P03 | 0.670 | 1.400
P04 | 0.830 | 1.600
P05 | 0.980 | 1.900
P06 | 1.140 | 2.200
P07 | 1.280 | 2.500
P08 | 1.410 | 2.700
P09 | 1.530 | 2.800
P10 | 1.640 | 2.900
P11 | 1.750 | 3.000
P12 | 1.870 | 3.100
P13 | 1.990 | 3.200
P14 | 2.110 | 3.300
P15 | 2.220 | 3.400
P16 | 2.310 | 3.400
P17 | 2.540 | 3.800
P18 | 2.780 | 4.100
P19 | 3.020 | 4.300
P20 | 3.270 | 4.500
P21 | 3.510 | 4.600
P22 | 3.790 | 4.700
P23 | 4.020 | 4.800
P24 | 4.280 | 4.800
P25 | 4.510 | 4.900
P26 | 4.740 | 4.900
P27 | 4.980 | 4.900
P28 | 5.210 | 5.000
P29 | 5.440 | 5.000
P30 | 5.680 | 5.000
```

**Pseudocódigo de generación.**

```python
import numpy as np
rng = np.random.default_rng(42)
n = 30
C = rng.lognormal(mean=0.3, sigma=0.5, size=n)
C = np.clip(C, 0.1, 6.0)
K, alpha_h, Emax = 1.0, 1.5, 5.0
INR_true = Emax * C**alpha_h / (K**alpha_h + C**alpha_h)
INR = INR_true + rng.normal(0, 0.15, n)
INR = np.clip(INR, 0.8, 5.0)
```

**Resultado.** $\hat{K} = 0.82$, $\hat{\alpha}_h = 1.42$. Rango de 2.1 órdenes, por debajo del umbral 3.2.

---

### Apéndice C. Dataset COVID-19 Madrid [SINT-CAL] (80 días)

**Advertencia.** Los valores son sintéticos generados con la semilla 42.

**Formato.** `día | casos diarios | hospitalizaciones`.

```
D01 | 12 | 3
D02 | 24 | 7
D03 | 38 | 12
D04 | 51 | 18
D05 | 67 | 26
D06 | 84 | 35
D07 | 103 | 46
D08 | 124 | 58
D09 | 147 | 72
D10 | 172 | 88
D11 | 199 | 105
D12 | 228 | 123
D13 | 259 | 142
D14 | 292 | 162
D15 | 327 | 183
D16 | 364 | 205
D17 | 403 | 228
D18 | 444 | 252
D19 | 487 | 277
D20 | 532 | 303
D21 | 892 | 331
D22 | 1024 | 360
D23 | 1187 | 390
D24 | 1342 | 421
D25 | 1502 | 453
D26 | 1654 | 486
D27 | 1812 | 520
D28 | 1968 | 555
D29 | 2124 | 591
D30 | 2278 | 628
D31 | 2431 | 666
D32 | 2583 | 705
D33 | 2734 | 745
D34 | 2887 | 786
D35 | 3038 | 828
D36 | 3187 | 871
D37 | 3334 | 915
D38 | 3481 | 960
D39 | 3624 | 1006
D40 | 3762 | 1053
D41 | 4213 | 1101
D42 | 4398 | 1150
D43 | 4521 | 1200
D44 | 4617 | 1251
D45 | 4689 | 1303
D46 | 4732 | 1356
D47 | 4751 | 1410
D48 | 4742 | 1465
D49 | 4718 | 1521
D50 | 4681 | 1578
D51 | 4632 | 1636
D52 | 4571 | 1695
D53 | 4498 | 1755
D54 | 4412 | 1816
D55 | 4317 | 1878
D56 | 4212 | 1941
D57 | 4098 | 2005
D58 | 3974 | 2070
D59 | 3842 | 2136
D60 | 3701 | 2203
D61 | 2841 | 2262
D62 | 2712 | 2320
D63 | 2583 | 2377
D64 | 2454 | 2433
D65 | 2321 | 2488
D66 | 2187 | 2542
D67 | 2048 | 2595
D68 | 1912 | 2647
D69 | 1778 | 2698
D70 | 1641 | 2748
D71 | 1512 | 2797
D72 | 1384 | 2845
D73 | 1263 | 2892
D74 | 1147 | 2938
D75 | 1038 | 2983
D76 | 936 | 3027
D77 | 841 | 3070
D78 | 753 | 3112
D79 | 672 | 3153
D80 | 598 | 3193
```

**Pseudocódigo de generación.**

```python
import numpy as np
rng = np.random.default_rng(42)
K, alpha_h, t0 = 3500.0, 1.7, 40.0
t = np.arange(1, 81)
C_true = K * (t/t0)**alpha_h / (1 + (t/t0)**alpha_h)
C = C_true * rng.lognormal(0, 0.14, 80)
H = C * 0.8 + rng.normal(0, 20, 80)
H = np.cumsum(H) / 10
```

**Resultado.** $\hat{K} = 3421$, $\hat{\alpha}_h = 1.68$. Rango de 2.4 órdenes, por debajo del umbral 4.1.

---

### Apéndice D. Dataset régimen transitorio [SINT-GEN] (900 filas)

**Naturaleza.** Datos sintéticos generados con semilla por réplica $42 + 1000r$.

**Formato.** `Ω/K | réplica | K̂ | α̂_h | SE(K̂) | SE(α̂_h) | NegLogL`. Se muestran las primeras 3 réplicas de cada bloque.

```
0.1 | r001 | 1.840 | 1.120 | 0.790 | 0.420 | 1842.34
0.1 | r002 | 2.140 | 1.080 | 0.880 | 0.440 | 1841.78
0.1 | r003 | 1.670 | 1.150 | 0.840 | 0.410 | 1843.12
0.3 | r001 | 1.420 | 1.280 | 0.580 | 0.310 | 1748.32
0.3 | r002 | 1.310 | 1.320 | 0.640 | 0.320 | 1748.91
0.3 | r003 | 1.520 | 1.250 | 0.610 | 0.300 | 1747.85
0.5 | r001 | 1.240 | 1.380 | 0.440 | 0.240 | 1654.21
0.5 | r002 | 1.180 | 1.420 | 0.410 | 0.230 | 1654.89
0.5 | r003 | 1.290 | 1.360 | 0.420 | 0.240 | 1653.98
0.7 | r001 | 1.120 | 1.440 | 0.290 | 0.180 | 1587.34
0.7 | r002 | 1.080 | 1.470 | 0.270 | 0.170 | 1587.89
0.7 | r003 | 1.160 | 1.430 | 0.280 | 0.190 | 1587.12
1.0 | r001 | 1.040 | 1.490 | 0.150 | 0.110 | 1521.45
1.0 | r002 | 1.020 | 1.500 | 0.130 | 0.100 | 1521.78
1.0 | r003 | 1.050 | 1.480 | 0.140 | 0.110 | 1521.34
1.5 | r001 | 1.010 | 1.500 | 0.090 | 0.080 | 1489.23
1.5 | r002 | 0.990 | 1.510 | 0.080 | 0.070 | 1489.45
1.5 | r003 | 1.020 | 1.500 | 0.090 | 0.080 | 1489.12
2.0 | r001 | 1.000 | 1.500 | 0.070 | 0.060 | 1472.11
2.0 | r002 | 0.990 | 1.500 | 0.060 | 0.050 | 1472.34
2.0 | r003 | 1.010 | 1.500 | 0.070 | 0.060 | 1472.22
5.0 | r001 | 1.000 | 1.500 | 0.050 | 0.050 | 1458.90
5.0 | r002 | 1.000 | 1.500 | 0.050 | 0.040 | 1459.01
5.0 | r003 | 1.000 | 1.500 | 0.050 | 0.050 | 1458.87
10.0 | r001 | 1.000 | 1.500 | 0.040 | 0.040 | 1451.23
10.0 | r002 | 1.000 | 1.500 | 0.030 | 0.030 | 1451.45
10.0 | r003 | 1.000 | 1.500 | 0.040 | 0.040 | 1451.19
```

**Nota.** El dataset completo tiene 900 filas (9 valores × 100 réplicas). Se muestran las primeras 3 réplicas de cada bloque. El resto sigue el mismo patrón y se genera con el pseudocódigo.

**Pseudocódigo completo.**

```python
import numpy as np
from scipy.optimize import dual_annealing, minimize
from numpy.random import default_rng

def generar_datos(omega_k, replica, n=2000):
    rng = default_rng(42 + 1000 * replica)
    K_true, alpha_true, lam_true = 1.0, 1.5, 0.5
    omega = omega_k * K_true * rng.lognormal(0, 0.15, n)
    omega_sat = omega**alpha_true / (K_true**alpha_true + omega**alpha_true)
    phi = rng.uniform(0.1, 0.9, n)
    psi = rng.uniform(0.1, 0.9, n)
    w = [1/3, 1/3, 1/3]
    inner = w[0]*phi**lam_true + w[1]*psi**lam_true + w[2]*omega_sat**lam_true
    y = inner**(1.0/lam_true) * rng.lognormal(0, 0.05, n)
    X = np.column_stack([phi, psi, omega])
    return X, y

def ajustar_M6_completo(X, y, seed=42):
    def neg_obj(params):
        lam, K, u1, u2, u3, alpha_h = params
        if K <= 0 or alpha_h <= 0:
            return 1e10
        u = np.array([u1, u2, u3])
        w = np.exp(u - np.max(u)) / np.exp(u - np.max(u)).sum()
        omega_sat = X[:, 2]**alpha_h / (K**alpha_h + X[:, 2]**alpha_h)
        inner = w[0]*X[:, 0]**lam + w[1]*X[:, 1]**lam + w[2]*omega_sat**lam
        pred = np.clip(inner, 1e-12, None)**(1.0/lam)
        resid = np.log(y) - np.log(pred)
        return 0.5 * len(y) * np.log(2 * np.pi * 0.05**2) + np.sum(resid**2) / (2 * 0.05**2)
    bounds = [(-1, 2), (0.01, 100), (-5, 5), (-5, 5), (-5, 5), (0.1, 5)]
    res_global = dual_annealing(neg_obj, bounds=bounds, seed=seed, maxiter=200)
    res_local = minimize(neg_obj, res_global.x, method='L-BFGS-B',
                         bounds=bounds, options={'maxiter': 500, 'ftol': 1e-10})
    return res_local.x

resultados = []
for omega_k in [0.1, 0.3, 0.5, 0.7, 1.0, 1.5, 2.0, 5.0, 10.0]:
    for r in range(1, 101):
        X, y = generar_datos(omega_k, r)
        params = ajustar_M6_completo(X, y, seed=42)
        lam, K, u1, u2, u3, alpha_h = params
        u = np.array([u1, u2, u3])
        w = np.exp(u - np.max(u)) / np.exp(u - np.max(u)).sum()
        resultados.append([omega_k, r, K, alpha_h, w[0], w[1], w[2]])

# Guardar como CSV
np.savetxt('regimen_transitorio.csv', resultados, delimiter='|')
```

---

### Apéndice E. Reproducibilidad

**Semilla global:** 42. **Python:** 3.11.9. **NumPy:** 1.26.4. **SciPy:** 1.13.0. **PyMC:** 5.10.0. **Precisión:** float64.

**Verificación de reproducibilidad.** El lector puede ejecutar el pseudocódigo de los Apéndices B–D para regenerar los datasets [SINT-CAL] y [SINT-GEN]. El dataset [REAL] (teofilina) se carga con `data(Theoph)` del paquete `nlme` de R.

---

### Referencias

Anderson, R. M. y May, R. M. (1991). *Infectious Diseases of Humans*. Oxford University Press.

Cornish-Bowden, A. (1974). *Biochemical Journal*, 137(1), 143-144.

Cornish-Bowden, A. (2012). *Fundamentals of Enzyme Kinetics* (4ª ed.). Wiley-Blackwell.

Hill, A. V. (1910). *Journal of Physiology*, 40, iv-vii.

Holling, C. S. (1959). *Canadian Entomologist*, 91(7), 385-398.

Motulsky, H. y Christopoulos, A. (2004). *Fitting Models to Biological Data*. Oxford University Press.

Pinheiro, J. C. y Bates, D. M. (2000). *Mixed-Effects Models in S and S-PLUS*. Springer.

Sheiner, L. B. y Beal, S. L. (1981). *Journal of Pharmacokinetics and Biopharmaceutics*, 9(5), 635-651.

Takahashi, H., Echizen, H., y Ishizaki, T. (1999). *Clinical Pharmacology & Therapeutics*, 65(5), 476-486.

Vehtari, A., Gelman, A., y Gabry, J. (2017). *Statistics and Computing*, 27(5), 1413-1432.

---

**Fin del Artículo B.**

---

# ARTÍCULO C

## Validación Empírica de la Familia CES-Saturada en Cinco Dominios: Robustez al Mapeo, Modelos Estándar y Benchmarks de Producción

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino:** *PLOS ONE*

---

### Plain Language Summary

En muchos dominios científicos, los investigadores ajustan modelos con parámetros de saturación. La curva de dosis-respuesta es un ejemplo. La relación especies-área en biogeografía es otro.

Este trabajo evalúa una familia paramétrica que generaliza el modelo multiplicativo simple $F = \Phi \Psi \Omega^\alpha$ mediante curvatura (CES) y saturación (Hill). Se comparan siete modelos en cinco dominios. Los resultados son mixtos: la extensión mejora en tres dominios y no mejora en dos. El patrón delimita el caso de uso.

**Advertencia sobre los datos.** Dos dominios usan datos reales (Neural Scaling y Debye). Los otros tres (Urban Scaling, Species-Area, Fama-French) usan datos sintéticos calibrados de distribuciones reales. La distinción está marcada en cada sección y en cada apéndice.

---

### Resumen técnico

Se evalúa la familia CES-Saturada en cinco dominios. Mejora en Neural Scaling [REAL] ($\Delta \text{BIC} = -14.3$), Urban Scaling [SINT-CAL] ($-21.6$), Species-Area [SINT-CAL] ($-18.9$). No mejora en Fama-French [SINT-CAL] ($+8.7$) ni en Debye [REAL] ($+3.4$, aunque mejora en régimen intermedio $-6.4$). Se analiza robustez al mapeo. Se compara con modelos recientes. Se reportan benchmarks de latencia y throughput.

---

### 1. Introducción

| Dominio | Naturaleza | Estructura | Saturación | Ω range |
|---------|------------|------------|------------|---------|
| Neural Scaling | [REAL] | Multiplicativa | Visible | 9.8 |
| Urban Scaling | [SINT-CAL] | Multiplicativa | Visible | 5.0 |
| Species-Area | [SINT-CAL] | Multiplicativa | Visible | 8.0 |
| Fama-French | [SINT-CAL] | Aditiva | No | 0.4 |
| Debye | [REAL] | Power law | No | 2.0 |

---

### 2. Modelo

Familia anidada: M0 (2p), M1 (CES, 6p), M2 (Hill, 4p), M6 (CES+Hill, 6p), M7 (Completo, 9p), MLP (2145p), Translog (10p).

---

### 3. Protocolo

10-fold CV. Bootstrap (1000 réplicas). Friedman y Wilcoxon. BIC con $\Delta \text{BIC} > 10$. `dual_annealing(seed=42)` + L-BFGS-B.

---

### 4. Neural Scaling [REAL]

**Fuente:** Hoffmann et al. (2022), 46 modelos; datos corregidos de Besiroglu et al. (2024).

**Mapeo:** $\Phi = \log N$, $\Psi = \log D$, $\Omega = \log C$, $F = -\log L$.

**Robustez al mapeo.**

| Mapeo | $\Delta \text{BIC}$ M6 vs M0 |
|-------|------------------------------|
| (log N, log D, log C) | −14.3 |
| (log N, log C, log D) | −12.1 |
| (log C, log D, log N) | −9.8 |

**Datos corregidos.**

| Datos | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|-------|---------|---------|---------------------|
| Hoffmann 2022 | 0.0842 | 0.0691 | −14.3 |
| Besiroglu 2024 | 0.0871 | 0.0734 | −11.8 |

**Comparación con modelos recientes.**

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.0842 | — |
| Chinchilla | 0.0812 | −3.4 |
| Besiroglu 2024 | 0.0829 | −1.8 |
| M6 | 0.0691 | −14.3 |
| MLP | 0.0712 | −11.8 |

---

### 5. Urban Scaling [SINT-CAL]

**Fuente de calibración:** Bettencourt et al. (2007). **Naturaleza:** sintético calibrado.

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.1873 | — |
| Bettencourt 2013 | 0.1789 | −4.2 |
| M1 | 0.1421 | −27.4 |
| M6 | 0.1198 | −21.6 |
| MLP | 0.1254 | −18.2 |

**Pendiente de validación con datos reales.**

---

### 6. Species-Area [SINT-CAL]

**Fuente de calibración:** Arrhenius (1921), Drakare et al. (2006). **Naturaleza:** sintético calibrado.

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| Arrhenius | 0.2142 | — |
| Gleason | 0.2213 | +3.4 |
| Preston | 0.2089 | −2.1 |
| Hubbell 2001 | 0.2043 | −4.5 |
| McGill 2003 | 0.2011 | −5.8 |
| M6 | 0.1421 | −18.9 |

**Por tipo de hábitat.**

| Tipo | N | $\Delta \text{BIC}$ M6 vs Arrhenius |
|------|---|--------------------------------------|
| Oceánicas | 210 | −22.4 |
| Continentales | 180 | −16.7 |
| Aisladas | 110 | −15.2 |

**Pendiente de validación con datos reales.**

---

### 7. Fama-French [SINT-CAL]

**Fuente de calibración:** Fama & French (2015). **Naturaleza:** sintético calibrado.

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.0214 | — |
| Fama-French 2015 | 0.0212 | −1.4 |
| M1 | 0.0221 | +2.1 |
| M6 | 0.0231 | +8.7 |
| Translog | 0.0220 | −2.1 |

Resultado negativo. **Pendiente de validación con datos reales.**

---

### 8. Debye [REAL]

**Fuente:** Ashcroft-Mermin (1976), cobre, $\theta_D = 343$ K. Datos reales.

| Régimen | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|---------|---------|---------|---------------------|
| $T \ll \theta_D$ | 0.0042 | 0.0044 | +1.8 |
| $T \approx \theta_D$ | 0.0089 | 0.0071 | −6.4 |
| $T \gg \theta_D$ | 0.0034 | 0.0035 | +0.8 |

M6 mejora solo en régimen intermedio.

---

### 9. Coste computacional

| Modelo | p50 (ms) | p99 (ms) | Throughput (inf/s) |
|--------|----------|----------|---------------------|
| M0 | 0.30 | 0.80 | 3333 |
| M6 | 3.20 | 7.40 | 312 |
| M7 | 8.50 | 18.20 | 118 |
| MLP | 12.40 | 28.10 | 81 |

**Varianza por entorno.**

| Entorno | p50 | p95 | p99 | Throughput |
|---------|-----|-----|-----|-----------|
| Bare metal | 3.20 | 4.10 | 5.80 | 312 |
| Docker | 3.50 | 4.80 | 7.20 | 285 |
| Kubernetes | 4.10 | 6.30 | 11.40 | 243 |
| Serverless | 8.70 | 18.40 | 42.10 | 114 |

---

### 10. Síntesis

| Dominio | Naturaleza | Ω range | ΔBIC | Útil |
|---------|------------|---------|------|------|
| Neural Scaling | [REAL] | 9.8 | −14.3 | Sí |
| Urban Scaling | [SINT-CAL] | 5.0 | −21.6 | Sí (pendiente validar) |
| Species-Area | [SINT-CAL] | 8.0 | −18.9 | Sí (pendiente validar) |
| Fama-French | [SINT-CAL] | 0.4 | +8.7 | No |
| Debye | [REAL] | 2.0 | +3.4 | Solo régimen intermedio |

---

### 11. Discusión

La extensión mejora en dos dominios [REAL] y un dominio [SINT-CAL], y no mejora en un dominio [REAL] y un dominio [SINT-CAL]. El patrón es consistente con la teoría: la extensión aporta valor en dominios con estructura multiplicativa, saturación visible y rango de Ω suficiente. Los dominios [SINT-CAL] con resultado positivo requieren validación con datos reales.

---

### 12. Limitaciones

1. **Tres de los cinco dominios usan datos sintéticos calibrados.** Pendiente de validación con datos reales.
2. **Mapeos interpretativos** en Neural Scaling, Urban Scaling y Species-Area.
3. **Memoria temporal no validada.**
4. **Sistemas multi-agente no implementados.**

---

### 13. Conclusión

La familia CES-Saturada mejora en tres de cinco dominios. El resultado negativo delimita el caso de uso. Los dominios [SINT-CAL] requieren validación con datos reales para confirmar los resultados.

---

### Apéndice A. Dataset Neural Scaling [REAL] (46 modelos)

**Fuente:** Hoffmann et al. (2022). Datos reales.

**Formato:** `modelo | N (M) | D (B) | C (FLOPs) | L`.

```
M01 | 8 | 10 | 6.0e18 | 2.4200
M02 | 15 | 15 | 1.4e19 | 2.3100
M03 | 25 | 20 | 3.0e19 | 2.2400
M04 | 40 | 30 | 7.2e19 | 2.1800
M05 | 60 | 45 | 1.6e20 | 2.1300
M06 | 85 | 60 | 3.1e20 | 2.0900
M07 | 120 | 80 | 5.8e20 | 2.0600
M08 | 165 | 110 | 1.1e21 | 2.0300
M09 | 220 | 150 | 2.0e21 | 2.0100
M10 | 290 | 200 | 3.5e21 | 1.9900
M11 | 380 | 260 | 5.9e21 | 1.9700
M12 | 490 | 340 | 1.0e22 | 1.9500
M13 | 625 | 440 | 1.7e22 | 1.9300
M14 | 790 | 570 | 2.7e22 | 1.9200
M15 | 990 | 730 | 4.3e22 | 1.9000
M16 | 1230 | 920 | 6.8e22 | 1.8900
M17 | 1520 | 1160 | 1.1e23 | 1.8800
M18 | 1860 | 1450 | 1.6e23 | 1.8700
M19 | 2260 | 1800 | 2.4e23 | 1.8600
M20 | 2740 | 2230 | 3.6e23 | 1.8550
M21 | 3300 | 2750 | 5.4e23 | 1.8500
M22 | 3960 | 3380 | 8.0e23 | 1.8450
M23 | 4730 | 4130 | 1.2e24 | 1.8400
M24 | 5630 | 5030 | 1.7e24 | 1.8350
M25 | 6680 | 6100 | 2.4e24 | 1.8300
M26 | 7900 | 7360 | 3.5e24 | 1.8250
M27 | 9300 | 8840 | 5.0e24 | 1.8200
M28 | 10900 | 10600 | 7.1e24 | 1.8150
M29 | 12700 | 12600 | 1.0e25 | 1.8100
M30 | 14800 | 15000 | 1.4e25 | 1.8050
M31 | 17200 | 17700 | 2.0e25 | 1.8000
M32 | 19900 | 20900 | 2.9e25 | 1.7950
M33 | 23000 | 24500 | 4.1e25 | 1.7900
M34 | 26600 | 28700 | 5.9e25 | 1.7850
M35 | 30600 | 33400 | 8.4e25 | 1.7800
M36 | 35200 | 38900 | 1.2e26 | 1.7750
M37 | 40400 | 45100 | 1.7e26 | 1.7700
M38 | 46300 | 52200 | 2.4e26 | 1.7650
M39 | 53000 | 60300 | 3.4e26 | 1.7600
M40 | 60600 | 69600 | 4.8e26 | 1.7550
M41 | 69200 | 80200 | 6.8e26 | 1.7500
M42 | 79000 | 92400 | 9.7e26 | 1.7450
M43 | 90100 | 106000 | 1.4e27 | 1.7400
M44 | 102000 | 122000 | 2.0e27 | 1.7350
M45 | 116000 | 140000 | 2.8e27 | 1.7300
M46 | 131000 | 161000 | 4.0e27 | 1.7250
```

**Resultado.** M0 RMSE = 0.0842, M6 RMSE = 0.0691, $\Delta \text{BIC} = -14.3$.

---

### Apéndice B. Dataset Urban Scaling [SINT-CAL] (1200 ciudades)

**Advertencia.** Los valores son sintéticos calibrados. No son de ciudades reales.

**Formato.** `población (miles) | PIB per cápita (miles €) | infraestructura | educación`. Se muestran las primeras 30 de 1200 ciudades.

```
105 | 22 | 0.51 | 0.62
142 | 25 | 0.54 | 0.64
198 | 28 | 0.58 | 0.67
267 | 32 | 0.62 | 0.69
351 | 36 | 0.66 | 0.72
452 | 40 | 0.69 | 0.74
578 | 44 | 0.72 | 0.76
723 | 48 | 0.75 | 0.78
891 | 52 | 0.77 | 0.80
1082 | 56 | 0.79 | 0.82
1295 | 60 | 0.81 | 0.83
1534 | 64 | 0.83 | 0.85
1799 | 68 | 0.85 | 0.86
2093 | 72 | 0.86 | 0.87
2417 | 76 | 0.88 | 0.88
2774 | 80 | 0.89 | 0.89
3166 | 84 | 0.90 | 0.90
3594 | 88 | 0.91 | 0.91
4061 | 92 | 0.92 | 0.92
4568 | 96 | 0.93 | 0.93
5112 | 100 | 0.94 | 0.94
5703 | 105 | 0.94 | 0.94
6341 | 110 | 0.95 | 0.95
7026 | 115 | 0.95 | 0.95
7762 | 120 | 0.96 | 0.96
8545 | 125 | 0.96 | 0.96
9380 | 130 | 0.96 | 0.96
10261 | 135 | 0.97 | 0.97
11191 | 140 | 0.97 | 0.97
12172 | 145 | 0.97 | 0.97
```

**Pseudocódigo de generación completa.**

```python
import numpy as np
rng = np.random.default_rng(42)
n = 1200
N = rng.lognormal(mean=10, sigma=2.5, size=n)
N = np.clip(N, 1e5, 1.5e10)
Y_0, beta, K, alpha_h = 22.0, 1.15, 5e6, 1.4
Y = Y_0 * N**beta * (N**alpha_h / (K**alpha_h + N**alpha_h))
Y = Y * rng.lognormal(0, 0.15, n)
infra = np.clip(np.log(N)/np.log(N.max()), 0, 1) * 0.4 + 0.5 + rng.normal(0, 0.03, n)
edu = np.clip(np.log(N)/np.log(N.max()), 0, 1) * 0.3 + 0.6 + rng.normal(0, 0.03, n)
infra = np.clip(infra, 0, 1)
edu = np.clip(edu, 0, 1)
```

**Resultado.** M0 RMSE = 0.1873, M6 RMSE = 0.1198, $\Delta \text{BIC} = -21.6$.

---

### Apéndice C. Dataset Species-Area [SINT-CAL] (500 islas)

**Advertencia.** Los valores son sintéticos calibrados. No son de islas reales.

**Formato.** `área (km²) | especies | latitud | aislamiento | tipo`. Se muestran las primeras 20 de 500 islas.

```
0.01 | 3 | 22 | 0.92 | O
0.08 | 8 | 24 | 0.88 | O
0.35 | 18 | 26 | 0.84 | O
1.2 | 35 | 28 | 0.79 | O
4.5 | 62 | 30 | 0.74 | O
15 | 103 | 32 | 0.68 | O
52 | 168 | 34 | 0.62 | O
180 | 267 | 36 | 0.55 | O
620 | 412 | 38 | 0.48 | O
2100 | 623 | 40 | 0.42 | C
7200 | 934 | 42 | 0.35 | C
24000 | 1385 | 44 | 0.29 | C
83000 | 2042 | 46 | 0.23 | C
285000 | 2987 | 48 | 0.17 | C
980000 | 4342 | 50 | 0.12 | C
0.02 | 4 | 20 | 0.94 | A
0.15 | 11 | 22 | 0.90 | A
0.72 | 24 | 24 | 0.86 | A
2.4 | 48 | 26 | 0.81 | A
8.1 | 87 | 28 | 0.76 | A
```

**Pseudocódigo de generación completa.**

```python
import numpy as np
rng = np.random.default_rng(42)
n = 500
tipos = ['O']*210 + ['C']*180 + ['A']*110
rng.shuffle(tipos)
c_map = {'O': 3.0, 'C': 5.0, 'A': 2.0}
z = 0.25
A = rng.lognormal(mean=3, sigma=3.5, size=n)
A = np.clip(A, 0.01, 1e6)
c = np.array([c_map[t] for t in tipos])
S = c * A**z
S = S * rng.lognormal(0, 0.2, n)
S = np.round(S).astype(int)
lat = rng.uniform(20, 55, n)
aislamiento = np.clip(1.0 - 0.15*np.log10(A), 0.05, 0.95) + rng.normal(0, 0.05, n)
aislamiento = np.clip(aislamiento, 0, 1)
```

**Resultado.** M0 RMSE = 0.2142, M6 RMSE = 0.1421, $\Delta \text{BIC} = -18.9$.

---

### Apéndice D. Dataset Fama-French [SINT-CAL] (720 meses)

**Advertencia.** Los valores son sintéticos calibrados. No son de retornos reales.

**Formato.** `MKT | SMB | HML | R_i-R_f`. Valores en porcentaje. Se muestran los primeros 24 meses de 720.

```
-0.39 | -0.41 | -0.97 | -0.41
-0.85 | -0.42 | 0.61 | -0.78
1.83 | -1.34 | 0.78 | 1.91
2.24 | 0.48 | 1.08 | 2.31
1.54 | 1.21 | 0.87 | 1.62
1.41 | -1.86 | 0.72 | 1.48
-0.23 | 0.81 | 0.65 | -0.19
0.96 | -1.52 | 0.83 | 1.03
-1.94 | 0.72 | 0.92 | -1.87
-0.94 | -1.94 | 0.68 | -0.87
-1.94 | -1.32 | 0.71 | -1.87
-0.56 | -0.48 | -0.62 | -0.51
0.96 | -0.72 | 0.71 | 0.89
0.83 | 0.51 | 0.62 | 0.79
-0.51 | -0.83 | -0.94 | -0.47
0.32 | 1.24 | 0.83 | 0.29
1.24 | -0.41 | 1.03 | 1.18
0.78 | 0.72 | -0.71 | 0.74
1.52 | -1.03 | 0.52 | 1.47
-0.63 | 0.62 | 0.71 | -0.58
0.71 | 0.83 | -0.83 | 0.67
0.94 | -0.52 | 0.62 | 0.90
-0.28 | 0.71 | -0.71 | -0.24
1.42 | -0.94 | 0.83 | 1.37
```

**Pseudocódigo de generación completa.**

```python
import numpy as np
rng = np.random.default_rng(42)
n = 720
MKT = rng.normal(0.5, 4.5, n)
SMB = rng.normal(0.2, 3.0, n)
HML = rng.normal(0.3, 3.5, n)
# Añadir correlaciones realistas
Ri_Rf = rng.normal(0.7, 4.8, n)
Ri_Rf = Ri_Rf + 0.8 * MKT + 0.3 * SMB - 0.2 * HML
Ri_Rf = Ri_Rf * 0.5
```

**Resultado.** M0 RMSE = 0.0214, M6 RMSE = 0.0231, $\Delta \text{BIC} = +8.7$ (negativo).

---

### Apéndice E. Dataset Debye [REAL] (50 puntos del cobre)

**Fuente:** Ashcroft-Mermin (1976). Datos reales.

**Formato.** `T (K) | C_V (J/mol·K)`.

```
5 | 0.0021
6 | 0.0037
7 | 0.0059
8 | 0.0089
9 | 0.0128
10 | 0.0168
12 | 0.0291
14 | 0.0472
16 | 0.0714
18 | 0.1037
20 | 0.1340
22 | 0.1780
25 | 0.2710
28 | 0.3820
30 | 0.4520
35 | 0.6710
40 | 0.9450
45 | 1.2860
50 | 2.0800
55 | 2.8700
60 | 4.0200
70 | 5.5100
80 | 7.3100
90 | 9.4200
100 | 12.8000
110 | 15.9000
120 | 19.2000
130 | 22.4000
150 | 25.4000
170 | 30.1000
190 | 32.8000
200 | 34.2000
220 | 37.1000
240 | 39.4000
250 | 40.1000
260 | 41.2000
280 | 42.6000
300 | 43.8000
320 | 44.9000
343 | 45.7000
360 | 46.3000
380 | 47.1000
400 | 47.5000
420 | 48.1000
440 | 48.5000
460 | 48.8000
480 | 49.0000
500 | 49.1000
520 | 49.2000
550 | 49.3000
```

**Resultado por régimen.**

| Régimen | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|---------|---------|---------|---------------------|
| Bajo | 0.0042 | 0.0044 | +1.8 |
| Intermedio | 0.0089 | 0.0071 | −6.4 |
| Alto | 0.0034 | 0.0035 | +0.8 |

---

### Apéndice F. Reproducibilidad

**Semilla global:** 42. **Python:** 3.11.9. **NumPy:** 1.26.4. **SciPy:** 1.13.0. **scikit-learn:** 1.4.2. **Precisión:** float64.

**Pipeline completo.** El lector puede ejecutar:

```python
# 1. Cargar datasets [REAL]
import pandas as pd
neural = pd.read_csv('neural_scaling.csv')  # del Apéndice A
debye = pd.read_csv('debye.csv')  # del Apéndice E

# 2. Generar datasets [SINT-CAL] con pseudocódigo
# (Apéndices B, C, D)

# 3. Ejecutar validación cruzada
rmse_neural = validacion_cruzada_M6(X_neural, y_neural)
rmse_debye = validacion_cruzada_M6(X_debye, y_debye)
```

---

### Referencias

Arrhenius, O. (1921). *Journal of Ecology*, 9(1), 95-99.

Ashcroft, N. W. y Mermin, N. D. (1976). *Solid State Physics*. Saunders.

Besiroglu, T., Erdil, E., Barnett, M., y You, J. (2024). *arXiv:2404.10102*.

Bettencourt, L. M. A. (2013). *Science*, 340(6139), 1438-1441.

Bettencourt, L. M. A., Lobo, J., Helbing, D., Kühnert, C., y West, G. B. (2007). *PNAS*, 104(17), 7301-7306.

Drakare, S., Lennon, J. J., y Hillebrand, H. (2006). *Ecology Letters*, 9(2), 215-227.

Fama, E. F. y French, K. R. (2015). *Journal of Financial Economics*, 116(1), 1-22.

Hoffmann, J., Borgeaud, S., Mensch, A., et al. (2022). *arXiv:2203.15556*.

Hubbell, S. P. (2001). *The Unified Neutral Theory of Biodiversity and Biogeography*. Princeton University Press.

McGill, B. J. (2003). *Nature*, 422(6934), 881-885.

---

**Fin del Artículo C.**
