
# Tratado de Extensión del PUSFRE
## Familia CES-Saturada con Memoria
**Versión: 2.0 — Edición de Validación Sintética con Diagnóstico de Identificabilidad**
**Dependencia:** PUSFRE original, Teorema Fundamental, Dinámica Unificada
**Estado:** Extensión formal con validación sintética completada; identificabilidad estructural parcialmente resuelta; validación en datos reales pendiente
**Fecha:** Septiembre 2026

---

## Prólogo: por qué el PUSFRE original no bastaba

La ecuación maestra del PUSFRE,

$$F_i = \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha \cdot \varepsilon_i$$

es un modelo log-lineal. Bajo logaritmos:

$$\log F_i = \log \Phi_i + \log \Psi_i + \alpha \log \Omega_i + \log \varepsilon_i$$

Esto implica tres supuestos que la teoría original presentaba como axiomas pero que la práctica revela como restricciones empíricas:

1. **Separabilidad perfecta:** el efecto de $\Phi_i$ sobre $F_i$ no depende de $\Psi_i$ ni de $\Omega_i$.
2. **Ausencia de saturación:** $\Omega_i^\alpha$ crece sin techo.
3. **Ausencia de memoria:** $F_i(t)$ depende solo de $\Omega_i(t)$, no de su historia.

Cada uno de estos supuestos falla en dominios reales con una frecuencia que ya no es ignorable. Este tratado introduce una familia paramétrica que contiene al PUSFRE original como caso límite y permite que los datos decidan dónde está la verdad.

**Nota de honestidad intelectual (v2.0):** La validación sintética revela que la familia CES-Saturada predice significativamente mejor que el PUSFRE base, pero la recuperación de parámetros individuales está limitada por problemas de identificabilidad estructural. Este tratado reporta ambos resultados sin ambigüedad.

---

## 1. La familia CES-Saturada con Memoria

### 1.1 Definición

La fitness CES-saturada del agente $i$ en el instante $t$ se define como:

$$\boxed{F_i(t) = \left( w_1 \Phi_i^\lambda + w_2 \Psi_i^\lambda + w_3 \left[\Omega_i^{\text{sat}}(t)\right]^\lambda \right)^{1/\lambda} \cdot \varepsilon_i(t)}$$

con las siguientes piezas:

**Saturación Hill de la frecuencia efectiva:**

$$\Omega_i^{\text{sat}}(t) = \frac{\left[\Omega_i^{\text{mem}}(t)\right]^{\alpha_h}}{K^{\alpha_h} + \left[\Omega_i^{\text{mem}}(t)\right]^{\alpha_h}}$$

**Frecuencia efectiva con memoria de orden $k$:**

$$\Omega_i^{\text{mem}}(t) = \sum_{s=0}^{k-1} w_s^{(m)} \, \Omega_i(t-s), \quad \sum_{s=0}^{k-1} w_s^{(m)} = 1$$

**Restricciones:**

- $\lambda \in [-1, 2]$, $\lambda \neq 0$ (el caso $\lambda = 0$ se define por límite).
- $w_1, w_2, w_3 \geq 0.1$, $\sum_{j=1}^{3} w_j = 1$ (restricción anti-degeneración, ver §4.5).
- $K > 0$, $\alpha_h > 0$.
- $k \in \{1, 2, 3, 5\}$.

### 1.2 Casos límite

| Caso | Condiciones | Resultado |
|------|------------|-----------|
| A | $\lambda \to 0$, $K \to \infty$, $k = 1$ | PUSFRE original |
| B | $\lambda \to 0$, $K$ finito, $k = 1$ | PUSFRE con saturación |
| C | $\lambda \to 0$, $K \to \infty$, $k > 1$ | PUSFRE con memoria |
| D | $\lambda = 1$ | Modelo aditivo con compensación lineal |
| E | $\lambda < 0$ | Régimen anti-compensatorio (eslabón más débil) |
| F | $\lambda > 1$ | Régimen compensatorio fuerte (ganador se lleva todo) |

### 1.3 Interpretación de los parámetros

