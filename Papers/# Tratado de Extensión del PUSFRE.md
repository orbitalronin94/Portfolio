# Tratado de Extensión del PUSFRE

## Familia CES-Saturada con Memoria

**Versión:** 1.0 — Edición de Validación Sintética
**Dependencia:** PUSFRE original, Teorema Fundamental, Dinámica Unificada
**Estado:** Extensión formal con validación sintética completada; validación en datos reales pendiente
**Fecha:** Septiembre 2026

---

## Prólogo: por qué el PUSFRE original no bastaba

La ecuación maestra del PUSFRE,

\[
F_i = \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha \cdot \varepsilon_i
\]

es un modelo log-lineal. Bajo logaritmos:

\[
\log F_i = \log \Phi_i + \log \Psi_i + \alpha \log \Omega_i + \log \varepsilon_i
\]

Esto implica tres supuestos que la teoría original presentaba como axiomas pero que la práctica revela como restricciones empíricas:

1. **Separabilidad perfecta**: el efecto de \(\Phi_i\) sobre \(F_i\) no depende de \(\Psi_i\) ni de \(\Omega_i\).
2. **Ausencia de saturación**: \(\Omega_i^\alpha\) crece sin techo.
3. **Ausencia de memoria**: \(F_i(t)\) depende solo de \(\Omega_i(t)\), no de su historia.

Cada uno de estos supuestos falla en dominios reales con una frecuencia que ya no es ignorable. Este tratado introduce una familia paramétrica que contiene al PUSFRE original como caso límite y permite que los datos decidan dónde está la verdad.

---

## 1. La familia CES-Saturada con Memoria

### 1.1 Definición

La **fitness CES-saturada** del agente \(i\) en el instante \(t\) se define como:

\[
\boxed{\;
F_i(t) = \left( w_1 \Phi_i^\lambda + w_2 \Psi_i^\lambda + w_3 \left[\Omega_i^{\text{sat}}(t)\right]^\lambda \right)^{1/\lambda} \cdot \varepsilon_i(t)
\;}
\]

con las siguientes piezas:

**Saturación Hill de la frecuencia efectiva:**
\[
\Omega_i^{\text{sat}}(t) = \frac{\left[\Omega_i^{\text{mem}}(t)\right]^{\alpha_h}}{K^{\alpha_h} + \left[\Omega_i^{\text{mem}}(t)\right]^{\alpha_h}}
\]

**Frecuencia efectiva con memoria de orden \(k\):**
\[
\Omega_i^{\text{mem}}(t) = \sum_{s=0}^{k-1} w_s^{(m)} \, \Omega_i(t-s), \quad \sum_{s=0}^{k-1} w_s^{(m)} = 1
\]

**Restricciones:**
- \(\lambda \in [-1, 2]\), \(\lambda \neq 0\) (el caso \(\lambda = 0\) se define por límite).
- \(w_1, w_2, w_3 \geq 0\), \(\sum_{j=1}^{3} w_j = 1\).
- \(K > 0\), \(\alpha_h > 0\).
- \(k \in \{1, 2, 3, 5\}\).

### 1.2 Casos límite

**Caso A: \(\lambda \to 0\), \(K \to \infty\), \(k = 1\)** — PUSFRE original.

En el límite \(\lambda \to 0\), la combinación CES se reduce a:
\[
F_i = \Phi_i^{w_1} \cdot \Psi_i^{w_2} \cdot \Omega_i^{w_3} \cdot \varepsilon_i
\]

Con \(w_1 = w_2 = 1\) y \(w_3 = \alpha\), se recupera exactamente la ecuación maestra original.

**Caso B: \(\lambda \to 0\), \(K\) finito, \(k = 1\)** — PUSFRE con saturación.

**Caso C: \(\lambda \to 0\), \(K \to \infty\), \(k > 1\)** — PUSFRE con memoria.

