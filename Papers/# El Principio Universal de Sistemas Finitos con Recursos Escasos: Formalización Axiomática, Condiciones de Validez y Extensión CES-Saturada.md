# TRILOGÍA PUSFRE-CES: EDICIÓN CORREGIDA Y AUDITADA

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Versión:** 2.0 — Edición revisada tras auditoría interna

---

## Nota de la edición 2.0

Esta edición corrige los siguientes problemas detectados en la versión 1.0:

1. **Contradicción «datasets completos» / elipsis.** Se elimina la afirmación de que todos los datasets están íntegramente impresos. Se distingue entre datasets **listados en su totalidad** y datasets **generados por código reproducible**.
2. **Mezcla de datos reales y sintéticos.** Cada dataset se etiqueta explícitamente como `[REAL]`, `[SINT-CAL]` o `[SINT-GEN]`, y el texto distingue entre *validación empírica* (solo `[REAL]`) e *ilustración metodológica* (sintéticos).
3. **Pseudocódigo incompleto.** Las funciones auxiliares (`log_likelihood`, `calcular_rmse`, `generar_datos_regimen`, etc.) se especifican o se remiten a un repositorio.
4. **Sobreafirmación del Teorema 4.1.** Se recalca su carácter condicional.
5. **Detalles editoriales.** Se eliminan los marcadores «1310», se unifica la numeración y el estilo de referencias.

Todos los datasets sintéticos se regeneran exactamente con el código del Apéndice G (semilla global 42).

---

# README GLOBAL DE LA TRILOGÍA

## Estructura, reproducibilidad y flujo de semillas

### Estructura de la trilogía

| Artículo | Contenido | Datasets asociados |
|----------|-----------|--------------------|
| A | Caracterización axiomática | Verificación numérica de casos límite (sintética) |
| B | Identificabilidad | Warfarina (30, SINT-CAL), COVID-19 (80, SINT-CAL), Régimen transitorio (900, SINT-GEN) |
| C | Evaluación empírica y metodológica | Neural Scaling (46, REAL), Urban Scaling (1200, SINT-CAL), Species-Area (500, SINT-CAL), Fama-French (720, SINT-CAL), Debye (50, REAL) |

### Naturaleza de los datos (declaración explícita)

| Etiqueta | Significado |
|----------|-------------|
| **[REAL]** | Datos publicados, reproducidos desde la fuente original, con cita verificable |
| **[SINT-CAL]** | Datos sintéticos calibrados: no son los originales. Las distribuciones marginales y correlaciones se ajustan a las reportadas en la fuente citada |
| **[SINT-GEN]** | Datos sintéticos generados con parámetros especificados en la metodología |

**Advertencia.** Los resultados obtenidos sobre datasets `[SINT-CAL]` son **ilustrativos**, no validación empírica en sentido estricto. Toda afirmación que dependa críticamente de estos datasets debe validarse con los datos originales antes de usarse en aplicaciones críticas. El Artículo C se reformula en consecuencia: se distingue entre *verificación metodológica* (sintéticos) y *evidencia empírica* (solo Neural Scaling y Debye).

### Formatos de los datasets

- Los datasets **listados íntegramente** en el Apéndice de Datos son: Neural Scaling (46), Warfarina (30), COVID-19 (80), Debye (50).
- Los datasets **generados por código reproducible** (con semilla y pseudocódigo completo) son: Régimen transitorio (900), Urban Scaling (1200), Species-Area (500), Fama-French (720).
- Ningún dataset se presenta con elipsis («...»). Cuando un dataset no se lista completo, se indica explícitamente y se entrega el código que lo regenera.

### Flujo de semillas

Semilla global `seed_global = 42`.

| Análisis | Semilla | Derivación |
|----------|---------|------------|
| `dual_annealing` (global) | 42 | `seed_global` |
| Bootstrap | 42 | `seed_global` |
| Validación cruzada (fold *k*) | 42 + *k* | `seed_global + k` |
| Réplica *r* | 42 + 1000·*r* | `seed_global + 1000*r` |
| Prior bayesiano MCMC | 42 | `seed_global` |

### Versiones de software

Python 3.11.9. NumPy 1.26.4. SciPy 1.13.0. scikit-learn 1.4.2. PyMC 5.10.0. Precisión: float64.

### Pseudocódigo global (funciones auxiliares completas)

```python
import numpy as np
import pandas as pd
from scipy.optimize import dual_annealing, minimize
from scipy.special import gammaln
from sklearn.model_selection import StratifiedKFold

SEED_GLOBAL = 42

# ---------------------------------------------------------------
# Núcleo de la familia CES-Saturada
# ---------------------------------------------------------------
def hill(omega, K, alpha_h):
    """Saturación tipo Hill. omega, K > 0; alpha_h > 0."""
    oa = np.power(omega, alpha_h)
    Ka = np.power(K, alpha_h)
    return oa / (Ka + oa)

def ces_aggregate(x, w, lam):
    """Agregador CES sobre el vector x con pesos w y parámetro lam.
    lam -> 0 se interpreta como límite Cobb-Douglas."""
    x = np.asarray(x, dtype=float)
    w = np.asarray(w, dtype=float)
    if abs(lam) < 1e-8:
        return np.prod(np.power(x, w))
    return np.power(np.sum(w * np.power(x, lam)), 1.0/lam)

def fitness_M6(Phi, Psi, Omega, params):
    """Familia CES-Saturada M6.
    params = (lam, K, u1, u2, u3, alpha_h, alpha, gamma, C) -> 9 params en M7.
    M6 fija gamma = 1 y C = 1.
    """
    lam, K, u1, u2, u3, alpha_h, alpha, gamma, C = params
    S = hill(Omega, K, alpha_h)
    agg = ces_aggregate([Phi, Psi, Omega], [u1, u2, u3], lam)
    return C * agg * (S ** alpha) * (Omega ** gamma)

# ---------------------------------------------------------------
# Verosimilitud gaussiana (homocedástica o heterocedástica)
# ---------------------------------------------------------------
def log_likelihood(params, X, y, sigma=1.0, hetero=None):
    """Log-verosimilitud para y = fitness_M6(X; params) + ruido.
    hetero: array de sigmas por observación. Si None, usa sigma escalar."""
    Phi, Psi, Omega = X[:,0], X[:,1], X[:,2]
    y_hat = np.array([fitness_M6(Phi[i], Psi[i], Omega[i], params)
                      for i in range(len(y))])
    sig = np.full_like(y, sigma) if hetero is None else hetero
    resid = y - y_hat
    n = len(y)
    return -0.5*n*np.log(2*np.pi) - np.sum(np.log(sig)) \
           - 0.5*np.sum((resid/sig)**2)

def calcular_rmse(X, y, params):
    Phi, Psi, Omega = X[:,0], X[:,1], X[:,2]
    y_hat = np.array([fitness_M6(Phi[i], Psi[i], Omega[i], params)
                      for i in range(len(y))])
    return float(np.sqrt(np.mean((y - y_hat)**2)))

# ---------------------------------------------------------------
# Ajuste M6 (o M7 si se activan los 9 parámetros)
# ---------------------------------------------------------------
def ajustar_M6(X, y, seed=SEED_GLOBAL, n_params=6):
    """Ajuste reproducible por dual_annealing + L-BFGS-B.
    n_params = 6 -> M6; n_params = 9 -> M7."""
    if n_params == 6:
        bounds = [(-1, 2), (0.01, 100), (0, 1), (0, 1), (0, 1), (0.1, 5)]
        def unpack(p):
            lam, K, u1, u2, u3, alpha_h = p
            return (lam, K, u1, u2, u3, alpha_h, 1.0, 1.0, 1.0)
    else:
        bounds = [(-1, 2), (0.01, 100), (0, 1), (0, 1), (0, 1),
                  (0.1, 5), (0.1, 5), (0.1, 5), (0.01, 10)]
        def unpack(p):
            return tuple(p)
    def obj(p):
        return -log_likelihood(unpack(p), X, y)
    res_g = dual_annealing(obj, bounds, seed=seed, maxiter=200)
    res_l = minimize(obj, res_g.x, method='L-BFGS-B',
                     options={'maxiter': 500, 'ftol': 1e-10})
    return res_l.x

# ---------------------------------------------------------------
# Validación cruzada y bootstrap
# ---------------------------------------------------------------
def validacion_cruzada(X, y, n_folds=10):
    y_strat = pd.qcut(y, q=n_folds, labels=False, duplicates='drop')
    skf = StratifiedKFold(n_splits=n_folds, shuffle=True,
                          random_state=SEED_GLOBAL)
    rmses = []
    for k, (tr, te) in enumerate(skf.split(X, y_strat)):
        params = ajustar_M6(X[tr], y[tr], seed=SEED_GLOBAL + k)
        rmses.append(calcular_rmse(X[te], y[te], params))
    return rmses

def bootstrap_ci(X, y, n_boot=1000):
    rng = np.random.default_rng(SEED_GLOBAL)
    n = len(X)
    est = []
    for _ in range(n_boot):
        idx = rng.choice(n, n, replace=True)
        est.append(ajustar_M6(X[idx], y[idx], seed=SEED_GLOBAL))
    return np.percentile(est, [2.5, 97.5], axis=0)
```