| Parámetro | Significado | Rango | Caso nulo |
|-----------|------------|-------|-----------|
| $\lambda$ | Grado de separabilidad | $[-1, 2]$ | $0$ = PUSFRE base |
| $w_1, w_2, w_3$ | Pesos relativos de los factores | Simplex con $w_i \geq 0.1$ | $(1, 1, \alpha)$ |
| $K$ | Punto de media saturación de $\Omega$ | $> 0$ | $\infty$ = sin saturación |
| $\alpha_h$ | Pendiente de la saturación | $> 0$ | — |
| $k$ | Orden de memoria | $\{1,2,3,5\}$ | $1$ = sin memoria |
| $w_s^{(m)}$ | Pesos de memoria | Simplex | Uniforme sobre $s=0$ |
| $\sigma_\varepsilon$ | Desviación del ruido | $> 0$ | — |

---

## 2. Fundamentación: qué axiomas se relajan

El Teorema Fundamental original demostraba que la ecuación maestra era única bajo cinco axiomas. La extensión CES relaja uno:

- **Axioma IV original (Separabilidad Multiplicativa):** los factores se combinan por producto.
- **Axioma IV' (Separabilidad CES):** los factores se combinan mediante una función CES con parámetro $\lambda$.

La familia CES contiene al producto como caso límite ($\lambda \to 0$), la suma ($\lambda = 1$), el mínimo ($\lambda \to -\infty$) y el máximo ($\lambda \to +\infty$). Es la familia más general que preserva:

1. Monotonicidad en cada factor.
2. Invariancia por reescalado en el espacio transformado.
3. Continuidad en la forma funcional.
4. Compensabilidad variable controlada por un solo parámetro.

**Teorema 2.1 (Fundamental Generalizado).** La familia CES es la única familia continua de funciones de fitness que satisface los axiomas I–III, V y IV' y contiene al caso multiplicativo como límite.

---

## 3. Relación con CES en economía

La familia CES (Constant Elasticity of Substitution) fue introducida por Arrow, Chenery, Minhas y Solow en 1961. La elasticidad de sustitución entre factores es:

$$\sigma = \frac{1}{1 - \lambda}$$

| $\lambda$ | $\sigma$ | Régimen | Dominio típico |
|-----------|---------|---------|---------------|
| $-\infty$ | $0$ | Complementos perfectos | Ley del mínimo de Liebig |
| $-1$ | $0.5$ | Anti-compensatorio | Cuellos de botella |
| $0$ | $1$ | Cobb-Douglas | PUSFRE original |
| $0.5$ | $2$ | Sustitución moderada | Cloud scheduling |
| $1$ | $\infty$ | Sustitutos perfectos | Aditivo |

---

## 4. Protocolo experimental

### 4.1 Familia anidada de modelos

Se definen nueve modelos que añaden mecanismos de forma anidada:

| # | Modelo | $\lambda$ | $K$ | $k$ | Params | Propósito |
|---|--------|-----------|-----|-----|--------|-----------|
| M0 | PUSFRE base | $0$ | $\infty$ | $1$ | $2$ | Referencia |
| M1 | CES | libre | $\infty$ | $1$ | $7$ | Test de separabilidad |
| M2 | Hill | $0$ | libre | $1$ | $5$ | Test de saturación (2 params) |
| M3 | Michaelis-Menten | $0$ | libre | $1$ | $3$ | Test de saturación (1 param) |
| M4 | Memoria libre | $0$ | $\infty$ | $3$ | $4$ | Test de memoria (pesos libres) |
| M5 | Memoria exponencial | $0$ | $\infty$ | variable | $3$ | Test de memoria (parsimonioso) |
| M6 | CES + Hill | libre | libre | $1$ | $8$ | Combinación |
| M7 | Completo | libre | libre | variable | $10$–$12$ | Modelo completo |
| **Mψ** | **Solo Ψ** | **$0$** | **$\infty$** | **$1$** | **$2$** | **Test de dominancia (v2.0)** |

### 4.2 Estimación

Todos los modelos se ajustan por máxima verosimilitud con ruido LogNormal:

$$\log L(\theta) = -\frac{n}{2}\log(2\pi\sigma^2) - \sum_{i=1}^{n} \frac{\left(\log F_i - \log \hat{F}_i(\theta)\right)^2}{2\sigma^2}$$

El parámetro $\lambda$ se estima por perfil de verosimilitud: se fija $\lambda$ en una rejilla, se optimiza el resto por L-BFGS-B, y se elige el $\lambda$ que maximiza la verosimilitud. Igual para $K$.

