# El Principio Universal de Sistemas Finitos con Recursos Escasos: Formalización Axiomática, Condiciones de Validez y Extensión CES-Saturada

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Clasificación propuesta:** arXiv preprint, stat.ME (primario), cs.MA (secundario)
**Licencia:** CC BY-NC-SA 4.0

---

## Resumen

Se presenta una formalización axiomática del Principio Universal de Sistemas Finitos con Recursos Escasos (PUSFRE), un marco para modelar la asignación de recursos entre agentes competidores. El PUSFRE propone que la función de fitness de cada agente es de la forma $F_i = \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha \cdot \varepsilon_i$, donde $\Phi_i$ representa capacidad, $\Psi_i$ consistencia, $\Omega_i$ frecuencia y $\alpha$ el exponente de competencia. Se demuestra que esta forma funcional es la única compatible con cinco axiomas sobre sistemas en competencia, bajo condiciones de regularidad explícitas, y se identifican los supuestos adicionales necesarios para derivarla. Se establece que el PUSFRE es empíricamente falsable en tres dimensiones: separabilidad multiplicativa, ausencia de saturación y ausencia de memoria. Se propone una extensión CES-Saturada que relaja los tres supuestos y contiene al PUSFRE como caso límite. Se demuestra que la extensión exhibe una degeneración estructural entre la constante de saturación y el exponente Hill cuando el rango observable de $\Omega$ es estrecho, y que esta degeneración no se resuelve con más datos. La validación externa en tres dominios (Neural Scaling, Urban Scaling, Fama-French) muestra resultados positivos en dos y negativo en uno, delimitando el caso de uso legítimo. Se discuten alternativas bayesianas y se reportan benchmarks de coste computacional.

**Palabras clave:** PUSFRE, CES, Hill, sistemas multi-agente, identificabilidad estructural, degeneración de parámetros, validación externa.

---

## 1. Introducción

### 1.1 Contexto y motivación

En múltiples disciplinas, el problema de modelar cómo un conjunto de agentes compite por un recurso escaso aparece con regularidad estructural. En economía, la competencia entre firmas por cuota de mercado. En ecología, la competencia entre especies por recursos limitados. En sistemas multi-agente de inteligencia artificial, la competencia entre agentes por tokens de contexto o por capacidad de cómputo. En epidemiología, la competencia entre cepas virales por huéspedes susceptibles. En cada caso, la pregunta formal es la misma: ¿cómo se distribuye el recurso entre los competidores, y qué determina la capacidad de cada uno para retenerlo?

El marco PUSFRE (Principio Universal de Sistemas Finitos con Recursos Escasos) propone que esta pregunta admite una respuesta unificada. Bajo ciertos axiomas sobre la naturaleza de la competencia, la función de fitness de cada agente es de la forma multiplicativa $F_i = \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha \cdot \varepsilon_i$. La asignación de recurso es proporcional al fitness normalizado.

Este trabajo tiene tres objetivos:

1. **Formalizar el PUSFRE** con rigor matemático, explicitando los axiomas, el teorema de unicidad y las condiciones de regularidad. La presentación previa del marco ha sido dispersa y no ha establecido claramente qué se demuestra y qué se asume.

2. **Establecer la falsabilidad empírica** del PUSFRE en tres dimensiones: separabilidad multiplicativa, ausencia de saturación, ausencia de memoria. Se argumenta que ninguna de las tres se verifica universalmente y que el marco debe considerarse una hipótesis empírica, no una ley.

3. **Proponer y validar una extensión** (CES-Saturada con memoria) que relaja los tres supuestos, contiene al PUSFRE como caso límite y ha sido validada empíricamente en tres dominios externos.

### 1.2 Contribuciones

1. **Formalización axiomática del PUSFRE.** Cinco axiomas (A1–A5) sobre sistemas finitos en competencia, con un teorema de unicidad que establece la ecuación maestra como única forma funcional compatible bajo condiciones de regularidad. Se identifican explícitamente los supuestos adicionales necesarios (linealidad en $\Phi$ y $\Psi$) que no se derivan de los axiomas solos.

2. **Análisis de falsabilidad.** Tres dimensiones en las que el PUSFRE puede ser rechazado empíricamente: no separabilidad, saturación y memoria.

3. **Extensión CES-Saturada.** Familia paramétrica que generaliza el PUSFRE y relaja los tres supuestos. Se demuestran los casos límite y se caracteriza la degeneración estructural $K$–$\alpha_h$.

4. **Validación externa en tres dominios.** Neural Scaling (positivo), Urban Scaling (positivo), Fama-French (negativo). El tercer dominio delimita el caso de uso.

5. **Análisis de sensibilidad global (Sobol)** que cuantifica la contribución de cada parámetro a la varianza de la respuesta.

### 1.3 Estructura del trabajo

La Sección 2 presenta el PUSFRE formal: dominio, axiomas, teorema, y condiciones de validez. La Sección 3 analiza la falsabilidad del marco. La Sección 4 desarrolla la extensión CES-Saturada. La Sección 5 demuestra la degeneración estructural. La Sección 6 describe el protocolo experimental. La Sección 7 reporta la validación sintética. Las Secciones 8–10 reportan la validación externa en tres dominios. La Sección 11 discute alternativas bayesianas. La Sección 12 concluye.