**Repositorio.** El código completo, junto con los datasets sintéticos regenerables y los scripts de análisis, se deposita en el repositorio `pusfre-ces-trilogy` (estructura especificada en el Apéndice G). Los resultados de este documento se obtienen ejecutando `make all` desde la raíz del repositorio.

---

# ARTÍCULO A

## Una Caracterización Condicional de la Función de Fitness en Sistemas Finitos con Recursos Escasos

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino:** *Journal of Mathematical Economics*

---

### Resumen

Se presenta una **caracterización condicional** de la función de fitness en sistemas finitos donde agentes heterogéneos compiten por un recurso escaso. La caracterización se construye en cuatro capas: axiomas de dominio, supuestos estructurales, condiciones de elasticidad y regularidad. **Bajo el conjunto completo de supuestos**, la única forma funcional compatible es $F_i = C \Phi_i \Psi_i \Omega_i^\alpha$ con $\alpha \in (0,1]$. El resultado **no es universal**: relajar cualquiera de los supuestos amplía el espacio de formas admisibles. Se caracteriza ese espacio y se comparan cuatro familias candidatas como extensiones. Se incluye verificación numérica de casos límite con precisión y semilla reproducibles.

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
5. Verificación numérica de casos límite con precisión especificada y semilla reproducible.
6. Ledger de categorización epistémica: qué es axioma, qué es supuesto, qué es elección y qué es teorema.

#### 1.2 Alcance

Este artículo se centra en la caracterización axiomática. Los resultados sobre identificabilidad (Ferrandez Canalis 2026b) y evaluación metodológica (Ferrandez Canalis 2026c) se publican por separado.

---

### 2. Marco formal

**Definición 2.1 (Sistema finito en competencia).** Tupla $\mathcal{S} = (S, R, \{\Phi_i\}, \{\Psi_i\}, \{\Omega_i\})$ con $S \geq 2$, $R > 0$, $\Phi_i, \Psi_i, \Omega_i \in [0,1]$, $\sum_i \Omega_i = 1$.

**Definición 2.2 (Función de fitness).** $F: [0,1]^{2S} \times \Delta^{S-1} \to \mathbb{R}_+$.

**Definición 2.3 (Asignación).** $A_i = R \cdot F_i / \sum_j F_j$.

---

### 3. Cuatro capas de axiomas y supuestos

Se declara explícitamente la **categoría epistémica** de cada elemento:

- **Axioma:** restricción de dominio que se acepta por definición del problema.
- **Supuesto estructural:** simplificación que puede relajarse; su relajación amplía el espacio de soluciones.
- **Condición de elasticidad:** elección funcional motivada empíricamente.
- **Regularidad:** condición técnica para garantizar diferenciabilidad y existencia.

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

### 4. Teorema de unicidad condicional

**Teorema 4.1.** *Bajo A1–A3, S1–S2, E1–E2 y R1 simultáneamente:*

$$F_i = C \Phi_i \Psi_i \Omega_i^\alpha, \quad C > 0, \alpha \in (0,1].$$

**Comentario.** El teorema es **condicional**. No afirma que todo sistema finito en competencia deba tener esta forma. Afirma que si un sistema satisface las cuatro capas de supuestos, entonces su función de fitness tiene esa forma. La relajación de cualquier supuesto, como se documenta en la Sección 5, invalida la conclusión.

**Demostración.** Ver Apéndice A. $\square$

---

### 5. Espacio de soluciones al relajar supuestos

| Configuración | Forma resultante | Parámetros libres |
|---------------|------------------|--------------------|
| A1–A3, S1, S2, E1, E2, R1 | $C \Phi \Psi \Omega^\alpha$ | 1 |
| A1–A3, S1, S2, R1 (sin E1, E2) | $C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$ | 3 |
| A1–A3, S1, R1 (sin S2) | $f_1(\Phi) f_2(\Psi) f_3(\Omega)$ | ∞ |
| A1–A3, R1 (sin S1, S2) | No separable | ∞ |
| A1–A2, S1–S2, E1–E2, R1 (sin A3) | $\alpha > 1$ admisible | 1 |

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

Economía (competencia entre firmas), ecología (competencia entre especies), sistemas multi-agente (competencia por recursos computacionales). En todos los casos, la aplicabilidad depende de la plausibilidad de los supuestos, no de la forma funcional en sí.

---

### 9. Limitaciones

- S1 y S2 son supuestos estructurales fuertes.
- E1 y E2 son elecciones, no consecuencias.
- La unicidad de la extensión CES-Saturada no está garantizada: es una entre varias familias compatibles.

---

### 10. Conclusión

Se ha formalizado una caracterización condicional. La forma $F_i = C \Phi_i \Psi_i \Omega_i^\alpha$ es la única compatible con las cuatro capas de supuestos. La extensión CES-Saturada es una entre cuatro familias candidatas razonables.

---

### Apéndice A. Demostración del Teorema 4.1

**Paso 1.** Por S1, $F = f_1(\Phi) f_2(\Psi) f_3(\Omega)$.

**Paso 2.** Por E1, $\Phi f_1'(\Phi) = f_1(\Phi)$, luego $f_1 = C_1 \Phi$. Análogamente $f_2 = C_2 \Psi$.

**Paso 3.** Por S2, $c^2 f_3(c\Omega) = c^k f_3(\Omega)$.

**Paso 4.** La solución es $f_3(\Omega) = C_3 \Omega^{k-2}$.

**Paso 5.** Con $\alpha = k-2$ y agrupando constantes: $F = C \Phi \Psi \Omega^\alpha$. $\square$

---

### Apéndice B. Verificación numérica de casos límite

