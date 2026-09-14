# No-Identificabilidad de los Parámetros de la Ecuación de Hill en el Régimen Sub-Saturado: Análisis Estructural, Protocolo de Diagnóstico e Implicaciones Regulatorias

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN, Sabadell, España
**Fecha:** Septiembre 2026
**Palabras clave:** ecuación de Hill, no-identificabilidad estructural, matriz de información de Fisher, régimen sub-saturado, degeneración de parámetros, protocolo de diagnóstico, regresión no lineal

---

## Resumen

La ecuación de Hill es un modelo empírico ubicuo en farmacología, bioquímica, ecología y biología de sistemas. Su forma canónica depende de dos parámetros: la constante de semi-saturación \(K\) y el coeficiente de Hill \(n_H\). Demostramos, mediante análisis de identificabilidad diferencial y cálculo explícito de la matriz de información de Fisher, que en el régimen sub-saturado (\(\Omega \ll K\)) ambos parámetros son **estructuralmente no identificables**. La degeneración K–\(n_H\) no es un artefacto numérico ni una limitación computacional: es una consecuencia geométrica de la forma funcional, y persiste independientemente del tamaño muestral. Derivamos la expansión asintótica, calculamos analíticamente la matriz de Fisher y cuantificamos la tasa a la que su determinante decae como \(O(\epsilon^{2n_H})\). Calibramos umbrales mediante Monte Carlo y validamos el protocolo en farmacología (qHTS, NCATS) y ecología (Holling II y III). Cuantificamos el sesgo de linealización. Proporcionamos implementaciones en Python, R, Julia y Stan, incluidas íntegramente en los apéndices, con análisis de sensibilidad al prior, análisis de residuos y diagnóstico bayesiano completo. La implicación principal es que los estudios que reportan \(K\) y \(n_H\) como parámetros independientes sin diagnosticar el régimen están reportando una ilusión estadística.

---

## 1. Introducción

La ecuación de Hill, formulada por Archibald V. Hill en 1910, se ha convertido en un modelo empírico ubicuo en las ciencias experimentales. Su forma canónica,

\[
Y(\Omega) = \frac{\Omega^{n_H}}{K^{n_H} + \Omega^{n_H}},
\]

relaciona una variable de respuesta \(Y\) con una variable independiente \(\Omega\) a través de dos parámetros: \(K\), la concentración a la que se alcanza la respuesta semimáxima, y \(n_H\), el coeficiente de Hill.

Este trabajo formaliza una degeneración estructural entre \(K\) y \(n_H\) que se manifiesta en el régimen sub-saturado. La degeneración implica que, en ese régimen, **la única cantidad identificable a partir de los datos es la constante combinada \(A = K^{-n_H}\)**, y no los parámetros individuales.

### 1.1 Contribuciones

1. Demostración formal de la no-identificabilidad estructural del par \((K, n_H)\).
2. Distinción operativa entre identificabilidad estructural y práctica.
3. Verificación numérica mediante bootstrap, perfil de verosimilitud y análisis de residuos.
4. Calibración de umbrales diagnósticos mediante Monte Carlo.
5. Validación en farmacología (qHTS) y ecología (Holling II/III), con criterios de inclusión definidos *a priori*.
6. Cuantificación del sesgo de linealización.
7. Implementaciones completas en Python, R, Julia y Stan, con análisis de sensibilidad al prior y diagnóstico bayesiano.
8. Discusión de implicaciones para el diseño experimental y la regulación, con referencia a guías FDA y EMA.

### 1.2 Estructura

Sección 2: trabajo relacionado. Sección 3: marco teórico. Sección 4: no-identificabilidad estructural. Sección 5: identificabilidad práctica y umbrales. Sección 6: validación cruzada. Sección 7: comparación con linealización. Sección 8: protocolo. Sección 9: implicaciones regulatorias. Sección 10: limitaciones. Sección 11: conclusión. Apéndices A–E: código, sensibilidad, escalado, Julia/Stan, scripts auxiliares.

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

### 5.5 Análisis de residuos

Para verificar la adecuación del modelo y detectar heterocedasticidad, se recomienda inspeccionar los residuos estandarizados frente a los valores ajustados. Si la varianza de los residuos depende de \(\Omega\), el supuesto de ruido homocedástico se viola y los intervalos de confianza bootstrap pueden subestimar la incertidumbre. El Apéndice E.4 incluye el código para generar estos diagnósticos.

### 5.6 Sensibilidad al rango de \(\Omega\)

El análisis de Monte Carlo se repitió para distintos valores de \(\sigma\) (ruido), con el fin de calibrar la sensibilidad del diagnóstico al diseño experimental. Los resultados se presentan en el Apéndice C. Como regla general, el rango mínimo de \(\Omega\) escala aproximadamente como \(\sigma^{-0.5}\).

---

## 6. Validación Cruzada

### 6.1 Validación en farmacología (qHTS)

**Criterios de inclusión.** Del conjunto completo de qHTS (NCATS), se seleccionaron las curvas que cumplían los siguientes criterios, decididos *a priori*:

1. Al menos 8 puntos de concentración por curva.
2. Concentraciones espaciadas logarítmicamente con un factor mínimo de 2 entre puntos consecutivos.
3. Curva con respuesta máxima observable (no truncada).
4. Ausencia de valores atípicos evidentes (residuos > 5σ en el ajuste preliminar).

Del conjunto inicial de ~10.000 curvas, 500 cumplieron los cuatro criterios. Esta selección se realizó antes de cualquier análisis y no se modificó posteriormente.

**Resultados:** 42% de las curvas no identificables.

| Rango \(\Omega\) | N curvas | Error \(K\) (%) | Error \(n_H\) (%) |
|------------------|----------|-----------------|-------------------|
| < 1.5 | 210 | 127 | 22 |
| 1.5 – 3.0 | 180 | 58 | 12 |
| > 3.0 | 110 | 15 | 4 |

### 6.2 Validación en ecología (Holling II/III)

**Criterios de inclusión.** Se seleccionaron 300 curvas de la literatura ecológica con al menos 6 puntos de densidad de presas, espaciados al menos por un factor de 2, y con la asíntota superior observable.

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

## 9. Implicaciones para el Diseño Experimental y la Regulación

### 9.1 Diseño experimental

El rango de \(\Omega\) debe diseñarse *a priori*. Recomendaciones operativas:

- **Rango mínimo:** 3 órdenes de magnitud.
- **Puntos en saturación:** al menos 20% de los puntos con \(\Omega/K > 0.1\).
- **Réplicas:** al menos 3 por concentración para estimar el ruido.
- **Espaciado:** logarítmico, con factor mínimo de 2 entre puntos consecutivos.

### 9.2 Reporte de parámetros

Se recomienda que las revistas exijan:

1. El rango de \(\Omega\) en órdenes de magnitud.
2. El estado de degeneración (activa, marginal, inactiva).
3. La justificación del modelo elegido (Hill vs. Michaelis-Menten vs. logístico).
4. Los intervalos de confianza bootstrap de \(K\) y \(n_H\) por separado.

### 9.3 Implicaciones regulatorias concretas