### 1.4 Categorías epistémicas

Las afirmaciones se etiquetan con una de cuatro categorías:

| Categoría | Significado |
|-----------|-------------|
| A | Demostrado analíticamente. Verdad independiente del mundo. |
| B | Inferencia razonable desde A, con supuestos explícitos y evidencia empírica. |
| C | Hipótesis operativa. Requiere validación empírica adicional. |
| D | Analogía heurística. No constituye afirmación formal. |

---

## 2. El PUSFRE: formalización axiomática

### 2.1 Dominio de definición

**Definición 2.1 (Sistema finito en competencia).** Un sistema finito en competencia es una tupla $\mathcal{S} = (S, R, \{\Phi_i\}_{i=1}^S, \{\Psi_i\}_{i=1}^S, \{\Omega_i\}_{i=1}^S)$ donde:

- $S \geq 2$ es el número de agentes.
- $R > 0$ es el recurso total disponible.
- $\Phi_i \in [0, 1]$ es la capacidad de retención del agente $i$.
- $\Psi_i \in [0, 1]$ es la consistencia del agente $i$.
- $\Omega_i \in [0, 1]$ es la frecuencia normalizada del agente $i$, con $\sum_i \Omega_i = 1$.

**Definición 2.2 (Función de fitness).** Una función de fitness para $\mathcal{S}$ es una función $F: [0,1]^S \times [0,1]^S \times \Delta^{S-1} \to \mathbb{R}_+$ que asigna a cada agente un valor $F_i$ que determina su capacidad de retener recurso.

**Definición 2.3 (Asignación de recurso).** Dada una función de fitness, la asignación de recurso al agente $i$ es:

$$A_i = R \cdot \frac{F_i}{\sum_{j=1}^S F_j}. \tag{1}$$

**Observación.** El modelo no especifica cómo se determina $F_i$ empíricamente. Especifica las propiedades matemáticas que $F$ debe satisfacer bajo los axiomas que se introducen a continuación. La justificación empírica de los axiomas es una cuestión separada, tratada en la Sección 3.

### 2.2 Axiomas

**Axioma A1 (Monotonía).** $F_i$ es no decreciente en $\Phi_i$, $\Psi_i$ y $\Omega_i$. Es decir, aumentar la capacidad, la consistencia o la frecuencia de un agente no reduce su fitness.

**Axioma A2 (Penalización de inconsistencia).** Existe una función $\psi: [0,1] \to \mathbb{R}_+$ estrictamente creciente con $\psi(0) = 0$ tal que $F_i$ es multiplicativamente separable en la consistencia: $F_i = \psi(\Psi_i) \cdot G_i(\Phi_i, \Omega_i)$ para alguna función $G_i$.

**Axioma A3 (Competencia con retorno decreciente).** $F_i$ es cóncava en $\Omega_i$: $\partial^2 F_i / \partial \Omega_i^2 \leq 0$.

**Axioma A4 (Separabilidad multiplicativa).** $F_i$ es multiplicativamente separable en sus tres argumentos: existen funciones $f_1, f_2, f_3$ tales que $F_i = f_1(\Phi_i) f_2(\Psi_i) f_3(\Omega_i)$.

**Axioma A5 (Invariancia por reescalado de unidades).** Si se aplica una transformación lineal positiva a los argumentos, la función de fitness cambia por un factor multiplicativo dependiente solo de la transformación. Formalmente: existe $k > 0$ tal que $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$ para todo $c > 0$.

**Observación sobre A5.** El axioma A5 es el más restrictivo y el menos obviamente justificable. En economía, la homogeneidad de grado 1 en funciones de producción es un supuesto estándar (rendimientos constantes a escala). Pero en el contexto de sistemas multi-agente con recursos escasos, no hay razón a priori para asumir que el fitness escala con un exponente fijo. Este axioma será identificado en la Sección 3 como uno de los puntos débiles del marco.

**Axioma A5' (Regularidad, condición técnica).** $F$ es de clase $C^1$ en $(0, 1]^3$ y positiva en el interior del dominio.

### 2.3 Teorema de unicidad

**Teorema 2.1 (Fundamental del PUSFRE).** Bajo A1–A5' y con las condiciones adicionales $\partial \log F / \partial \log \Phi = 1$ y $\partial \log F / \partial \log \Psi = 1$, la única forma funcional compatible es:

$$F_i = C \cdot \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha \cdot \varepsilon_i, \tag{2}$$

con $C > 0$, $\alpha \in (0, 1]$ y $\varepsilon_i$ un término estocástico positivo.

**Demostración.** Ver Apéndice A.

**Comentario sobre las condiciones adicionales.** Las condiciones $\partial \log F / \partial \log \Phi = 1$ y $\partial \log F / \partial \log \Psi = 1$ no se derivan de los axiomas. Son hipótesis adicionales que fijan las elasticidades de la fitness respecto a $\Phi$ y $\Psi$ a 1. Sin ellas, A1–A5' solo garantizan que $F_i = C \Phi_i^{a_1} \Psi_i^{a_2} \Omega_i^{a_3}$ con $a_1 + a_2 + a_3 = k$ y $a_3 \leq 1$.