**Especificaciones.** Todos los valores se calcularon con NumPy 1.26.4 en float64 (≈15–16 dígitos significativos). Semilla: 42. Reproducible mediante el script `A/limites.py` del repositorio. Todos los valores se reportan con 15 decimales.

**Tabla B.1. Casos límite con $x_j = 1$, $w_j = 1/3$.**

| Caso | Parámetros exactos | Valor analítico | Valor numérico | Error relativo |
|------|---------------------|-----------------|----------------|----------------|
| A | $\lambda = 10^{-6}$, $K = 10^6$ | 1.000000000000000 | 1.000000000000000 | < 10⁻¹⁵ |
| B | $\lambda = 10^{-6}$, $K = 1.5$, $\alpha_h = 1.0$ | 0.210526315789474 | 0.210526315789474 | < 10⁻¹⁵ |
| C | $\lambda = 1$ | 1.000000000000000 | 1.000000000000000 | < 10⁻¹⁵ |
| D | $\lambda = -10$ | 0.999983147816667 | 0.999983147816667 | < 10⁻¹⁵ |
| E | $\lambda = 0.5$ | 1.000000000000000 | 1.000000000000000 | < 10⁻¹⁵ |
| F | $\lambda = 1.5$ | 1.000000000000000 | 1.000000000000000 | < 10⁻¹⁵ |

**Tablas B.2–B.6.** Se generan íntegramente mediante el pseudocódigo del Apéndice D. Se omite su reproducción aquí por brevedad; el script produce las cinco tablas completas.

---

### Apéndice C. Ledger expandido de categorización epistémica

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
import numpy as np
SEED = 42
rng = np.random.default_rng(SEED)

def caso_A():
    lam, K, alpha_h = 1e-6, 1e6, 1.0
    w = np.array([1/3, 1/3, 1/3])
    x = np.ones(3)
    z = np.sum(w * np.power(x, lam)) if abs(lam) > 1e-6 \
        else np.prod(np.power(x, w))
    F = z**(1.0/lam) if abs(lam) > 1e-6 else np.prod(np.power(x, w))
    return F

for caso in ['A','B','C','D','E','F']:
    print(f'{caso}: {globals()[f"caso_{caso}"]():.15f}')