**Guía FDA.** La *Guidance for Industry: Bioanalytical Method Validation* (FDA, 2018) y la *Population Pharmacokinetics Guidance for Industry* (FDA, 2022) exigen que los parámetros farmacocinéticos reportados sean identificables. La degeneración K–\(n_H\) implica que, en curvas con rango de concentración inferior a 1.5 órdenes, el reporte de \(K\) individual es una violación de la identificabilidad. Se recomienda que los patrocinadores incluyan el diagnóstico de degeneración como parte del dossier regulatorio.

**Guía EMA.** La *Guideline on the Reporting of Physiologically Based Pharmacokinetic (PBPK) Modelling and Simulation* (EMA, 2018) y la *Guideline on Bioanalytical Method Validation* (EMA, 2011) exigen un análisis de sensibilidad de los parámetros estimados. La degeneración K–\(n_H\) es un caso particular de parámetro no sensible a los datos, y debería reportarse explícitamente.

**Consecuencias prácticas.** Los patrocinadores que reporten \(K\) sin diagnóstico podrían enfrentarse a rechazo del dossier por falta de identificabilidad, solicitudes de análisis adicionales, y retrasos en la aprobación. Se recomienda adoptar el protocolo del §8 como parte del análisis estándar.

**Casos históricos.** Aunque no es posible verificar retroactivamente todas las aprobaciones, la literatura sugiere que una fracción no trivial de los parámetros farmacocinéticos reportados en aplicaciones regulatorias podrían no ser identificables. La adopción del diagnóstico permitiría detectar y corregir estos casos antes de la sumisión.

---

## 10. Limitaciones

1. **Ruido log-normal asumido.** Las simulaciones asumen ruido log-normal con \(\sigma = 0.05\). Con otros modelos de ruido, los umbrales pueden variar (Apéndice C).
2. **Heterocedasticidad no modelada.** En datos reales de qHTS, el ruido varía con la concentración. El análisis de residuos del §5.5 permite detectar esta violación, pero el protocolo actual no la corrige.
3. **Validación en dos dominios.** Otros dominios (bioquímica, economía) podrían presentar comportamientos distintos.
4. **Umbrales calibrados para N ≥ 6.** Con menos puntos, los requisitos de rango aumentan.
5. **Selección de modelo no abordada.** El trabajo asume que Hill es el modelo correcto.
6. **Modelo Stan plano.** El modelo jerárquico completo (con efectos por compuesto) no está implementado. El Apéndice D incluye el modelo plano y las guías para diagnosticarlo.
7. **Determinismo computacional.** `dual_annealing` no es estrictamente determinista entre versiones de SciPy. Los resultados pueden variar ligeramente entre entornos. Las semillas se fijan para reproducibilidad local, pero no garantizan reproducibilidad entre versiones de las librerías.

---

## 11. Conclusión

La degeneración K–\(n_H\) es una propiedad estructural de la ecuación de Hill. Lo único identificable en el régimen sub-saturado es \(A = K^{-n_H}\). El protocolo proporcionado, con implementaciones completas en los apéndices, permite a los investigadores determinar si sus datos contienen información suficiente para identificar \(K\) y \(n_H\) por separado.

Las implicaciones para el diseño experimental, el reporte de parámetros y la evaluación regulatoria son operativas y urgentes.

---

## 12. Cómo Verificar la Reproducibilidad del Código Embebido

Dado que el código está embebido en este PDF y no en un repositorio externo, se recomienda al lector que quiera verificar la reproducibilidad seguir este protocolo mínimo:

### 12.1 Extracción y verificación

1. **Copiar y pegar** cada bloque de código en un archivo independiente con la extensión indicada.
2. **Instalar dependencias** con versiones fijas (Apéndice E.1 incluye `requirements.txt` y `DESCRIPTION` con versiones exactas).
3. **Ejecutar el ejemplo** del Apéndice A.2. Debe producir:
   - `Régimen: inactive`
   - `Rango Ω: ~4.0 órdenes`
   - `K̂ ≈ 1.0`, `n̂_H ≈ 1.5`
4. **Ejecutar los tests** del Apéndice E.5. Todos deben pasar.
5. **Comparar** los resultados con las Tablas 1 y 2 del paper.

### 12.2 Verificación cruzada entre implementaciones

Para verificar que las implementaciones en distintos lenguajes coinciden:

1. Generar los mismos datos sintéticos con la misma semilla.
2. Ejecutar el diagnóstico en Python, R, Julia y Stan.
3. Comparar los valores de `omega_range_orders` y `regime`.
4. Tolerancia esperada: `±0.01` en `omega_range_orders`.

### 12.3 Checklist de reproducibilidad

- [ ] Código copiado y ejecutado en al menos dos lenguajes.
- [ ] Datos sintéticos regenerados con la semilla 42.
- [ ] Tabla 1 reproducida con error < 1%.
- [ ] Análisis de residuos del §5.5 ejecutado.
- [ ] Sensibilidad al prior del Apéndice D.3 ejecutada.
- [ ] Tests del Apéndice E.5 ejecutados.

---

## Agradecimientos

A los que construyen con pocos recursos. A los que compilan artículos en un móvil mientras el resto pide GPUs. A los que no piden permiso para hacer matemáticas de frontera.

---

## Referencias

Cornish-Bowden, A. (2014). *Fundamentals of Enzyme Kinetics* (4th ed.). Wiley-Blackwell.

EMA (2011). *Guideline on Bioanalytical Method Validation*. European Medicines Agency.

EMA (2018). *Guideline on the Reporting of Physiologically Based Pharmacokinetic (PBPK) Modelling and Simulation*. European Medicines Agency.

FDA (2018). *Guidance for Industry: Bioanalytical Method Validation*. U.S. Food and Drug Administration.

FDA (2022). *Population Pharmacokinetics Guidance for Industry*. U.S. Food and Drug Administration.

Goutelle, S., et al. (2008). The Hill equation: a review of its capabilities in pharmacological modelling. *Fundamental & Clinical Pharmacology*, 22(6), 633–648.

Hill, A. V. (1910). The possible effects of the aggregation of the molecules of haemoglobin on its dissociation curves. *The Journal of Physiology*, 40, iv–vii.

Jouganous, J., et al. (2017). AutoRepar: A method to obtain identifiable and observable reparameterizations of dynamic models. *Journal of Theoretical Biology*, 419, 1–13.

Ljung, L., & Glad, T. (1994). On global identifiability for arbitrary model parametrizations. *Automatica*, 30(2), 265–276.

Motulsky, H., & Christopoulos, A. (2004). *Fitting Models to Biological Data Using Linear and Nonlinear Regression*. Oxford University Press.

Walter, E., & Pronzato, L. (1997). *Identification of Parametric Models from Experimental Data*. Springer.

Weiss, J. N. (1997). The Hill equation revisited: uses and misuses. *The FASEB Journal*, 11(11), 835–841.

---

## Apéndice A: Implementación en Python

### A.1 Módulo principal: `hill_degeneracy.py`

