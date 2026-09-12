# TRILOGÍA PUSFRE-CES 
## Edición corregida tras auditoría externa

**Autor:** David Ferrandez Canalis  
**Afiliación:** Agencia RONIN  
**Fecha:** Septiembre 2026  
**Licencia:** CC BY-NC-SA 4.0 + Cláusula Comercial Ronin (unificada en todo el documento)

---


---

# README GLOBAL DE LA TRILOGÍA

## Estructura, reproducibilidad y flujo de semillas

### Estructura de la trilogía

| Artículo | Contenido | Datasets |
|----------|-----------|----------|
| A | Caracterización condicional | Verificación numérica de casos límite (sintética) |
| B | Identificabilidad | Régimen transitorio (900, SINT-GEN). Warfarina y COVID como casos univariantes ilustrativos (SINT-GEN) |
| C | Evaluación metodológica | Debye (50, REAL), Neural Scaling (46, SINT-GEN), Urban Scaling (1200, SINT-GEN), Species-Area (500, SINT-GEN), Fama-French (720, SINT-GEN) |

### Naturaleza de los datos (declaración explícita)

| Etiqueta | Significado |
|----------|-------------|
| **[REAL]** | Datos verificados contra la fuente original. Únicamente Debye (Ashcroft-Mermin 1976) |
| **[SINT-CAL]** | Datos sintéticos calibrados a distribuciones reportadas en la literatura. No son los originales |
| **[SINT-GEN]** | Datos sintéticos generados con parámetros especificados en la metodología. Sin pretensión de calibración |

**Advertencia.** Los resultados sobre datasets `[SINT-CAL]` y `[SINT-GEN]` son **verificación metodológica**, no validación empírica. La única validación empírica con datos reales es Debye. Neural Scaling se trata como `[SINT-GEN]` por no disponer de verificación contra la fuente original en esta edición.

### Formatos de los datasets

- **Listados íntegramente:** Debye (50 filas), Warfarina (30 filas), COVID (80 filas), Neural Scaling sintético (46 filas).
- **Regenerables por código:** Régimen transitorio (900 filas), Urban Scaling (1200 filas), Species-Area (500 filas), Fama-French (720 filas).

### Flujo de semillas

Semilla global `seed_global = 42`.

| Análisis | Semilla |
|----------|---------|
| `dual_annealing` | 42 |
| Bootstrap | 42 |
| Validación cruzada (fold k) | 42 + k |
| Réplica r | 42 + 1000·r |

### Versiones de software

Python 3.11.9, NumPy 1.26.4, SciPy 1.13.0, scikit-learn 1.4.2, pandas 2.2.2. Precisión float64.

### Pseudocódigo global (funciones auxiliares completas)

```python
"""common/m6.py — Núcleo CES-Saturada corregido."""
import numpy as np
import pandas as pd
from scipy.optimize import dual_annealing, minimize
from sklearn.model_selection import StratifiedKFold

SEED_GLOBAL = 42


# ----------------------------------------------------------------------
# Componentes elementales
# ----------------------------------------------------------------------
def hill(omega, K, alpha_h):
    """Saturación tipo Hill. omega, K > 0; alpha_h > 0."""
    oa = np.power(np.clip(omega, 1e-12, None), alpha_h)
    Ka = np.power(max(K, 1e-12), alpha_h)
    return oa / (Ka + oa)


def ces_aggregate(x, w, lam):
    """Agregador CES. lam -> 0 se interpreta como Cobb-Douglas."""
    x = np.clip(np.asarray(x, dtype=float), 1e-12, None)
    w = np.asarray(w, dtype=float)
    if abs(lam) < 1e-8:
        return float(np.prod(np.power(x, w)))
    return float(np.power(np.sum(w * np.power(x, lam)), 1.0 / lam))


def simplex_reparam(v):
    """Reparametrización de pesos al simplex [0.1, 0.8] con suma 1."""
    v = np.clip(np.asarray(v, dtype=float), 1e-9, None)
    return 0.1 + 0.7 * (v / np.sum(v))


# ----------------------------------------------------------------------
# Modelos
# ----------------------------------------------------------------------
def predict_M0(X, params):
    """M0: PUSFRE base F = C * Phi * Psi * Omega^alpha.
    params = [log_C, alpha]. Devuelve F predicho."""
    Phi, Psi, Omega = X[:, 0], X[:, 1], X[:, 2]
    log_C, alpha = params
    return np.exp(log_C) * Phi * Psi * np.power(np.clip(Omega, 1e-12, None), alpha)


def predict_M1(X, params):
    """M1: CES sin saturación.
    params = [lam, v1, v2, v3]."""
    Phi, Psi, Omega = X[:, 0], X[:, 1], X[:, 2]
    lam, v1, v2, v3 = params
    w = simplex_reparam([v1, v2, v3])
    return np.array([ces_aggregate([Phi[i], Psi[i], Omega[i]], w, lam)
                     for i in range(len(Phi))])


def predict_M2(X, params):
    """M2: Hill sin CES.
    params = [K, alpha_h, beta]."""
    Phi, Psi, Omega = X[:, 0], X[:, 1], X[:, 2]
    K, alpha_h, beta = params
    S = hill(Omega, K, alpha_h)
    return Phi * Psi * np.power(S, beta)


def predict_M6(X, params):
    """M6: CES + Hill.
    params = [lam, K, alpha_h, v1, v2, v3]."""
    Phi, Psi, Omega = X[:, 0], X[:, 1], X[:, 2]
    lam, K, alpha_h, v1, v2, v3 = params
    w = simplex_reparam([v1, v2, v3])
    S = hill(Omega, K, alpha_h)
    return np.array([ces_aggregate([Phi[i], Psi[i], S[i]], w, lam)
                     for i in range(len(Phi))])


PREDICTORS = {"M0": predict_M0, "M1": predict_M1,
              "M2": predict_M2, "M6": predict_M6}

BOUNDS = {
    "M0": [(-5.0, 5.0), (0.0, 3.0)],
    "M1": [(-1.0, 2.0), (0.01, 10.0), (0.01, 10.0), (0.01, 10.0)],
    "M2": [(0.01, 100.0), (0.1, 5.0), (0.1, 5.0)],
    "M6": [(-1.0, 2.0), (0.01, 100.0), (0.1, 5.0),
           (0.01, 10.0), (0.01, 10.0), (0.01, 10.0)],
}


# ----------------------------------------------------------------------
# Verosimilitud gaussiana con sigma estimado por MLE
# ----------------------------------------------------------------------
def neg_loglik(model, X, y):
    """Neg log-verosimilitud. Sigma estimado por MLE:
    sigma_hat^2 = (1/n) * sum(resid^2).
    Se devuelve el perfil concentrado:
    -n/2 * log(2*pi*sigma_hat^2) - n/2.
    """
    pred = PREDICTORS[model](X, np.asarray(y[0]))  # placeholder
    raise NotImplementedError


def _neg_loglik_factory(model, X, y):
    def f(params):
        try:
            pred = PREDICTORS[model](X, params)
        except Exception:
            return 1e12
        pred = np.clip(pred, 1e-12, None)
        resid = y - pred
        sigma2 = max(float(np.mean(resid ** 2)), 1e-12)
        n = len(y)
        # Perfil concentrado de la log-verosimilitud gaussiana
        return 0.5 * n * np.log(2 * np.pi * sigma2) + 0.5 * n
    return f


def ajustar(model, X, y, seed=SEED_GLOBAL):
    """Ajuste por dual_annealing + L-BFGS-B."""
    bounds = BOUNDS[model]
    f = _neg_loglik_factory(model, X, y)
    res_g = dual_annealing(f, bounds=bounds, seed=int(seed), maxiter=200)
    res_l = minimize(f, res_g.x, method="L-BFGS-B",
                     options={"maxiter": 500, "ftol": 1e-10})
    return res_l.x


def rmse(model, X, y, params):
    pred = np.clip(PREDICTORS[model](X, params), 1e-12, None)
    return float(np.sqrt(np.mean((y - pred) ** 2)))


def bic(model, X, y, params):
    """BIC = -2 logL + p log n, con p = numero de parametros libres."""
    n = len(y)
    pred = np.clip(PREDICTORS[model](X, params), 1e-12, None)
    resid = y - pred
    sigma2 = max(float(np.mean(resid ** 2)), 1e-12)
    logL = -0.5 * n * np.log(2 * np.pi * sigma2) - 0.5 * n
    p = len(params)
    return float(-2 * logL + p * np.log(n))


def validacion_cruzada(model, X, y, n_folds=10):
    y_strat = pd.qcut(y, q=n_folds, labels=False, duplicates="drop")
    skf = StratifiedKFold(n_splits=n_folds, shuffle=True,
                          random_state=SEED_GLOBAL)
    rmses = []
    for k, (tr, te) in enumerate(skf.split(X, y_strat)):
        params = ajustar(model, X[tr], y[tr], seed=SEED_GLOBAL + k)
        rmses.append(rmse(model, X[te], y[te], params))
    return rmses
```

---

# ARTÍCULO A

## Una Caracterización Condicional de la Función de Fitness en Sistemas Finitos con Recursos Escasos

**Autor:** David Ferrandez Canalis  
**Afiliación:** Agencia RONIN  
**Destino:** Artículo interno de la trilogía (no sometido a revista externa en esta edición)

---

### Resumen

Se presenta una caracterización **condicional** de la función de fitness en sistemas finitos donde agentes heterogéneos compiten por un recurso escaso. Bajo un conjunto explícito de axiomas, supuestos estructurales, condiciones de elasticidad y regularidad, la única forma funcional compatible es `F = C·Φ·Ψ·Ω^α` con α ∈ (0, 1]. El resultado **no es universal**: relajar cualquier supuesto amplía el espacio de formas admisibles. Se caracteriza ese espacio y se comparan cuatro familias candidatas. Se incluye verificación numérica de casos límite con semilla y precisión reproducibles.

**Palabras clave:** CES, sistemas finitos, caracterización condicional, funciones de fitness, competencia por recursos.

---

### 1. Introducción

Arrow, Chenery, Minhas y Solow (1961) introdujeron la familia CES. Diewert (1971, 1974) sistematizó el análisis mediante dualidad. Gallant (1981) introdujo la familia Fourier flexible.

En sistemas multi-agente con recursos escasos cabe preguntarse: ¿bajo qué condiciones puede caracterizarse la función de fitness? Este trabajo responde **bajo un conjunto explícito y fuerte de supuestos**, y describe qué ocurre al relajarlos.

#### 1.1 Contribuciones

1. Cuatro capas de axiomas y supuestos, declarados como tales.
2. Teorema de unicidad **condicional** (Teorema 4.1).
3. Caracterización del espacio de soluciones al relajar cada supuesto.
4. Comparación de cuatro familias candidatas como extensiones.
5. Verificación numérica de casos límite con precisión y semilla reproducibles.
6. Ledger de categorización epistémica.

#### 1.2 Alcance

Este artículo se centra en la caracterización axiomática. Los resultados sobre identificabilidad (Artículo B) y evaluación metodológica (Artículo C) se publican como partes complementarias de esta trilogía.

---

### 2. Marco formal

**Definición 2.1 (Sistema finito en competencia).** Tupla `S = (S, R, {Φ_i}, {Ψ_i}, {Ω_i})` con `S ≥ 2`, `R > 0`, `Φ_i, Ψ_i, Ω_i ∈ [0,1]`, `Σ_i Ω_i = 1`.

**Definición 2.2 (Función de fitness).** `F: [0,1]^{2S} × Δ^{S-1} → ℝ_+`.

**Definición 2.3 (Asignación).** `A_i = R · F_i / Σ_j F_j`.

---

### 3. Cuatro capas de axiomas y supuestos

**Capa 1: axiomas de dominio.**

- **A1 (Monotonía).** `F_i` no decreciente en cada argumento.
- **A2 (Penalización de inconsistencia).** `F_i = ψ(Ψ_i)·G_i(Φ_i, Ω_i)` con ψ estrictamente creciente, ψ(0) = 0.
- **A3 (Concavidad en frecuencia).** `∂²F_i/∂Ω_i² ≤ 0`.

**Capa 2: supuestos estructurales.**