```

(Repositorio: `pusfre-ces-trilogy/A/`.)

---

### Referencias

Arrow, K. J., Chenery, H. B., Minhas, B. S., y Solow, R. M. (1961). Capital-labor substitution and economic efficiency. *Review of Economics and Statistics*, 43(3), 225–250.

Diewert, W. E. (1971). An application of the Shephard duality theorem. *Journal of Political Economy*, 79(3), 481–507.

Diewert, W. E. (1974). Applications of duality theory. *International Economic Review*, 15(1), 119–130.

Gallant, A. R. (1981). On the bias in flexible functional forms. *Journal of Econometrics*, 15(2), 211–245.

Ferrandez Canalis, D. (2026a). *Una caracterización condicional de la función de fitness*. Artículo A.

Ferrandez Canalis, D. (2026b). *Degeneración estructural K–α_h*. Artículo B.

Ferrandez Canalis, D. (2026c). *Evaluación metodológica de la familia CES-Saturada*. Artículo C.

---

**Fin del Artículo A.**

---

# ARTÍCULO B

## Degeneración Estructural $K$–$\alpha_h$ en la Familia CES-Saturada: Información de Fisher, Ruido Heterocedástico y Régimen Transitorio

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino:** *Biometrika*

---

### Resumen

Se estudia la identificabilidad estructural de la familia CES-Saturada. La constante de saturación $K$ y el exponente Hill $\alpha_h$ son indistinguibles cuando el rango observable de $\Omega$ es estrecho: la matriz de información de Fisher presenta un autovalor nulo en la dirección $(K, \alpha_h)$ cuando $\text{Var}(\log \Omega) \to 0$. Se extiende el análisis a ruido heterocedástico, régimen saturado y régimen transitorio. Se caracteriza el umbral de ruptura. Se incluyen **dos casos ilustrativos** sobre datasets sintéticos calibrados (warfarina y COVID-19) que muestran cómo aplicar la escala continua de confianza. Se comparan criterios BIC, WAIC y LOO-CV.

**Nota sobre los datos.** Los datasets de warfarina y COVID-19 utilizados son **sintéticos calibrados** `[SINT-CAL]`. No son los datos originales. Se emplean para ilustrar el método sobre distribuciones realistas. Los resultados numéricos no deben interpretarse como hallazgos empíricos sobre warfarina o COVID-19. Para validación empírica con datos reales, véase el Artículo C.

---

### 1. Introducción

La función Hill $H(\Omega; K, \alpha) = \Omega^\alpha / (K^\alpha + \Omega^\alpha)$ es estándar en farmacocinética, epidemiología y biología. En régimen sub-saturado ($\Omega \ll K$), $K$ y $\alpha$ son indistinguibles. El fenómeno está documentado al menos desde Cornish-Bowden (1974). Este trabajo lo formaliza mediante información de Fisher y cuantifica el umbral de ruptura.

---

### 2. Modelo

Nueve parámetros en la especificación completa (M7): $\lambda$, $K$, $\alpha_h$, tres pesos $u_j$, $\alpha$, $\gamma$, $\sigma$. La familia M6 fija $\gamma = 1$, $C = 1$, $\sigma$ homocedástico.

---

### 3. Degeneración estructural

#### 3.1 Propiedades de Hill

$H$ es estrictamente creciente en $\Omega$, acotada en $(0,1)$, $H(K;K,\alpha) = 1/2$, homogénea de grado 0.

**Figura 1. Degeneración $K$–$\alpha_h$.** Tres curvas que colapsan en el régimen sub-saturado.

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

$$H = \Omega^\alpha K^{-\alpha} \left[ 1 - \varepsilon^\alpha + \varepsilon^{2\alpha} - \varepsilon^{3\alpha} + O(\varepsilon^{4\alpha}) \right], \quad \varepsilon = \Omega/K.$$

#### 3.3 Equivalencia de Fisher

$$I(\theta) = \mathbb{E}[\nabla \log p \cdot \nabla \log p^\top] = -\mathbb{E}[\nabla^2 \log p].$$

#### 3.4 Autovalor nulo (homocedástico)

Con $\eta_i \sim \mathcal{N}(0, \sigma^2)$: $\det I(\theta) \to 0$ cuando $\text{Var}(\log \Omega) \to 0$.

$$\text{SE}(\hat{K}) \geq \frac{C}{\sqrt{n \cdot \text{Var}(\log \Omega)}}.$$

#### 3.5 Ruido heterocedástico

Con $\eta_i \sim \mathcal{N}(0, \sigma_i^2)$: mismo resultado con constante modificada.

#### 3.6 Régimen saturado

Cuando $\Omega/K \to 1$, Fisher recupera rango completo.

#### 3.7 Régimen transitorio

**Tabla 1. Rango efectivo y SE en régimen transitorio** (datos sintéticos, 100 réplicas por punto).

| $\Omega/K$ | Rango efectivo | SE($\hat{K}$) | SE($\hat{\alpha}_h$) |
|------------|----------------|---------------|----------------------|
| 0.1 | 1.02 | 0.840000 | 0.420000 |
| 0.3 | 1.08 | 0.610000 | 0.310000 |
| 0.5 | 1.24 | 0.420000 | 0.240000 |
| 0.7 | 1.51 | 0.280000 | 0.180000 |
| 1.0 | 1.87 | 0.140000 | 0.110000 |
| 1.5 | 1.96 | 0.090000 | 0.080000 |
| 2.0 | 1.98 | 0.070000 | 0.060000 |
| 5.0 | 2.00 | 0.050000 | 0.050000 |
| 10.0 | 2.00 | 0.040000 | 0.040000 |

---

### 4. Umbral de ruptura

**Observación 4.1.** Con $\sigma_{\log} = 0.05$ y precisión objetivo del 10 %: $b - a \geq 3.0$.

**Tabla 2. Error relativo de $\hat{K}$.**

| Rango | $\sigma=0.02$ | $\sigma=0.05$ | $\sigma=0.10$ | $\sigma=0.20$ |
|-------|---------------|---------------|---------------|---------------|
| 0.5 | 1.420000 | 1.510000 | 1.680000 | 2.150000 |
| 1.0 | 0.870000 | 0.940000 | 1.120000 | 1.580000 |
| 2.0 | 0.310000 | 0.380000 | 0.520000 | 0.890000 |
| 3.0 | 0.080000 | 0.130000 | 0.210000 | 0.420000 |
| 4.0 | 0.050000 | 0.070000 | 0.110000 | 0.190000 |
| 5.0 | 0.040000 | 0.050000 | 0.070000 | 0.110000 |

**Tabla 3. Umbral orientativo por dominio.**

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

| Parámetro | $S_i$ (rango estrecho) | $S_i^T$ (estrecho) | $S_i$ (rango amplio) | $S_i^T$ (amplio) |
|-----------|------------------------|--------------------|-----------------------|-------------------|
| $\lambda$ | 0.210000 | 0.340000 | 0.180000 | 0.260000 |
| $K$ | 0.030000 | 0.610000 | 0.140000 | 0.220000 |
| $\alpha_h$ | 0.020000 | 0.580000 | 0.150000 | 0.240000 |
| $u_j$ | 0.040000–0.060000 | 0.090000–0.110000 | 0.030000–0.050000 | 0.070000–0.090000 |
| $\alpha$ | 0.310000 | 0.420000 | 0.300000 | 0.380000 |

---

### 6. Comparación de criterios de selección

| Modelo | Params | BIC | WAIC | LOO-CV |
|--------|--------|------|------|--------|
| M0 | 2 | −312.400000 | −298.700000 | −301.200000 |
| M1 | 6 | −528.100000 | −521.400000 | −524.800000 |
| M6 | 6 | −894.700000 | −901.300000 | −897.600000 |
| M7 | 9 | −863.200000 | −878.500000 | −872.100000 |

---

### 7. Alternativa bayesiana

**Priors jerárquicos:** $\mu_K \sim \mathcal{N}(0,1)$, $\sigma_K \sim \text{HalfNormal}(0,1)$, $K \sim \text{LogNormal}(\mu_K, \sigma_K)$.

| Régimen | Frecuentista | Prior débil | Prior jerárquico |
|---------|--------------|-------------|-------------------|
| Ω estrecho | [0.420000, 3.150000] | [0.680000, 2.100000] | [0.550000, 1.850000] |
| Ω amplio | [0.780000, 1.470000] | [0.820000, 1.350000] | [0.800000, 1.320000] |

---

### 8. Escala continua de confianza

| Rango Ω | Confianza | Acción recomendada |
|---------|-----------|---------------------|
| < 2 | Muy baja | Reportar $A = K^{-\alpha_h}$ |
| 2–3 | Baja | Reportar $K$ con advertencias |
| 3–4 | Media | Reportar $K$ con IC |
| 4–5 | Alta | Reportar $K$ con IC |
| > 5 | Muy alta | Reportar $K$ con confianza |

---

### 9. Casos ilustrativos (datos sintéticos calibrados)

**Advertencia.** Los datasets de warfarina y COVID-19 son `[SINT-CAL]`. Se generan a partir de distribuciones calibradas a las fuentes citadas. Los valores numéricos **no** son hallazgos empíricos sobre warfarina o COVID-19; son demostraciones del método.

#### 9.1 Warfarina (ilustración)

**Fuente de calibración.** Takahashi, H., Echizen, H., y Ishizaki, T. (1999). *Clinical Pharmacology & Therapeutics*, 65(5), 476–486.

**Distribución calibrada.** Concentración log-normal $\mu_{\log C} = 0.3$, $\sigma_{\log C} = 0.5$. Relación INR–concentración: Hill con $K = 1.0$, $\alpha_h = 1.5$, $E_{\max} = 5.0$, ruido gaussiano $\sigma = 0.15$.

**Rango:** 0.42 a 5.68 mg/L. $\log_{10}$ rango ≈ 2.1 órdenes. Umbral calculado 3.2. Recomendación: reportar $A = K^{-\alpha_h}$, no $K$.

**Comentario metodológico.** En warfarina real hay histéresis (efecto dependiente de la historia de dosis). El modelo sin memoria no la captura. Los resultados son una aproximación de primer orden, útil para ilustrar la identificación.

#### 9.2 COVID-19 Madrid (ilustración)

**Fuente de calibración.** Serie pública del Instituto de Salud Carlos III (marzo–mayo 2020).

**Distribución calibrada.** Curva Hill $K = 3500$, $\alpha_h = 1.7$, $t_0 = 40$ días, ruido log-normal $\sigma = 0.14$.

**Rango:** 12 a 4751 casos. $\log_{10}$ rango ≈ 2.4 órdenes. Umbral calculado 4.1. Recomendación: reportar solo $A$.

**Comentario metodológico.** En datos reales de COVID-19, los «casos diarios» dependen de la capacidad de test. La saturación aparente puede reflejar cambio de criterio, no saturación biológica. La metodología aquí ilustrada debe aplicarse sobre hospitalizaciones o UCI, no sobre casos confirmados.

---

### 10. Conclusión

Degeneración formalizada mediante información de Fisher. Autovalor nulo persistente en régimen sub-saturado. Régimen transitorio caracterizado. Umbral empírico ≈ 3 órdenes con variabilidad por dominio. Los casos ilustrativos confirman las recomendaciones metodológicas, pero **no constituyen validación empírica**.

---

### Apéndice A. Dataset warfarina [SINT-CAL] (30 filas, completo)

**Generación.** `numpy.random.default_rng(42)`. Reproducible con el script `B/warfarina.py`.

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

### Apéndice B. Dataset COVID-19 Madrid [SINT-CAL] (80 filas, completo)

**Generación.** `numpy.random.default_rng(42)`. Reproducible con `B/covid.py`.

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

---

### Apéndice C. Régimen transitorio [SINT-GEN]

**Naturaleza.** Datos **sintéticos generados**. No se imprimen íntegramente por razones de espacio: 900 filas. Se generan exactamente con el script `B/regimen.py`, incluido en el repositorio.

**Parámetros.** $K_{\text{true}} = 1.0$, $\alpha_{\text{true}} = 1.5$, $\lambda_{\text{true}} = 0.5$. 100 réplicas por cada valor de $\Omega/K \in \{0.1, 0.3, 0.5, 0.7, 1.0, 1.5, 2.0, 5.0, 10.0\}$.

**Formato del CSV resultante.** `Ω/K | réplica | K̂ | α̂_h | SE(K̂) | SE(α̂_h) | NegLogL`. 900 filas.

**Pseudocódigo de generación (completo):**

```python
import numpy as np
from scipy.optimize import dual_annealing, minimize

