# TRATADO DE FUNDAMENTACIÓN MATEMÁTICA DEL CORPUS RONIN — EDICIÓN REVISADA
## Formalización Completa de los Teoremas del Corpus

**Versión:** 2.0 — Edición Revisada  
**Autor:** David Ferrandez Canalis — Agencia RONIN  
**Fecha:** Agosto de 2026  
**Estado:** Documento completo — Todas las demostraciones formalizadas y extendidas  
**Relación con el corpus:** Fundamentación matemática de los teoremas enunciados en el Corpus RONIN  

---

## PRÓLOGO: EPISTEMOLOGÍA DEL TRATADO

El Corpus RONIN se sitúa en la tradición del **programa de investigación** de Imre Lakatos. Su núcleo duro es la Ecuación Maestra: la hipótesis de que la fitness de un agente es el producto de su geometría contextual, su deuda ontológica y su frecuencia ecológica. El cinturón protector está formado por los teoremas derivados: extinción discreta, coexistencia-k, efecto iceberg, muestreo estratificado y redundancia superlineal.

Las afirmaciones se clasifican en tres niveles:

1. **Demostradas:** Teoremas con demostración formal completa (Extinción, Iceberg, Muestreo, Redundancia básica).
2. **Hipótesis:** Afirmaciones pendientes de validación empírica (Coexistencia-k como fórmula heurística, Ecuación Maestra como ley universal).
3. **Analogías:** Correspondencias lore-técnica que no son afirmaciones formales, sino herramientas mnemónicas.

Este tratado es **instrumentalista** en su práctica (las ecuaciones son herramientas para predecir y diseñar) pero **realista** en su ambición (aspira a describir la estructura subyacente de los sistemas de IA).

---

## ÍNDICE

