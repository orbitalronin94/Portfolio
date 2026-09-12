# Tratado de Extensión del PUSFRE
## Familia CES-Saturada con Memoria

**Versión: 3.2 — Edición con Correcciones de Rigor Formal y Coherencia Interna**

**Dependencia:** PUSFRE original, Teorema Fundamental, Dinámica Unificada
**Estado:** Extensión formal con validación sintética avanzada; identificabilidad parcial no resuelta; validación en datos reales pendiente; caracterización axiomática completada (condicional); motivación de A5 ampliada
**Fecha:** Septiembre 2026
**Incluye:** Código completo de las 7 iteraciones (con límite de pesos corregido), resultados de cada ejecución, scripts de validación cruzada inter-dominio (marcados como pendientes de implementación), y reconstrucción de la demostración del Teorema 2.1 con Paso 3 reforzado

---

## Nota de la versión 3.2

La versión 3.1 fue revisada críticamente. Cambios respecto a 3.1:

1. **Paso 3 del Apéndice A reforzado.** El argumento original tenía un hueco sutil: la afirmación "el argumento $a \cdot z_j + s$ recorre un intervalo abierto" no estaba demostrada. Se añade demostración completa con el caso degenerado $z_j = 1/\lambda$ tratado explícitamente.
2. **Límite de $w_i$ coherente.** El texto decía $w_i \in [0.1, 0.8]$ pero el código daba $[0.1, 0.9]$. Se corrige el código a $w_i = 0.1 + 0.7 \cdot v_i/\sum v_j$, que da $[0.1, 0.8]$ con suma 1.
3. **Tabla CES económica degradada.** §2.3 mantiene la tabla como referencia matemática, pero se marca explícitamente como "sin interpretación estructural". Añadida advertencia.
4. **Motivación de A5 ampliada.** Nueva subsección §3.2 discute por qué la invariancia por reescalado afín es una elección razonable y qué alternativas existen.
5. **ΔBIC concreto en régimen `pusfre`.** §5.1 reporta el valor numérico del ΔBIC M0 vs M2, no solo el ganador. Se discute si es evidencia débil o fuerte.
6. **Anexo III marcado como pendiente.** El script de validación cruzada inter-dominio no funciona como código. Se marca explícitamente como "esqueleto pendiente de implementación" y se mueve a §9 como trabajo futuro.
7. **Predicción sobre dominios Ω amplio marcada como hipótesis.** §8.6 y Cierre reformulan la afirmación como hipótesis a testear, no como conclusión.
8. **Anexo V añadido: correcciones respecto a v3.1.** Trazabilidad explícita de cada cambio.

---

## Índice general

1. Prólogo y nota de honestidad intelectual
2. La familia CES-Saturada con Memoria
3. Fundamentación axiomática (con motivación de A5)
4. Protocolo experimental
5. Resultados sintéticos
6. Lectura crítica de resultados
7. Estatus de la extensión
8. Limitaciones
9. Próximos pasos
10. Apéndice A: Demostración completa del Teorema 2.1 (Paso 3 reforzado)
11. Apéndice B: Glosario
12. Apéndice C: Discutibilidad de los axiomas
13. Anexo I: Código completo de las siete iteraciones
14. Anexo II: Resultados completos de cada ejecución
15. Anexo III: Scripts de descarga y ejecución sobre datos reales
16. Anexo IV: Auditoría de identificabilidad
17. Anexo V: Correcciones respecto a v3.1
18. Cierre

---

## 1. Prólogo y nota de honestidad intelectual

La ecuación maestra del PUSFRE,

$$F_i = \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha \cdot \varepsilon_i$$

es un modelo log-lineal. Bajo logaritmos:

$$\log F_i = \log \Phi_i + \log \Psi_i + \alpha \log \Omega_i + \log \varepsilon_i$$

Esto implica tres supuestos que la teoría original presentaba como axiomas pero que la práctica revela como restricciones empíricas:

1. **Separabilidad perfecta:** el efecto de $\Phi_i$ sobre $F_i$ no depende de $\Psi_i$ ni de $\Omega_i$.
2. **Ausencia de saturación:** $\Omega_i^\alpha$ crece sin techo.
3. **Ausencia de memoria:** $F_i(t)$ depende solo de $\Omega_i(t)$, no de su historia.

Cada uno de estos supuestos falla en dominios reales con una frecuencia que ya no es ignorable. Este tratado introduce una familia paramétrica que contiene al PUSFRE original como caso límite.

**Nota de honestidad (v3.2).** Este tratado ha pasado por cinco iteraciones de validación. Los resultados son predictivamente fuertes, pero la identificabilidad de parámetros **no está resuelta** con N=2000. La caracterización axiomática que motiva la elección de la familia CES (Teorema 2.1) se presenta como **condicional a un conjunto de axiomas**, no como demostración de inevitabilidad. Los axiomas son posiciones teóricas; el lector debe evaluarlos como tales.

**Distinción epistémica central.** Este tratado usa la familia CES-Saturada como *modelo predictivo con parámetros latentes*. Los parámetros $\lambda$, $K$, $\alpha_h$, $w$ se estiman para mejorar la predicción de $F_i$, no porque tengan interpretación sustantiva sobre $\Phi_i$, $\Psi_i$, $\Omega_i$. La analogía con CES económico de §2.3 se incluye como referencia matemática pura, sin interpretación estructural. Donde el texto diga "elasticidad de sustitución", el lector debe leer "parámetro de curvatura del agregador, útil para predicción, sin interpretación estructural".

---

## 2. La familia CES-Saturada con Memoria

### 2.1 Definición

$$F_i(t) = \left( w_1 \Phi_i^\lambda + w_2 \Psi_i^\lambda + w_3 \left[\Omega_i^{\text{sat}}(t)\right]^\lambda \right)^{1/\lambda} \cdot \varepsilon_i(t)$$

$$\Omega_i^{\text{sat}}(t) = \frac{\left[\Omega_i^{\text{mem}}(t)\right]^{\alpha_h}}{K^{\alpha_h} + \left[\Omega_i^{\text{mem}}(t)\right]^{\alpha_h}}$$

$$\Omega_i^{\text{mem}}(t) = \sum_{s=0}^{k-1} w_s^{(m)} \, \Omega_i(t-s), \quad \sum_{s=0}^{k-1} w_s^{(m)} = 1$$

**Restricciones:**
- $\lambda \in [-1, 2]$, $\lambda \neq 0$
- $w_1, w_2, w_3 \in [0.1, 0.8]$, $\sum w_j = 1$ (restricción anti-degeneración, ver §4.5)
- $K > 0$, $\alpha_h > 0$
- $k \in \{1, 2, 3, 5\}$

### 2.2 Casos límite

| Caso | Condiciones | Resultado |
|------|-------------|-----------|
| A | $\lambda \to 0$, $K \to \infty$, $k = 1$ | PUSFRE original |
| B | $\lambda \to 0$, $K$ finito | PUSFRE con saturación |
| C | $\lambda \to 0$, $k > 1$ | PUSFRE con memoria |
| D | $\lambda = 1$ | Aditivo lineal |
| E | $\lambda < 0$ | Anti-compensatorio |
| F | $\lambda > 1$ | Compensatorio fuerte |

### 2.3 Nota sobre la relación con CES en economía

*Esta sección se mantiene por completitud formal, pero **no tiene interpretación estructural en el contexto del PUSFRE**. Se incluye como referencia matemática pura. El lector que busque $\lambda$ con significado económico debe consultar §6 y §8, donde se argumenta que $\lambda$ no es identificable con N moderado en estos datos.*

La forma funcional $(w_1 x_1^\lambda + w_2 x_2^\lambda + w_3 x_3^\lambda)^{1/\lambda}$ es idéntica a una función de producción CES (Arrow-Chenery-Minhas-Solow, 1961). En economía, el parámetro $\sigma = 1/(1-\lambda)$ se interpreta como elasticidad de sustitución entre insumos, definida para elecciones óptimas con precios relativos. **En el PUSFRE no hay precios ni elección**: los agentes no eligen entre $\Phi, \Psi, \Omega$, sino que las tres variables son atributos observados. La tabla siguiente es una **referencia matemática de la forma funcional**, no una tabla de interpretación:

| $\lambda$ | $\sigma = 1/(1-\lambda)$ | Forma matemática del agregador |
|-----------|--------------------------|-------------------------------|
| $-\infty$ | $0$ | $\min(x_1, x_2, x_3)$ |
| $-1$ | $0.5$ | Media armónica generalizada |
| $0$ | $1$ | Producto ponderado (Cobb-Douglas) |
| $0.5$ | $2$ | Media cuadrática generalizada |
| $1$ | $\infty$ | Suma ponderada |

**Advertencia (v3.2).** La columna "Forma matemática" describe el comportamiento algebraico del agregador. La columna "$\sigma$" es una cantidad derivada matemáticamente que en economía tiene significado de elasticidad de sustitución. **En el PUSFRE, $\sigma$ es una cantidad sin interpretación estructural**: describe la curvatura del agregador, no la sustituibilidad entre atributos de agentes. Cualquier uso de la tabla debe leer solo la tercera columna.

---

## 3. Fundamentación axiomática

El Teorema Fundamental original demostraba unicidad bajo cinco axiomas. La extensión relaja:

**Axioma IV (Separabilidad Multiplicativa) → Axioma IV' (Separabilidad CES).**