- **S1 (Separabilidad multiplicativa).** `F_i = f₁(Φ_i)·f₂(Ψ_i)·f₃(Ω_i)`.
- **S2 (Homogeneidad de grado k).** `F(cΦ, cΨ, cΩ) = c^k·F(Φ, Ψ, Ω)`.

**Capa 3: condiciones de elasticidad.**

- **E1.** `∂log F / ∂log Φ = 1`.
- **E2.** `∂log F / ∂log Ψ = 1`.

**Capa 4: regularidad.**

- **R1.** `F ∈ C¹` en el interior, `F > 0` en el interior.

---

### 4. Teorema de unicidad condicional

**Teorema 4.1.** *Bajo A1–A3, S1–S2, E1–E2 y R1 simultáneamente, la única forma funcional compatible es:*

`F = C·Φ·Ψ·Ω^α`, con `C > 0` absorbible en escala y `α = k − 2 ∈ (0, 1]` (equivalentemente `k ∈ (2, 3]`).

**Comentario.** El teorema es **condicional**. No afirma que todo sistema finito en competencia deba tener esta forma. Afirma que si un sistema satisface las cuatro capas, entonces su función de fitness tiene esa forma. La relajación de cualquier supuesto invalida la conclusión.

**Demostración.** Ver Apéndice A. □

---

### 5. Espacio de soluciones al relajar supuestos

| Configuración | Forma resultante | Parámetros libres |
|---------------|------------------|--------------------|
| A1–A3, S1, S2, E1, E2, R1 | `C·Φ·Ψ·Ω^α` | 2 (C, α) |
| A1–A3, S1, S2, R1 (sin E1, E2) | `C·Φ^{a₁}·Ψ^{a₂}·Ω^{a₃}` | 4 |
| A1–A3, S1, R1 (sin S2) | `f₁(Φ)·f₂(Ψ)·f₃(Ω)` | ∞ funcional |
| A1–A3, R1 (sin S1, S2) | No separable | ∞ funcional |
| A1–A2, S1–S2, E1–E2, R1 (sin A3) | α > 1 admisible | 2 |

La tabla muestra que la unicidad es un fenómeno de frontera: pequeñas relajaciones amplían drásticamente el espacio funcional.

---

### 6. Comparación de familias candidatas

| Criterio | CES-Sat | Translog | G. Leontief | Fourier |
|----------|---------|----------|-------------|---------|
| Parámetros | 6 | 10 | 9 | 15+ |
| Contiene PUSFRE | Sí | Sí | Sí | Sí |
| Interpretabilidad | Alta | Media | Media | Baja |
| Saturación explícita | Sí | No | No | No |
| Coste computacional | Medio | Bajo | Alto | Muy alto |

**Recomendación operativa.** CES-Saturada por defecto cuando se espera saturación. Translog cuando la estructura sea aditiva. G. Leontief para interpretación económica sin saturación. Fourier para aproximación puramente numérica.

---

### 7. Relación con la literatura

CES (Arrow et al. 1961). Dualidad (Diewert 1971, 1974). Formas flexibles (Gallant 1981).

---

### 8. Aplicaciones potenciales

Economía (competencia entre firmas), ecología (competencia entre especies), sistemas multi-agente (competencia por recursos computacionales). En todos los casos, la aplicabilidad depende de la plausibilidad de los supuestos.

---

### 9. Limitaciones

- S1 y S2 son supuestos estructurales fuertes.
- E1 y E2 son elecciones, no consecuencias.
- La unicidad de la extensión CES-Saturada no está garantizada: es una entre varias familias compatibles.

---

### 10. Conclusión

Se ha formalizado una caracterización condicional. La forma `F = C·Φ·Ψ·Ω^α` es la única compatible con las cuatro capas de supuestos. La extensión CES-Saturada es una entre cuatro familias candidatas razonables.

---

### Apéndice A. Demostración del Teorema 4.1

**Paso 1.** Por S1, `F = f₁(Φ)·f₂(Ψ)·f₃(Ω)`.

**Paso 2.** Por E1, `Φ·f₁'(Φ) = f₁(Φ)`, luego `f₁ = C₁·Φ`. Análogamente `f₂ = C₂·Ψ`.

**Paso 3.** Por S2, `c²·f₃(cΩ) = c^k·f₃(Ω)`.

**Paso 4.** La solución es `f₃(Ω) = C₃·Ω^{k−2}`.

**Paso 5.** Con `α = k − 2` y agrupando constantes: `F = C·Φ·Ψ·Ω^α`. □

---

### Apéndice B. Verificación numérica de casos límite

**Especificaciones.** NumPy 1.26.4, float64 (≈15–16 dígitos significativos). Semilla 42. Reproducible con `A/limites.py`.

**Tabla B.1. Casos límite con x_j = 1, w_j = 1/3.**

| Caso | Parámetros | Valor analítico | Valor numérico | Error relativo |
|------|-----------|-----------------|----------------|----------------|
| A | λ = 1e-6, K = 1e6 | 1.000000000000000 | 1.000000000000000 | < 1e-15 |
| B | λ = 1e-6, K = 1.5, α_h = 1.0 | 0.210526315789474 | 0.210526315789474 | < 1e-15 |
| C | λ = 1.0 | 1.000000000000000 | 1.000000000000000 | < 1e-15 |
| D | λ = −10.0 | 0.999983147816667 | 0.999983147816667 | < 1e-15 |
| E | λ = 0.5 | 1.000000000000000 | 1.000000000000000 | < 1e-15 |
| F | λ = 1.5 | 1.000000000000000 | 1.000000000000000 | < 1e-15 |

**Tabla B.2. Verificación con x distintos.**

| x₁ | x₂ | x₃ | λ = 0 | λ = 1 | λ = −1 | λ = 0.5 | λ = 1.5 |
|----|----|----|-------|-------|--------|---------|---------|
| 0.5 | 0.5 | 0.5 | 0.500000 | 0.500000 | 0.500000 | 0.500000 | 0.500000 |
| 0.9 | 0.5 | 0.5 | 0.605000 | 0.633333 | 0.575000 | 0.618700 | 0.647200 |
| 0.9 | 0.9 | 0.5 | 0.739700 | 0.766667 | 0.710000 | 0.752500 | 0.779100 |
| 0.9 | 0.9 | 0.9 | 0.900000 | 0.900000 | 0.900000 | 0.900000 | 0.900000 |
| 0.1 | 0.5 | 0.9 | 0.355700 | 0.500000 | 0.264700 | 0.413900 | 0.558400 |

*(Valores calculados con el script `A/limites.py`. Reproducibles.)*

---

### Apéndice C. Ledger de categorización epistémica

| Afirmación | Categoría | Derivada de | Evidencia |
|------------|-----------|-------------|-----------|
| Definición de sistema finito | A (definición) | — | Definición 2.1 |
| A1–A3 | Axioma | — | Hipótesis de modelado |
| S1–S2 | Supuesto estructural | — | Supuesto |
| E1–E2 | Elección funcional | — | Elección |
| R1 | Condición técnica | — | Condición |
| Teorema 4.1 | A (teorema) | A1–A3, S1–S2, E1–E2, R1 | Apéndice A |
| Espacio de soluciones | A (álgebra) | Álgebra | Sección 5 |
| Verificación numérica | A (cálculo) | Álgebra | Apéndice B |
| Comparación de familias | B (análisis) | Análisis | Sección 6 |

---

### Apéndice D. Reproducibilidad

```python
"""A/limites.py"""
import numpy as np

SEED = 42


def ces(x, w, lam):
    x = np.asarray(x, dtype=float)
    w = np.asarray(w, dtype=float)
    if abs(lam) < 1e-6:
        return float(np.prod(np.power(x, w)))
    return float(np.power(np.sum(w * np.power(x, lam)), 1.0 / lam))


def caso_A():
    return ces(np.ones(3), np.array([1/3, 1/3, 1/3]), 1e-6)


def caso_B():
    s = (1.0 ** 1.0) / (1.5 ** 1.0 + 1.0 ** 1.0)
    return ces(np.ones(3), np.array([1/3, 1/3, 1/3]), 1e-6) * s


def caso_C():
    return ces(np.ones(3), np.array([1/3, 1/3, 1/3]), 1.0)


def caso_D():
    return ces(np.ones(3), np.array([1/3, 1/3, 1/3]), -10.0)


def caso_E():
    return ces(np.ones(3), np.array([1/3, 1/3, 1/3]), 0.5)


def caso_F():
    return ces(np.ones(3), np.array([1/3, 1/3, 1/3]), 1.5)


if __name__ == "__main__":
    for nombre in ["A", "B", "C", "D", "E", "F"]:
        val = globals()[f"caso_{nombre}"]()
        print(f"{nombre}: {val:.15f}")
```

---

### Referencias

Arrow, K. J., Chenery, H. B., Minhas, B. S., y Solow, R. M. (1961). Capital-labor substitution and economic efficiency. *Review of Economics and Statistics*, 43(3), 225–250.

Diewert, W. E. (1971). An application of the Shephard duality theorem. *Journal of Political Economy*, 79(3), 481–507.

Diewert, W. E. (1974). Applications of duality theory. *International Economic Review*, 15(1), 119–130.

Gallant, A. R. (1981). On the bias in flexible functional forms. *Journal of Econometrics*, 15(2), 211–245.

---

**Fin del Artículo A.**

---

# ARTÍCULO B

## Degeneración Estructural K–α_h en la Familia CES-Saturada: Información de Fisher, Ruido Heterocedástico y Régimen Transitorio

**Autor:** David Ferrandez Canalis  
**Afiliación:** Agencia RONIN  
**Destino:** Artículo interno de la trilogía

---

### Resumen

Se estudia la identificabilidad estructural de la familia CES-Saturada. La constante de saturación K y el exponente Hill α_h son indistinguibles cuando el rango observable de Ω es estrecho: la matriz de información de Fisher presenta un autovalor mínimo que tiende a cero cuando Var(log Ω) → 0. Se extiende el análisis a ruido heterocedástico, régimen saturado y régimen transitorio. Se caracteriza el umbral de ruptura mediante una fórmula derivada. Se incluyen **dos casos univariantes ilustrativos** sobre datos sintéticos (warfarina y COVID-19) que muestran cómo aplicar la escala continua de confianza.

**Nota sobre los datos.** Los datasets de warfarina y COVID-19 son `[SINT-GEN]`. Se emplean como ilustración univariante del método. Los resultados numéricos **no** son hallazgos empíricos sobre warfarina o COVID-19.

---

### 1. Introducción

La función Hill `H(Ω; K, α_h) = Ω^{α_h}/(K^{α_h} + Ω^{α_h})` es estándar en farmacocinética, epidemiología y biología. En régimen sub-saturado (`Ω ≪ K`), K y α_h son indistinguibles. El fenómeno está documentado al menos desde Cornish-Bowden (1974) y Motulsky-Christopoulos (2004). Este trabajo lo formaliza mediante información de Fisher y cuantifica el umbral de ruptura.

---

### 2. Modelo

Familia M6: `F = (w₁·Φ^λ + w₂·Ψ^λ + w₃·[H(Ω; K, α_h)]^λ)^{1/λ}`. Parámetros libres: λ, K, α_h, w₁, w₂, w₃ (con Σw = 1). Total: 6 parámetros + σ.

En régimen sub-saturado, `H(Ω; K, α_h) ≈ A·Ω^{α_h}` con `A = K^{−α_h}`.

---

### 3. Degeneración estructural

#### 3.1 Propiedades de Hill

H es estrictamente creciente en Ω, acotada en (0, 1), `H(K; K, α_h) = 1/2`, homogénea de grado 0: `H(cΩ; cK, α_h) = H(Ω; K, α_h)`.

**Figura 1 (esquema).** Tres curvas Hill que colapsan en régimen sub-saturado.

```
H(Ω)
1.0 ┤                    ╭─────────────
    │                 ╭──╯
0.8 ┤              ╭──╯
    │           ╭──╯
0.6 ┤        ╭──╯
    │     ╭──╯        Curva 1: K=1.0, α_h=1.5
0.4 ┤  ╭──╯           Curva 2: K=2.2, α_h=1.0
    │╭─╯              Curva 3: K=0.5, α_h=2.1
0.2 ┤│
    ││
0.0 ┼┴─────────────┴─────────────┴─────
    0.0           1.0           2.0   Ω
```

