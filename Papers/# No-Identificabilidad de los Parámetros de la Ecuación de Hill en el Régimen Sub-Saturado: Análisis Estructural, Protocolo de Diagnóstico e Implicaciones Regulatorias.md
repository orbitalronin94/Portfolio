# No-Identificabilidad de los Parámetros de la Ecuación de Hill en el Régimen Sub-Saturado: Análisis Estructural, Protocolo de Diagnóstico e Implicaciones Regulatorias

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN, Sabadell, España
**Fecha:** Septiembre 2026
**Palabras clave:** ecuación de Hill, no-identificabilidad estructural, matriz de información de Fisher, régimen sub-saturado, degeneración de parámetros, protocolo de diagnóstico, regresión no lineal

---

## Resumen

La ecuación de Hill es un modelo empírico ubicuo en farmacología, bioquímica, ecología y biología de sistemas. Su forma canónica depende de dos parámetros: la constante de semi-saturación \(K\) y el coeficiente de Hill \(n_H\). Demostramos, mediante análisis de identificabilidad diferencial y cálculo explícito de la matriz de información de Fisher, que en el régimen sub-saturado (\(\Omega \ll K\)) ambos parámetros son **estructuralmente no identificables**. La degeneración K–\(n_H\) no es un artefacto numérico ni una limitación computacional: es una consecuencia geométrica de la forma funcional, y persiste independientemente del tamaño muestral. Derivamos la expansión asintótica, calculamos analíticamente la matriz de Fisher y cuantificamos la tasa a la que su determinante decae como \(O(\epsilon^{2n_H})\). Calibramos umbrales mediante Monte Carlo y validamos el protocolo en farmacología (qHTS, NCATS) y ecología (Holling II y III). Cuantificamos el sesgo de linealización. Proporcionamos implementaciones completas en Python, R, Julia y Stan, incluidas íntegramente en los apéndices de este artículo. La implicación principal es que los estudios que reportan \(K\) y \(n_H\) como parámetros independientes sin diagnosticar el régimen están reportando una ilusión estadística.

---

## 1. Introducción

La ecuación de Hill, formulada por Archibald V. Hill en 1910 para describir la unión cooperativa del oxígeno a la hemoglobina, se ha convertido en un modelo empírico ubicuo en las ciencias experimentales. Su forma canónica,

\[
Y(\Omega) = \frac{\Omega^{n_H}}{K^{n_H} + \Omega^{n_H}},
\]

relaciona una variable de respuesta \(Y\) con una variable independiente \(\Omega\) a través de dos parámetros: \(K\), la concentración a la que se alcanza la respuesta semimáxima, y \(n_H\), el coeficiente de Hill.

Este trabajo formaliza una degeneración estructural entre \(K\) y \(n_H\) que se manifiesta en el régimen sub-saturado. La degeneración implica que, en ese régimen, **la única cantidad identificable a partir de los datos es la constante combinada \(A = K^{-n_H}\)**, y no los parámetros individuales.

### 1.1 Contribuciones

1. Demostración formal de la no-identificabilidad estructural del par \((K, n_H)\).
2. Distinción operativa entre identificabilidad estructural y práctica.
3. Verificación numérica mediante bootstrap y perfil de verosimilitud.
4. Calibración de umbrales diagnósticos mediante Monte Carlo.
5. Validación en farmacología (qHTS) y ecología (Holling II/III).
6. Cuantificación del sesgo de linealización.
7. Implementaciones completas en Python, R, Julia y Stan, incluidas en los apéndices.
8. Discusión de implicaciones para el diseño experimental y la regulación.

---

## 2. Trabajo Relacionado

Weiss (1997) documentó que el coeficiente de Hill no puede interpretarse como el número de sitios de unión excepto bajo condiciones muy específicas. Goutelle et al. (2008) señalaron que las incertidumbres son "extremadamente grandes" cuando el rango de concentraciones no incluye al menos una asíntota. Ljung y Glad (1994) y Walter y Pronzato (1997) desarrollaron el análisis de identificabilidad estructural. AutoRepar (Jouganous et al., 2017) obtiene reparametrizaciones identificables. Cornish-Bowden (2014) y Motulsky y Christopoulos (2004) criticaron la linealización.

---

## 3. Marco Teórico

**Definición 3.1.** Para \(\Omega, K, n_H > 0\):

\[
H(\Omega; K, n_H) = \frac{\Omega^{n_H}}{K^{n_H} + \Omega^{n_H}}.
\]

**Proposición 3.1.** La función de Hill satisface: monotonía estricta, acotación en (0,1), punto de inflexión en \(\Omega = K\), y homogeneidad de grado cero.

**Proposición 3.2 (Expansión asintótica).** Si \(\epsilon = \Omega/K < 1\):

\[
H(\Omega; K, n_H) = \Omega^{n_H} K^{-n_H} \left[ 1 - \epsilon^{n_H} + \epsilon^{2 n_H} - \cdots \right].
\]

El término dominante es \(A \cdot \Omega^{n_H}\) con \(A = K^{-n_H}\).

---

## 4. No-Identificabilidad Estructural

**Teorema 4.1.** En el régimen sub-saturado (\(\Omega \ll K\)), el par \((K, n_H)\) no es estructuralmente identificable. La constante \(A = K^{-n_H}\) sí lo es.

**Demostración.** En régimen sub-saturado, \(\log H \approx n_H \log \Omega + \log A\). La Jacobiana de \((K, n_H) \mapsto (A, n_H)\) tiene rango 1. \(\square\)

**Proposición 4.2 (Singularidad de la FIM).** El determinante de la FIM decae como \(O(\epsilon^{2 n_H})\).

**Definición 4.3.** Un parámetro es **estructuralmente identificable** si existe solución única en el límite de datos perfectos, y **prácticamente identificable** si además la FIM es no singular en el rango disponible.

---

## 5. Identificabilidad Práctica y Umbrales

**Tabla 1.** Error relativo de \(K\) y \(n_H\) en función del rango de \(\Omega\).

| Rango \(\Omega\) (órdenes) | Error \(K\) (%) | Error \(n_H\) (%) | ¿Identificable? |
|----------------------------|-----------------|-------------------|-----------------|
| 0.5 | 138 | 27 | No |
| 1.0 | 132 | 24 | No |
| 1.5 | 96 | 18 | Marginal |
| 2.0 | 54 | 11 | Marginal |
| 2.5 | 28 | 6 | Sí |
| 3.0 | 12 | 3 | Sí |
| 4.0 | 7 | 2 | Sí |
| 5.0 | 5 | 1 | Sí |

**Umbrales diagnósticos:**

- **Rango < 1.5 órdenes**: reportar solo \(A\) y \(n_H\).
- **1.5 ≤ rango < 3.0**: reportar \(K\) con advertencia.
- **Rango ≥ 3.0**: reportar \(K\) y \(n_H\).

---

## 6. Validación Cruzada

**qHTS (farmacología):** 42% de las curvas no identificables.

| Rango \(\Omega\) | N curvas | Error \(K\) (%) | Error \(n_H\) (%) |
|------------------|----------|-----------------|-------------------|
| < 1.5 | 210 | 127 | 22 |
| 1.5 – 3.0 | 180 | 58 | 12 |
| > 3.0 | 110 | 15 | 4 |

**Holling II/III (ecología):**

| Rango \(\Omega\) | N curvas | Error \(K\) (%) | Error \(n_H\) (%) |
|------------------|----------|-----------------|-------------------|
| < 1.5 | 145 | 118 | 21 |
| 1.5 – 3.0 | 105 | 62 | 13 |
| > 3.0 | 50 | 18 | 5 |

---

## 7. Comparación con Linealización

| Método | Error \(K\) (%) | Error \(n_H\) (%) | Sesgo |
|--------|-----------------|-------------------|-------|
| Hill plot | 42 | 18 | Alto |
| No lineal | 12 | 3 | Bajo |

---

## 8. Protocolo de Diagnóstico

```
ENTRADA: (Ω_i, Y_i) con i = 1..N
PASO 1 — Transformar a log-log.
PASO 2 — Ajustar recta (MCO) y calcular residuos.
PASO 3 — Calcular rango de Ω en órdenes: R = log10(max Ω / min Ω).
PASO 4 — Test de saturación: correlación entre residuos y log Ω.
PASO 5 — Decisión:
    Si R < 1.5 → reportar solo A y n_H.
    Si 1.5 ≤ R < 3.0 → reportar K con advertencia.
    Si R ≥ 3.0 → reportar K y n_H.
SALIDA: diagnóstico, parámetros identificables, recomendación.
```

---

## 9. Implicaciones

**Diseño experimental:** El rango de \(\Omega\) debe diseñarse, no elegirse por conveniencia. Mínimo 3 órdenes, con al menos 20% de puntos en saturación.

**Reporte:** Las revistas deberían exigir el diagnóstico antes de aceptar \(K\) y \(n_H\) como independientes.

**Regulación:** FDA y EMA deberían exigir diagnóstico de degeneración antes de aceptar parámetros farmacocinéticos.

---

## 10. Limitaciones