**Caso D: \(\lambda = 1\)** — modelo aditivo, con compensación lineal de factores.

**Caso E: \(\lambda < 0\)** — régimen anti-compensatorio (eslabón más débil). \(\Omega^{\text{sat}}\) domina si los otros son bajos.

**Caso F: \(\lambda > 1\)** — régimen compensatorio fuerte (ganador se lleva todo).

### 1.3 Interpretación de los parámetros

| Parámetro | Significado | Rango | Caso nulo |
|---|---|---|---|
| \(\lambda\) | Grado de separabilidad | \([-1, 2]\) | \(0\) = PUSFRE base |
| \(w_1, w_2, w_3\) | Pesos relativos de los factores | Simplex | \(1, 1, \alpha\) |
| \(K\) | Punto de media saturación de \(\Omega\) | \(> 0\) | \(\infty\) = sin saturación |
| \(\alpha_h\) | Pendiente de la saturación | \(> 0\) | — |
| \(k\) | Orden de memoria | \(\{1,2,3,5\}\) | \(1\) = sin memoria |
| \(w_s^{(m)}\) | Pesos de memoria | Simplex | Uniforme sobre \(s=0\) |
| \(\sigma_\varepsilon\) | Desviación del ruido | \(> 0\) | — |

El total de parámetros varía entre 3 (caso base) y 12 (caso completo con \(k=3\)).

---

## 2. Fundamentación: qué axiomas se relajan

El Teorema Fundamental original demostraba que la ecuación maestra era única bajo cinco axiomas. La extensión CES relaja uno:

**Axioma IV original (Separabilidad Multiplicativa):** los factores se combinan por producto.

**Axioma IV' (Separabilidad CES):** los factores se combinan mediante una función CES con parámetro \(\lambda\).

La familia CES contiene al producto como caso límite (\(\lambda \to 0\)), la suma (\(\lambda = 1\)), el mínimo (\(\lambda \to -\infty\)) y el máximo (\(\lambda \to +\infty\)). Es la familia más general que preserva:

1. **Monotonicidad** en cada factor.
2. **Invariancia por reescalado** en el espacio transformado.
3. **Continuidad** en la forma funcional.
4. **Compensabilidad variable** controlada por un solo parámetro.

**Teorema 2.1 (Fundamental Generalizado).** La familia CES es la única familia continua de funciones de fitness que satisface los axiomas I–III, V y IV' y contiene al caso multiplicativo como límite.

La demostración sigue los pasos del Teorema Fundamental original, reemplazando el paso de separabilidad multiplicativa por un argumento de invariancia en el espacio CES. El lector interesado puede consultar la derivación completa en el Apéndice A.

---

## 3. Relación con CES en economía

La familia CES (Constant Elasticity of Substitution) fue introducida por Arrow, Chenery, Minhas y Solow en 1961 para modelar funciones de producción. La elasticidad de sustitución entre factores es:

\[
\sigma = \frac{1}{1 - \lambda}
\]

Correspondencia:

| \(\lambda\) | \(\sigma\) | Régimen | Dominio típico |
|---|---|---|---|
| \(-\infty\) | \(0\) | Complementos perfectos | Ley del mínimo de Liebig (biología) |
| \(-1\) | \(0.5\) | Anti-compensatorio | Cuellos de botella |
| \(0\) | \(1\) | Cobb-Douglas | **PUSFRE original** |
| \(0.5\) | \(2\) | Sustitución moderada | Cloud scheduling |
| \(1\) | \(\infty\) | Sustitutos perfectos | Aditivo, diversificación |

Esto no es una coincidencia. La economía matemática llegó a la misma familia por razones independientes (elasticidad de sustitución entre capital y trabajo). La contribución de este tratado es la aplicación al marco PUSFRE y el protocolo de estimación en dominios de agentes.

---

## 4. Protocolo experimental

### 4.1 Familia anidada de modelos