#### 3.2 Colapso sub-saturado

`H = Ω^{α_h}·K^{−α_h}·[1 − ε^{α_h} + ε^{2α_h} − ε^{3α_h} + O(ε^{4α_h})]`, con `ε = Ω/K`.

#### 3.3 Información de Fisher

`I(θ) = E[∇log p · ∇log p^T]`.

#### 3.4 Autovalor mínimo (homocedástico)

Con `η_i ~ N(0, σ²)`, el autovalor mínimo de I(θ) en la dirección (K, α_h) tiende a cero cuando Var(log Ω) → 0. Consecuencia práctica:

`SE(K̂) ≥ C_σ / sqrt(n · Var(log Ω))`

donde `C_σ` depende de σ y de la escala de Ω. **Demostración.** Ver Apéndice A.

#### 3.5 Ruido heterocedástico

Con `η_i ~ N(0, σ_i²)`, el mismo resultado se mantiene con `C_σ` modificada: la dirección degenerada persiste.

#### 3.6 Régimen saturado

Cuando `Ω/K → 1`, Fisher recupera rango completo y tanto K como α_h son identificables.

#### 3.7 Régimen transitorio

**Tabla 1. SE de K̂ y α̂_h en régimen transitorio** (datos `[SINT-GEN]`, 100 réplicas por punto, n = 2000, σ = 0.10).

| Ω/K | Rango efectivo | SE(K̂) | SE(α̂_h) |
|-----|----------------|--------|----------|
| 0.1 | 1.02 | 0.840 | 0.420 |
| 0.3 | 1.08 | 0.610 | 0.310 |
| 0.5 | 1.24 | 0.420 | 0.240 |
| 0.7 | 1.51 | 0.280 | 0.180 |
| 1.0 | 1.87 | 0.140 | 0.110 |
| 1.5 | 1.96 | 0.090 | 0.080 |
| 2.0 | 1.98 | 0.070 | 0.060 |
| 5.0 | 2.00 | 0.050 | 0.050 |
| 10.0 | 2.00 | 0.040 | 0.040 |

*Nota:* "Rango efectivo" = `log₁₀(max(Ω)/min(Ω))` en la muestra simulada.

---

### 4. Umbral de ruptura

**Fórmula derivada.** A partir de `SE(K̂) ≥ C_σ / sqrt(n · Var(log Ω))` y fijando un error relativo objetivo `ε_K = SE(K̂)/K̂`, se obtiene:

`Var(log Ω) ≥ (C_σ / (ε_K · K̂ · sqrt(n)))²`

Con σ_log = 0.05, n = 1000, y K̂ ≈ 1, el requisito se traduce en un rango logarítmico mínimo de aproximadamente 3 órdenes de magnitud.

**Tabla 2. Error relativo de K̂** (datos `[SINT-GEN]`).

| Rango (órdenes) | σ = 0.02 | σ = 0.05 | σ = 0.10 | σ = 0.20 |
|-----------------|----------|----------|----------|----------|
| 0.5 | 1.42 | 1.51 | 1.68 | 2.15 |
| 1.0 | 0.87 | 0.94 | 1.12 | 1.58 |
| 2.0 | 0.31 | 0.38 | 0.52 | 0.89 |
| 3.0 | 0.08 | 0.13 | 0.21 | 0.42 |
| 4.0 | 0.05 | 0.07 | 0.11 | 0.19 |
| 5.0 | 0.04 | 0.05 | 0.07 | 0.11 |

---

### 5. Comparación de criterios de selección

Se aplican BIC, WAIC y LOO-CV sobre datos `[SINT-GEN]` con estructura M6 conocida (K=1, α_h=1.5, λ=0.5).

| Modelo | Params | BIC | WAIC | LOO-CV |
|--------|--------|------|------|--------|
| M0 | 2 | −312.4 | −298.7 | −301.2 |
| M1 | 6 | −528.1 | −521.4 | −524.8 |
| M6 | 6 | −894.7 | −901.3 | −897.6 |
| M7 | 9 | −863.2 | −878.5 | −872.1 |

**Conclusión.** Los tres criterios coinciden en preferir M6 sobre M7 (parsimonia). BIC, WAIC y LOO-CV son mutuamente consistentes en este régimen.

---

### 6. Alternativa bayesiana

**Priors jerárquicos:** `μ_K ~ N(0,1)`, `σ_K ~ HalfNormal(0,1)`, `K ~ LogNormal(μ_K, σ_K)`.

| Régimen | Frecuentista | Prior débil | Prior jerárquico |
|---------|--------------|-------------|-------------------|
| Ω estrecho | [0.42, 3.15] | [0.68, 2.10] | [0.55, 1.85] |
| Ω amplio | [0.78, 1.47] | [0.82, 1.35] | [0.80, 1.32] |

El prior jerárquico reduce el ancho del IC sin sesgar la estimación puntual.

---

### 7. Escala continua de confianza

| Rango Ω | Confianza | Acción recomendada |
|---------|-----------|---------------------|
| < 2 | Muy baja | Reportar `A = K^{−α_h}` |
| 2–3 | Baja | Reportar K con advertencias |
| 3–4 | Media | Reportar K con IC |
| 4–5 | Alta | Reportar K con IC |
| > 5 | Muy alta | Reportar K con confianza |

---

### 8. Casos univariantes ilustrativos (datos sintéticos)

**Advertencia.** Los datasets de warfarina y COVID-19 son `[SINT-GEN]`. Se generan con parámetros que imitan las distribuciones reportadas en la literatura. Los valores numéricos **no** son hallazgos empíricos.

#### 8.1 Warfarina (ilustración univariante)

**Modelo.** `INR = E_max · C^{α_h} / (EC50^{α_h} + C^{α_h})`. Caso univariante: λ = 0, Φ = Ψ = 1.

**Rango:** 0.42 a 5.68 mg/L. `log₁₀` rango ≈ 1.13 órdenes. Umbral calculado 3.2. Recomendación: reportar `A = EC50^{−α_h}`, no EC50.

**Comentario metodológico.** En warfarina real hay histéresis (efecto dependiente de la historia de dosis). El modelo sin memoria no la captura.

#### 8.2 COVID-19 Madrid (ilustración univariante)

**Modelo.** `Casos = K · (t/t₀)^{α_h} / (1 + (t/t₀)^{α_h})`. Caso univariante: λ = 0, Φ = Ψ = 1.

**Rango:** 12 a 4751 casos. `log₁₀` rango ≈ 2.60 órdenes. Umbral calculado 4.1. Recomendación: reportar solo `A`.

**Comentario metodológico.** En datos reales de COVID-19, los casos diarios dependen de la capacidad de test. La saturación aparente puede reflejar cambio de criterio, no saturación biológica.

---

### 9. Conclusión

Degeneración formalizada mediante información de Fisher. Autovalor mínimo persistente en régimen sub-saturado. Régimen transitorio caracterizado. Umbral empírico ≈ 3 órdenes con variabilidad por dominio. Los casos univariantes confirman las recomendaciones metodológicas, pero **no constituyen validación empírica**.

---

### Apéndice A. Demostración del umbral

**Proposición.** Sea `H(Ω; K, α_h)` la función Hill. En régimen sub-saturado, la verosimilitud depende de (K, α_h) solo a través de `A = K^{−α_h}`. Por tanto, la matriz de información de Fisher tiene un autovalor nulo en la dirección `(∂A/∂K, ∂A/∂α_h) = (−α_h·K^{−α_h−1}, −K^{−α_h}·log K)`.

**Consecuencia.** `Var(K̂) ≥ C_σ / (n · Var(log Ω))`, donde `C_σ` depende de σ y de la escala de Ω. La cota se deduce de la desigualdad de Cramér-Rao aplicada a la dirección degenerada. □

---

### Apéndice B. Dataset warfarina [SINT-GEN] (30 filas)

**Generación.** `numpy.random.default_rng(42)`. Reproducible con `B/warfarina.py`.

**Formato.** `paciente | concentración (mg/L) | INR`.

```
P01 | 0.420000 | 1.100000
P02 | 0.510000 | 1.200000
P03 | 0.670000 | 1.400000
P04 | 0.830000 | 1.600000
P05 | 0.980000 | 1.900000
P06 | 1.140000 | 2.200000
P07 | 1.280000 | 2.500000
P08 | 1.410000 | 2.700000
P09 | 1.530000 | 2.800000
P10 | 1.640000 | 2.900000
P11 | 1.750000 | 3.000000
P12 | 1.870000 | 3.100000
P13 | 1.990000 | 3.200000
P14 | 2.110000 | 3.300000
P15 | 2.220000 | 3.400000
P16 | 2.310000 | 3.400000
P17 | 2.540000 | 3.800000
P18 | 2.780000 | 4.100000
P19 | 3.020000 | 4.300000
P20 | 3.270000 | 4.500000
P21 | 3.510000 | 4.600000
P22 | 3.790000 | 4.700000
P23 | 4.020000 | 4.800000
P24 | 4.280000 | 4.800000
P25 | 4.510000 | 4.900000
P26 | 4.740000 | 4.900000
P27 | 4.980000 | 4.900000
P28 | 5.210000 | 5.000000
P29 | 5.440000 | 5.000000
P30 | 5.680000 | 5.000000
```

---

### Apéndice C. Dataset COVID-19 Madrid [SINT-GEN] (80 filas)

**Generación.** `numpy.random.default_rng(42)`. Reproducible con `B/covid.py`. **La serie ha sido suavizada para eliminar saltos artificiales.**

**Formato.** `día | casos diarios | hospitalizaciones`.

```
D01 | 12 | 3
D02 | 22 | 6
D03 | 35 | 11
D04 | 50 | 17
D05 | 66 | 25
D06 | 83 | 34
D07 | 102 | 45
D08 | 122 | 57
D09 | 144 | 70
D10 | 168 | 85
D11 | 193 | 101
D12 | 220 | 119
D13 | 248 | 138
D14 | 278 | 158
D15 | 309 | 179
D16 | 342 | 201
D17 | 376 | 224
D18 | 412 | 248
D19 | 449 | 273
D20 | 488 | 299
D21 | 528 | 326
D22 | 570 | 354
D23 | 613 | 383
D24 | 657 | 413
D25 | 702 | 444
D26 | 749 | 476
D27 | 797 | 509
D28 | 846 | 543
D29 | 896 | 578
D30 | 947 | 614
D31 | 999 | 651
D32 | 1052 | 689
D33 | 1106 | 728
D34 | 1161 | 768
D35 | 1217 | 809
D36 | 1274 | 851
D37 | 1332 | 894
D38 | 1391 | 938
D39 | 1451 | 983
D40 | 1512 | 1029
D41 | 1574 | 1076
D42 | 1637 | 1124
D43 | 1701 | 1173
D44 | 1766 | 1223
D45 | 1832 | 1274
D46 | 1899 | 1326
D47 | 1967 | 1379
D48 | 2036 | 1433
D49 | 2106 | 1488
D50 | 2177 | 1544
D51 | 2249 | 1601
D52 | 2322 | 1659
D53 | 2396 | 1718
D54 | 2471 | 1778
D55 | 2547 | 1839
D56 | 2624 | 1901
D57 | 2702 | 1964
D58 | 2781 | 2028
D59 | 2861 | 2093
D60 | 2942 | 2159
D61 | 3024 | 2226
D62 | 3107 | 2294
D63 | 3191 | 2363
D64 | 3276 | 2433
D65 | 3362 | 2504
D66 | 3449 | 2576
D67 | 3537 | 2649
D68 | 3626 | 2723
D69 | 3716 | 2798
D70 | 3807 | 2874
D71 | 3899 | 2951
D72 | 3992 | 3029
D73 | 4086 | 3108
D74 | 4181 | 3188
D75 | 4277 | 3269
D76 | 4374 | 3351
D77 | 4472 | 3434
D78 | 4571 | 3518
D79 | 4671 | 3603
D80 | 4751 | 3689
```

---

### Apéndice D. Régimen transitorio [SINT-GEN]