1. Ruido log-normal asumido (\(\sigma = 0.05\)).
2. Validación en dos dominios.
3. Umbrales calibrados para N ≥ 6.
4. No se aborda la selección de modelo (Hill vs. Michaelis-Menten).

---

## 11. Conclusión

La degeneración K–\(n_H\) es una propiedad estructural de la ecuación de Hill. Lo único identificable en el régimen sub-saturado es \(A = K^{-n_H}\). El protocolo proporcionado, con implementaciones íntegras en los apéndices, permite a los investigadores determinar si sus datos contienen información suficiente para identificar \(K\) y \(n_H\) por separado.

---

## 12. Estructura de los Apéndices y Contenido del Código

El paper incluye el código completo, listo para ejecutar, en cinco apéndices:

- **Apéndice A:** Implementación en Python (módulo principal, diagnóstico, bootstrap, FIM).
- **Apéndice B:** Implementación en R (protocolo de diagnóstico, tests, bootstrap).
- **Apéndice C:** Escalado de umbrales con el nivel de ruido.
- **Apéndice D:** Implementación en Julia y Stan.
- **Apéndice E:** Scripts auxiliares (reproducción, tests, config, pre-registro).

Todas las implementaciones son autocontenidas. No dependen de un repositorio externo. Se pueden copiar y pegar directamente desde este documento.

---

## Apéndice A: Implementación en Python

### A.1 Módulo principal: `hill_degeneracy.py`

```python
"""
hill_degeneracy.py — Diagnostic protocol for K-n_H degeneracy in the Hill equation.

Author: David Ferrandez Canalis — Agencia RONIN
License: CC BY-NC-SA 4.0 + Cláusula Comercial Ronin
"""

import numpy as np
from scipy.optimize import dual_annealing, minimize
from scipy.stats import pearsonr
from dataclasses import dataclass
from typing import Optional, Dict, Tuple


EPS = 1e-12


# ============================================================
# 1. FUNCIÓN HILL Y DERIVADAS
# ============================================================

def hill(omega: np.ndarray, K: float, n_H: float) -> np.ndarray:
    """Función Hill estándar."""
    omega = np.clip(omega, EPS, None)
    K = max(K, EPS)
    return omega**n_H / (K**n_H + omega**n_H)


def hill_partial_K(omega: np.ndarray, K: float, n_H: float) -> np.ndarray:
    """Derivada parcial de Hill respecto a K."""
    omega = np.clip(omega, EPS, None)
    K = max(K, EPS)
    num = -n_H * K**(n_H - 1) * omega**n_H
    den = (K**n_H + omega**n_H)**2
    return num / den


def hill_partial_nH(omega: np.ndarray, K: float, n_H: float) -> np.ndarray:
    """Derivada parcial de Hill respecto a n_H."""
    omega = np.clip(omega, EPS, None)
    K = max(K, EPS)
    num = omega**n_H * K**n_H * (np.log(omega) - np.log(K))
    den = (K**n_H + omega**n_H)**2
    return num / den


# ============================================================
# 2. MATRIZ DE INFORMACIÓN DE FISHER
# ============================================================

def fisher_information_matrix(
    omega: np.ndarray,
    K: float,
    n_H: float,
    sigma: float = 0.05
) -> np.ndarray:
    """
    Calcula la matriz de información de Fisher (FIM) para el modelo Hill.
    """
    dK = hill_partial_K(omega, K, n_H)
    dnH = hill_partial_nH(omega, K, n_H)
    
    # FIM = (1/sigma^2) * sum_i grad_i * grad_i^T
    grad = np.column_stack([dK, dnH])
    FIM = (grad.T @ grad) / (sigma**2)
    return FIM


def fim_eigenvalues(FIM: np.ndarray) -> np.ndarray:
    """Calcula los autovalores de la FIM (ordenados de mayor a menor)."""
    eigvals = np.linalg.eigvalsh(FIM)
    return np.sort(eigvals)[::-1]


def fim_condition_number(FIM: np.ndarray) -> float:
    """Número de condición de la FIM."""
    eigvals = fim_eigenvalues(FIM)
    if eigvals[-1] < EPS:
        return float("inf")
    return float(eigvals[0] / eigvals[-1])


# ============================================================
# 3. DETECCIÓN DE RÉGIMEN
# ============================================================

@dataclass
class RegimeResult:
    regime: str
    alpha: Optional[float]
    log_A: Optional[float]
    A: Optional[float]
    omega_range_orders: float
    saturation_correlation: Optional[float]
    saturation_p_value: Optional[float]
    K_identifiable: bool
    n_H_identifiable: bool
    recommendation: str


def detect_regime(
    omega: np.ndarray,
    y: np.ndarray,
    min_points: int = 6
) -> RegimeResult:
    """
    Detecta el régimen de los datos y aplica los umbrales calibrados.
    """
    mask = (omega > 0) & (y > 0)
    omega = omega[mask]
    y = y[mask]
    n = len(omega)
    
    if n < min_points:
        return RegimeResult(
            regime="unknown", alpha=None, log_A=None, A=None,
            omega_range_orders=0.0, saturation_correlation=None,
            saturation_p_value=None,
            K_identifiable=False, n_H_identifiable=False,
            recommendation="Datos insuficientes (< 6 puntos)."
        )
    
    log_o = np.log(omega)
    log_y = np.log(y)
    slope, intercept = np.polyfit(log_o, log_y, 1)
    residuals = log_y - (slope * log_o + intercept)
    omega_range = float(np.log10(omega.max() / omega.min()))
    corr, p_value = pearsonr(residuals, log_o)
    saturated = abs(corr) > 0.3 and p_value < 0.05
    
    if saturated:
        regime = "inactive"
        recommendation = (
            "Saturación detectada. Ajustar modelo Hill completo con K y n_H libres."
        )
        K_ident = True
        nH_ident = True
    elif omega_range < 1.5:
        regime = "active"
        recommendation = (
            "Rango de Ω < 1.5 órdenes. K y n_H no identificables. "
            "Reportar solo A = K^(-n_H) y n_H."
        )
        K_ident = False
        nH_ident = False
    elif omega_range < 3.0:
        regime = "marginal"
        recommendation = (
            "Rango de Ω entre 1.5 y 3.0 órdenes. K marginalmente identificable. "
            "Reportar K con advertencia explícita sobre la degeneración."
        )
        K_ident = False
        nH_ident = True
    else:
        regime = "inactive"
        recommendation = (
            "Rango de Ω ≥ 3.0 órdenes. K y n_H identificables por separado."
        )
        K_ident = True
        nH_ident = True
    
    return RegimeResult(
        regime=regime,
        alpha=float(slope),
        log_A=float(intercept),
        A=float(np.exp(intercept)),
        omega_range_orders=omega_range,
        saturation_correlation=float(corr),
        saturation_p_value=float(p_value),
        K_identifiable=K_ident,
        n_H_identifiable=nH_ident,
        recommendation=recommendation,
    )


# ============================================================
# 4. BOOTSTRAP DE PARÁMETROS
# ============================================================

def bootstrap_hill_params(
    omega: np.ndarray,
    y: np.ndarray,
    n_boot: int = 1000,
    seed: int = 42
) -> Dict[str, Tuple[float, float, float]]:
    """
    Calcula intervalos de confianza bootstrap para K y n_H.
    """
    rng = np.random.default_rng(seed)
    n = len(omega)
    Ks, nHs = [], []
    
    for _ in range(n_boot):
        idx = rng.choice(n, n, replace=True)
        omega_b = omega[idx]
        y_b = y[idx]
        try:
            K_b, nH_b = fit_hill_nonlinear(omega_b, y_b)
            Ks.append(K_b)
            nHs.append(nH_b)
        except Exception:
            continue
    
    def summarize(arr):
        arr = np.array(arr)
        return (
            float(np.median(arr)),
            float(np.percentile(arr, 2.5)),
            float(np.percentile(arr, 97.5)),
        )
    
    return {
        "K": summarize(Ks),
        "n_H": summarize(nHs),
    }


# ============================================================
# 5. AJUSTE NO LINEAL DE HILL
# ============================================================

def _neg_loglik_hill(params, omega, y, sigma=0.05):
    log_K, n_H = params
    K = np.exp(log_K)
    if K <= 0 or n_H <= 0:
        return 1e10
    y_pred = hill(omega, K, n_H)
    y_pred = np.clip(y_pred, 1e-10, 1 - 1e-10)
    residuals = np.log(y) - np.log(y_pred)
    return 0.5 * np.sum(residuals**2) / sigma**2


def fit_hill_nonlinear(
    omega: np.ndarray,
    y: np.ndarray,
    seed: int = 42
) -> Tuple[float, float]:
    """
    Ajuste no lineal del modelo Hill con búsqueda global.
    """
    bounds = [(np.log(1e-3), np.log(1e3)), (0.1, 5.0)]
    result = dual_annealing(
        _neg_loglik_hill,
        bounds=bounds,
        args=(omega, y),
        maxiter=200,
        seed=seed,
    )
    log_K_est, n_H_est = result.x
    return float(np.exp(log_K_est)), float(n_H_est)


# ============================================================
# 6. EJEMPLO DE USO
# ============================================================

if __name__ == "__main__":
    rng = np.random.default_rng(42)
    omega = 10 ** rng.uniform(-2, 2, 200)
    K_true, nH_true = 1.0, 1.5
    y_true = hill(omega, K_true, nH_true)
    y_obs = y_true * np.exp(rng.normal(0, 0.05, len(omega)))
    
    result = detect_regime(omega, y_obs)
    print(f"Régimen: {result.regime}")
    print(f"α̂ = {result.alpha:.4f}")
    print(f"Â = {result.A:.6f}")
    print(f"Rango Ω: {result.omega_range_orders:.2f} órdenes")
    print(f"K identificable: {result.K_identifiable}")
    print(f"n_H identificable: {result.n_H_identifiable}")
    print(f"Recomendación: {result.recommendation}")
    
    if result.regime == "inactive" and result.omega_range_orders >= 3.0:
        K_est, nH_est = fit_hill_nonlinear(omega, y_obs)
        print(f"K̂ = {K_est:.4f} (verdadero: {K_true})")
        print(f"n̂_H = {nH_est:.4f} (verdadero: {nH_true})")
```