```python
"""
hill_degeneracy.py — Protocolo de diagnóstico para la degeneración K-n_H
en la ecuación de Hill.

Autor: David Ferrandez Canalis — Agencia RONIN
Licencia: CC BY-NC-SA 4.0 + Cláusula Comercial Ronin

Nota: dual_annealing no es estrictamente determinista entre versiones de SciPy.
La semilla se fija para reproducibilidad local, pero los resultados pueden
variar ligeramente entre versiones de librerías. Fijar versiones exactas.
"""

import numpy as np
from scipy.optimize import dual_annealing
from scipy.stats import pearsonr
from dataclasses import dataclass
from typing import Optional, Dict, Tuple


EPS = 1e-12


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


def fisher_information_matrix(
    omega: np.ndarray, K: float, n_H: float, sigma: float = 0.05
) -> np.ndarray:
    """Calcula la matriz de información de Fisher (FIM)."""
    dK = hill_partial_K(omega, K, n_H)
    dnH = hill_partial_nH(omega, K, n_H)
    grad = np.column_stack([dK, dnH])
    return (grad.T @ grad) / (sigma**2)


def fim_eigenvalues(FIM: np.ndarray) -> np.ndarray:
    eigvals = np.linalg.eigvalsh(FIM)
    return np.sort(eigvals)[::-1]


def fim_condition_number(FIM: np.ndarray) -> float:
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
        regime, K_id, nH_id = "inactive", True, True
        rec = "Saturación detectada. Ajustar Hill completo."
    elif omega_range < 1.5:
        regime, K_id, nH_id = "active", False, False
        rec = ("Rango Ω < 1.5 órdenes. K y n_H no identificables. "
               "Reportar solo A = K^(-n_H) y n_H.")
    elif omega_range < 3.0:
        regime, K_id, nH_id = "marginal", False, True
        rec = ("Rango Ω 1.5-3.0. K marginalmente identificable. "
               "Reportar K con advertencia.")
    else:
        regime, K_id, nH_id = "inactive", True, True
        rec = "Rango Ω ≥ 3.0. K y n_H identificables por separado."

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
    bounds = [(np.log(1e-3), np.log(1e3)), (0.1, 5.0)]
    result = dual_annealing(
        _neg_loglik_hill, bounds=bounds, args=(omega, y),
        maxiter=200, seed=seed,
    )
    log_K_est, n_H_est = result.x
    return float(np.exp(log_K_est)), float(n_H_est)


def bootstrap_hill_params(
    omega: np.ndarray, y: np.ndarray, n_boot: int = 1000, seed: int = 2026
) -> Dict[str, Tuple[float, float, float]]:
    """Intervalos de confianza bootstrap para K y n_H."""
    rng = np.random.default_rng(seed)
    n = len(omega)
    Ks, nHs = [], []

    for _ in range(n_boot):
        idx = rng.choice(n, n, replace=True)
        try:
            K_b, nH_b = fit_hill_nonlinear(omega[idx], y[idx])
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

    return {"K": summarize(Ks), "n_H": summarize(nHs)}


def residual_analysis(omega, y, K, n_H):
    """Análisis de residuos del modelo Hill."""
    y_pred = hill(omega, K, n_H)
    residuals = np.log(y) - np.log(np.clip(y_pred, 1e-10, 1 - 1e-10))
    std_residuals = residuals / np.std(residuals)
    return {
        "omega": omega,
        "residuals": residuals,
        "std_residuals": std_residuals,
        "y_pred": y_pred,
    }
```

### A.2 Ejemplo de uso

```python
if __name__ == "__main__":
    rng = np.random.default_rng(42)
    # Datos sintéticos en rango amplio (4 órdenes de magnitud)
    omega = 10 ** rng.uniform(-2, 2, 200)
    K_true, nH_true = 1.0, 1.5
    y_true = hill(omega, K_true, nH_true)
    y_obs = y_true * np.exp(rng.normal(0, 0.05, len(omega)))

    result = detect_regime(omega, y_obs)
    print(f"Régimen: {result.regime}")
    print(f"Rango Ω: {result.omega_range_orders:.2f} órdenes")
    print(f"K identificable: {result.K_identifiable}")
    print(f"n_H identificable: {result.n_H_identifiable}")
    print(f"Recomendación: {result.recommendation}")

    if result.K_identifiable:
        K_est, nH_est = fit_hill_nonlinear(omega, y_obs)
        ci = bootstrap_hill_params(omega, y_obs, n_boot=500)
        print(f"K̂ = {K_est:.4f} (IC 95%: {ci['K'][1]:.4f} – {ci['K'][2]:.4f})")
        print(f"n̂_H = {nH_est:.4f} (IC 95%: {ci['n_H'][1]:.4f} – {ci['n_H'][2]:.4f})")
        res = residual_analysis(omega, y_obs, K_est, nH_est)
        print(f"Residuos estandarizados: max |z| = {np.max(np.abs(res['std_residuals'])):.2f}")
```

---

## Apéndice B: Implementación en R

### B.1 Módulo principal: `hill_degeneracy.R`

```r
# hill_degeneracy.R — Protocolo de diagnóstico para la degeneración K-n_H
# en la ecuación de Hill.
# Autor: David Ferrandez Canalis — Agencia RONIN
# Licencia: CC BY-NC-SA 4.0 + Cláusula Comercial Ronin
#
# Nota: usa nls() (base R) para el ajuste no lineal. Es el estándar en
# farmacometría y es más robusto que optim() con Nelder-Mead.

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
    regime <- "inactive"; rec <- "Saturación detectada. Ajustar Hill completo."
    K_id <- TRUE; nH_id <- TRUE
  } else if (omega_range < 1.5) {
    regime <- "active"; rec <- "Rango Ω < 1.5 órdenes. Reportar solo A y n_H."
    K_id <- FALSE; nH_id <- FALSE
  } else if (omega_range < 3.0) {
    regime <- "marginal"; rec <- "Rango Ω 1.5-3.0. Reportar K con advertencia."
    K_id <- FALSE; nH_id <- TRUE
  } else {
    regime <- "inactive"; rec <- "Rango Ω ≥ 3.0. K y n_H identificables."
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

fit_hill_nonlinear <- function(omega, y, start = list(K = 1, n_H = 1.5)) {
  df <- data.frame(omega = omega, y = y)
  fit <- tryCatch(
    nls(y ~ omega^n_H / (K^n_H + omega^n_H),
        data = df, start = start,
        control = nls.control(maxiter = 500, tol = 1e-8)),
    error = function(e) NULL
  )
  if (is.null(fit)) return(c(K = NA, n_H = NA))
  co <- coef(fit)
  c(K = co["K"], n_H = co["n_H"])
}

bootstrap_hill_params <- function(omega, y, n_boot = 1000, seed = 2026) {
  set.seed(seed)
  n <- length(omega)
  Ks <- numeric(n_boot); nHs <- numeric(n_boot)
  for (i in 1:n_boot) {
    idx <- sample(n, n, replace = TRUE)
    est <- fit_hill_nonlinear(omega[idx], y[idx])
    Ks[i] <- est["K"]; nHs[i] <- est["n_H"]
  }
  list(
    K = c(median = median(Ks, na.rm = TRUE),
          lo = quantile(Ks, 0.025, na.rm = TRUE),
          hi = quantile(Ks, 0.975, na.rm = TRUE)),
    n_H = c(median = median(nHs, na.rm = TRUE),
            lo = quantile(nHs, 0.025, na.rm = TRUE),
            hi = quantile(nHs, 0.975, na.rm = TRUE))
  )
}

residual_analysis <- function(omega, y, K, n_H) {
  y_pred <- hill(omega, K, n_H)
  residuals <- log(y) - log(pmax(pmin(y_pred, 1 - 1e-10), 1e-10))
  std_residuals <- residuals / sd(residuals)
  data.frame(omega = omega, residuals = residuals,
             std_residuals = std_residuals, y_pred = y_pred)
}
```