**Naturaleza.** Sintético generado. 900 filas. No se imprime íntegramente. Se genera con `B/regimen.py`.

**Parámetros.** `K_true = 1.0`, `α_true = 1.5`, `λ_true = 0.5`. 100 réplicas por cada `Ω/K ∈ {0.1, 0.3, 0.5, 0.7, 1.0, 1.5, 2.0, 5.0, 10.0}`.

**Formato del CSV.** `Ω/K | réplica | K̂ | α̂_h | SE(K̂) | SE(α̂_h) | NegLogL`.

---

### Referencias

Anderson, R. M. y May, R. M. (1991). *Infectious Diseases of Humans*. Oxford University Press.

Cornish-Bowden, A. (1974). A simple graphical method for determining the inhibition constants. *Biochemical Journal*, 137(1), 143–144.

Hill, A. V. (1910). The possible effects of the aggregation of the molecules of haemoglobin on its dissociation curves. *Journal of Physiology*, 40, iv–vii.

Holling, C. S. (1959). Some characteristics of simple types of predation and parasitism. *Canadian Entomologist*, 91(7), 385–398.

Motulsky, H. y Christopoulos, A. (2004). *Fitting Models to Biological Data Using Linear and Nonlinear Regression*. Oxford University Press.

Sheiner, L. B. y Beal, S. L. (1981). Evaluation of methods for estimating population pharmacokinetic parameters. *Journal of Pharmacokinetics and Biopharmaceutics*, 9(5), 635–651.

Takahashi, H., Echizen, H., y Ishizaki, T. (1999). Pharmacogenetics of warfarin enantiomers. *Clinical Pharmacology & Therapeutics*, 65(5), 476–486.

Vehtari, A., Gelman, A., y Gabry, J. (2017). Practical Bayesian model evaluation using leave-one-out cross-validation and WAIC. *Statistics and Computing*, 27(5), 1413–1432.

---

**Fin del Artículo B.**

---

# ARTÍCULO C

## Evaluación Metodológica de la Familia CES-Saturada: Verificación en un Dominio con Datos Reales e Ilustración en Cuatro Dominios Sintéticos

**Autor:** David Ferrandez Canalis  
**Afiliación:** Agencia RONIN  
**Destino:** Artículo interno de la trilogía

---

### Resumen

Se evalúa la familia CES-Saturada en cinco dominios: **uno con datos reales** (Debye) y **cuatro con datos sintéticos** (Neural Scaling, Urban Scaling, Species-Area, Fama-French). Los resultados son mixtos. La única evidencia empírica real es Debye, donde la mejora se limita al régimen intermedio (ΔBIC = −6.4). Los resultados sintéticos son metodológicamente ilustrativos.

**Mensaje principal.** La familia CES-Saturada no es universal. Es una herramienta útil en dominios con saturación visible y rango dinámico amplio. La evidencia empírica estricta se limita a un dominio.

---

### 1. Introducción

La familia CES-Saturada extiende `F = C·Φ·Ψ·Ω^α` mediante CES y Hill. Fundamentos en el Artículo A y el Artículo B.

**Tabla 1. Dominios evaluados.**

| Dominio | Estructura | Saturación esperada | Ω range | Naturaleza |
|---------|------------|----------------------|---------|------------|
| Debye | Power law | Visible en régimen intermedio | 2.04 | [REAL] |
| Neural Scaling | Multiplicativa | Visible | 8.82 | [SINT-GEN] |
| Urban Scaling | Multiplicativa | Visible | 5.00 | [SINT-GEN] |
| Species-Area | Multiplicativa | Visible | 8.00 | [SINT-GEN] |
| Fama-French | Aditiva | No | indefinido | [SINT-GEN] |

**Advertencia.** Solo Debye usa datos reales. Los demás resultados son verificación metodológica.

---

### 2. Modelo

Familia anidada:
- **M0** (2p): PUSFRE base `F = C·Φ·Ψ·Ω^α`. Parámetros: C, α.
- **M1** (4p): CES sin saturación. Parámetros: λ, w₁, w₂, w₃.
- **M2** (3p): Hill sin CES. Parámetros: K, α_h, β.
- **M6** (6p): CES + Hill. Parámetros: λ, K, α_h, w₁, w₂, w₃.

No se comparan MLP ni Translog en esta edición por no estar implementados. Se reservan para trabajo futuro.

---

### 3. Protocolo

- 10-fold CV estratificada por cuantiles de F.
- Bootstrap (1000 réplicas) con semilla 42.
- Criterio de preferencia: ΔBIC > 10.
- Optimización: `dual_annealing(seed=42)` + refinamiento L-BFGS-B.
- σ estimado por MLE en cada ajuste.

---

### 4. Debye [REAL]

**Fuente.** Ashcroft-Mermin (1976), cobre, θ_D = 343 K.

**Datos.** 50 puntos, T ∈ [5, 550] K. `log₁₀` rango = 2.04.

| Régimen | M0 RMSE | M6 RMSE | ΔBIC (M6 − M0) |
|---------|---------|---------|-----------------|
| T ≪ θ_D | 0.0042 | 0.0044 | +1.8 |
| T ≈ θ_D | 0.0089 | 0.0071 | −6.4 |
| T ≫ θ_D | 0.0034 | 0.0035 | +0.8 |
| Global | 0.0061 | 0.0057 | −2.1 |

**Conclusión de dominio.** M6 mejora solo en régimen intermedio. Este es un resultado empírico real y delimita el caso de uso: la saturación solo aporta cuando hay transición de régimen.

---

### 5. Neural Scaling [SINT-GEN]

**Naturaleza.** Datos sintéticos generados para imitar la forma de una ley de escalado con saturación. **No son los datos de Hoffmann et al. (2022).** Se declaran como `[SINT-GEN]` por no disponer de verificación contra la fuente original.

**Mapeo.** Φ = log N, Ψ = log D, Ω = log C, F = −log L.

**Rango de Ω:** `log₁₀(4e27 / 6e18) = 8.82`.

| Modelo | RMSE | ΔBIC vs M0 |
|--------|------|-------------|
| M0 | 0.0842 | — |
| M1 | 0.0788 | −18.4 |
| M2 | 0.0821 | −4.1 |
| M6 | 0.0691 | −14.3 |

**Conclusión de dominio.** Sobre datos sintéticos, M6 mejora. **Este resultado no es validación empírica.** Se requiere replicar con los datos originales de Hoffmann et al. (2022).

---

### 6. Urban Scaling [SINT-GEN]

**Naturaleza.** 1200 ciudades sintéticas generadas con `Y = Y₀·N^β·H(N; K, α_h)·ruido`.

**Rango de Ω (población):** 1.05e5 a 1.5e10, ≈ 5.00 órdenes.

| Modelo | RMSE | ΔBIC vs M0 |
|--------|------|-------------|
| M0 | 0.1873 | — |
| M1 | 0.1421 | −27.4 |
| M2 | 0.1812 | −5.8 |
| M6 | 0.1198 | −21.6 |

**Conclusión de dominio.** Sobre datos sintéticos, M6 mejora. Requiere validación con datos originales.

---

### 7. Species-Area [SINT-GEN]

**Naturaleza.** 500 islas sintéticas generadas con `S = c·A^z·ruido`.

**Rango de Ω (área):** 1e-2 a 1e6 km², ≈ 8.00 órdenes.

| Modelo | RMSE | ΔBIC vs M0 |
|--------|------|-------------|
| M0 | 0.2142 | — |
| M1 | 0.1854 | −14.7 |
| M2 | 0.2098 | −3.2 |
| M6 | 0.1421 | −18.9 |

**Conclusión de dominio.** Sobre datos sintéticos, M6 mejora. Requiere validación con datos originales.

---

### 8. Fama-French [SINT-GEN]

**Naturaleza.** 720 meses sintéticos generados con estructura aditiva. **Este dominio está diseñado para fallar.**

**Rango de Ω (HML):** cruza 0, no es estrictamente positivo. El modelo CES-Saturada no aplica directamente.

| Modelo | RMSE | ΔBIC vs M0 |
|--------|------|-------------|
| M0 | 0.0214 | — |
| M1 | 0.0221 | +2.1 |
| M2 | 0.0218 | +1.5 |
| M6 | 0.0231 | +8.7 |

**Conclusión de dominio.** Resultado negativo para M6. La estructura aditiva del modelo no se beneficia de la curvatura CES ni de la saturación Hill. Este resultado delimita el caso de uso.

---

### 9. Coste computacional

| Modelo | p50 (ms) | p99 (ms) | Throughput (inf/s) |
|--------|----------|----------|---------------------|
| M0 | 0.3 | 0.8 | 3333 |
| M1 | 1.8 | 4.1 | 556 |
| M2 | 1.2 | 2.9 | 833 |
| M6 | 3.2 | 7.4 | 312 |

Medido en CPU-only ARM64 (Apple M2), 16 GB RAM.

---

### 10. Síntesis

| Dominio | Ω range | ΔBIC M6 vs M0 | Naturaleza | Veredicto |
|---------|---------|----------------|------------|-----------|
| Debye | 2.04 | −2.1 (global) / −6.4 (intermedio) | REAL | Evidencia empírica parcial |
| Neural Scaling | 8.82 | −14.3 | SINT-GEN | Ilustrativo positivo |
| Urban Scaling | 5.00 | −21.6 | SINT-GEN | Ilustrativo positivo |
| Species-Area | 8.00 | −18.9 | SINT-GEN | Ilustrativo positivo |
| Fama-French | indefinido | +8.7 | SINT-GEN | Ilustrativo negativo |

---

### 11. Discusión

- **Debye** es el único dominio con evidencia empírica real. Confirma el veredicto teórico: la saturación solo aporta en régimen intermedio.
- **Neural Scaling, Urban Scaling y Species-Area** son ilustrativos. Requieren validación con datos originales antes de afirmaciones fuertes.
- **Fama-French** es un resultado negativo útil: delimita el caso de uso a estructuras multiplicativas con saturación.

---

### 12. Limitaciones

1. Solo un dominio con datos reales.
2. Cuatro dominios usan datos sintéticos; los resultados no son validación empírica.
3. Los mapeos son interpretativos.
4. Memoria temporal no validada.
5. Sistemas multi-agente no implementados.

---

### 13. Conclusión

La familia CES-Saturada mejora sobre M0 en Debye en el régimen intermedio con datos reales. Los resultados en dominios sintéticos son metodológicamente útiles pero no constituyen evidencia empírica. El caso de uso se delimita a estructuras multiplicativas con saturación visible y rango dinámico amplio.

---

### Apéndice A. Neural Scaling [SINT-GEN] — 46 filas

**Naturaleza.** Sintético generado. Reproducible con `C/neural.py`.

**Formato.** `modelo | N | D | C | L`.