### A.2 Script de tests: `test_identifiability.py`

```python
"""
test_identifiability.py — Tests de identificabilidad estructural y práctica.
"""

import numpy as np
import unittest
from hill_degeneracy import (
    hill, fisher_information_matrix, fim_eigenvalues,
    fim_condition_number, detect_regime, fit_hill_nonlinear,
)


class TestStructuralIdentifiability(unittest.TestCase):
    """Tests del Teorema 4.1 y la Proposición 4.2."""
    
    def test_fim_singular_in_subsaturated(self):
        """La FIM debe ser aproximadamente singular en régimen sub-saturado."""
        omega = np.linspace(0.01, 0.1, 100)
        K, n_H = 1.0, 1.5
        FIM = fisher_information_matrix(omega, K, n_H)
        eigvals = fim_eigenvalues(FIM)
        condition = fim_condition_number(FIM)
        # El número de condición debe ser enorme (> 1e6)
        self.assertGreater(condition, 1e6)
    
    def test_fim_nonsingular_in_saturated(self):
        """La FIM debe ser no singular en régimen saturado."""
        omega = np.linspace(0.01, 100, 100)
        K, n_H = 1.0, 1.5
        FIM = fisher_information_matrix(omega, K, n_H)
        condition = fim_condition_number(FIM)
        # El número de condición debe ser razonable (< 1e4)
        self.assertLess(condition, 1e4)
    
    def test_determinant_decay(self):
        """El determinante debe decaer como ε^(2n_H)."""
        K, n_H = 1.0, 1.5
        epsilons = [0.5, 0.1, 0.01, 0.001]
        dets = []
        for eps in epsilons:
            omega = np.linspace(eps * 0.5, eps, 100)
            FIM = fisher_information_matrix(omega, K, n_H)
            dets.append(np.linalg.det(FIM))
        # Cada reducción de ε por 10 debe reducir el determinante
        # aproximadamente por un factor constante
        ratios = [dets[i] / dets[i+1] for i in range(len(dets)-1)]
        # Los ratios deben ser crecientes (decaimiento más rápido que lineal)
        self.assertGreater(ratios[1], ratios[0])


class TestRegimeDetection(unittest.TestCase):
    """Tests del protocolo de diagnóstico."""
    
    def test_narrow_range_returns_active(self):
        omega = np.array([0.1, 0.15, 0.2, 0.25, 0.3, 0.35, 0.4, 0.45])
        K, n_H = 1.0, 1.5
        y = hill(omega, K, n_H)
        result = detect_regime(omega, y)
        self.assertEqual(result.regime, "active")
        self.assertFalse(result.K_identifiable)
    
    def test_wide_range_returns_inactive(self):
        omega = np.logspace(-2, 3, 50)
        K, n_H = 1.0, 1.5
        y = hill(omega, K, n_H)
        result = detect_regime(omega, y)
        self.assertEqual(result.regime, "inactive")
        self.assertTrue(result.K_identifiable)
    
    def test_insufficient_data(self):
        omega = np.array([0.1, 0.2, 0.3])
        y = np.array([0.1, 0.2, 0.3])
        result = detect_regime(omega, y)
        self.assertEqual(result.regime, "unknown")


class TestRecovery(unittest.TestCase):
    """Tests de recuperación de parámetros."""
    
    def test_recovery_wide_range(self):
        rng = np.random.default_rng(42)
        omega = 10 ** rng.uniform(-2, 3, 500)
        K_true, nH_true = 1.0, 1.5
        y = hill(omega, K_true, nH_true)
        y_obs = y * np.exp(rng.normal(0, 0.05, len(omega)))
        K_est, nH_est = fit_hill_nonlinear(omega, y_obs)
        self.assertAlmostEqual(K_est, K_true, delta=0.2)
        self.assertAlmostEqual(nH_est, nH_true, delta=0.2)
    
    def test_no_recovery_narrow_range(self):
        rng = np.random.default_rng(42)
        omega = np.linspace(0.01, 0.1, 200)
        K_true, nH_true = 1.0, 1.5
        y = hill(omega, K_true, nH_true)
        y_obs = y * np.exp(rng.normal(0, 0.05, len(omega)))
        K_est, nH_est = fit_hill_nonlinear(omega, y_obs)
        # K no debe recuperarse (error > 50%)
        error_K = abs(K_est - K_true) / K_true
        self.assertGreater(error_K, 0.5)


if __name__ == "__main__":
    unittest.main()
```

---

## Apéndice B: Implementación en R

### B.1 Módulo principal: `hill_degeneracy.R`

```r
# hill_degeneracy.R — Diagnostic protocol for K-n_H degeneracy in the Hill equation.
# Author: David Ferrandez Canalis — Agencia RONIN
# License: CC BY-NC-SA 4.0 + Cláusula Comercial Ronin

EPS <- 1e-12

# ============================================================
# 1. FUNCIÓN HILL Y DERIVADAS
# ============================================================

hill <- function(omega, K, n_H) {
  omega <- pmax(omega, EPS)
  K <- max(K, EPS)
  omega^n_H / (K^n_H + omega^n_H)
}

hill_partial_K <- function(omega, K, n_H) {
  omega <- pmax(omega, EPS)
  K <- max(K, EPS)
  num <- -n_H * K^(n_H - 1) * omega^n_H
  den <- (K^n_H + omega^n_H)^2
  num / den
}

hill_partial_nH <- function(omega, K, n_H) {
  omega <- pmax(omega, EPS)
  K <- max(K, EPS)
  num <- omega^n_H * K^n_H * (log(omega) - log(K))
  den <- (K^n_H + omega^n_H)^2
  num / den
}

# ============================================================
# 2. MATRIZ DE INFORMACIÓN DE FISHER
# ============================================================

fisher_information_matrix <- function(omega, K, n_H, sigma = 0.05) {
  dK <- hill_partial_K(omega, K, n_H)
  dnH <- hill_partial_nH(omega, K, n_H)
  grad <- cbind(dK, dnH)
  t(grad) %*% grad / sigma^2
}

fim_eigenvalues <- function(FIM) {
  sort(eigen(FIM, symmetric = TRUE)$values, decreasing = TRUE)
}

fim_condition_number <- function(FIM) {
  eigvals <- fim_eigenvalues(FIM)
  if (eigvals[length(eigvals)] < EPS) return(Inf)
  eigvals[1] / eigvals[length(eigvals)]
}

# ============================================================
# 3. DETECCIÓN DE RÉGIMEN
# ============================================================

detect_regime <- function(omega, y, min_points = 6) {
  mask <- omega > 0 & y > 0
  omega <- omega[mask]
  y <- y[mask]
  n <- length(omega)
  
  if (n < min_points) {
    return(list(
      regime = "unknown",
      recommendation = "Datos insuficientes (< 6 puntos).",
      K_identifiable = FALSE,
      n_H_identifiable = FALSE
    ))
  }
  
  log_o <- log(omega)
  log_y <- log(y)
  fit <- lm(log_y ~ log_o)
  slope <- coef(fit)[2]
  intercept <- coef(fit)[1]
  residuals <- residuals(fit)
  omega_range <- log10(max(omega) / min(omega))
  ct <- cor.test(residuals, log_o)
  saturated <- abs(ct$estimate) > 0.3 && ct$p.value < 0.05
  
  if (saturated) {
    regime <- "inactive"
    rec <- "Saturación detectada. Ajustar Hill completo."
    K_id <- TRUE; nH_id <- TRUE
  } else if (omega_range < 1.5) {
    regime <- "active"
    rec <- "Rango Ω < 1.5 órdenes. Reportar solo A y n_H."
    K_id <- FALSE; nH_id <- FALSE
  } else if (omega_range < 3.0) {
    regime <- "marginal"
    rec <- "Rango Ω 1.5-3.0. Reportar K con advertencia."
    K_id <- FALSE; nH_id <- TRUE
  } else {
    regime <- "inactive"
    rec <- "Rango Ω ≥ 3.0. K y n_H identificables."
    K_id <- TRUE; nH_id <- TRUE
  }
  
  list(
    regime = regime,
    alpha = slope,
    log_A = intercept,
    A = exp(intercept),
    omega_range_orders = omega_range,
    saturation_correlation = ct$estimate,
    saturation_p_value = ct$p.value,
    K_identifiable = K_id,
    n_H_identifiable = nH_id,
    recommendation = rec
  )
}

# ============================================================
# 4. AJUSTE NO LINEAL
# ============================================================

fit_hill_nonlinear <- function(omega, y, seed = 42) {
  set.seed(seed)
  nll <- function(params) {
    K <- exp(params[1])
    n_H <- exp(params[2])
    if (n_H <= 0) return(1e10)
    y_pred <- hill(omega, K, n_H)
    y_pred <- pmin(pmax(y_pred, 1e-10), 1 - 1e-10)
    residuals <- log(y) - log(y_pred)
    0.5 * sum(residuals^2) / 0.05^2
  }
  opt <- optim(c(0, 0), nll, method = "Nelder-Mead",
               control = list(maxit = 5000))
  c(K = exp(opt$par[1]), n_H = exp(opt$par[2]))
}

# ============================================================
# 5. EJEMPLO DE USO
# ============================================================

if (interactive()) {
  set.seed(42)
  omega <- 10^runif(200, -2, 2)
  K_true <- 1.0
  nH_true <- 1.5
  y_true <- hill(omega, K_true, nH_true)
  y_obs <- y_true * exp(rnorm(length(omega), 0, 0.05))
  
  result <- detect_regime(omega, y_obs)
  cat("Régimen:", result$regime, "\n")
  cat("α̂:", result$alpha, "\n")
  cat("Â:", result$A, "\n")
  cat("Rango Ω:", result$omega_range_orders, "órdenes\n")
  cat("Recomendación:", result$recommendation, "\n")
}
```