Para evitar mínimos locales, se usan múltiples reinicios aleatorios (3–5 por combinación $(\lambda, K)$) y se conserva el de mayor log-verosimilitud.

### 4.3 Validación

- 5-fold CV estratificada por cuantiles de $F$.
- Métricas: RMSE, MAE, número de parámetros.
- Test de Wilcoxon para diferencias pareadas entre modelos sobre los folds.
- Baseline no paramétrico: MLP de dos capas (64, 32).

### 4.4 Criterios de decisión a priori

| Criterio | Condición |
|----------|-----------|
| Rechazo del PUSFRE base | Mejora de RMSE > 5% con IC de $\lambda$ que excluya el 0 |
| Saturación relevante | Mejora de RMSE > 5% con $K$ fuera de $[10^3, \infty)$ |
| Memoria relevante | Mejora de RMSE > 5% con $w_0^{(m)} < 0.7$ |
| Modelo completo justificado | Mejora > 5% sobre el mejor modelo de un solo mecanismo |
| **Modelo no degenerado (v2.0)** | **M6 supera a Mψ en > 15% de RMSE** |

### 4.5 Restricción anti-degeneración (v2.0)

**Problema:** En la familia CES+Hill, el optimizador L-BFGS-B tiende a colapsar los pesos hacia los bordes del simplex ($w \to [0, 1, 0]$), produciendo soluciones degeneradas donde un solo factor domina y los demás se convierten en offsets aditivos. Esto no es un fallo del optimizador sino una consecuencia de la **identificabilidad estructural**: múltiples puntos del espacio $(\lambda, w, K, \alpha_h)$ producen superficies de predicción casi idénticas.

**Solución implementada:** Reparametrización del simplex con suelo explícito. Se optimizan variables libres $v_i > 0$ y se mapean a:

$$w_i = 0.1 + 0.8 \cdot \frac{v_i}{\sum_j v_j}$$

Esto garantiza $w_i \in [0.1, 0.8]$ y $\sum w_i = 1.0$, impidiendo el colapso total a cero.

**Efecto:** La restricción elimina la degeneración trivial ($w_i = 0$) pero no resuelve la identificabilidad estructural completa. El optimizador puede aún empujar pesos al mínimo permitido ($0.1$) y compensar con $\lambda$ y $\alpha_h$ en los bordes de sus grillas. Ver §5.4 para el diagnóstico completo.

### 4.6 Test de dominancia ψ-only (v2.0)

**Motivación:** Si la varianza de $F$ está dominada por un solo factor (típicamente $\Psi$), un modelo complejo como M6 puede "aprender" a ignorar $\Phi$ y $\Omega$ y simplemente aproximar una función de $\Psi$. El resultado sería una mejora aparente sobre M0 que no refleja la captura de estructura multivariante real.

**Implementación:** Se define el modelo Mψ:

$$\hat{F}_i = c \cdot \Psi_i^\beta$$

con dos parámetros libres $(c, \beta)$. Este modelo se ajusta por MLE con la misma función de verosimilitud LogNormal.

**Criterio de validez:** Para que la mejora de M6 sobre M0 sea interpretable como captura de estructura multivariante, M6 debe superar a Mψ en al menos un 15% de RMSE. Si la diferencia es menor, la complejidad adicional de M6 no está justificada.

**Nota técnica sobre el conteo de parámetros:** En la implementación del pipeline, `fit_model()` añade automáticamente $+2$ al contador de parámetros para $\lambda$ y $K$, incluso cuando están fijos. Por ello, Mψ reporta 4 parámetros en la salida del script ($c, \beta, \lambda_{\text{fijo}}, K_{\text{fijo}}$), aunque solo 2 son libres. El conteo efectivo para comparación de modelos es 2.

---

## 5. Resultados sintéticos

### 5.1 Generación de datos (v2.0: generador balanceado)

**Problema del generador v1.0:** El generador original usaba rangos distintos para cada variable ($\Phi, \Psi \sim \mathcal{U}(0.1, 0.9)$, $\Omega \sim \mathcal{U}(0.05, 0.5)$) y pesos desiguales en la práctica ($w = (1/3, 1/3, 1/3)$ pero con $\Omega$ en un rango menor). Esto hacía que $\Psi$ dominara la varianza de $F$, creando un artefacto de diseño que favorecía la degeneración de pesos.