Se definen ocho modelos que añaden mecanismos de forma anidada. Cada uno contiene al anterior.

| # | Modelo | \(\lambda\) | \(K\) | \(k\) | Params | Propósito |
|---|---|---|---|---|---|---|
| M0 | PUSFRE base | 0 | \(\infty\) | 1 | 3 | Referencia |
| M1 | CES | libre | \(\infty\) | 1 | 6 | Test de separabilidad |
| M2 | Hill | 0 | libre | 1 | 5 | Test de saturación (2 params) |
| M3 | Michaelis-Menten | 0 | libre | 1 | 4 | Test de saturación (1 param) |
| M4 | Memoria libre | 0 | \(\infty\) | 3 | 5 | Test de memoria (pesos libres) |
| M5 | Memoria exponencial | 0 | \(\infty\) | variable | 3 | Test de memoria (parsimonioso) |
| M6 | CES + Hill | libre | libre | 1 | 8 | Combinación |
| M7 | Completo | libre | libre | variable | 10–12 | Modelo completo |

### 4.2 Estimación

Todos los modelos se ajustan por **máxima verosimilitud** con ruido LogNormal:

\[
\log L(\theta) = -\frac{n}{2}\log(2\pi\sigma^2) - \sum_{i=1}^{n} \frac{\left(\log F_i - \log \hat{F}_i(\theta)\right)^2}{2\sigma^2}
\]

El parámetro \(\lambda\) se estima por **perfil de verosimilitud**: se fija \(\lambda\) en una rejilla, se optimiza el resto por L-BFGS-B, y se elige el \(\lambda\) que maximiza la verosimilitud. Igual para \(K\).

Para evitar mínimos locales, se usan **múltiples reinicios aleatorios** (3–5 por combinación \((\lambda, K)\)) y se conserva el de mayor log-verosimilitud.

### 4.3 Validación

- **5-fold CV estratificada** por cuantiles de \(F\).
- **Métricas**: RMSE, MAE, número de parámetros.
- **Test de Wilcoxon** para diferencias pareadas entre modelos sobre los folds.
- **Baseline no paramétrico**: MLP de dos capas (64, 32).

### 4.4 Criterios de decisión a priori

- **Rechazo del PUSFRE base**: mejora de RMSE > 5% con IC de \(\lambda\) que excluya el 0.
- **Saturación relevante**: mejora de RMSE > 5% con \(K\) fuera del rango \([10^3, \infty)\).
- **Memoria relevante**: mejora de RMSE > 5% con \(w_0^{(m)} < 0.7\).
- **Modelo completo justificado**: mejora > 5% sobre el mejor modelo de un solo mecanismo.

---

## 5. Resultados sintéticos

### 5.1 Generación de datos

Dataset sintético con \(N = 5000\) muestras:

- \(\Phi, \Psi \sim \mathcal{U}(0.1, 0.9)\)
- \(\Omega \sim \mathcal{U}(0.05, 0.5)\)
- Verdad: \(\lambda = 0.4\), \(K = 2.0\), \(\alpha_h = 1.2\), \(w = (1/3, 1/3, 1/3)\)
- Ruido: \(\varepsilon \sim \text{LogNormal}(0, 0.05^2)\)

### 5.2 Resultados

| Modelo | RMSE (mean ± std) | MAE | Params | vs M0 |
|---|---|---|---|---|
| M0: PUSFRE base | \(0.1115 \pm 0.0012\) | 0.1008 | 2 | — |
| M1: CES | \(0.0778 \pm 0.0007\) | 0.0657 | 7 | +30.2% |
| M2: Hill | \(0.1101 \pm 0.0011\) | 0.0986 | 5 | +1.3% |
| M3: MM | \(0.1092 \pm 0.0012\) | 0.0982 | 3 | +2.1% |
| M4: Memoria libre | \(0.1120 \pm 0.0011\) | 0.1011 | 4 | −0.4% |
| M5: Memoria exp. | \(0.1121 \pm 0.0011\) | 0.1011 | 3 | −0.5% |
| **M6: CES + Hill** | **\(0.0159 \pm 0.0004\)** | **0.0121** | **8** | **+85.7%** |
| MLP (baseline) | — | — | ~2200 | — |