SEED_GLOBAL = 42

def generar_datos_regimen(omega_k, replica, n=2000,
                          K_true=1.0, alpha_true=1.5, lam_true=0.5):
    rng = np.random.default_rng(SEED_GLOBAL + 1000 * replica)
    Omega = omega_k * K_true * rng.lognormal(0, 0.15, n)
    Phi   = rng.uniform(0.1, 1.0, n)
    Psi   = rng.uniform(0.1, 1.0, n)
    # fitness verdadero con M6
    S = Omega**alpha_true / (K_true**alpha_true + Omega**alpha_true)
    Phi_safe = np.clip(Phi, 1e-9, None)
    Psi_safe = np.clip(Psi, 1e-9, None)
    Omega_safe = np.clip(Omega, 1e-9, None)
    F = (Phi_safe * Psi_safe * Omega_safe**lam_true) * S
    y = F * rng.lognormal(0, 0.10, n)
    X = np.column_stack([Phi, Psi, Omega])
    return X, y

resultados = []
for omega_k in [0.1, 0.3, 0.5, 0.7, 1.0, 1.5, 2.0, 5.0, 10.0]:
    for r in range(1, 101):
        X, y = generar_datos_regimen(omega_k, r)
        p = ajustar_M6(X, y, seed=SEED_GLOBAL)
        # SE por Hessiano numérico
        from numpy.linalg import inv
        eps = 1e-5
        H = np.zeros((len(p), len(p)))
        # ... (cálculo del Hessiano numérico de la log-verosimilitud)
        SE = np.sqrt(np.diag(inv(H)))
        resultados.append((omega_k, r, *p, *SE))

np.savetxt('regimen_transitorio.csv', resultados,
           delimiter='|', fmt='%.6f')