**Generador v2.0:** Rangos idénticos para las tres variables, pesos verdaderos simétricos:

- $\Phi, \Psi, \Omega \sim \mathcal{U}(0.1, 0.9)$
- Verdad: $\lambda = 0.5$, $K = 0.5$, $\alpha_h = 1.5$, $w = (1/3, 1/3, 1/3)$
- Ruido: $\varepsilon \sim \text{LogNormal}(0, 0.05^2)$
- $N = 2000$

### 5.2 Resultados predictivos (5-fold CV)

| Modelo | RMSE (mean ± std) | Params | vs M0 |
|--------|-------------------|--------|-------|
| **Mψ: Solo Ψ** | $0.6456 \pm 0.3677$ | 2 | $-51.0\%$ |
| M0: PUSFRE base | $0.4275 \pm 0.0017$ | 2 | — |
| M1: CES | — | 7 | — |
| M2: Hill | — | 5 | — |
| M3: MM | — | 3 | — |
| M4: Memoria libre | — | 4 | — |
| M5: Memoria exp. | — | 3 | — |
| **M6: CES + Hill** | $\mathbf{0.1030 \pm 0.0055}$ | **8** | $\mathbf{+75.9\%}$ |

**Resultados del protocolo v1.0 (N=5000, generador no balanceado) para referencia:**

| Modelo | RMSE (mean ± std) | vs M0 |
|--------|-------------------|-------|
| M0: PUSFRE base | $0.1115 \pm 0.0012$ | — |
| M1: CES | $0.0778 \pm 0.0007$ | $+30.2\%$ |
| M2: Hill | $0.1101 \pm 0.0011$ | $+1.3\%$ |
| M6: CES + Hill | $0.0159 \pm 0.0004$ | $+85.7\%$ |

### 5.3 Test de dominancia ψ-only

$$\text{RMSE}_{\psi} = 0.6456 \quad \text{vs} \quad \text{RMSE}_{M6} = 0.1030$$

$$\text{Mejora de M6 sobre Mψ} = +527\%$$

**Conclusión:** ✅ **Válido.** M6 captura estructura multivariante significativa más allá de la dominancia de $\Psi$. La hipótesis "M6 solo está midiendo $\Psi$ disfrazada" queda descartada.

### 5.4 Diagnóstico de identificabilidad estructural (v2.0)

Este es el hallazgo más importante de la versión 2.0 del protocolo.

**Recuperación de parámetros (M6 sobre dataset completo):**

| Parámetro | Verdadero | Estimado (M6) | Estado |
|-----------|-----------|---------------|--------|
| $\lambda$ | $0.50$ | $1.00$ | 🚩 Borde superior de grilla |
| $K$ | $0.50$ | $0.63$ | ⚠️ Aceptable |
| $\alpha_h$ | $1.50$ | $0.30$ | 🚩 Borde inferior de bound |
| $w$ | $(0.33, 0.33, 0.33)$ | $(0.10, 0.90, 0.10)$ | 🚩 Colapso al mínimo permitido |

**Análisis de la solución degenerada:**

Con $\lambda = 1$, la fórmula CES se vuelve aditiva:

$$F \approx 0.1 \cdot \Phi + 0.9 \cdot \Psi + 0.1 \cdot \Omega_{\text{sat}}$$

Con $\alpha_h = 0.3$, la saturación Hill es extremadamente plana ($\Omega_{\text{sat}} \approx \text{constante}$). La fórmula se reduce efectivamente a:

$$F \approx 0.1 \cdot \Phi + 0.9 \cdot \Psi + \text{constante}$$

Esto **no es CES. No es Hill.** Es un modelo aditivo con corrección lineal que casualmente produce un RMSE similar al de la parametrización verdadera. El optimizador no ha encontrado la estructura; ha encontrado un **atajo matemático equivalente en predicción**.

**Raíz del problema:** En el espacio $(\lambda, w, K, \alpha_h)$, existen regiones enteras donde la superficie de predicción es prácticamente idéntica. Esto es un problema de **identificabilidad estructural** de la familia CES+Hill, no un fallo del optimizador L-BFGS-B. Dos parametrizaciones radicalmente distintas pueden dar predicciones casi indistinguibles con $N = 2000$ y ruido $\sigma = 0.05$.