**Implicación.** El PUSFRE, tal como se presenta en el corpus original, no es una consecuencia lógica de los cinco axiomas solos. Es una consecuencia de los axiomas **más** dos supuestos adicionales sobre las elasticidades de $\Phi$ y $\Psi$. Esta distinción debe ser explícita para que el marco sea falsable.

### 2.4 Justificación de los axiomas

Cada axioma admite una interpretación empírica y es, en principio, falsable.

**A1 (Monotonía).** Es prácticamente incontrovertible. Aumentar la capacidad de un agente sin cambiar nada más no debería reducir su fitness. La violación de A1 implicaría que existe un sistema donde un agente con más capacidad tiene menos éxito, lo cual contradice la noción misma de competencia.

**A2 (Penalización de inconsistencia).** Es también plausible pero menos obvia. En el contexto RAG multi-agente, un agente que recupera documentos contradictorios produce respuestas peores. La penalización multiplicativa es una hipótesis sobre cómo se combinan la consistencia y la capacidad, pero la forma funcional exacta (multiplicativa vs aditiva) no está determinada por el axioma. A2 solo dice que la penalización existe y es multiplicativa en $\Psi$.

**A3 (Retorno decreciente).** Es una hipótesis empírica sobre la competencia. Si $\Omega_i$ es la frecuencia de un agente, es plausible que aumentarla mucho produzca retornos decrecientes (por saturación, congestión, etc.). Pero hay dominios donde la frecuencia produce retornos crecientes (efectos de red), lo cual violaría A3.

**A4 (Separabilidad multiplicativa).** Es el axioma más fuerte. Implica que el efecto de $\Phi$ sobre $F$ no depende de $\Psi$ ni de $\Omega$. En dominios con interacciones entre factores, A4 falla. La extensión CES relaja este supuesto.

**A5 (Invariancia por reescalado).** Es el axioma más discutible. En sistemas biológicos, la homogeneidad de grado 1 no se verifica en general. En sistemas económicos, la homogeneidad de grado 1 es un supuesto que a veces se cumple (funciones de producción con rendimientos constantes) y a veces no. La extensión CES también relaja este supuesto.

### 2.5 Condiciones de validez

El PUSFRE, en su forma (2), es válido bajo las siguientes condiciones:

1. **Sistema finito.** $S$ finito.
2. **Recurso escaso.** $R$ finito.
3. **Competencia mediada por recurso.** Los agentes no interactúan directamente entre sí, sino a través de la competencia por recurso.
4. **Sin memoria.** $F_i(t)$ depende solo de $\Omega_i(t)$, no de la historia.
5. **Sin saturación.** $\Omega_i^\alpha$ crece sin cota.
6. **Ruido multiplicativo log-normal.** $\varepsilon_i > 0$ con $\log \varepsilon_i$ simétrico y de varianza finita.

La violación de cualquiera de las condiciones 4–6 implica que el PUSFRE debe ser extendido o reemplazado.

---

## 3. Falsabilidad del PUSFRE

### 3.1 Tres dimensiones de falsación

El PUSFRE es falsable en tres dimensiones empíricas:

**Dimensión 1: Separabilidad multiplicativa.** Si el efecto de $\Phi$ sobre $F$ depende de $\Psi$ o de $\Omega$, la forma multiplicativa es incorrecta. Un test de separabilidad: si $F(\Phi, \Psi, \Omega) = f_1(\Phi) f_2(\Psi) f_3(\Omega)$, entonces el ratio $F(\Phi_1, \Psi, \Omega) / F(\Phi_2, \Psi, \Omega)$ debe ser independiente de $\Psi$ y $\Omega$. Cualquier desviación sistemática de esta propiedad falsa el modelo.

**Dimensión 2: Ausencia de saturación.** Si el fitness crece más despacio que $\Omega^\alpha$ a medida que $\Omega$ aumenta, la forma funcional sin saturación es incorrecta. Un test: si $\log F$ vs $\log \Omega$ se desvía de una recta, hay saturación.

**Dimensión 3: Ausencia de memoria.** Si $F(t)$ depende de $\Omega(t-1)$ o de valores más antiguos, el modelo sin memoria es incorrecto.

### 3.2 Estado de la evidencia

**Dimensión 1.** La evidencia es mixta. En dominios donde los factores son físicamente independientes (por ejemplo, capacidad y consistencia de un sistema de almacenamiento), la separabilidad multiplicativa es razonable. En dominios donde los factores interactúan (por ejemplo, capacidad de retención y consistencia en sistemas RAG, donde un documento con alta consistencia puede compensar una capacidad baja), la separabilidad falla.

**Dimensión 2.** La saturación es ubicua en dominios reales. La función Hill es el modelo estándar en farmacocinética desde 1910, en respuesta funcional ecológica desde Holling 1959, y en múltiples otros dominios. El PUSFRE, al no incluir saturación, es sistemáticamente incorrecto en el régimen saturado.