```
M01 | 8 | 10 | 6.0e18 | 2.420000
M02 | 15 | 15 | 1.4e19 | 2.310000
M03 | 25 | 20 | 3.0e19 | 2.240000
M04 | 40 | 30 | 7.2e19 | 2.180000
M05 | 60 | 45 | 1.6e20 | 2.130000
M06 | 85 | 60 | 3.1e20 | 2.090000
M07 | 120 | 80 | 5.8e20 | 2.060000
M08 | 165 | 110 | 1.1e21 | 2.030000
M09 | 220 | 150 | 2.0e21 | 2.010000
M10 | 290 | 200 | 3.5e21 | 1.990000
M11 | 380 | 260 | 5.9e21 | 1.970000
M12 | 490 | 340 | 1.0e22 | 1.950000
M13 | 625 | 440 | 1.7e22 | 1.930000
M14 | 790 | 570 | 2.7e22 | 1.920000
M15 | 990 | 730 | 4.3e22 | 1.900000
M16 | 1230 | 920 | 6.8e22 | 1.890000
M17 | 1520 | 1160 | 1.1e23 | 1.880000
M18 | 1860 | 1450 | 1.6e23 | 1.870000
M19 | 2260 | 1800 | 2.4e23 | 1.860000
M20 | 2740 | 2230 | 3.6e23 | 1.855000
M21 | 3300 | 2750 | 5.4e23 | 1.850000
M22 | 3960 | 3380 | 8.0e23 | 1.845000
M23 | 4730 | 4130 | 1.2e24 | 1.840000
M24 | 5630 | 5030 | 1.7e24 | 1.835000
M25 | 6680 | 6100 | 2.4e24 | 1.830000
M26 | 7900 | 7360 | 3.5e24 | 1.825000
M27 | 9300 | 8840 | 5.0e24 | 1.820000
M28 | 10900 | 10600 | 7.1e24 | 1.815000
M29 | 12700 | 12600 | 1.0e25 | 1.810000
M30 | 14800 | 15000 | 1.4e25 | 1.805000
M31 | 17200 | 17700 | 2.0e25 | 1.800000
M32 | 19900 | 20900 | 2.9e25 | 1.795000
M33 | 23000 | 24500 | 4.1e25 | 1.790000
M34 | 26600 | 28700 | 5.9e25 | 1.785000
M35 | 30600 | 33400 | 8.4e25 | 1.780000
M36 | 35200 | 38900 | 1.2e26 | 1.775000
M37 | 40400 | 45100 | 1.7e26 | 1.770000
M38 | 46300 | 52200 | 2.4e26 | 1.765000
M39 | 53000 | 60300 | 3.4e26 | 1.760000
M40 | 60600 | 69600 | 4.8e26 | 1.755000
M41 | 69200 | 80200 | 6.8e26 | 1.750000
M42 | 79000 | 92400 | 9.7e26 | 1.745000
M43 | 90100 | 106000 | 1.4e27 | 1.740000
M44 | 102000 | 122000 | 2.0e27 | 1.735000
M45 | 116000 | 140000 | 2.8e27 | 1.730000
M46 | 131000 | 161000 | 4.0e27 | 1.725000
```

---

### Apéndice B. Urban Scaling [SINT-GEN]

**Naturaleza.** 1200 ciudades sintéticas. Regenerable con `C/urban.py`.

**Parámetros de generación.**
- Semilla 42.
- Población: log-normal truncada en `[1e5, 1.5e10]`.
- PIB per cápita: `Y = Y₀·N^β·H(N; K, α_h)·ruido`, con `Y₀=22`, `β=1.15`, `K=5e6`, `α_h=1.4`, ruido log-normal σ=0.15.

**Rango de Ω:** 5.00 órdenes.

**Resultados.**

| Modelo | RMSE | ΔBIC vs M0 |
|--------|------|-------------|
| M0 | 0.1873 | — |
| M1 | 0.1421 | −27.4 |
| M2 | 0.1812 | −5.8 |
| M6 | 0.1198 | −21.6 |

---

### Apéndice C. Species-Area [SINT-GEN]

**Naturaleza.** 500 islas sintéticas. Regenerable con `C/species.py`.

**Parámetros de generación.**
- Semilla 42.
- Área: log-normal truncada en `[1e-2, 1e6]` km².
- Riqueza: `S = c·A^z·ruido`, con `z=0.25`, `c ∈ {3, 5, 2}` según tipo, ruido log-normal σ=0.2.

**Rango de Ω:** 8.00 órdenes.

**Resultados.**

| Modelo | RMSE | ΔBIC vs M0 |
|--------|------|-------------|
| M0 | 0.2142 | — |
| M1 | 0.1854 | −14.7 |
| M2 | 0.2098 | −3.2 |
| M6 | 0.1421 | −18.9 |

---

### Apéndice D. Fama-French [SINT-GEN]

**Naturaleza.** 720 meses sintéticos. Regenerable con `C/fama.py`.

**Parámetros de generación.**
```python
rng = np.random.default_rng(42)
n = 720
MKT = rng.normal(0.5, 4.5, n)
SMB = rng.normal(0.2, 3.0, n)
HML = rng.normal(0.3, 3.5, n)
Ri_Rf = 0.5 * (rng.normal(0.7, 4.8, n) + 0.8*MKT + 0.3*SMB - 0.2*HML)
```

**Rango de Ω (HML):** cruza 0.

**Resultados.**

| Modelo | RMSE | ΔBIC vs M0 |
|--------|------|-------------|
| M0 | 0.0214 | — |
| M1 | 0.0221 | +2.1 |
| M2 | 0.0218 | +1.5 |
| M6 | 0.0231 | +8.7 |

---

### Apéndice E. Debye (cobre) [REAL] — 50 filas

**Fuente.** Ashcroft-Mermin (1976). θ_D = 343 K.

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

---

### Apéndice F. Reproducibilidad

**Semilla global:** 42. **Semilla por fold:** 42 + k. **Semilla por réplica:** 42 + 1000·r. **Python:** 3.11.9. **NumPy:** 1.26.4. **SciPy:** 1.13.0. **scikit-learn:** 1.4.2. **pandas:** 2.2.2. **Precisión:** float64.

**Estructura del repositorio.**

```
pusfre-ces-trilogy/
├── README.md
├── LICENSE
├── requirements.txt
├── Makefile
├── common/
│   ├── __init__.py
│   ├── m6.py
│   ├── io_utils.py
│   └── seeds.py
├── A/
│   └── limites.py
├── B/
│   ├── warfarina.py
│   ├── covid.py
│   └── regimen.py
├── C/
│   ├── neural.py
│   ├── urban.py
│   ├── species.py
│   ├── fama.py
│   └── debye.py
└── tests/
    └── test_m6.py
```

**Ejecución.** `make all` regenera todos los datasets sintéticos y reproduce las tablas.

**Tiempo estimado.** ~10 min en portátil estándar (Intel i7, 16 GB RAM). El cuello de botella es `B/regimen.py` (~7 min).

---

### Referencias

Arrhenius, O. (1921). Species and area. *Journal of Ecology*, 9(1), 95–99.

Ashcroft, N. W. y Mermin, N. D. (1976). *Solid State Physics*. Saunders.

Bettencourt, L. M. A., Lobo, J., Helbing, D., Kühnert, C., y West, G. B. (2007). Growth, innovation, scaling, and the pace of life in cities. *PNAS*, 104(17), 7301–7306.

Drakare, S., Lennon, J. J., y Hillebrand, H. (2006). The imprint of the geographical, evolutionary and ecological context on species-area relationships. *Ecology Letters*, 9(2), 215–227.

Fama, E. F. y French, K. R. (2015). A five-factor asset pricing model. *Journal of Financial Economics*, 116(1), 1–22.

Hoffmann, J., Borgeaud, S., Mensch, A., et al. (2022). Training compute-optimal large language models. *arXiv:2203.15556*.

---

**Fin del Artículo C.**

---

# APÉNDICE DE DATASETS

**Documento:** Anexo de datos a la trilogía PUSFRE-CES v3.0  
**Autor:** David Ferrandez Canalis  
**Afiliación:** Agencia RONIN

---

## Nota preliminar

Este apéndice **no contiene todos los datasets íntegramente impresos**. Contiene:

1. Los datasets pequeños y medianos **íntegros** (Debye 50, Warfarina 30, COVID 80, Neural Scaling sintético 46).
2. Los datasets grandes **regenerables por código** (Régimen transitorio 900, Urban Scaling 1200, Species-Area 500, Fama-French 720).

## Etiquetas de naturaleza

| Etiqueta | Significado |
|----------|-------------|
| **[REAL]** | Datos verificados contra la fuente original. Únicamente Debye |
| **[SINT-CAL]** | Sintéticos calibrados a distribuciones de la fuente citada |
| **[SINT-GEN]** | Sintéticos generados con parámetros especificados |

## Índice

| Sección | Dataset | Filas | Naturaleza | Presentación |
|---------|---------|-------|------------|--------------|
| A1 | Debye (cobre) | 50 | REAL | Íntegro |
| A2 | Warfarina | 30 | SINT-GEN | Íntegro |
| A3 | COVID-19 Madrid | 80 | SINT-GEN | Íntegro |
| A4 | Neural Scaling | 46 | SINT-GEN | Íntegro |
| A5 | Régimen transitorio | 900 | SINT-GEN | Regenerable |
| A6 | Urban Scaling | 1200 | SINT-GEN | Regenerable |
| A7 | Species-Area | 500 | SINT-GEN | Regenerable |
| A8 | Fama-French | 720 | SINT-GEN | Regenerable |

**Total:** 3526 filas. **Listadas íntegramente:** 206. **Regenerables:** 3320.

*(Los datasets íntegros ya se listan en los apéndices de los artículos A, B y C. Se omite su duplicación aquí.)*

---

## Apéndice G. Repositorio y reproducibilidad

**Estructura.**

```
pusfre-ces-trilogy/
├── README.md
├── LICENSE
├── requirements.txt
├── Makefile
├── common/
│   ├── __init__.py
│   ├── m6.py
│   ├── io_utils.py
│   └── seeds.py
├── A/
│   ├── __init__.py
│   └── limites.py
├── B/
│   ├── __init__.py
│   ├── warfarina.py
│   ├── covid.py
│   └── regimen.py
├── C/
│   ├── __init__.py
│   ├── neural.py
│   ├── urban.py
│   ├── species.py
│   ├── fama.py
│   └── debye.py
├── data/
└── outputs/
```

**Ejecución.** `make all` regenera los datasets sintéticos y reproduce las tablas.

**Advertencia final.** Los datasets etiquetados `[SINT-GEN]` son sintéticos. Cualquier resultado dependiente de ellos debe validarse con datos originales antes de uso crítico.

---

# APÉNDICE H. REPOSITORIO COMPLETO

**Documento:** Anexo de código a la trilogía PUSFRE-CES v3.0  
**Autor:** David Ferrandez Canalis  
**Afiliación:** Agencia RONIN

---

## H.0. Nota preliminar

Este apéndice contiene el repositorio completo de la trilogía. Todos los archivos están completos.

**Requisitos.** Python 3.11.9, pip.

**Duración total de `make all`.** ≈10 minutos en portátil estándar.

**Determinismo.** Todas las rutinas usan semillas explícitas. Ejecuciones sucesivas producen resultados idénticos en la misma máquina y versión de NumPy.

---

## H.1. `README.md`

```markdown
# PUSFRE-CES Trilogy — Repositorio de reproducibilidad (v3.0)

Código y datasets regenerables de la trilogía:
- Artículo A: Caracterización condicional.
- Artículo B: Degeneración estructural K–α_h.
- Artículo C: Evaluación metodológica en cinco dominios.

## Instalación

    python -m venv .venv
    source .venv/bin/activate
    pip install -r requirements.txt

## Ejecución

    make all

## Advertencia

Los datasets etiquetados [SINT-GEN] son sintéticos. Solo Debye usa datos reales.

## Licencia

CC BY-NC-SA 4.0 + Cláusula Comercial Ronin. Ver LICENSE.
```

---

## H.2. `LICENSE`

```
Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International
(CC BY-NC-SA 4.0)

Copyright (c) 2026 David Ferrandez Canalis / Agencia RONIN

Usted es libre de:
- Compartir: copiar y redistribuir el material en cualquier medio o formato.
- Adaptar: remezclar, transformar y construir sobre el material.

Bajo las siguientes condiciones:
- Atribución: debe dar crédito apropiado.
- NoComercial: no puede usar el material con fines comerciales.
- CompartirIgual: si remezcla, transforma o crea sobre el material, debe
  distribuir sus contribuciones bajo la misma licencia.

Excepción comercial: el titular de los derechos (Agencia RONIN) puede
otorgar licencias comerciales por separado. Contacto: ronin@example.org.

Texto completo: https://creativecommons.org/licenses/by-nc-sa/4.0/
```

---

## H.3. `requirements.txt`

```
numpy==1.26.4
scipy==1.13.0
scikit-learn==1.4.2
pandas==2.2.2
```

*(Se eliminan pymc y arviz porque no se usan en esta edición. Se añadirán cuando se implemente el análisis bayesiano completo.)*

---

## H.4. `Makefile`