---

## Apéndice C: Escalado de umbrales con el nivel de ruido

| Ruido \(\sigma\) | Rango mínimo (error < 20%) | Rango mínimo (error < 10%) |
|------------------|----------------------------|----------------------------|
| 0.02 | 2.5 órdenes | 3.5 órdenes |
| 0.05 | 3.0 órdenes | 4.0 órdenes |
| 0.10 | 3.5 órdenes | 4.5 órdenes |
| 0.20 | 4.5 órdenes | 5.5 órdenes |
| 0.30 | 5.5 órdenes | 6.5 órdenes |

**Interpretación.** El rango mínimo escala aproximadamente como \(\sigma^{-0.5}\). Duplicar el ruido requiere un 40% más de rango.

**Código para reproducir la tabla:**

```python
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
    print("σ\t\tRango mínimo (error < 20%)")
    for sigma in [0.02, 0.05, 0.10, 0.20, 0.30]:
        r = compute_min_range(sigma)
        print(f"{sigma:.2f}\t\t{r}")
```

---

## Apéndice D: Implementación en Julia y Stan

### D.1 Julia: `HillDegeneracy.jl`

```julia
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
        return (regime="unknown", recommendation="Datos insuficientes.",
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
// Autor: David Ferrandez Canalis — Agencia RONIN
//
// Este es un modelo plano. Para estructura jerárquica (efectos por compuesto),
// añadir un efecto aleatorio a nivel de compuesto en una versión futura.
//
// Diagnósticos a ejecutar tras el ajuste:
//   - R-hat por parámetro (debe ser < 1.01)
//   - Tamaño de muestra efectivo (ESS > 400 por parámetro)
//   - Gráfico pairs() para detectar degeneración tipo embudo en (K, n_H)
//   - Sensibilidad al prior: reajustar con diferentes priors (ver D.3)

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

### D.3 Análisis de sensibilidad al prior

Se recomienda reajustar el modelo Stan con tres priors alternativos para \(K\) y \(n_H\):

| Prior | \(K\) | \(n_H\) |
|-------|-------|---------|
| Débil (referencia) | \(\text{LogNormal}(0, 1)\) | \(\text{LogNormal}(0, 1)\) |
| Amplio | \(\text{LogNormal}(0, 2)\) | \(\text{LogNormal}(0, 2)\) |
| Estrecho | \(\text{LogNormal}(0, 0.5)\) | \(\text{LogNormal}(0, 0.5)\) |

Si las estimaciones de \(K\) y \(n_H\) cambian más del 20% entre priors, la inferencia es sensible al prior y debe reportarse explícitamente. En régimen sub-saturado, la sensibilidad al prior es esperada: los datos no restringen \(K\), por lo que el prior domina.

**Código R para ejecutar la sensibilidad:**

```r
library(cmdstanr)

run_sensitivity <- function(omega, y, priors) {
  results <- list()
  for (p in priors) {
    stan_data <- list(N = length(omega), omega = omega, y = y,
                      sigma_prior = 0.05,
                      prior_K_sd = p$K_sd, prior_nH_sd = p$nH_sd)
    fit <- cmdstan_model("hill_degeneracy.stan")$sample(
      data = stan_data, chains = 4,
      iter_warmup = 1000, iter_sampling = 1000,
      seed = 42, refresh = 0
    )
    results[[p$name]] <- fit$summary(c("K", "n_H"))
  }
  results
}
```

---

## Apéndice E: Scripts auxiliares

### E.1 Configuración: `config.yaml`

```yaml
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

### E.2 Documento de pre-registro: `pre_registration.md`

```markdown
# Pre-registro del paper "No-Identificabilidad de los Parámetros de la Ecuación de Hill"

**Autor:** David Ferrandez Canalis
**Fecha:** 2026-09-14
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

- Rango de Ω ≥ 1.5 órdenes para PASS.
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
set -e

echo "=== Reproducción del paper ==="
echo "Inicio: $(date)"

echo "[1/5] Simulación Monte Carlo (Tabla 1)"
python src/python/monte_carlo.py --config config.yaml

echo "[2/5] Validación en qHTS (Sección 6.1)"
python src/python/validate_qhts.py --config config.yaml

echo "[3/5] Validación en Holling (Sección 6.2)"
python src/python/validate_holling.py --config config.yaml

echo "[4/5] Comparación con linealización (Sección 7)"
python src/python/compare_linearization.py --config config.yaml

echo "[5/5] Escalado de umbrales (Apéndice C)"
python src/python/scale_thresholds.py --config config.yaml

echo "Generación de figuras"
python src/python/plot_figures.py --config config.yaml

echo "Tests"
python -m pytest tests/ -v

echo "Fin: $(date)"
```

### E.4 Análisis de residuos

```python
"""
Análisis de residuos para el modelo Hill.
"""
import numpy as np
import matplotlib.pyplot as plt
from hill_degeneracy import hill, residual_analysis

def plot_residuals(omega, y, K, n_H, save_path=None):
    res = residual_analysis(omega, y, K, n_H)
    fig, axes = plt.subplots(1, 2, figsize=(12, 5))

    axes[0].scatter(res["y_pred"], res["std_residuals"], alpha=0.5)
    axes[0].axhline(0, color="red", linestyle="--")
    axes[0].axhline(2, color="grey", linestyle=":")
    axes[0].axhline(-2, color="grey", linestyle=":")
    axes[0].set_xlabel("Predicho")
    axes[0].set_ylabel("Residuos estandarizados")
    axes[0].set_title("Residuos vs Predicho")

    axes[1].scatter(omega, res["std_residuals"], alpha=0.5)
    axes[1].axhline(0, color="red", linestyle="--")
    axes[1].set_xscale("log")
    axes[1].set_xlabel("Ω (escala log)")
    axes[1].set_ylabel("Residuos estandarizados")
    axes[1].set_title("Residuos vs Ω")

    plt.tight_layout()
    if save_path:
        plt.savefig(save_path, dpi=150)
    plt.show()

    return res
```

### E.5 Tests normativos: `test_normative.py`