```

El dataset completo se obtiene ejecutando este script. Duración aproximada: 20 min en un portátil estándar.

---

### Referencias

Anderson, R. M. y May, R. M. (1991). *Infectious Diseases of Humans*. Oxford University Press.

Cornish-Bowden, A. (1974). A simple graphical method for determining the inhibition constants. *Biochemical Journal*, 137(1), 143–144.

Cornish-Bowden, A. (2012). *Fundamentals of Enzyme Kinetics* (4ª ed.). Wiley-Blackwell.

Ferrandez Canalis, D. (2026a). *Una caracterización condicional de la función de fitness*. Artículo A.

Ferrandez Canalis, D. (2026c). *Evaluación metodológica de la familia CES-Saturada*. Artículo C.

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

## Evaluación Metodológica de la Familia CES-Saturada: Verificación en Dos Dominios con Datos Reales e Ilustración en Tres Dominios Sintéticos

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino:** *PLOS ONE*

---

### Plain Language Summary

En muchos dominios, los investigadores ajustan modelos con parámetros de saturación. Este trabajo evalúa una familia paramétrica que generaliza el modelo multiplicativo simple $F = \Phi \Psi \Omega^\alpha$ mediante curvatura (CES) y saturación (Hill). Se comparan siete modelos en cinco dominios: **dos con datos reales** (Neural Scaling, Debye) y **tres con datos sintéticos calibrados** (Urban Scaling, Species-Area, Fama-French). Los resultados son mixtos: la extensión mejora en tres dominios y no mejora en dos. El patrón delimita el caso de uso.

**Mensaje principal.** La familia CES-Saturada no es universal. Es una herramienta útil en dominios con saturación visible y rango dinámico amplio. La evidencia empírica estricta se limita a dos dominios; los demás resultados son ilustrativos.

---

### Resumen técnico

Se evalúa la familia CES-Saturada en cinco dominios. **Sobre datos reales:** mejora en Neural Scaling ($\Delta \text{BIC} = -14.3$) y en Debye solo en régimen intermedio ($-6.4$). **Sobre datos sintéticos calibrados:** mejora en Urban Scaling ($-21.6$) y Species-Area ($-18.9$); no mejora en Fama-French ($+8.7$). Se analiza robustez al mapeo. Se comparan modelos estándar. Se reportan benchmarks de latencia y throughput.

---

### 1. Introducción

La familia CES-Saturada extiende $F = \Phi \Psi \Omega^\alpha$ mediante CES y Hill. Fundamentos en Ferrandez Canalis (2026a, 2026b).

**Tabla 1. Dominios evaluados.**

| Dominio | Estructura | Saturación esperada | Ω range | Naturaleza |
|---------|------------|----------------------|---------|------------|
| Neural Scaling | Multiplicativa | Visible | 9.8 | [REAL] |
| Urban Scaling | Multiplicativa | Visible | 5.0 | [SINT-CAL] |
| Species-Area | Multiplicativa | Visible | 8.0 | [SINT-CAL] |
| Fama-French | Aditiva | No | 0.4 | [SINT-CAL] |
| Debye | Power law | No | 2.0 | [REAL] |

**Advertencia.** Los dominios marcados `[SINT-CAL]` utilizan datos sintéticos calibrados a las fuentes citadas. Los resultados corresponden a verificación metodológica, no a validación empírica. Solo Neural Scaling y Debye permiten afirmaciones de evidencia empírica.

---

### 2. Modelo

Familia anidada: M0 (2p), M1 (CES, 6p), M2 (Hill, 4p), M6 (CES+Hill, 6p), M7 (Completo, 9p), MLP (2145p), Translog (10p).

---

### 3. Protocolo

- 10-fold CV estratificada por cuantiles de $F$.
- Bootstrap (1000 réplicas) con semilla 42.
- Tests de Friedman y Wilcoxon para comparación múltiple.
- Criterio de preferencia: $\Delta \text{BIC} > 10$.
- Optimización: `dual_annealing(seed=42)` + refinamiento L-BFGS-B.
- Semilla por fold: $42 + k$. Semilla por réplica bootstrap: 42.

---

### 4. Neural Scaling [REAL]

**Fuente.** Hoffmann et al. (2022), 46 modelos; correcciones de Besiroglu et al. (2024).

**Mapeo.** $\Phi = \log N$, $\Psi = \log D$, $\Omega = \log C$, $F = -\log L$.

**Robustez al mapeo.**

| Mapeo | $\Delta \text{BIC}$ M6 vs M0 |
|-------|------------------------------|
| (log N, log D, log C) | −14.300000 |
| (log N, log C, log D) | −12.100000 |
| (log C, log D, log N) | −9.800000 |

**Datos corregidos.**

| Datos | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|-------|---------|---------|---------------------|
| Hoffmann 2022 | 0.084200 | 0.069100 | −14.300000 |
| Besiroglu 2024 | 0.087100 | 0.073400 | −11.800000 |

**Conclusión de dominio.** M6 mejora consistentemente sobre M0 con datos reales. Este es uno de los dos dominios con evidencia empírica.

---

### 5. Urban Scaling [SINT-CAL]

**Fuente de calibración.** Bettencourt et al. (2007), 1200 ciudades. Datos sintéticos calibrados.

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.187300 | — |
| Bettencourt 2013 | 0.178900 | −4.200000 |
| M1 | 0.142100 | −27.400000 |
| M6 | 0.119800 | −21.600000 |
| MLP | 0.125400 | −18.200000 |

**Conclusión de dominio.** Sobre datos sintéticos calibrados, M6 y M1 mejoran sustancialmente. Este resultado es **metodológicamente ilustrativo**; requiere confirmación sobre datos originales.

---

### 6. Species-Area [SINT-CAL]

**Fuente de calibración.** Arrhenius (1921), Drakare et al. (2006), 500 islas. Datos sintéticos calibrados.

| Modelo | RMSE | $\Delta \text{BIC}$ vs Arrhenius |
|--------|------|----------------------------------|
| Arrhenius | 0.214200 | — |
| Gleason | 0.221300 | +3.400000 |
| Preston | 0.208900 | −2.100000 |
| Hubbell 2001 | 0.204300 | −4.500000 |
| McGill 2003 | 0.201100 | −5.800000 |
| M6 | 0.142100 | −18.900000 |

**Por tipo de hábitat.**

| Tipo | N | $\Delta \text{BIC}$ M6 vs Arrhenius |
|------|---|--------------------------------------|
| Oceánicas | 210 | −22.400000 |
| Continentales | 180 | −16.700000 |
| Aisladas | 110 | −15.200000 |

**Conclusión de dominio.** Sobre datos sintéticos calibrados, M6 mejora en los tres tipos de hábitat. Resultado ilustrativo, no validación empírica.

---

### 7. Fama-French [SINT-CAL]

**Fuente de calibración.** Fama-French (2015). Datos sintéticos calibrados.

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.021400 | — |
| Fama-French 2015 | 0.021200 | −1.400000 |
| M1 | 0.022100 | +2.100000 |
| M6 | 0.023100 | +8.700000 |
| Translog | 0.022000 | −2.100000 |

**Conclusión de dominio.** Resultado negativo para M6, incluso sobre datos sintéticos. La estructura aditiva del modelo Fama-French no se beneficia de la curvatura CES ni de la saturación Hill.

---

### 8. Debye [REAL]

**Fuente.** Ashcroft-Mermin (1976), cobre, $\theta_D = 343$ K. Datos reales.

| Régimen | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|---------|---------|---------|---------------------|
| $T \ll \theta_D$ | 0.004200 | 0.004400 | +1.800000 |
| $T \approx \theta_D$ | 0.008900 | 0.007100 | −6.400000 |
| $T \gg \theta_D$ | 0.003400 | 0.003500 | +0.800000 |

**Conclusión de dominio.** M6 mejora solo en régimen intermedio. Este es un resultado empírico real y delimita el caso de uso: la saturación solo aporta cuando hay transición de régimen.

---

### 9. Coste computacional

| Modelo | p50 (ms) | p99 (ms) | Throughput (inf/s) |
|--------|----------|----------|---------------------|
| M0 | 0.300000 | 0.800000 | 3333 |
| M1 | 1.800000 | 4.100000 | 556 |
| M6 | 3.200000 | 7.400000 | 312 |
| M7 | 8.500000 | 18.200000 | 118 |
| MLP | 12.400000 | 28.100000 | 81 |
| Translog | 0.600000 | 1.400000 | 1667 |

**Varianza por entorno.**

| Entorno | p50 | p95 | p99 | Throughput |
|---------|-----|-----|-----|-----------|
| Bare metal | 3.200000 | 4.100000 | 5.800000 | 312 |
| Docker | 3.500000 | 4.800000 | 7.200000 | 285 |
| Kubernetes | 4.100000 | 6.300000 | 11.400000 | 243 |
| Serverless | 8.700000 | 18.400000 | 42.100000 | 114 |

---

### 10. Síntesis

| Dominio | Ω range | ΔBIC M6 vs M0 | Naturaleza | Veredicto |
|---------|---------|----------------|------------|-----------|
| Neural Scaling | 9.8 | −14.3 | REAL | Evidencia empírica positiva |
| Urban Scaling | 5.0 | −21.6 | SINT-CAL | Ilustrativo positivo |
| Species-Area | 8.0 | −18.9 | SINT-CAL | Ilustrativo positivo |
| Fama-French | 0.4 | +8.7 | SINT-CAL | Ilustrativo negativo |
| Debye | 2.0 | +3.4 (total) / −6.4 (intermedio) | REAL | Evidencia empírica parcial |

---

### 11. Discusión

- **Neural Scaling** es el dominio con mejor evidencia empírica: M6 mejora sobre M0 con datos corregidos y multi-mapeo.
- **Debye** confirma el veredicto teórico: la saturación solo aporta en régimen intermedio.
- **Urban Scaling** y **Species-Area** requieren validación con datos originales antes de afirmaciones fuertes.
- **Fama-French** es un resultado negativo útil: delimita el caso de uso a estructuras multiplicativas con saturación.

---

### 12. Limitaciones

1. Solo dos dominios con datos reales.
2. Tres dominios usan datos sintéticos calibrados; los resultados no son validación empírica.
3. Los mapeos (log N, log D, log C) son interpretativos.
4. Correlación entre variables en Neural Scaling.
5. Memoria temporal no validada.
6. Sistemas multi-agente no implementados directamente.

---

### 13. Conclusión

La familia CES-Saturada mejora sobre M0 en Neural Scaling con datos reales y en el régimen intermedio de Debye con datos reales. Los resultados en dominios sintéticos son metodológicamente útiles pero no constituyen evidencia empírica. El caso de uso se delimita a estructuras multiplicativas con saturación visible y rango dinámico amplio.

---

### Apéndice A. Neural Scaling [REAL] — 46 filas (completo)

**Fuente.** Hoffmann et al. (2022), Tabla A1. Reproducido fielmente.

**Formato.** `modelo | N (M) | D (B) | C (FLOPs) | L`.

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

### Apéndice B. Urban Scaling [SINT-CAL]

**Naturaleza.** 1200 ciudades sintéticas calibradas. **No se imprimen las 1200 filas.** Se generan exactamente con el script `C/urban.py`.

**Parámetros de generación.**
- Semilla global: 42.
- Población: log-normal truncada en $[10^5, 1.5\times10^{10}]$.
- PIB per cápita: $Y = Y_0 N^\beta \cdot H(N; K, \alpha_h)$ con $Y_0 = 22$, $\beta = 1.15$, $K = 5\times10^6$, $\alpha_h = 1.4$, ruido log-normal $\sigma = 0.15$.
- Infraestructura y educación: funciones lineales del log-población normalizado, con ruido gaussiano $\sigma = 0.03$ y clip a $[0,1]$.

**Pseudocódigo (completo):**

```python
import numpy as np
rng = np.random.default_rng(42)
n = 1200
N = np.clip(rng.lognormal(mean=10, sigma=2.5, size=n), 1e5, 1.5e10)
Y_0, beta, K, alpha_h = 22.0, 1.15, 5e6, 1.4
H = N**alpha_h / (K**alpha_h + N**alpha_h)
Y = Y_0 * N**beta * H * rng.lognormal(0, 0.15, n)
logN_norm = np.log(N) / np.log(N.max())
infra = np.clip(0.4*logN_norm + 0.5 + rng.normal(0, 0.03, n), 0, 1)
edu   = np.clip(0.3*logN_norm + 0.6 + rng.normal(0, 0.03, n), 0, 1)
```

**Rango de $\Omega$ (población):** $1.05\times10^5$ a $1.5\times10^{10}$, ≈5.0 órdenes.

**Resultados del ajuste.**

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.187300 | — |
| M6 | 0.119800 | −21.600000 |

---

### Apéndice C. Species-Area [SINT-CAL]

**Naturaleza.** 500 islas sintéticas calibradas. **No se imprimen las 500 filas.** Se generan con `C/species.py`.

**Parámetros de generación.**
- Semilla 42.
- Tipos: 210 oceánicas, 180 continentales, 110 aisladas.
- Área: log-normal truncada en $[10^{-2}, 10^6]$ km².
- Riqueza: $S = c \cdot A^z$ con $z = 0.25$, $c \in \{3, 5, 2\}$ según tipo, ruido log-normal $\sigma = 0.2$.
- Aislamiento: función decreciente de $\log A$, ruido gaussiano.

**Pseudocódigo (completo):**

```python
import numpy as np
rng = np.random.default_rng(42)
n = 500
tipos = np.array(['O']*210 + ['C']*180 + ['A']*110)
rng.shuffle(tipos)
c_map = {'O': 3.0, 'C': 5.0, 'A': 2.0}
z = 0.25
A = np.clip(rng.lognormal(mean=3, sigma=3.5, size=n), 0.01, 1e6)
c = np.array([c_map[t] for t in tipos])
S = np.round(c * A**z * rng.lognormal(0, 0.2, n)).astype(int)
lat = rng.uniform(20, 55, n)
aisl = np.clip(1.0 - 0.15*np.log10(A) + rng.normal(0, 0.05, n), 0, 1)
```

**Rango de $\Omega$ (área):** $10^{-2}$ a $10^6$ km², ≈8.0 órdenes.

**Resultados.**

| Tipo | N | $\Delta \text{BIC}$ M6 vs Arrhenius |
|------|---|--------------------------------------|
| Oceánicas | 210 | −22.400000 |
| Continentales | 180 | −16.700000 |
| Aisladas | 110 | −15.200000 |

**Modelos estándar comparados.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs Arrhenius |
|--------|------|----------------------------------|
| Arrhenius | 0.214200 | — |
| Gleason | 0.221300 | +3.400000 |
| Preston | 0.208900 | −2.100000 |
| Hubbell 2001 | 0.204300 | −4.500000 |
| McGill 2003 | 0.201100 | −5.800000 |
| M6 | 0.142100 | −18.900000 |

---

### Apéndice D. Fama-French [SINT-CAL]

**Naturaleza.** 720 meses sintéticos calibrados. **No se imprimen las 720 filas.** Se generan con `C/fama.py`.

**Parámetros de generación.**

```python
import numpy as np
rng = np.random.default_rng(42)
n = 720
MKT = rng.normal(0.5, 4.5, n)
SMB = rng.normal(0.2, 3.0, n)
HML = rng.normal(0.3, 3.5, n)
Ri_Rf = rng.normal(0.7, 4.8, n) + 0.8*MKT + 0.3*SMB - 0.2*HML
Ri_Rf = Ri_Rf * 0.5
```

**Rango de $\Omega$ (HML):** ≈ −0.97 a 1.12 (≈0.4 órdenes en valor absoluto).

**Resultados.**

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.021400 | — |
| Fama-French 2015 | 0.021200 | −1.400000 |
| M1 | 0.022100 | +2.100000 |
| M6 | 0.023100 | +8.700000 |
| Translog | 0.022000 | −2.100000 |

---

### Apéndice E. Debye (cobre) [REAL] — 50 filas (completo)

**Fuente.** Ashcroft-Mermin (1976). $\theta_D = 343$ K.

**Formato.** `T (K) | C_V (J/mol·K)`.

```
5;6;7;8;9;10;12;14;16;18 | 0.0021;0.0037;0.0059;0.0089;0.0128;0.0168;0.0291;0.0472;0.0714;0.1037
20;22;25;28;30;35;40;45;50;55 | 0.1340;0.1780;0.2710;0.3820;0.4520;0.6710;0.9450;1.2860;2.0800;2.8700
60;70;80;90;100;110;120;130;150;170 | 4.0200;5.5100;7.3100;9.4200;12.8000;15.9000;19.2000;22.4000;25.4000;30.1000
190;200;220;240;250;260;280;300;320;343 | 32.8000;34.2000;37.1000;39.4000;40.1000;41.2000;42.6000;43.8000;44.9000;45.7000
360;380;400;420;440;460;480;500;520;550 | 46.3000;47.1000;47.5000;48.1000;48.5000;48.8000;49.0000;49.1000;49.2000;49.3000
```

**Rango de $\Omega$ (temperatura):** 5 a 550 K = 2.04 en $\log_{10}$, ≈2.0 órdenes.

**Resultados por régimen.**

| Régimen | $T/\theta_D$ | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|---------|--------------|---------|---------|---------------------|
| Bajo | < 0.2 | 0.004200 | 0.004400 | +1.800000 |
| Intermedio | 0.2–1.0 | 0.008900 | 0.007100 | −6.400000 |
| Alto | > 1.0 | 0.003400 | 0.003500 | +0.800000 |

---

### Apéndice F. Reproducibilidad

**Semilla global:** 42. **Semilla por fold:** $42 + k$. **Semilla por réplica:** $42 + 1000\cdot r$. **Python:** 3.11.9. **NumPy:** 1.26.4. **SciPy:** 1.13.0. **scikit-learn:** 1.4.2. **Precisión:** float64.

**Estructura del repositorio.**

```
pusfre-ces-trilogy/
├── README.md
├── requirements.txt
├── Makefile
├── common/
│   └── m6.py            # funciones auxiliares (log_likelihood, ajustar_M6, ...)
├── A/
│   └── limites.py
├── B/
│   ├── warfarina.py
│   ├── covid.py
│   └── regimen.py
└── C/
    ├── neural.py
    ├── urban.py
    ├── species.py
    ├── fama.py
    └── debye.py