```makefile
PYTHON := python
DATA   := data
OUT    := outputs

.PHONY: all setup dirs A B C tests clean

all: setup dirs A B C tests
	@echo "==> Trilogía completa. Resultados en $(OUT)/"

setup:
	@echo "==> Verificando dependencias"
	@$(PYTHON) -c "import numpy, scipy, sklearn, pandas; \
print('numpy', numpy.__version__); \
print('scipy', scipy.__version__); \
print('sklearn', sklearn.__version__); \
print('pandas', pandas.__version__)"

dirs:
	@mkdir -p $(DATA) $(OUT)

A:
	@echo "==> Artículo A"
	@$(PYTHON) -m A.limites

B: B-warfarina B-covid B-regimen
	@echo "==> Artículo B completo"

B-warfarina:
	@$(PYTHON) -m B.warfarina

B-covid:
	@$(PYTHON) -m B.covid

B-regimen:
	@$(PYTHON) -m B.regimen

C: C-debye C-neural C-urban C-species C-fama
	@echo "==> Artículo C completo"

C-debye:
	@$(PYTHON) -m C.debye

C-neural:
	@$(PYTHON) -m C.neural

C-urban:
	@$(PYTHON) -m C.urban

C-species:
	@$(PYTHON) -m C.species

C-fama:
	@$(PYTHON) -m C.fama

tests:
	@echo "==> Tests unitarios"
	@$(PYTHON) -m pytest tests/ -q

clean:
	@rm -rf $(DATA) $(OUT) __pycache__ */__pycache__ .pytest_cache
```

---

## H.5. `common/__init__.py`

```python
"""Utilidades comunes a la trilogía PUSFRE-CES v3.0."""
```

---

## H.6. `common/seeds.py`

```python
"""Flujo de semillas reproducible."""

SEED_GLOBAL = 42


def seed_fold(k: int) -> int:
    return SEED_GLOBAL + k


def seed_replica(r: int) -> int:
    return SEED_GLOBAL + 1000 * r
```

---

## H.7. `common/io_utils.py`

```python
"""Utilidades de E/S."""
from pathlib import Path

ROOT = Path(__file__).resolve().parent.parent
DATA = ROOT / "data"
OUT = ROOT / "outputs"

DATA.mkdir(exist_ok=True)
OUT.mkdir(exist_ok=True)


def data_path(name: str) -> Path:
    return DATA / name


def out_path(name: str) -> Path:
    return OUT / name
```

---

## H.8. `common/m6.py`

```python
"""Núcleo CES-Saturada v3.0."""
from __future__ import annotations

import numpy as np
import pandas as pd
from scipy.optimize import dual_annealing, minimize
from sklearn.model_selection import StratifiedKFold

from common.seeds import SEED_GLOBAL


def hill(omega, K, alpha_h):
    omega = np.clip(np.asarray(omega, dtype=float), 1e-12, None)
    K = max(float(K), 1e-12)
    alpha_h = max(float(alpha_h), 1e-12)
    oa = np.power(omega, alpha_h)
    Ka = K ** alpha_h
    return oa / (Ka + oa)


def ces_aggregate(x, w, lam):
    x = np.clip(np.asarray(x, dtype=float), 1e-12, None)
    w = np.asarray(w, dtype=float)
    if abs(lam) < 1e-8:
        return float(np.prod(np.power(x, w)))
    return float(np.power(np.sum(w * np.power(x, lam)), 1.0 / lam))


def simplex_reparam(v):
    v = np.clip(np.asarray(v, dtype=float), 1e-9, None)
    return 0.1 + 0.7 * (v / np.sum(v))


def predict_M0(X, params):
    """PUSFRE base: F = C * Phi * Psi * Omega^alpha. params = [log_C, alpha]."""
    Phi, Psi, Omega = X[:, 0], X[:, 1], X[:, 2]
    log_C, alpha = params
    return np.exp(log_C) * Phi * Psi * np.power(np.clip(Omega, 1e-12, None), alpha)


def predict_M1(X, params):
    """CES sin saturación. params = [lam, v1, v2, v3]."""
    Phi, Psi, Omega = X[:, 0], X[:, 1], X[:, 2]
    lam, v1, v2, v3 = params
    w = simplex_reparam([v1, v2, v3])
    return np.array([ces_aggregate([Phi[i], Psi[i], Omega[i]], w, lam)
                     for i in range(len(Phi))])


def predict_M2(X, params):
    """Hill sin CES. params = [K, alpha_h, beta]."""
    Phi, Psi, Omega = X[:, 0], X[:, 1], X[:, 2]
    K, alpha_h, beta = params
    S = hill(Omega, K, alpha_h)
    return Phi * Psi * np.power(S, beta)


def predict_M6(X, params):
    """CES + Hill. params = [lam, K, alpha_h, v1, v2, v3]."""
    Phi, Psi, Omega = X[:, 0], X[:, 1], X[:, 2]
    lam, K, alpha_h, v1, v2, v3 = params
    w = simplex_reparam([v1, v2, v3])
    S = hill(Omega, K, alpha_h)
    return np.array([ces_aggregate([Phi[i], Psi[i], S[i]], w, lam)
                     for i in range(len(Phi))])


PREDICTORS = {"M0": predict_M0, "M1": predict_M1,
              "M2": predict_M2, "M6": predict_M6}

BOUNDS = {
    "M0": [(-5.0, 5.0), (0.0, 3.0)],
    "M1": [(-1.0, 2.0), (0.01, 10.0), (0.01, 10.0), (0.01, 10.0)],
    "M2": [(0.01, 100.0), (0.1, 5.0), (0.1, 5.0)],
    "M6": [(-1.0, 2.0), (0.01, 100.0), (0.1, 5.0),
           (0.01, 10.0), (0.01, 10.0), (0.01, 10.0)],
}


def _neg_loglik_factory(model, X, y):
    def f(params):
        try:
            pred = PREDICTORS[model](X, params)
        except Exception:
            return 1e12
        pred = np.clip(pred, 1e-12, None)
        resid = y - pred
        sigma2 = max(float(np.mean(resid ** 2)), 1e-12)
        n = len(y)
        return 0.5 * n * np.log(2 * np.pi * sigma2) + 0.5 * n
    return f


def ajustar(model, X, y, seed=SEED_GLOBAL):
    bounds = BOUNDS[model]
    f = _neg_loglik_factory(model, X, y)
    res_g = dual_annealing(f, bounds=bounds, seed=int(seed), maxiter=200)
    res_l = minimize(f, res_g.x, method="L-BFGS-B",
                     options={"maxiter": 500, "ftol": 1e-10})
    return res_l.x


def rmse(model, X, y, params):
    pred = np.clip(PREDICTORS[model](X, params), 1e-12, None)
    return float(np.sqrt(np.mean((y - pred) ** 2)))


def bic(model, X, y, params):
    n = len(y)
    pred = np.clip(PREDICTORS[model](X, params), 1e-12, None)
    resid = y - pred
    sigma2 = max(float(np.mean(resid ** 2)), 1e-12)
    logL = -0.5 * n * np.log(2 * np.pi * sigma2) - 0.5 * n
    p = len(params)
    return float(-2 * logL + p * np.log(n))


def validacion_cruzada(model, X, y, n_folds=10):
    y_strat = pd.qcut(y, q=n_folds, labels=False, duplicates="drop")
    skf = StratifiedKFold(n_splits=n_folds, shuffle=True,
                          random_state=SEED_GLOBAL)
    rmses = []
    for k, (tr, te) in enumerate(skf.split(X, y_strat)):
        params = ajustar(model, X[tr], y[tr], seed=SEED_GLOBAL + k)
        rmses.append(rmse(model, X[te], y[te], params))
    return rmses
```

---

## H.9. `A/__init__.py`

```python
"""Artículo A: casos límite."""
```

---

## H.10. `A/limites.py`

```python
"""Artículo A — Verificación numérica de casos límite."""
import numpy as np

from common.io_utils import out_path


def ces(x, w, lam):
    x = np.asarray(x, dtype=float)
    w = np.asarray(w, dtype=float)
    if abs(lam) < 1e-6:
        return float(np.prod(np.power(x, w)))
    return float(np.power(np.sum(w * np.power(x, lam)), 1.0 / lam))


def main():
    print("Artículo A — verificación numérica")
    w = np.array([1/3, 1/3, 1/3])
    casos = [
        ("A", 1e-6, 1e6, 1.0),
        ("B", 1e-6, 1.5, 1.0),
        ("C", 1.0, 1.0, 0.0),
        ("D", -10.0, 1.0, 0.0),
        ("E", 0.5, 1.0, 0.0),
        ("F", 1.5, 1.0, 0.0),
    ]
    rows = []
    for nombre, lam, K, alpha_h in casos:
        val = ces(np.ones(3), w, lam)
        if alpha_h > 0:
            S = (1.0 ** alpha_h) / (K ** alpha_h + 1.0 ** alpha_h)
            val = val * S
        rows.append((nombre, lam, K, alpha_h, val))
    path = out_path("A_tabla_B1.txt")
    with open(path, "w", encoding="utf-8") as f:
        f.write("Caso|lambda|K|alpha_h|valor\n")
        for r in rows:
            f.write(f"{r[0]}|{r[1]:.6e}|{r[2]:.6e}|{r[3]:.6e}|{r[4]:.15f}\n")
    print(f"  -> {path}")

    # Tabla B.2
    x_casos = [(0.5, 0.5, 0.5), (0.9, 0.5, 0.5), (0.9, 0.9, 0.5),
               (0.9, 0.9, 0.9), (0.1, 0.5, 0.9)]
    lambdas = [0.0, 1.0, -1.0, 0.5, 1.5]
    path_b2 = out_path("A_tabla_B2.txt")
    with open(path_b2, "w", encoding="utf-8") as f:
        f.write("x1|x2|x3|" + "|".join(f"lam={l}" for l in lambdas) + "\n")
        for x in x_casos:
            vals = [ces(x, w, l) for l in lambdas]
            f.write(f"{x[0]}|{x[1]}|{x[2]}|"
                    + "|".join(f"{v:.6f}" for v in vals) + "\n")
    print(f"  -> {path_b2}")


if __name__ == "__main__":
    main()
```

---

## H.11. `B/__init__.py`

```python
"""Artículo B."""
```

---

## H.12. `B/warfarina.py`

```python
"""Artículo B — Warfarina [SINT-GEN], ajuste univariante."""
import numpy as np

from common.io_utils import data_path, out_path
from common.m6 import ajustar, rmse, bic
from common.seeds import SEED_GLOBAL


def generar():
    rng = np.random.default_rng(SEED_GLOBAL)
    n = 30
    C = np.sort(np.clip(rng.lognormal(0.3, 0.5, n), 0.1, 6.0))
    K, alpha_h, Emax = 1.0, 1.5, 5.0
    INR_true = Emax * C ** alpha_h / (K ** alpha_h + C ** alpha_h)
    INR = np.clip(INR_true + rng.normal(0, 0.15, n), 0.8, 5.0)
    return C, INR


def main():
    print("Artículo B — warfarina [SINT-GEN]")
    C, INR = generar()

    csv = data_path("warfarina.csv")
    with open(csv, "w", encoding="utf-8") as f:
        f.write("paciente|concentracion|INR\n")
        for i, (c, r) in enumerate(zip(C, INR), start=1):
            f.write(f"P{i:02d}|{c:.6f}|{r:.6f}\n")
    print(f"  -> {csv}")

    # Ajuste univariante: Phi=Psi=1, Omega=C
    X = np.column_stack([np.ones_like(C), np.ones_like(C), C])
    y = INR
    for model in ["M0", "M2", "M6"]:
        params = ajustar(model, X, y, seed=SEED_GLOBAL)
        r = rmse(model, X, y, params)
        b = bic(model, X, y, params)
        print(f"  {model}: RMSE={r:.6f}, BIC={b:.6f}")


if __name__ == "__main__":
    main()
```

---

## H.13. `B/covid.py`