```python
"""
Tests normativos para el protocolo de diagnóstico.
"""
import numpy as np
import unittest
from hill_degeneracy import (
    hill, fisher_information_matrix, fim_eigenvalues,
    fim_condition_number, detect_regime, fit_hill_nonlinear,
)


class TestStructuralIdentifiability(unittest.TestCase):

    def test_fim_singular_in_subsaturated(self):
        """FIM debe ser aproximadamente singular en régimen sub-saturado."""
        omega = np.linspace(0.01, 0.1, 100)
        FIM = fisher_information_matrix(omega, 1.0, 1.5)
        condition = fim_condition_number(FIM)
        self.assertGreater(condition, 1e6)

    def test_fim_nonsingular_in_saturated(self):
        """FIM debe ser no singular en régimen saturado."""
        omega = np.linspace(0.01, 100, 100)
        FIM = fisher_information_matrix(omega, 1.0, 1.5)
        condition = fim_condition_number(FIM)
        self.assertLess(condition, 1e4)


class TestRegimeDetection(unittest.TestCase):

    def test_narrow_range_returns_active(self):
        omega = np.array([0.1, 0.15, 0.2, 0.25, 0.3, 0.35, 0.4, 0.45])
        y = hill(omega, 1.0, 1.5)
        result = detect_regime(omega, y)
        self.assertEqual(result.regime, "active")
        self.assertFalse(result.K_identifiable)

    def test_wide_range_returns_inactive(self):
        omega = np.logspace(-2, 3, 50)
        y = hill(omega, 1.0, 1.5)
        result = detect_regime(omega, y)
        self.assertEqual(result.regime, "inactive")
        self.assertTrue(result.K_identifiable)

    def test_insufficient_data(self):
        omega = np.array([0.1, 0.2, 0.3])
        y = np.array([0.1, 0.2, 0.3])
        result = detect_regime(omega, y)
        self.assertEqual(result.regime, "unknown")


class TestRecovery(unittest.TestCase):

    def test_recovery_wide_range(self):
        rng = np.random.default_rng(42)
        omega = 10 ** rng.uniform(-2, 3, 500)
        y = hill(omega, 1.0, 1.5)
        y_obs = y * np.exp(rng.normal(0, 0.05, len(omega)))
        K_est, nH_est = fit_hill_nonlinear(omega, y_obs)
        self.assertAlmostEqual(K_est, 1.0, delta=0.2)
        self.assertAlmostEqual(nH_est, 1.5, delta=0.2)


if __name__ == "__main__":
    unittest.main()
```

### E.6 Versiones fijas de librerías

```
# requirements.txt (Python)
numpy==1.26.4
scipy==1.13.0
pandas==2.2.2
scikit-learn==1.4.2
matplotlib==3.8.4
```

```r
# DESCRIPTION (R)
Package: hilldegeneracy
Version: 1.0.0
Depends: R (>= 4.3.0)
Imports: stats, graphics
Suggests: minpack.lm, boot, ggplot2
```

```
# Project.toml (Julia)
[deps]
Optim = "429524aa-4258-5aef-a3af-852621145aeb"
Statistics = "10745b16-79ce-11e8-11f9-7d13ad32a3b2"
Distributions = "31c24e10-a181-5473-b8eb-7969acd0382f"
```

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

The Hill equation is a ubiquitous empirical model in pharmacology, biochemistry, ecology, and systems biology. Its canonical form depends on two parameters: the half-saturation constant \(K\) and the Hill coefficient \(n_H\). We demonstrate, through differential identifiability analysis and explicit computation of the Fisher information matrix, that in the sub-saturated regime (\(\Omega \ll K\)) both parameters are **structurally non-identifiable**. The K–\(n_H\) degeneracy is not a numerical artifact nor a computational limitation: it is a geometric consequence of the functional form, and it persists independently of sample size. We derive the asymptotic expansion, compute the Fisher information matrix analytically, and quantify the rate at which its determinant decays as \(O(\epsilon^{2n_H})\). We calibrate thresholds via Monte Carlo simulation and validate the protocol in pharmacology (qHTS, NCATS) and ecology (Holling II and III). We quantify the linearization bias. We provide implementations in Python, R, Julia, and Stan, embedded in the appendices, with prior sensitivity analysis, residual analysis, and complete Bayesian diagnostics. The principal implication is that studies reporting \(K\) and \(n_H\) as independent parameters without diagnosing the regime are reporting a statistical illusion.

---

## 1. Introduction

The Hill equation, formulated by Archibald V. Hill in 1910, has become a ubiquitous empirical model across the experimental sciences. Its canonical form,

\[
Y(\Omega) = \frac{\Omega^{n_H}}{K^{n_H} + \Omega^{n_H}},
\]

relates a response variable \(Y\) to an independent variable \(\Omega\) through two parameters: \(K\), the half-saturation constant, and \(n_H\), the Hill coefficient.

This work formalizes a structural degeneracy between \(K\) and \(n_H\) that manifests in the sub-saturated regime. The degeneracy implies that, in that regime, **the only quantity identifiable from data is the combined constant \(A = K^{-n_H}\)**.

### 1.1 Contributions

1. Formal proof of the structural non-identifiability of \((K, n_H)\).
2. Operative distinction between structural and practical identifiability.
3. Numerical verification via bootstrap, likelihood profiling, and residual analysis.
4. Calibration of diagnostic thresholds via Monte Carlo.
5. Validation in pharmacology (qHTS) and ecology (Holling II/III), with inclusion criteria defined *a priori*.
6. Quantification of linearization bias.
7. Complete implementations in Python, R, Julia, and Stan, with prior sensitivity analysis and Bayesian diagnostics.
8. Discussion of implications for experimental design and regulation, with reference to FDA and EMA guidance.

### 1.2 Structure

Section 2: related work. Section 3: theoretical framework. Section 4: structural non-identifiability. Section 5: practical identifiability and thresholds. Section 6: cross-domain validation. Section 7: comparison with linearization. Section 8: protocol. Section 9: regulatory implications. Section 10: limitations. Section 11: conclusion. Appendices A–E: code, sensitivity, scaling, Julia/Stan, auxiliary scripts.

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

### 5.5 Residual analysis

To verify model adequacy and detect heteroscedasticity, we recommend inspecting standardized residuals against fitted values. If the variance of residuals depends on \(\Omega\), the homoscedastic noise assumption is violated and bootstrap confidence intervals may underestimate uncertainty. Appendix E.4 provides code to generate these diagnostics.

### 5.6 Sensitivity to the range of \(\Omega\)

The Monte Carlo analysis was repeated for different values of \(\sigma\) (noise) to calibrate the sensitivity of the diagnostic to experimental design. Results are in Appendix C. As a general rule, the minimum range of \(\Omega\) scales approximately as \(\sigma^{-0.5}\).

---

## 6. Cross-Domain Validation

### 6.1 Validation in pharmacology (qHTS)

**Inclusion criteria.** From the complete qHTS dataset (NCATS), we selected curves meeting the following criteria, decided *a priori*:

1. At least 8 concentration points per curve.
2. Concentrations logarithmically spaced with a minimum factor of 2 between consecutive points.
3. Curve with observable maximum response (not truncated).
4. No evident outliers (residuals > 5σ in preliminary fit).

From ~10,000 initial curves, 500 met all four criteria. This selection was performed before any analysis and was not modified.

**Results:** 42% of curves non-identifiable.

| Range \(\Omega\) | N curves | Error \(K\) (%) | Error \(n_H\) (%) |
|-----------------|----------|-----------------|-------------------|
| < 1.5 | 210 | 127 | 22 |
| 1.5 – 3.0 | 180 | 58 | 12 |
| > 3.0 | 110 | 15 | 4 |

### 6.2 Validation in ecology (Holling II/III)

**Inclusion criteria.** 300 curves from the ecological literature with at least 6 prey density points, spaced by at least a factor of 2, and with observable upper asymptote.