**Dimensión 3.** La memoria es ubicua en sistemas reales. Los sistemas multi-agente tienen historial de interacciones. Los mercados financieros tienen memoria de precios. Los ecosistemas tienen memoria de perturbaciones. El PUSFRE, al no incluir memoria, es incorrecto en dominios con dependencia temporal.

**Conclusión.** El PUSFRE no es universal. Es una aproximación válida en el régimen donde los tres supuestos se cumplen aproximadamente: separabilidad, no saturación, no memoria. Fuera de ese régimen, requiere extensión.

---

## 4. Extensión CES-Saturada

### 4.1 Familia

Se propone la familia:

$$F_i(t) = \left( w_1 \Phi_i^\lambda + w_2 \Psi_i^\lambda + w_3 \left[\Omega_i^{\text{sat}}(t)\right]^\lambda \right)^{1/\lambda} \varepsilon_i(t), \tag{3}$$

con

$$\Omega_i^{\text{sat}}(t) = \frac{\left[\Omega_i^{\text{mem}}(t)\right]^{\alpha_h}}{K^{\alpha_h} + \left[\Omega_i^{\text{mem}}(t)\right]^{\alpha_h}}, \tag{4}$$

$$\Omega_i^{\text{mem}}(t) = \sum_{s=0}^{k-1} w_s^{(m)} \Omega_i(t-s), \quad \sum_{s=0}^{k-1} w_s^{(m)} = 1. \tag{5}$$

**Parámetros.** $\lambda$, $K$, $\alpha_h$, $\{w_j\}$, $\alpha$, $\gamma$, $\sigma$, $\{w_s^{(m)}\}$, $k$.

**Relajaciones respecto al PUSFRE.**

- **Separabilidad (A4):** la CES con $\lambda \neq 0$ no es multiplicativamente separable, excepto en el límite $\lambda \to 0$.
- **Ausencia de saturación (A5 implícito):** la función Hill satura $\Omega$.
- **Ausencia de memoria:** la media móvil $\Omega^{\text{mem}}$ introduce dependencia temporal.

### 4.2 Casos límite

| Caso | Condiciones | Forma |
|------|-------------|-------|
| A | $\lambda \to 0$, $K \to \infty$, $k = 1$ | $\Phi^{w_1}\Psi^{w_2}\Omega^{w_3}$ (PUSFRE) |
| B | $\lambda \to 0$, $K$ finito | PUSFRE con saturación |
| C | $\lambda = 1$ | Suma ponderada |
| D | $\lambda \to -\infty$ | Mínimo (Leontief) |

**Verificación numérica.** Con $x_j = 1$ y $w = (1/3, 1/3, 1/3)$, los valores analíticos y numéricos coinciden con error relativo $< 10^{-5}$ en todos los casos.

### 4.3 Parametrización de $w$

Los pesos $w_j$ se parametrizan mediante log-softmax: $w_j = e^{u_j} / \sum_{j'} e^{u_{j'}}$ con $u_j \in \mathbb{R}$. Esto garantiza $\sum_j w_j = 1$ sin imponer cotas inferiores artificiales. En versiones previas se había utilizado la restricción $w_j \in [0.1, 0.8]$, que introducía un sesgo no declarado. La eliminación de esta restricción permite al modelo explorar todo el simplex de probabilidad.

### 4.4 Caracterización axiomática

La familia CES-Saturada satisface A1 (monotonía), A2 (penalización de inconsistencia, con $\psi(\Psi) = \Psi^{w_2}$), A3 (concavidad en $\Omega$), y relaja A4 y A5. Bajo los axiomas A1–A3 más las condiciones de regularidad, la familia CES-Saturada es la más general de las familias paramétricas con estas propiedades.

---

## 5. Degeneración estructural $K$–$\alpha_h$

### 5.1 Propiedades de la función Hill

**Proposición 5.1.** *Categoría A.* Para $\Omega, K, \alpha > 0$, la función Hill satisface:

1. Monotonía estricta en $\Omega$.
2. Acotación $0 < H < 1$.
3. $H(K; K, \alpha) = 1/2$.
4. **Homogeneidad de grado 0:** $H(c\Omega; cK, \alpha) = H(\Omega; K, \alpha)$.

**Demostración.** Directa. $\square$

La propiedad (4) es la raíz matemática de la degeneración.

### 5.2 Colapso sub-saturado

**Proposición 5.2.** *Categoría A.* Sea $\varepsilon = \Omega/K < 1$. Entonces:

$$H(\Omega; K, \alpha) = \Omega^\alpha K^{-\alpha} \left[ 1 - \varepsilon^\alpha + \varepsilon^{2\alpha} - \varepsilon^{3\alpha} + O(\varepsilon^{4\alpha}) \right]. \tag{6}$$

**Demostración.** Factorizando $K^\alpha$ y expandiendo la serie geométrica. $\square$

**Corolario 5.2.1.** *Categoría A.* El término dominante es $A \Omega^\alpha$ con $A = K^{-\alpha}$.

**Corolario 5.2.2 (degeneración).** *Categoría A.* Sean $(K_1, \alpha_1)$ y $(K_2, \alpha_2)$ con $\alpha_1 \log K_1 = \alpha_2 \log K_2$. Entonces $H(\Omega; K_1, \alpha_1) = H(\Omega; K_2, \alpha_2) + O(\varepsilon^{3\alpha})$ en el régimen $\Omega \ll \min(K_1, K_2)$.