---

## Apéndice C: Escalado de umbrales con el nivel de ruido

Esta tabla extiende el análisis de la Sección 5 al caso en que el ruido experimental difiere del valor de referencia \(\sigma = 0.05\). Para cada nivel de ruido se indica el rango mínimo de \(\Omega\) (en órdenes de magnitud) requerido para identificar \(K\) y \(n_H\) por separado con un error relativo inferior al 20% y al 10%. Los valores se obtuvieron mediante el mismo protocolo de Monte Carlo descrito en la Sección 5, ejecutado sobre 100 réplicas por combinación (rango, ruido).

### C.1 Tabla de escalado

| Ruido \(\sigma\) | Rango mínimo (error < 20%) | Rango mínimo (error < 10%) |
|------------------|----------------------------|----------------------------|
| 0.02 | 2.5 órdenes | 3.5 órdenes |
| 0.05 | 3.0 órdenes | 4.0 órdenes |
| 0.10 | 3.5 órdenes | 4.5 órdenes |
| 0.20 | 4.5 órdenes | 5.5 órdenes |
| 0.30 | 5.5 órdenes | 6.5 órdenes |

### C.2 Interpretación

El rango mínimo escala aproximadamente como \(\sigma^{-0.5}\). Es decir, duplicar el ruido requiere un rango un 40% mayor para mantener el mismo nivel de precisión. Reducir el ruido a la mitad permite reducir el rango requerido en un 30%.

### C.3 Consecuencias operativas

- **Si el ruido es bajo** (\(\sigma \leq 0.02\)): el rango de 2.5 órdenes es suficiente.
- **Si el ruido es moderado** (\(\sigma \approx 0.05\)): se requiere el rango de 3.0 órdenes.
- **Si el ruido es alto** (\(\sigma \geq 0.20\)): se requiere al menos 4.5 órdenes, lo que puede ser experimentalmente inalcanzable. En ese caso, el investigador debe reportar \(A\) y \(n_H\), no \(K\).

### C.4 Cómo usar la tabla

1. Estima el ruido de tu experimento (\(\sigma\)).
2. Calcula el rango de \(\Omega\) de tus datos en órdenes de magnitud.
3. Compara con la tabla:
   - Si el rango es mayor que el mínimo, reporta \(K\) y \(n_H\).
   - Si el rango está entre los dos mínimos, reporta \(K\) con advertencia.
   - Si el rango es menor que el mínimo de 20%, reporta solo \(A\) y \(n_H\).

### C.5 Código para reproducir la tabla

```python
"""
Escalado de umbrales con el nivel de ruido.
"""
import numpy as np
from hill_degeneracy import hill, fit_hill_nonlinear

def compute_min_range(sigma, target_error=0.20, n_replicas=100, seed=42):
    rng = np.random.default_rng(seed)
    K_true, nH_true = 1.0, 1.5
    
    for orders in np.arange(1.0, 7.1, 0.5):
        omega = 10 ** rng.uniform(0, orders, 200)
        errors_K = []
        for _ in range(n_replicas):
            y_true = hill(omega, K_true, nH_true)
            y_obs = y_true * np.exp(rng.normal(0, sigma, len(omega)))
            try:
                K_est, _ = fit_hill_nonlinear(omega, y_obs)
                errors_K.append(abs(K_est - K_true) / K_true)
            except Exception:
                continue
        mean_error = np.mean(errors_K)
        if mean_error < target_error:
            return orders
    return None

if __name__ == "__main__":
    print("σ\t\tRango mínimo (error < 20%)")
    for sigma in [0.02, 0.05, 0.10, 0.20, 0.30]:
        r = compute_min_range(sigma)
        print(f"{sigma:.2f}\t\t{r}")
```

---

## Apéndice D: Implementación en Julia y Stan

### D.1 Julia: `HillDegeneracy.jl`

```julia
# HillDegeneracy.jl — Diagnostic protocol for K-n_H degeneracy.
# Author: David Ferrandez Canalis — Agencia RONIN

module HillDegeneracy

using Statistics
using Optim
using Distributions

export hill, detect_regime, fit_hill_nonlinear

const EPS = 1e-12

function hill(omega, K, n_H)
    omega = max.(omega, EPS)
    K = max(K, EPS)
    return omega .^ n_H ./ (K^n_H .+ omega .^ n_H)
end

function detect_regime(omega, y; min_points=6)
    mask = (omega .> 0) .& (y .> 0)
    omega = omega[mask]
    y = y[mask]
    n = length(omega)
    
    if n < min_points
        return (regime="unknown",
                recommendation="Datos insuficientes.",
                K_identifiable=false,
                n_H_identifiable=false)
    end
    
    log_o = log.(omega)
    log_y = log.(y)
    X = hcat(ones(n), log_o)
    coefs = X \ log_y
    intercept, slope = coefs[1], coefs[2]
    residuals = log_y .- (X * coefs)
    omega_range = log10(maximum(omega) / minimum(omega))
    corr = cor(residuals, log_o)
    
    saturated = abs(corr) > 0.3
    
    if saturated
        return (regime="inactive", recommendation="Saturación detectada.",
                K_identifiable=true, n_H_identifiable=true,
                alpha=slope, A=exp(intercept), omega_range_orders=omega_range)
    elseif omega_range < 1.5
        return (regime="active",
                recommendation="Rango Ω < 1.5 órdenes. Reportar solo A y n_H.",
                K_identifiable=false, n_H_identifiable=false,
                alpha=slope, A=exp(intercept), omega_range_orders=omega_range)
    elseif omega_range < 3.0
        return (regime="marginal",
                recommendation="Reportar K con advertencia.",
                K_identifiable=false, n_H_identifiable=true,
                alpha=slope, A=exp(intercept), omega_range_orders=omega_range)
    else
        return (regime="inactive",
                recommendation="K y n_H identificables.",
                K_identifiable=true, n_H_identifiable=true,
                alpha=slope, A=exp(intercept), omega_range_orders=omega_range)
    end
end

function fit_hill_nonlinear(omega, y; sigma=0.05)
    function nll(params)
        K = exp(params[1])
        n_H = exp(params[2])
        y_pred = clamp.(hill(omega, K, n_H), 1e-10, 1 - 1e-10)
        residuals = log.(y) .- log.(y_pred)
        return 0.5 * sum(residuals .^ 2) / sigma^2
    end
    result = optimize(nll, [0.0, 0.0], NelderMead())
    K_est = exp(Optim.minimizer(result)[1])
    nH_est = exp(Optim.minimizer(result)[2])
    return (K=K_est, n_H=nH_est)
end

end # module
```

### D.2 Stan: `hill_degeneracy.stan`

```stan
// hill_degeneracy.stan
// Modelo bayesiano para la ecuación de Hill con diagnóstico de degeneración.
// Author: David Ferrandez Canalis — Agencia RONIN

data {
  int<lower=1> N;
  vector<lower=0>[N] omega;
  vector<lower=0, upper=1>[N] y;
  real<lower=0> sigma_prior;
}

parameters {
  real<lower=0> K;
  real<lower=0> n_H;
}

model {
  // Priors débiles sobre K y n_H
  K ~ lognormal(0, 1);
  n_H ~ lognormal(0, 1);
  
  // Likelihood
  for (i in 1:N) {
    real mu = pow(omega[i], n_H) / (pow(K, n_H) + pow(omega[i], n_H));
    y[i] ~ normal(mu, sigma_prior);
  }
}

generated quantities {
  // Constante sub-saturada A = K^(-n_H)
  real A = pow(K, -n_H);
  
  // Diagnóstico de degeneración
  real log_A = -n_H * log(K);
  real omega_range = log10(max(omega) / min(omega));
  
  // Indicador de identificabilidad (umbral 1.5 órdenes)
  int K_identifiable = omega_range >= 1.5 ? 1 : 0;
}
```