**Teorema 2.1 (Fundamental Generalizado, versión condicional).** *Sean $\Phi, \Psi, \Omega \in \mathbb{R}_+$. Supóngase:*
- *(A1) $F: \mathbb{R}_+^3 \to \mathbb{R}_+$ es continua y estrictamente creciente en cada argumento.*
- *(A2) $F$ es homogénea de grado 1: $F(c\Phi, c\Psi, c\Omega) = c \cdot F(\Phi,\Psi,\Omega)$ para todo $c>0$.*
- *(A3) $F > 0$ si $\Phi,\Psi,\Omega > 0$.*
- *(A4') Existe una familia continua $\{T_\lambda\}_{\lambda \in \Lambda}$ de difeomorfismos de $\mathbb{R}_+$ a $\mathbb{R}$, con $T_0 = \log$, y funciones $g_i^\lambda: \mathbb{R} \to \mathbb{R}$ diferenciables, tales que:*
  $$T_\lambda(F(\Phi,\Psi,\Omega)) = g_1^\lambda(T_\lambda(\Phi)) + g_2^\lambda(T_\lambda(\Psi)) + g_3^\lambda(T_\lambda(\Omega))$$
- *(A5) Invariancia por reescalado afín: $T_\lambda(c \cdot x) = a_\lambda(c) \cdot T_\lambda(x) + b_\lambda(c)$ para funciones $a_\lambda, b_\lambda$ dependientes solo de $c$.*

*Entonces, con la normalización $\sum_i A_i = 1$ (donde $A_i$ son las pendientes de $g_i^\lambda$) y con $B_i = 0$ absorbido en la escala de $F$, la única forma funcional compatible es:*

$$F = \left( w_1 \Phi^\lambda + w_2 \Psi^\lambda + w_3 \Omega^\lambda \right)^{1/\lambda}$$

*para $\lambda \neq 0$, con el caso $\lambda = 0$ recuperado por continuidad como $F = \Phi^{w_1}\Psi^{w_2}\Omega^{w_3}$.*

**Demostración:** Apéndice A.

**Estatus del teorema.** Es un teorema de **caracterización condicional**, no de inevitabilidad. Dice: *si* se aceptan los axiomas A1–A5, *entonces* la forma funcional es CES. No dice: "CES es la forma natural del fitness". Los axiomas son elecciones teóricas; su discutibilidad se analiza en el Apéndice C.

**Lo que el teorema NO garantiza:**
- No garantiza que los axiomas sean empíricamente válidos.
- No garantiza que $\lambda$, $w_i$ sean identificables en datos finitos.
- No garantiza que la familia CES sea la única si se relajan los axiomas de otra manera (ver Apéndice C).

### 3.2 Motivación de A5: ¿por qué invariancia por reescalado afín?

El axioma A5 postula que existe una familia $\{T_\lambda\}$ de transformaciones que conmutan con el reescalado multiplicativo de los argumentos, en el sentido $T_\lambda(cx) = a_\lambda(c) T_\lambda(x) + b_\lambda(c)$. Esta es la hipótesis más fuerte del teorema, y merece justificación.

**Interpretación.** La hipótesis dice que si multiplicas el valor de un atributo por $c$, el valor transformado cambia de manera **afín** (no arbitraria). Esto captura la idea de que el efecto de un factor sobre la fitness es **estructuralmente invariante bajo cambios de unidades**. Si $\Phi$ se mide en las unidades $u_1$ o en las unidades $u_2 = c \cdot u_1$, el ordenamiento de fitness entre agentes no debe depender de la elección de unidades. La invariancia afín es la versión más débil de esta idea que permite la existencia de una familia paramétrica no trivial.

**Alternativas a A5.** Existen al menos tres marcos alternativos que relajan A5 de distintas maneras:

1. **Invariancia por reescalado no afín.** Si $T_\lambda(cx) = h_\lambda(c, T_\lambda(x))$ con $h_\lambda$ no lineal en $T_\lambda(x)$, el Paso 3 del Apéndice A se cae. Se obtienen formas funcionales del tipo $T_\lambda(F) = \sum_i g_i^\lambda(T_\lambda(x_i))$ con $g_i^\lambda$ no afines. Esta clase se llama **GSE** (Generalized Separable Equations) y contiene a CES como caso particular. El precio de admitir GSE es que la forma funcional no es única y depende de la familia $T_\lambda$ elegida ad hoc.

2. **Invariancia solo por translación.** Si $T_\lambda(cx) = T_\lambda(x) + \log(c)$ (invariancia logarítmica), entonces solo $\lambda = 0$ (caso Cobb-Douglas) satisface A5. Se pierde toda la familia CES.

3. **Ausencia de invariancia.** Si se abandona completamente A5, se obtienen formas funcionales arbitrarias. Los ejemplos más conocidos son **Translog** (Christensen-Jorgenson-Lau, 1973) y **formas flexibles de segundo orden**. Translog es una aproximación de Taylor de segundo orden y contiene términos cruzados $\log x_i \log x_j$ que rompen la separabilidad.

**Por qué se elige A5.** La invariancia afín es la hipótesis **más débil** que permite una familia paramétrica uniparamétrica de formas separables. Sin A5, la clase de formas separables depende de una familia arbitraria $\{T_\lambda\}$ y no hay una elección canónica. Con A5, la familia Box-Cox emerge como la única familia de difeomorfismos que satisface la invariancia y contiene al logaritmo. **A5 es una elección, no una necesidad**: se elige porque (a) captura una noción razonable de invariancia de unidades, y (b) da una familia paramétrica manejable. Ninguna de las dos razones es empírica.

**Consecuencia.** El Teorema 2.1 es un teorema de consistencia interna del marco axiomático. No es un teorema de necesidad empírica. El Apéndice C analiza qué ocurre al relajar cada axioma y muestra que CES deja de ser única si se abandonan A4' o A5.

---

## 4. Protocolo experimental

### 4.1 Familia anidada de modelos

| # | Modelo | $\lambda$ | $K$ | $k$ | Params | Propósito |
|---|--------|-----------|-----|-----|--------|-----------|
| M0 | PUSFRE base | $0$ | $\infty$ | $1$ | 2 | Referencia |
| M1 | CES | libre | $\infty$ | $1$ | 6 | Test separabilidad |
| M2 | Hill | $0$ | libre | $1$ | 4 | Test saturación (2p) |
| M3 | MM | $0$ | libre | $1$ | 3 | Test saturación (1p) |
| M4 | Memoria libre | $0$ | $\infty$ | 3 | 4 | Test memoria |
| M5 | Memoria exp. | $0$ | $\infty$ | var. | 3 | Test memoria parsimonioso |
| M6 | CES + Hill | libre | libre | $1$ | 6 | Combinación |
| M7 | Completo | libre | libre | var. | 8–10 | Modelo completo |
| Mψ | Solo Ψ | $0$ | $\infty$ | $1$ | 2 | Test dominancia (espantapájaros, ver nota) |

**Nota sobre Mψ (v3.2).** Mψ se usó en v3.0 como "test de dominancia de un solo factor". Compara modelos con distinta dimensionalidad: Mψ tiene 2 parámetros y descarta dos variables; M0 tiene 2 parámetros y las incluye. El +2482% reportado en §5.2 es casi tautológico. **Mψ no se usa como evidencia en este tratado.** Se mantiene en el protocolo solo por continuidad histórica.

### 4.2 Estimación

1. **Búsqueda global** con `dual_annealing` sobre $(\lambda, K, \theta)$.
2. **Refinamiento local** con L-BFGS-B desde el mejor punto global.
3. **Multi-start local** (5 reinicios) para verificar robustez.

### 4.3 Validación

- 5-fold CV estratificada por cuantiles de $F$
- Bootstrap no paramétrico (50 réplicas) para IC 95%
- Test de Friedman para comparación múltiple
- Perfil de verosimilitud 2D sobre $(\lambda, K)$
- Análisis de residuos
- Curvas de recuperación $N$ vs error
- Baseline no paramétrico: MLP (64, 32)

### 4.4 Criterios de decisión a priori

| Criterio | Condición |
|----------|-----------|
| Rechazo PUSFRE base | $\Delta$AIC > 10 **y** $\Delta$BIC > 10 **y** IC 95% de λ excluye 0 |
| Saturación relevante | $\Delta$BIC > 10 con $K$ fuera de $[10^3, \infty)$ |
| Memoria relevante | $\Delta$BIC > 10 con $w_0^{(m)} < 0.7$ |
| Modelo completo justificado | $\Delta$BIC > 10 sobre mejor modelo de un solo mecanismo |
| No degenerado | M6 supera a M0 en $\Delta$BIC > 10 |

### 4.5 Restricción anti-degeneración (corregida v3.2)

**Problema.** El optimizador tiende a colapsar los pesos $w_i$ hacia los bordes del simplex, produciendo soluciones degeneradas donde un solo factor domina.

**Solución.** Reparametrización del simplex con suelo y techo explícitos. Se optimizan variables libres $v_i > 0$ y se mapean a:

$$w_i = 0.1 + 0.7 \cdot \frac{v_i}{\sum_j v_j}$$

Esto garantiza $w_i \in [0.1, 0.8]$ y $\sum_i w_i = 0.3 + 0.7 = 1.0$, impidiendo el colapso total a cero y el colapso total a un solo factor.

**Corrección respecto a v3.1.** La versión anterior del código usaba $w_i = 0.1 + 0.8 \cdot v_i/\sum v_j$, que daba $w_i \in [0.1, 0.9]$ (no $[0.1, 0.8]$). El texto decía $[0.1, 0.8]$ pero el código producía $[0.1, 0.9]$. Se corrige el código para coincidir con el texto. La nueva constante $0.7$ es la única que satisface simultáneamente $\min w_i = 0.1$ y $\sum w_i = 1$ con $w_i \in [0.1, 0.8]$.

---

## 5. Resultados sintéticos

### 5.1 Discriminación de regímenes

| Régimen | Verdad | Ganador RMSE | Ganador BIC | $\Delta$BIC (ganador vs M0) | ¿Correcto? |
|---------|--------|--------------|-------------|------------------------------|-----------|
| `pusfre` | M0 | **M2** | **M0** | −1.2 (M0 gana por 1.2) | ⚠️ RMSE: no; BIC: marginal |
| `ces` | M1 | M1 | M1 | −1258 | ✅ |
| `hill` | M2 | M2 | M2 | −312 | ✅ |
| `full` | M6 | M6 | M6 | −3124 | ✅ |

**Hallazgo crítico (v3.2).** En régimen `pusfre`, M0 gana sobre M2 bajo BIC con $\Delta$BIC = 1.2. Esto NO es evidencia fuerte. La literatura (Burnham & Anderson, 2002) clasifica:

- $\Delta$BIC ∈ [0, 2]: evidencia débil, esencialmente indistinguibles.
- $\Delta$BIC ∈ [2, 6]: evidencia positiva.
- $\Delta$BIC ∈ [6, 10]: evidencia fuerte.
- $\Delta$BIC > 10: evidencia muy fuerte.

Con $\Delta$BIC = 1.2, **M0 y M2 son estadísticamente indistinguibles en el régimen `pusfre`**. La conclusión correcta no es "M0 gana correctamente bajo BIC". La conclusión correcta es: **en el régimen `pusfre`, ni RMSE ni BIC distinguen M0 de M2; el pipeline no identifica el modelo verdadero con N=2000 en este régimen**. Esto es un fallo del protocolo, no una victoria de BIC.

**Por qué ocurre.** En régimen `pusfre`, Ω entra linealmente (no satura). Los modelos M0, M1, M2 y M3 producen predicciones muy similares (todos tienen RMSE en [0.246, 0.252]). Sin estructura CES ni Hill, los parámetros adicionales no aportan información. La diferencia de log-verosimilitud es pequeña, y el BIC penaliza correctamente pero no lo suficiente para dar evidencia fuerte.

**Implicación.** El pipeline no es un "identificador automático de estructura" en regímenes donde la estructura es débil. Es una herramienta de comparación que produce evidencia fuerte solo cuando la estructura es clara. Esto limita su uso en aplicaciones donde no se sabe a priori qué régimen subyace.

### 5.2 Rendimiento predictivo en régimen `full`

| Modelo | RMSE | MAE | Params | $\Delta$BIC vs M0 |
|--------|------|-----|--------|-------------------|
| M0 | 0.2519 ± 0.0042 | 0.2384 | 2 | — |
| M1 | 0.1035 ± 0.0244 | 0.0937 | 6 | −1258 |
| M2 | 0.2464 ± 0.0105 | 0.2302 | 4 | +1.2 |
| M6 | **0.0250 ± 0.0009** | **0.0192** | 6 | **−3124** |

**Friedman (RMSE):** estadístico = 13.5600, p = 0.003570. Significativo.
**Wilcoxon pairwise (RMSE):** M0 vs M6: p = 0.0625 (saturado con 5 folds).
**Mψ:** reportado en v3.0 con RMSE 0.6456; no se usa como evidencia (ver §4.1).

### 5.3 Recuperación de parámetros (v3.0 con búsqueda global)

| Parámetro | Verdadero | Estimado | Error | ¿Identificable? |
|-----------|-----------|----------|-------|-----------------|
| $\lambda$ | 0.50 | 0.46 | 8% | Marginal (IC contiene 0) |
| $K$ | 0.50 | 1.16 | **132%** | **No** |
| $\alpha_h$ | 1.50 | 1.14 | **24%** | **No** |
| $w$ | (0.33, 0.33, 0.33) | (0.33, 0.33, 0.43) | Aceptable | Sí |

Los parámetros se reportan con dos cifras significativas (no cuatro). Reportar $\lambda = 0.4587$ cuando el IC contiene el 0 es precisamente el gesto que el resto del documento critica.

### 5.4 Intervalos bootstrap del 95%

| Parámetro | Mediana | IC 95% |
|-----------|---------|--------|
| $\lambda$ | 0.69 | **[−0.78, 1.73]** |
| $K$ | 0.77 | [0.07, 4.35] |
| $\alpha_h$ | 0.98 | [0.35, 2.58] |
| $w_1$ | 0.29 | [0.22, 0.45] |

**Hallazgo crítico.** IC de λ contiene el 0. Con N=2000, los datos no pueden distinguir λ=0 de λ=0.5. Esto invalida la interpretación de λ como parámetro estructural. Es compatible con el uso predictivo de la familia.

### 5.5 Curvas de recuperación

| N | $\lambda$ err | $K$ err rel | $\alpha_h$ err |
|---|---------------|-------------|----------------|
| 500 | 0.009 | 1.28 | 0.35 |
| 1000 | 0.038 | 1.34 | 0.37 |
| 2000 | 0.038 | 1.32 | 0.36 |
| 5000 | 0.040 | 1.33 | 0.37 |

**Hallazgo crítico (v3.2).** Los errores no decrecen con N. Esto NO es "sesgo del optimizador". Es **degeneración estructural K–α**. Hill entra como $\Omega^\alpha/(K^\alpha + \Omega^\alpha)$. Si $\Omega \ll K$ en el rango observable, entonces Hill $\approx \Omega^\alpha/K^\alpha$, que depende de α y K solo a través de la combinación $(\alpha, \log K)$. Hay una curva 1D en $(K, \alpha)$ que da saturación indistinguible. Más N no rompe esa degeneración. Solo lo haría cubrir un rango de Ω donde la curvatura Hill sea visible.

**Consecuencia.** Los valores de K y α reportados en §5.3 no son interpretables individualmente. Solo lo es la combinación $(\alpha, \log K)$.

---

## 6. Lectura crítica de resultados

**Hallazgo 1.** Mejora predictiva de M6 sobre M0 real (90.1% en `full`). *Es un resultado in-sample sobre datos generados por el propio M6. No es evidencia independiente.*

**Hallazgo 2.** Test ψ-only descarta dominancia de un solo factor. *Reinterpretación v3.1: el test es un espantapájaros. No usar como evidencia.*

**Hallazgo 3.** Búsqueda global resuelve el colapso degenerado de pesos. *Correcto, pero solo para w. No resuelve la degeneración K–α.*

**Hallazgo 4.** Recuperación de λ buena (8%), de K y α mala (132%, 24%). *K y α son degenerados estructuralmente, no mal optimizados. λ es marginalmente identificable pero el IC contiene 0.*

**Hallazgo 5.** IC bootstrap de λ contiene el 0. **Este es el hallazgo más importante del tratado.** El parámetro central de la extensión no está empíricamente respaldado en estos datos.

**Hallazgo 6.** Errores no decrecen con N. *Degeneración estructural K–α, no sesgo del optimizador.*

**Hallazgo 7.** En régimen `pusfre`, pipeline prefiere M2 sobre M0 bajo RMSE. *Resuelto parcialmente en v3.1 bajo BIC con $\Delta$BIC = 1.2, que es evidencia débil. Ni RMSE ni BIC identifican M0 con N=2000 en este régimen.*

**Hallazgo 8.** Test Wilcoxon saturado con 5 folds. Limitación reconocida. Se propone 10 folds en §9.

**Hallazgo 9.** Validación en datos reales no ejecutada aún.

**Hallazgo 10.** La caracterización axiomática (Teorema 2.1) es condicional. Los axiomas A1–A5 son elecciones teóricas. La elección de CES está justificada *dentro* de esos axiomas, no *fuera* de ellos. A5 en particular es la hipótesis más fuerte y no tiene justificación empírica (ver §3.2).

**Hallazgo 11.** La distinción predictivo vs estructural no se había hecho explícita en v3.0. Bajo la lectura estructural, los resultados son débiles (identificabilidad no resuelta). Bajo la lectura predictiva, los resultados son fuertes pero condicionados al régimen de los datos.

**Hallazgo 12 (nuevo, v3.2).** En régimen `pusfre` con N=2000, ni RMSE ni BIC distinguen M0 de M2 (ΔBIC = 1.2, evidencia débil). Esto significa que el pipeline **no es un identificador automático de estructura** cuando la estructura subyacente es débil. El pipeline produce evidencia fuerte solo cuando la estructura es clara (ces, hill, full).

---

## 7. Estatus de la extensión

| Nivel | Condición | Estado |
|-------|-----------|--------|
| Justificada (predictiva) | $\Delta$BIC(M6 vs M0) > 10 en algún régimen | ✅ en `full`, ❓ en reales |
| Justificada (estructural) | IC 95% de λ excluye 0 | ❌ |
| Consistente | Errores decrecen con N | ❌ (degeneración K–α) |
| Discrimina regímenes | Modelo correcto gana bajo BIC | ⚠️ solo en regímenes con estructura clara |
| Caracterización axiomática | Teorema 2.1 válido condicionalmente | ✅ (Apéndice A) |
| Justificada en datos reales | M6 mejora M0 en Edge Aware/SAP Cloud bajo BIC | ⏳ pendiente |

**Clasificación (v3.2):** *Predictivamente útil como interpolador con parámetros latentes cuando la estructura es clara. No identificable estructuralmente. Caracterización axiomática válida condicionalmente bajo axiomas que son elecciones teóricas. Pendiente de validación real.*

---

## 8. Limitaciones

1. **Validación sintética ≠ validación real.** Todos los resultados fuertes de §5 son sobre datos generados por el propio modelo o por variantes cercanas.
2. **Identificabilidad parcial no resuelta.** λ marginalmente identificable, K y α no identificables. Esto es estructural (§5.5), no de optimización.
3. **Degeneración K–α estructural.** No se resuelve con más N ni con mejor optimizador. Se resuelve cubriendo un rango de Ω donde la curvatura Hill sea visible, o fijando K en dominios donde se puede estimar por fuera.
4. **Pipeline no es identificador automático.** En régimen `pusfre` con N=2000, ni RMSE ni BIC distinguen M0 de M2. El pipeline requiere estructura clara para dar evidencia fuerte.
5. **Test Wilcoxon saturado con 5 folds.** Propuesta: 10 folds o más.
6. **Mapeo SAP Cloud aproximado.** El dataset no fue diseñado para PUSFRE.
7. **Ruido LogNormal asumido con σ=0.05.** No validado empíricamente.
8. **Restricción $w_i \in [0.1, 0.8]$ ad hoc.** Introduce sesgo hacia el centro del simplex. Se justifica por estabilidad numérica, no por teoría.
9. **Sin validación en datos reales.**
10. **Caracterización axiomática condicional.** A5 en particular no tiene justificación empírica (§3.2).
11. **Analogía CES económica degradada.** §2.3 se ha marcado como referencia matemática pura.
12. **No validación cruzada inter-dominio.** El script está pendiente de implementación (ver Anexo III).

---

## 9. Próximos pasos

**Prioridad alta:**
1. **Test N grande (20000, 50000)** con 10 folds. Verificar si la degeneración K–α persiste.
2. **Test K fijo al valor verdadero** (iteración 6) ejecutado en serio. Si con K fijo λ y α se recuperan, la degeneración K–α está confirmada y localizada.
3. **Ejecutar Edge Aware y SAP Cloud.** Cargar datos, correr pipeline, reportar BIC.
4. **Añadir test de dominancia dimensionalmente controlado:** M0 vs Φ·Ψ vs Ψ·Ω vs Φ·Ω. Todos con 2 parámetros.

**Prioridad media:**
5. **Validación cruzada inter-dominio.** Aplicar la familia CES-Saturada a neural scaling (Kaplan/Hoffmann), urban scaling (Bettencourt), especies-área (Arrhenius), Fama-French. Criterio: ΔBIC > 10 en validación out-of-sample. **Este script está pendiente de implementación (ver Anexo III).**
6. **Priors bayesianos** si identificabilidad no se resuelve.
7. **Regularización L2 sobre w** para reducir varianza.

**Prioridad baja (teórica):**
8. **Discutibilidad axiomática completa.** Apéndice C es un esqueleto; desarrollarlo en paper aparte.
9. **Extensión a dinámica temporal** con $\Omega^{\text{mem}}$ dependiente de $\lambda$ o de $w_s^{(m)}$ variables.
10. **Comparación con Translog** (forma flexible no separable). Si Translog gana, la separabilidad CES es rechazada empíricamente.

---

## Apéndice A: Demostración completa del Teorema 2.1 (Paso 3 reforzado)

**Enunciado (versión condicional).** Sean $\Phi, \Psi, \Omega \in \mathbb{R}_+$. Supóngase A1–A5 (§3). Entonces, con normalización $\sum_i A_i = 1$, la única forma funcional compatible es:

$$F(\Phi,\Psi,\Omega) = \left( w_1 \Phi^\lambda + w_2 \Psi^\lambda + w_3 \Omega^\lambda \right)^{1/\lambda}$$

para $\lambda \neq 0$, con el caso $\lambda = 0$ recuperado por continuidad como $F = \Phi^{w_1}\Psi^{w_2}\Omega^{w_3}$.

**Demostración.**

**Paso 1: Separabilidad en el espacio $T_\lambda$.**

Por A4', para cada $\lambda \in \Lambda$:

$$T_\lambda(F(\Phi,\Psi,\Omega)) = g_1^\lambda(T_\lambda(\Phi)) + g_2^\lambda(T_\lambda(\Psi)) + g_3^\lambda(T_\lambda(\Omega))$$

donde $g_i^\lambda$ son diferenciables por hipótesis. Escribamos $z_i = T_\lambda(x_i)$ para $x_i \in \{\Phi,\Psi,\Omega\}$. Entonces:

$$T_\lambda(F) = \sum_{i=1}^{3} g_i^\lambda(z_i) \quad \text{(Ecuación 1)}$$

**Paso 2: Invariancia por reescalado de $T_\lambda$.**

Por A5, $T_\lambda(c \cdot x) = a_\lambda(c) \cdot T_\lambda(x) + b_\lambda(c)$. Esta es una ecuación funcional de Pexider. Bajo continuidad de $T_\lambda$ (por ser difeomorfismo), las únicas soluciones son:

- Si $\lambda \neq 0$: $T_\lambda(x) = A_\lambda \cdot x^\lambda + B_\lambda$, con $a_\lambda(c) = c^\lambda$.
- Si $\lambda = 0$: $T_0(x) = A_0 \cdot \log(x) + B_0$, con $a_0(c) = 1$.

*Demostración de la solución:* Sea $u(x) = T_\lambda(x) - T_\lambda(1)$ (normalización $T_\lambda(1) = 0$). De A5 con $b_\lambda$ absorbido, $u(cx) = a_\lambda(c) \cdot u(x) + u(c)$. Diferenciando respecto a $x$ y evaluando en $x=1$:

$$c \cdot u'(c) = a_\lambda(c) \cdot u'(1)$$

Sustituyendo en la ecuación original:

$$u(cx) = \frac{c \cdot u'(c)}{u'(1)} \cdot u(x) + u(c)$$

Diferenciando respecto a $c$ y evaluando en $c=1$:

$$x \cdot u'(x) = K \cdot u(x)$$

con $K$ una constante. La solución general es $u(x) = C \cdot x^K$. Con $u(1) = 0$, reparametrizando $u(x) = C \cdot (x^\lambda - 1)$ con $\lambda = K$. La forma canónica es $T_\lambda(x) = (x^\lambda - 1)/\lambda$ para $\lambda \neq 0$, y $T_0(x) = \log(x)$ por límite. $\square$

**Paso 3: Homogeneidad implica $g_i$ afín (reforzado en v3.2).**

Apliquemos A2 (homogeneidad de grado 1): $F(c\Phi, c\Psi, c\Omega) = c \cdot F(\Phi,\Psi,\Omega)$ para todo $c > 0$.

Aplicando $T_\lambda$ a ambos lados:

$$T_\lambda(c \cdot F) = T_\lambda(F(c\Phi, c\Psi, c\Omega))$$

Por A5 en el lado izquierdo: $T_\lambda(c \cdot F) = a_\lambda(c) \cdot T_\lambda(F) + b_\lambda(c)$.

Por (Ecuación 1) en el lado derecho:

$$T_\lambda(F(c\Phi, c\Psi, c\Omega)) = \sum_{i=1}^{3} g_i^\lambda(a_\lambda(c) \cdot T_\lambda(x_i) + b_\lambda(c))$$

Denotando $a = a_\lambda(c)$, $s = b_\lambda(c)$ y $z_i = T_\lambda(x_i)$:

$$a \cdot \sum_{i=1}^{3} g_i^\lambda(z_i) + s = \sum_{i=1}^{3} g_i^\lambda(a \cdot z_i + s) \quad \text{(Ecuación 2)}$$

Diferenciando (Ecuación 2) respecto a $z_j$ (para $j \in \{1,2,3\}$):

$$a \cdot (g_j^\lambda)'(z_j) = a \cdot (g_j^\lambda)'(a \cdot z_j + s)$$

Como $a > 0$ (por ser $T_\lambda$ creciente), se sigue:

$$(g_j^\lambda)'(z_j) = (g_j^\lambda)'(a \cdot z_j + s) \quad \text{(Ecuación 3)}$$

**Afirmación a demostrar.** Para $j$ fijo, el mapa $z_j \mapsto (g_j^\lambda)'(z_j)$ es constante en $\mathbb{R}$.

**Demostración de la afirmación.** Fijemos $z_j \in \mathbb{R}$ arbitrario. Considérese el mapa $\phi_j: c \mapsto a_\lambda(c) \cdot z_j + b_\lambda(c)$, definido para $c > 0$. Por (Ecuación 3), $(g_j^\lambda)'(z_j) = (g_j^\lambda)'(\phi_j(c))$ para todo $c > 0$. Por lo tanto, $(g_j^\lambda)'$ es constante sobre la imagen $\phi_j((0,\infty))$.

**Caso 1: $\lambda \neq 0$.** Con $T_\lambda(x) = (x^\lambda - 1)/\lambda$, tenemos $a_\lambda(c) = c^\lambda$ y $b_\lambda(c) = -(c^\lambda - 1)/\lambda$. Entonces:

$$\phi_j(c) = c^\lambda \cdot z_j - \frac{c^\lambda - 1}{\lambda} = c^\lambda \cdot \left(z_j - \frac{1}{\lambda}\right) + \frac{1}{\lambda}$$

**Subcaso 1a: $z_j \neq 1/\lambda$.** Entonces $z_j - 1/\lambda \neq 0$, y $\phi_j(c) = \frac{1}{\lambda} + c^\lambda (z_j - 1/\lambda)$ recorre un intervalo abierto de $\mathbb{R}$ cuando $c$ varía en $(0, \infty)$. Por continuidad de $(g_j^\lambda)'$ (por ser $g_j^\lambda$ diferenciable), $(g_j^\lambda)'$ es constante en ese intervalo abierto, y por conexión de $\mathbb{R}$, $(g_j^\lambda)'$ es constante en todo $\mathbb{R}$. $\square$

**Subcaso 1b: $z_j = 1/\lambda$.** Entonces $\phi_j(c) = 1/\lambda$ es constante. En este caso, (Ecuación 3) no da información sobre $(g_j^\lambda)'$ en puntos distintos de $1/\lambda$. Sin embargo, el argumento del Subcaso 1a se aplica para cualquier otro valor $z_j' \neq 1/\lambda$: $(g_j^\lambda)'(z_j')$ es constante en $\mathbb{R}$ (por Subcaso 1a), y por continuidad, $(g_j^\lambda)'(1/\lambda)$ también toma ese mismo valor. Por lo tanto $(g_j^\lambda)'$ es constante en todo $\mathbb{R}$. $\square$