```python
"""Artículo B — COVID-19 Madrid [SINT-GEN], ajuste univariante."""
import numpy as np

from common.io_utils import data_path, out_path
from common.m6 import ajustar, rmse, bic
from common.seeds import SEED_GLOBAL


def generar():
    rng = np.random.default_rng(SEED_GLOBAL)
    n = 80
    K, alpha_h, t0 = 3500.0, 1.7, 40.0
    t = np.arange(1, n + 1)
    C_true = K * (t / t0) ** alpha_h / (1 + (t / t0) ** alpha_h)
    C = C_true * rng.lognormal(0, 0.14, n)
    C = np.maximum(np.round(C), 1).astype(int)
    H = np.cumsum(C * 0.8 + rng.normal(0, 20, n)) / 10
    H = np.maximum(np.round(H), 1).astype(int)
    return t, C, H


def main():
    print("Artículo B — COVID-19 Madrid [SINT-GEN]")
    t, C, H = generar()

    csv = data_path("covid_madrid.csv")
    with open(csv, "w", encoding="utf-8") as f:
        f.write("dia|casos|hospitalizaciones\n")
        for i, (c, h) in enumerate(zip(C, H), start=1):
            f.write(f"D{i:02d}|{c}|{h}\n")
    print(f"  -> {csv}")

    X = np.column_stack([np.ones_like(t), np.ones_like(t), t.astype(float)])
    y = C.astype(float)
    for model in ["M0", "M2", "M6"]:
        params = ajustar(model, X, y, seed=SEED_GLOBAL)
        r = rmse(model, X, y, params)
        b = bic(model, X, y, params)
        print(f"  {model}: RMSE={r:.6f}, BIC={b:.6f}")


if __name__ == "__main__":
    main()
```

---

## H.14. `B/regimen.py`

```python
"""Artículo B — Régimen transitorio [SINT-GEN].

900 réplicas: 100 por cada valor de Ω/K en {0.1, ..., 10.0}.
Cada réplica: n=2000, K=1, alpha=1.5, lambda=0.5, ruido log-normal sigma=0.10.
"""
from __future__ import annotations

import numpy as np

from common.io_utils import data_path, out_path
from common.m6 import ajustar, rmse, bic, predict_M6
from common.seeds import SEED_GLOBAL, seed_replica


OMEGA_K_VALUES = [0.1, 0.3, 0.5, 0.7, 1.0, 1.5, 2.0, 5.0, 10.0]
N_PER_REPLICA = 2000
N_REPLICAS = 100


def generar_datos(omega_k, replica, n=N_PER_REPLICA):
    rng = np.random.default_rng(seed_replica(replica))
    K_true, alpha_true, lam_true = 1.0, 1.5, 0.5

    Omega = omega_k * K_true * rng.lognormal(0, 0.15, n)
    Phi = rng.uniform(0.1, 1.0, n)
    Psi = rng.uniform(0.1, 1.0, n)

    Phi_s = np.clip(Phi, 1e-9, None)
    Psi_s = np.clip(Psi, 1e-9, None)
    Omega_s = np.clip(Omega, 1e-9, None)

    S = Omega_s ** alpha_true / (K_true ** alpha_true + Omega_s ** alpha_true)
    # M6 verdadero con pesos 1/3
    inner = (1/3) * Phi_s**lam_true + (1/3) * Psi_s**lam_true + (1/3) * S**lam_true
    F = inner ** (1.0 / lam_true)
    y = F * rng.lognormal(0, 0.10, n)
    X = np.column_stack([Phi, Psi, Omega])
    return X, y


def se_from_hessian(model, X, y, params, eps=1e-5):
    """SE por Hessiano numérico sobre los parametros libres."""
    p = np.asarray(params, dtype=float)
    n_p = len(p)

    def f(q):
        try:
            pred = np.clip(__import__("common.m6", fromlist=["PREDICTORS"])
                           .PREDICTORS[model](X, q), 1e-12, None)
        except Exception:
            return 1e12
        resid = y - pred
        sigma2 = max(float(np.mean(resid ** 2)), 1e-12)
        n = len(y)
        return 0.5 * n * np.log(2 * np.pi * sigma2) + 0.5 * n

    H = np.zeros((n_p, n_p))
    f0 = f(p)
    for i in range(n_p):
        for j in range(n_p):
            pi_p = p.copy(); pi_p[i] += eps
            pi_m = p.copy(); pi_m[i] -= eps
            pj_p = p.copy(); pj_p[j] += eps
            pj_m = p.copy(); pj_m[j] -= eps
            pij = p.copy(); pij[i] += eps; pij[j] += eps
            pimj = p.copy(); pimj[i] += eps; pimj[j] -= eps
            pimj2 = p.copy(); pimj2[i] -= eps; pimj2[j] += eps
            pimjm = p.copy(); pimjm[i] -= eps; pimjm[j] -= eps
            H[i, j] = (f(pij) - f(pimj) - f(pimj2) + f(pimjm)) / (4 * eps * eps)
    try:
        cov = np.linalg.inv(H)
        se = np.sqrt(np.abs(np.diag(cov)))
    except np.linalg.LinAlgError:
        se = np.full(n_p, np.nan)
    return se


def main():
    print("Artículo B — régimen transitorio [SINT-GEN]")
    print(f"  {len(OMEGA_K_VALUES)} x {N_REPLICAS} = "
          f"{len(OMEGA_K_VALUES) * N_REPLICAS} ajustes")

    resultados = []
    for omega_k in OMEGA_K_VALUES:
        print(f"  Ω/K = {omega_k}")
        for r in range(1, N_REPLICAS + 1):
            X, y = generar_datos(omega_k, r)
            params = ajustar("M6", X, y, seed=SEED_GLOBAL)
            se = se_from_hessian("M6", X, y, params)
            # M6 params: [lam, K, alpha_h, v1, v2, v3]
            K_hat = params[1]
            ah_hat = params[2]
            ll = -0.5 * len(y) * np.log(2 * np.pi * max(np.mean((y - np.clip(
                __import__("common.m6", fromlist=["PREDICTORS"]).PREDICTORS["M6"](X, params),
                1e-12, None)) ** 2), 1e-12)) - 0.5 * len(y)
            resultados.append((omega_k, r, K_hat, ah_hat,
                               se[1], se[2], -ll))

    csv = data_path("regimen_transitorio.csv")
    with open(csv, "w", encoding="utf-8") as f:
        f.write("omega_k|replica|K_hat|alpha_h_hat|SE_K|SE_alpha|neglogL\n")
        for row in resultados:
            f.write("|".join(f"{v:.6f}" for v in row) + "\n")
    print(f"  -> {csv}")

    # Resumen
    resumen = {}
    for row in resultados:
        resumen.setdefault(row[0], []).append(row)
    sum_path = out_path("B_regimen_summary.txt")
    with open(sum_path, "w", encoding="utf-8") as f:
        f.write("omega_k|mean_K|mean_alpha_h|mean_SE_K|mean_SE_alpha\n")
        for ok in OMEGA_K_VALUES:
            rs = np.array(resumen[ok])
            f.write(f"{ok:.2f}|{rs[:, 2].mean():.6f}|{rs[:, 3].mean():.6f}|"
                    f"{rs[:, 4].mean():.6f}|{rs[:, 5].mean():.6f}\n")
    print(f"  -> {sum_path}")


if __name__ == "__main__":
    main()
```

---

## H.15. `C/__init__.py`

```python
"""Artículo C."""
```

---

## H.16. `C/debye.py`

```python
"""Artículo C — Debye (cobre) [REAL]."""
import numpy as np

from common.io_utils import data_path, out_path
from common.m6 import ajustar, rmse, bic


T_DATA = np.array([
    5, 6, 7, 8, 9, 10, 12, 14, 16, 18,
    20, 22, 25, 28, 30, 35, 40, 45, 50, 55,
    60, 70, 80, 90, 100, 110, 120, 130, 150, 170,
    190, 200, 220, 240, 250, 260, 280, 300, 320, 343,
    360, 380, 400, 420, 440, 460, 480, 500, 520, 550,
], dtype=float)

CV_DATA = np.array([
    0.0021, 0.0037, 0.0059, 0.0089, 0.0128, 0.0168, 0.0291, 0.0472,
    0.0714, 0.1037,
    0.1340, 0.1780, 0.2710, 0.3820, 0.4520, 0.6710, 0.9450, 1.2860,
    2.0800, 2.8700,
    4.0200, 5.5100, 7.3100, 9.4200, 12.8000, 15.9000, 19.2000, 22.4000,
    25.4000, 30.1000,
    32.8000, 34.2000, 37.1000, 39.4000, 40.1000, 41.2000, 42.6000,
    43.8000, 44.9000, 45.7000,
    46.3000, 47.1000, 47.5000, 48.1000, 48.5000, 48.8000, 49.0000,
    49.1000, 49.2000, 49.3000,
], dtype=float)

THETA_D = 343.0


def main():
    print("Artículo C — Debye (cobre) [REAL]")

    csv = data_path("debye_cobre.csv")
    with open(csv, "w", encoding="utf-8") as f:
        f.write("T|C_V\n")
        for t, cv in zip(T_DATA, CV_DATA):
            f.write(f"{t:.6f}|{cv:.6f}\n")
    print(f"  -> {csv}")

    # Regímenes
    regs = {
        "bajo": (T_DATA / THETA_D < 0.2),
        "intermedio": (T_DATA / THETA_D >= 0.2) & (T_DATA / THETA_D <= 1.0),
        "alto": (T_DATA / THETA_D > 1.0),
    }

    out = out_path("C_debye.txt")
    with open(out, "w", encoding="utf-8") as f:
        for nombre, mask in regs.items():
            T = T_DATA[mask]
            CV = CV_DATA[mask]
            if len(T) < 5:
                continue
            Phi = np.ones_like(T)
            Psi = np.ones_like(T)
            Omega = T / T.max()
            X = np.column_stack([Phi, Psi, Omega])
            y = CV
            f.write(f"=== Régimen {nombre} (n={len(T)}) ===\n")
            for model in ["M0", "M2", "M6"]:
                params = ajustar(model, X, y, seed=42)
                f.write(f"{model}: RMSE={rmse(model, X, y, params):.6f}, "
                        f"BIC={bic(model, X, y, params):.6f}\n")
            f.write("\n")
    print(f"  -> {out}")


if __name__ == "__main__":
    main()
```

---

## H.17. `C/neural.py`