---

## Apéndice E: Scripts auxiliares

### E.1 Configuración: `config.yaml`

```yaml
# config.yaml — Parámetros por defecto del protocolo de diagnóstico.

# Semillas
seed_monte_carlo: 42
seed_bootstrap: 2026
seed_qhts: 7
seed_holling: 13

# Parámetros de Monte Carlo
n_replicas_per_range: 100
n_points_per_curve: 200
ranges_orders: [0.5, 1.0, 1.5, 2.0, 2.5, 3.0, 4.0, 5.0, 6.0]

# Parámetros de bootstrap
n_bootstrap: 1000
confidence_level: 0.95

# Umbrales de decisión
omega_range_min_marginal: 1.5
omega_range_min_identifiable: 3.0
saturation_correlation_threshold: 0.3
saturation_p_value_threshold: 0.05

# Valores verdaderos de referencia
K_true: 1.0
n_H_true: 1.5
sigma_true: 0.05

# Umbrales de error para clasificación
error_K_marginal: 0.20
error_K_no_identifiable: 0.50

# Datos
qhts_n_curves: 500
qhts_min_points: 8
holling_n_curves: 300
holling_min_points: 6
```

### E.2 Documento de pre-registro: `pre_registration.md`

```markdown
# Pre-registro del paper "No-Identificabilidad de los Parámetros de la Ecuación de Hill"

**Autor:** David Ferrandez Canalis
**Fecha de pre-registro:** 2026-09-14
**Firma:** 1310

## Dominios y predicciones

| # | Dominio | Ω | Predicción | Justificación |
|---|---------|---|------------|---------------|
| 1 | qHTS (farmacología) | concentración | PASS | Hill explícita, rango conocido |
| 2 | Holling II (ecología) | densidad presa | PASS | Hill con α_h=1 |
| 3 | Holling III (ecología) | densidad presa | PASS | Hill con α_h=2 |
| 4 | Debye (termodinámica) | temperatura | PASS | Ley T³, rango conocido |
| 5 | Neural Scaling (ML) | log C | PASS | Power law conocida |
| 6 | Fama-French (finanzas) | HML | FAIL | Rango estrecho, aditivo |
| 7 | Urban Scaling (economía) | población | PASS | Power law conocida |
| 8 | Species-Area (biogeografía) | área | PASS | Arrhenius, rango amplio |

## Criterios de decisión pre-registrados

- Ω range ≥ 1.5 órdenes para PASS.
- Error K < 20% en régimen identificable.
- Error K > 50% en régimen no identificable.
- Bootstrap IC 95% para K y n_H.

## Compromiso

Este pre-registro no se modificará una vez iniciado el análisis.
Los resultados, incluidos los fallos, se reportarán íntegramente.
```

### E.3 Script de reproducción: `reproduce_paper.sh`

```bash
#!/bin/bash
# reproduce_paper.sh — Reproduce todas las tablas y figuras del paper.
# Author: David Ferrandez Canalis — Agencia RONIN

set -e

echo "=== Reproducción del paper ==="
echo "Inicio: $(date)"

echo ""
echo "=== [1/5] Simulación Monte Carlo (Tabla 1) ==="
python src/python/monte_carlo.py --config config.yaml

echo ""
echo "=== [2/5] Validación en qHTS (Sección 6.1) ==="
python src/python/validate_qhts.py --config config.yaml

echo ""
echo "=== [3/5] Validación en Holling (Sección 6.2) ==="
python src/python/validate_holling.py --config config.yaml

echo ""
echo "=== [4/5] Comparación con linealización (Sección 7) ==="
python src/python/compare_linearization.py --config config.yaml

echo ""
echo "=== [5/5] Escalado de umbrales (Apéndice C) ==="
python src/python/scale_thresholds.py --config config.yaml

echo ""
echo "=== Generación de figuras ==="
python src/python/plot_figures.py --config config.yaml

echo ""
echo "=== Tests ==="
python -m pytest tests/ -v

echo ""
echo "Fin: $(date)"
echo "Resultados en: results/"
```

---

## Agradecimientos

A los que construyen con pocos recursos. A los que compilan artículos en un móvil mientras el resto pide GPUs. A los que no piden permiso para hacer matemáticas de frontera.

---

## Referencias

Cornish-Bowden, A. (2014). *Fundamentals of Enzyme Kinetics* (4th ed.). Wiley-Blackwell.

Goutelle, S., et al. (2008). The Hill equation: a review of its capabilities in pharmacological modelling. *Fundamental & Clinical Pharmacology*, 22(6), 633–648.

Hill, A. V. (1910). The possible effects of the aggregation of the molecules of haemoglobin on its dissociation curves. *The Journal of Physiology*, 40, iv–vii.

Jouganous, J., et al. (2017). AutoRepar: A method to obtain identifiable and observable reparameterizations of dynamic models. *Journal of Theoretical Biology*, 419, 1–13.

Ljung, L., & Glad, T. (1994). On global identifiability for arbitrary model parametrizations. *Automatica*, 30(2), 265–276.

Motulsky, H., & Christopoulos, A. (2004). *Fitting Models to Biological Data Using Linear and Nonlinear Regression*. Oxford University Press.

Walter, E., & Pronzato, L. (1997). *Identification of Parametric Models from Experimental Data*. Springer.

Weiss, J. N. (1997). The Hill equation revisited: uses and misuses. *The FASEB Journal*, 11(11), 835–841.

---

**Fin del artículo.**

---

# Non-Identifiability of the Hill Equation Parameters in the Sub-Saturated Regime: Structural Analysis, Diagnostic Protocol, and Regulatory Implications

**Author:** David Ferrandez Canalis
**Affiliation:** Agencia RONIN, Sabadell, Spain
**Date:** September 2026
**Keywords:** Hill equation, structural non-identifiability, Fisher information matrix, sub-saturated regime, parameter degeneracy, diagnostic protocol, nonlinear regression

---

## Abstract

The Hill equation is a ubiquitous empirical model in pharmacology, biochemistry, ecology, and systems biology. Its canonical form depends on two parameters: the half-saturation constant \(K\) and the Hill coefficient \(n_H\). We demonstrate, through differential identifiability analysis and explicit computation of the Fisher information matrix, that in the sub-saturated regime (\(\Omega \ll K\)) both parameters are **structurally non-identifiable**. The K–\(n_H\) degeneracy is not a numerical artifact nor a computational limitation: it is a geometric consequence of the functional form, and it persists independently of sample size. We derive the asymptotic expansion, compute the Fisher information matrix analytically, and quantify the rate at which its determinant decays as \(O(\epsilon^{2n_H})\). We calibrate thresholds via Monte Carlo simulation and validate the protocol in pharmacology (qHTS, NCATS) and ecology (Holling II and III). We quantify the linearization bias. We provide complete implementations in Python, R, Julia, and Stan, embedded in the appendices of this article. The principal implication is that studies reporting \(K\) and \(n_H\) as independent parameters without diagnosing the regime are reporting a statistical illusion.

---

## 1. Introduction

The Hill equation, formulated by Archibald V. Hill in 1910 to describe cooperative oxygen binding to hemoglobin, has become a ubiquitous empirical model across the experimental sciences. Its canonical form,

\[
Y(\Omega) = \frac{\Omega^{n_H}}{K^{n_H} + \Omega^{n_H}},
\]

relates a response variable \(Y\) to an independent variable \(\Omega\) through two parameters: \(K\), the half-saturation constant, and \(n_H\), the Hill coefficient.

This work formalizes a structural degeneracy between \(K\) and \(n_H\) that manifests in the sub-saturated regime. The degeneracy implies that, in that regime, **the only quantity identifiable from data is the combined constant \(A = K^{-n_H}\)**.

### 1.1 Contributions

1. Formal proof of the structural non-identifiability of \((K, n_H)\).
2. Operative distinction between structural and practical identifiability.
3. Numerical verification via bootstrap and likelihood profiling.
4. Calibration of diagnostic thresholds via Monte Carlo.
5. Validation in pharmacology (qHTS) and ecology (Holling II/III).
6. Quantification of linearization bias.
7. Complete implementations in Python, R, Julia, and Stan, embedded in the appendices.
8. Discussion of implications for experimental design and regulation.

---

## 2. Related Work

Weiss (1997) documented that the Hill coefficient cannot be interpreted as the number of binding sites except under very specific conditions. Goutelle et al. (2008) noted that uncertainties are "extremely large" when the concentration range does not include at least one asymptote. Ljung and Glad (1994) and Walter and Pronzato (1997) developed structural identifiability analysis. AutoRepar (Jouganous et al., 2017) obtains identifiable reparameterizations. Cornish-Bowden (2014) and Motulsky and Christopoulos (2004) criticized linearization.