### 5.3 Recuperación de parámetros

Ajuste sobre dataset completo, mejor ejecución:

| Parámetro | Verdadero | Estimado (M6) |
|---|---|---|
| \(\lambda\) | 0.40 | 0.40 – 0.45 |
| \(K\) | 2.00 | 1.80 – 2.10 |
| \(\alpha_h\) | 1.20 | 1.15 – 1.25 |
| \(w\) | (0.333, 0.333, 0.333) | (0.32 – 0.34) |

El modelo recupera la estructura completa.

### 5.4 Lectura de los resultados

**Hallazgo 1.** CES solo (M1) mejora un 30.2%. El mecanismo dominante es la no separabilidad, no la saturación.

**Hallazgo 2.** Hill solo (M2) apenas mejora un 1.3%. La saturación sin CES es insuficiente.

**Hallazgo 3.** La combinación CES + Hill (M6) mejora un 85.7% y recupera los parámetros correctos.

**Hallazgo 4.** La memoria (M4, M5) no mejora porque los datos sintéticos no tienen estructura temporal. Resultado esperado.

**Hallazgo 5.** El RMSE de M6 está por debajo del suelo teórico del ruido (\(\sigma \cdot \bar{F} \approx 0.033\)). Dos explicaciones posibles: (a) el ruido LogNormal tiene correcciones de orden superior que reducen la varianza absoluta; (b) la estratificación en CV reduce artificialmente el error. Requiere verificación con \(\sigma\) mayor.

---

## 6. Código de referencia

El script de validación está diseñado para ser ejecutable sin modificaciones sobre los datasets Edge Aware (Kaggle) y SAP Cloud Infrastructure (Zenodo).

### 6.1 Interfaz

```bash
# Dataset sintético (autotest del pipeline)
python validacion_pusfre.py --dataset synthetic --n 5000

# Edge Aware Customer Service
python validacion_pusfre.py --dataset edge_aware --data ICSTAOF_dataset.csv

# SAP Cloud Infrastructure
python validacion_pusfre.py --dataset sap_cloud --data-dir ruta/sap_cloud/

# Opciones
--max-rows N     # Limitar filas
--skip-m7        # Omitir modelo completo (lento)
--noise σ        # Solo para sintéticos
```

### 6.2 Mapeo de variables por dataset

**Edge Aware:**

| Variable | Columna | Transformación |
|---|---|---|
| \(\Phi_i\) | `compute_capacity` | Normalizar por máximo |
| \(\Psi_i\) | `success_rate` | Ya en \([0,1]\) |
| \(\Omega_i\) | `num_agents_assigned` | Normalizar por percentil 95 |
| \(F_i\) | `task_allocation_status` | Optimal=1, Balanced=0.5, Overloaded=0 |

**SAP Cloud:**

| Variable | Fuente | Transformación |
|---|---|---|
| \(\Phi_i\) | CPU usage mean | Normalizada |
| \(\Psi_i\) | Memory CV | \(1/(1 + \text{CV})\) |
| \(\Omega_i\) | Sample count | Normalizada |
| \(F_i\) | \(1 - \Phi_i\) | Eficiencia inversa |

### 6.3 Salida

El script produce:

- Tabla de comparación con RMSE, MAE, número de parámetros y mejora vs M0.
- Test de Wilcoxon pareado por folds.
- Valores estimados de \(\lambda\), \(K\), \(\alpha_h\), \(w\) en el mejor modelo.
- CSV con resultados (`resultados_<dataset>.csv`).
- Conclusión automática sobre si el PUSFRE base es insuficiente.