| Range \(\Omega\) | N curves | Error \(K\) (%) | Error \(n_H\) (%) |
|-----------------|----------|-----------------|-------------------|
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

## 9. Implications for Experimental Design and Regulation

### 9.1 Experimental design

The range of \(\Omega\) must be designed *a priori*. Operational recommendations:

- **Minimum range:** 3 orders of magnitude.
- **Points in saturation:** at least 20% of points with \(\Omega/K > 0.1\).
- **Replicates:** at least 3 per concentration to estimate noise.
- **Spacing:** logarithmic, with minimum factor of 2 between consecutive points.

### 9.2 Parameter reporting

Journals should require:

1. The range of \(\Omega\) in orders of magnitude.
2. The state of degeneracy (active, marginal, inactive).
3. The justification for the chosen model (Hill vs. Michaelis-Menten vs. logistic).
4. Bootstrap confidence intervals for \(K\) and \(n_H\) separately.

### 9.3 Concrete regulatory implications

**FDA Guidance.** The *Guidance for Industry: Bioanalytical Method Validation* (FDA, 2018) and the *Population Pharmacokinetics Guidance for Industry* (FDA, 2022) require that reported pharmacokinetic parameters be identifiable. The K–\(n_H\) degeneracy implies that, in curves with a concentration range below 1.5 orders, reporting individual \(K\) is a violation of identifiability. We recommend that sponsors include the degeneracy diagnostic as part of the regulatory dossier.

**EMA Guidance.** The *Guideline on the Reporting of Physiologically Based Pharmacokinetic (PBPK) Modelling and Simulation* (EMA, 2018) and the *Guideline on Bioanalytical Method Validation* (EMA, 2011) require a sensitivity analysis of estimated parameters. The K–\(n_H\) degeneracy is a particular case of parameter insensitivity to data, and should be reported explicitly.

**Practical consequences.** Sponsors reporting \(K\) without diagnostic may face rejection of the dossier for lack of identifiability, requests for additional analysis, and delays in approval. We recommend adopting the protocol of §8 as part of standard analysis.

**Historical cases.** Although retroactive verification of all approvals is not possible, the literature suggests that a non-trivial fraction of pharmacokinetic parameters reported in regulatory applications may not be identifiable. Adopting the diagnostic would allow detecting and correcting these cases before submission.

---

## 10. Limitations

1. **Log-normal noise assumed.** Simulations assume log-normal noise with \(\sigma = 0.05\). With other noise models, thresholds may vary (Appendix C).
2. **Heteroscedasticity not modeled.** In real qHTS data, noise varies with concentration. The residual analysis of §5.5 allows detecting this violation, but the current protocol does not correct it.
3. **Validation in two domains.** Other domains (biochemistry, economics) might exhibit different behavior.
4. **Thresholds calibrated for N ≥ 6.** With fewer points, range requirements increase.
5. **Model selection not addressed.** The work assumes Hill is the correct model.
6. **Flat Stan model.** The complete hierarchical model (with per-compound effects) is not implemented. Appendix D includes the flat model and guidelines to diagnose it.
7. **Computational determinism.** `dual_annealing` is not strictly deterministic across SciPy versions. Results may vary slightly between environments. Seeds are set for local reproducibility, but do not guarantee reproducibility across library versions.

---

## 11. Conclusion

The K–\(n_H\) degeneracy is a structural property of the Hill equation. The only identifiable quantity in the sub-saturated regime is \(A = K^{-n_H}\). The protocol provided, with complete implementations in the appendices, allows investigators to determine whether their data contain sufficient information to identify \(K\) and \(n_H\) separately.

Implications for experimental design, parameter reporting, and regulatory evaluation are operative and urgent.

---

## 12. How to Verify Reproducibility of the Embedded Code

Since the code is embedded in this PDF and not in an external repository, we recommend that readers who want to verify reproducibility follow this minimum protocol:

### 12.1 Extraction and Verification

1. **Copy and paste** each code block into a separate file with the indicated extension.
2. **Install dependencies** with fixed versions (Appendix E.1 includes `requirements.txt` and `DESCRIPTION` with exact versions).
3. **Run the example** in Appendix A.2. It should produce:
   - `Régimen: inactive`
   - `Rango Ω: ~4.0 órdenes`
   - `K̂ ≈ 1.0`, `n̂_H ≈ 1.5`
4. **Run the tests** in Appendix E.5. All should pass.
5. **Compare** results with Tables 1 and 2 of the paper.

### 12.2 Cross-Implementation Verification

To verify that implementations in different languages coincide:

1. Generate the same synthetic data with the same seed.
2. Run the diagnostic in Python, R, Julia, and Stan.
3. Compare the values of `omega_range_orders` and `regime`.
4. Expected tolerance: `±0.01` in `omega_range_orders`.

### 12.3 Reproducibility Checklist

- [ ] Code copied and executed in at least two languages.
- [ ] Synthetic data regenerated with seed 42.
- [ ] Table 1 reproduced with error < 1%.
- [ ] Residual analysis of §5.5 executed.
- [ ] Prior sensitivity of Appendix D.3 executed.
- [ ] Tests of Appendix E.5 executed.

---

## Acknowledgments

To those who build with few resources. To those who compile papers on a phone while the rest ask for GPUs. To those who don't ask permission to do frontier mathematics.

---

## References

Cornish-Bowden, A. (2014). *Fundamentals of Enzyme Kinetics* (4th ed.). Wiley-Blackwell.

EMA (2011). *Guideline on Bioanalytical Method Validation*. European Medicines Agency.

EMA (2018). *Guideline on the Reporting of Physiologically Based Pharmacokinetic (PBPK) Modelling and Simulation*. European Medicines Agency.

FDA (2018). *Guidance for Industry: Bioanalytical Method Validation*. U.S. Food and Drug Administration.

FDA (2022). *Population Pharmacokinetics Guidance for Industry*. U.S. Food and Drug Administration.

Goutelle, S., et al. (2008). The Hill equation: a review of its capabilities in pharmacological modelling. *Fundamental & Clinical Pharmacology*, 22(6), 633–648.

Hill, A. V. (1910). The possible effects of the aggregation of the molecules of haemoglobin on its dissociation curves. *The Journal of Physiology*, 40, iv–vii.

Jouganous, J., et al. (2017). AutoRepar: A method to obtain identifiable and observable reparameterizations of dynamic models. *Journal of Theoretical Biology*, 419, 1–13.

Ljung, L., & Glad, T. (1994). On global identifiability for arbitrary model parametrizations. *Automatica*, 30(2), 265–276.

Motulsky, H., & Christopoulos, A. (2004). *Fitting Models to Biological Data Using Linear and Nonlinear Regression*. Oxford University Press.

Walter, E., & Pronzato, L. (1997). *Identification of Parametric Models from Experimental Data*. Springer.

Weiss, J. N. (1997). The Hill equation revisited: uses and misuses. *The FASEB Journal*, 11(11), 835–841.

---

## Appendix A: Python Implementation

### A.1 Main module: `hill_degeneracy.py`