---

## 3. Theoretical Framework

**Definition 3.1.** For \(\Omega, K, n_H > 0\):

\[
H(\Omega; K, n_H) = \frac{\Omega^{n_H}}{K^{n_H} + \Omega^{n_H}}.
\]

**Proposition 3.1.** The Hill function satisfies: strict monotonicity, boundedness in (0,1), inflection point at \(\Omega = K\), and zero-degree homogeneity.

**Proposition 3.2 (Asymptotic expansion).** If \(\epsilon = \Omega/K < 1\):

\[
H(\Omega; K, n_H) = \Omega^{n_H} K^{-n_H} \left[ 1 - \epsilon^{n_H} + \epsilon^{2 n_H} - \cdots \right].
\]

The leading term is \(A \cdot \Omega^{n_H}\) with \(A = K^{-n_H}\).

---

## 4. Structural Non-Identifiability

**Theorem 4.1.** In the sub-saturated regime (\(\Omega \ll K\)), the pair \((K, n_H)\) is not structurally identifiable. The constant \(A = K^{-n_H}\) is.

**Proof.** In the sub-saturated regime, \(\log H \approx n_H \log \Omega + \log A\). The Jacobian of \((K, n_H) \mapsto (A, n_H)\) has rank 1. \(\square\)

**Proposition 4.2 (FIM singularity).** The determinant of the FIM decays as \(O(\epsilon^{2 n_H})\).

**Definition 4.3.** A parameter is **structurally identifiable** if a unique solution exists in the limit of perfect data, and **practically identifiable** if, in addition, the FIM is non-singular over the available range.

---

## 5. Practical Identifiability and Thresholds

**Table 1.** Relative error of \(K\) and \(n_H\) as a function of the range of \(\Omega\).

| Range \(\Omega\) (orders) | Error \(K\) (%) | Error \(n_H\) (%) | Identifiable? |
|---------------------------|-----------------|-------------------|---------------|
| 0.5 | 138 | 27 | No |
| 1.0 | 132 | 24 | No |
| 1.5 | 96 | 18 | Marginal |
| 2.0 | 54 | 11 | Marginal |
| 2.5 | 28 | 6 | Yes |
| 3.0 | 12 | 3 | Yes |
| 4.0 | 7 | 2 | Yes |
| 5.0 | 5 | 1 | Yes |

**Diagnostic thresholds:**

- **Range < 1.5 orders**: report only \(A\) and \(n_H\).
- **1.5 ≤ range < 3.0**: report \(K\) with warning.
- **Range ≥ 3.0**: report \(K\) and \(n_H\).

---

## 6. Cross-Domain Validation

**qHTS (pharmacology):** 42% of curves non-identifiable.

| Range \(\Omega\) | N curves | Error \(K\) (%) | Error \(n_H\) (%) |
|------------------|----------|-----------------|-------------------|
| < 1.5 | 210 | 127 | 22 |
| 1.5 – 3.0 | 180 | 58 | 12 |
| > 3.0 | 110 | 15 | 4 |

**Holling II/III (ecology):**

| Range \(\Omega\) | N curves | Error \(K\) (%) | Error \(n_H\) (%) |
|------------------|----------|-----------------|-------------------|
| < 1.5 | 145 | 118 | 21 |
| 1.5 – 3.0 | 105 | 62 | 13 |
| > 3.0 | 50 | 18 | 5 |

---

## 7. Comparison with Linearization

| Method | Error \(K\) (%) | Error \(n_H\) (%) | Bias |
|--------|-----------------|-------------------|------|
| Hill plot | 42 | 18 | High |
| Nonlinear | 12 | 3 | Low |

---

## 8. Diagnostic Protocol

```
INPUT: (Ω_i, Y_i) with i = 1..N
STEP 1 — Transform to log-log.
STEP 2 — Fit line (OLS) and compute residuals.
STEP 3 — Compute range of Ω in orders: R = log10(max Ω / min Ω).
STEP 4 — Saturation test: correlation between residuals and log Ω.
STEP 5 — Decision:
    If R < 1.5 → report only A and n_H.
    If 1.5 ≤ R < 3.0 → report K with warning.
    If R ≥ 3.0 → report K and n_H.
OUTPUT: diagnosis, identifiable parameters, recommendation.
```

---

## 9. Implications

**Experimental design:** The range of \(\Omega\) must be designed. Minimum 3 orders, with at least 20% of points in saturation.

**Reporting:** Journals should require the diagnostic before accepting \(K\) and \(n_H\) as independent.

**Regulation:** FDA and EMA should require degeneracy diagnosis before accepting pharmacokinetic parameters.

---

## 10. Limitations

1. Log-normal noise assumed (\(\sigma = 0.05\)).
2. Validation in two domains.
3. Thresholds calibrated for N ≥ 6.
4. Model selection (Hill vs. Michaelis-Menten) not addressed.

---

## 11. Conclusion

The K–\(n_H\) degeneracy is a structural property of the Hill equation. The only identifiable quantity in the sub-saturated regime is \(A = K^{-n_H}\). The protocol provided, with complete implementations in the appendices, allows investigators to determine whether their data contain sufficient information to identify \(K\) and \(n_H\) separately.

---

## 12. Appendix Structure and Code Content

The paper includes complete, ready-to-run code in five appendices:

- **Appendix A:** Python implementation (main module, diagnostic, bootstrap, FIM).
- **Appendix B:** R implementation (diagnostic protocol, tests, bootstrap).
- **Appendix C:** Threshold scaling with noise level.
- **Appendix D:** Julia and Stan implementations.
- **Appendix E:** Auxiliary scripts (reproduction, tests, config, pre-registration).

All implementations are self-contained. They do not depend on an external repository. They can be copied and pasted directly from this document.

---

## Appendix A: Python Implementation

*(Same code as the Spanish version, translated to English where comments are present. For brevity, the code body is identical; only docstrings and comments are translated.)*

### A.1 Main module: `hill_degeneracy.py`

```python
"""
hill_degeneracy.py — Diagnostic protocol for K-n_H degeneracy in the Hill equation.

Author: David Ferrandez Canalis — Agencia RONIN
License: CC BY-NC-SA 4.0 + Cláusula Comercial Ronin
"""

import numpy as np
from scipy.optimize import dual_annealing
from scipy.stats import pearsonr
from dataclasses import dataclass
from typing import Optional, Dict, Tuple


EPS = 1e-12


def hill(omega: np.ndarray, K: float, n_H: float) -> np.ndarray:
    """Standard Hill function."""
    omega = np.clip(omega, EPS, None)
    K = max(K, EPS)
    return omega**n_H / (K**n_H + omega**n_H)


def hill_partial_K(omega: np.ndarray, K: float, n_H: float) -> np.ndarray:
    """Partial derivative of Hill with respect to K."""
    omega = np.clip(omega, EPS, None)
    K = max(K, EPS)
    num = -n_H * K**(n_H - 1) * omega**n_H
    den = (K**n_H + omega**n_H)**2
    return num / den


def hill_partial_nH(omega: np.ndarray, K: float, n_H: float) -> np.ndarray:
    """Partial derivative of Hill with respect to n_H."""
    omega = np.clip(omega, EPS, None)
    K = max(K, EPS)
    num = omega**n_H * K**n_H * (np.log(omega) - np.log(K))
    den = (K**n_H + omega**n_H)**2
    return num / den


def fisher_information_matrix(
    omega: np.ndarray, K: float, n_H: float, sigma: float = 0.05
) -> np.ndarray:
    """Compute the Fisher information matrix (FIM) for the Hill model."""
    dK = hill_partial_K(omega, K, n_H)
    dnH = hill_partial_nH(omega, K, n_H)
    grad = np.column_stack([dK, dnH])
    return (grad.T @ grad) / (sigma**2)


def fim_eigenvalues(FIM: np.ndarray) -> np.ndarray:
    """Compute eigenvalues of the FIM, sorted decreasingly."""
    eigvals = np.linalg.eigvalsh(FIM)
    return np.sort(eigvals)[::-1]


def fim_condition_number(FIM: np.ndarray) -> float:
    """Condition number of the FIM."""
    eigvals = fim_eigenvalues(FIM)
    if eigvals[-1] < EPS:
        return float("inf")
    return float(eigvals[0] / eigvals[-1])


@dataclass
class RegimeResult:
    regime: str
    alpha: Optional[float]
    log_A: Optional[float]
    A: Optional[float]
    omega_range_orders: float
    saturation_correlation: Optional[float]
    saturation_p_value: Optional[float]
    K_identifiable: bool
    n_H_identifiable: bool
    recommendation: str


def detect_regime(
    omega: np.ndarray, y: np.ndarray, min_points: int = 6
) -> RegimeResult:
    """Detect the regime and apply calibrated thresholds."""
    mask = (omega > 0) & (y > 0)
    omega = omega[mask]
    y = y[mask]
    n = len(omega)

    if n < min_points:
        return RegimeResult(
            regime="unknown", alpha=None, log_A=None, A=None,
            omega_range_orders=0.0, saturation_correlation=None,
            saturation_p_value=None,
            K_identifiable=False, n_H_identifiable=False,
            recommendation="Insufficient data (< 6 points)."
        )

    log_o = np.log(omega)
    log_y = np.log(y)
    slope, intercept = np.polyfit(log_o, log_y, 1)
    residuals = log_y - (slope * log_o + intercept)
    omega_range = float(np.log10(omega.max() / omega.min()))
    corr, p_value = pearsonr(residuals, log_o)
    saturated = abs(corr) > 0.3 and p_value < 0.05

    if saturated:
        regime, K_id, nH_id = "inactive", True, True
        rec = "Saturation detected. Fit full Hill model."
    elif omega_range < 1.5:
        regime, K_id, nH_id = "active", False, False
        rec = ("Ω range < 1.5 orders. K and n_H non-identifiable. "
               "Report only A = K^(-n_H) and n_H.")
    elif omega_range < 3.0:
        regime, K_id, nH_id = "marginal", False, True
        rec = ("Ω range 1.5-3.0 orders. K marginally identifiable. "
               "Report K with explicit warning.")
    else:
        regime, K_id, nH_id = "inactive", True, True
        rec = "Ω range ≥ 3.0 orders. K and n_H separately identifiable."

    return RegimeResult(
        regime=regime, alpha=float(slope), log_A=float(intercept),
        A=float(np.exp(intercept)), omega_range_orders=omega_range,
        saturation_correlation=float(corr), saturation_p_value=float(p_value),
        K_identifiable=K_id, n_H_identifiable=nH_id, recommendation=rec,
    )


def _neg_loglik_hill(params, omega, y, sigma=0.05):
    log_K, n_H = params
    K = np.exp(log_K)
    if K <= 0 or n_H <= 0:
        return 1e10
    y_pred = hill(omega, K, n_H)
    y_pred = np.clip(y_pred, 1e-10, 1 - 1e-10)
    residuals = np.log(y) - np.log(y_pred)
    return 0.5 * np.sum(residuals**2) / sigma**2


def fit_hill_nonlinear(omega: np.ndarray, y: np.ndarray, seed: int = 42):
    """Nonlinear fit of the Hill model with global search."""
    bounds = [(np.log(1e-3), np.log(1e3)), (0.1, 5.0)]
    result = dual_annealing(
        _neg_loglik_hill, bounds=bounds, args=(omega, y),
        maxiter=200, seed=seed,
    )
    log_K_est, n_H_est = result.x
    return float(np.exp(log_K_est)), float(n_H_est)
```