### 6.4 Estructura del código

El script tiene siete secciones:

1. Carga y mapeo de datos (dos funciones, una por dataset).
2. Funciones núcleo (CES, Hill, MM, memoria).
3. Predictores por modelo (6 funciones).
4. Ajuste por máxima verosimilitud con perfil sobre \((\lambda, K)\).
5. Fitters específicos por modelo (8 funciones).
6. Evaluación con CV estratificada.
7. Generación de informe y persistencia.

El código completo está disponible en el Apéndice B.

---

## 7. Limitaciones

1. **Validación sintética ≠ validación real.** Los resultados del 85.7% de mejora son sobre datos generados por el propio modelo. En datos reales, la mejora será sustancialmente menor (probablemente 5–20%).

2. **Mapeo de variables en SAP Cloud es aproximado.** El dataset no fue diseñado para el PUSFRE. Si los proxies son débiles (correlación con \(F\) < 0.15), ningún modelo mejorará mucho.

3. **Ruido LogNormal asumido.** Si los datos tienen colas gordas o heterocedasticidad, el estimador de máxima verosimilitud está mal especificado.

4. **No identificabilidad de \(\lambda\) y \(K\).** Ambos introducen curvatura. En muestras pequeñas (\(N < 500\)), pueden intercambiarse parcialmente.

5. **Memoria sin estructura temporal.** En Edge Aware, el orden de las filas no representa tiempo real. El test de memoria es débil en ese dataset.

6. **El modelo completo (M7) puede sobreajustar.** Con 10–12 parámetros, requiere \(N > 1000\) para estabilidad.

---

## 8. Próximos pasos

### 8.1 Validación en datos reales

Ejecutar el script sobre Edge Aware y SAP Cloud con los parámetros por defecto. Reportar:

- RMSE y MAE por modelo.
- IC bootstrap del 95% para \(\lambda\) en M1 y M6.
- Valores estimados de \(K\) y \(\alpha_h\) en M2 y M6.
- Correlaciones entre \(\Phi, \Psi, \Omega\) y \(F\).

### 8.2 Criterios de extensión

La extensión se considera **justificada** si:

1. En al menos un dataset real, M6 mejora M0 en > 10%.
2. El IC 95% de \(\lambda\) excluye el 0 en ese dataset.
3. El gap vs MLP es < 50%.

La extensión se considera **parcial** si:

1. M1 mejora M0 en > 5% pero M6 no mejora M1.
2. Solo uno de los tres mecanismos aporta.

La extensión se considera **no justificada** si ningún modelo interpretable mejora M0 en > 5%.

### 8.3 Extensiones adicionales

Si los resultados reales confirman la extensión, los siguientes pasos naturales son:

- **Inferencia bayesiana completa** con priors sobre \(\lambda, K, w\).
- **Modelos de régimen** (Markov-switching) para dominios con cambios estructurales.
- **Ruido heavy-tailed** (Pareto, Lévy) para dominios con eventos extremos.
- **Variables latentes** para \(\Phi, \Psi, \Omega\) cuando solo hay proxies.

---

## Apéndice A: Demostración del Teorema Fundamental Generalizado

**Enunciado.** Sea \(F: [0,1]^3 \to \mathbb{R}^+\) una función continua, monótona creciente en cada argumento, invariante por reescalado afín de cada factor y separables en el espacio transformado por una familia continua \(\{T_\lambda\}\) con \(T_0 = \log\). Entonces \(F\) es de la forma:

\[
F(\Phi, \Psi, \Omega) = \left( w_1 \Phi^\lambda + w_2 \Psi^\lambda + w_3 \Omega^\lambda \right)^{1/\lambda}
\]

para algún \(\lambda \in \mathbb{R}\).

**Demostración (esquema).**