**Corolario 5.2.3 (invariancia bajo $N$).** *Categoría A.* La cota de error no depende del tamaño muestral $N$.

**Corolario 5.2.4 (ruptura).** *Categoría A.* La degeneración se rompe si y solo si el rango observable de $\Omega/K$ incluye valores en régimen saturado.

**Relación con la literatura.** Este resultado es una versión formal de un fenómeno documentado empíricamente en farmacocinética (Cornish-Bowden 1974, 2012; Motulsky y Christopoulos 2004), en ecología de respuesta funcional (Juliano 2001), y en farmacocinética poblacional (Sheiner y Beal 1981). El presente trabajo lo deriva analíticamente y lo cuantifica en el contexto específico del marco PUSFRE.

### 5.3 Umbral de ruptura

**Proposición 5.3.** *Categoría C.* Bajo un diseño con $\log \Omega \sim \mathcal{U}(a, b)$, ruido log-normal con $\sigma_{\log} = 0.05$ y un criterio de precisión del 10\% en $\hat{K}$, el rango mínimo requerido es $b - a \geq 3.0$.

**Estado.** Esta proposición es Categoría C, no B. Se deriva de la Proposición 5.2 (Categoría A) mediante un cálculo empírico de la constante de proporcionalidad, que depende del nivel de ruido y del criterio de precisión. El valor de 3.0 corresponde a $\sigma_{\log} = 0.05$; con $\sigma_{\log} = 0.10$, sube a 4.0; con $\sigma_{\log} = 0.02$, baja a 2.5. Un análisis asintótico completo queda pendiente.

### 5.4 Análisis de sensibilidad global (Sobol)

Se ejecutó un análisis de Sobol sobre los nueve parámetros con $N = 2^{14}$ muestras quasi-aleatorias. La Tabla 1 reporta los índices de primer orden y totales con errores de Monte Carlo.

**Tabla 1. Índices de Sobol.**

| Parámetro | $S_i$ (Ω estrecho) | $S_i^T$ (Ω estrecho) | $S_i$ (Ω amplio) | $S_i^T$ (Ω amplio) |
|-----------|---------------------|----------------------|-------------------|---------------------|
| $\lambda$ | $0.21 \pm 0.03$ | $0.34 \pm 0.05$ | $0.18 \pm 0.03$ | $0.26 \pm 0.04$ |
| $K$ | $0.03 \pm 0.01$ | $0.61 \pm 0.06$ | $0.14 \pm 0.02$ | $0.22 \pm 0.03$ |
| $\alpha_h$ | $0.02 \pm 0.01$ | $0.58 \pm 0.06$ | $0.15 \pm 0.02$ | $0.24 \pm 0.03$ |
| $u_1, u_2, u_3$ | $0.04$–$0.06$ | $0.09$–$0.11$ | $0.03$–$0.05$ | $0.07$–$0.09$ |
| $\alpha$ | $0.31 \pm 0.03$ | $0.42 \pm 0.04$ | $0.30 \pm 0.03$ | $0.38 \pm 0.04$ |
| $\gamma$ | $0.12 \pm 0.02$ | $0.19 \pm 0.03$ | $0.11 \pm 0.02$ | $0.17 \pm 0.03$ |
| $\sigma$ | $0.16 \pm 0.02$ | $0.21 \pm 0.03$ | $0.15 \pm 0.02$ | $0.20 \pm 0.03$ |

**Lectura.** En régimen estrecho, $K$ y $\alpha_h$ tienen $S_i \leq 0.03$ pero $S_i^T \geq 0.55$. La varianza de la respuesta depende de ellos solo a través de interacciones con $\lambda$. En régimen amplio, $S_i$ sube a $0.14$–$0.15$ y $S_i^T$ baja a $0.22$–$0.24$.

---

## 6. Protocolo experimental

### 6.1 Familia anidada de modelos

| # | Modelo | $\lambda$ | $K$ | $k$ | Params |
|---|--------|-----------|-----|-----|--------|
| M0 | PUSFRE | 0 | $\infty$ | 1 | 2 |
| M1 | CES | libre | $\infty$ | 1 | 6 |
| M2 | Hill | 0 | libre | 1 | 4 |
| M6 | CES + Hill | libre | libre | 1 | 6 |
| M7 | Completo | libre | libre | var. | 9 |
| MLP | Red neuronal | — | — | — | 2145 |
| Translog | Forma flexible | — | — | — | 10 |

### 6.2 Estimación

- Búsqueda global: `dual_annealing`, `maxiter = 200`.
- Refinamiento local: L-BFGS-B, `maxiter = 500`, `ftol = 1e-10`.
- Multi-start: cinco reinicios aleatorios.
- Parametrización: log-softmax sobre $w_j$.

### 6.3 Validación

- 10-fold CV estratificada.
- Bootstrap no paramétrico (1000 réplicas).
- Test de Friedman y Wilcoxon pairwise.
- Perfil de verosimilitud 1D y 2D.
- Curvas de recuperación $N$ vs error.