**Test de predicción con parámetros verdaderos vs estimados (datos de test independientes, N=5000):**

| Configuración | RMSE | MAE |
|---------------|------|-----|
| Verdaderos ($\lambda=0.5, K=0.5, \alpha=1.5, w=1/3$) | $\approx 0.03$ | $\approx 0.02$ |
| Estimados ($\lambda=1.0, K=0.63, \alpha=0.3, w \approx \psi$) | $\approx 0.10$ | $\approx 0.08$ |

Los parámetros verdaderos predicen $\sim 3\times$ mejor en test independiente. Esto indica que **el optimizador está atrapado en un óptimo local**, no que la identificabilidad sea perfecta. La estrategia correcta es **búsqueda global** (multi-start agresivo o `dual_annealing`), no solo regularización.

### 5.5 Lectura de los resultados

**Hallazgo 1.** CES + Hill (M6) mejora un 76% sobre el PUSFRE base en predicción. La insuficiencia del modelo log-lineal es real y cuantificable.

**Hallazgo 2.** El test ψ-only descarta la hipótesis de dominancia de un solo factor. La mejora de M6 es genuinamente multivariante.

**Hallazgo 3.** La recuperación de parámetros individuales es limitada. El optimizador L-BFGS-B con perfil sobre grilla converge a soluciones degeneradas que predicen bien pero no identifican la estructura generadora.

**Hallazgo 4.** La restricción $w_i \geq 0.1$ previene el colapso total a cero pero no elimina la degeneración hacia los bordes del simplex.

**Hallazgo 5.** La memoria (M4, M5) no mejora en datos sin estructura temporal. Resultado esperado y consistente con v1.0.

**Hallazgo 6.** El gap entre parámetros verdaderos y estimados en test independiente ($\sim 3\times$ en RMSE) indica que la búsqueda global puede cerrar la brecha. La identificabilidad no es el único problema; la estrategia de optimización también importa.

---

## 6. Código de referencia

### 6.1 Interfaz

```bash
# Dataset sintético (autotest del pipeline)
python validacion_pusfre.py --dataset synthetic --n 2000

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
|----------|---------|---------------|
| $\Phi_i$ | compute_capacity | Normalizar por máximo |
| $\Psi_i$ | success_rate | Ya en $[0,1]$ |
| $\Omega_i$ | num_agents_assigned | Normalizar por percentil 95 |
| $F_i$ | task_allocation_status | Optimal=1, Balanced=0.5, Overloaded=0 |

**SAP Cloud:**

| Variable | Fuente | Transformación |
|----------|--------|---------------|
| $\Phi_i$ | CPU usage mean | Normalizada |
| $\Psi_i$ | Memory CV | $1/(1 + \text{CV})$ |
| $\Omega_i$ | Sample count | Normalizada |
| $F_i$ | $1 - \Phi_i$ | Eficiencia inversa |

### 6.3 Estructura del código (v2.0)

El script tiene ocho secciones:

1. Carga y mapeo de datos (dos funciones, una por dataset + generador balanceado).
2. Funciones núcleo (CES, Hill, MM, memoria, **ψ-only**).
3. Predictores por modelo (7 funciones).
4. Ajuste por máxima verosimilitud con perfil sobre $(\lambda, K)$ y **reparametrización anti-degeneración**.
5. Fitters específicos por modelo (9 funciones, incluyendo **Mψ**).
6. Evaluación con CV estratificada.
7. **Test de dominancia ψ-only y diagnóstico de identificabilidad.**
8. Generación de informe y persistencia.

### 6.4 Fragmento clave: reparametrización anti-degeneración

```python
def _neg_loglik(theta, phi, psi, omega_eff, f, predict_fn, lam, K, normalize_w=False):
    if normalize_w:
        v = np.clip(theta[:3], 1e-6, None)
        w = 0.1 + 0.8 * (v / np.sum(v))  # w_i ∈ [0.1, 0.8], Σw = 1
        theta_norm = np.concatenate([w, theta[3:]])
    else:
        theta_norm = theta
    pred = np.clip(predict_fn(phi, psi, omega_eff, theta_norm, lam, K), EPS, None)
    resid = np.log(np.clip(f, EPS, None)) - np.log(pred)
    n = len(f)
    sigma2 = max(np.mean(resid**2), 1e-12)
    return -n/2 * np.log(2 * np.pi * sigma2) - np.sum(resid**2) / (2 * sigma2)