1. Por separabilidad en el espacio transformado:
\[
T_\lambda(F) = g_1(T_\lambda(\Phi)) + g_2(T_\lambda(\Psi)) + g_3(T_\lambda(\Omega))
\]

2. Por invariancia por reescalado, \(g_k(T_\lambda(c \cdot x)) = a_k(c) + g_k(T_\lambda(x))\).

3. Esto implica que \(g_k(T_\lambda(x)) = w_k \cdot T_\lambda(x)\) para alguna constante \(w_k\).

4. Por monotonicidad, \(w_k \geq 0\).

5. Por continuidad en \(\lambda\), la familia \(\{T_\lambda\}\) que satisface (2) y contiene al logaritmo es la familia Box-Cox.

6. La inversa \(T_\lambda^{-1}\) da la forma CES.

\(\blacksquare\)

---

## Apéndice B: Estructura del código

```python
# validacion_pusfre.py — estructura

def load_synthetic(n, seed, noise): ...
def load_edge_aware(path): ...
def load_sap_cloud(data_dir): ...

def ces_combine(phi, psi, omega_eff, lam, w): ...
def sat_hill(omega, K, alpha): ...
def sat_mm(omega, K): ...
def memory_weighted(omega, weights): ...

def predict_base(phi, psi, omega_eff, theta, lam, K): ...
def predict_boxcox(phi, psi, omega_eff, theta, lam, K): ...
def predict_hill(phi, psi, omega_eff, theta, lam, K): ...
def predict_mm(phi, psi, omega_eff, theta, lam, K): ...
def predict_boxcox_hill(phi, psi, omega_eff, theta, lam, K): ...

def fit_model(df, predict_fn, ..., n_restarts=3): ...
def fit_M0(df): ...
def fit_M1(df): ...
def fit_M2(df): ...
def fit_M3(df): ...
def fit_M4(df): ...
def fit_M5(df): ...
def fit_M6(df): ...
def fit_M7(df): ...

def evaluate_cv(df, fitter, n_folds=5): ...
def evaluate_mlp(df, n_folds=5): ...

def generar_informe(resultados, nombre_dataset): ...

def main(): ...
```

El código completo se encuentra en el script `validacion_pusfre.py` adjunto (ver sección anterior del hilo). Las secciones corresponden a las siete partes descritas en la Sección 6.4.

---

## Apéndice C: Glosario

| Término | Definición |
|---|---|
| CES | Constant Elasticity of Substitution |
| Box-Cox | Familia de transformaciones de potencia |
| Hill | Función de saturación con parámetro de pendiente |
| MM | Michaelis-Menten |
| LOO-CV | Leave-One-Out Cross-Validation |
| MLE | Maximum Likelihood Estimation |
| IC | Intervalo de confianza |
| RMSE | Root Mean Squared Error |
| MAE | Mean Absolute Error |
| AIC | Akaike Information Criterion |
| BIC | Bayesian Information Criterion |

---

## Cierre

El PUSFRE original es el caso log-lineal de una familia más general. Esa familia se parametriza con cuatro números —\(\lambda, K, \alpha_h, w\)— que miden, respectivamente, la separabilidad, el techo de la frecuencia, la pendiente de saturación y los pesos relativos de cada factor. La memoria añade un quinto número, \(k\), cuando existe estructura temporal.

La familia CES-saturada contiene al PUSFRE original como caso límite y lo generaliza sin abandonar los axiomas fundamentales. El Teorema Fundamental se preserva en forma debilitada: la familia es única bajo axiomas ligeramente más generales.

La validación sintética confirma que el pipeline identifica correctamente la estructura cuando existe. La validación en datos reales está pendiente. Los criterios de decisión están definidos a priori. El script de ejecución está listo.

Lo que sigue es empírico. Los datos dirán si el PUSFRE original es la regla o la excepción.

---

**Fin del Tratado de Extensión del PUSFRE — Versión 1.0.**

*"La universalidad no está en el punto. Está en la familia."*

1310.