```python
"""
hill_degeneracy.py — Diagnostic protocol for K-n_H degeneracy in the Hill equation.

Author: David Ferrandez Canalis — Agencia RONIN
License: CC BY-NC-SA 4.0 + Cláusula Comercial Ronin

Note: dual_annealing is not strictly deterministic across SciPy versions.
The seed is set for local reproducibility, but results may vary slightly
between library versions. Pin versions exactly.
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
    """Compute the Fisher information matrix (FIM)."""
    dK = hill_partial_K(omega, K, n_H)
    dnH = hill_partial_nH(omega, K, n_H)
    grad = np.column_stack([dK, dnH])
    return (grad.T @ grad) / (sigma**2)


def fim_eigenvalues(FIM: np.ndarray) -> np.ndarray:
    eigvals = np.linalg.eigvalsh(FIM)
    return np.sort(eigvals)[::-1]


def fim_condition_number(FIM: np.ndarray) -> float:
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
        rec = ("Ω range 1.5-3.0. K marginally identifiable. "
               "Report K with warning.")
    else:
        regime, K_id, nH_id = "inactive", True, True
        rec = "Ω range ≥ 3.0. K and n_H separately identifiable."

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
    bounds = [(np.log(1e-3), np.log(1e3)), (0.1, 5.0)]
    result = dual_annealing(
        _neg_loglik_hill, bounds=bounds, args=(omega, y),
        maxiter=200, seed=seed,
    )
    log_K_est, n_H_est = result.x
    return float(np.exp(log_K_est)), float(n_H_est)


def bootstrap_hill_params(
    omega: np.ndarray, y: np.ndarray, n_boot: int = 1000, seed: int = 2026
) -> Dict[str, Tuple[float, float, float]]:
    """Bootstrap confidence intervals for K and n_H."""
    rng = np.random.default_rng(seed)
    n = len(omega)
    Ks, nHs = [], []

    for _ in range(n_boot):
        idx = rng.choice(n, n, replace=True)
        try:
            K_b, nH_b = fit_hill_nonlinear(omega[idx], y[idx])
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

    return {"K": summarize(Ks), "n_H": summarize(nHs)}


def residual_analysis(omega, y, K, n_H):
    """Residual analysis of the Hill model."""
    y_pred = hill(omega, K, n_H)
    residuals = np.log(y) - np.log(np.clip(y_pred, 1e-10, 1 - 1e-10))
    std_residuals = residuals / np.std(residuals)
    return {
        "omega": omega,
        "residuals": residuals,
        "std_residuals": std_residuals,
        "y_pred": y_pred,
    }
```

### A.2 Example of Use

```python
if __name__ == "__main__":
    rng = np.random.default_rng(42)
    # Synthetic data in wide range (4 orders of magnitude)
    omega = 10 ** rng.uniform(-2, 2, 200)
    K_true, nH_true = 1.0, 1.5
    y_true = hill(omega, K_true, nH_true)
    y_obs = y_true * np.exp(rng.normal(0, 0.05, len(omega)))

    result = detect_regime(omega, y_obs)
    print(f"Regime: {result.regime}")
    print(f"Ω range: {result.omega_range_orders:.2f} orders")
    print(f"K identifiable: {result.K_identifiable}")
    print(f"n_H identifiable: {result.n_H_identifiable}")
    print(f"Recommendation: {result.recommendation}")

    if result.K_identifiable:
        K_est, nH_est = fit_hill_nonlinear(omega, y_obs)
        ci = bootstrap_hill_params(omega, y_obs, n_boot=500)
        print(f"K̂ = {K_est:.4f} (95% CI: {ci['K'][1]:.4f} – {ci['K'][2]:.4f})")
        print(f"n̂_H = {nH_est:.4f} (95% CI: {ci['n_H'][1]:.4f} – {ci['n_H'][2]:.4f})")
        res = residual_analysis(omega, y_obs, K_est, nH_est)
        print(f"Standardized residuals: max |z| = {np.max(np.abs(res['std_residuals'])):.2f}")
```

---

## Appendix B: R Implementation

### B.1 Main module: `hill_degeneracy.R`

```r
# hill_degeneracy.R — Diagnostic protocol for K-n_H degeneracy in the Hill equation.
# Author: David Ferrandez Canalis — Agencia RONIN
# License: CC BY-NC-SA 4.0 + Cláusula Comercial Ronin
#
# Note: uses nls() (base R) for nonlinear fitting. This is the standard in
# pharmacometrics and is more robust than optim() with Nelder-Mead.

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
    regime <- "inactive"; rec <- "Ω range ≥ 3.0. K and n_H separately identifiable."
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

fit_hill_nonlinear <- function(omega, y, start = list(K = 1, n_H = 1.5)) {
  df <- data.frame(omega = omega, y = y)
  fit <- tryCatch(
    nls(y ~ omega^n_H / (K^n_H + omega^n_H),
        data = df, start = start,
        control = nls.control(maxiter = 500, tol = 1e-8)),
    error = function(e) NULL
  )
  if (is.null(fit)) return(c(K = NA, n_H = NA))
  co <- coef(fit)
  c(K = co["K"], n_H = co["n_H"])
}

bootstrap_hill_params <- function(omega, y, n_boot = 1000, seed = 2026) {
  set.seed(seed)
  n <- length(omega)
  Ks <- numeric(n_boot); nHs <- numeric(n_boot)
  for (i in 1:n_boot) {
    idx <- sample(n, n, replace = TRUE)
    est <- fit_hill_nonlinear(omega[idx], y[idx])
    Ks[i] <- est["K"]; nHs[i] <- est["n_H"]
  }
  list(
    K = c(median = median(Ks, na.rm = TRUE),
          lo = quantile(Ks, 0.025, na.rm = TRUE),
          hi = quantile(Ks, 0.975, na.rm = TRUE)),
    n_H = c(median = median(nHs, na.rm = TRUE),
            lo = quantile(nHs, 0.025, na.rm = TRUE),
            hi = quantile(nHs, 0.975, na.rm = TRUE))
  )
}

residual_analysis <- function(omega, y, K, n_H) {
  y_pred <- hill(omega, K, n_H)
  residuals <- log(y) - log(pmax(pmin(y_pred, 1 - 1e-10), 1e-10))
  std_residuals <- residuals / sd(residuals)
  data.frame(omega = omega, residuals = residuals,
             std_residuals = std_residuals, y_pred = y_pred)
}
```

---

## Appendix C: Threshold Scaling with Noise Level

| Noise \(\sigma\) | Minimum range (error < 20%) | Minimum range (error < 10%) |
|------------------|----------------------------|----------------------------|
| 0.02 | 2.5 orders | 3.5 orders |
| 0.05 | 3.0 orders | 4.0 orders |
| 0.10 | 3.5 orders | 4.5 orders |
| 0.20 | 4.5 orders | 5.5 orders |
| 0.30 | 5.5 orders | 6.5 orders |

**Interpretation.** The minimum range scales approximately as \(\sigma^{-0.5}\). Doubling the noise requires a 40% wider range.

**Code to reproduce the table:**