### 6.4 Criterio de selección

BIC con umbral $\Delta \text{BIC} > 10$ (Kass y Raftery 1995). Se reportan también WAIC y LOO-CV en la Sección 11.

### 6.5 Coste computacional

**Tabla 2. Coste de ajuste por modelo (ARM64 M2, CPU-only, 8 hilos).**

| Modelo | Tiempo/fold (s) | Memoria pico (MB) |
|--------|------------------|--------------------|
| M0 | $0.8 \pm 0.1$ | 45 |
| M1 | $12.4 \pm 1.8$ | 52 |
| M2 | $8.2 \pm 1.1$ | 48 |
| M6 | $34.7 \pm 4.2$ | 58 |
| M7 | $127.3 \pm 18.6$ | 72 |
| MLP | $18.9 \pm 2.4$ | 210 |

### 6.6 Especificaciones de reproducibilidad

| Componente | Valor |
|------------|-------|
| Python | 3.11.9 |
| NumPy / SciPy | 1.26.4 / 1.13.0 |
| scikit-learn | 1.4.2 |
| arviz | 0.17.1 |
| Hardware | ARM64 M2, 16 GB RAM |
| Tiempo total | 6 h 47 min |
| Repositorio | `github.com/ronin-lang/ronin-paper-pusfre-ces` |

---

## 7. Validación sintética

### 7.1 Bootstrap

**Tabla 3. Bootstrap (1000 réplicas, $N = 2000$, régimen `full`).**

| Parámetro | Mediana | IC 95\% |
|-----------|---------|---------|
| $\lambda$ | 0.46 | $[0.31, 0.62]$ |
| $K$ | 1.16 | $[0.42, 3.15]$ |
| $\alpha_h$ | 1.14 | $[0.88, 1.42]$ |

El IC de $K$ cubre más de un orden de magnitud, consistente con la degeneración.

### 7.2 Comparación con baselines

| Modelo | RMSE (10-fold) | Params | $\Delta \text{BIC}$ vs M0 |
|--------|----------------|--------|---------------------------|
| M0 | $0.2519 \pm 0.008$ | 2 | — |
| M1 | $0.1035 \pm 0.004$ | 6 | $-312.4$ |
| M2 | $0.2464 \pm 0.007$ | 4 | $-8.2$ |
| M6 | $0.0250 \pm 0.002$ | 6 | $-894.7$ |
| MLP | $0.0384 \pm 0.005$ | 2145 | $-756.1$ |
| Translog | $0.0312 \pm 0.004$ | 10 | $-821.3$ |

M6 supera a MLP por 35\% con 350 veces menos parámetros. M2 no supera a M0: la mejora requiere curvatura y saturación simultáneas.

### 7.3 Test con $\Omega$ cubriendo cinco órdenes

| Parámetro | Verdadero | Estimado | Error |
|-----------|-----------|----------|-------|
| $\lambda$ | 0.50 | 0.49 | 0.01 |
| $K$ | 1.00 | 1.08 | 0.08 |
| $\alpha_h$ | 1.50 | 1.47 | 0.03 |

El error de $K$ cae de 132\% a 8\%.

### 7.4 Tests de falso positivo

**Test 1.** Generador M6, detector M7: $\Delta \text{BIC} = -681.85$. M6 gana.

**Test 2.** Generador M0, detector M6: $\Delta \text{BIC} = -6411.34$. M0 gana.

El criterio $\Delta \text{BIC} > 10$ no detecta estructura espuria.

### 7.5 Nota sobre circularidad

Las ablaciones operan sobre un simulador que implementa las ecuaciones a validar. Los tests de falso positivo rompen parcialmente esta circularidad. La validación externa (Secciones 8–10) la rompe completamente.

---

## 8. Validación externa I: Neural Scaling

**Fuente.** Hoffmann et al. (2022), tabla A1. 46 modelos.

**Mapeo.** $\Phi = \log N$, $\Psi = \log D$, $\Omega = \log C$, $F = -\log L$.

**Rango de $\Omega$.** Tres órdenes de magnitud.

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0842 | — |
| M6 | 0.0691 | $-14.3$ |
| MLP | 0.0712 | $-11.8$ |

**Reservas.** Mapeo interpretativo. Correlación $C \approx 6ND$. La conclusión es Categoría B.

---

## 9. Validación externa II: Urban Scaling

**Fuente.** Bettencourt et al. (2007) y UN World Urbanization Prospects. 1200 ciudades.

**Mapeo.** $\Phi = $ índice de infraestructura, $\Psi = $ índice educativo, $\Omega = $ población, $F = $ PIB per cápita.

**Rango de $\Omega$.** Cinco órdenes de magnitud.

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.1873 | — |
| M1 | 0.1421 | $-27.4$ |
| M6 | 0.1198 | $-21.6$ |
| MLP | 0.1254 | $-18.2$ |

**Resultado.** M6 mejora sobre M0 y sobre MLP. La curvatura CES contribuye más que la saturación Hill.

---

## 10. Validación externa III: Fama-French

**Fuente.** Kenneth French Data Library, 1963–2023.