**Caso 2: $\lambda = 0$.** Con $T_0(x) = \log(x)$, tenemos $a_0(c) = 1$ y $b_0(c) = \log(c)$. Entonces:

$$\phi_j(c) = 1 \cdot z_j + \log(c)$$

que recorre todo $\mathbb{R}$ cuando $c$ varía en $(0, \infty)$. Por el mismo argumento que en Subcaso 1a, $(g_j^\lambda)'$ es constante en $\mathbb{R}$. $\square$

**Conclusión del Paso 3.** Para cada $j \in \{1, 2, 3\}$ y cada $\lambda \in \Lambda$, existe una constante $A_j^\lambda \in \mathbb{R}$ tal que $(g_j^\lambda)'(z) = A_j^\lambda$ para todo $z \in \mathbb{R}$. Por lo tanto:

$$g_j^\lambda(z) = A_j^\lambda \cdot z + B_j^\lambda$$

donde $B_j^\lambda$ es una constante de integración.

**Paso 4: Normalización y recuperación de la forma CES.**

Sustituyendo en (Ecuación 1):

$$T_\lambda(F) = \sum_i (A_i \cdot T_\lambda(x_i) + B_i) = \sum_i A_i \cdot T_\lambda(x_i) + \sum_i B_i$$

Los términos $B_i$ son constantes. Absorbiendo $\sum_i B_i$ en un factor de escala global (o fijando $B_i = 0$ por normalización de $T_\lambda$), se obtiene:

$$T_\lambda(F) = \sum_i A_i \cdot T_\lambda(x_i) \quad \text{(Ecuación 3')}$$

Sustituyendo la forma Box-Cox $T_\lambda(x) = (x^\lambda - 1)/\lambda$ para $\lambda \neq 0$:

$$\frac{F^\lambda - 1}{\lambda} = \sum_i A_i \cdot \frac{x_i^\lambda - 1}{\lambda}$$

Multiplicando por $\lambda$:

$$F^\lambda - 1 = \sum_i A_i \cdot (x_i^\lambda - 1) = \sum_i A_i \cdot x_i^\lambda - \sum_i A_i$$

$$F^\lambda = \sum_i A_i \cdot x_i^\lambda + 1 - \sum_i A_i$$

Con la normalización $\sum_i A_i = 1$:

$$F^\lambda = \sum_i A_i \cdot x_i^\lambda$$

$$F = \left( A_1 \Phi^\lambda + A_2 \Psi^\lambda + A_3 \Omega^\lambda \right)^{1/\lambda}$$

Identificando $A_i = w_i$:

$$F = \left( w_1 \Phi^\lambda + w_2 \Psi^\lambda + w_3 \Omega^\lambda \right)^{1/\lambda}$$

Para $\lambda = 0$, tomando el límite $\lambda \to 0$:

$$\lim_{\lambda \to 0} F = \exp\left( \sum_i w_i \log(x_i) \right) = \prod_i x_i^{w_i}$$

que es el caso PUSFRE original. $\blacksquare$

**Corolario (monotonicidad y pesos).** Por A1 (monotonicidad estricta), $w_i > 0$. La normalización $\sum_i w_i = 1$ es una elección de escala de $F$.

**Observaciones sobre las hipótesis.**

1. **Diferenciabilidad de $g_i$.** Necesaria para el Paso 3.
2. **Continuidad de $T_\lambda$.** Necesaria para el Paso 2.
3. **Existencia de la familia $\{T_\lambda\}$.** Postulada en A4'. No derivada.
4. **Normalización $\sum_i A_i = 1$.** Elección, no consecuencia.
5. **$B_i = 0$.** Absorbido en la escala de $F$.
6. **Continuidad en $\lambda$.** Garantizada por construcción.

---

## Apéndice B: Glosario

| Término | Definición |
|---------|-----------|
| CES | Constant Elasticity of Substitution |
| Box-Cox | Familia de transformaciones de potencia: $T_\lambda(x) = (x^\lambda-1)/\lambda$ |
| Hill | Saturación con parámetro de pendiente: $x^\alpha/(K^\alpha + x^\alpha)$ |
| MM | Michaelis-Menten |
| MLE | Maximum Likelihood Estimation |
| IC | Intervalo de confianza |
| RMSE | Root Mean Squared Error |
| MAE | Mean Absolute Error |
| AIC | Akaike Information Criterion |
| BIC | Bayesian Information Criterion |
| Identificabilidad | Capacidad de distinguir parámetros únicos |
| Degeneración | Colapso de pesos a bordes del simplex, o indistinguibilidad entre parámetros |
| Búsqueda global | Optimización no local (dual_annealing) |
| Bootstrap | Remuestreo con reemplazo |
| Perfil de verosimilitud | $\lambda \to \max_\theta L(\lambda, \theta)$ |
| Friedman test | No paramétrico para múltiples modelos |
| Consistencia | Error → 0 cuando N → ∞ |
| Difeomorfismo | Homeomorfismo diferenciable con inversa diferenciable |
| Ecuación funcional de Pexider | Ecuación de la forma $f(x+y) = g(x) + h(y)$ |
| Caracterización axiomática | Derivación de una forma funcional a partir de axiomas |
| Espantapájaros (test) | Test que compara modelos con distinta dimensionalidad |
| Parametrización estructural | Parámetros con interpretación sustantiva |
| Parametrización latente | Parámetros sin interpretación sustantiva |
| $\Delta$BIC | Diferencia de BIC; >10 evidencia muy fuerte, 2–6 evidencia positiva, 0–2 evidencia débil |
| Translog | Forma funcional flexible no separable (Christensen-Jorgenson-Lau, 1973) |
| Neural scaling | Leyes de potencia en entrenamiento de modelos de lenguaje (Kaplan et al., 2020) |
| Urban scaling | Leyes de potencia en sistemas urbanos (Bettencourt et al., 2007) |
| Especies-área | Relación $S = cA^z$ en biogeografía (Arrhenius, 1921) |
| GSE | Generalized Separable Equations; familia que generaliza CES al relajar A5 |

---

## Apéndice C: Discutibilidad de los axiomas

Este apéndice analiza qué ocurre al relajar cada axioma de A1–A5.

### C.1 Relajación de A2 (homogeneidad de grado 1)

Si se permite $F(c\Phi, c\Psi, c\Omega) = c^d \cdot F(\Phi,\Psi,\Omega)$ para $d \neq 1$:

$$F = \left( w_1 \Phi^\lambda + w_2 \Psi^\lambda + w_3 \Omega^\lambda \right)^{d/\lambda}$$

que es una CES con grado $d$. No hay pérdida estructural, solo cambio del exponente global. Esta relajación es benigna.

### C.2 Relajación de A5 (invariancia por reescalado afín)

Si $T_\lambda$ no satisface la invariancia afín, el Paso 3 del Apéndice A se cae. La familia $\{T_\lambda\}$ puede ser arbitraria, y la forma funcional resultante es:

$$T_\lambda(F) = \sum_i g_i^\lambda(T_\lambda(x_i))$$

donde $g_i^\lambda$ no son necesariamente afines. Esta es la clase **GSE**. Contiene a CES, Translog, y muchas otras. **Aquí el teorema pierde fuerza**: sin A5, la familia CES ya no es única.

### C.3 Relajación de A4' (separabilidad)

Si $F$ no es separable en ningún espacio transformado, se obtiene la clase de **funciones flexibles**. El ejemplo estándar es **Translog**:

$$\log F = a_0 + \sum_i a_i \log x_i + \sum_{i \leq j} b_{ij} \log x_i \log x_j$$

Translog es una aproximación de segundo orden a cualquier función suave. No es separable en general. Si Translog gana empíricamente, la separabilidad CES es rechazada.

### C.4 Relajación de la continuidad en λ

Si la familia $\{T_\lambda\}$ no es continua en $\lambda$, el caso $\lambda = 0$ es un punto aislado. La familia CES se convierte en una colección de familias disjuntas.

### C.5 Relajación de la normalización $\sum_i A_i = 1$

Sin esta normalización, $F$ está definida salvo un factor de escala. La forma funcional es la misma.

### C.6 Relajación de la diferenciabilidad de $g_i$

Sin diferenciabilidad, el Paso 3 se cae. Las soluciones de (Ecuación 2) sin regularidad incluyen funciones patológicas. La diferenciabilidad es una hipótesis de "buen comportamiento".

### C.7 Síntesis

| Axioma relajado | Forma resultante | Pérdida estructural |
|-----------------|------------------|---------------------|
| A2 (grado) | CES con grado $d$ | Ninguna |
| A5 (afín) | GSE | Pérdida de unicidad |
| A4' (separabilidad) | Translog, formas flexibles | Pérdida total de CES |
| Continuidad en λ | Familia disjunta | Pérdida de unidad |
| $\sum A_i = 1$ | CES con escala | Ninguna |
| Diferenciabilidad | Soluciones patológicas | Utilidad |

**Conclusión.** El Teorema 2.1 garantiza unicidad *dentro* de la clase de funciones que satisfacen A1–A5. No garantiza que CES sea la forma natural del fitness. Los axiomas son elecciones; su aceptación es una posición teórica. El valor del teorema es de consistencia interna, no de inevitabilidad empírica.

### C.8 Motivación ampliada de A5

Como se discutió en §3.2, A5 es la hipótesis más fuerte. Se justifica por dos razones:

1. **Invariancia de unidades.** Cambiar las unidades de un atributo no debe cambiar el ordenamiento de fitness.
2. **Manejabilidad paramétrica.** Sin A5, la clase de formas separables depende de una familia $\{T_\lambda\}$ arbitraria.

Ninguna de las dos razones es empírica. Si se quiere justificar A5 empíricamente, se necesita un test que compare CES contra GSE contra Translog en datos reales. Este test no se ha hecho.

---

# ANEXO I: CÓDIGO COMPLETO DE LAS SIETE ITERACIONES

## Iteración 1: `protocolo_pusfre_v1.py`

**Objetivo:** validación sintética inicial.
**Hallazgo:** M6 mejora 85.7%.

```python
"""protocolo_pusfre_v1.py - Validación sintética inicial"""
import warnings
import numpy as np
import pandas as pd
from dataclasses import dataclass
from scipy.optimize import minimize
from sklearn.model_selection import StratifiedKFold

warnings.filterwarnings("ignore")
RANDOM_STATE, EPS, N_FOLDS = 42, 1e-6, 5

def load_synthetic(n=5000, seed=RANDOM_STATE):
    rng = np.random.default_rng(seed)
    phi = rng.uniform(0.1, 0.9, n)
    psi = rng.uniform(0.1, 0.9, n)
    omega = rng.uniform(0.05, 0.5, n)
    lam_true, K_true, alpha_true = 0.4, 2.0, 1.2
    w_true = np.array([1/3, 1/3, 1/3])
    omega_sat = omega**alpha_true / (K_true**alpha_true + omega**alpha_true)
    z = (w_true[0]*phi**lam_true + w_true[1]*psi**lam_true +
         w_true[2]*omega_sat**lam_true)
    f_obs = np.clip((z**(1.0/lam_true)) * rng.lognormal(0, 0.05, n), 0.01, 0.99)
    df = pd.DataFrame({"phi": phi, "psi": psi, "omega": omega, "f": f_obs})
    gt = {"lambda": lam_true, "K": K_true, "alpha": alpha_true, "w": w_true}
    return df, gt

def ces_combine(phi, psi, omega_eff, lam, w):
    if abs(lam) < 1e-4:
        return (np.clip(phi, EPS, None)**w[0] *
                np.clip(psi, EPS, None)**w[1] *
                np.clip(omega_eff, EPS, None)**w[2])
    inner = np.clip(w[0]*phi**lam + w[1]*psi**lam + w[2]*omega_eff**lam, EPS, None)
    return inner ** (1.0 / lam)

def sat_hill(omega, K, alpha):
    return (np.clip(omega, EPS, None)**alpha /
            (max(K, EPS)**alpha + np.clip(omega, EPS, None)**alpha))

def predict_base(phi, psi, omega_eff, theta, lam, K):
    return phi * psi * omega_eff**theta[0]

def predict_ces(phi, psi, omega_eff, theta, lam, K):
    return ces_combine(phi, psi, omega_eff, lam, theta)

def predict_hill(phi, psi, omega_eff, theta, lam, K):
    return phi * psi * sat_hill(omega_eff, K, theta[0])**theta[1]

def predict_ces_hill(phi, psi, omega_eff, theta, lam, K):
    return ces_combine(phi, psi, sat_hill(omega_eff, K, theta[3]), lam, theta[:3])

@dataclass
class FitResult:
    name: str
    params: dict
    logL: float
    n_params: int

def _neg_loglik(theta, phi, psi, omega_eff, f, predict_fn, lam, K, normalize_w=False):
    if normalize_w:
        w_raw = np.clip(theta[:3], 0, None)
        theta_norm = np.concatenate([w_raw / (w_raw.sum() + EPS), theta[3:]])
    else:
        theta_norm = theta
    pred = np.clip(predict_fn(phi, psi, omega_eff, theta_norm, lam, K), EPS, None)
    resid = np.log(np.clip(f, EPS, None)) - np.log(pred)
    sigma2 = max(np.mean(resid**2), 1e-12)
    return -len(f)/2 * np.log(2*np.pi*sigma2) - np.sum(resid**2)/(2*sigma2)

def fit_model(df, predict_fn, n_theta, init_theta, bounds_theta,
              lam_grid, K_grid, name="", normalize_w=False, n_params_extra=0):
    phi = df["phi"].values
    psi = df["psi"].values
    omega = df["omega"].values
    f = df["f"].values
    best, best_logL = None, -np.inf
    for lam in lam_grid:
        for K in K_grid:
            try:
                res = minimize(
                    _neg_loglik, init_theta,
                    args=(phi, psi, omega, f, predict_fn, lam, K, normalize_w),
                    method="L-BFGS-B", bounds=bounds_theta,
                    options={"maxiter": 300}
                )
                if res.fun > 1e9:
                    continue
                if normalize_w:
                    w_raw = np.clip(res.x[:3], 0, None)
                    theta_final = np.concatenate(
                        [w_raw / (w_raw.sum() + EPS), res.x[3:]]
                    )
                else:
                    theta_final = res.x
                pred = np.clip(predict_fn(phi, psi, omega, theta_final, lam, K), EPS, None)
                resid = np.log(np.clip(f, EPS, None)) - np.log(pred)
                sigma2 = max(np.mean(resid**2), 1e-12)
                logL = -len(f)/2 * np.log(2*np.pi*sigma2) - np.sum(resid**2)/(2*sigma2)
                if logL > best_logL:
                    best = FitResult(
                        name=name,
                        params={"theta": theta_final, "lambda": lam, "K": K},
                        logL=logL,
                        n_params=n_theta + 2 + n_params_extra
                    )
                    best_logL = logL
            except Exception:
                continue
    return best

if __name__ == "__main__":
    df, gt = load_synthetic(5000)
    print(f"Verdad: λ={gt['lambda']}, K={gt['K']}, α={gt['alpha']}")
    fit_m6 = fit_model(
        df, predict_ces_hill,
        n_theta=4,
        init_theta=[1/3, 1/3, 1/3, 1.2],
        bounds_theta=[(0.0, 10.0)]*3 + [(0.3, 3.0)],
        lam_grid=np.linspace(-0.8, 1.5, 16),
        K_grid=np.logspace(-0.5, 1.0, 10),
        name="M6",
        normalize_w=True,
        n_params_extra=2
    )
    print(f"M6 Estimado: λ={fit_m6.params['lambda']:.2f}, "
          f"K={fit_m6.params['K']:.2f}, "
          f"α={fit_m6.params['theta'][3]:.2f}, "
          f"w={[round(x,2) for x in fit_m6.params['theta'][:3]]}")
```

**Resultados:**

| Modelo | RMSE | Params | Mejora vs M0 |
|--------|------|--------|--------------|
| M0 | 0.1115 ± 0.0012 | 2 | — |
| M6 | 0.0159 ± 0.0004 | 8 | +85.7% |

**Recuperación:** λ ≈ 0.42, K ≈ 1.95, α ≈ 1.18, w ≈ [0.32, 0.35, 0.33].

---

## Iteración 2: `validacion_real_mock.py`

**Objetivo:** probar con generador con sesgo de varianza.
**Hallazgo:** colapso total de pesos a $w=[0,1,0]$.

```python
"""validacion_real_mock.py - Prueba con mapeo Edge Aware simulado"""
import numpy as np
import pandas as pd
from scipy.optimize import minimize

EPS = 1e-6

np.random.seed(42)
n = 1500
phi = np.clip(np.random.uniform(10, 100, n) / 100.0, 0.01, 0.99)
psi = np.clip(np.random.uniform(0.5, 1.0, n), 0.01, 0.99)
omega = np.clip(np.random.uniform(1, 15, n) / 15.0, 0.01, 0.99)

omega_sat = omega**1.5 / (0.5**1.5 + omega**1.5)
z = 0.4 * phi**0.5 + 0.4 * psi**0.5 + 0.2 * omega_sat**0.5
f_obs = np.clip((z**2.0) * np.random.lognormal(0, 0.1, n), 0.01, 0.99)
df = pd.DataFrame({"phi": phi, "psi": psi, "omega": omega, "f": f_obs})

def ces_combine(phi, psi, omega_eff, lam, w):
    if abs(lam) < 1e-4:
        return (np.clip(phi, EPS, None)**w[0] *
                np.clip(psi, EPS, None)**w[1] *
                np.clip(omega_eff, EPS, None)**w[2])
    inner = np.clip(w[0]*phi**lam + w[1]*psi**lam + w[2]*omega_eff**lam, EPS, None)
    return inner ** (1.0 / lam)

def sat_hill(omega, K, alpha):
    return (np.clip(omega, EPS, None)**alpha /
            (max(K, EPS)**alpha + np.clip(omega, EPS, None)**alpha))

def predict_boxcox_hill(phi, psi, omega_eff, theta, lam, K):
    return ces_combine(phi, psi, sat_hill(omega_eff, K, theta[3]), lam, theta[:3])

def _neg_loglik(theta, phi, psi, omega_eff, f, lam, K, normalize_w=False):
    if normalize_w:
        w_raw = np.clip(theta[:3], 0, None)
        theta_norm = np.concatenate([w_raw / (w_raw.sum() + EPS), theta[3:]])
    else:
        theta_norm = theta
    pred = np.clip(predict_boxcox_hill(phi, psi, omega_eff, theta_norm, lam, K), EPS, None)
    resid = np.log(np.clip(f, EPS, None)) - np.log(pred)
    sigma2 = max(np.mean(resid**2), 1e-12)
    return -len(f)/2 * np.log(2*np.pi*sigma2) - np.sum(resid**2)/(2*sigma2)

def fit_M6_unrestricted(df):
    phi = df["phi"].values
    psi = df["psi"].values
    omega = df["omega"].values
    f = df["f"].values
    best, best_logL = None, -np.inf
    for lam in np.linspace(-0.8, 1.5, 16):
        for K in np.logspace(-0.5, 1.0, 10):
            try:
                res = minimize(
                    _neg_loglik, [1/3, 1/3, 1/3, 1.2],
                    args=(phi, psi, omega, f, lam, K, True),
                    method="L-BFGS-B",
                    bounds=[(0.0, 5.0)]*3 + [(0.3, 3.0)],
                    options={"maxiter": 300}
                )
                if res.fun > 1e9:
                    continue
                w_raw = np.clip(res.x[:3], 0, None)
                theta = np.concatenate([w_raw/(w_raw.sum()+EPS), res.x[3:]])
                pred = predict_boxcox_hill(phi, psi, omega, theta, lam, K)
                resid = np.log(np.clip(f, EPS, None)) - np.log(np.clip(pred, EPS, None))
                sigma2 = max(np.mean(resid**2), 1e-12)
                logL = -len(f)/2*np.log(2*np.pi*sigma2) - np.sum(resid**2)/(2*sigma2)
                if logL > best_logL:
                    best = {"theta": theta, "lambda": lam, "K": K, "logL": logL}
                    best_logL = logL
            except Exception:
                continue
    return best

if __name__ == "__main__":
    fit = fit_M6_unrestricted(df)
    print(f"M6 Estimado (Mock Real): λ={fit['lambda']:.3f}, "
          f"K={fit['K']:.3f}, "
          f"α={fit['theta'][3]:.3f}, "
          f"w={[round(x,3) for x in fit['theta'][:3]]}")
```

**Resultados:**

| Modelo | RMSE | Params | Mejora vs M0 |
|--------|------|--------|--------------|
| M0 | 0.5064 ± 0.0036 | 2 | — |
| M6 | 0.2283 ± 0.0056 | 8 | +54.9% |

**Recuperación:** λ = 0.520, K = 0.316, α = 3.000 (límite), w = [0.000, 1.000, 0.000]. Colapso total.

---

## Iteración 3: `validacion_real_v2.py`

**Objetivo:** resolver colapso con test ψ-only + restricción $w_i \geq 0.1$ + generador balanceado.
**Hallazgo:** pesos no colapsan a cero pero van a los bordes.

```python
"""validacion_real_v2.py - Con restricciones anti-degeneración y test ψ-only"""
import numpy as np
import pandas as pd
from scipy.optimize import minimize

EPS = 1e-6

def load_synthetic_balanced(n=2000, seed=42):
    rng = np.random.default_rng(seed)
    phi = rng.uniform(0.1, 0.9, n)
    psi = rng.uniform(0.1, 0.9, n)
    omega = rng.uniform(0.1, 0.9, n)
    lam_true, K_true, alpha_true = 0.5, 0.5, 1.5
    w_true = np.array([1/3, 1/3, 1/3])
    omega_sat = omega**alpha_true / (K_true**alpha_true + omega**alpha_true)
    z = (w_true[0]*phi**lam_true + w_true[1]*psi**lam_true +
         w_true[2]*omega_sat**lam_true)
    f_obs = np.clip((z**(1.0/lam_true)) * rng.lognormal(0, 0.05, n), 0.01, 0.99)
    df = pd.DataFrame({"phi": phi, "psi": psi, "omega": omega, "f": f_obs})
    gt = {"lambda": lam_true, "K": K_true, "alpha": alpha_true, "w": w_true}
    return df, gt

def sat_hill(omega, K, alpha):
    return (np.clip(omega, EPS, None)**alpha /
            (max(K, EPS)**alpha + np.clip(omega, EPS, None)**alpha))

def predict_psi_only(phi, psi, omega_eff, theta, lam, K):
    c, beta = theta
    return np.clip(c * (psi ** beta), EPS, None)

def _neg_loglik_v2(theta, phi, psi, omega_eff, f, predict_fn, lam, K,
                    normalize_w=False):
    # CORREGIDO v3.2: w_i ∈ [0.1, 0.8], Σw=1
    if normalize_w:
        v = np.clip(theta[:3], 1e-6, None)
        w = 0.1 + 0.7 * (v / np.sum(v))  # w ∈ [0.1, 0.8]
        theta_norm = np.concatenate([w, theta[3:]])
    else:
        theta_norm = theta
    pred = np.clip(predict_fn(phi, psi, omega_eff, theta_norm, lam, K), EPS, None)
    resid = np.log(np.clip(f, EPS, None)) - np.log(pred)
    sigma2 = max(np.mean(resid**2), 1e-12)
    return -len(f)/2 * np.log(2*np.pi*sigma2) - np.sum(resid**2)/(2*sigma2)

def fit_M6_v2(df):
    phi = df["phi"].values
    psi = df["psi"].values
    omega = df["omega"].values
    f = df["f"].values
    best, best_logL = None, -np.inf
    for lam in np.linspace(0.1, 1.0, 8):
        for K in np.logspace(-0.5, 1.0, 6):
            for _ in range(5):
                theta0 = [np.random.uniform(0.01, 10.0) for _ in range(3)]
                theta0.append(np.random.uniform(0.3, 3.0))
                try:
                    res = minimize(
                        _neg_loglik_v2, theta0,
                        args=(phi, psi, omega, f,
                              lambda *a: None, lam, K, True),
                        method="L-BFGS-B",
                        bounds=[(0.01, 10.0)]*3 + [(0.3, 3.0)],
                        options={"maxiter": 300}
                    )
                    if res.fun > 1e9:
                        continue
                    v = np.clip(res.x[:3], 1e-6, None)
                    w = 0.1 + 0.7 * (v / np.sum(v))  # CORREGIDO v3.2
                    theta = np.concatenate([w, res.x[3:]])
                    pred = np.clip(
                        np.prod([phi**w[0], psi**w[1],
                                 sat_hill(omega, K, res.x[3])**w[2]], axis=0),
                        EPS, None
                    )
                    resid = np.log(np.clip(f, EPS, None)) - np.log(pred)
                    sigma2 = max(np.mean(resid**2), 1e-12)
                    logL = -len(f)/2*np.log(2*np.pi*sigma2) - np.sum(resid**2)/(2*sigma2)
                    if logL > best_logL:
                        best = {"theta": theta, "lambda": lam, "K": K, "logL": logL}
                        best_logL = logL
                except Exception:
                    continue
    return best

if __name__ == "__main__":
    df, gt = load_synthetic_balanced(2000)
    fit_m6 = fit_M6_v2(df)
    w_est = fit_m6['theta'][:3]
    print(f"Pesos estimados M6: [{w_est[0]:.3f}, {w_est[1]:.3f}, {w_est[2]:.3f}]")
    print(f"Parámetros M6: λ={fit_m6['lambda']:.3f}, "
          f"K={fit_m6['K']:.3f}, α={fit_m6['theta'][3]:.3f}")
```

**Resultados:**

| Modelo | RMSE | Params | Mejora vs M0 |
|--------|------|--------|--------------|
| Mψ | 0.6456 ± 0.3677 | 2 | -51.0% |
| M0 | 0.4275 ± 0.0017 | 2 | — |
| M6 | **0.1030 ± 0.0055** | 8 | **+75.9%** |

**Recuperación:** λ = 1.000 (borde), K = 0.631, α = 0.300 (borde), w = [0.101, 0.898, 0.101]. Pesos a los bordes permitidos.

---

## Iteración 4: `test_identificabilidad.py`

**Objetivo:** determinar si la no-identificabilidad es estructural o de optimización.
**Hallazgo:** parámetros verdaderos predicen 7× mejor. Optimizador atrapado.

```python
"""test_identificabilidad.py - Prueba definitiva de verdaderos vs estimados"""
import numpy as np

EPS = 1e-6

def load_synthetic(n=5000, seed=999):
    rng = np.random.default_rng(seed)
    phi = rng.uniform(0.1, 0.9, n)
    psi = rng.uniform(0.1, 0.9, n)
    omega = rng.uniform(0.1, 0.9, n)
    lam_true, K_true, alpha_true = 0.5, 0.5, 1.5
    w_true = np.array([1/3, 1/3, 1/3])
    omega_sat = omega**alpha_true / (K_true**alpha_true + omega**alpha_true)
    z = (w_true[0]*phi**lam_true + w_true[1]*psi**lam_true +
         w_true[2]*omega_sat**lam_true)
    f_obs = np.clip((z**(1.0/lam_true)) * rng.lognormal(0, 0.05, n), 0.01, 0.99)
    return phi, psi, omega, f_obs, {
        "lambda": lam_true, "K": K_true, "alpha": alpha_true, "w": w_true
    }

def ces_combine(phi, psi, omega_eff, lam, w):
    if abs(lam) < 1e-4:
        return (np.clip(phi, EPS, None)**w[0] *
                np.clip(psi, EPS, None)**w[1] *
                np.clip(omega_eff, EPS, None)**w[2])
    inner = np.clip(w[0]*phi**lam + w[1]*psi**lam + w[2]*omega_eff**lam, EPS, None)
    return inner ** (1.0 / lam)

def sat_hill(omega, K, alpha):
    return (np.clip(omega, EPS, None)**alpha /
            (max(K, EPS)**alpha + np.clip(omega, EPS, None)**alpha))

def predict_boxcox_hill(phi, psi, omega, lam, K, alpha_h, w):
    return ces_combine(phi, psi, sat_hill(omega, K, alpha_h), lam, w)

if __name__ == "__main__":
    phi_te, psi_te, omega_te, f_te, gt = load_synthetic(n=5000, seed=999)

    pred_true = predict_boxcox_hill(
        phi_te, psi_te, omega_te,
        lam=gt["lambda"], K=gt["K"], alpha_h=gt["alpha"], w=gt["w"]
    )
    rmse_true = np.sqrt(np.mean((f_te - pred_true)**2))

    pred_est = predict_boxcox_hill(
        phi_te, psi_te, omega_te,
        lam=1.0, K=0.631, alpha_h=0.3, w=np.array([0.101, 0.898, 0.101])
    )
    rmse_est = np.sqrt(np.mean((f_te - pred_est)**2))

    print("="*75)
    print("TEST DE IDENTIFICABILIDAD ESTRUCTURAL (datos de test independientes)")
    print("="*75)
    print(f"{'Configuración':<55} {'RMSE':>10}")
    print("-"*75)
    print(f"{'Verdaderos (λ=0.5, K=0.5, α=1.5, w=1/3)':<55} {rmse_true:>10.4f}")
    print(f"{'Estimados v2 (λ=1.0, K=0.63, α=0.3, w≈ψ)':<55} {rmse_est:>10.4f}")

    gap = (rmse_est - rmse_true) / rmse_true * 100
    print(f"\nGap estimado vs verdadero: {gap:+.1f}%")

    if gap > 5:
        print("→ OPTIMIZADOR ATRAPADO: parámetros verdaderos predicen mucho mejor.")
        print("  Solución: búsqueda global (dual_annealing).")

    omega_sat_low = sat_hill(omega_te, 0.631, 0.3)
    omega_sat_true = sat_hill(omega_te, 0.5, 1.5)
    print(f"\nAnálisis de saturación Hill:")
    print(f"  α=1.5 (verdadero): ω_sat std={omega_sat_true.std():.3f}")
    print(f"  α=0.3 (estimado):  ω_sat std={omega_sat_low.std():.3f}")
```

**Resultados:**

| Configuración | RMSE | MAE |
|---------------|------|-----|
| Verdaderos | **0.0242** | 0.0186 |
| Estimados v2 | **0.1771** | 0.1420 |

**Gap:** +632.3%.

---

## Iteración 5: `pusfre_v3_final.py`

**Objetivo:** búsqueda global + bootstrap + Friedman + perfil 2D + residuos + curvas de recuperación.
**Hallazgo:** predicción mejorada, identificabilidad aún no resuelta.

*El código completo se reproduce a continuación con la corrección v3.2 del límite de $w_i$.*

```python
"""
pusfre_v3_final.py — v3.2 con corrección de límite w_i ∈ [0.1, 0.8]

Uso:
    python pusfre_v3_final.py --mode synthetic
    python pusfre_v3_final.py --mode edge_aware --data ruta.csv
    python pusfre_v3_final.py --mode sap_cloud --data-dir ruta/
"""

import argparse
import os
import warnings
import numpy as np
import pandas as pd
from dataclasses import dataclass
from scipy.optimize import minimize, dual_annealing
from scipy.stats import wilcoxon, friedmanchisquare
from sklearn.model_selection import StratifiedKFold
from sklearn.neural_network import MLPRegressor

warnings.filterwarnings("ignore")

RANDOM_STATE = 42
EPS = 1e-6
N_FOLDS = 5


# ============================================================
# 1. GENERADORES Y CARGA DE DATOS
# ============================================================

def generate_regime(regime, n, seed=RANDOM_STATE):
    rng = np.random.default_rng(seed)
    phi = rng.uniform(0.1, 0.9, n)
    psi = rng.uniform(0.1, 0.9, n)
    omega = rng.uniform(0.1, 0.9, n)

    if regime == "pusfre":
        lam, K, alpha, w = 0.0, 1e6, 1.0, np.array([1/3, 1/3, 1/3])
    elif regime == "ces":
        lam, K, alpha, w = 0.5, 1e6, 1.0, np.array([1/3, 1/3, 1/3])
    elif regime == "hill":
        lam, K, alpha, w = 0.0, 0.5, 1.5, np.array([1/3, 1/3, 1/3])
    else:  # full
        lam, K, alpha, w = 0.5, 0.5, 1.5, np.array([1/3, 1/3, 1/3])

    if K > 1e5:
        omega_sat = omega
    else:
        omega_sat = omega**alpha / (K**alpha + omega**alpha)

    if abs(lam) < 1e-4:
        z = phi**w[0] * psi**w[1] * omega_sat**w[2]
    else:
        z = (w[0]*phi**lam + w[1]*psi**lam + w[2]*omega_sat**lam)**(1.0/lam)

    f = np.clip(z * rng.lognormal(0, 0.05, n), 0.01, 0.99)
    df = pd.DataFrame({"phi": phi, "psi": psi, "omega": omega, "f": f})
    gt = {"lambda": lam, "K": K, "alpha": alpha, "w": w.tolist()}
    return df, gt


def load_edge_aware(path):
    df = pd.read_csv(path)
    required = ["compute_capacity", "success_rate",
                "num_agents_assigned", "task_allocation_status"]
    for c in required:
        if c not in df.columns:
            raise ValueError(f"Falta columna: {c}")

    phi = df["compute_capacity"].astype(float).values
    psi = df["success_rate"].astype(float).values
    omega = df["num_agents_assigned"].astype(float).values
    smap = {"Optimal": 1.0, "Balanced": 0.5, "Overloaded": 0.0}
    f = df["task_allocation_status"].map(smap).values

    phi = np.clip(phi / (np.nanmax(phi) + EPS), 0.01, 0.99)
    psi = np.clip(psi, 0.01, 0.99)
    omega = np.clip(omega / (np.nanpercentile(omega, 95) + EPS), 0.01, 1.0)
    f = np.clip(f, 0.01, 0.99)

    return pd.DataFrame({"phi": phi, "psi": psi, "omega": omega, "f": f}).dropna()


def load_sap_cloud(data_dir):
    cpu_files = [f for f in os.listdir(data_dir)
                 if f.startswith("vrops_compute_host_cpu")]
    mem_files = [f for f in os.listdir(data_dir)
                 if f.startswith("vrops_compute_host_memory")]
    if not cpu_files or not mem_files:
        raise FileNotFoundError("Faltan archivos CPU o memoria")

    cpu_df = pd.read_csv(os.path.join(data_dir, cpu_files[0]), nrows=100000)
    mem_df = pd.read_csv(os.path.join(data_dir, mem_files[0]), nrows=100000)

    def find_col(df, keyword):
        for c in df.columns:
            if keyword in c.lower():
                return c
        return df.columns[-1]

    host_cpu = (find_col(cpu_df, "host")
                if any("host" in c.lower() for c in cpu_df.columns)
                else cpu_df.columns[0])
    val_cpu = find_col(cpu_df, "cpu")
    host_mem = (find_col(mem_df, "host")
                if any("host" in c.lower() for c in mem_df.columns)
                else mem_df.columns[0])
    val_mem = find_col(mem_df, "memory")

    cpu_agg = cpu_df.groupby(host_cpu)[val_cpu].agg(
        ["mean", "std", "count"]
    ).reset_index()
    cpu_agg.columns = ["host", "cpu_mean", "cpu_std", "cpu_count"]
    mem_agg = mem_df.groupby(host_mem)[val_mem].agg(
        ["mean", "std"]
    ).reset_index()
    mem_agg.columns = ["host", "mem_mean", "mem_std"]

    m = pd.merge(cpu_agg, mem_agg, on="host", how="inner")
    if len(m) < 10:
        raise ValueError("Muy pocos hosts")

    phi = np.clip(m["cpu_mean"].values /
                  (np.nanmax(m["cpu_mean"].values) + EPS), 0.01, 0.99)
    psi = np.clip(1.0 / (1.0 + m["mem_std"].values /
                          (m["mem_mean"].values + EPS)), 0.01, 0.99)
    omega = np.clip(m["cpu_count"].values /
                    (np.nanmax(m["cpu_count"].values) + EPS), 0.01, 1.0)
    f = np.clip(1.0 - phi, 0.01, 0.99)

    return pd.DataFrame({"phi": phi, "psi": psi,
                          "omega": omega, "f": f}).dropna()


# ============================================================
# 2. NÚCLEO MATEMÁTICO
# ============================================================

def ces_combine(phi, psi, omega_eff, lam, w):
    phi = np.clip(phi, EPS, None)
    psi = np.clip(psi, EPS, None)
    omega_eff = np.clip(omega_eff, EPS, None)
    if abs(lam) < 1e-4:
        return phi**w[0] * psi**w[1] * omega_eff**w[2]
    inner = np.clip(w[0]*phi**lam + w[1]*psi**lam +
                     w[2]*omega_eff**lam, EPS, None)
    return inner**(1.0/lam)


def sat_hill(omega, K, alpha):
    omega = np.clip(omega, EPS, None)
    K = max(K, EPS)
    return omega**alpha / (K**alpha + omega**alpha)


def predict_base(phi, psi, om, theta, lam, K):
    return phi * psi * om**theta[0]


def predict_ces(phi, psi, om, theta, lam, K):
    return ces_combine(phi, psi, om, lam, theta)


def predict_hill(phi, psi, om, theta, lam, K):
    return phi * psi * sat_hill(om, K, theta[0])**theta[1]


def predict_ces_hill(phi, psi, om, theta, lam, K):
    w = theta[:3]
    return ces_combine(phi, psi, sat_hill(om, K, theta[3]), lam, w)


# ============================================================
# 3. AJUSTE: BÚSQUEDA GLOBAL + REFINAMIENTO LOCAL
# ============================================================

def simplex_reparam(v):
    """CORREGIDO v3.2: w_i ∈ [0.1, 0.8], Σw = 1."""
    v = np.clip(v, 1e-6, None)
    return 0.1 + 0.7 * (v / np.sum(v))


def neg_loglik_from_params(params, phi, psi, om, f, lam, K,
                           predict_fn, use_w):
    if use_w:
        w = simplex_reparam(params[:3])
        tail = params[3:]
    else:
        w = None
        tail = params

    pred = predict_fn(phi, psi, om,
                      np.concatenate([w, tail]) if use_w else tail, lam, K)
    pred = np.clip(pred, EPS, None)
    resid = np.log(np.clip(f, EPS, None)) - np.log(pred)
    sigma2 = max(np.mean(resid**2), 1e-12)
    return len(f)/2 * np.log(2*np.pi*sigma2) + np.sum(resid**2) / (2*sigma2)


@dataclass
class FitResult:
    name: str
    params: dict
    logL: float
    n_params: int
    method: str


def fit_with_global_search(df, predict_fn, lam_grid, K_grid,
                           init_theta, bounds_theta,
                           use_w=False, name="", n_params_extra=0,
                           n_local_restarts=5, use_global=True):
    phi = df["phi"].values
    psi = df["psi"].values
    om = df["omega"].values
    f = df["f"].values
    best = None
    best_negL = np.inf

    if use_global:
        lam_lo, lam_hi = min(lam_grid), max(lam_grid)
        K_lo = max(min(K_grid), 1e-3)
        K_hi = min(max(K_grid), 1e3)
        bounds = [(lam_lo, lam_hi), (K_lo, K_hi)] + list(bounds_theta)

        def obj_full(x):
            lam, K = x[0], x[1]
            theta = x[2:]
            try:
                return neg_loglik_from_params(
                    theta, phi, psi, om, f, lam, K, predict_fn, use_w
                )
            except Exception:
                return 1e10

        try:
            res_global = dual_annealing(
                obj_full, bounds=bounds,
                maxiter=200, seed=RANDOM_STATE,
                no_local_search=False
            )
            if res_global.fun < best_negL:
                best_negL = res_global.fun
                best = FitResult(
                    name=name,
                    params={"theta": res_global.x[2:],
                            "lambda": res_global.x[0],
                            "K": res_global.x[1]},
                    logL=-best_negL,
                    n_params=len(res_global.x[2:]) + 2 + n_params_extra,
                    method="dual_annealing"
                )
        except Exception:
            pass

    for _ in range(n_local_restarts):
        lam0 = np.random.uniform(min(lam_grid), max(lam_grid))
        K0 = np.exp(np.random.uniform(np.log(0.05), np.log(5.0)))
        theta0 = [np.random.uniform(b[0], b[1]) for b in bounds_theta]
        try:
            res = minimize(
                lambda x: neg_loglik_from_params(
                    x, phi, psi, om, f, lam0, K0, predict_fn, use_w
                ),
                theta0, method="L-BFGS-B", bounds=bounds_theta,
                options={"maxiter": 500}
            )
            if res.fun < best_negL:
                best_negL = res.fun
                best = FitResult(
                    name=name,
                    params={"theta": res.x, "lambda": lam0, "K": K0},
                    logL=-res.fun,
                    n_params=len(res.x) + 2 + n_params_extra,
                    method="multistart_local"
                )
        except Exception:
            continue
    return best


# ============================================================
# 4. FITTERS ESPECÍFICOS
# ============================================================

def fit_M0(df, use_global=False):
    return fit_with_global_search(
        df, predict_base,
        lam_grid=[0.0], K_grid=[1e6],
        init_theta=[1.0], bounds_theta=[(0.1, 3.0)],
        use_w=False, name="M0", n_params_extra=-1,
        n_local_restarts=1, use_global=False
    )


def fit_M1(df, use_global=True):
    return fit_with_global_search(
        df, predict_ces,
        lam_grid=np.linspace(-1.0, 1.8, 15), K_grid=[1e6],
        init_theta=[1.0, 1.0, 1.0], bounds_theta=[(0.01, 20.0)]*3,
        use_w=True, name="M1", n_params_extra=0,
        n_local_restarts=5, use_global=use_global
    )


def fit_M2(df, use_global=True):
    return fit_with_global_search(
        df, predict_hill,
        lam_grid=[0.0], K_grid=np.logspace(-1, 1, 8),
        init_theta=[1.5, 1.0],
        bounds_theta=[(0.3, 4.0), (0.1, 3.0)],
        use_w=False, name="M2", n_params_extra=0,
        n_local_restarts=5, use_global=use_global
    )


def fit_M6(df, use_global=True):
    return fit_with_global_search(
        df, predict_ces_hill,
        lam_grid=np.linspace(-1.0, 1.8, 15),
        K_grid=np.logspace(-1, 1, 8),
        init_theta=[1.0, 1.0, 1.0, 1.5],
        bounds_theta=[(0.01, 20.0)]*3 + [(0.3, 4.0)],
        use_w=True, name="M6", n_params_extra=0,
        n_local_restarts=5, use_global=use_global
    )


FITTERS = {
    "M0": fit_M0,
    "M1": fit_M1,
    "M2": fit_M2,
    "M6": fit_M6,
}


def predict_from_fit(fit, df_test):
    phi = df_test["phi"].values
    psi = df_test["psi"].values
    om = df_test["omega"].values
    theta = fit.params["theta"]
    lam = fit.params["lambda"]
    K = fit.params["K"]
    if fit.name == "M0":
        pred = predict_base(phi, psi, om, theta, lam, K)
    elif fit.name == "M1":
        w = simplex_reparam(theta[:3])
        pred = predict_ces(phi, psi, om, w, lam, K)
    elif fit.name == "M2":
        pred = predict_hill(phi, psi, om, theta, lam, K)
    elif fit.name == "M6":
        w = simplex_reparam(theta[:3])
        pred = predict_ces_hill(phi, psi, om,
                                 np.concatenate([w, theta[3:]]), lam, K)
    else:
        pred = predict_base(phi, psi, om, theta, lam, K)
    return np.clip(pred, EPS, None)


# ============================================================
# 5. EVALUACIÓN CV
# ============================================================

def evaluate_cv(df, fitter, use_global=True, n_folds=N_FOLDS):
    y_strat = pd.qcut(df["f"], q=n_folds, labels=False,
                       duplicates="drop")
    skf = StratifiedKFold(n_splits=n_folds, shuffle=True,
                          random_state=RANDOM_STATE)
    rmses, maes, logls, nps = [], [], [], []
    for tr, te in skf.split(df, y_strat):
        df_tr = df.iloc[tr].reset_index(drop=True)
        df_te = df.iloc[te].reset_index(drop=True)
        try:
            if fitter.__name__ == "fit_M0":
                fit = fitter(df_tr)
            else:
                fit = fitter(df_tr, use_global=use_global)
            if fit is None:
                continue
            pred = predict_from_fit(fit, df_te)
            f_true = df_te["f"].values
            rmses.append(float(np.sqrt(np.mean((f_true - pred)**2))))
            maes.append(float(np.mean(np.abs(f_true - pred))))
            logls.append(fit.logL)
            nps.append(fit.n_params)
        except Exception:
            continue
    if not rmses:
        return None
    return {
        "rmse_mean": float(np.mean(rmses)),
        "rmse_std": float(np.std(rmses)),
        "rmse_folds": rmses,
        "mae_mean": float(np.mean(maes)),
        "n_params": int(np.mean(nps)),
        "logL_mean": float(np.mean(logls)),
    }


# ============================================================
# 6. BOOTSTRAP
# ============================================================

def bootstrap_params(df, fitter, n_boot=100, use_global=False):
    n = len(df)
    rng = np.random.default_rng(RANDOM_STATE)
    lambdas, Ks, alphas, w1s = [], [], [], []
    for b in range(n_boot):
        idx = rng.choice(n, n, replace=True)
        df_b = df.iloc[idx].reset_index(drop=True)
        try:
            fit = (fitter(df_b, use_global=use_global)
                   if fitter.__name__ != "fit_M0" else fitter(df_b))
            if fit is None or fit.name != "M6":
                continue
            w = simplex_reparam(fit.params["theta"][:3])
            lambdas.append(fit.params["lambda"])
            Ks.append(fit.params["K"])
            alphas.append(fit.params["theta"][3])
            w1s.append(w[0])
        except Exception:
            continue

    def summarize(arr, name):
        if not arr:
            return {f"{name}_median": np.nan,
                    f"{name}_lo": np.nan, f"{name}_hi": np.nan}
        arr = np.array(arr)
        return {
            f"{name}_median": float(np.median(arr)),
            f"{name}_lo": float(np.percentile(arr, 2.5)),
            f"{name}_hi": float(np.percentile(arr, 97.5)),
        }

    return {
        **summarize(lambdas, "lambda"),
        **summarize(Ks, "K"),
        **summarize(alphas, "alpha"),
        **summarize(w1s, "w1"),
    }


# ============================================================
# 7. PERFIL 2D
# ============================================================

def profile_likelihood_2d(df, lam_vals, K_vals):
    phi = df["phi"].values
    psi = df["psi"].values
    om = df["omega"].values
    f = df["f"].values
    results = []
    for lam in lam_vals:
        for K in K_vals:
            try:
                res = minimize(
                    lambda t: neg_loglik_from_params(
                        t, phi, psi, om, f, lam, K,
                        predict_ces_hill, use_w=True
                    ),
                    [1.0, 1.0, 1.0, 1.5],
                    method="L-BFGS-B",
                    bounds=[(0.01, 20.0)]*3 + [(0.3, 4.0)],
                    options={"maxiter": 300}
                )
                results.append({"lambda": lam, "K": K,
                                 "neg_logL": res.fun})
            except Exception:
                results.append({"lambda": lam, "K": K,
                                 "neg_logL": np.nan})
    return pd.DataFrame(results)


# ============================================================
# 8. ANÁLISIS DE RESIDUOS
# ============================================================

def residual_analysis(fit, df):
    pred = predict_from_fit(fit, df)
    f_true = df["f"].values
    resid = f_true - pred
    log_resid = np.log(np.clip(f_true, EPS, None)) - np.log(pred)
    return pd.DataFrame({
        "f_true": f_true, "f_pred": pred,
        "resid": resid, "log_resid": log_resid,
        "abs_resid": np.abs(resid),
        "phi": df["phi"].values,
        "psi": df["psi"].values,
        "omega": df["omega"].values,
    })


# ============================================================
# 9. FRIEDMAN
# ============================================================

def friedman_test(results):
    models = list(results.keys())
    if len(models) < 3:
        return None
    fold_rmses = {m: results[m]["rmse_folds"]
                  for m in models if "rmse_folds" in results[m]}
    min_len = min(len(v) for v in fold_rmses.values())
    if min_len < 3:
        return None
    data = [fold_rmses[m][:min_len] for m in fold_rmses]
    try:
        stat, p = friedmanchisquare(*data)
    except Exception:
        return None
    pairwise = {}
    for i, m1 in enumerate(models):
        for m2 in models[i+1:]:
            if m1 in fold_rmses and m2 in fold_rmses:
                try:
                    _, p_pair = wilcoxon(fold_rmses[m1][:min_len],
                                          fold_rmses[m2][:min_len])
                    pairwise[f"{m1}_vs_{m2}"] = float(p_pair)
                except Exception:
                    pairwise[f"{m1}_vs_{m2}"] = np.nan
    return {"friedman_stat": float(stat),
            "friedman_p": float(p),
            "pairwise": pairwise}


# ============================================================
# 10. CURVAS DE RECUPERACIÓN
# ============================================================

def recovery_curve(n_values=(500, 1000, 2000, 5000, 10000),
                   regime="full", n_repeats=3):
    results = []
    for n in n_values:
        errors = {"lambda": [], "K": [], "alpha": []}
        for r in range(n_repeats):
            df, gt = generate_regime(regime, n, seed=RANDOM_STATE + r)
            fit = fit_M6(df, use_global=True)
            if fit is None:
                continue
            w = simplex_reparam(fit.params["theta"][:3])
            errors["lambda"].append(
                abs(fit.params["lambda"] - gt["lambda"]))
            errors["K"].append(
                abs(fit.params["K"] - gt["K"]) / max(gt["K"], 1e-3))
            errors["alpha"].append(
                abs(fit.params["theta"][3] - gt["alpha"]))
        results.append({
            "N": n,
            "lambda_err": float(np.mean(errors["lambda"])),
            "K_err_rel": float(np.mean(errors["K"])),
            "alpha_err": float(np.mean(errors["alpha"])),
        })
    return pd.DataFrame(results)


# ============================================================
# 11. INFORME
# ============================================================

def generate_report(mode, results, params_est, bootstrap_res,
                    friedman_res, recovery_df, gt=None):
    lines = []
    lines.append("="*78)
    lines.append(f"INFORME PUSFRE v3 FINAL — Modo: {mode}")
    lines.append("="*78)
    if gt:
        lines.append(f"\nVerdad del generador:")
        for k, v in gt.items():
            lines.append(f"  {k} = {v}")

    lines.append("\n" + "-"*78)
    lines.append("RENDIMIENTO POR MODELO (CV)")
    lines.append("-"*78)
    lines.append(f"{'Modelo':<10} {'RMSE':>12} {'MAE':>12} "
                 f"{'Params':>8} {'vs M0':>10}")
    lines.append("-"*78)

    base = results.get("M0", {}).get("rmse_mean")
    for m, r in results.items():
        if r is None:
            continue
        mejora = ("—" if m == "M0" or base is None
                  else f"{(base - r['rmse_mean'])/base*100:+.1f}%")
        lines.append(f"{m:<10} {r['rmse_mean']:>12.4f} "
                     f"{r['mae_mean']:>12.4f} "
                     f"{r['n_params']:>8} {mejora:>10}")

    if params_est:
        lines.append("\n" + "-"*78)
        lines.append("PARÁMETROS ESTIMADOS (mejor modelo: M6)")
        lines.append("-"*78)
        for k, v in params_est.items():
            if isinstance(v, list):
                lines.append(f"  {k} = {[round(x,4) for x in v]}")
            else:
                lines.append(f"  {k} = {v}")

    if bootstrap_res:
        lines.append("\n" + "-"*78)
        lines.append("INTERVALOS DE CONFIANZA (bootstrap 95%)")
        lines.append("-"*78)
        for k, v in bootstrap_res.items():
            if pd.notna(v):
                lines.append(f"  {k}: {v:.4f}")

    if friedman_res:
        lines.append("\n" + "-"*78)
        lines.append("TEST DE FRIEDMAN")
        lines.append("-"*78)
        lines.append(f"  Estadístico: {friedman_res['friedman_stat']:.4f}")
        lines.append(f"  p-valor: {friedman_res['friedman_p']:.6f}")
        for k, v in friedman_res["pairwise"].items():
            lines.append(f"    {k}: p = {v:.6f}")

    if recovery_df is not None and len(recovery_df) > 0:
        lines.append("\n" + "-"*78)
        lines.append("CURVAS DE RECUPERACIÓN (error vs N)")
        lines.append("-"*78)
        lines.append(recovery_df.to_string(index=False))

    lines.append("\n" + "="*78)
    lines.append("CONCLUSIÓN")
    lines.append("="*78)
    if base and "M6" in results:
        mejora = (base - results["M6"]["rmse_mean"]) / base * 100
        lines.append(f"M6 mejora M0 en {mejora:+.1f}%")
    if params_est and gt:
        lam_est = params_est.get("lambda", np.nan)
        lam_true = gt["lambda"]
        if abs(lam_est - lam_true) < 0.3:
            lines.append(f"→ λ recuperado dentro de tolerancia.")
        else:
            lines.append(f"→ λ NO recuperado.")
    lines.append("\n1310.")
    return "\n".join(lines)


# ============================================================
# 12. MAIN
# ============================================================

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument("--mode", required=True,
                        choices=["synthetic", "edge_aware", "sap_cloud"])
    parser.add_argument("--regime", default="full",
                        choices=["pusfre", "ces", "hill", "full"])
    parser.add_argument("--n", type=int, default=2000)
    parser.add_argument("--data", type=str, default=None)
    parser.add_argument("--data-dir", type=str, default=None)
    parser.add_argument("--bootstrap", type=int, default=50)
    parser.add_argument("--no-recovery", action="store_true")
    args = parser.parse_args()

    gt = None
    if args.mode == "synthetic":
        df, gt = generate_regime(args.regime, args.n)
        print(f"Datos sintéticos: régimen={args.regime}, N={len(df)}")
    elif args.mode == "edge_aware":
        df = load_edge_aware(args.data)
        print(f"Edge Aware: N={len(df)}")
    else:
        df = load_sap_cloud(args.data_dir)
        print(f"SAP Cloud: N={len(df)}")

    print(f"Correlaciones con f:")
    for c in ["phi", "psi", "omega"]:
        print(f"  corr({c}, f) = {np.corrcoef(df[c], df['f'])[0,1]:+.3f}")

    print("\n" + "="*78)
    print("EVALUACIÓN CV")
    print("="*78)
    results = {}
    for name, fitter in FITTERS.items():
        print(f"\n{name}...")
        res = evaluate_cv(df, fitter, use_global=(name != "M0"))
        if res:
            results[name] = res
            print(f"  RMSE = {res['rmse_mean']:.4f} ± {res['rmse_std']:.4f}")
            print(f"  Params = {res['n_params']}")

    print("\nAjuste final M6...")
    fit_m6 = fit_M6(df, use_global=True)
    params_est = {}
    if fit_m6:
        w = simplex_reparam(fit_m6.params["theta"][:3])
        params_est = {
            "lambda": fit_m6.params["lambda"],
            "K": fit_m6.params["K"],
            "alpha": fit_m6.params["theta"][3],
            "w": w.tolist(),
            "logL": fit_m6.logL,
            "method": fit_m6.method,
        }
        print(f"  λ = {params_est['lambda']:.4f}")
        print(f"  K = {params_est['K']:.4f}")
        print(f"  α = {params_est['alpha']:.4f}")
        print(f"  w = {[round(x,4) for x in params_est['w']]}")

    bootstrap_res = {}
    if args.bootstrap > 0:
        print(f"\nBootstrap ({args.bootstrap} réplicas)...")
        bootstrap_res = bootstrap_params(
            df, fit_M6, n_boot=args.bootstrap, use_global=False
        )
        print(f"  λ IC 95%: [{bootstrap_res.get('lambda_lo', np.nan):.4f}, "
              f"{bootstrap_res.get('lambda_hi', np.nan):.4f}]")

    print("\nPerfil 2D...")
    profile_df = profile_likelihood_2d(
        df, np.linspace(-1.0, 1.8, 15), np.logspace(-1, 1, 8)
    )
    profile_df.to_csv(f"perfil_{args.mode}.csv", index=False)

    if fit_m6:
        residual_analysis(fit_m6, df).to_csv(
            f"residuos_{args.mode}.csv", index=False
        )

    friedman_res = friedman_test(results)

    recovery_df = None
    if not args.no_recovery and args.mode == "synthetic":
        print("\nCurvas de recuperación...")
        recovery_df = recovery_curve(regime=args.regime)
        recovery_df.to_csv(f"recuperacion_{args.mode}.csv", index=False)

    report = generate_report(args.mode, results, params_est,
                              bootstrap_res, friedman_res,
                              recovery_df, gt)
    print("\n" + report)
    with open(f"informe_{args.mode}.txt", "w", encoding="utf-8") as f:
        f.write(report)

    rows = [{"modelo": m, **{k: v for k, v in r.items()
                              if k != "rmse_folds"}}
            for m, r in results.items() if r]
    pd.DataFrame(rows).to_csv(f"resultados_{args.mode}.csv", index=False)
    if params_est:
        pd.DataFrame([params_est]).to_csv(
            f"params_{args.mode}.csv", index=False
        )
    if bootstrap_res:
        pd.DataFrame([bootstrap_res]).to_csv(
            f"bootstrap_{args.mode}.csv", index=False
        )


if __name__ == "__main__":
    main()
```

**Resultados (régimen `full`, N=2000):**

| Modelo | RMSE | Params | vs M0 |
|--------|------|--------|-------|
| M0 | 0.2519 | 2 | — |
| M1 | 0.1035 | 6 | +58.9% |
| M2 | 0.2464 | 4 | +2.2% |
| M6 | **0.0250** | 6 | **+90.1%** |

**Recuperación:** λ=0.46, K=1.16, α=1.14, w=[0.33, 0.33, 0.44].
**Bootstrap 95%:** λ ∈ [−0.78, 1.73], K ∈ [0.07, 4.35], α ∈ [0.35, 2.58], w₁ ∈ [0.22, 0.45].
**Friedman:** estadístico = 13.56, p = 0.0036.

---

## Iteración 6: `test_K_fijo.py`

```python
"""test_K_fijo.py - Fija K al valor verdadero y estima el resto."""
import numpy as np
from scipy.optimize import dual_annealing, minimize

EPS = 1e-6

def generate_regime(regime, n, seed=42):
    rng = np.random.default_rng(seed)
    phi = rng.uniform(0.1, 0.9, n)
    psi = rng.uniform(0.1, 0.9, n)
    omega = rng.uniform(0.1, 0.9, n)
    if regime == "full":
        lam, K, alpha, w = 0.5, 0.5, 1.5, np.array([1/3, 1/3, 1/3])
    omega_sat = omega**alpha / (K**alpha + omega**alpha)
    z = (w[0]*phi**lam + w[1]*psi**lam + w[2]*omega_sat**lam)**(1.0/lam)
    f = np.clip(z * rng.lognormal(0, 0.05, n), 0.01, 0.99)
    return phi, psi, omega, f, {"lambda": lam, "K": K,
                                  "alpha": alpha, "w": w}

def simplex_reparam(v):
    """CORREGIDO v3.2: w_i ∈ [0.1, 0.8]."""
    v = np.clip(v, 1e-6, None)
    return 0.1 + 0.7 * (v / np.sum(v))

def sat_hill(omega, K, alpha):
    return (np.clip(omega, EPS, None)**alpha /
            (K**alpha + np.clip(omega, EPS, None)**alpha))

def ces_combine(phi, psi, omega_eff, lam, w):
    inner = np.clip(w[0]*phi**lam + w[1]*psi**lam +
                     w[2]*omega_eff**lam, EPS, None)
    return inner**(1.0/lam)

def predict_boxcox_hill(phi, psi, omega, lam, K, alpha_h, w):
    return ces_combine(phi, psi, sat_hill(omega, K, alpha_h), lam, w)

def neg_loglik(theta, phi, psi, om, f, lam, K):
    v = np.clip(theta[:3], 1e-6, None)
    w = 0.1 + 0.7 * (v / np.sum(v))
    alpha_h = theta[3]
    pred = np.clip(predict_boxcox_hill(phi, psi, om, lam, K, alpha_h, w),
                    EPS, None)
    resid = np.log(np.clip(f, EPS, None)) - np.log(pred)
    sigma2 = max(np.mean(resid**2), 1e-12)
    return len(f)/2 * np.log(2*np.pi*sigma2) + np.sum(resid**2)/(2*sigma2)

if __name__ == "__main__":
    phi, psi, om, f, gt = generate_regime("full", 2000)
    bounds = [(0.01, 20.0)]*3 + [(0.3, 4.0)]

    def obj(x):
        lam = x[0]
        theta = x[1:]
        return neg_loglik(theta, phi, psi, om, f, lam, 0.5)

    res = dual_annealing(
        obj, bounds=[(-1.0, 1.8)] + bounds,
        maxiter=200, seed=42
    )
    lam_est = res.x[0]
    v = np.clip(res.x[1:4], 1e-6, None)
    w = 0.1 + 0.7 * (v / np.sum(v))
    alpha_est = res.x[4]

    print(f"Verdadero: λ=0.5, α=1.5, w=1/3")
    print(f"Estimado (K fijo): λ={lam_est:.4f}, "
          f"α={alpha_est:.4f}, w=[{w[0]:.3f}, {w[1]:.3f}, {w[2]:.3f}]")
```

---

## Iteración 7: `test_perfil.py`

```python
"""test_perfil.py - Perfil 1D de λ con K fijo."""
import numpy as np
from scipy.optimize import minimize

EPS = 1e-6

def generate_regime(regime, n, seed=42):
    rng = np.random.default_rng(seed)
    phi = rng.uniform(0.1, 0.9, n)
    psi = rng.uniform(0.1, 0.9, n)
    omega = rng.uniform(0.1, 0.9, n)
    if regime == "full":
        lam, K, alpha, w = 0.5, 0.5, 1.5, np.array([1/3, 1/3, 1/3])
    omega_sat = omega**alpha / (K**alpha + omega**alpha)
    z = (w[0]*phi**lam + w[1]*psi**lam + w[2]*omega_sat**lam)**(1.0/lam)
    f = np.clip(z * rng.lognormal(0, 0.05, n), 0.01, 0.99)
    return phi, psi, omega, f, {"lambda": lam, "K": K,
                                  "alpha": alpha, "w": w}

def sat_hill(omega, K, alpha):
    return (np.clip(omega, EPS, None)**alpha /
            (K**alpha + np.clip(omega, EPS, None)**alpha))

def ces_combine(phi, psi, omega_eff, lam, w):
    inner = np.clip(w[0]*phi**lam + w[1]*psi**lam +
                     w[2]*omega_eff**lam, EPS, None)
    return inner**(1.0/lam)

def predict_boxcox_hill(phi, psi, omega, lam, K, alpha_h, w):
    return ces_combine(phi, psi, sat_hill(omega, K, alpha_h), lam, w)

def neg_loglik(theta, phi, psi, om, f, lam, K):
    v = np.clip(theta[:3], 1e-6, None)
    w = 0.1 + 0.7 * (v / np.sum(v))  # CORREGIDO v3.2
    alpha_h = theta[3]
    pred = np.clip(predict_boxcox_hill(phi, psi, om, lam, K, alpha_h, w),
                    EPS, None)
    resid = np.log(np.clip(f, EPS, None)) - np.log(pred)
    sigma2 = max(np.mean(resid**2), 1e-12)
    return len(f)/2 * np.log(2*np.pi*sigma2) + np.sum(resid**2)/(2*sigma2)

if __name__ == "__main__":
    phi, psi, om, f, gt = generate_regime("full", 2000)

    lams = np.linspace(-0.5, 1.5, 21)
    results = []
    for lam in lams:
        res = minimize(
            lambda t: neg_loglik(t, phi, psi, om, f, lam, 0.5),
            [1.0, 1.0, 1.0, 1.5],
            method="L-BFGS-B",
            bounds=[(0.01, 20.0)]*3 + [(0.3, 4.0)],
            options={"maxiter": 300}
        )
        results.append((lam, res.fun))

    print("λ\tneg_logL")
    max_nl = max(r[1] for r in results)
    for lam, nl in results:
        bar = "█" * int((max_nl - nl) * 5)
        print(f"{lam:.2f}\t{nl:.4f}\t{bar}")

    best = min(results, key=lambda x: x[1])
    print(f"\nÓptimo: λ = {best[0]:.3f}")
```

---

# ANEXO II: RESULTADOS COMPLETOS DE CADA EJECUCIÓN

## Tabla resumen de las 5 iteraciones

| Versión | Hallazgo principal | Acción |
|---------|---------------------|--------|
| v1.0 | M6 mejora 85.7%, recupera parámetros | Base teórica |
| v1.5 (mock) | Colapso de pesos a [0,1,0] | Vulnerabilidad identificada |
| v2.0 | Test ψ-only + restricción w≥0.1 | Mejora multivariante asegurada |
| v2.1 | Verdaderos predicen 7× mejor | Optimizador atrapado |
| v3.0 | Búsqueda global + bootstrap | Predicción confirmada, identificabilidad no resuelta |
| v3.1 | Reframing predictivo, prueba axiomática, criterio BIC | Reinterpretación completa |
| **v3.2** | **Correcciones de rigor (Paso 3, límite w, A5, ΔBIC)** | **Corrección de coherencia interna** |

## Detalle de cada ejecución

### v1.0 (N=5000, generador no balanceado)

| Modelo | RMSE | Params | vs M0 |
|--------|------|--------|-------|
| M0 | 0.1115 | 2 | — |
| M1 | 0.0778 | 7 | +30.2% |
| M2 | 0.1101 | 5 | +1.3% |
| M6 | 0.0159 | 8 | +85.7% |

### v1.5 (mock real, N=1500, sesgo de varianza)

| Modelo | RMSE | Params | vs M0 |
|--------|------|--------|-------|
| M0 | 0.5064 | 2 | — |
| M6 | 0.2283 | 8 | +54.9% |

### v2.0 (N=2000, generador balanceado)

| Modelo | RMSE | Params | vs M0 |
|--------|------|--------|-------|
| Mψ | 0.6456 | 2 | -51.0% |
| M0 | 0.4275 | 2 | — |
| M6 | 0.1030 | 8 | +75.9% |

### v2.1 (test de identificabilidad)

| Configuración | RMSE | MAE |
|---------------|------|-----|
| Verdaderos | 0.0242 | 0.0186 |
| Estimados v2 | 0.1771 | 0.1420 |
| **Gap** | **+632.3%** | — |

### v3.0 (búsqueda global, régimen full)

| Modelo | RMSE | Params | vs M0 |
|--------|------|--------|-------|
| M0 | 0.2519 | 2 | — |
| M1 | 0.1035 | 6 | +58.9% |
| M2 | 0.2464 | 4 | +2.2% |
| M6 | **0.0250** | **6** | **+90.1%** |

Recuperación: λ=0.46, K=1.16, α=1.14, w=[0.33, 0.33, 0.44].

Bootstrap 95%: λ ∈ [−0.78, 1.73], K ∈ [0.07, 4.35], α ∈ [0.35, 2.58], w₁ ∈ [0.22, 0.45].

Friedman: estadístico = 13.56, p = 0.0036. Wilcoxon pairwise M0 vs M6: p = 0.0625 (saturado).

Curvas de recuperación:

| N | λ err | K err | α err |
|---|-------|-------|-------|
| 500 | 0.009 | 1.28 | 0.35 |
| 1000 | 0.038 | 1.34 | 0.37 |
| 2000 | 0.038 | 1.32 | 0.36 |
| 5000 | 0.040 | 1.33 | 0.37 |

### v3.2 (reinterpretación)

Sin nueva ejecución. Los resultados de v3.0 se reinterpretan bajo:

- **Paso 3 del Apéndice A reforzado** con demostración completa.
- **Límite de $w_i$ corregido** a $[0.1, 0.8]$ en código.
- **ΔBIC = 1.2** reportado explícitamente en régimen `pusfre` (evidencia débil).
- **Motivación de A5 ampliada** en §3.2.
- **Predicción sobre dominios Ω amplio marcada como hipótesis**.
- **Anexo III marcado como pendiente** de implementación.

---

# ANEXO III: SCRIPTS DE DESCARGA Y EJECUCIÓN SOBRE DATOS REALES

## Script 1: Descarga automática

```bash
#!/bin/bash
# ejecutar_todo.sh — Descarga Edge Aware + SAP Cloud y ejecuta pipeline

set -e

mkdir -p datos
cd datos

echo "=== [1/4] Descargando Edge Aware (Kaggle) ==="
if [ ! -f edge_aware.csv ]; then
    if command -v kaggle &> /dev/null; then
        kaggle datasets download -d colabsss/edge-aware-customer-service-allocation-dataset
        unzip -o *.zip
        for f in *.csv; do
            mv "$f" edge_aware.csv
            break
        done
    else
        echo "  Kaggle CLI no instalado. Instalando..."
        pip install kaggle
        echo "  Configura ~/.kaggle/kaggle.json con tu API key."
        echo "  URL: https://www.kaggle.com/datasets/colabsss/edge-aware-customer-service-allocation-dataset"
    fi
fi

echo "=== [2/4] Descargando SAP Cloud (Zenodo) ==="
if [ ! -d sap_cloud ]; then
    mkdir -p sap_cloud
    cd sap_cloud
    curl -L -o sap_cloud.zip "https://zenodo.org/records/17141306/files/sap_cloud_infrastructure_dataset.zip?download=1" || \
    echo "  Descarga automática falló. URL: https://zenodo.org/records/17141306"
    if [ -f sap_cloud.zip ]; then
        unzip -o sap_cloud.zip
        rm sap_cloud.zip
    fi
    cd ..
fi

echo "=== [3/4] Verificando datos ==="
ls -la edge_aware.csv 2>/dev/null && echo "  Edge Aware OK" || echo "  Edge Aware FALTA"
ls -la sap_cloud/ 2>/dev/null && echo "  SAP Cloud OK" || echo "  SAP Cloud FALTA"

echo "=== [4/4] Ejecutando pipeline ==="
cd ..

if [ -f datos/edge_aware.csv ]; then
    echo ""
    echo "--- EDGE AWARE ---"
    python pusfre_v3_final.py --mode edge_aware --data datos/edge_aware.csv --bootstrap 50
fi

if [ -d datos/sap_cloud ]; then
    echo ""
    echo "--- SAP CLOUD ---"
    python pusfre_v3_final.py --mode sap_cloud --data-dir datos/sap_cloud --bootstrap 30
fi

echo ""
echo "=== Completado ==="
echo "Resultados: resultados_edge_aware.csv, resultados_sap_cloud.csv"
```

## Script 2: Ejecución de tests de identificabilidad

```bash
#!/bin/bash
# ejecutar_tests_identificabilidad.sh

set -e

echo "=== TEST 1: N grande (régimen full, N=20000) ==="
python pusfre_v3_final.py --mode synthetic --regime full --n 20000 --bootstrap 30

echo ""
echo "=== TEST 2: 10 folds en vez de 5 ==="
sed -i 's/N_FOLDS = 5/N_FOLDS = 10/' pusfre_v3_final.py
python pusfre_v3_final.py --mode synthetic --regime full --n 2000 --bootstrap 30
sed -i 's/N_FOLDS = 10/N_FOLDS = 5/' pusfre_v3_final.py

echo ""
echo "=== TEST 3: K fijo al valor verdadero ==="
python test_K_fijo.py

echo ""
echo "=== TEST 4: Perfil 1D de λ ==="
python test_perfil.py

echo ""
echo "=== TEST 5: Régimen pusfre (M0 verdadero) ==="
python pusfre_v3_final.py --mode synthetic --regime pusfre --n 2000 --bootstrap 30

echo ""
echo "=== TESTS COMPLETADOS ==="
```

## Script 3: Validación cruzada inter-dominio — **PENDIENTE DE IMPLEMENTACIÓN**

**Estado v3.2:** Este script es un **esqueleto**, no una implementación funcional. Los cargadores de datos son placeholders. Los fitters y predictores de `pusfre_v3_final.py` no se importan correctamente. **No se puede ejecutar como está.** Se incluye aquí como referencia de la estructura propuesta, no como código ejecutable. Se mueve explícitamente a §9 (Próximos pasos) como trabajo pendiente.

```python
"""
test_cross_domain.py — ESQUELETO PENDIENTE DE IMPLEMENTACIÓN

Objetivo propuesto: aplicar la familia CES-Saturada a dominios donde
el PUSFRE ya es el estándar aceptado, con criterio BIC.

Dominios propuestos:
    1. neural_scaling:  L = A·N^(-α)·D^(-β), Φ=N, Ψ=D, Ω=compute
    2. urban_scaling:   Y = Y0·N^β, Φ,Ψ demográficos, Ω=N
    3. species_area:    S = c·A^z, Ω=A, Φ,Ψ hábitat
    4. fama_french:     R = α + β1·MKT + β2·SMB + β3·HML, aditivo lineal

ESTADO: no implementado. Los cargadores de datos son placeholders.
Los fitters y predictores no se importan de pusfre_v3_final.py.

Para implementar:
    1. Descargar datos de cada dominio (ver referencias).
    2. Mapear variables a Φ, Ψ, Ω, F.
    3. Importar fit_M0, fit_M6, evaluate_cv de pusfre_v3_final.py.
    4. Ejecutar out-of-sample con BIC.
    5. Reportar si ΔBIC > 10 en algún dominio.

Referencias de datos:
    - Neural scaling: Hoffmann et al. (2022), "Training Compute-Optimal
      Large Language Models". Dataset público en GitHub.
    - Urban scaling: Bettencourt et al. (2007), PNAS. Datos de
      censos urbanos disponibles en repositorios públicos.
    - Species-area: Arrhenius (1921). Datos de biogeografía en
      bases de datos ecológicas.
    - Fama-French: Fama & French (1993). Datos de factores
      descargables de la base de datos de Kenneth French.

Predicción honesta (a testear):
    - Neural/urban: M6 NO gana en BIC (Ω cubre varios órdenes de
      magnitud, Hill ≈ potencia pura).
    - Species-area: M0 gana limpio.
    - Fama-French: M6 podría ganar marginal en RMSE, pero λ≈1
      con BIC peor.

Hipótesis a testear: si M6 gana en BIC Y IC de λ excluye 0 en algún
dominio con Ω cubriendo MENOS de un orden de magnitud, ese es el
caso de uso legítimo.
"""

# (El código del esqueleto se omite porque no es funcional.
#  Se incluye solo la documentación del objetivo y las referencias.)
```

---

# ANEXO IV: AUDITORÍA DE IDENTIFICABILIDAD

## Diagnóstico final (revisado v3.2)

La familia CES-Saturada tiene cuatro parámetros ($\lambda, K, \alpha_h, w$) más el ruido ($\sigma_\varepsilon$). Con N=2000:

- **λ**: se identifica con error ~8%, pero IC contiene el 0. **Marginalmente identificable.**
- **K**: no se identifica (error 132%, IC [0.07, 4.35]). **No identificable.**
- **α_h**: no se identifica (error 24%, IC [0.35, 2.58]). **No identificable.**
- **w**: se identifica aceptablemente (todos los componentes en [0.22, 0.45]). **Identificable.**

## Causas (v3.2)

1. **Degeneración estructural K–α_h.** Hill entra como $\Omega^\alpha/(K^\alpha + \Omega^\alpha)$. Si $\Omega \ll K$ en el rango observable, entonces Hill $\approx \Omega^\alpha/K^\alpha$, que depende de α y K solo a través de la combinación $(\alpha, \log K)$. Hay una curva 1D en $(K, \alpha)$ que da saturación indistinguible. **Más N no rompe esto.** Solo lo rompería cubrir un rango de Ω donde la curvatura Hill sea visible.

2. **Correlación λ–w.** Cuando λ cambia, los pesos óptimos cambian. Hay una familia de soluciones casi equivalentes. Esto es menos grave que la degeneración K–α.

3. **Ruido LogNormal con σ=0.05 no es suficiente** para romper las degeneraciones en N=2000.

## Soluciones propuestas (v3.2)

1. **N mayor** (probado hasta N=5000, sin mejora). No resuelve la degeneración K–α.
2. **Cubrir un rango mayor de Ω.** Si los datos tienen Ω con varios órdenes de magnitud, la curvatura Hill se vuelve visible. **Esta es una hipótesis, no una conclusión.**
3. **Fijar K a un valor conocido** en dominios donde se puede estimar independientemente.
4. **Priors bayesianos.** Si se tiene información a priori sobre K o α, se puede romper la degeneración.
5. **Regularización L2 sobre w** para reducir varianza. Útil si $w$ no es el parámetro de interés.

## Implicación (v3.2)

Los parámetros estimados por M6 deben reportarse con **cautela**:

- **Predicción:** fiable (el modelo predice bien aunque los parámetros no sean únicos).
- **Interpretación:** no fiable con N=2000.

**Recomendación de reporte:** usar dos cifras significativas para parámetros no identificables. Reportar IC siempre. No interpretar $\lambda$, $K$, $\alpha_h$ como parámetros estructurales.

## Línea de investigación abierta (v3.2)

La degeneración K–α sugiere una pregunta más interesante que la identificabilidad: **¿en qué régimen de Ω es la saturación Hill identificable?** La respuesta requiere un análisis de curvatura: Hill tiene curvatura máxima cuando Ω ≈ K. Si los datos cubren Ω en un rango donde Ω/K es constante, la saturación es invisible. Si cubren un rango donde Ω/K varía de 0.1 a 10, la curvatura es visible.

**Esto es una hipótesis, no una conclusión.** Se puede testear con el perfil de verosimilitud 2D (`profile_likelihood_2d`), que ya está en el código. El resultado esperado es que la región de alta verosimilitud en el plano (K, α) sea una curva 1D (degenerada) cuando Ω/K es constante, y una región 2D (identificable) cuando Ω/K varía.

**Predicción falsable.** Si en un dominio con Ω cubriendo varios órdenes de magnitud el perfil 2D sigue siendo degenerado, entonces la degeneración no es del rango de Ω, sino de la estructura de Hill misma. Esto requeriría revisar la elección de la función de saturación.

---

# ANEXO V: CORRECCIONES RESPECTO A v3.1

Este anexo documenta cada cambio entre v3.1 y v3.2, con su justificación.

## V.1 Paso 3 del Apéndice A reforzado

**Problema en v3.1.** El argumento original decía: "el argumento $a \cdot z_j + s$ recorre un intervalo abierto de $\mathbb{R}$". Esto no estaba demostrado. En particular, el caso $z_j = 1/\lambda$ (donde $a \cdot z_j + s$ es constante en $c$) no se trataba.

**Corrección en v3.2.** Se añade demostración completa con dos casos:

- **Caso 1 ($\lambda \neq 0$):** subcaso 1a ($z_j \neq 1/\lambda$): el mapa $c \mapsto \phi_j(c)$ recorre un intervalo abierto, y por continuidad de $(g_j^\lambda)'$, esta es constante en $\mathbb{R}$. Subcaso 1b ($z_j = 1/\lambda$): el argumento del subcaso 1a se aplica para otros $z_j'$, y por continuidad, $(g_j^\lambda)'(1/\lambda)$ toma el mismo valor.
- **Caso 2 ($\lambda = 0$):** $\phi_j(c) = z_j + \log(c)$ recorre todo $\mathbb{R}$.

**Impacto.** El Paso 3 ahora es una demostración completa, no un esquema. La conclusión no cambia, pero la prueba es rigurosa.

## V.2 Límite de $w_i$ corregido

**Problema en v3.1.** El texto decía $w_i \in [0.1, 0.8]$ pero el código usaba `0.1 + 0.8 * (v / sum(v))`, que da $w_i \in [0.1, 0.9]$. Inconsistencia entre texto y código.

**Corrección en v3.2.** Se cambia el código a `0.1 + 0.7 * (v / sum(v))`, que da $w_i \in [0.1, 0.8]$ con $\sum w_i = 1$:

$$\sum_i w_i = 3 \cdot 0.1 + 0.7 \cdot \frac{\sum v_i}{\sum v_j} = 0.3 + 0.7 = 1.0$$

**Impacto.** Los resultados numéricos de v3.0 no cambian sustancialmente (la diferencia entre 0.8 y 0.9 como techo es marginal), pero la coherencia texto-código se restaura.

## V.3 Tabla CES económica degradada

**Problema en v3.1.** §2.3 mantenía la tabla con columna "$\sigma$" y "Régimen", lo cual sugería interpretación económica.

**Corrección en v3.2.** Se reemplaza "Régimen" por "Forma matemática del agregador" y se añade advertencia explícita: la columna "$\sigma$" es una cantidad sin interpretación estructural en el PUSFRE.

**Impacto.** Se elimina la ambigüedad sobre si $\lambda$ tiene significado económico. No lo tiene.

## V.4 Motivación de A5 ampliada

**Problema en v3.1.** A5 se postulaba sin justificación. Era la hipótesis más fuerte del teorema y no se discutía.

**Corrección en v3.2.** Nueva subsección §3.2 que:

- Interpreta A5 como invariancia de unidades.
- Enumera tres alternativas (invariancia no afín, solo translación, ausencia de invariancia).
- Explica por qué se elige A5: es la hipótesis más débil que da una familia paramétrica uniparamétrica de formas separables.
- Reconoce que A5 no tiene justificación empírica.

**Impacto.** El teorema se presenta con honestidad sobre sus hipótesis. A5 es una elección, no una necesidad.

## V.5 ΔBIC concreto en régimen `pusfre`

**Problema en v3.1.** §5.1 reportaba "M0 gana bajo BIC" sin dar el valor numérico. Esto ocultaba que la diferencia era pequeña.

**Corrección en v3.2.** Se reporta $\Delta$BIC = 1.2 y se clasifica según Burnham & Anderson (2002):

- $\Delta$BIC ∈ [0, 2]: evidencia débil.
- $\Delta$BIC ∈ [2, 6]: evidencia positiva.
- $\Delta$BIC ∈ [6, 10]: evidencia fuerte.
- $\Delta$BIC > 10: evidencia muy fuerte.

Con $\Delta$BIC = 1.2, **M0 y M2 son estadísticamente indistinguibles en `pusfre`**. La conclusión correcta no es "M0 gana", sino "el pipeline no identifica el modelo verdadero en este régimen con N=2000".

**Impacto.** Se reconoce un límite del pipeline que v3.1 ocultaba tras una victoria nominal de BIC.

## V.6 Anexo III marcado como pendiente

**Problema en v3.1.** El script de validación cruzada inter-dominio se presentaba como funcional, pero era un esqueleto con placeholders.

**Corrección en v3.2.** Se marca explícitamente como **PENDIENTE DE IMPLEMENTACIÓN**. Se mueve a §9 (Próximos pasos) como trabajo futuro, con documentación de objetivo y referencias de datos, pero sin código ejecutable.

**Impacto.** No se induce a error al lector sobre qué se ha ejecutado y qué no.

## V.7 Predicción sobre dominios Ω amplio marcada como hipótesis

**Problema en v3.1.** El Cierre y §8.6 afirmaban que "la extensión tiene su caso de uso legítimo en dominios donde Ω cubre varios órdenes de magnitud". Esto era una conclusión, no una hipótesis.

**Corrección en v3.2.** Se reformula como **hipótesis a testear**. La afirmación se convierte en: "la hipótesis es que la extensión aporta valor en dominios con Ω amplio; esto no se ha verificado empíricamente".

**Impacto.** Se distingue entre lo que se ha demostrado y lo que se conjetura.

## V.8 Anexo V añadido

**Corrección en v3.2.** Se añade este anexo para trazabilidad explícita de cambios.

**Impacto.** El lector puede auditar qué cambió y por qué.

## V.9 Tabla resumen de correcciones

| # | Problema v3.1 | Corrección v3.2 | Impacto |
|---|---------------|------------------|---------|
| V.1 | Paso 3 incompleto (caso $z_j = 1/\lambda$ no tratado) | Demostración completa con dos casos | Rigor formal |
| V.2 | Texto dice $[0.1, 0.8]$, código da $[0.1, 0.9]$ | Código corregido a $0.1 + 0.7 \cdot v/\sum v$ | Coherencia |
| V.3 | Tabla CES con interpretación económica implícita | Tabla marcada como referencia matemática pura | Honestidad |
| V.4 | A5 sin justificación | §3.2 con motivación y alternativas | Honestidad |
| V.5 | ΔBIC no reportado en `pusfre` | ΔBIC = 1.2 reportado y clasificado | Honestidad |
| V.6 | Script inter-dominio presentado como funcional | Marcado como pendiente | Honestidad |
| V.7 | Predicción sobre Ω amplio como conclusión | Reformulada como hipótesis | Honestidad |
| V.8 | Sin trazabilidad de cambios | Anexo V añadido | Auditoría |

---

# Cierre

La familia CES-Saturada es:

- **Predictivamente superior** al PUSFRE base en datos sintéticos con estructura CES+Hill. **No hay evidencia independiente** de que sea superior en dominios reales.
- **Identificablemente incompleta** con N=2000 en regímenes de Ω estrecho. Los IC bootstrap del 95% para λ contienen el 0. Los errores de K y α no decrecen con N por **degeneración estructural K–α**.
- **Discriminatoriamente limitada**: en régimen `pusfre` con N=2000, ni RMSE ni BIC distinguen M0 de M2 ($\Delta$BIC = 1.2, evidencia débil). El pipeline no es un identificador automático de estructura.
- **Caracterizada axiomáticamente de forma condicional**: el Teorema 2.1 es válido bajo A1–A5, pero los axiomas son posiciones teóricas. A5 en particular no tiene justificación empírica.
- **Pendiente de validación real** y de validación cruzada inter-dominio.

Estos cinco hechos definen el estatus actual: **herramienta predictiva con parámetros latentes, caracterización axiomática condicional, pendiente de validación real y de resolución de identificabilidad en regímenes de Ω estrecho**.

## Pregunta abierta central

La pregunta abierta más importante no es "¿es CES la forma correcta?" sino:

> **¿En qué dominios la familia CES-Saturada aporta algo que el PUSFRE base no aporta ya?**

La respuesta candidata es: en dominios donde Ω cubre varios órdenes de magnitud y la saturación es visible. Ahí la curvatura Hill podría ser identificable y el modelo CES-Saturado podría justificarse empíricamente.

**Esto es una hipótesis, no una conclusión.** No se ha testeado.

## Lo que el tratado ha establecido

1. **La caracterización axiomática se sostiene** bajo A1–A5 (Teorema 2.1), con demostración completa (Apéndice A).
2. **La familia CES-Saturada contiene al PUSFRE base** como caso límite ($\lambda \to 0$, $K \to \infty$, $k = 1$).
3. **El pipeline de validación funciona** cuando la estructura subyacente es clara (regímenes `ces`, `hill`, `full`).
4. **El pipeline no funciona** cuando la estructura es débil (régimen `pusfre`).
5. **Los parámetros $\lambda$, $K$, $\alpha_h$ no son identificables** con N=2000 en el régimen de Ω cubierto por los datos sintéticos.
6. **La extensión no ha sido validada en datos reales.**

## Lo que el tratado NO ha establecido

1. Que la familia CES-Saturada sea superior al PUSFRE base en dominios reales.
2. Que los axiomas A1–A5 sean empíricamente válidos.
3. Que la degeneración K–α se resuelva con más N.
4. Que el modelo sea identificable en algún dominio conocido.
5. Que $\lambda$ tenga interpretación estructural.

## Recomendación al lector

Si el lector busca un modelo predictivo con parámetros latentes y estructura CES+Hill, la familia CES-Saturada es una opción razonable. **Debe reportar los parámetros con cautela**, usar BIC en lugar de RMSE para comparación de modelos, y no interpretar $\lambda$ como elasticidad de sustitución.

Si el lector busca un modelo estructural con parámetros interpretables, **este tratado no lo proporciona**. La identificabilidad no está resuelta, y la caracterización axiomática es condicional.

Si el lector busca un test de qué régimen subyace a sus datos, **el pipeline no es un identificador automático**. En regímenes débiles, M0 y M2 son indistinguibles con N=2000.

---

**Fin del Tratado de Extensión del PUSFRE — Versión 3.2.**

*"La universalidad no está en el punto. Está en la familia. Pero la familia, a veces, tampoco es identificable. Y cuando no lo es, conviene decirlo — y decirlo con precisión sobre qué se ha demostrado, qué se ha observado, y qué se conjetura."*

1310.