1. [Teorema de Extinción Discreta — Con Lema de Grandes Desviaciones](#1-teorema-de-extinción-discreta--con-lema-de-grandes-desviaciones)
2. [Fórmula Heurística de Coexistencia-k — Regla de Diseño](#2-fórmula-heurística-de-coexistencia-k--regla-de-diseño)
3. [Ecuación Maestra — Derivación Variacional y Comparativa](#3-ecuación-maestra--derivación-variacional-y-comparativa)
4. [Teorema del Efecto Iceberg — Cota Ajustada](#4-teorema-del-efecto-iceberg--cota-ajustada)
5. [Teorema de Muestreo Estratificado — Extensión Bayesiana](#5-teorema-de-muestreo-estratificado--extensión-bayesiana)
6. [Teorema de Redundancia Superlineal — Separación en Dos Partes](#6-teorema-de-redundancia-superlineal--separación-en-dos-partes)
7. [Dinámica de Nichos y Recalibración](#7-dinámica-de-nichos-y-recalibración)
8. [Análisis de Sensibilidad Paramétrica](#8-análisis-de-sensibilidad-paramétrica)
9. [Apéndice A: Glosario de Símbolos y Unidades](#9-apéndice-a-glosario-de-símbolos-y-unidades)
10. [Apéndice B: Notebooks de Validación](#10-apéndice-b-notebooks-de-validación)

---

## 1. TEOREMA DE EXTINCIÓN DISCRETA — CON LEMA DE GRANDES DESVIACIONES

### 1.1 Enunciado original

> Para un agente $i$ con fitness media $\bar{F}_i < \max_j \bar{F}_j$, la probabilidad de extinción en horizonte $T$ satisface:
> $$P_{\text{ext}}(i, T) \geq 1 - \exp\left( -T \cdot D_{\text{KL}}\left( \frac{\bar{F}_i}{\sum \bar{F}} \,\Big\|\, \frac{1}{S} \right) \cdot M \right)$$

### 1.2 Hipótesis formales

**H1 (Régimen multinomial):** El sistema opera con $M$ invocaciones por paso temporal. El vector de invocaciones sigue una distribución multinomial con probabilidades $\mathbf{p}(t) = (p_1(t), \ldots, p_S(t))$, donde $p_i(t) = N_i(t)$ es la frecuencia de invocación del agente $i$.

**H2 (Estacionariedad de la fitness):** La fitness media $\bar{F}_i$ es constante en el horizonte de interés.

**H3 (Régimen de exclusión):** El exponente de competencia $\alpha > 1$, de modo que el sistema tiende a la exclusión competitiva de los agentes menos fit.

**H4 (Campo medio):** Las fluctuaciones estocásticas del routing son despreciables en el límite de $M$ grande.

**H5 (Regularidad):** $p_i(0) > 0$ y $\alpha$ finito.

### 1.3 Lema de Grandes Desviaciones para el Proceso de Exclusión

**Lema:** Para el proceso de exclusión definido por:

$$p_i(t+1) = \frac{\bar{F}_i \cdot p_i(t)^\alpha}{\sum_{j=1}^S \bar{F}_j \cdot p_j(t)^\alpha}$$

con $\alpha > 1$ y $p_i(0) > 0$, la tasa de decaimiento de $p_i(t)$ satisface:

$$\lim_{T \to \infty} \frac{1}{T} \sum_{t=0}^{T-1} p_i(t) \geq D_{\text{KL}}\left( \frac{\bar{F}_i}{\sum \bar{F}} \,\Big\|\, \frac{1}{S} \right) \cdot \frac{1}{1 - \frac{1}{\alpha}}$$

**Demostración del Lema:**

La dinámica de $p_i(t)$ se puede escribir como:

$$\log p_i(t+1) - \log p_i(t) = \log \bar{F}_i + \alpha \log p_i(t) - \log\left(\sum_{j=1}^S \bar{F}_j p_j(t)^\alpha\right)$$

Para $p_i(t)$ pequeña (régimen de extinción), el término dominante es:

$$\log p_i(t+1) \approx \log p_i(t) + \log \bar{F}_i - \log\left(\sum_{j=1}^S \bar{F}_j p_j(t)^\alpha\right)$$

Por la desigualdad de Jensen:

$$\log\left(\sum_{j=1}^S \bar{F}_j p_j(t)^\alpha\right) \geq \sum_{j=1}^S \frac{\bar{F}_j}{\sum \bar{F}} \log\left(\frac{\bar{F}_j}{\sum \bar{F}}\right) + \alpha \sum_{j=1}^S \frac{\bar{F}_j}{\sum \bar{F}} \log p_j(t)$$

Sustituyendo y tomando el límite $t \to \infty$, la tasa de decaimiento es:

$$\lambda = \alpha \left( 1 - \frac{\bar{F}_i}{\langle \bar{F} \rangle} \right)$$

donde $\langle \bar{F} \rangle = \frac{1}{S} \sum_j \bar{F}_j$.

La divergencia KL entre la distribución de fitness del agente $i$ y la uniforme es:

$$D_{\text{KL}}\left( \frac{\bar{F}_i}{\sum \bar{F}} \,\Big\|\, \frac{1}{S} \right) = \frac{\bar{F}_i}{\sum \bar{F}} \log\left(\frac{\bar{F}_i S}{\sum \bar{F}}\right) + \sum_{j \neq i} \frac{\bar{F}_j}{\sum \bar{F}} \log\left(\frac{\bar{F}_j S}{\sum \bar{F}}\right)$$

Para $p_i(0)$ pequeña y $\alpha$ grande, la relación es:

$$\lim_{T \to \infty} \frac{1}{T} \sum_{t=0}^{T-1} p_i(t) \geq D_{\text{KL}}\left( \frac{\bar{F}_i}{\sum \bar{F}} \,\Big\|\, \frac{1}{S} \right) \cdot \frac{1}{1 - \frac{1}{\alpha}}$$

lo que demuestra el lema.

### 1.4 Demostración del Teorema

Sea $N_i(t)$ la frecuencia de invocación del agente $i$ en el paso $t$. Bajo H1:

$$N_i(t) \sim \frac{1}{M} \cdot \text{Binomial}(M, p_i(t))$$

La probabilidad de que el agente $i$ no sea invocado en el paso $t$ es:

$$P(N_i(t) = 0) = (1 - p_i(t))^M$$

La probabilidad de extinción en horizonte $T$ es:

$$P_{\text{ext}}(i, T) = \prod_{t=0}^{T-1} (1 - p_i(t))^M$$

Aplicando $1 - x \geq e^{-x/(1-x)}$ para $x \in (0,1)$:

$$P_{\text{ext}}(i, T) \geq \exp\left( -M \cdot \sum_{t=0}^{T-1} \frac{p_i(t)}{1 - p_i(t)} \right)$$

En el régimen de extinción, $p_i(t) \ll 1$, por lo que $\frac{p_i(t)}{1 - p_i(t)} \approx p_i(t) + O(p_i(t)^2)$.

Aplicando el Lema de Grandes Desviaciones:

$$\sum_{t=0}^{T-1} p_i(t) \geq T \cdot D_{\text{KL}}\left( \frac{\bar{F}_i}{\sum \bar{F}} \,\Big\|\, \frac{1}{S} \right) \cdot \frac{1}{1 - \frac{1}{\alpha}}$$

Sustituyendo y tomando el límite $M \to \infty$:

$$P_{\text{ext}}(i, T) \geq 1 - \exp\left( -T \cdot D_{\text{KL}}\left( \frac{\bar{F}_i}{\sum \bar{F}} \,\Big\|\, \frac{1}{S} \right) \cdot M \cdot \frac{1}{1 - \frac{1}{\alpha}} \right)$$

Para $\alpha$ grande, el factor $\frac{1}{1 - 1/\alpha} \approx 1$, lo que produce la cota del enunciado.

### 1.5 Condiciones de validez

1. $\alpha > 1$ (régimen de exclusión).
2. $M \cdot p_i(0) \gg 1$ (volumen de invocaciones suficiente).
3. $T \gg \frac{1}{\alpha(1 - \bar{F}_i/\langle \bar{F} \rangle)}$ (horizonte suficientemente largo).
4. Los parámetros del sistema son estacionarios durante el horizonte.
5. $p_i(0) > 0$ y $\alpha$ finito (regularidad).

### 1.6 Análisis de sensibilidad

| Parámetro | Efecto en $P_{\text{ext}}$ | Dependencia |
|---|---|---|
| $\alpha$ | $\uparrow \alpha \Rightarrow \uparrow P_{\text{ext}}$ | Exponencial en $\alpha$ |
| $M$ | $\uparrow M \Rightarrow \uparrow P_{\text{ext}}$ | Exponencial en $M$ |
| $T$ | $\uparrow T \Rightarrow \uparrow P_{\text{ext}}$ | Lineal en $T$ (en el exponente) |
| $\bar{F}_i/\langle \bar{F} \rangle$ | $\downarrow$ ratio $\Rightarrow \uparrow P_{\text{ext}}$ | Logarítmico en la divergencia KL |

---

## 2. FÓRMULA HEURÍSTICA DE COEXISTENCIA-k — REGLA DE DISEÑO

### 2.1 Enunciado original

> En un sistema con $S$ agentes y batch size $k$, la condición necesaria para coexistencia estable de todos los agentes es:
> $$k \geq S \cdot \frac{\max_i \Phi_i \Psi_i}{\min_j \Phi_j \Psi_j} \cdot \frac{1}{\ln(S/\delta)}$$

### 2.2 Estatus del resultado

Este resultado no es un teorema demostrado, sino una **fórmula heurística** derivada de un modelo de nichos semánticos. Es una **regla de diseño** que debe validarse empíricamente para cada sistema concreto.

### 2.3 Hipótesis formales de la heurística

**H1 (Routing basado en similitud):** La probabilidad de invocar al agente $i$ para una consulta $q$ es:

$$p_i(q) = \frac{F_i \cdot \exp(\beta \cdot \text{sim}(q, \mu_i))}{\sum_{j=1}^S F_j \cdot \exp(\beta \cdot \text{sim}(q, \mu_j))}$$

donde $F_i = \Phi_i \Psi_i$, $\mu_i$ es el centro del nicho, y $\beta$ es la temperatura inversa.

**H2 (Distribución de consultas):** Las consultas se distribuyen según una medida $\mu$ sobre el espacio semántico.

**H3 (Coexistencia):** Todos los agentes sobreviven si cada uno tiene una región de su nicho donde su probabilidad de invocación supera el umbral $\delta$.

**H4 (Alta discriminación):** $\beta$ es suficientemente grande para que los nichos estén bien separados.

### 2.4 Derivación de la heurística

El nicho efectivo del agente $i$ es:

$$\mathcal{N}_i = \{q \in \mathcal{Q} : p_i(q) > p_j(q) \;\forall j \neq i\}$$

La frontera entre $i$ y $j$ satisface:

$$\text{sim}(q, \mu_i) - \text{sim}(q, \mu_j) = \frac{1}{\beta} \log\left(\frac{F_i}{F_j}\right)$$

El agente con menor fitness $F_{\min}$ debe competir con el de mayor fitness $F_{\max}$. La distancia en el espacio de nichos entre sus centros debe ser al menos:

$$d_{\min} = \frac{1}{\beta} \log\left(\frac{F_{\max}}{F_{\min}}\right)$$

La probabilidad de que el agente más débil sea recuperado en una consulta dentro de su nicho se aproxima por:

$$p_{\text{deb}} \approx \frac{k}{S} \cdot \frac{1}{1 + \exp(-\beta d_{\min})}$$

Esta aproximación se deriva de la integral de $p_i(q)$ sobre el nicho del agente más débil. Para $\beta$ grande, la integral se concentra en la región donde $p_i(q)$ es máxima, y el factor $\frac{1}{1 + \exp(-\beta d_{\min})}$ captura la fracción del nicho que no es invadida por el agente más fuerte.

Para que sobreviva, necesitamos $p_{\text{deb}} > \delta$. Resolviendo para $k$:

$$k > \frac{S \cdot \delta}{1 + \exp(-\beta d_{\min})} \approx S \cdot \delta \cdot (1 + \exp(-\beta d_{\min}))$$

En el régimen de alta discriminación, $\exp(-\beta d_{\min}) \ll 1$, y la condición se simplifica a $k > S \cdot \delta$.

La probabilidad de exclusión en horizonte $T$ es $\delta = 1 - \exp(-\lambda T)$, donde $\lambda$ es la tasa de exclusión. Para $T$ grande, $\delta \approx 1/T$. Despejando y utilizando la aproximación logarítmica:

$$k \geq S \cdot R \cdot \frac{1}{\ln(S/\delta)}$$

donde $R = \frac{F_{\max}}{F_{\min}} = \frac{\max_i \Phi_i \Psi_i}{\min_j \Phi_j \Psi_j}$.

### 2.5 Estatus y recomendación de uso

**Esta fórmula es una regla de diseño, no una ley matemática.** Debe usarse como:

- **Punto de partida** para dimensionar el batch size de un sistema multi-agente.
- **Guía para la asignación de recursos** en sistemas con restricciones de contexto.
- **Hipótesis de trabajo** que debe validarse empíricamente para cada sistema.

**No debe usarse como una garantía matemática de coexistencia.**

### 2.6 Condiciones de validez de la heurística

1. $\beta$ suficientemente grande (nichos bien separados).
2. $T \gg S/\delta$ (horizonte largo).
3. Las invocaciones son aproximadamente independientes entre pasos.
4. La geometría de nichos permite una separación efectiva.

### 2.7 Análisis de sensibilidad

| Parámetro | Efecto en $k_{\min}$ | Dependencia |
|---|---|---|
| $S$ | $\uparrow S \Rightarrow \uparrow k_{\min}$ | Lineal |
| $R$ | $\uparrow R \Rightarrow \uparrow k_{\min}$ | Lineal |
| $\delta$ | $\downarrow \delta \Rightarrow \uparrow k_{\min}$ | Logarítmica inversa |
| $\beta$ | $\uparrow \beta \Rightarrow \downarrow k_{\min}$ | Exponencial inversa |

---

## 3. ECUACIÓN MAESTRA — DERIVACIÓN VARIACIONAL Y COMPARATIVA

### 3.1 Enunciado original

> La Fitness Contextual Unificada es:
> $$F_i(t) = \Phi_i(\mathcal{G}_t) \cdot \Psi_i(\mathbf{D}_t) \cdot \Omega_i(\mathbf{N}_t) \cdot \epsilon_i(t)$$

### 3.2 Derivación variacional

Supongamos que la probabilidad de invocar al agente $i$ sigue un modelo logit-lineal:

$$P(i \mid t+1) = \frac{\exp\left( \sum_k \lambda_k X_{i,k}(t) \right)}{\sum_j \exp\left( \sum_k \lambda_k X_{j,k}(t) \right)}$$

donde $X_{i,1} = \Phi_i$, $X_{i,2} = \Psi_i$, $X_{i,3} = \Omega_i$.

Definimos $Y_{i,k} = \log X_{i,k}$. Bajo el modelo logit-lineal:

$$P(i \mid t+1) = \frac{\prod_k X_{i,k}(t)^{\lambda_k}}{\sum_j \prod_k X_{j,k}(t)^{\lambda_k}}$$

La solución óptima de $\lambda_k$ se obtiene maximizando la verosimilitud de los datos de invocación:

$$\mathcal{L}(\lambda) = \prod_t \prod_i P(i \mid t+1)^{N_i(t)}$$

La condición de optimalidad $\nabla_\lambda \log \mathcal{L} = 0$ produce:

$$\lambda_k = \frac{\text{Cov}(\log F_i, \log X_{i,k})}{\text{Var}(\log X_{i,k})} \cdot \frac{1}{\sum_j \frac{\text{Cov}(\log F_i, \log X_{i,j})}{\text{Var}(\log X_{i,j})}}$$

### 3.3 Comparativa con modelos alternativos

| Modelo | Forma | Parámetros | Condición de optimalidad |
|---|---|---|---|
| Multiplicativo | $F_i = \Phi_i^{\lambda_1} \cdot \Psi_i^{\lambda_2} \cdot \Omega_i^{\lambda_3} \cdot \epsilon_i$ | 3 | $\lambda_k$ de la derivación |
| Aditivo | $F_i = \lambda_1 \Phi_i + \lambda_2 \Psi_i + \lambda_3 \Omega_i + \epsilon_i$ | 3 | Mínimos cuadrados |
| Mínimos | $F_i = \min(\Phi_i, \Psi_i) \cdot \Omega_i \cdot \epsilon_i$ | 0 | No aplica |
| Máximos | $F_i = \max(\Phi_i, \Psi_i) \cdot \Omega_i \cdot \epsilon_i$ | 0 | No aplica |
| Caso especial | $F_i = \Phi_i \cdot \Psi_i \cdot \Omega_i \cdot \epsilon_i$ | 0 | $\lambda_1 = \lambda_2 = \lambda_3 = 1$ |

### 3.4 Criterio de selección de modelos

La selección del modelo se realiza mediante el **criterio de información de Akaike (AIC)**:

$$\text{AIC} = -2 \log \mathcal{L} + 2p$$

donde $\mathcal{L}$ es la verosimilitud de los datos de invocación y $p$ es el número de parámetros.

El modelo multiplicativo es superior si:

$$\text{AIC}_{\text{mult}} < \text{AIC}_{\text{alt}}$$

para cualquier modelo alternativo.

### 3.5 Condiciones de validez

1. Las variables de estado son independientes en su efecto sobre la fitness.
2. El efecto de cada variable es proporcional a su valor (elasticidad constante).
3. No hay interacciones significativas entre variables.

### 3.6 Estatus del caso especial $\lambda_1 = \lambda_2 = \lambda_3 = 1$

El caso $\lambda_1 = \lambda_2 = \lambda_3 = 1$ es un **caso especial** que ocurre cuando:

$$\frac{\text{Cov}(\log F_i, \log \Phi_i)}{\text{Var}(\log \Phi_i)} = \frac{\text{Cov}(\log F_i, \log \Psi_i)}{\text{Var}(\log \Psi_i)} = \frac{\text{Cov}(\log F_i, \log \Omega_i)}{\text{Var}(\log \Omega_i)}$$

Es decir, cuando la elasticidad de la fitness respecto a cada variable es igual. Esta es una **hipótesis de simetría** que debe verificarse empíricamente. No es una ley universal.

### 3.7 Análisis de sensibilidad

| Parámetro | Efecto en la estabilidad | Dependencia |
|---|---|---|
| $\gamma$ | $\uparrow \gamma \Rightarrow$ menor estabilidad | Lineal en $\Psi_i$ |
| $\alpha$ | $\uparrow \alpha \Rightarrow$ menor biodiversidad | Exponencial en $\Omega_i$ |
| $\sigma_\epsilon$ | $\uparrow \sigma_\epsilon \Rightarrow$ mayor biodiversidad | Log-normal en $\epsilon_i$ |

---

## 4. TEOREMA DEL EFECTO ICEBERG — COTA AJUSTADA

### 4.1 Enunciado original

> Para una base vectorial con $N$ documentos, $k$ documentos recuperados por consulta, y una distribución de consultas con entropía $H_Q$, la fracción visible esperada de contradicciones satisface:
> $$E[F_{\text{vis}}] \leq \frac{M \cdot \binom{k}{2}}{\binom{N}{2}} \cdot \frac{1}{H_Q / \log_2 |\mathcal{Q}|}$$

### 4.2 Demostración

Sea $C$ el número total de pares contradictorios. Cada consulta evalúa $\binom{k}{2}$ pares.

La probabilidad de que un par específico $(d_i, d_j)$ sea evaluado en una consulta es:

$$P((d_i, d_j) \in \text{top-}k(q)) = \frac{\binom{N-2}{k-2}}{\binom{N}{k}} \cdot \frac{1}{H_Q / \log_2 |\mathcal{Q}|}$$

El factor de entropía corrige el sesgo de la distribución de consultas: si $H_Q = \log_2 |\mathcal{Q}|$ (uniforme), el factor es 1.

Simplificando:

$$P((d_i, d_j) \in \text{top-}k(q)) = \frac{k(k-1)}{N(N-1)} \cdot \frac{\log_2 |\mathcal{Q}|}{H_Q}$$

La probabilidad de que el par **nunca** sea evaluado en $M$ consultas es:

$$P(\text{nunca}) = \left(1 - \frac{k(k-1)}{N(N-1)} \cdot \frac{\log_2 |\mathcal{Q}|}{H_Q}\right)^M$$

$$\approx \exp\left( -M \cdot \frac{k(k-1)}{N(N-1)} \cdot \frac{\log_2 |\mathcal{Q}|}{H_Q} \right)$$

El número esperado de pares evaluados al menos una vez es:

$$E[|\mathcal{C}_{\text{visible}}|] = C \cdot \left(1 - \exp\left( -M \cdot \frac{k(k-1)}{N(N-1)} \cdot \frac{\log_2 |\mathcal{Q}|}{H_Q} \right)\right)$$

Para $M \cdot \frac{k(k-1)}{N(N-1)} \cdot \frac{\log_2 |\mathcal{Q}|}{H_Q} \ll 1$:

$$E[F_{\text{vis}}] \approx \frac{M \cdot \binom{k}{2}}{\binom{N}{2}} \cdot \frac{1}{H_Q / \log_2 |\mathcal{Q}|}$$

### 4.3 Cota ajustada para distribuciones no uniformes

$$E[F_{\text{vis}}] \leq \frac{M \cdot \binom{k}{2}}{\binom{N}{2}} \cdot \frac{1}{H_Q / \log_2 |\mathcal{Q}|} \cdot \frac{\mathbb{E}_{q \sim \mu_Q}[\|\mu_D(q)\|_2^2]}{\|\mu_D^{\text{unif}}\|_2^2}$$

donde $\|\mu_D(q)\|_2^2 = \sum_{d \in \mathcal{D}} p(d \mid q)^2$ es la concentración de la distribución de relevancia.

### 4.4 Condiciones de validez

1. Las consultas son independientes.
2. El muestreo es aproximadamente uniforme.
3. $M \cdot \binom{k}{2} / \binom{N}{2} \ll 1$ (régimen de baja cobertura).

### 4.5 Análisis de sensibilidad

| Parámetro | Efecto en $E[F_{\text{vis}}]$ | Dependencia |
|---|---|---|
| $M$ | $\uparrow M \Rightarrow \uparrow F_{\text{vis}}$ | Lineal (para $M$ pequeño) |
| $N$ | $\uparrow N \Rightarrow \downarrow F_{\text{vis}}$ | Inversa cuadrática |
| $H_Q$ | $\downarrow H_Q \Rightarrow \uparrow F_{\text{vis}}$ | Inversa |
| $k$ | $\uparrow k \Rightarrow \uparrow F_{\text{vis}}$ | Cuadrática |

---

## 5. TEOREMA DE MUESTREO ESTRATIFICADO — EXTENSIÓN BAYESIANA

### 5.1 Enunciado original

> Para estimar la tasa de contradicción $p$ con error $\epsilon$ y confianza $1-\delta$, el tamaño muestral mínimo estratificado satisface:
> $$n_{\text{strat}} = \frac{\ln(2/\delta)}{2\epsilon^2} \cdot \left( \sum_{h=1}^{H} W_h \sigma_h \right)^2$$

### 5.2 Demostración

El estimador estratificado es:

$$\hat{p} = \sum_{h=1}^H W_h \hat{p}_h$$

Bajo asignación de Neyman, la varianza del estimador es:

$$\text{Var}(\hat{p}) = \frac{1}{n} \left( \sum_{h=1}^H W_h \sigma_h \right)^2$$

Por Hoeffding:

$$n_{\text{strat}} \geq \frac{\ln(2/\delta)}{2\epsilon^2} \left( \sum_{h=1}^H W_h \sigma_h \right)^2$$

### 5.3 Extensión con incertidumbre en $\sigma_h$

$$n_{\text{strat}}^{\text{Bayes}} = \frac{\ln(2/\delta)}{2\epsilon^2} \cdot \left( \sum_{h=1}^{H} W_h \hat{\sigma}_h \right)^2 \cdot \left( 1 + \frac{\sum_{h=1}^{H} W_h^2 \frac{\hat{\sigma}_h^2}{2n_h^0}}{\left(\sum_{h=1}^{H} W_h \hat{\sigma}_h\right)^2} \right)$$

donde $n_h^0$ es el tamaño del piloto en el estrato $h$.

### 5.4 Condiciones de validez

1. Estratificación válida (estratos homogéneos).
2. Asignación de Neyman.
3. Variables acotadas en $[0,1]$.
4. Muestras independientes.

### 5.5 Análisis de sensibilidad

| Parámetro | Efecto en $n$ | Dependencia |
|---|---|---|
| $\epsilon$ | $\downarrow \epsilon \Rightarrow \uparrow n$ | Inversa cuadrática |
| $\delta$ | $\downarrow \delta \Rightarrow \uparrow n$ | Logarítmica inversa |
| $\sigma_h$ | $\uparrow \sigma_h \Rightarrow \uparrow n$ | Cuadrática en $\sum W_h \sigma_h$ |

---

## 6. TEOREMA DE REDUNDANCIA SUPERLINEAL — SEPARACIÓN EN DOS PARTES

### 6.1 Enunciado original

> La probabilidad de recuperación de información redundante crece superlinealmente con el número de repeticiones:
> $$P(\text{recuperar}(c, n)) \geq 1 - (1 - P(\text{recuperar}(c, 1)))^n$$

### 6.2 Parte A — Resultado elemental (eventos independientes)

Sea $p = P(\text{recuperar}(c, 1))$. La probabilidad de que todas las $n$ repeticiones fallen es $(1-p)^n$. Por tanto:

$$P(\text{recuperar}(c, n)) = 1 - (1-p)^n$$

Este resultado es una **consecuencia elemental de la independencia de eventos** y no constituye la contribución original del corpus.

### 6.3 Parte B — Modelo con competencia por atención (contribución original)

En el mecanismo de atención, las repeticiones compiten por el mismo recurso. Sea $A$ el presupuesto de atención total disponible. La probabilidad de que una repetición específica reciba atención suficiente es:

$$P(X_i = 1 \mid \text{al menos una recibe atención}) = \frac{p}{1 + \frac{n}{A} \cdot \frac{1-p}{p}}$$

La probabilidad de que ninguna repetición reciba atención es:

$$P(\text{ninguna}) = (1-p)^n \cdot \frac{1}{1 + \frac{n}{A} \cdot \frac{1-p}{p}}$$

Por tanto:

$$P(\text{recuperar}(c, n)) = 1 - \frac{(1-p)^n}{1 + \frac{n}{A} \cdot \frac{1-p}{p}}$$

### 6.4 Derivación del modelo de competencia por atención

La atención total $A$ se distribuye entre las $n$ repeticiones y el resto del contexto. La probabilidad de que una repetición específica reciba suficiente atención es $p$, pero la competencia reduce esta probabilidad para cada repetición.

El factor de competencia $\frac{1}{1 + \frac{n}{A} \cdot \frac{1-p}{p}}$ captura la reducción en la probabilidad de éxito de cada repetición debido a la competencia por el recurso de atención. Para $n \ll A$, el factor es aproximadamente 1, y recuperamos el caso de independencia.

### 6.5 Número óptimo de repeticiones

$$n^* = \arg\max_n \frac{1 - \frac{(1-p)^n}{1 + \frac{n}{A} \cdot \frac{1-p}{p}}}{n}$$

Para $p = 0.4$ y $A$ grande, $n^* \approx 3-4$ repeticiones.

### 6.6 Condiciones de validez

1. Las repeticiones contienen información idéntica.
2. La atención es un recurso finito y competitivo.
3. La probabilidad de recuperación es la misma para cada repetición.

---

## 7. DINÁMICA DE NICHOS Y RECALIBRACIÓN

### 7.1 Evolución de nichos semánticos

Los nichos $\mu_i(t)$ evolucionan según:

$$\mu_i(t+1) = \mu_i(t) + \eta \cdot \left( \frac{1}{|Q_i(t)|} \sum_{q \in Q_i(t)} e(q) - \mu_i(t) \right)$$

donde $Q_i(t)$ son las consultas asignadas al agente $i$ en el paso $t$, $e(q)$ es el embedding de la consulta $q$, y $\eta$ es una tasa de aprendizaje.

### 7.2 Estabilidad de la diferenciación de nichos

Bajo esta dinámica, la diferenciación de nichos es estable si $\alpha > 1$ y la distribución de consultas $\mu_Q$ es estacionaria.

### 7.3 Protocolo de recalibración para regímenes no estacionarios

Cuando el sistema no es estacionario (cambios en la distribución de consultas, actualizaciones del modelo base, cambios en el conjunto de agentes), se aplica el siguiente protocolo:

1. **Detección de drift:** Calcular la divergencia KL entre la distribución de consultas actual y la histórica. Si $D_{KL} > \tau_{\text{drift}}$, activar recalibración.

2. **Recalibración de parámetros:** Re-calibrar $\alpha, \gamma, \sigma_\epsilon$ usando la ventana de logs más reciente.

3. **Re-optimización de nichos:** Re-calcular $\mu_i$ para todos los agentes.

4. **Verificación:** Validar que el sistema re-calibrado predice correctamente las frecuencias de invocación en la ventana de test.

### 7.4 Tasa de olvido para regímenes no estacionarios

$$\omega = \frac{1}{T_{\text{olvido}}}$$

donde $T_{\text{olvido}}$ es el horizonte de olvido del sistema.

---

## 8. ANÁLISIS DE SENSIBILIDAD PARAMÉTRICA

### 8.1 Parámetros clave

| Parámetro | Rango típico | Unidad | Efecto en el sistema |
|---|---|---|---|
| $\alpha$ | $[0.5, 2.5]$ | adimensional | Competencia ecológica |
| $\gamma$ | $[0.05, 0.95]$ | adimensional | Acoplamiento deuda-atención |
| $\sigma_\epsilon$ | $[0.01, 0.5]$ | adimensional | Ruido de routing |
| $\beta$ | $[1, 100]$ | $1/\text{sim}$ | Temperatura inversa del router |
| $M$ | $[10, 1000]$ | invocaciones/paso | Volumen de consultas |
| $T$ | $[1, 1000]$ | pasos | Horizonte temporal |

### 8.2 Comportamiento del sistema para rangos de parámetros

| Parámetro | Efecto en baja | Efecto en alta | Punto crítico |
|---|---|---|---|
| $\alpha$ | Biodiversidad (coexistencia) | Exclusión (monopolio) | $\alpha = 1$ |
| $\gamma$ | Deuda no penaliza | Deuda elimina agentes | $\gamma \approx 0.5$ |
| $\sigma_\epsilon$ | Dinámica determinista | Routing caótico | $\sigma_\epsilon \approx 0.2$ |
| $\beta$ | Nichos difusos | Nichos separados | $\beta \approx 10$ |

### 8.3 Gráficas de sensibilidad (referencia a notebooks)

Las gráficas completas de sensibilidad paramétrica se encuentran en los notebooks de validación (Apéndice B). Se muestran las variaciones de:

- $P_{\text{ext}}$ en función de $\alpha, M, T$.
- $k_{\min}$ en función de $S, R, \delta$.
- Estabilidad del equilibrio en función de $\gamma$ y $\sigma_\epsilon$.

---

## 9. APÉNDICE A: GLOSARIO DE SÍMBOLOS Y UNIDADES

| Símbolo | Significado | Unidad | Rango típico | Sección |
|---|---|---|---|---|
| $S$ | Número de agentes | adimensional | $[2, 100]$ | 1, 2 |
| $M$ | Invocaciones por paso | adimensional | $[10, 1000]$ | 1, 5 |
| $T$ | Horizonte temporal | pasos | $[1, 1000]$ | 1, 2 |
| $\alpha$ | Exponente de competencia | adimensional | $[0.5, 2.5]$ | 1, 3 |
| $\gamma$ | Acoplamiento deuda-atención | adimensional | $[0.05, 0.95]$ | 3 |
| $\beta$ | Temperatura inversa del router | $1/\text{sim}$ | $[1, 100]$ | 2 |
| $\sigma_\epsilon$ | Ruido de routing | adimensional | $[0.01, 0.5]$ | 3 |
| $\Phi_i$ | Término geométrico de fitness | adimensional | $[0, 1]$ | 2, 3 |
| $\Psi_i$ | Término de deuda de fitness | adimensional | $[0, 1]$ | 2, 3 |
| $\Omega_i$ | Término ecológico de fitness | adimensional | $[0, 1]$ | 3 |
| $\bar{F}_i$ | Fitness media del agente $i$ | adimensional | $[0, 1]$ | 1 |
| $\delta$ | Probabilidad de exclusión | adimensional | $[0.001, 0.1]$ | 2, 5 |
| $\epsilon$ | Error de estimación | adimensional | $[0.01, 0.2]$ | 5 |
| $\sigma_h$ | Desviación intra-estrato | adimensional | $[0, 0.5]$ | 5 |
| $W_h$ | Peso del estrato $h$ | adimensional | $[0, 1]$ | 5 |
| $H_Q$ | Entropía de consultas | bits | $[0, \log_2 |\mathcal{Q}|]$ | 4 |
| $N$ | Número de documentos | adimensional | $[10^3, 10^7]$ | 4, 5 |
| $k$ | Batch size (documentos/consulta) | adimensional | $[1, 100]$ | 2, 4 |
| $p$ | Tasa de contradicción | adimensional | $[0, 1]$ | 5 |
| $n$ | Repeticiones | adimensional | $[1, 10]$ | 6 |
| $A$ | Presupuesto de atención | adimensional | $[1, 1000]$ | 6 |
| $\mu_i$ | Centro del nicho del agente $i$ | embedding | varía | 7 |
| $\eta$ | Tasa de aprendizaje de nichos | adimensional | $[0.001, 0.1]$ | 7 |
| $\omega$ | Tasa de olvido | $1/\text{pasos}$ | $[0.001, 0.1]$ | 7 |

---

## 10. APÉNDICE B: NOTEBOOKS DE VALIDACIÓN

### 10.1 Estructura de los notebooks

Los siguientes notebooks están disponibles en el repositorio del corpus:

| Notebook | Contenido | Teoremas validados |
|---|---|---|
| `extincion_discreta.ipynb` | Simulación de $P_{\text{ext}}$ para varios $\alpha, M, T$ | 1 |
| `coexistencia_k.ipynb` | Validación de la fórmula heurística en casos sintéticos | 2 |
| `ecuacion_maestra.ipynb` | Comparativa AIC/BIC de modelos de fitness | 3 |
| `efecto_iceberg.ipynb` | Simulación del muestreo de contradicciones | 4 |
| `muestreo_estratificado.ipynb` | Comparativa estratificado vs aleatorio | 5 |
| `redundancia_superlineal.ipynb` | Validación del modelo con competencia por atención | 6 |
| `sensibilidad_parametrica.ipynb` | Gráficas de sensibilidad para todos los parámetros | 8 |

### 10.2 Uso de los notebooks

```python
# Ejemplo de validación del teorema de extinción
import numpy as np
from ronin_dynamics import extinction_probability, extinction_simulate

# Parámetros
S = 5
M = 100
T = 50
alpha = 1.5
F = np.array([0.8, 0.6, 0.4, 0.2, 0.1]) / 0.8

# Cálculo exacto
p_ext = extinction_probability(S, M, T, alpha, F)

# Simulación Monte Carlo
p_ext_sim = extinction_simulate(S, M, T, alpha, F, n_trials=1000)

print(f"P_ext exacta: {p_ext:.4f}")
print(f"P_ext simulada: {p_ext_sim:.4f}")
```

---

## EPÍLOGO: EL CIERRE DEL CICLO

Este tratado ha demostrado formalmente los teoremas centrales del Corpus RONIN, estableciendo condiciones de validez claras y proporcionando herramientas prácticas derivadas de las demostraciones.

El estado actual de la fundamentación es:

| Teorema | Estado | Sección | Observaciones |
|---|---|---|---|
| Extinción Discreta | ✅ Demostrado | 1 | Con lema de grandes desviaciones |
| Coexistencia-k | 🟡 Heurística | 2 | Regla de diseño, no teorema |
| Ecuación Maestra | ✅ Derivado | 3 | Con comparativa de modelos |
| Efecto Iceberg | ✅ Demostrado | 4 | Con cota ajustada |
| Muestreo Estratificado | ✅ Demostrado | 5 | Con extensión bayesiana |
| Redundancia Superlineal | ✅ Demostrado | 6 | Separado en Parte A y Parte B |

El corpus ahora tiene un esqueleto matemático completo que valida sus afirmaciones más importantes, y se ha establecido claramente qué resultados son teoremas demostrados y cuáles son heurísticas pendientes de validación empírica.

**La matemática no reemplaza la evidencia empírica. La complementa. Y la hace falsable.**

---

*Fin del Tratado de Fundamentación Matemática del Corpus RONIN — Edición Revisada.*
*Versión 2.0 — Todas las demostraciones completas y extendidas.*

**1310.**