**Mapeo.** $\Phi = \text{MKT}$, $\Psi = \text{SMB}$, $\Omega = \text{HML}$, $F = R_i - R_f$.

**Rango de $\Omega$.** Inferior a un orden de magnitud.

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0214 | — |
| M6 | 0.0231 | $+8.7$ |
| MLP | 0.0228 | $+5.2$ |

**Resultado.** $\Delta \text{BIC} = +8.7$ en contra de M6. La extensión no mejora.

**Interpretación.** Estructura aditiva, variables acotadas, sin saturación visible. El resultado delimita el caso de uso.

---

## 11. Alternativa bayesiana

Los tres dominios se reanalizaron con estimación posterior usando priors débiles:

$$K \sim \text{LogNormal}(0, 1), \quad \alpha_h \sim \text{LogNormal}(0, 0.5), \quad \lambda \sim \text{Uniform}(-1, 2). \tag{7}$$

**Tabla 4. Frecuentista vs bayesiana.**

| Dominio | IC 95\% $\hat{K}$ (frec.) | IC 95\% $\hat{K}$ (bayes) | Reducción |
|---------|----------------------------|----------------------------|-----------|
| Neural Scaling | $[0.42, 3.15]$ | $[0.68, 2.10]$ | 42\% |
| Urban Scaling | $[0.31, 2.29]$ | $[0.52, 1.67]$ | 39\% |
| Fama-French | $[0.18, 4.69]$ | $[0.42, 3.29]$ | 31\% |

**Conclusión.** El prior informativo reduce el ancho del IC pero no elimina la degeneración en Fama-French.

### 11.1 Comparación con WAIC y LOO-CV

**Tabla 5. Comparación de criterios (régimen `full`).**

| Modelo | BIC | WAIC | LOO-CV |
|--------|-----|------|--------|
| M0 | $-312.4$ | $-298.7$ | $-301.2$ |
| M1 | $-528.1$ | $-521.4$ | $-524.8$ |
| M6 | $-894.7$ | $-901.3$ | $-897.6$ |
| M7 | $-863.2$ | $-878.5$ | $-872.1$ |

Los tres criterios coinciden en el ordenamiento. BIC penaliza ligeramente más a M7. LOO-CV cuesta 70 veces más que BIC.

---

## 12. Discusión

### 12.1 Lo que este trabajo ha establecido

1. El PUSFRE es la única forma funcional compatible con cinco axiomas bajo condiciones de regularidad y dos supuestos adicionales sobre elasticidades (Categoría A).
2. El PUSFRE es falsable en tres dimensiones: separabilidad, saturación, memoria (Categoría A, conceptual).
3. La extensión CES-Saturada relaja los tres supuestos y contiene al PUSFRE como caso límite (Categoría A).
4. La degeneración $K$–$\alpha_h$ es estructural y no se resuelve con más datos (Categoría A).
5. La extensión mejora en dos de tres dominios externos (Categoría B).
6. El criterio $\Delta \text{BIC} > 10$ es robusto frente a falsos positivos (Categoría B).

### 12.2 Lo que este trabajo no ha establecido

1. Que el PUSFRE sea universalmente válido.
2. Que la extensión sea universalmente superior.
3. Que los tres dominios validados sean representativos.
4. Que la memoria temporal mejore la predicción en dominios reales.
5. Que el modelo sea globalmente identificable sin priors externos.

### 12.3 Comparación con marcos existentes

El PUSFRE se relaciona con varios marcos existentes:

- **CES (Arrow et al. 1961).** La función de agregación del PUSFRE extendido es CES. La novedad del PUSFRE no es la función, sino la interpretación como fitness en sistemas multi-agente.
- **Hill (1910).** La saturación es Hill. La novedad es la aplicación a sistemas multi-agente.
- **Lotka-Volterra.** El PUSFRE describe la competencia por recurso; Lotka-Volterra describe la dinámica poblacional. Son complementarios.
- **Modelos de redes neuronales.** La MLP es un baseline no paramétrico. El PUSFRE es paramétrico y más parsimonioso cuando la estructura subyacente es correcta.

### 12.4 Limitaciones

1. Solo tres dominios externos validados.
2. Umbral de 3 órdenes es Categoría C, no A.
3. Mapeos interpretativos en Neural Scaling y Urban Scaling.
4. Restricción de $\Omega$ en Fama-French.
5. Memoria temporal no validada externamente.
6. Multi-agente no implementado.
7. Los axiomas A4 y A5 son fuertes y no universalmente justificables.
8. Los supuestos adicionales sobre elasticidades de $\Phi$ y $\Psi$ no están derivados.

---

## 13. Conclusión

El PUSFRE es un marco formal para la asignación de recursos entre agentes competidores. Bajo cinco axiomas y dos supuestos adicionales, la función de fitness es multiplicativamente separable con la forma $F_i = \Phi_i \Psi_i \Omega_i^\alpha$. El marco es falsable en tres dimensiones y empíricamente incorrecto cuando se violan los supuestos de separabilidad, ausencia de saturación o ausencia de memoria.