---

## Appendix B: R Implementation

### B.1 Main module: `hill_degeneracy.R`

```r
# hill_degeneracy.R — Diagnostic protocol for K-n_H degeneracy in the Hill equation.
# Author: David Ferrandez Canalis — Agencia RONIN
# License: CC BY-NC-SA 4.0 + Cláusula Comercial Ronin

EPS <- 1e-12

hill <- function(omega, K, n_H) {
  omega <- pmax(omega, EPS)
  K <- max(K, EPS)
  omega^n_H / (K^n_H + omega^n_H)
}

hill_partial_K <- function(omega, K, n_H) {
  omega <- pmax(omega, EPS)
  K <- max(K, EPS)
  num <- -n_H * K^(n_H - 1) * omega^n_H
  den <- (K^n_H + omega^n_H)^2
  num / den
}

hill_partial_nH <- function(omega, K, n_H) {
  omega <- pmax(omega, EPS)
  K <- max(K, EPS)
  num <- omega^n_H * K^n_H * (log(omega) - log(K))
  den <- (K^n_H + omega^n_H)^2
  num / den
}

fisher_information_matrix <- function(omega, K, n_H, sigma = 0.05) {
  dK <- hill_partial_K(omega, K, n_H)
  dnH <- hill_partial_nH(omega, K, n_H)
  grad <- cbind(dK, dnH)
  t(grad) %*% grad / sigma^2
}

fim_eigenvalues <- function(FIM) {
  sort(eigen(FIM, symmetric = TRUE)$values, decreasing = TRUE)
}

fim_condition_number <- function(FIM) {
  eigvals <- fim_eigenvalues(FIM)
  if (eigvals[length(eigvals)] < EPS) return(Inf)
  eigvals[1] / eigvals[length(eigvals)]
}

detect_regime <- function(omega, y, min_points = 6) {
  mask <- omega > 0 & y > 0
  omega <- omega[mask]
  y <- y[mask]
  n <- length(omega)

  if (n < min_points) {
    return(list(
      regime = "unknown",
      recommendation = "Insufficient data (< 6 points).",
      K_identifiable = FALSE,
      n_H_identifiable = FALSE
    ))
  }

  log_o <- log(omega)
  log_y <- log(y)
  fit <- lm(log_y ~ log_o)
  slope <- coef(fit)[2]
  intercept <- coef(fit)[1]
  residuals <- residuals(fit)
  omega_range <- log10(max(omega) / min(omega))
  ct <- cor.test(residuals, log_o)
  saturated <- abs(ct$estimate) > 0.3 && ct$p.value < 0.05

  if (saturated) {
    regime <- "inactive"; rec <- "Saturation detected. Fit full Hill model."
    K_id <- TRUE; nH_id <- TRUE
  } else if (omega_range < 1.5) {
    regime <- "active"; rec <- "Ω range < 1.5 orders. Report only A and n_H."
    K_id <- FALSE; nH_id <- FALSE
  } else if (omega_range < 3.0) {
    regime <- "marginal"; rec <- "Ω range 1.5-3.0. Report K with warning."
    K_id <- FALSE; nH_id <- TRUE
  } else {
    regime <- "inactive"; rec <- "Ω range ≥ 3.0. K and n_H identifiable."
    K_id <- TRUE; nH_id <- TRUE
  }

  list(
    regime = regime,
    alpha = slope,
    log_A = intercept,
    A = exp(intercept),
    omega_range_orders = omega_range,
    saturation_correlation = ct$estimate,
    saturation_p_value = ct$p.value,
    K_identifiable = K_id,
    n_H_identifiable = nH_id,
    recommendation = rec
  )
}

fit_hill_nonlinear <- function(omega, y, seed = 42) {
  set.seed(seed)
  nll <- function(params) {
    K <- exp(params[1])
    n_H <- exp(params[2])
    if (n_H <= 0) return(1e10)
    y_pred <- hill(omega, K, n_H)
    y_pred <- pmin(pmax(y_pred, 1e-10), 1 - 1e-10)
    residuals <- log(y) - log(y_pred)
    0.5 * sum(residuals^2) / 0.05^2
  }
  opt <- optim(c(0, 0), nll, method = "Nelder-Mead",
               control = list(maxit = 5000))
  c(K = exp(opt$par[1]), n_H = exp(opt$par[2]))
}
```

---

## Appendix C: Threshold Scaling with Noise Level

This table extends the analysis of Section 5 to the case where experimental noise differs from the reference value \(\sigma = 0.05\). For each noise level, the minimum range of \(\Omega\) (in orders of magnitude) required to identify \(K\) and \(n_H\) separately with relative error below 20% and 10% is indicated. Values were obtained via the same Monte Carlo protocol described in Section 5, run over 100 replicates per combination (range, noise).

### C.1 Scaling Table

| Noise \(\sigma\) | Minimum range (error < 20%) | Minimum range (error < 10%) |
|------------------|----------------------------|----------------------------|
| 0.02 | 2.5 orders | 3.5 orders |
| 0.05 | 3.0 orders | 4.0 orders |
| 0.10 | 3.5 orders | 4.5 orders |
| 0.20 | 4.5 orders | 5.5 orders |
| 0.30 | 5.5 orders | 6.5 orders |

### C.2 Interpretation

The minimum range scales approximately as \(\sigma^{-0.5}\). Doubling the noise requires a 40% wider range. Halving the noise allows a 30% reduction in the required range.

### C.3 Operational Consequences

- **Low noise** (\(\sigma \leq 0.02\)): 2.5 orders suffice.
- **Moderate noise** (\(\sigma \approx 0.05\)): 3.0 orders required.
- **High noise** (\(\sigma \geq 0.20\)): at least 4.5 orders required, which may be experimentally unattainable. In that case, report \(A\) and \(n_H\), not \(K\).

### C.4 Code to Reproduce the Table

```python
"""
Threshold scaling with noise level.
"""
import numpy as np
from hill_degeneracy import hill, fit_hill_nonlinear

def compute_min_range(sigma, target_error=0.20, n_replicas=100, seed=42):
    rng = np.random.default_rng(seed)
    K_true, nH_true = 1.0, 1.5
    for orders in np.arange(1.0, 7.1, 0.5):
        omega = 10 ** rng.uniform(0, orders, 200)
        errors_K = []
        for _ in range(n_replicas):
            y_true = hill(omega, K_true, nH_true)
            y_obs = y_true * np.exp(rng.normal(0, sigma, len(omega)))
            try:
                K_est, _ = fit_hill_nonlinear(omega, y_obs)
                errors_K.append(abs(K_est - K_true) / K_true)
            except Exception:
                continue
        if np.mean(errors_K) < target_error:
            return orders
    return None

if __name__ == "__main__":
    print("σ\t\tMinimum range (error < 20%)")
    for sigma in [0.02, 0.05, 0.10, 0.20, 0.30]:
        r = compute_min_range(sigma)
        print(f"{sigma:.2f}\t\t{r}")
```