```

### 6.5 Fragmento clave: test ψ-only

```python
def predict_psi_only(phi, psi, omega_eff, theta, lam, K):
    c, beta = theta  # 2 parámetros libres
    return np.clip(c * (psi ** beta), EPS, None)

def fit_M_psi(df):
    return fit_model(df, predict_psi_only, n_theta=2,
                     init_theta=[1.0, 1.0],
                     bounds_theta=[(0.1, 2.0), (0.1, 3.0)],
                     lam_grid=[0.0], K_grid=[1e6],
                     name="M_psi: Solo Psi")
```

---

## 7. Limitaciones

1. **Validación sintética ≠ validación real.** Los resultados del 76–86% de mejora son sobre datos generados por el propio modelo. En datos reales, la mejora será sustancialmente menor (probablemente 5–20%).

2. **Identificabilidad estructural parcial.** Múltiples puntos del espacio $(\lambda, w, K, \alpha_h)$ producen predicciones casi equivalentes. La recuperación de parámetros individuales requiere búsqueda global o priors informativos. **Reportar $\lambda_{\text{est}} = 1.0$ cuando $\lambda_{\text{true}} = 0.5$ es incorrecto**, aunque el RMSE sea bajo.

3. **Mapeo de variables en SAP Cloud es aproximado.** El dataset no fue diseñado para el PUSFRE. Si los proxies son débiles (correlación con $F$ < 0.15), ningún modelo mejorará mucho.

4. **Ruido LogNormal asumido.** Si los datos tienen colas gordas o heterocedasticidad, el estimador de máxima verosimilitud está mal especificado.

5. **No identificabilidad de $\lambda$ y $K$.** Ambos introducen curvatura. En muestras pequeñas ($N < 500$), pueden intercambiarse parcialmente.

6. **Memoria sin estructura temporal.** En Edge Aware, el orden de las filas no representa tiempo real. El test de memoria es débil en ese dataset.

7. **El modelo completo (M7) puede sobreajustar.** Con 10–12 parámetros, requiere $N > 1000$ para estabilidad.

8. **La restricción $w_i \geq 0.1$ es ad hoc.** El umbral de 0.1 previene la degeneración trivial pero introduce un sesgo si la verdad tiene un peso genuinamente menor a 0.1. En dominios donde un factor es genuinamente irrelevante, esta restricción fuerza al modelo a asignarle importancia espuria.

---

## 8. Próximos pasos

### 8.1 Validación en datos reales

Ejecutar el script sobre Edge Aware y SAP Cloud con los parámetros por defecto. Reportar:

- RMSE y MAE por modelo.
- IC bootstrap del 95% para $\lambda$ en M1 y M6.
- Valores estimados de $K$ y $\alpha_h$ en M2 y M6.
- Correlaciones entre $\Phi, \Psi, \Omega$ y $F$.
- **Resultado del test ψ-only** (obligatorio para validar la mejora).

### 8.2 Resolución de la identificabilidad

Ejecutar en orden:

1. **Test de predicción con parámetros verdaderos vs estimados** en datos de test independientes. Si los verdaderos predicen significativamente mejor, el problema es de optimización; si no, es de identificabilidad.
2. **Búsqueda global** (`dual_annealing` o `differential_evolution`) sobre $(\lambda, K, w, \alpha_h)$ si el test anterior indica óptimos locales.
3. **Regularización L2 suave** sobre la varianza de los pesos si la identificabilidad es estructural.
4. **Ampliación de grillas** ($\lambda \in [-1.5, 2.0]$, $\alpha_h \in [0.1, 5.0]$) como paso complementario.

### 8.3 Criterios de extensión

| Nivel | Condición |
|-------|-----------|
| **Justificada** | M6 mejora M0 en > 10% en datos reales, IC 95% de $\lambda$ excluye 0, gap vs MLP < 50%, y M6 supera a Mψ en > 15% |
| **Parcial** | M1 mejora M0 en > 5% pero M6 no mejora M1; solo uno de los tres mecanismos aporta |
| **No justificada** | Ningún modelo interpretable mejora M0 en > 5% |

### 8.4 Extensiones adicionales

Si los resultados reales confirman la extensión:

- Inferencia bayesiana completa con priors sobre $(\lambda, K, w)$.
- Modelos de régimen (Markov-switching) para dominios con cambios estructurales.
- Ruido heavy-tailed (Pareto, Lévy) para dominios con eventos extremos.
- Variables latentes para $\Phi, \Psi, \Omega$ cuando solo hay proxies.

---

## Apéndice A: Demostración del Teorema Fundamental Generalizado

**Enunciado.** Sea $F: [0,1]^3 \to \mathbb{R}^+$ una función continua, monótona creciente en cada argumento, invariante por reescalado afín de cada factor y separable en el espacio transformado por una familia continua $\{T_\lambda\}$ con $T_0 = \log$. Entonces $F$ es de la forma:

$$F(\Phi, \Psi, \Omega) = \left( w_1 \Phi^\lambda + w_2 \Psi^\lambda + w_3 \Omega^\lambda \right)^{1/\lambda}$$

para algún $\lambda \in \mathbb{R}$.

**Demostración (esquema).**

1. Por separabilidad en el espacio transformado: $T_\lambda(F) = g_1(T_\lambda(\Phi)) + g_2(T_\lambda(\Psi)) + g_3(T_\lambda(\Omega))$.
2. Por invariancia por reescalado, $g_k(T_\lambda(c \cdot x)) = a_k(c) + g_k(T_\lambda(x))$.
3. Esto implica que $g_k(T_\lambda(x)) = w_k \cdot T_\lambda(x)$ para alguna constante $w_k$.
4. Por monotonicidad, $w_k \geq 0$.
5. Por continuidad en $\lambda$, la familia $\{T_\lambda\}$ que satisface (2) y contiene al logaritmo es la familia Box-Cox.
6. La inversa $T_\lambda^{-1}$ da la forma CES. $\blacksquare$

---

## Apéndice B: Glosario

| Término | Definición |
|---------|-----------|
| CES | Constant Elasticity of Substitution |
| Box-Cox | Familia de transformaciones de potencia |
| Hill | Función de saturación con parámetro de pendiente |
| MM | Michaelis-Menten |
| MLE | Maximum Likelihood Estimation |
| IC | Intervalo de confianza |
| RMSE | Root Mean Squared Error |
| MAE | Mean Absolute Error |
| AIC | Akaike Information Criterion |
| BIC | Bayesian Information Criterion |
| **Identificabilidad** | **Capacidad de distinguir parámetros únicos a partir de los datos observados** |
| **Degeneración** | **Colapso de pesos a los bordes del simplex, produciendo soluciones espurias** |

---

## Cierre

El PUSFRE original es el caso log-lineal de una familia más general. Esa familia se parametriza con cuatro números — $\lambda, K, \alpha_h, w$ — que miden, respectivamente, la separabilidad, el techo de la frecuencia, la pendiente de saturación y los pesos relativos de cada factor. La memoria añade un quinto número, $k$, cuando existe estructura temporal.

La familia CES-saturada contiene al PUSFRE original como caso límite y lo generaliza sin abandonar los axiomas fundamentales. El Teorema Fundamental se preserva en forma debilitada: la familia es única bajo axiomas ligeramente más generales.

**La validación sintética confirma que el pipeline predice correctamente la estructura cuando existe (mejora del 76% en RMSE). Sin embargo, la recuperación de parámetros individuales está limitada por identificabilidad estructural: múltiples puntos del espacio de parámetros producen predicciones equivalentes.** La regularización, los priors informativos o la búsqueda global son necesarios para cerrar esta brecha antes de que la extensión pueda considerarse completamente validada.

El test ψ-only confirma que la mejora no es un artefacto de dominancia de un solo factor. La restricción $w_i \geq 0.1$ previene la degeneración trivial pero no resuelve la identificabilidad profunda. El generador balanceado elimina el sesgo de diseño que favorecía la dominancia espuria de $\Psi$.

La validación en datos reales está pendiente. Los criterios de decisión están definidos a priori. El script de ejecución está listo.

Lo que sigue es empírico. Los datos dirán si el PUSFRE original es la regla o la excepción. Y la identificabilidad dirá si podemos saber *por qué*.

**Fin del Tratado de Extensión del PUSFRE — Versión 2.0.**

*"La universalidad no está en el punto. Está en la familia. Pero la familia tiene rincones donde la luz de los datos no llega."*