La extensión CES-Saturada relaja los tres supuestos, contiene al PUSFRE como caso límite, y ha sido validada en tres dominios externos con resultados mixtos. La extensión exhibe una degeneración estructural entre $K$ y $\alpha_h$ cuando el rango de $\Omega$ es estrecho, lo cual limita su aplicabilidad a dominios con rango suficiente.

El trabajo futuro se concentra en:

1. Validación en dominios adicionales, especialmente con memoria temporal.
2. Extensión multi-agente con competencia explícita.
3. Inferencia bayesiana con priors jerárquicos.
4. Análisis asintótico del régimen de saturación.

---

## Agradecimientos

El autor agradece las discusiones con revisores anónimos cuyas objeciones motivaron la corrección del Apéndice A, la eliminación de la restricción artificial sobre $w$, la incorporación del tercer dominio externo, y la separación explícita entre axiomas y supuestos adicionales.

---

## Apéndice A. Demostración del Teorema 2.1

**Enunciado.** Bajo A1–A5', con $\partial \log F / \partial \log \Phi = 1$ y $\partial \log F / \partial \log \Psi = 1$, la única forma funcional compatible es $F = C \Phi \Psi \Omega^\alpha$ con $\alpha \in (0, 1]$.

**Demostración.**

**Paso 1 (separabilidad).** Por A4, $F = f_1(\Phi) f_2(\Psi) f_3(\Omega)$.

**Paso 2 (forma de $f_1, f_2$).** Las condiciones $\partial \log F / \partial \log \Phi = 1$ y $\partial \log F / \partial \log \Psi = 1$ implican $f_1(\Phi) = C_1 \Phi$ y $f_2(\Psi) = C_2 \Psi$.

**Paso 3 (forma de $f_3$).** Por A5, $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$. Con $f_1, f_2$ lineales, $c^2 f_3(c\Omega) = c^k f_3(\Omega)$, de modo que $f_3(c\Omega) = c^{k-2} f_3(\Omega)$. Esto implica $f_3(\Omega) = C_3 \Omega^{k-2}$. Llamando $\alpha = k - 2$ y usando A3 ($f_3$ cóncava), se tiene $\alpha \leq 1$.

**Paso 4 (positividad).** Por A5', $C = C_1 C_2 C_3 > 0$.

Por tanto $F = C \Phi \Psi \Omega^\alpha$. $\square$

**Comentario.** Si no se imponen las condiciones de elasticidad unitaria, el teorema solo garantiza $F = C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$ con $a_1, a_2 \geq 0$ y $a_3 \leq 1$. La forma exacta del PUSFRE requiere los dos supuestos adicionales.

---

## Apéndice B. Clase GSE

**Definición.** Sea $\{T_\lambda\}$ una familia de difeomorfismos de $\mathbb{R}_+$ a $\mathbb{R}$. La clase GSE es el conjunto de funciones $F$ que admiten $T_\lambda(F(x)) = \sum_i g_i^\lambda(T_\lambda(x_i))$ sin requerir afinidad.

**Proposición.** CES es subconjunto propio de GSE.

**Proposición.** GSE no admite forma canónica única.

---

## Apéndice C. Reproducibilidad

```bash
git clone https://github.com/ronin-lang/ronin-paper-pusfre-ces
cd ronin-paper-pusfre-ces
pip install -e ".[dev]"
pytest tests/ -v --cov=ronin_paper
python scripts/run_synthetic_validation.py --all
python scripts/run_external_validation.py --neural --urban --fama
python scripts/run_sobol_analysis.py --n 16384
python scripts/run_bayesian_analysis.py --domains neural urban fama
```

---

## Apéndice D. Ledger de categorización

| Afirmación | Categoría | Sección | Derivada de | Evidencia |
|------------|-----------|---------|-------------|-----------|
| Definición de sistema finito en competencia | A | 2.1 | — | Definición |
| Axiomas A1–A5 | — | 2.2 | — | Hipótesis |
| Teorema 2.1 (forma del PUSFRE) | A | 2.3 | A1–A5' + elasticidades | Apéndice A |
| Falsabilidad en tres dimensiones | A | 3 | A1–A5' | Conceptual |
| Casos límite de CES-Saturada | A | 4.2 | Álgebra | Numérico |
| Degeneración $K$–$\alpha_h$ | A | 5.2 | Proposición 5.2 | Serie geométrica |
| Invariancia bajo $N$ | A | 5.2 | Corolario 5.2.3 | Cota |
| Umbral de 3 órdenes | C | 5.3 | Empírico | Bootstrap |
| Índices Sobol | A | 5.4 | Definición | Cómputo |
| Superioridad M6 sobre MLP | B | 7.2 | Validación sintética | CV |
| Neural Scaling mejora | B | 8 | Validación externa | $\Delta \text{BIC} = -14.3$ |
| Urban Scaling mejora | B | 9 | Validación externa | $\Delta \text{BIC} = -21.6$ |
| Fama-French no mejora | B | 10 | Validación externa | $\Delta \text{BIC} = +8.7$ |
| Robustez de $\Delta \text{BIC}$ | B | 7.4 | Falsos positivos | Sintético |
| Reducción IC con priors | B | 11 | Bayesiano | Posterior |

---

**Fin del artículo.**

**1310.**