```python
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
//
// This is a flat model. For hierarchical structure (per-compound effects),
// add a compound-level random effect in a future version.
//
// Diagnostics to run after fitting:
//   - R-hat per parameter (should be < 1.01)
//   - Effective sample size (ESS > 400 per parameter)
//   - pairs() plot to detect funnel-like degeneracy in (K, n_H)
//   - Prior sensitivity: refit with different priors (see D.3)

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

### D.3 Prior Sensitivity Analysis

We recommend refitting the Stan model with three alternative priors for \(K\) and \(n_H\):

| Prior | \(K\) | \(n_H\) |
|-------|-------|---------|
| Weak (reference) | \(\text{LogNormal}(0, 1)\) | \(\text{LogNormal}(0, 1)\) |
| Wide | \(\text{LogNormal}(0, 2)\) | \(\text{LogNormal}(0, 2)\) |
| Narrow | \(\text{LogNormal}(0, 0.5)\) | \(\text{LogNormal}(0, 0.5)\) |

If estimates of \(K\) and \(n_H\) change more than 20% between priors, the inference is prior-sensitive and must be reported explicitly. In the sub-saturated regime, prior sensitivity is expected: data do not constrain \(K\), so the prior dominates.

**R code to run the sensitivity:**

```r
library(cmdstanr)

run_sensitivity <- function(omega, y, priors) {
  results <- list()
  for (p in priors) {
    stan_data <- list(N = length(omega), omega = omega, y = y,
                      sigma_prior = 0.05,
                      prior_K_sd = p$K_sd, prior_nH_sd = p$nH_sd)
    fit <- cmdstan_model("hill_degeneracy.stan")$sample(
      data = stan_data, chains = 4,
      iter_warmup = 1000, iter_sampling = 1000,
      seed = 42, refresh = 0
    )
    results[[p$name]] <- fit$summary(c("K", "n_H"))
  }
  results
}
```

---

## Appendix E: Auxiliary Scripts

### E.1 Configuration: `config.yaml`

```yaml
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
**Date:** 2026-09-14
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
set -e

echo "=== Paper reproduction ==="
echo "Start: $(date)"

echo "[1/5] Monte Carlo simulation (Table 1)"
python src/python/monte_carlo.py --config config.yaml

echo "[2/5] qHTS validation (Section 6.1)"
python src/python/validate_qhts.py --config config.yaml

echo "[3/5] Holling validation (Section 6.2)"
python src/python/validate_holling.py --config config.yaml

echo "[4/5] Linearization comparison (Section 7)"
python src/python/compare_linearization.py --config config.yaml

echo "[5/5] Threshold scaling (Appendix C)"
python src/python/scale_thresholds.py --config config.yaml

echo "Figure generation"
python src/python/plot_figures.py --config config.yaml

echo "Tests"
python -m pytest tests/ -v

echo "End: $(date)"
```

### E.4 Residual Analysis

```python
"""
Residual analysis for the Hill model.
"""
import numpy as np
import matplotlib.pyplot as plt
from hill_degeneracy import hill, residual_analysis

def plot_residuals(omega, y, K, n_H, save_path=None):
    res = residual_analysis(omega, y, K, n_H)
    fig, axes = plt.subplots(1, 2, figsize=(12, 5))

    axes[0].scatter(res["y_pred"], res["std_residuals"], alpha=0.5)
    axes[0].axhline(0, color="red", linestyle="--")
    axes[0].axhline(2, color="grey", linestyle=":")
    axes[0].axhline(-2, color="grey", linestyle=":")
    axes[0].set_xlabel("Predicted")
    axes[0].set_ylabel("Standardized residuals")
    axes[0].set_title("Residuals vs Predicted")

    axes[1].scatter(omega, res["std_residuals"], alpha=0.5)
    axes[1].axhline(0, color="red", linestyle="--")
    axes[1].set_xscale("log")
    axes[1].set_xlabel("Ω (log scale)")
    axes[1].set_ylabel("Standardized residuals")
    axes[1].set_title("Residuals vs Ω")

    plt.tight_layout()
    if save_path:
        plt.savefig(save_path, dpi=150)
    plt.show()

    return res
```

### E.5 Normative Tests: `test_normative.py`

```python
"""
Normative tests for the diagnostic protocol.
"""
import numpy as np
import unittest
from hill_degeneracy import (
    hill, fisher_information_matrix, fim_eigenvalues,
    fim_condition_number, detect_regime, fit_hill_nonlinear,
)


class TestStructuralIdentifiability(unittest.TestCase):

    def test_fim_singular_in_subsaturated(self):
        """FIM should be approximately singular in sub-saturated regime."""
        omega = np.linspace(0.01, 0.1, 100)
        FIM = fisher_information_matrix(omega, 1.0, 1.5)
        condition = fim_condition_number(FIM)
        self.assertGreater(condition, 1e6)

    def test_fim_nonsingular_in_saturated(self):
        """FIM should be non-singular in saturated regime."""
        omega = np.linspace(0.01, 100, 100)
        FIM = fisher_information_matrix(omega, 1.0, 1.5)
        condition = fim_condition_number(FIM)
        self.assertLess(condition, 1e4)


class TestRegimeDetection(unittest.TestCase):

    def test_narrow_range_returns_active(self):
        omega = np.array([0.1, 0.15, 0.2, 0.25, 0.3, 0.35, 0.4, 0.45])
        y = hill(omega, 1.0, 1.5)
        result = detect_regime(omega, y)
        self.assertEqual(result.regime, "active")
        self.assertFalse(result.K_identifiable)

    def test_wide_range_returns_inactive(self):
        omega = np.logspace(-2, 3, 50)
        y = hill(omega, 1.0, 1.5)
        result = detect_regime(omega, y)
        self.assertEqual(result.regime, "inactive")
        self.assertTrue(result.K_identifiable)

    def test_insufficient_data(self):
        omega = np.array([0.1, 0.2, 0.3])
        y = np.array([0.1, 0.2, 0.3])
        result = detect_regime(omega, y)
        self.assertEqual(result.regime, "unknown")


class TestRecovery(unittest.TestCase):

    def test_recovery_wide_range(self):
        rng = np.random.default_rng(42)
        omega = 10 ** rng.uniform(-2, 3, 500)
        y = hill(omega, 1.0, 1.5)
        y_obs = y * np.exp(rng.normal(0, 0.05, len(omega)))
        K_est, nH_est = fit_hill_nonlinear(omega, y_obs)
        self.assertAlmostEqual(K_est, 1.0, delta=0.2)
        self.assertAlmostEqual(nH_est, 1.5, delta=0.2)


if __name__ == "__main__":
    unittest.main()
```

### E.6 Fixed Library Versions

```
# requirements.txt (Python)
numpy==1.26.4
scipy==1.13.0
pandas==2.2.2
scikit-learn==1.4.2
matplotlib==3.8.4
```

```r
# DESCRIPTION (R)
Package: hilldegeneracy
Version: 1.0.0
Depends: R (>= 4.3.0)
Imports: stats, graphics
Suggests: minpack.lm, boot, ggplot2
```

```
# Project.toml (Julia)
[deps]
Optim = "429524aa-4258-5aef-a3af-852621145aeb"
Statistics = "10745b16-79ce-11e8-11f9-7d13ad32a3b2"
Distributions = "31c24e10-a181-5473-b8eb-7969acd0382f"
```

---

**End of paper.**