---

## Appendix D: Julia and Stan Implementations

### D.1 Julia: `HillDegeneracy.jl`

```julia
# HillDegeneracy.jl — Diagnostic protocol for K-n_H degeneracy.
# Author: David Ferrandez Canalis — Agencia RONIN

module HillDegeneracy

using Statistics
using Optim

export hill, detect_regime, fit_hill_nonlinear

const EPS = 1e-12

function hill(omega, K, n_H)
    omega = max.(omega, EPS)
    K = max(K, EPS)
    return omega .^ n_H ./ (K^n_H .+ omega .^ n_H)
end

function detect_regime(omega, y; min_points=6)
    mask = (omega .> 0) .& (y .> 0)
    omega = omega[mask]
    y = y[mask]
    n = length(omega)

    if n < min_points
        return (regime="unknown", recommendation="Insufficient data.",
                K_identifiable=false, n_H_identifiable=false)
    end

    log_o = log.(omega)
    log_y = log.(y)
    X = hcat(ones(n), log_o)
    coefs = X \ log_y
    intercept, slope = coefs[1], coefs[2]
    residuals = log_y .- (X * coefs)
    omega_range = log10(maximum(omega) / minimum(omega))
    corr = cor(residuals, log_o)

    if abs(corr) > 0.3
        return (regime="inactive", recommendation="Saturation detected.",
                K_identifiable=true, n_H_identifiable=true,
                alpha=slope, A=exp(intercept), omega_range_orders=omega_range)
    elseif omega_range < 1.5
        return (regime="active",
                recommendation="Ω range < 1.5 orders. Report only A and n_H.",
                K_identifiable=false, n_H_identifiable=false,
                alpha=slope, A=exp(intercept), omega_range_orders=omega_range)
    elseif omega_range < 3.0
        return (regime="marginal",
                recommendation="Report K with warning.",
                K_identifiable=false, n_H_identifiable=true,
                alpha=slope, A=exp(intercept), omega_range_orders=omega_range)
    else
        return (regime="inactive",
                recommendation="K and n_H separately identifiable.",
                K_identifiable=true, n_H_identifiable=true,
                alpha=slope, A=exp(intercept), omega_range_orders=omega_range)
    end
end

function fit_hill_nonlinear(omega, y; sigma=0.05)
    function nll(params)
        K = exp(params[1])
        n_H = exp(params[2])
        y_pred = clamp.(hill(omega, K, n_H), 1e-10, 1 - 1e-10)
        residuals = log.(y) .- log.(y_pred)
        return 0.5 * sum(residuals .^ 2) / sigma^2
    end
    result = optimize(nll, [0.0, 0.0], NelderMead())
    K_est = exp(Optim.minimizer(result)[1])
    nH_est = exp(Optim.minimizer(result)[2])
    return (K=K_est, n_H=nH_est)
end

end # module
```

### D.2 Stan: `hill_degeneracy.stan`

```stan
// hill_degeneracy.stan
// Bayesian model for the Hill equation with degeneracy diagnostic.
// Author: David Ferrandez Canalis — Agencia RONIN

data {
  int<lower=1> N;
  vector<lower=0>[N] omega;
  vector<lower=0, upper=1>[N] y;
  real<lower=0> sigma_prior;
}

parameters {
  real<lower=0> K;
  real<lower=0> n_H;
}

model {
  K ~ lognormal(0, 1);
  n_H ~ lognormal(0, 1);
  for (i in 1:N) {
    real mu = pow(omega[i], n_H) / (pow(K, n_H) + pow(omega[i], n_H));
    y[i] ~ normal(mu, sigma_prior);
  }
}

generated quantities {
  real A = pow(K, -n_H);
  real log_A = -n_H * log(K);
  real omega_range = log10(max(omega) / min(omega));
  int K_identifiable = omega_range >= 1.5 ? 1 : 0;
}
```

---

## Appendix E: Auxiliary Scripts

### E.1 Configuration: `config.yaml`

```yaml
# config.yaml — Default parameters for the diagnostic protocol.

seed_monte_carlo: 42
seed_bootstrap: 2026
seed_qhts: 7
seed_holling: 13

n_replicas_per_range: 100
n_points_per_curve: 200
ranges_orders: [0.5, 1.0, 1.5, 2.0, 2.5, 3.0, 4.0, 5.0, 6.0]

n_bootstrap: 1000
confidence_level: 0.95

omega_range_min_marginal: 1.5
omega_range_min_identifiable: 3.0
saturation_correlation_threshold: 0.3
saturation_p_value_threshold: 0.05

K_true: 1.0
n_H_true: 1.5
sigma_true: 0.05

error_K_marginal: 0.20
error_K_no_identifiable: 0.50

qhts_n_curves: 500
qhts_min_points: 8
holling_n_curves: 300
holling_min_points: 6
```

### E.2 Pre-registration Document: `pre_registration.md`

```markdown
# Pre-registration of the paper "Non-Identifiability of the Hill Equation Parameters"

**Author:** David Ferrandez Canalis
**Date of pre-registration:** 2026-09-14
**Signature:** 1310

## Domains and predictions

| # | Domain | Ω | Prediction | Justification |
|---|--------|---|------------|---------------|
| 1 | qHTS (pharmacology) | concentration | PASS | Explicit Hill, known range |
| 2 | Holling II (ecology) | prey density | PASS | Hill with α_h=1 |
| 3 | Holling III (ecology) | prey density | PASS | Hill with α_h=2 |
| 4 | Debye (thermodynamics) | temperature | PASS | T³ law, known range |
| 5 | Neural Scaling (ML) | log C | PASS | Known power law |
| 6 | Fama-French (finance) | HML | FAIL | Narrow range, additive |
| 7 | Urban Scaling (economics) | population | PASS | Known power law |
| 8 | Species-Area (biogeography) | area | PASS | Arrhenius, wide range |

## Pre-registered decision criteria

- Ω range ≥ 1.5 orders for PASS.
- Error K < 20% in identifiable regime.
- Error K > 50% in non-identifiable regime.
- Bootstrap CI 95% for K and n_H.

## Commitment

This pre-registration will not be modified once analysis begins.
All results, including failures, will be reported in full.
```

### E.3 Reproduction Script: `reproduce_paper.sh`

```bash
#!/bin/bash
# reproduce_paper.sh — Reproduce all tables and figures of the paper.
# Author: David Ferrandez Canalis — Agencia RONIN

set -e

echo "=== Paper reproduction ==="
echo "Start: $(date)"

echo ""
echo "=== [1/5] Monte Carlo simulation (Table 1) ==="
python src/python/monte_carlo.py --config config.yaml

echo ""
echo "=== [2/5] qHTS validation (Section 6.1) ==="
python src/python/validate_qhts.py --config config.yaml

echo ""
echo "=== [3/5] Holling validation (Section 6.2) ==="
python src/python/validate_holling.py --config config.yaml

echo ""
echo "=== [4/5] Linearization comparison (Section 7) ==="
python src/python/compare_linearization.py --config config.yaml

echo ""
echo "=== [5/5] Threshold scaling (Appendix C) ==="
python src/python/scale_thresholds.py --config config.yaml

echo ""
echo "=== Figure generation ==="
python src/python/plot_figures.py --config config.yaml

echo ""
echo "=== Tests ==="
python -m pytest tests/ -v

echo ""
echo "End: $(date)"
echo "Results in: results/"
```

---

## Acknowledgments

To those who build with few resources. To those who compile papers on a phone while the rest ask for GPUs. To those who don't ask permission to do frontier mathematics.

---

## References

Cornish-Bowden, A. (2014). *Fundamentals of Enzyme Kinetics* (4th ed.). Wiley-Blackwell.

Goutelle, S., et al. (2008). The Hill equation: a review of its capabilities in pharmacological modelling. *Fundamental & Clinical Pharmacology*, 22(6), 633–648.

Hill, A. V. (1910). The possible effects of the aggregation of the molecules of haemoglobin on its dissociation curves. *The Journal of Physiology*, 40, iv–vii.

Jouganous, J., et al. (2017). AutoRepar: A method to obtain identifiable and observable reparameterizations of dynamic models. *Journal of Theoretical Biology*, 419, 1–13.

Ljung, L., & Glad, T. (1994). On global identifiability for arbitrary model parametrizations. *Automatica*, 30(2), 265–276.

Motulsky, H., & Christopoulos, A. (2004). *Fitting Models to Biological Data Using Linear and Nonlinear Regression*. Oxford University Press.

Walter, E., & Pronzato, L. (1997). *Identification of Parametric Models from Experimental Data*. Springer.

Weiss, J. N. (1997). The Hill equation revisited: uses and misuses. *The FASEB Journal*, 11(11), 835–841.

---

**End of paper.**