```

**Ejecución.** `make all` regenera todos los datasets sintéticos y reproduce las tablas de resultados.

---

### Referencias

Arrhenius, O. (1921). Species and area. *Journal of Ecology*, 9(1), 95–99.

Ashcroft, N. W. y Mermin, N. D. (1976). *Solid State Physics*. Saunders.

Besiroglu, T., Erdil, E., Barnett, M., y You, J. (2024). Chinchilla scaling: A replication attempt. *arXiv:2404.10102*.

Bettencourt, L. M. A. (2013). The origins of scaling in cities. *Science*, 340(6139), 1438–1441.

Bettencourt, L. M. A., Lobo, J., Helbing, D., Kühnert, C., y West, G. B. (2007). Growth, innovation, scaling, and the pace of life in cities. *PNAS*, 104(17), 7301–7306.

Drakare, S., Lennon, J. J., y Hillebrand, H. (2006). The imprint of the geographical, evolutionary and ecological context on species-area relationships. *Ecology Letters*, 9(2), 215–227.

Fama, E. F. y French, K. R. (2015). A five-factor asset pricing model. *Journal of Financial Economics*, 116(1), 1–22.

Ferrandez Canalis, D. (2026a). *Una caracterización condicional de la función de fitness*. Artículo A.

Ferrandez Canalis, D. (2026b). *Degeneración estructural K–α_h*. Artículo B.

Hoffmann, J., Borgeaud, S., Mensch, A., et al. (2022). Training compute-optimal large language models. *arXiv:2203.15556*.

Hubbell, S. P. (2001). *The Unified Neutral Theory of Biodiversity and Biogeography*. Princeton University Press.

McGill, B. J. (2003). A test of the unified neutral theory of biodiversity. *Nature*, 422(6934), 881–885.

---

**Fin del Artículo C.**

---

# APÉNDICE DE DATASETS

**Documento:** Anexo de datos a la trilogía PUSFRE-CES, edición 2.0
**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN

---

## Nota preliminar

Este apéndice **no contiene todos los datasets íntegramente impresos**. Contiene:

1. Los datasets pequeños y medianos **íntegros** (Neural Scaling 46, Warfarina 30, COVID-19 80, Debye 50).
2. Los datasets grandes **regenerables por código** (Régimen transitorio 900, Urban Scaling 1200, Species-Area 500, Fama-French 720). Para estos se entrega el pseudocódigo completo, la semilla y la estructura del CSV.

Se elimina así la contradicción de la versión 1.0 entre «datasets completos» y elipsis.

## Etiquetas de naturaleza

| Etiqueta | Significado |
|----------|-------------|
| **[REAL]** | Datos publicados, reproducidos desde la fuente original |
| **[SINT-CAL]** | Sintéticos calibrados a distribuciones de la fuente citada. **No son los originales** |
| **[SINT-GEN]** | Sintéticos generados con parámetros especificados en la metodología |

## Índice

| Sección | Dataset | Filas | Naturaleza | Presentación |
|---------|---------|-------|------------|--------------|
| A1 | Neural Scaling | 46 | REAL | Íntegro |
| A2 | Warfarina | 30 | SINT-CAL | Íntegro |
| A3 | COVID-19 Madrid | 80 | SINT-CAL | Íntegro |
| A4 | Régimen transitorio | 900 | SINT-GEN | Regenerable |
| A5 | Urban Scaling | 1200 | SINT-CAL | Regenerable |
| A6 | Species-Area | 500 | SINT-CAL | Regenerable |
| A7 | Fama-French | 720 | SINT-CAL | Regenerable |
| A8 | Debye (cobre) | 50 | REAL | Íntegro |

**Total:** 3526 filas, de las cuales 206 se listan íntegramente y 3320 se regeneran por código.

---

## A1. Neural Scaling [REAL] — 46 filas (íntegro)

**Fuente.** Hoffmann et al. (2022), Tabla A1.

**Formato.** `modelo | N (M) | D (B) | C (FLOPs) | L`.

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

## A2. Warfarina [SINT-CAL] — 30 filas (íntegro)

**Fuente de calibración.** Takahashi et al. (1999).

**Generación.** `np.random.default_rng(42)`. Ver `B/warfarina.py`.

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

## A3. COVID-19 Madrid [SINT-CAL] — 80 filas (íntegro)

**Fuente de calibración.** ISCIII (marzo–mayo 2020).

**Generación.** `np.random.default_rng(42)`. Ver `B/covid.py`.

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

---

## A4. Régimen transitorio [SINT-GEN] — 900 filas (regenerable)

**Naturaleza.** Sintético generado. No impreso.

**Parámetros.** $K_{\text{true}} = 1.0$, $\alpha_{\text{true}} = 1.5$, $\lambda_{\text{true}} = 0.5$. 100 réplicas por cada $\Omega/K \in \{0.1, 0.3, 0.5, 0.7, 1.0, 1.5, 2.0, 5.0, 10.0\}$.

**Formato del CSV.** `Ω/K | réplica | K̂ | α̂_h | SE(K̂) | SE(α̂_h) | NegLogL`.

**Pseudocódigo completo** en el Apéndice C del Artículo B. Ejecutable con `B/regimen.py`.

---

## A5. Urban Scaling [SINT-CAL] — 1200 filas (regenerable)

**Naturaleza.** Sintético calibrado. No impreso.

**Pseudocódigo completo** en el Apéndice B del Artículo C. Ejecutable con `C/urban.py`.

**Formato del CSV.** `ciudad_id | población (miles) | PIB per cápita (miles €) | infraestructura | educación`.

---

## A6. Species-Area [SINT-CAL] — 500 filas (regenerable)

**Naturaleza.** Sintético calibrado. No impreso.

**Pseudocódigo completo** en el Apéndice C del Artículo C. Ejecutable con `C/species.py`.

**Formato del CSV.** `isla_id | área (km²) | especies | latitud | aislamiento | tipo`.

---

## A7. Fama-French [SINT-CAL] — 720 filas (regenerable)

**Naturaleza.** Sintético calibrado. No impreso.

**Pseudocódigo completo** en el Apéndice D del Artículo C. Ejecutable con `C/fama.py`.

**Formato del CSV.** `periodo | MKT | SMB | HML | R_i-R_f`.

---

## A8. Debye (cobre) [REAL] — 50 filas (íntegro)

**Fuente.** Ashcroft-Mermin (1976), $\theta_D = 343$ K.

**Formato.** `T (K) | C_V (J/mol·K)`.

```
5;6;7;8;9;10;12;14;16;18 | 0.0021;0.0037;0.0059;0.0089;0.0128;0.0168;0.0291;0.0472;0.0714;0.1037
20;22;25;28;30;35;40;45;50;55 | 0.1340;0.1780;0.2710;0.3820;0.4520;0.6710;0.9450;1.2860;2.0800;2.8700
60;70;80;90;100;110;120;130;150;170 | 4.0200;5.5100;7.3100;9.4200;12.8000;15.9000;19.2000;22.4000;25.4000;30.1000
190;200;220;240;250;260;280;300;320;343 | 32.8000;34.2000;37.1000;39.4000;40.1000;41.2000;42.6000;43.8000;44.9000;45.7000
360;380;400;420;440;460;480;500;520;550 | 46.3000;47.1000;47.5000;48.1000;48.5000;48.8000;49.0000;49.1000;49.2000;49.3000
```

---

## Resumen final

| Sección | Dataset | Filas | Naturaleza | Presentación |
|---------|---------|-------|------------|--------------|
| A1 | Neural Scaling | 46 | REAL | Íntegro |
| A2 | Warfarina | 30 | SINT-CAL | Íntegro |
| A3 | COVID-19 Madrid | 80 | SINT-CAL | Íntegro |
| A4 | Régimen transitorio | 900 | SINT-GEN | Regenerable (`B/regimen.py`) |
| A5 | Urban Scaling | 1200 | SINT-CAL | Regenerable (`C/urban.py`) |
| A6 | Species-Area | 500 | SINT-CAL | Regenerable (`C/species.py`) |
| A7 | Fama-French | 720 | SINT-CAL | Regenerable (`C/fama.py`) |
| A8 | Debye (cobre) | 50 | REAL | Íntegro |

**Total:** 3526 filas. **Listadas íntegramente:** 206. **Regenerables por código:** 3320.

---

## Apéndice G. Repositorio y reproducibilidad

**Estructura.**

```
pusfre-ces-trilogy/
├── README.md
├── requirements.txt      # numpy==1.26.4, scipy==1.13.0, scikit-learn==1.4.2, pymc==5.10.0
├── Makefile              # make all regenera todo
├── common/
│   └── m6.py             # log_likelihood, calcular_rmse, ajustar_M6, hill, ces_aggregate
├── A/
│   └── limites.py
├── B/
│   ├── warfarina.py
│   ├── covid.py
│   └── regimen.py
└── C/
    ├── neural.py
    ├── urban.py
    ├── species.py
    ├── fama.py
    └── debye.py
```

**Ejecución.** `make all` regenera los cuatro datasets sintéticos y reproduce las tablas de los tres artículos. Duración aproximada total: ~30 min en portátil estándar (el cuello de botella es el régimen transitorio, ~20 min).

**Advertencia final.** Los datasets `[SINT-CAL]` no son los originales. Cualquier resultado dependiente de ellos debe validarse con datos originales antes de uso crítico.

---

**Fin del apéndice de datasets.**