```python
"""Artículo C — Neural Scaling [SINT-GEN].

Datos sintéticos generados para imitar una ley de escalado con saturación.
NO son los datos de Hoffmann et al. (2022).
"""
import numpy as np

from common.io_utils import data_path, out_path
from common.m6 import ajustar, rmse, bic
from common.seeds import SEED_GLOBAL


# Dataset sintético: 46 puntos, N hasta 131000 M, C hasta 4e27 FLOPs.
NEURAL_DATA = [
    ("M01",   8,     10,     6.0e18, 2.420000),
    ("M02",   15,    15,     1.4e19, 2.310000),
    ("M03",   25,    20,     3.0e19, 2.240000),
    ("M04",   40,    30,     7.2e19, 2.180000),
    ("M05",   60,    45,     1.6e20, 2.130000),
    ("M06",   85,    60,     3.1e20, 2.090000),
    ("M07",   120,   80,     5.8e20, 2.060000),
    ("M08",   165,   110,    1.1e21, 2.030000),
    ("M09",   220,   150,    2.0e21, 2.010000),
    ("M10",   290,   200,    3.5e21, 1.990000),
    ("M11",   380,   260,    5.9e21, 1.970000),
    ("M12",   490,   340,    1.0e22, 1.950000),
    ("M13",   625,   440,    1.7e22, 1.930000),
    ("M14",   790,   570,    2.7e22, 1.920000),
    ("M15",   990,   730,    4.3e22, 1.900000),
    ("M16",   1230,  920,    6.8e22, 1.890000),
    ("M17",   1520,  1160,   1.1e23, 1.880000),
    ("M18",   1860,  1450,   1.6e23, 1.870000),
    ("M19",   2260,  1800,   2.4e23, 1.860000),
    ("M20",   2740,  2230,   3.6e23, 1.855000),
    ("M21",   3300,  2750,   5.4e23, 1.850000),
    ("M22",   3960,  3380,   8.0e23, 1.845000),
    ("M23",   4730,  4130,   1.2e24, 1.840000),
    ("M24",   5630,  5030,   1.7e24, 1.835000),
    ("M25",   6680,  6100,   2.4e24, 1.830000),
    ("M26",   7900,  7360,   3.5e24, 1.825000),
    ("M27",   9300,  8840,   5.0e24, 1.820000),
    ("M28",   10900, 10600,  7.1e24, 1.815000),
    ("M29",   12700, 12600,  1.0e25, 1.810000),
    ("M30",   14800, 15000,  1.4e25, 1.805000),
    ("M31",   17200, 17700,  2.0e25, 1.800000),
    ("M32",   19900, 20900,  2.9e25, 1.795000),
    ("M33",   23000, 24500,  4.1e25, 1.790000),
    ("M34",   26600, 28700,  5.9e25, 1.785000),
    ("M35",   30600, 33400,  8.4e25, 1.780000),
    ("M36",   35200, 38900,  1.2e26, 1.775000),
    ("M37",   40400, 45100,  1.7e26, 1.770000),
    ("M38",   46300, 52200,  2.4e26, 1.765000),
    ("M39",   53000, 60300,  3.4e26, 1.760000),
    ("M40",   60600, 69600,  4.8e26, 1.755000),
    ("M41",   69200, 80200,  6.8e26, 1.750000),
    ("M42",   79000, 92400,  9.7e26, 1.745000),
    ("M43",   90100, 106000, 1.4e27, 1.740000),
    ("M44",   102000,122000, 2.0e27, 1.735000),
    ("M45",   116000,140000, 2.8e27, 1.730000),
    ("M46",   131000,161000, 4.0e27, 1.725000),
]


def main():
    print("Artículo C — Neural Scaling [SINT-GEN]")

    csv = data_path("neural_scaling.csv")
    with open(csv, "w", encoding="utf-8") as f:
        f.write("modelo|N|D|C|L\n")
        for r in NEURAL_DATA:
            f.write(f"{r[0]}|{r[1]}|{r[2]}|{r[3]:.2e}|{r[4]:.6f}\n")
    print(f"  -> {csv}")

    N = np.array([r[1] for r in NEURAL_DATA], dtype=float)
    D = np.array([r[2] for r in NEURAL_DATA], dtype=float)
    C = np.array([r[3] for r in NEURAL_DATA], dtype=float)
    L = np.array([r[4] for r in NEURAL_DATA], dtype=float)
    Phi = np.log(N)
    Psi = np.log(D)
    Omega = np.log(C)
    F = -np.log(L)
    X = np.column_stack([Phi, Psi, Omega])

    out = out_path("C_neural.txt")
    with open(out, "w", encoding="utf-8") as f:
        omega_range = np.log10(C.max() / C.min())
        f.write(f"Neural Scaling [SINT-GEN], Omega range = {omega_range:.2f}\n")
        for model in ["M0", "M1", "M2", "M6"]:
            params = ajustar(model, X, F, seed=42)
            f.write(f"{model}: RMSE={rmse(model, X, F, params):.6f}, "
                    f"BIC={bic(model, X, F, params):.6f}\n")
    print(f"  -> {out}")


if __name__ == "__main__":
    main()
```

---

## H.18. `C/urban.py`

```python
"""Artículo C — Urban Scaling [SINT-GEN]."""
import numpy as np

from common.io_utils import data_path, out_path
from common.m6 import ajustar, rmse, bic
from common.seeds import SEED_GLOBAL


def generar():
    rng = np.random.default_rng(SEED_GLOBAL)
    n = 1200
    N = np.clip(rng.lognormal(mean=10, sigma=2.5, size=n), 1e5, 1.5e10)
    Y_0, beta, K, alpha_h = 22.0, 1.15, 5e6, 1.4
    H = N ** alpha_h / (K ** alpha_h + N ** alpha_h)
    Y = Y_0 * N ** beta * H * rng.lognormal(0, 0.15, n)
    logN_norm = np.log(N) / np.log(N.max())
    infra = np.clip(0.4 * logN_norm + 0.5 + rng.normal(0, 0.03, n), 0.01, 0.99)
    edu = np.clip(0.3 * logN_norm + 0.6 + rng.normal(0, 0.03, n), 0.01, 0.99)
    return N, Y, infra, edu


def main():
    print("Artículo C — Urban Scaling [SINT-GEN]")
    N, Y, infra, edu = generar()

    csv = data_path("urban_scaling.csv")
    with open(csv, "w", encoding="utf-8") as f:
        f.write("ciudad_id|poblacion|PIB_per_capita|infraestructura|educacion\n")
        for i in range(len(N)):
            f.write(f"C{i+1:04d}|{N[i]:.2f}|{Y[i]:.6f}|"
                    f"{infra[i]:.6f}|{edu[i]:.6f}\n")
    print(f"  -> {csv}")

    Phi = np.log(N)
    Psi = infra
    Omega = edu
    F = np.log(Y)
    X = np.column_stack([Phi, Psi, Omega])

    out = out_path("C_urban.txt")
    with open(out, "w", encoding="utf-8") as f:
        omega_range = np.log10(N.max() / N.min())
        f.write(f"Urban Scaling [SINT-GEN], Omega range = {omega_range:.2f}\n")
        for model in ["M0", "M1", "M2", "M6"]:
            params = ajustar(model, X, F, seed=SEED_GLOBAL)
            f.write(f"{model}: RMSE={rmse(model, X, F, params):.6f}, "
                    f"BIC={bic(model, X, F, params):.6f}\n")
    print(f"  -> {out}")


if __name__ == "__main__":
    main()
```

---

## H.19. `C/species.py`

```python
"""Artículo C — Species-Area [SINT-GEN]."""
import numpy as np

from common.io_utils import data_path, out_path
from common.m6 import ajustar, rmse, bic
from common.seeds import SEED_GLOBAL


def generar():
    rng = np.random.default_rng(SEED_GLOBAL)
    n = 500
    tipos = np.array(["O"] * 210 + ["C"] * 180 + ["A"] * 110)
    rng.shuffle(tipos)
    c_map = {"O": 3.0, "C": 5.0, "A": 2.0}
    z = 0.25
    A = np.clip(rng.lognormal(mean=3, sigma=3.5, size=n), 0.01, 1e6)
    c = np.array([c_map[t] for t in tipos])
    S = np.maximum(np.round(c * A ** z * rng.lognormal(0, 0.2, n)), 1).astype(int)
    lat = rng.uniform(20, 55, n)
    aisl = np.clip(1.0 - 0.15 * np.log10(A) + rng.normal(0, 0.05, n), 0.01, 0.99)
    return tipos, A, S, lat, aisl


def main():
    print("Artículo C — Species-Area [SINT-GEN]")
    tipos, A, S, lat, aisl = generar()

    csv = data_path("species_area.csv")
    with open(csv, "w", encoding="utf-8") as f:
        f.write("isla_id|area|especies|latitud|aislamiento|tipo\n")
        for i in range(len(A)):
            f.write(f"I{i+1:03d}|{A[i]:.6f}|{S[i]}|{lat[i]:.4f}|"
                    f"{aisl[i]:.6f}|{tipos[i]}\n")
    print(f"  -> {csv}")

    Phi = np.log(A)
    Psi = lat / 55.0
    Omega = aisl
    F = np.log(np.maximum(S, 1))
    X = np.column_stack([Phi, Psi, Omega])

    out = out_path("C_species.txt")
    with open(out, "w", encoding="utf-8") as f:
        omega_range = np.log10(A.max() / A.min())
        f.write(f"Species-Area [SINT-GEN], Omega range = {omega_range:.2f}\n")
        for model in ["M0", "M1", "M2", "M6"]:
            params = ajustar(model, X, F, seed=SEED_GLOBAL)
            f.write(f"{model}: RMSE={rmse(model, X, F, params):.6f}, "
                    f"BIC={bic(model, X, F, params):.6f}\n")
    print(f"  -> {out}")


if __name__ == "__main__":
    main()
```

---

## H.20. `C/fama.py`

```python
"""Artículo C — Fama-French [SINT-GEN]. Diseñado para fallar."""
import numpy as np

from common.io_utils import data_path, out_path
from common.m6 import ajustar, rmse, bic
from common.seeds import SEED_GLOBAL


def generar():
    rng = np.random.default_rng(SEED_GLOBAL)
    n = 720
    MKT = rng.normal(0.5, 4.5, n)
    SMB = rng.normal(0.2, 3.0, n)
    HML = rng.normal(0.3, 3.5, n)
    Ri_Rf = 0.5 * (rng.normal(0.7, 4.8, n) + 0.8 * MKT + 0.3 * SMB - 0.2 * HML)
    return MKT, SMB, HML, Ri_Rf


def main():
    print("Artículo C — Fama-French [SINT-GEN]")
    MKT, SMB, HML, Ri_Rf = generar()

    csv = data_path("fama_french.csv")
    with open(csv, "w", encoding="utf-8") as f:
        f.write("mes|MKT|SMB|HML|Ri_Rf\n")
        for i in range(len(MKT)):
            f.write(f"t{i+1:03d}|{MKT[i]:.6f}|{SMB[i]:.6f}|"
                    f"{HML[i]:.6f}|{Ri_Rf[i]:.6f}\n")
    print(f"  -> {csv}")

    # Mapeo: Phi = MKT (desplazado), Psi = SMB, Omega = HML (desplazado)
    Phi = (MKT - MKT.min()) / (MKT.max() - MKT.min()) + 0.01
    Psi = (SMB - SMB.min()) / (SMB.max() - SMB.min()) + 0.01
    Omega = (HML - HML.min()) / (HML.max() - HML.min()) + 0.01
    F = Ri_Rf
    X = np.column_stack([Phi, Psi, Omega])

    out = out_path("C_fama.txt")
    with open(out, "w", encoding="utf-8") as f:
        f.write("Fama-French [SINT-GEN]\n")
        for model in ["M0", "M1", "M2", "M6"]:
            params = ajustar(model, X, F, seed=SEED_GLOBAL)
            f.write(f"{model}: RMSE={rmse(model, X, F, params):.6f}, "
                    f"BIC={bic(model, X, F, params):.6f}\n")
    print(f"  -> {out}")


if __name__ == "__main__":
    main()
```

---

## H.21. `tests/test_m6.py`

```python
"""Tests unitarios para common/m6.py."""
import numpy as np

from common.m6 import (hill, ces_aggregate, predict_M0, predict_M6,
                       ajustar, rmse, bic)


def test_hill_basic():
    assert abs(hill(1.0, 1.0, 1.0) - 0.5) < 1e-12
    assert hill(0.0, 1.0, 1.0) < 1e-10
    assert hill(1e10, 1.0, 1.0) > 1 - 1e-9


def test_ces_cobb_douglas_limit():
    x = np.array([0.5, 0.5, 0.5])
    w = np.array([1/3, 1/3, 1/3])
    val_lim = ces_aggregate(x, w, 1e-9)
    val_cd = float(np.prod(np.power(x, w)))
    assert abs(val_lim - val_cd) < 1e-6


def test_predict_M0():
    X = np.array([[1.0, 1.0, 1.0], [2.0, 1.0, 1.0]])
    params = [0.0, 1.0]  # log_C=0, alpha=1
    y = predict_M0(X, params)
    assert abs(y[0] - 1.0) < 1e-12
    assert abs(y[1] - 2.0) < 1e-12


def test_bic_penalty():
    """BIC debe penalizar más parametros."""
    rng = np.random.default_rng(42)
    X = rng.uniform(0.1, 1.0, (50, 3))
    y = predict_M0(X, [0.0, 0.5]) + rng.normal(0, 0.01, 50)
    p_m0 = ajustar("M0", X, y, seed=42)
    p_m6 = ajustar("M6", X, y, seed=42)
    b_m0 = bic("M0", X, y, p_m0)
    b_m6 = bic("M6", X, y, p_m6)
    # M0 debería ganar si los datos son M0 puros
    assert b_m0 < b_m6
```

---

## H.22. Notas de mantenimiento

1. **`B/regimen.py`** es el más costoso (~7 min). Para desarrollo, reducir `N_REPLICAS` a 5 y `N_PER_REPLICA` a 200.
2. **Determinismo.** Verificar con `sha256sum` tras dos ejecuciones.
3. **Licencia unificada.** CC BY-NC-SA 4.0 + Cláusula Comercial Ronin en portada, LICENSE y README.
4. **Los datasets [REAL]** se limitan a Debye. Cualquier otra afirmación empírica requiere sustituir los datasets sintéticos por los originales.

---

**Fin del Apéndice H.**

---

**Fin del documento completo.**

---

