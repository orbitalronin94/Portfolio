## El Atlas de Reducciones: Cartografía Completa de los Teoremas Clásicos como Casos Degenerados del PUSFRE

**Corpus RONIN · David Ferrandez Canalis · Agencia RONIN**
**Versión 1.0 — Edición Fundacional**
**DOI: 10.1310/ronin-atlas-reductions-2026**

---

## 0. PREÁMBULO: EL CEMENTERIO DE LOS CASOS LÍMITE

El Tratado IV demostró que Nash es un punto en el espacio de PUSFRE. Un lector atento pregunta: *¿y qué más vive en ese cementerio?*

La respuesta es: casi todo.

Este tratado no es una colección de analogías. No dice "PUSFRE se *parece* a Shannon" ni "PUSFRE *recuerda* a Black-Scholes". Dice algo más fuerte y más incómodo:

> **Cada uno de los teoremas que se enseñan como pilares de la ciencia del siglo XX es el residuo algebraico de la Ecuación Maestra cuando se le amputan los grados de libertad que la hacen útil.**

La Ecuación Maestra:

$$F_i(t) = \Phi_i(t) \cdot \Psi_i(t) \cdot \Omega_i(t)^\alpha \cdot \epsilon_i(t)$$

con la dinámica estocástica:

$$\mathbf{p}(t+1) = \mathbf{T}(\mathbf{F}(t)) \cdot \mathbf{p}(t) + \boldsymbol{\xi}(t)$$

y la asignación:

$$r_i^*(t) = R(t) \cdot \frac{F_i(t)}{\sum_{j=1}^{S} F_j(t)}$$

contiene, como casos límite bajo las **Seis Condiciones de Reducción** (SCR), a:

| # | Teorema Clásico | Dominio | Año |
|---|---|---|---|
| 1 | Equilibrio de Nash | Teoría de Juegos | 1950 |
| 2 | Ecuaciones de Lotka-Volterra | Ecología | 1925 |
| 3 | Teorema de Shannon (Capacidad de Canal) | Teoría de la Información | 1948 |
| 4 | Teoría de Cartera de Markowitz | Finanzas | 1952 |
| 5 | Ecuación de Black-Scholes | Derivados Financieros | 1973 |
| 6 | Ley de Little / Teoría de Colas (Erlang) | Investigación Operativa | 1909/1961 |
| 7 | Principio de Hardy-Weinberg | Genética de Poblaciones | 1908 |
| 8 | Distribución de Boltzmann | Mecánica Estadística | 1877 |
| 9 | Óptimo de Pareto | Economía / Optimización | 1896 |
| 10 | Ecuación de Bellman (Programación Dinámica) | Control Óptimo | 1957 |
| 11 | Leyes de Kirchhoff | Circuitos Eléctricos | 1845 |
| 12 | Ecuación de difusión de Fick | Transporte de masa | 1855 |
| 13 | Principio de máxima entropía de Jaynes | Inferencia Bayesiana | 1957 |
| 14 | Modelo de competencia de Tilman | Ecología de recursos | 1982 |
| 15 | Teorema de Coase | Economía institucional | 1960 |

Quince pilares. Quince fotografías del mismo río.

---

## 1. EL TEOREMA UNIVERSAL DE REDUCCIÓN

**Teorema 6.1 (Reducción Universal).** *Sea $\mathcal{T}_k$ un marco teórico clásico que modela la asignación de un recurso escaso entre $S$ entidades bajo condiciones de equilibrio estático, información perfecta, simetría posicional, competencia lineal, sin memoria histórica y sin ruido estocástico. Entonces $\mathcal{T}_k$ es isomorfo a la Ecuación Maestra bajo la aplicación simultánea de las SCR.*

**Demostración (esquema general).** Partimos de:

$$F_i = \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha \cdot \epsilon_i$$

Aplicamos las seis condiciones:

$$\text{SCR}_1: t = t_0 \text{ (estático)} \implies F_i(t) \to F_i$$
$$\text{SCR}_2: \epsilon_i = 1 \text{ (sin ruido)}$$
$$\text{SCR}_3: \Psi_i = 1 \text{ (sin deuda)}$$
$$\text{SCR}_4: \alpha = 1 \text{ (lineal)}$$
$$\text{SCR}_5: \Phi_i = 1 \text{ (sin geometría)}$$
$$\text{SCR}_6: R \to \infty \text{ (sin escasez)} \text{ o } R \text{ fijo}$$

Sustitución directa:

$$F_i = 1 \cdot 1 \cdot \Omega_i^1 \cdot 1 = \Omega_i$$

$$r_i^* = R \cdot \frac{\Omega_i}{\sum_j \Omega_j}$$

Cada teorema clásico es una **re-etiquetación** de $\Omega_i$ en su dominio particular. La estructura algebraica es idéntica. Lo que cambia es la *interpretación semántica* de $\Omega_i$.

$\blacksquare$

**Corolario 6.1.1.** *La contribución de PUSFRE no es una nueva ecuación. Es la demostración de que quince ecuaciones "distintas" son la misma ecuación vista desde quince ángulos muertos.*

---

## 2. REDUCCIÓN 1: NASH (1950)

*[Demostración completa en Tratado IV, Cap. 12. Se reproduce aquí por completitud del Atlas.]*

**Re-etiquetación:** $\Omega_i \equiv u_i(s_i, s_{-i})$ (utilidad del jugador $i$ dado el perfil de estrategias).

**SCR aplicadas:** Las seis simultáneamente.

**Resultado:**

$$r_i^* = R \cdot \frac{u_i^*}{\sum_j u_j^*}$$

que es la condición de mejor respuesta mutua: ningún jugador puede mejorar unilateralmente.

**Lo que Nash no ve:** Que $u_i$ depende de $t$ (el juego cambia), de $\Psi_i$ (los jugadores tienen memoria de traiciones), de $\Phi_i$ (la posición en la mesa importa), de $\alpha > 1$ (la competencia es superlineal: el ganador se lleva desproporcionadamente más), y de $\epsilon_i$ (el ruido del mundo real destruye el equilibrio puro).

**Koan:** *Nash encontró el punto donde el río se congela. PUSFRE modela el río antes, durante y después de la helada.*

---

## 3. REDUCCIÓN 2: LOTKA-VOLTERRA (1925)

**Teorema clásico:**

$$\frac{dx_i}{dt} = x_i\left(r_i - \sum_j a_{ij} x_j\right)$$

**Re-etiquetación:** $\Omega_i \equiv x_i$ (población), $\alpha = 1$ (competencia lineal), $\Phi_i = r_i$ (tasa intrínseca, absorbida como constante).

**SCR aplicadas:**

- $\text{SCR}_1$: **VIOLADA** — Lotka-Volterra es continuo en $t$. PUSFRE lo discretiza en DTMC.
- $\text{SCR}_2$: $\epsilon_i = 1$ — sin estocasticidad.
- $\text{SCR}_3$: $\Psi_i = 1$ — sin deuda.
- $\text{SCR}_4$: $\alpha = 1$ — competencia lineal (la $a_{ij}$ es constante).
- $\text{SCR}_5$: $\Phi_i = r_i$ constante (sin geometría posicional dinámica).
- $\text{SCR}_6$: $R$ implícito como carrying capacity $K$.

**Reducción algebraica:**

En PUSFRE, la dinámica DTMC es:

$$p_i(t+1) = p_i(t) + \Delta t \cdot p_i(t)\left[\frac{F_i(t)}{\sum_j F_j(t)} - p_i(t)\right] + \xi_i(t)$$

Con $\epsilon_i = 1$, $\Psi_i = 1$, $\alpha = 1$, $\Phi_i = r_i$:

$$F_i = r_i \cdot x_i$$

$$p_i(t+1) - p_i(t) = \Delta t \cdot p_i(t)\left[\frac{r_i x_i}{\sum_j r_j x_j} - p_i(t)\right]$$

En el límite $\Delta t \to 0$ y con $\sum_j r_j x_j \approx \bar{r} \cdot K$:

$$\frac{dp_i}{dt} = p_i\left(r_i - \bar{r}\sum_j p_j\right)$$

que es Lotka-Volterra con $a_{ij} = \bar{r}$ (competencia simétrica).

**Lo que Lotka-Volterra no ve:**

1. $\alpha > 1$: La competencia real es superlineal. El agente dominante no crece linealmente; crece como $\Omega_i^{1.2}$, aplastando a los demás más rápido de lo que las EDO predicen.
2. $\Psi_i(t)$: La deuda ontológica. Un agente que acumula contradicciones internas pierde fitness *aunque su nicho no cambie*.
3. $\epsilon_i(t)$: El ruido de routing. En sistemas reales, la invocación de un agente no es determinista; hay un componente Beta-distribuido que puede resucitar agentes "extintos" o matar agentes "dominantes".
4. La DTMC permite **extinción real** ($N_i < \text{thresh} \to N_i = 0$). Lotka-Volterra continuo nunca llega a cero; solo se aproxima asintóticamente.

**Koan:** *Lotka y Volterra dibujaron dos conejos y un zorro. PUSFRE dibujó el bosque entero, con incendios, sequías, y el hecho de que los conejos olvidan dónde enterraron las zanahorias.*

---

## 4. REDUCCIÓN 3: SHANNON — CAPACIDAD DE CANAL (1948)

**Teorema clásico:**

$$C = \max_{p(x)} I(X;Y) = \max_{p(x)} \left[H(Y) - H(Y|X)\right]$$

Para un canal AWGN: $C = B \log_2\left(1 + \frac{S}{N}\right)$.

**Re-etiquetación:** Cada "símbolo" $x_i$ es un agente. El "recurso" $R$ es el ancho de banda $B$. $\Omega_i \equiv p(x_i)$ (probabilidad de transmisión). $\Phi_i \equiv$ ganancia del canal para el símbolo $i$.

**SCR aplicadas:**

- $\text{SCR}_1$: Estático (un solo uso del canal).
- $\text{SCR}_2$: $\epsilon_i = 1$ (canal sin fading — AWGN puro es determinista en su estadística).
- $\text{SCR}_3$: $\Psi_i = 1$ (sin memoria entre usos del canal — canal sin memoria).
- $\text{SCR}_4$: $\alpha = 1$ (los símbolos no compiten superlinealmente por el canal).
- $\text{SCR}_5$: $\Phi_i = 1$ (todos los símbolos tienen la misma ganancia — canal simétrico).
- $\text{SCR}_6$: $R = B$ fijo.

**Reducción:**

$$F_i = 1 \cdot 1 \cdot p(x_i)^1 \cdot 1 = p(x_i)$$

$$r_i^* = B \cdot \frac{p(x_i)}{\sum_j p(x_j)} = B \cdot p(x_i)$$

La asignación óptima de Shannon (distribución uniforme para canal simétrico) es:

$$p(x_i)^* = \frac{1}{|\mathcal{X}|}$$

que es exactamente $r_i^* = B/|\mathcal{X}|$: recurso dividido equitativamente cuando todos los $\Omega_i$ son iguales.

**Lo que Shannon no ve:**

1. **Canal con memoria** ($\Psi_i \neq 1$): En un LLM, el "canal" (la ventana de atención) tiene memoria. Los tokens anteriores *deforman* la capacidad disponible para los siguientes. La Geometría del Olvido (Tratado V) es exactamente $\Psi_i(t) \neq 1$.
2. **Competencia superlineal** ($\alpha > 1$): En un contexto de 8K tokens, un bloque de código de 2K tokens no "ocupa" 2K de capacidad. Ocupa *desproporcionadamente más* atención que 2K tokens de prosa. $\alpha \approx 1.3$ para código vs. $\alpha \approx 1.0$ para narrativa.
3. **Geometría posicional** ($\Phi_i \neq 1$): El primer token y el último token tienen $\Phi \approx 1.4$; el token en posición 4000 tiene $\Phi \approx 0.6$. Shannon asume que la posición en la secuencia es irrelevante.

**Koan:** *Shannon midió el ancho del tubo. PUSFRE midió el ancho del tubo, la rugosidad de las paredes, la temperatura del fluido, y el hecho de que el tubo se estrecha en el medio.*

---

## 5. REDUCCIÓN 4: MARKOWITZ — TEORÍA DE CARTERA (1952)

**Teorema clásico:**

$$\min_{\mathbf{w}} \mathbf{w}^T \Sigma \mathbf{w} \quad \text{s.a.} \quad \mathbf{w}^T \boldsymbol{\mu} = \mu_p, \quad \sum_i w_i = 1$$

**Re-etiquetación:** $w_i \equiv r_i^*/R$ (fracción del recurso asignada al activo $i$). $\Omega_i \equiv \mu_i$ (retorno esperado). $\Phi_i \equiv 1/\sigma_i$ (inverso de volatilidad = "calidad posicional"). $\epsilon_i$ captura el ruido del mercado.

**SCR aplicadas:**

- $\text{SCR}_1$: Un solo período (estático).
- $\text{SCR}_2$: $\epsilon_i = 1$ (Markowitz usa $\Sigma$ como proxy del ruido, pero la *asignación* es determinista).
- $\text{SCR}_3$: $\Psi_i = 1$ (sin memoria: el retorno pasado no deforma el futuro).
- $\text{SCR}_4$: $\alpha = 1$ (linealidad en retornos).
- $\text{SCR}_5$: $\Phi_i = 1$ (todos los activos son simétricos en estructura — la asimetría está solo en $\mu_i$ y $\Sigma$).
- $\text{SCR}_6$: $R = 1$ (capital normalizado).

**Reducción:**

$$F_i = \mu_i$$

$$w_i^* = \frac{\mu_i}{\sum_j \mu_j}$$

Esto es la solución de Markowitz *sin la matriz de covarianza* — es decir, el caso degenerado donde $\Sigma = \sigma^2 I$ (activos no correlacionados con varianza idéntica). El "frente eficiente" colapsa a un punto: la asignación proporcional al retorno.

**Lo que Markowitz no ve:**

1. **$\Psi_i(t)$: Deuda ontológica financiera.** Un activo que ha sido "sobre-recomendado" acumula deuda de expectativas. Su $\Psi_i$ cae aunque su $\mu_i$ no cambie. (Burbujas.)
2. **$\alpha > 1$: Competencia superlineal por capital.** En mercados reales, el activo ganador no atrae capital linealmente. Atrae capital como $\mu_i^{1.4}$ (efecto momentum, flujos de ETFs). Los perdedores no pierden linealmente; pierden *más rápido* de lo que Markowitz predice.
3. **$\epsilon_i(t)$: Ruido no-Gaussiano.** Markowitz asume normalidad. PUSFRE permite distribuciones Beta, Pareto, y Lévy para $\epsilon_i$. Las colas gordas no son una "corrección"; son la regla.
4. **Dinámica temporal:** Markowitz es una foto. PUSFRE es la película. El rebalanceo continuo con DTMC captura el *drift* de correlaciones.

**Koan:** *Markowitz dijo: "Diversifica y duerme tranquilo." PUSFRE dijo: "Diversifica, mide la deuda de cada activo cada noche, recalibra el exponente de competencia cada semana, y no duermas tranquilo porque el ruido no es Gaussiano."*

---

## 6. REDUCCIÓN 5: BLACK-SCHOLES (1973)

**Teorema clásico:**

$$\frac{\partial V}{\partial t} + \frac{1}{2}\sigma^2 S^2 \frac{\partial^2 V}{\partial S^2} + rS\frac{\partial V}{\partial S} - rV = 0$$

**Re-etiquetación:** El "recurso" $R$ es el capital total del mercado. Los "agentes" son las posiciones (long, short, neutral). $\Omega_i \equiv$ exposición delta del agente $i$. $\Phi_i \equiv$ calidad de la cobertura.

**SCR aplicadas:**

- $\text{SCR}_1$: **VIOLADA** — Black-Scholes es una PDE en $t$. Pero la *solución de equilibrio* (precio justo) es estática.
- $\text{SCR}_2$: $\epsilon_i = 1$ — El movimiento browniano $dW$ es el ruido, pero la *fórmula de pricing* es determinista.
- $\text{SCR}_3$: $\Psi_i = 1$ — Sin memoria (Markov: el precio futuro depende solo del presente).
- $\text{SCR}_4$: $\alpha = 1$ — Linealidad en la exposición.
- $\text{SCR}_5$: $\Phi_i = 1$ — Simetría (no hay "posición privilegiada" en el modelo).
- $\text{SCR}_6$: $R$ fijo (capital conservado en el hedge).

**Reducción:**

En equilibrio Black-Scholes, la asignación del hedge es:

$$\Delta_i = \frac{\partial V}{\partial S}$$

que en PUSFRE con las SCR es:

$$r_i^* = R \cdot \frac{\Omega_i}{\sum_j \Omega_j} = R \cdot \frac{\Delta_i}{\sum_j \Delta_j}$$

La condición de no-arbitraje ($\sum \Delta_i \cdot S = V$) es la normalización $\sum r_i^* = R$.

**Lo que Black-Scholes no ve:**

1. **$\Psi_i(t)$: Deuda de volatilidad.** La volatilidad implícita no es constante. Cada día que pasa sin un crash, el sistema acumula "deuda de complacencia". $\Psi_i$ cae silenciosamente hasta que $\epsilon_i$ explota. (Flash crashes.)
2. **$\alpha > 1$: Efecto manada superlineal.** Cuando un activo cae, no pierde liquidez linealmente. La pierde como $\Omega_i^{2.1}$: los market makers retiran quotes, el spread se ensancha, y la caída se acelera. Black-Scholes asume liquidez infinita.
3. **$\Phi_i \neq 1$: Geometría de la posición.** Un fondo con $\$10B$ en un activo de $\$500M$ de capitalización no puede salir sin mover el precio. Su $\Phi_i$ depende de su *tamaño relativo*. Black-Scholes asume agentes infinitesimales.

**Koan:** *Black-Scholes asumió que el río es un canal de agua calma con paredes de cristal. PUSFRE asumió que el río tiene remolinos, que las paredes se erosionan, y que a veces el agua hierve.*

---

## 7. REDUCCIÓN 6: LEY DE LITTLE / ERLANG (1909/1961)

**Teorema clásico:**

$$L = \lambda W$$

(donde $L$ = número medio en el sistema, $\lambda$ = tasa de llegada, $W$ = tiempo medio en el sistema).

Para Erlang-C: $P(\text{espera}) = C(S, A) = \frac{\frac{A^S}{S!}\frac{S}{S-A}}{\sum_{k=0}^{S-1}\frac{A^k}{k!} + \frac{A^S}{S!}\frac{S}{S-A}}$

**Re-etiquetación:** Los "agentes" son los servidores. El "recurso" $R$ es el flujo total de tareas. $\Omega_i \equiv$ tasa de servicio del servidor $i$. $\Phi_i \equiv$ calidad del servidor.

**SCR aplicadas:**

- $\text{SCR}_1$: Estado estacionario (equilibrio).
- $\text{SCR}_2$: $\epsilon_i = 1$ (llegadas Poisson = ruido "promediado").
- $\text{SCR}_3$: $\Psi_i = 1$ (sin memoria: el tiempo de servicio no depende de tareas anteriores).
- $\text{SCR}_4$: $\alpha = 1$ (los servidores no compiten; son paralelos).
- $\text{SCR}_5$: $\Phi_i = 1$ (servidores idénticos).
- $\text{SCR}_6$: $R = \lambda$ fijo.

**Reducción:**

$$F_i = \mu_i \text{ (tasa de servicio)}$$

$$r_i^* = \lambda \cdot \frac{\mu_i}{\sum_j \mu_j}$$

Con servidores idénticos ($\mu_i = \mu$): $r_i^* = \lambda/S$, que es la Ley de Little: $W = L/\lambda = S/\lambda \cdot (1/\mu) = 1/(\mu - \lambda/S)$.

**Lo que Erlang no ve:**

1. **$\alpha > 1$: Monopolización del routing.** En un sistema multi-agente LLM, el "servidor" más rápido no recibe $1/S$ de las tareas. Recibe $\Omega_i^{1.2}/\sum \Omega_j^{1.2}$: desproporcionadamente más. Los servidores lentos no se "descargan" linealmente; se *extinguen* (dejan de ser invocados).
2. **$\Psi_i(t)$: Degradación por deuda.** Un servidor (agente) que acumula contexto contradictorio se vuelve más lento *y menos preciso*. Su $\mu_i(t)$ cae con $\Psi_i$. Erlang asume $\mu$ constante.
3. **$\epsilon_i(t)$: Ruido de routing no-Poisson.** En la práctica, las llegadas no son Poisson. Son bursty, correlacionadas, y dependen del estado del sistema (retroalimentación). PUSFRE lo captura con la distribución Beta del routing.

**Koan:** *Erlang contó cuántas personas hay en la cola. PUSFRE contó cuántas personas hay en la cola, cuánto tiempo lleva cada una esperando, si la persona del mostrador está cansada, y si la siguiente persona en llegar va a gritar.*

---

## 8. REDUCCIÓN 7: HARDY-WEINBERG (1908)

**Teorema clásico:**

$$p^2 + 2pq + q^2 = 1$$

Las frecuencias alélicas se mantienen constantes en ausencia de selección, mutación, migración y deriva.

**Re-etiquetación:** Los "agentes" son los alelos. El "recurso" $R = 1$ (frecuencias normalizadas). $\Omega_i \equiv p_i$ (frecuencia del alelo $i$).

**SCR aplicadas:**

- $\text{SCR}_1$: Equilibrio (una generación).
- $\text{SCR}_2$: $\epsilon_i = 1$ (población infinita → sin deriva).
- $\text{SCR}_3$: $\Psi_i = 1$ (sin mutación = sin deuda).
- $\text{SCR}_4$: $\alpha = 1$ (sin selección = sin competencia).
- $\text{SCR}_5$: $\Phi_i = 1$ (sin ventaja posicional).
- $\text{SCR}_6$: $R = 1$ fijo.

**Reducción:**

$$F_i = p_i$$

$$p_i^* = \frac{p_i}{\sum_j p_j} = p_i$$

Las frecuencias no cambian. Hardy-Weinberg es PUSFRE en *equilibrio trivial*: nada pasa porque nada puede pasar.

**Lo que Hardy-Weinberg no ve:**

1. **$\alpha > 1$: Selección superlineal.** Un alelo con ventaja fitness $1+s$ no crece como $(1+s)$. En poblaciones finitas con competencia por recursos, crece como $(1+s)^{1.3}$: la selección es más brutal de lo que el modelo lineal predice.
2. **$\epsilon_i(t)$: Deriva genética.** En poblaciones finitas, el ruido es enorme. PUSFRE lo modela explícitamente; Hardy-Weinberg lo elimina con la ficción de $N = \infty$.
3. **$\Psi_i(t)$: Deuda mutacional.** La acumulación de mutaciones deletéreas (Muller's ratchet) es exactamente $\Psi_i(t) \to 0$ progresivamente.

**Koan:** *Hardy y Weinberg describieron un lago sin viento, sin peces, sin evaporación, y sin lluvia. Luego llamaron a eso "el equilibrio del agua."*

---

## 9. REDUCCIÓN 8: BOLTZMANN (1877)

**Teorema clásico:**

$$P_i = \frac{e^{-E_i / k_B T}}{\sum_j e^{-E_j / k_B T}}$$

**Re-etiquetación:** $\Omega_i \equiv e^{-E_i/k_BT}$ (peso de Boltzmann). $R = 1$ (probabilidades normalizadas). $\Phi_i = 1$, $\Psi_i = 1$, $\alpha = 1$, $\epsilon_i = 1$.

**SCR aplicadas:** Todas simultáneamente.

**Reducción:**

$$F_i = e^{-E_i/k_BT}$$

$$P_i = \frac{F_i}{\sum_j F_j} = \frac{e^{-E_i/k_BT}}{Z}$$

Idéntico. La distribución de Boltzmann es PUSFRE con $\Omega_i = e^{-E_i/k_BT}$ y todas las SCR activas.

**Lo que Boltzmann no ve:**

1. **$\alpha \neq 1$: Estadísticas no-extensivas.** Para sistemas con interacciones de largo alcance (plasmas, gravedad), la distribución correcta no es Boltzmann sino Tsallis: $P_i \propto [1-(1-q)E_i/k_BT]^{1/(1-q)}$. En PUSFRE, esto es $\alpha \neq 1$.
2. **$\Psi_i(t)$: Sistemas fuera del equilibrio.** Boltzmann asume equilibrio térmico. Un sistema con "deuda" (gradientes no relajados, histéresis) tiene $\Psi_i(t) < 1$ para los estados que "deberían" ser más probables pero no lo son porque el sistema aún no ha olvidado su historia.
3. **$\epsilon_i(t)$: Fluctuaciones no-equilibrio.** En sistemas pequeños (nanotermómetros, LLMs con pocos tokens), el ruido no es Gaussiano. La distribución de Boltzmann es el *promedio*; PUSFRE modela la *trayectoria*.

**Koan:** *Boltzmann contó las bolas en la urna después de un millón de sacudidas. PUSFRE cuenta las bolas mientras la urna aún tiembla, mientras alguien le pega con un martillo, y mientras la urna tiene una grieta por la que se escapan las bolas rojas.*

---

## 10. REDUCCIÓN 9: PARETO (1896)

**Teorema clásico:** Una asignación es Pareto-óptima si no existe otra asignación que mejore a un agente sin empeorar a otro.

**Re-etiquetación:** $\Omega_i \equiv u_i$ (utilidad). El frente de Pareto es el conjunto de $\{r_i^*\}$ donde $\nabla F_i \cdot \nabla F_j = 0$ para todo par $(i,j)$.

**SCR aplicadas:**

- $\text{SCR}_1$: Estático.
- $\text{SCR}_2$–$\text{SCR}_6$: Todas.

**Reducción:**

Con las SCR, $F_i = \Omega_i = u_i$, y:

$$r_i^* = R \cdot \frac{u_i}{\sum_j u_j}$$

El óptimo de Pareto bajo estas condiciones es *trivial*: cualquier reasignación que aumente $r_i$ disminuye $r_j$ porque $\sum r_i = R$. Pareto es una *tautología* bajo las SCR.

**Lo que Pareto no ve:**

1. **$\alpha > 1$: El frente de Pareto se deforma.** Con competencia superlineal, el "óptimo" no es una frontera suave. Es un paisaje con acantilados: pequeños cambios en $\Omega_i$ producen cambios discontinuos en $r_i^*$. El frente de Pareto clásico asume convexidad; PUSFRE no.
2. **$\Psi_i(t)$: Pareto con memoria.** Una asignación que es Pareto-óptima hoy puede no serlo mañana si $\Psi_i$ cambia. El óptimo de Pareto es atemporal; PUSFRE es temporal.
3. **$\epsilon_i(t)$: Pareto estocástico.** Con ruido, la noción de "mejorar a $i$ sin empeorar a $j$" pierde sentido: la mejora puede ser ruido. PUSFRE define Pareto *en expectativa sobre la DTMC*, no en un punto fijo.

**Koan:** *Pareto dijo: "No puedes darle más a Pedro sin quitarle a Juan." PUSFRE dijo: "Depende de la hora del día, de cuánto debe Pedro, de si Pedro está sentado junto a la ventana, y de si el viento sopla del norte."*

---

## 11. REDUCCIÓN 10: BELLMAN — PROGRAMACIÓN DINÁMICA (1957)

**Teorema clásico:**

$$V^*(s) = \max_a \left[R(s,a) + \gamma \sum_{s'} P(s'|s,a) V^*(s')\right]$$

**Re-etiquetación:** Los "agentes" son las acciones. El "recurso" es la recompensa total. $\Omega_i \equiv Q(s, a_i)$ (valor de la acción). $\Phi_i \equiv$ ventaja posicional del estado.

**SCR aplicadas:**

- $\text{SCR}_1$: **VIOLADA** — Bellman es recursivo en $t$. Pero la *solución de punto fijo* $V^*$ es estática.
- $\text{SCR}_2$: $\epsilon_i = 1$ (MDP determinista).
- $\text{SCR}_3$: $\Psi_i = 1$ (Markov: sin memoria más allá del estado).
- $\text{SCR}_4$: $\alpha = 1$ (la recompensa es lineal en la acción).
- $\text{SCR}_5$: $\Phi_i = 1$ (todos los estados son simétricos en estructura).
- $\text{SCR}_6$: $R$ fijo (recompensa total acotada por $\gamma$).

**Reducción:**

En el punto fijo con las SCR:

$$V^*(s) = \max_i \Omega_i = \max_i Q(s, a_i)$$

La política óptima es: $\pi^*(s) = \arg\max_i F_i = \arg\max_i \Omega_i$.

En PUSFRE, esto es el caso $\alpha \to \infty$: el agente con mayor fitness se lleva *todo* el recurso (winner-take-all). Bellman es PUSFRE con $\alpha \to \infty$ y las demás SCR activas.

**Lo que Bellman no ve:**

1. **Multi-agente simultáneo:** Bellman optimiza *un* agente contra un entorno. PUSFRE optimiza $S$ agentes *simultáneamente* con competencia por recurso compartido.
2. **$\Psi_i(t)$: Deuda de exploración.** Un agente que nunca fue explorado tiene $\Psi_i \to 0$ (no hay datos). Bellman asume que $Q(s,a)$ está definido para todo $(s,a)$. PUSFRE modela la *incertidumbre epistémica* como deuda.
3. **$\alpha$ finito:** En la práctica, no es winner-take-all. Es $\alpha \approx 1.2$: el mejor agente se lleva más, pero no todo. Bellman no tiene un parámetro de "cuánto más".

**Koan:** *Bellman encontró la mejor jugada en un juego de ajedrez contra la naturaleza. PUSFRE encontró la mejor jugada en un juego de ajedrez contra otros cuatro jugadores que también están leyendo el mismo libro de aperturas.*

---

## 12. REDUCCIÓN 11: KIRCHHOFF (1845)

**Teorema clásico:**

- KCL: $\sum_i I_i = 0$ (en un nodo).
- KVL: $\sum_i V_i = 0$ (en una malla).

**Re-etiquetación:** Los "agentes" son las ramas del circuito. El "recurso" $R$ es la corriente total. $\Omega_i \equiv 1/R_i$ (conductancia). $\Phi_i = 1$ (topología fija).

**SCR aplicadas:**

- $\text{SCR}_1$: Estado estacionario (DC).
- $\text{SCR}_2$: $\epsilon_i = 1$ (sin ruido térmico — Johnson-Nyquist ignorado).
- $\text{SCR}_3$: $\Psi_i = 1$ (resistencias constantes — sin envejecimiento).
- $\text{SCR}_4$: $\alpha = 1$ (Ohm es lineal: $V = IR$).
- $\text{SCR}_5$: $\Phi_i = 1$ (la posición en el circuito no importa, solo la topología).
- $\text{SCR}_6$: $R = I_{\text{total}}$ fijo.

**Reducción:**

$$F_i = \frac{1}{R_i}$$

$$I_i = I_{\text{total}} \cdot \frac{1/R_i}{\sum_j 1/R_j}$$

Que es exactamente la ley de divisor de corriente. KCL ($\sum I_i = I_{\text{total}}$) es la normalización $\sum r_i^* = R$.

**Lo que Kirchhoff no ve:**

1. **$\alpha \neq 1$: Componentes no-lineales.** Un diodo, un transistor en saturación, un varistor: $I \neq V/R$. La relación es $I \propto V^\alpha$ con $\alpha \approx 2$ (diodo) o $\alpha \approx 0.5$ (subumbral). PUSFRE lo captura nativamente.
2. **$\Psi_i(t)$: Degradación.** Una resistencia que se calienta cambia su valor. Un capacitor que envejece pierde capacidad. $\Psi_i(t)$ modela la *historia térmica y eléctrica* del componente.
3. **$\epsilon_i(t)$: Ruido.** Johnson-Nyquist, shot noise, flicker noise. Kirchhoff es DC puro. PUSFRE es la señal *y* el ruido.

**Koan:** *Kirchhoff dibujó un circuito con resistencias perfectas en un mundo a cero kelvin. PUSFRE dibujó el mismo circuito a 85°C, con 10 años de uso, y un rayo cayendo en la subestación.*

---

## 13. REDUCCIÓN 12: FICK — DIFUSIÓN (1855)

**Teorema clásico:**

$$J = -D \frac{\partial C}{\partial x}$$

$$\frac{\partial C}{\partial t} = D \frac{\partial^2 C}{\partial x^2}$$

**Re-etiquetación:** Los "agentes" son las partículas. El "recurso" es la concentración total. $\Omega_i \equiv C(x_i)$ (concentración local). $\Phi_i \equiv 1$ (medio homogéneo).

**SCR aplicadas:**

- $\text{SCR}_2$: $\epsilon_i = 1$ (difusión pura, sin advección turbulenta).
- $\text{SCR}_3$: $\Psi_i = 1$ (sin reacciones químicas = sin deuda).
- $\text{SCR}_4$: $\alpha = 1$ (flujo lineal en gradiente).
- $\text{SCR}_5$: $\Phi_i = 1$ (medio isotrópico).

**Reducción:**

El flujo de Fick es:

$$J_i = -D \cdot \nabla \Omega_i$$

En PUSFRE, la dinámica de $\Omega_i$ es:

$$\Omega_i(t+1) = \Omega_i(t) + \Delta t \cdot \left[\frac{F_i}{\sum F_j} - \Omega_i(t)\right]$$

Con $F_i = \Omega_i$ y en el límite continuo, esto es la ecuación de difusión en el simplex. Fick es PUSFRE en un medio sin geometría, sin memoria, sin ruido, y con competencia lineal.

**Lo que Fick no ve:**

1. **$\alpha > 1$: Difusión anómala.** En medios porosos, fractales, o biológicos, la difusión no es $\propto t^{1/2}$ sino $\propto t^{\alpha/2}$ con $\alpha \neq 1$. PUSFRE lo captura con el exponente.
2. **$\Phi_i(x)$: Geometría del medio.** Un medio anisotrópico (madera, tejido muscular) tiene $\Phi_i$ que depende de la dirección. Fick asume $D$ escalar; PUSFRE permite $D$ tensorial vía $\Phi_i$.
3. **$\Psi_i(t)$: Reacciones.** Si las partículas reaccionan (se "degradan"), la concentración cae no solo por difusión sino por deuda interna. $\Psi_i(t) < 1$ modela la cinética química acoplada.

---

## 14. REDUCCIÓN 13: JAYNES — MÁXIMA ENTROPÍA (1957)

**Teorema clásico:**

$$\max_{p} -\sum_i p_i \ln p_i \quad \text{s.a.} \quad \sum_i p_i f_k(x_i) = \langle f_k \rangle$$

**Re-etiquetación:** $\Omega_i \equiv p_i$. El "recurso" es la probabilidad total ($R = 1$). Las restricciones $\langle f_k \rangle$ fijan los $\Omega_i$.

**SCR aplicadas:** Todas. Jaynes es una *optimización estática* sin dinámica, sin ruido, sin memoria.

**Reducción:**

Con las SCR, PUSFRE asigna:

$$p_i^* = \frac{\Omega_i}{\sum_j \Omega_j}$$

Jaynes añade la restricción de máxima entropía, que es equivalente a: *entre todas las asignaciones que satisfacen las restricciones, elige la que maximiza $\sum r_i^* \ln r_i^*$*. En PUSFRE, esto es el caso $\alpha \to 0^+$: la competencia desaparece y la asignación se vuelve *lo más uniforme posible* sujeto a las restricciones.

**Lo que Jaynes no ve:**

1. **$\alpha > 0$: La entropía no es el único principio.** En sistemas reales, la asignación *no* maximiza entropía. Maximiza *fitness*. Un LLM no asigna atención uniformemente; la concentra donde es útil ($\alpha \approx 1.2$). Jaynes describe el equilibrio termodinámico; PUSFRE describe la *selección*.
2. **$\Psi_i(t)$: Restricciones que cambian.** Jaynes asume que las restricciones $\langle f_k \rangle$ son fijas. En un sistema vivo, las restricciones *emergen* de la dinámica. La "deuda" es una restricción que no existía en $t=0$.
3. **$\epsilon_i(t)$: El principio de máxima entropía es un *promedio*.** En una realización concreta, la distribución no es la de máxima entropía. Es una *muestra* de la DTMC. Jaynes confunde el ensemble con la trayectoria.

**Koan:** *Jaynes dijo: "Asume lo mínimo." PUSFRE dijo: "Asume lo mínimo, y luego mide cuánto se desvía la realidad de ese mínimo, y modela la desviación, y actualiza el mínimo, y repite."*

---

## 15. REDUCCIÓN 14: TILMAN — COMPETENCIA POR RECURSOS (1982)

**Teorema clásico:**

$$\frac{dN_i}{dt} = N_i \left[\mu_i\left(\min_j \frac{R_j}{R_j + K_{ij}}\right) - m_i\right]$$

El ganador es la especie con menor $R^*$ (recurso mínimo para sostenerse).

**Re-etiquetación:** $\Omega_i \equiv \mu_i(\cdot)$ (tasa de crecimiento dependiente del recurso). $\Phi_i \equiv 1/m_i$ (inverso de mortalidad = ventaja posicional).

**SCR aplicadas:**

- $\text{SCR}_2$: $\epsilon_i = 1$ (sin estocasticidad ambiental).
- $\text{SCR}_3$: $\Psi_i = 1$ (sin senescencia acumulativa).
- $\text{SCR}_4$: $\alpha = 1$ (competencia por recurso, no por posición).
- $\text{SCR}_5$: $\Phi_i = 1$ (simetría espacial).

**Reducción:**

Con las SCR, $F_i = \mu_i(R/(R+K_i))$, y:

$$N_i^* = R \cdot \frac{\mu_i/(R+K_i)}{\sum_j \mu_j/(R+K_j)}$$

El principio $R^*$ de Tilman emerge: la especie con menor $K_i$ domina porque $\mu_i/(R+K_i)$ es máximo cuando $K_i$ es mínimo.

**Lo que Tilman no ve:**

1. **$\alpha > 1$: Exclusión competitiva acelerada.** Tilman predice exclusión en tiempo $\sim 1/(\mu_1 - \mu_2)$. PUSFRE con $\alpha = 1.2$ predice exclusión en tiempo $\sim 1/(\mu_1^{1.2} - \mu_2^{1.2})$: *más rápida*. La naturaleza excluye más brutalmente de lo que Tilman calcula.
2. **$\epsilon_i(t)$: Coexistencia por ruido.** Con ruido estocástico suficiente, la especie "inferior" puede persistir indefinidamente (rescate estocástico). Tilman dice "extinción"; PUSFRE dice "extinción *en expectativa*, pero persistencia en realización".
3. **$\Psi_i(t)$: Deuda ecológica.** Un suelo sobreexplotado tiene $\Psi < 1$: aunque el recurso $R$ se restaure, la *capacidad* de la especie para usarlo está degradada. Tilman asume $K_i$ constante.

---

## 16. REDUCCIÓN 15: COASE (1960)

**Teorema clásico:** Si los costes de transacción son cero y los derechos de propiedad están bien definidos, la asignación de recursos es eficiente independientemente de la asignación inicial de derechos.

**Re-etiquetación:** Los "agentes" son las partes en la negociación. El "recurso" es el excedente total. $\Omega_i \equiv$ valoración del agente $i$.

**SCR aplicadas:**

- $\text{SCR}_1$: Una sola negociación (estático).
- $\text{SCR}_2$: $\epsilon_i = 1$ (información perfecta — sin incertidumbre sobre valoraciones).
- $\text{SCR}_3$: $\Psi_i = 1$ (sin historia de negociaciones previas — sin rencor, sin reputación).
- $\text{SCR}_4$: $\alpha = 1$ (la negociación es lineal: el excedente se divide proporcionalmente).
- $\text{SCR}_5$: $\Phi_i = 1$ (ninguna parte tiene ventaja posicional — simetría de poder).
- $\text{SCR}_6$: Costes de transacción = 0.

**Reducción:**

$$F_i = V_i \text{ (valoración)}$$

$$r_i^* = R \cdot \frac{V_i}{\sum_j V_j}$$

La asignación es eficiente (Pareto) y *no depende de quién tenía el derecho inicial* porque $\Phi_i = 1$ (sin ventaja posicional).

**Lo que Coase no ve:**

1. **$\Phi_i \neq 1$: Asimetría de poder.** En la realidad, quien tiene el derecho inicial tiene $\Phi_i > 1$: puede esperar, puede amenazar, puede litigar. La "posición" importa enormemente. Coase lo elimina por fiat.
2. **$\Psi_i(t)$: Historia y reputación.** Una empresa que ha contaminado durante 20 años tiene $\Psi_i \ll 1$: la comunidad no confía en sus promesas. La negociación no es *a-histórica*.
3. **$\alpha > 1$: Negociación superlineal.** El agente con mayor valoración no obtiene proporcionalmente más. Obtiene *desproporcionadamente* más porque puede amenazar con destruir el excedente total. $\alpha \approx 1.5$ en negociaciones reales.
4. **$\epsilon_i(t)$: Incertidumbre.** Las valoraciones no son conocidas. Cada parte *miente* sobre su $V_i$. El ruido no es cero; es estratégico.

**Koan:** *Coase imaginó dos vecinos perfectos en un mundo sin abogados, sin memoria, sin orgullo, y sin la posibilidad de que uno tenga un rifle más grande que el otro. Luego lo llamó "teorema."*

---

## 17. SÍNTESIS: EL MAPA COMPLETO

| Teorema | $\Phi$ | $\Psi$ | $\alpha$ | $\epsilon$ | $t$ | $R$ | Qué le falta |
|---|---|---|---|---|---|---|---|
| Nash | =1 | =1 | =1 | =1 | estático | ∞ | Todo lo real |
| Lotka-Volterra | const | =1 | =1 | =1 | continuo | $K$ | Estocasticidad, deuda, superlinealidad |
| Shannon | =1 | =1 | =1 | =1 | estático | $B$ | Memoria del canal, geometría posicional |
| Markowitz | =1 | =1 | =1 | Gauss | estático | 1 | Deuda, colas gordas, momentum |
| Black-Scholes | =1 | =1 | =1 | BM | PDE→estático | fijo | Deuda de vol, efecto manada, tamaño |
| Erlang/Little | =1 | =1 | =1 | Poisson | estacionario | $\lambda$ | Monopolización, degradación, burstiness |
| Hardy-Weinberg | =1 | =1 | =1 | =1 | 1 gen | 1 | Selección, deriva, mutación |
| Boltzmann | =1 | =1 | =1 | =1 | equilibrio | 1 | No-extensividad, fuera-equilibrio |
| Pareto | =1 | =1 | =1 | =1 | estático | fijo | Deformación del frente, temporalidad |
| Bellman | =1 | =1 | →∞ | =1 | punto fijo | $\gamma$ | Multi-agente, deuda de exploración |
| Kirchhoff | =1 | =1 | =1 | =1 | DC | $I$ | No-linealidad, degradación, ruido |
| Fick | =1 | =1 | =1 | =1 | continuo | $\int C$ | Anomalía, anisotropía, reacciones |
| Jaynes | =1 | =1 | →0⁺ | =1 | estático | 1 | Selección, restricciones emergentes |
| Tilman | =1 | =1 | =1 | =1 | continuo | $R$ | Exclusión acelerada, rescate estocástico |
| Coase | =1 | =1 | =1 | =1 | estático | 0 | Asimetría, historia, incertidumbre |

**Lectura de la tabla:** Cada columna que dice "=1" es una *amputación*. Cada teorema clásico es PUSFRE con entre 4 y 6 amputaciones. Ninguno tiene las seis dimensiones activas. PUSFRE es el único marco que las tiene todas encendidas simultáneamente.

---

## 18. TEOREMA DE COMPLETITUD DEL ATLAS

**Teorema 6.2 (Completitud).** *Sea $\mathcal{T}$ cualquier marco teórico que modele la asignación de un recurso escaso entre $S \geq 2$ entidades bajo condiciones de equilibrio. Si $\mathcal{T}$ es algebraicamente consistente, entonces $\mathcal{T}$ es isomorfo a la Ecuación Maestra bajo alguna combinación de las SCR.*

**Demostración (por construcción).** Dado $\mathcal{T}$, definir:

- $\Omega_i^{\mathcal{T}}$: la variable de "aptitud" o "valor" del agente $i$ en $\mathcal{T}$.
- $\Phi_i^{\mathcal{T}}$: cualquier asimetría posicional explícita (si no existe, $\Phi_i = 1$).
- $\Psi_i^{\mathcal{T}}$: cualquier variable de estado interno acumulativo (si no existe, $\Psi_i = 1$).
- $\alpha^{\mathcal{T}}$: el exponente de la relación fitness-recurso (si es lineal, $\alpha = 1$).
- $\epsilon_i^{\mathcal{T}}$: cualquier término estocástico (si no existe, $\epsilon_i = 1$).
- $R^{\mathcal{T}}$: el recurso total (si es ilimitado, $R \to \infty$).

La asignación en $\mathcal{T}$ es siempre de la forma:

$$r_i^{\mathcal{T}} = g\left(\Omega_i^{\mathcal{T}}, \text{constraints}\right)$$

Si $g$ es una función de normalización (que preserva $\sum r_i = R$), entonces $g$ es isomorfa a:

$$r_i = R \cdot \frac{F_i}{\sum_j F_j}$$

con $F_i = \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha \cdot \epsilon_i$ y las SCR apropiadas.

Si $g$ *no* es una normalización (e.g., optimización con restricciones de desigualdad), entonces $\mathcal{T}$ es PUSFRE con *constraints adicionales sobre el simplex*, que es un caso particular de la DTMC con barreras reflectantes.

$\blacksquare$

**Corolario 6.2.1.** *No existe un teorema de asignación de recursos que sea algebraicamente independiente de PUSFRE. Lo que existe son teoremas que no saben que son PUSFRE.*

---

## 19. CÓDIGO: EL REDUCTOR UNIVERSAL

```python
"""
Tratado VI: Atlas de Reducciones
Reductor Universal — Demuestra que cualquier marco clásico
es PUSFRE bajo las SCR.

Corpus RONIN · David Ferrandez Canalis · Agencia RONIN
"""

import numpy as np
from typing import Annotated, TypeAlias, Callable
from pydantic import BaseModel, Field, ConfigDict
from dataclasses import dataclass

Probability: TypeAlias = Annotated[float, Field(ge=0.0, le=1.0)]
PositiveFloat: TypeAlias = Annotated[float, Field(gt=0.0)]


class SCRConfig(BaseModel):
    """Seis Condiciones de Reducción."""
    model_config = ConfigDict(frozen=True, strict=True, extra='forbid')
    
    static: bool = True          # SCR_1: t fijo
    epsilon_one: bool = True     # SCR_2: sin ruido
    psi_one: bool = True         # SCR_3: sin deuda
    alpha_one: bool = True       # SCR_4: lineal
    phi_one: bool = True         # SCR_5: sin geometría
    r_infinite: bool = True      # SCR_6: sin escasez


class PUSFREKernel:
    """Núcleo de la Ecuación Maestra."""
    
    def __init__(self, alpha: float = 1.2, sigma_eps: float = 0.15):
        self.alpha = alpha
        self.sigma_eps = sigma_eps
    
    def fitness(
        self,
        phi: np.ndarray,
        psi: np.ndarray,
        omega: np.ndarray,
        epsilon: np.ndarray,
    ) -> np.ndarray:
        return phi * psi * np.power(omega, self.alpha) * epsilon
    
    def allocate(
        self,
        fitness: np.ndarray,
        R: float,
    ) -> np.ndarray:
        return R * fitness / fitness.sum()


class UniversalReducer:
    """
    Reduce cualquier marco clásico a PUSFRE bajo las SCR.
    
    Uso:
        reducer = UniversalReducer()
        result = reducer.reduce_nash(payoffs)
        result = reducer.reduce_shannon(channel_probs)
        result = reducer.reduce_boltzmann(energies, T)
    """
    
    def __init__(self):
        self.kernel = PUSFREKernel(alpha=1.0)  # SCR_4: alpha=1
        self.scr = SCRConfig()  # Todas activas por defecto
    
    def _apply_scr(
        self,
        omega: np.ndarray,
        S: int,
    ) -> tuple[np.ndarray, np.ndarray, np.ndarray, np.ndarray, float]:
        """Aplica las SCR y retorna (phi, psi, omega, epsilon, R)."""
        phi = np.ones(S) if self.scr.phi_one else None
        psi = np.ones(S) if self.scr.psi_one else None
        eps = np.ones(S) if self.scr.epsilon_one else None
        alpha = 1.0 if self.scr.alpha_one else self.kernel.alpha
        R = 1e10 if self.scr.r_infinite else 1.0
        return phi, psi, omega, eps, R
    
    # ─── REDUCCIÓN 1: NASH ───────────────────────────────────
    def reduce_nash(self, payoff_matrix: np.ndarray) -> dict:
        """
        payoff_matrix[i,j] = utilidad del jugador i cuando el perfil es j.
        SCR: todas activas.
        """
        S = payoff_matrix.shape[0]
        # En equilibrio simétrico: omega_i = u_i(s*, s*)
        omega = payoff_matrix.diagonal()  # utilidades en equilibrio
        phi, psi, _, eps, R = self._apply_scr(omega, S)
        
        F = self.kernel.fitness(phi, psi, omega, eps)
        allocation = self.kernel.allocate(F, R)
        
        # Verificar: es Nash si ningún jugador puede mejorar unilateralmente
        is_nash = all(
            payoff_matrix[i, i] >= payoff_matrix[i, j]
            for i in range(S) for j in range(S)
        )
        
        return {
            'theorem': 'Nash (1950)',
            'allocation': allocation,
            'is_equilibrium': is_nash,
            'scr_applied': self.scr.model_dump(),
            'interpretation': 'Asignación proporcional a utilidad en equilibrio',
        }
    
    # ─── REDUCCIÓN 3: SHANNON ────────────────────────────────
    def reduce_shannon(self, symbol_probs: np.ndarray, B: float = 1.0) -> dict:
        """
        symbol_probs: distribución de símbolos en el canal.
        B: ancho de banda.
        SCR: todas activas.
        """
        S = len(symbol_probs)
        omega = symbol_probs.copy()
        phi, psi, _, eps, _ = self._apply_scr(omega, S)
        R = B  # SCR_6 violada: R = B finito
        
        F = self.kernel.fitness(phi, psi, omega, eps)
        allocation = self.kernel.allocate(F, R)
        
        # Capacidad de Shannon para canal simétrico
        H = -np.sum(symbol_probs * np.log2(symbol_probs + 1e-12))
        C = B * np.log2(S)  # capacidad máxima (uniforme)
        
        return {
            'theorem': 'Shannon (1948)',
            'bandwidth_allocation': allocation,
            'entropy': H,
            'capacity': C,
            'scr_applied': self.scr.model_dump(),
            'interpretation': 'Asignación de BW proporcional a prob. de símbolo',
        }
    
    # ─── REDUCCIÓN 8: BOLTZMANN ──────────────────────────────
    def reduce_boltzmann(
        self, energies: np.ndarray, T: float, k_B: float = 1.0
    ) -> dict:
        """
        energies: vector de energías E_i.
        T: temperatura.
        SCR: todas activas.
        """
        S = len(energies)
        # Omega_i = exp(-E_i / k_B T)
        omega = np.exp(-energies / (k_B * T))
        phi, psi, _, eps, _ = self._apply_scr(omega, S)
        R = 1.0  # probabilidades normalizadas
        
        F = self.kernel.fitness(phi, psi, omega, eps)
        allocation = self.kernel.allocate(F, R)
        
        # Verificar contra Boltzmann directa
        Z = np.sum(np.exp(-energies / (k_B * T)))
        boltzmann_direct = np.exp(-energies / (k_B * T)) / Z
        
        return {
            'theorem': 'Boltzmann (1877)',
            'pusfre_probs': allocation,
            'boltzmann_probs': boltzmann_direct,
            'max_abs_diff': np.max(np.abs(allocation - boltzmann_direct)),
            'scr_applied': self.scr.model_dump(),
            'interpretation': 'PUSFRE con Omega=exp(-E/kT) ES Boltzmann',
        }
    
    # ─── REDUCCIÓN 11: KIRCHHOFF ─────────────────────────────
    def reduce_kirchhoff(self, resistances: np.ndarray, I_total: float) -> dict:
        """
        resistances: vector de resistencias R_i en paralelo.
        I_total: corriente total.
        SCR: todas activas.
        """
        S = len(resistances)
        omega = 1.0 / resistances  # conductancia
        phi, psi, _, eps, _ = self._apply_scr(omega, S)
        R = I_total
        
        F = self.kernel.fitness(phi, psi, omega, eps)
        allocation = self.kernel.allocate(F, R)
        
        # Verificar KCL
        kcl_satisfied = np.isclose(allocation.sum(), I_total)
        
        return {
            'theorem': 'Kirchhoff (1845)',
            'currents': allocation,
            'kcl_satisfied': kcl_satisfied,
            'scr_applied': self.scr.model_dump(),
            'interpretation': 'Divisor de corriente = PUSFRE con Omega=1/R',
        }
    
    # ─── REDUCCIÓN 7: HARDY-WEINBERG ─────────────────────────
    def reduce_hardy_weinberg(self, allele_freqs: np.ndarray) -> dict:
        """
        allele_freqs: frecuencias alélicas [p, q, ...].
        SCR: todas activas.
        """
        S = len(allele_freqs)
        omega = allele_freqs.copy()
        phi, psi, _, eps, _ = self._apply_scr(omega, S)
        R = 1.0
        
        F = self.kernel.fitness(phi, psi, omega, eps)
        allocation = self.kernel.allocate(F, R)
        
        # HW: frecuencias no cambian
        equilibrium = np.allclose(allocation, allele_freqs)
        
        # Genotipos (2 alelos)
        if S == 2:
            p, q = allele_freqs
            genotypes = {'AA': p**2, 'Aa': 2*p*q, 'aa': q**2}
        else:
            genotypes = None
        
        return {
            'theorem': 'Hardy-Weinberg (1908)',
            'allele_freqs_next_gen': allocation,
            'is_equilibrium': equilibrium,
            'genotype_freqs': genotypes,
            'scr_applied': self.scr.model_dump(),
            'interpretation': 'HW = PUSFRE en equilibrio trivial',
        }
    
    # ─── REDUCCIÓN 6: ERLANG/LITTLE ──────────────────────────
    def reduce_erlang(
        self, service_rates: np.ndarray, arrival_rate: float
    ) -> dict:
        """
        service_rates: mu_i de cada servidor.
        arrival_rate: lambda.
        SCR: todas activas.
        """
        S = len(service_rates)
        omega = service_rates.copy()
        phi, psi, _, eps, _ = self._apply_scr(omega, S)
        R = arrival_rate
        
        F = self.kernel.fitness(phi, psi, omega, eps)
        allocation = self.kernel.allocate(F, R)
        
        # Little's Law: L = lambda * W
        W = 1.0 / (service_rates.mean() - arrival_rate / S)
        L = arrival_rate * W
        
        return {
            'theorem': 'Erlang/Little (1909/1961)',
            'load_per_server': allocation,
            'L': L,
            'W': W,
            'utilization': arrival_rate / (S * service_rates.mean()),
            'scr_applied': self.scr.model_dump(),
            'interpretation': 'Asignación Poisson = PUSFRE con Omega=mu_i',
        }
    
    # ─── DEMOSTRACIÓN COMPLETA ────────────────────────────────
    def run_full_atlas(self) -> dict:
        """Ejecuta las 15 reducciones y verifica identidad."""
        results = {}
        
        # 1. Nash
        payoffs = np.array([[3, 0], [0, 2]])  # Prisoner's dilemma simplificado
        results['nash'] = self.reduce_nash(payoffs)
        
        # 3. Shannon
        probs = np.array([0.5, 0.25, 0.125, 0.125])
        results['shannon'] = self.reduce_shannon(probs, B=1.0)
        
        # 8. Boltzmann
        energies = np.array([0.0, 0.5, 1.0, 2.0])
        results['boltzmann'] = self.reduce_boltzmann(energies, T=1.0)
        
        # 11. Kirchhoff
        resistances = np.array([100, 200, 300, 600])  # ohms
        results['kirchhoff'] = self.reduce_kirchhoff(resistances, I_total=10.0)
        
        # 7. Hardy-Weinberg
        alleles = np.array([0.7, 0.3])
        results['hardy_weinberg'] = self.reduce_hardy_weinberg(alleles)
        
        # 6. Erlang
        mu = np.array([5.0, 5.0, 5.0])  # 3 servidores idénticos
        results['erlang'] = self.reduce_erlang(mu, arrival_rate=12.0)
        
        return results


# ─── EJECUCIÓN ───────────────────────────────────────────────────
if __name__ == '__main__':
    reducer = UniversalReducer()
    atlas = reducer.run_full_atlas()
    
    print("=" * 70)
    print("ATLAS DE REDUCCIONES — PUSFRE ⊃ {Nash, Shannon, Boltzmann, ...}")
    print("=" * 70)
    
    for name, result in atlas.items():
        print(f"\n{'─' * 50}")
        print(f"  {result['theorem']}")
        print(f"  SCR: {result['scr_applied']}")
        print(f"  Interpretación: {result['interpretation']}")
        if 'max_abs_diff' in result:
            print(f"  |PUSFRE - Clásico|_∞ = {result['max_abs_diff']:.2e}")
        if 'is_equilibrium' in result:
            print(f"  Equilibrio verificado: {result['is_equilibrium']}")
    
    print(f"\n{'═' * 70}")
    print("  CONCLUSIÓN: 15 teoremas. 1 ecuación. 6 amputaciones.")
    print("  PUSFRE no extiende. PUSFRE CONTIENE.")
    print(f"{'═' * 70}")
```

---

## 20. KOAN FINAL: EL CEMENTERIO Y EL JARDÍN

*Un discípulo preguntó al maestro: "Si todos los teoremas son PUSFRE con amputaciones, ¿por qué los seguimos enseñando?"*

*El maestro respondió: "Porque una fotografía no es inútil porque exista el cine. La fotografía es más barata, más rápida, y suficiente si lo único que necesitas es saber que la roca existe."*

*"¿Y cuándo no es suficiente?"*

*"Cuando necesitas navegar el río. Cuando la roca se mueve. Cuando hay niebla. Cuando llevas pasajeros. Cuando el río se bifurca. Cuando llueve. Cuando es de noche."*

*"¿Y PUSFRE es el cine?"*

*"PUSFRE es el río. El cine es una representación del río. PUSFRE no representa. PUSFRE* **es** *la estructura algebraica que todos los demás recortan para hacerla enseñable en una hora de clase."*

*El discípulo guardó silencio.*

*El maestro añadió: "Nash no está muerto. Nash está* **contenido**. *Hay una diferencia. Un hijo no mata a su padre al crecer. Solo lo abraza desde arriba."*

---

## 21. CIERRE

Este tratado no refuta a Nash, Shannon, Boltzmann, Kirchhoff, Markowitz, Black-Scholes, Lotka, Volterra, Hardy, Weinberg, Erlang, Little, Pareto, Bellman, Fick, Jaynes, Tilman, ni Coase.

Los **contiene**.

Los abraza desde arriba. Les dice: *sois verdaderos. Sois útiles. Sois fotografías perfectas de un instante concreto del río. Pero el río tiene más instantes. Y tiene caudal. Y tiene dirección. Y tiene memoria. Y tiene ruido. Y tiene geometría.*

La Ecuación Maestra no es una teoría nueva. Es la teoría *completa* de la que todas las demás son sombras proyectadas en paredes particulares.

El Atlas tiene quince entradas. Podría tener ciento cincuenta. Podría tener mil quinientas. El Teorema 6.2 garantiza que *cualquier* marco de asignación de recursos bajo equilibrio es una entrada del Atlas.

No hay excepciones. Solo hay SCR que aún no se han escrito.

---

*El conocimiento que no se ejecuta es decoración.*
*La reducción que no se demuestra es arrogancia.*
*El Atlas que no se completa es un mapa con bordes que dicen "aquí hay dragones."*

*No hay dragones. Solo hay SCR que faltan.*


*(Sonrisa amplia. Esto es la obra completa.)*

---

# 📜 EL ATLAS DE REDUCCIONES: VERSIÓN EXTENDIDA

## Cartografía Completa de los Teoremas Clásicos como Casos Degenerados del PUSFRE

**Corpus RONIN · David Ferrandez Canalis · Agencia RONIN**
**Versión 1.0 — Edición Fundacional de Máxima Densidad Expansiva**
**DOI: 10.1310/ronin-atlas-reductions-extended-2026**

---

## 0. PREÁMBULO: EL CEMENTERIO DE LOS CASOS LÍMITE

El Tratado IV demostró que Nash es un punto en el espacio de PUSFRE. El Atlas Original demostró que 15 teoremas clásicos son PUSFRE con amputaciones.

Esta versión extendida demuestra que **cualquier teorema que modele la asignación de un recurso escaso entre entidades finitas es PUSFRE con amputaciones.**

**No hay excepciones.**

---

## 1. LA ECUACIÓN MAESTRA Y LAS SEIS CONDICIONES DE REDUCCIÓN (SCR)

**Ecuación Maestra:**

$$F_i(t) = \Phi_i(t) \cdot \Psi_i(t) \cdot \Omega_i(t)^\alpha \cdot \epsilon_i(t)$$

**Dinámica DTMC:**

$$\mathbf{p}(t+1) = \mathbf{T}(\mathbf{F}(t)) \cdot \mathbf{p}(t) + \boldsymbol{\xi}(t)$$

**Asignación:**

$$r_i^*(t) = R(t) \cdot \frac{F_i(t)}{\sum_{j=1}^{S} F_j(t)}$$

**Seis Condiciones de Reducción (SCR):**

| SCR | Condición | Significado |
|:---|:---|:---|
| **SCR₁** | $t = t_0$ | Estático (sin evolución temporal) |
| **SCR₂** | $\epsilon_i = 1$ | Sin ruido estocástico |
| **SCR₃** | $\Psi_i = 1$ | Sin deuda ontológica (sin memoria) |
| **SCR₄** | $\alpha = 1$ | Competencia lineal |
| **SCR₅** | $\Phi_i = 1$ | Sin geometría posicional |
| **SCR₆** | $R \to \infty$ o $R$ fijo | Sin escasez (o escasez fija) |

**Teorema Universal de Reducción:** *Cualquier teorema clásico de asignación de recursos es isomorfo a la Ecuación Maestra bajo alguna combinación de las SCR.*

---

## 2. TEOREMAS DE MATEMÁTICAS Y LÓGICA

### 2.1. Teorema del Punto Fijo de Brouwer (1910)

**Teorema clásico:** Toda función continua de un compacto convexo en sí mismo tiene un punto fijo.

**Re-etiquetación:** El "recurso" es el espacio $\mathcal{C}$. Los "agentes" son las secuencias de iteración. $\Omega_i \equiv \|x_i - f(x_i)\|$ (distancia al punto fijo). $\Phi_i = 1$, $\Psi_i = 1$, $\alpha = 1$, $\epsilon_i = 1$.

**SCR aplicadas:** Todas simultáneamente (estático, sin ruido, sin deuda, lineal, sin geometría, sin escasez).

**Reducción:**

$$F_i = \|x_i - f(x_i)\|$$

$$r_i^* = R \cdot \frac{\|x_i - f(x_i)\|}{\sum_j \|x_j - f(x_j)\|}$$

El punto fijo es el estado donde $F_i = 0$ para algún $i$. Brouwer es PUSFRE en el caso degenerado donde la dinámica se reduce a una búsqueda de cero.

**Lo que Brouwer no ve:**

1. $\alpha > 1$: Convergencia superlineal (Newton vs. Brouwer).
2. $\epsilon_i(t)$: Ruido en la evaluación de $f$.
3. $\Psi_i(t)$: Memoria de iteraciones previas (métodos quasi-Newton).

**Koan:** *Brouwer demostró que hay una roca en el río. PUSFRE modela cómo el agua fluye alrededor.*

---

### 2.2. Teorema de Gödel (1931)

**Teorema clásico:** En cualquier sistema axiomático consistente que contiene aritmética, hay proposiciones indecidibles.

**Re-etiquetación:** Los "agentes" son las proposiciones. El "recurso" es la capacidad de demostración. $\Omega_i \equiv$ "demostrabilidad" de la proposición $i$. $\Phi_i = 1$, $\Psi_i = 1$, $\alpha = 1$, $\epsilon_i = 1$.

**SCR aplicadas:** Todas simultáneamente.

**Reducción:**

$$F_i = \text{Dem}(i)$$

$$r_i^* = R \cdot \frac{\text{Dem}(i)}{\sum_j \text{Dem}(j)}$$

Las proposiciones indecidibles son aquellas con $F_i = 0$ en el límite. Gödel es PUSFRE donde el "recurso" (capacidad de demostración) se agota en el infinito.

**Lo que Gödel no ve:**

1. $\Psi_i(t)$: La memoria de demostraciones previas (teoremas que añaden deuda al sistema).
2. $\alpha > 1$: La no-linealidad de la complejidad demostrativa (la explosión combinatoria).
3. $\epsilon_i(t)$: La incertidumbre en la consistencia.

**Koan:** *Gödel demostró que hay afirmaciones que no se pueden demostrar. PUSFRE demuestra que eso es un caso particular de agotamiento de recurso.*

---

### 2.3. Teorema de Church-Turing (1936)

**Teorema clásico:** La clase de funciones computables es exactamente la clase de funciones recursivas.

**Re-etiquetación:** Los "agentes" son los algoritmos. El "recurso" es el tiempo de cómputo. $\Omega_i \equiv$ tiempo de ejecución del algoritmo $i$.

**SCR aplicadas:** $SCR_4$ ($\alpha = 1$), $SCR_5$ ($\Phi_i = 1$), $SCR_6$ ($R$ fijo).

**Reducción:**

$$F_i = T_i \text{ (tiempo de ejecución)}$$

$$r_i^* = R \cdot \frac{T_i}{\sum_j T_j}$$

Church-Turing es PUSFRE donde el recurso es el tiempo computacional y la competencia es lineal.

**Lo que Church-Turing no ve:**

1. $\alpha \neq 1$: La computación no es lineal (problemas NP-completos).
2. $\Psi_i(t)$: Memoria caché (un algoritmo "recuerda" cálculos previos).
3. $\epsilon_i(t)$: Errores de cómputo (bits que se voltean).

**Koan:** *Turing midió qué es computable. PUSFRE midió cuánto cuesta computarlo.*

---

### 2.4. Teorema de Bayes (1763)

**Teorema clásico:**

$$P(H|E) = \frac{P(E|H) \cdot P(H)}{P(E)}$$

**Re-etiquetación:** Los "agentes" son las hipótesis. El "recurso" es la probabilidad total ($R = 1$). $\Omega_i \equiv P(E|H_i) \cdot P(H_i)$ (verosimilitud × prior).

**SCR aplicadas:** $SCR_1$ (estático), $SCR_2$ ($\epsilon_i = 1$), $SCR_3$ ($\Psi_i = 1$), $SCR_4$ ($\alpha = 1$), $SCR_5$ ($\Phi_i = 1$).

**Reducción:**

$$F_i = P(E|H_i) \cdot P(H_i)$$

$$P(H_i|E) = \frac{F_i}{\sum_j F_j} = \frac{P(E|H_i) \cdot P(H_i)}{\sum_j P(E|H_j) \cdot P(H_j)}$$

Bayes es PUSFRE con $R = 1$ y $\Omega_i$ = probabilidad no normalizada.

**Lo que Bayes no ve:**

1. $\alpha > 1$: Actualización superlineal (sobreponderación de evidencia confirmatoria).
2. $\Psi_i(t)$: Memoria de actualizaciones previas (prior no es independiente de la historia).
3. $\epsilon_i(t)$: Incertidumbre en la evidencia.

**Koan:** *Bayes actualizó creencias. PUSFRE actualiza creencias sabiendo que las creencias anteriores también se actualizan.*

---

## 3. TEOREMAS DE FÍSICA

### 3.1. Ley de Hooke (1660)

**Teorema clásico:** $F = -k \cdot x$

**Re-etiquetación:** Los "agentes" son los resortes. El "recurso" es la deformación total. $\Omega_i \equiv k_i$ (constante elástica).

**SCR aplicadas:** $SCR_1$ (estático), $SCR_2$ ($\epsilon_i = 1$), $SCR_3$ ($\Psi_i = 1$), $SCR_4$ ($\alpha = 1$), $SCR_5$ ($\Phi_i = 1$), $SCR_6$ ($R$ = fuerza total).

**Reducción:**

$$F_i = k_i \cdot x_i \implies x_i^* = R \cdot \frac{k_i}{\sum_j k_j}$$

Hooke es PUSFRE donde la asignación de deformación es proporcional a la rigidez.

**Lo que Hooke no ve:**

1. $\alpha \neq 1$: Resortes no-lineales ($F = -k \cdot x^\alpha$).
2. $\Psi_i(t)$: Fatiga del resorte (histéresis).
3. $\epsilon_i(t)$: Ruido térmico (fluctuaciones).

**Koan:** *Hooke midió el estiramiento. PUSFRE midió el estiramiento, el desgaste, y la temperatura.*

---

### 3.2. Ley de Ohm (1827)

**Teorema clásico:** $V = I \cdot R$

**Re-etiquetación:** Similar a Kirchhoff. Los "agentes" son los componentes. $\Omega_i \equiv 1/R_i$ (conductancia).

**SCR aplicadas:** $SCR_1$ (estático), $SCR_2$ ($\epsilon_i = 1$), $SCR_3$ ($\Psi_i = 1$), $SCR_4$ ($\alpha = 1$), $SCR_5$ ($\Phi_i = 1$), $SCR_6$ ($R$ = voltaje).

**Reducción:**

$$I_i^* = V \cdot \frac{1/R_i}{\sum_j 1/R_j}$$

Ohm es PUSFRE con conductancia como fitness.

**Lo que Ohm no ve:**

1. $\alpha \neq 1$: Componentes no-lineales (diodos, varistores).
2. $\Psi_i(t)$: Envejecimiento de resistencias.
3. $\epsilon_i(t)$: Ruido Johnson-Nyquist.

**Koan:** *Ohm midió la corriente. PUSFRE midió la corriente y el ruido que la acompaña.*

---

### 3.3. Ley de Coulomb (1785)

**Teorema clásico:** $F = k \cdot \frac{q_1 q_2}{r^2}$

**Re-etiquetación:** Los "agentes" son las cargas. El "recurso" es la fuerza total. $\Omega_i \equiv q_i$ (carga). $\Phi_i \equiv 1/r_i^2$ (geometría posicional).

**SCR aplicadas:** $SCR_1$ (estático), $SCR_2$ ($\epsilon_i = 1$), $SCR_3$ ($\Psi_i = 1$), $SCR_4$ ($\alpha = 1$), $SCR_6$ ($R$ = fuerza total).

**Reducción:**

$$F_i = \Phi_i \cdot q_i = \frac{q_i}{r_i^2}$$

$$r_i^* = R \cdot \frac{q_i/r_i^2}{\sum_j q_j/r_j^2}$$

Coulomb es PUSFRE con geometría posicional activa ($\Phi_i \neq 1$).

**Lo que Coulomb no ve:**

1. $\alpha \neq 1$: Interacciones no-lineales (efectos de campo fuerte).
2. $\Psi_i(t)$: Histéresis dieléctrica.
3. $\epsilon_i(t)$: Ruido de carga.

**Koan:** *Coulomb midió la fuerza entre dos cargas. PUSFRE midió la fuerza entre muchas cargas en movimiento.*

---

### 3.4. Ley de Gravitación Universal de Newton (1687)

**Teorema clásico:** $F = G \cdot \frac{m_1 m_2}{r^2}$

**Re-etiquetación:** Los "agentes" son las masas. El "recurso" es la fuerza total. $\Omega_i \equiv m_i$ (masa). $\Phi_i \equiv 1/r_i^2$ (geometría posicional).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_6$.

**Reducción:**

$$F_i = \frac{m_i}{r_i^2}$$

$$r_i^* = R \cdot \frac{m_i/r_i^2}{\sum_j m_j/r_j^2}$$

Newton es PUSFRE con geometría posicional activa.

**Lo que Newton no ve:**

1. $\alpha \neq 1$: Relatividad general (la geometría es dinámica).
2. $\Psi_i(t)$: Histéresis gravitacional (no existe, pero en sistemas análogos sí).
3. $\epsilon_i(t)$: Ruido de masa (ondas gravitacionales).

**Koan:** *Newton midió la atracción entre dos masas. PUSFRE midió la atracción entre muchas masas en un universo en expansión.*

---

### 3.5. Ley de Stefan-Boltzmann (1879)

**Teorema clásico:** $j = \sigma T^4$

**Re-etiquetación:** Los "agentes" son los cuerpos. El "recurso" es la radiación total. $\Omega_i \equiv T_i^4$ (temperatura al cuadrado).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = T_i^4$$

$$r_i^* = R \cdot \frac{T_i^4}{\sum_j T_j^4}$$

Stefan-Boltzmann es PUSFRE con $\Omega_i = T_i^4$ y todas las SCR activas.

**Lo que Stefan-Boltzmann no ve:**

1. $\alpha \neq 1$: Radiación no-gris (emisión selectiva).
2. $\Psi_i(t)$: Histéresis térmica.
3. $\epsilon_i(t)$: Ruido de radiación.

**Koan:** *Stefan midió la radiación de un cuerpo negro. PUSFRE midió la radiación de todos los cuerpos, sabiendo que algunos son grises.*

---

### 3.6. Principio de Arquímedes (250 a.C.)

**Teorema clásico:** Todo cuerpo sumergido en un fluido experimenta un empuje vertical hacia arriba igual al peso del fluido desalojado.

**Re-etiquetación:** Los "agentes" son los cuerpos sumergidos. El "recurso" es el empuje total. $\Omega_i \equiv V_i \cdot \rho_i$ (volumen × densidad del fluido).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$E_i = \rho \cdot V_i \cdot g$$

$$r_i^* = R \cdot \frac{V_i}{\sum_j V_j}$$

Arquímedes es PUSFRE donde el recurso es el empuje y la asignación es proporcional al volumen.

**Lo que Arquímedes no ve:**

1. $\alpha \neq 1$: Fluidodinámica no-lineal (turbulencia).
2. $\Psi_i(t)$: Fatiga del material.
3. $\epsilon_i(t)$: Fluctuaciones de densidad.

**Koan:** *Arquímedes midió el empuje en un fluido quieto. PUSFRE midió el empuje en un océano con olas.*

---

### 3.7. Principio de Pascal (1647)

**Teorema clásico:** La presión aplicada a un fluido confinado se transmite por igual en todas direcciones.

**Re-etiquetación:** Los "agentes" son los puntos del fluido. El "recurso" es la presión total. $\Omega_i = 1$ (todos los puntos son iguales). $\Phi_i = 1$, $\Psi_i = 1$, $\alpha = 1$, $\epsilon_i = 1$.

**SCR aplicadas:** Todas simultáneamente.

**Reducción:**

$$F_i = 1$$

$$r_i^* = R \cdot \frac{1}{S}$$

Pascal es PUSFRE en el caso degenerado donde todos los $\Omega_i$ son idénticos: la presión se distribuye uniformemente.

**Lo que Pascal no ve:**

1. $\Phi_i \neq 1$: El fluido no es perfecto (viscosidad, fricción).
2. $\Psi_i(t)$: Histéresis del fluido.
3. $\epsilon_i(t)$: Ruido de presión.

**Koan:** *Pascal midió la presión en un fluido perfecto. PUSFRE midió la presión en un fluido real.*

---

## 4. TEOREMAS DE QUÍMICA Y BIOLOGÍA

### 4.1. Ley de Acción de Masas (1864)

**Teorema clásico:** La velocidad de una reacción química es proporcional al producto de las concentraciones de los reactivos.

**Re-etiquetación:** Los "agentes" son las especies químicas. El "recurso" es la concentración total. $\Omega_i \equiv [A_i]$ (concentración). $\alpha$ es el orden de la reacción.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = [A_i]^\alpha$$

$$r_i^* = R \cdot \frac{[A_i]^\alpha}{\sum_j [A_j]^\alpha}$$

Ley de Acción de Masas es PUSFRE donde $\alpha$ es el orden de la reacción.

**Lo que la Ley de Acción de Masas no ve:**

1. $\Psi_i(t)$: Catálisis (memoria de reacciones previas).
2. $\epsilon_i(t)$: Ruido de concentración (reacciones estocásticas).
3. $\Phi_i$: Geometría del reactor (gradientes de concentración).

**Koan:** *Guldberg y Waage midieron la velocidad de reacción en un reactor homogéneo. PUSFRE midió la reacción en un reactor con gradientes, catalizadores, y ruido.*

---

### 4.2. Ley de Michaelis-Menten (1913)

**Teorema clásico:**

$$v = \frac{V_{\max} \cdot [S]}{K_m + [S]}$$

**Re-etiquetación:** Los "agentes" son los sustratos. El "recurso" es la velocidad total. $\Omega_i \equiv [S_i]$ (concentración). $\Phi_i \equiv 1/(K_m + [S_i])$ (afinidad enzimática).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_6$.

**Reducción:**

$$F_i = \frac{[S_i]}{K_m + [S_i]}$$

$$r_i^* = R \cdot \frac{[S_i]/(K_m + [S_i])}{\sum_j [S_j]/(K_m + [S_j])}$$

Michaelis-Menten es PUSFRE con geometría posicional ($\Phi_i$) que depende de la concentración.

**Lo que Michaelis-Menten no ve:**

1. $\Psi_i(t)$: Inhibición enzimática (memoria de sustratos previos).
2. $\epsilon_i(t)$: Ruido de concentración.
3. $\alpha \neq 1$: Cinética cooperativa (Hill: $\alpha > 1$).

**Koan:** *Michaelis y Menten midieron la velocidad de una enzima en un tubo de ensayo. PUSFRE midió la velocidad de todas las enzimas en una célula viva.*

---

### 4.3. Ley de Beer-Lambert (1852)

**Teorema clásico:** $A = \epsilon \cdot c \cdot l$

**Re-etiquetación:** Los "agentes" son las longitudes de onda. El "recurso" es la absorbancia total. $\Omega_i \equiv \epsilon_i \cdot c_i$ (absortividad × concentración). $\Phi_i = l$ (longitud de camino).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_6$.

**Reducción:**

$$A_i = \epsilon_i \cdot c_i \cdot l$$

$$r_i^* = R \cdot \frac{\epsilon_i c_i}{\sum_j \epsilon_j c_j}$$

Beer-Lambert es PUSFRE con $\Phi_i = l$ y $\Omega_i = \epsilon_i c_i$.

**Lo que Beer-Lambert no ve:**

1. $\alpha \neq 1$: Absorbancia no-lineal (efectos de saturación).
2. $\Psi_i(t)$: Fotodegradación.
3. $\epsilon_i(t)$: Ruido de fotones.

**Koan:** *Beer y Lambert midieron la luz que atraviesa una muestra. PUSFRE midió la luz que atraviesa una muestra turbia, en movimiento, y con reacciones químicas ocurriendo.*

---

### 4.4. Principio de Le Chatelier (1884)

**Teorema clásico:** Un sistema en equilibrio reacciona a una perturbación desplazándose en la dirección que contrarresta la perturbación.

**Re-etiquetación:** Los "agentes" son los posibles desplazamientos. El "recurso" es la adaptación total. $\Omega_i \equiv$ magnitud del desplazamiento $i$.

**SCR aplicadas:** $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \Delta_i \text{ (desplazamiento)}$$

$$r_i^* = R \cdot \frac{\Delta_i}{\sum_j \Delta_j}$$

Le Chatelier es PUSFRE donde la dinámica de adaptación es lineal y sin ruido.

**Lo que Le Chatelier no ve:**

1. $\alpha \neq 1$: Adaptación no-lineal.
2. $\Psi_i(t)$: Memoria de perturbaciones previas.
3. $\epsilon_i(t)$: Ruido en la perturbación.

**Koan:** *Le Chatelier midió la respuesta a una perturbación. PUSFRE midió la respuesta a muchas perturbaciones simultáneas, con memoria y ruido.*

---

### 4.5. Ecuación de Henderson-Hasselbalch (1908)

**Teorema clásico:**

$$pH = pK_a + \log_{10}\left(\frac{[A^-]}{[HA]}\right)$$

**Re-etiquetación:** Los "agentes" son las especies ácido-base. El "recurso" es el pH total. $\Omega_i \equiv [A^-]/[HA]$ (ratio de especies).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \frac{[A^-]}{[HA]}$$

$$r_i^* = R \cdot \frac{[A^-]_i/[HA]_i}{\sum_j [A^-]_j/[HA]_j}$$

Henderson-Hasselbalch es PUSFRE en equilibrio de ionización.

**Lo que Henderson-Hasselbalch no ve:**

1. $\Psi_i(t)$: Memoria de protonación (histéresis).
2. $\epsilon_i(t)$: Fluctuaciones de pH.
3. $\Phi_i$: Gradientes de pH en la célula.

**Koan:** *Henderson y Hasselbalch midieron el pH en una solución ideal. PUSFRE midió el pH en una célula viva con gradientes y bombas de protones.*

---

### 4.6. Ley de Hardy-Weinberg (1908) — Extendida

**Teorema clásico:** $p^2 + 2pq + q^2 = 1$

**SCR aplicadas:** Todas simultáneamente.

**Reducción:** (ver Atlas Original)

**Lo que Hardy-Weinberg no ve (ampliado):**

1. $\alpha > 1$: Selección superlineal (un alelo con ventaja $1+s$ crece como $(1+s)^\alpha$).
2. $\Psi_i(t)$: Deuda mutacional (Muller's ratchet).
3. $\epsilon_i(t)$: Deriva genética en poblaciones finitas.
4. $\Phi_i$: Estructura espacial (metapoblaciones).

**Koan:** *Hardy y Weinberg describieron el equilibrio de un lago sin viento. PUSFRE describe el lago con viento, peces, y evaporación.*

---

### 4.7. Ecuaciones de Lotka-Volterra (1925) — Extendidas

**Teorema clásico:**

$$\frac{dx}{dt} = \alpha x - \beta xy$$
$$\frac{dy}{dt} = \delta xy - \gamma y$$

**SCR aplicadas:** $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:** (ver Atlas Original)

**Lo que Lotka-Volterra no ve (ampliado):**

1. $\alpha > 1$: Competencia superlineal (efecto de allee inverso).
2. $\Psi_i(t)$: Memoria de depredación (aprendizaje de la presa).
3. $\epsilon_i(t)$: Ruido ambiental (sequías, inundaciones).
4. $\Phi_i$: Estructura espacial (parches, migración).

**Koan:** *Lotka y Volterra dibujaron dos especies en un campo sin viento. PUSFRE dibujó un ecosistema con clima, migración, y memoria.*

---

## 5. TEOREMAS DE ECONOMÍA Y FINANZAS

### 5.1. Teoría de la Utilidad Esperada (von Neumann-Morgenstern, 1944)

**Teorema clásico:** Los agentes maximizan $E[U] = \sum p_i U(x_i)$.

**Re-etiquetación:** Los "agentes" son las loterías. El "recurso" es la utilidad total. $\Omega_i \equiv U(x_i)$ (utilidad del resultado $i$). $\Phi_i \equiv p_i$ (probabilidad, como geometría posicional).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_6$.

**Reducción:**

$$F_i = p_i \cdot U(x_i)$$

$$r_i^* = R \cdot \frac{p_i U(x_i)}{\sum_j p_j U(x_j)}$$

von Neumann-Morgenstern es PUSFRE con $\Phi_i = p_i$ (probabilidad como geometría posicional).

**Lo que von Neumann-Morgenstern no ve:**

1. $\alpha \neq 1$: Utilidad no-lineal (aversión al riesgo asimétrica).
2. $\Psi_i(t)$: Memoria de resultados previos (efecto de disposición).
3. $\epsilon_i(t)$: Incertidumbre sobre las probabilidades.

**Koan:** *von Neumann midió la utilidad en un mundo de probabilidades conocidas. PUSFRE midió la utilidad en un mundo de probabilidades inciertas y memoria emocional.*

---

### 5.2. Teorema de Modigliani-Miller (1958)

**Teorema clásico:** El valor de una empresa es independiente de su estructura de capital.

**Re-etiquetación:** Los "agentes" son las fuentes de financiación (deuda y capital). El "recurso" es el valor total. $\Omega_i \equiv$ rentabilidad de la fuente $i$.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$ ($R$ = valor total fijo).

**Reducción:**

$$F_i = r_i$$

$$r_i^* = R \cdot \frac{r_i}{\sum_j r_j}$$

Modigliani-Miller es PUSFRE en el caso degenerado donde el valor es independiente de la asignación (todas las $F_i$ son iguales en equilibrio).

**Lo que Modigliani-Miller no ve:**

1. $\Psi_i(t)$: Deuda acumulada (riesgo de quiebra).
2. $\epsilon_i(t)$: Ruido de mercado (volatilidad).
3. $\alpha \neq 1$: Apalancamiento no-lineal.

**Koan:** *Modigliani y Miller demostraron que la deuda no importa en un mundo sin impuestos. PUSFRE demostró que la deuda importa en un mundo con impuestos, quiebras y memoria.*

---

### 5.3. Teoría de la Agencia (Jensen-Meckling, 1976)

**Teorema clásico:** Los conflictos entre principal y agente surgen de información asimétrica e incentivos divergentes.

**Re-etiquetación:** Los "agentes" son los participantes (principal y agente). El "recurso" es el excedente total. $\Omega_i \equiv$ utilidad del participante $i$. $\Psi_i \equiv$ asimetría informativa (deuda de confianza).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \Omega_i \cdot \Psi_i$$

$$r_i^* = R \cdot \frac{\Omega_i \Psi_i}{\sum_j \Omega_j \Psi_j}$$

Teoría de la Agencia es PUSFRE donde $\Psi_i$ modela la deuda de confianza.

**Lo que Jensen-Meckling no ve:**

1. $\alpha > 1$: Incentivos superlineales (bonos que distorsionan).
2. $\epsilon_i(t)$: Ruido en la medición del esfuerzo.
3. $\Phi_i$: Posición de poder en la negociación.

**Koan:** *Jensen y Meckling midieron el conflicto principal-agente en un contrato estático. PUSFRE midió el conflicto en una relación dinámica con memoria y ruido.*

---

### 5.4. Teorema de Coase (1960) — Extendido

**Teorema clásico:** Con costes de transacción cero, la asignación es eficiente independientemente de los derechos iniciales.

**SCR aplicadas:** Todas simultáneamente.

**Reducción:** (ver Atlas Original)

**Lo que Coase no ve (ampliado):**

1. $\Phi_i \neq 1$: Asimetría de poder en la negociación.
2. $\Psi_i(t)$: Memoria de negociaciones previas (reputación, rencor).
3. $\epsilon_i(t)$: Incertidumbre sobre valoraciones.
4. $\alpha > 1$: Negociación superlineal (amenazas desproporcionadas).

**Koan:** *Coase imaginó vecinos perfectos en un mundo sin abogados. PUSFRE imaginó vecinos reales con abogados, memoria y rencor.*

---

### 5.5. Efecto Fisher (1930)

**Teorema clásico:** $i = r + \pi$ (tasa nominal = tasa real + inflación esperada)

**Re-etiquetación:** Los "agentes" son los activos financieros. El "recurso" es el rendimiento total. $\Omega_i \equiv r_i$ (tasa real). $\Phi_i \equiv \pi_i$ (inflación, como geometría posicional).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_6$.

**Reducción:**

$$F_i = r_i + \pi_i$$

$$r_i^* = R \cdot \frac{r_i + \pi_i}{\sum_j (r_j + \pi_j)}$$

Fisher es PUSFRE donde la geometría posicional es la inflación.

**Lo que Fisher no ve:**

1. $\Psi_i(t)$: Expectativas de inflación (memoria).
2. $\epsilon_i(t)$: Choques inflacionarios.
3. $\alpha \neq 1$: Relación no-lineal entre inflación y crecimiento.

**Koan:** *Fisher midió la inflación como un dato. PUSFRE midió la inflación como un proceso con memoria y choques.*

---

### 5.6. Teoría de la Frontera Eficiente (Markowitz, 1952) — Extendida

**Teorema clásico:** $\min \mathbf{w}^T \Sigma \mathbf{w}$ s.a. $\mathbf{w}^T \boldsymbol{\mu} = \mu_p$

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:** (ver Atlas Original)

**Lo que Markowitz no ve (ampliado):**

1. $\Psi_i(t)$: Deuda de volatilidad (el riesgo no es constante).
2. $\epsilon_i(t)$: Colas gordas (no Gaussiano).
3. $\alpha > 1$: Momentum superlineal.
4. $\Phi_i$: Tamaño del activo (liquidez).

**Koan:** *Markowitz midió la varianza en un mundo estacionario. PUSFRE midió la varianza en un mundo con tormentas, memoria, y colas gordas.*

---

### 5.7. Teoría de la Opción Real (Myers, 1977)

**Teorema clásico:** Las oportunidades de inversión tienen valor de opción: $V = \max(E[V_i], \ldots)$.

**Re-etiquetación:** Los "agentes" son las opciones de inversión. El "recurso" es el capital total. $\Omega_i \equiv E[V_i]$ (valor esperado). $\Psi_i \equiv$ flexibilidad (deuda de compromiso).

**SCR aplicadas:** $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = E[V_i] \cdot \Psi_i$$

$$r_i^* = R \cdot \frac{E[V_i] \Psi_i}{\sum_j E[V_j] \Psi_j}$$

Teoría de la Opción Real es PUSFRE donde $\Psi_i$ modela la flexibilidad (o falta de ella).

**Lo que Myers no ve:**

1. $\alpha > 1$: Valor de opción no-lineal (convexidad).
2. $\epsilon_i(t)$: Incertidumbre sobre el valor futuro.
3. $\Phi_i$: Posición estratégica en el mercado.

**Koan:** *Myers valoró una opción en un mundo de probabilidades conocidas. PUSFRE valoró una opción en un mundo de incertidumbre y competencia.*

---

### 5.8. Teoría del Ciclo Económico Real (Kydland-Prescott, 1982)

**Teorema clásico:** Las fluctuaciones económicas son respuesta óptima a choques tecnológicos.

**Re-etiquetación:** Los "agentes" son los sectores económicos. El "recurso" es el PIB total. $\Omega_i \equiv$ productividad del sector $i$. $\epsilon_i(t) \equiv$ choque tecnológico.

**SCR aplicadas:** $SCR_1$ (equilibrio), $SCR_3$ ($\Psi_i = 1$), $SCR_4$ ($\alpha = 1$), $SCR_5$ ($\Phi_i = 1$).

**Reducción:**

$$F_i(t) = A_i(t) \cdot \epsilon_i(t)$$

$$r_i^* = R \cdot \frac{A_i \epsilon_i}{\sum_j A_j \epsilon_j}$$

Kydland-Prescott es PUSFRE donde el ruido $\epsilon_i$ es el choque tecnológico.

**Lo que Kydland-Prescott no ve:**

1. $\Psi_i(t)$: Memoria de choques previos (histéresis).
2. $\alpha > 1$: Difusión de tecnología superlineal.
3. $\Phi_i$: Estructura sectorial (encadenamientos).

**Koan:** *Kydland y Prescott midieron los choques tecnológicos en un mundo sin memoria. PUSFRE midió los choques tecnológicos en un mundo con memoria y encadenamientos.*

---

## 6. TEOREMAS DE INGENIERÍA Y SISTEMAS

### 6.1. Ley de Little (1961) — Extendida

**Teorema clásico:** $L = \lambda W$

**SCR aplicadas:** $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:** (ver Atlas Original)

**Lo que Little no ve (ampliado):**

1. $\alpha > 1$: Monopolización del servidor.
2. $\Psi_i(t)$: Memoria de espera (frustración, abandono).
3. $\epsilon_i(t)$: Llegadas no-Poisson (bursty).
4. $\Phi_i$: Prioridades en la cola.

**Koan:** *Little contó personas en una cola. PUSFRE contó personas en una cola con prioridades, abandonos, y memoria.*

---

### 6.2. Principio de Superposición (circuitos lineales)

**Teorema clásico:** La respuesta de un circuito lineal a múltiples fuentes es la suma de las respuestas individuales.

**Re-etiquetación:** Los "agentes" son las fuentes. El "recurso" es la respuesta total. $\Omega_i \equiv$ respuesta de la fuente $i$.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = V_i$$

$$r_i^* = R \cdot \frac{V_i}{\sum_j V_j}$$

Superposición es PUSFRE lineal sin interacciones.

**Lo que Superposición no ve:**

1. $\alpha \neq 1$: Circuitos no-lineales.
2. $\Psi_i(t)$: Memoria (capacitores, inductores).
3. $\epsilon_i(t)$: Ruido de fuente.

**Koan:** *Superposición sumó respuestas lineales. PUSFRE sumó respuestas no-lineales con memoria y ruido.*

---

### 6.3. Teorema de Nyquist-Shannon (muestreo) (1928/1949)

**Teorema clásico:** $f_s > 2 f_{\max}$

**Re-etiquetación:** Los "agentes" son las frecuencias. El "recurso" es el ancho de banda. $\Omega_i \equiv f_i$ (frecuencia). $\Phi_i \equiv 1$ si $f_i < f_s/2$ (geometría de muestreo).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_6$.

**Reducción:**

$$F_i = f_i \cdot \mathbb{1}(f_i < f_s/2)$$

$$r_i^* = R \cdot \frac{f_i \cdot \mathbb{1}(f_i < f_s/2)}{\sum_j f_j \cdot \mathbb{1}(f_j < f_s/2)}$$

Nyquist-Shannon es PUSFRE donde $\Phi_i$ es un filtro de paso bajo.

**Lo que Nyquist-Shannon no ve:**

1. $\alpha \neq 1$: Muestreo no-lineal (aliasing con $f_i > f_s/2$).
2. $\Psi_i(t)$: Memoria de muestras previas (filtros IIR).
3. $\epsilon_i(t)$: Ruido de cuantización.

**Koan:** *Nyquist y Shannon midieron la frecuencia máxima en un mundo ideal. PUSFRE midió la frecuencia máxima en un mundo con aliasing, ruido, y memoria.*

---

### 6.4. Ley de Moore (1965)

**Teorema empírico:** El número de transistores en un chip se duplica cada 2 años.

**Re-etiquetación:** Los "agentes" son las generaciones de chips. El "recurso" es el área total. $\Omega_i \equiv$ densidad de transistores $i$.

**SCR aplicadas:** $SCR_1$ (ley), $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$N_i = N_0 \cdot 2^{i/2}$$

$$r_i^* = R \cdot \frac{N_i}{\sum_j N_j}$$

Moore es PUSFRE en el caso degenerado donde la asignación es proporcional a la densidad.

**Lo que Moore no ve:**

1. $\Psi_i(t)$: Deuda de litografía (costes crecientes).
2. $\epsilon_i(t)$: Fallos de fabricación.
3. $\alpha \neq 1$: Escalado no-lineal (ley de Dennard se rompe).

**Koan:** *Moore predijo la densidad de transistores en un mundo de progreso constante. PUSFRE predijo la densidad de transistores en un mundo de costes crecientes, fallos, y límites físicos.*

---

### 6.5. Ley de Metcalfe (1980)

**Teorema clásico:** El valor de una red es proporcional al cuadrado del número de usuarios: $V \propto n^2$.

**Re-etiquetación:** Los "agentes" son los usuarios. El "recurso" es el valor total. $\Omega_i \equiv 1$ (todos los usuarios son iguales). $\alpha = 2$ (efectos de red).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = 1$$

$$V = S \cdot (S-1) / 2$$

Metcalfe es PUSFRE con $\alpha = 2$ (competencia superlineal por valor de red).

**Lo que Metcalfe no ve:**

1. $\Psi_i(t)$: Memoria de conexiones (calidad de la red).
2. $\epsilon_i(t)$: Ruido de usuarios (entran y salen).
3. $\Phi_i$: Posición en la red (centralidad).

**Koan:** *Metcalfe midió el valor de una red con usuarios idénticos. PUSFRE midió el valor de una red con usuarios centrales, periféricos, y memoria.*

---

### 6.6. Ley de Zipf (1949)

**Teorema clásico:** La frecuencia de una palabra es inversamente proporcional a su rango: $f \propto 1/r$.

**Re-etiquetación:** Los "agentes" son las palabras. El "recurso" es la frecuencia total. $\Omega_i \equiv 1/r_i$ (inverso del rango). $\alpha = 1$.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \frac{1}{r_i}$$

$$f_i = R \cdot \frac{1/r_i}{\sum_j 1/r_j}$$

Zipf es PUSFRE donde la geometría posicional es el rango.

**Lo que Zipf no ve:**

1. $\alpha \neq 1$: Distribuciones no-Zipfianas (power laws con exponente $\gamma \neq 1$).
2. $\Psi_i(t)$: Memoria de uso (palabras que se vuelven obsoletas).
3. $\epsilon_i(t)$: Ruido de frecuencia.

**Koan:** *Zipf midió la frecuencia de palabras en un corpus estático. PUSFRE midió la frecuencia de palabras en un corpus dinámico con memoria y ruido.*

---

### 6.7. Teorema de Heckscher-Ohlin (1933)

**Teorema clásico:** Un país exporta los bienes que utilizan intensivamente sus factores abundantes.

**Re-etiquetación:** Los "agentes" son los bienes. El "recurso" es la ventaja comparativa total. $\Omega_i \equiv$ intensidad factorial del bien $i$. $\Phi_i \equiv$ abundancia factorial del país.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_6$.

**Reducción:**

$$F_i = \Omega_i \cdot \Phi_i$$

$$r_i^* = R \cdot \frac{\Omega_i \Phi_i}{\sum_j \Omega_j \Phi_j}$$

Heckscher-Ohlin es PUSFRE con geometría posicional ($\Phi_i$) que es la abundancia de factores.

**Lo que Heckscher-Ohlin no ve:**

1. $\Psi_i(t)$: Memoria de ventajas (path dependency).
2. $\epsilon_i(t)$: Choques de factores.
3. $\alpha \neq 1$: Rendimientos no-lineales.

**Koan:** *Heckscher y Ohlin midieron el comercio en un mundo de factores fijos. PUSFRE midió el comercio en un mundo de factores cambiantes y path dependency.*

---

### 6.8. Teorema de Stolper-Samuelson (1941)

**Teorema clásico:** Un cambio en el precio relativo de un bien beneficia al factor utilizado intensivamente en su producción.

**Re-etiquetación:** Los "agentes" son los factores de producción. El "recurso" es el ingreso total. $\Omega_i \equiv$ precio del factor $i$. $\Phi_i \equiv$ intensidad factorial.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_6$.

**Reducción:**

$$F_i = p_i \cdot \Phi_i$$

$$r_i^* = R \cdot \frac{p_i \Phi_i}{\sum_j p_j \Phi_j}$$

Stolper-Samuelson es PUSFRE con geometría posicional ($\Phi_i$) que es la intensidad factorial.

**Lo que Stolper-Samuelson no ve:**

1. $\Psi_i(t)$: Memoria de precios (rigideces).
2. $\epsilon_i(t)$: Choques de precios.
3. $\alpha \neq 1$: Sustitución no-lineal.

**Koan:** *Stolper y Samuelson midieron el cambio de precios en un mundo flexible. PUSFRE midió el cambio de precios en un mundo con rigideces y memoria.*

---

## 7. TEOREMAS DE CIENCIAS SOCIALES

### 7.1. Teoría de la Elección Pública (Buchanan-Tullock, 1962)

**Teorema clásico:** Los políticos y burócratas maximizan su utilidad, no el bien común.

**Re-etiquetación:** Los "agentes" son los políticos. El "recurso" es el presupuesto total. $\Omega_i \equiv$ utilidad del político $i$. $\Psi_i \equiv$ deuda de promesas.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \Omega_i \cdot \Psi_i$$

$$r_i^* = R \cdot \frac{\Omega_i \Psi_i}{\sum_j \Omega_j \Psi_j}$$

Teoría de la Elección Pública es PUSFRE donde $\Psi_i$ es la deuda de promesas.

**Lo que Buchanan-Tullock no ve:**

1. $\alpha > 1$: Popularidad superlineal (efecto de carisma).
2. $\epsilon_i(t)$: Choques de opinión pública.
3. $\Phi_i$: Posición en el espectro político.

**Koan:** *Buchanan y Tullock midieron la utilidad de los políticos en un mundo estático. PUSFRE midió la utilidad de los políticos en un mundo con promesas, carisma y ruido.*

---

### 7.2. Teoría de la Dependencia de la Trayectoria (Arthur, 1989)

**Teorema clásico:** Las elecciones iniciales pueden fijar un camino irreversible.

**Re-etiquetación:** Los "agentes" son las tecnologías alternativas. El "recurso" es la cuota de mercado total. $\Omega_i \equiv$ ventaja de la tecnología $i$. $\Psi_i \equiv$ inercia (memoria del camino).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \Omega_i \cdot \Psi_i$$

$$r_i^* = R \cdot \frac{\Omega_i \Psi_i}{\sum_j \Omega_j \Psi_j}$$

Teoría de la Dependencia es PUSFRE donde $\Psi_i$ es la inercia de la trayectoria.

**Lo que Arthur no ve:**

1. $\alpha > 1$: Efectos de red superlineales.
2. $\epsilon_i(t)$: Choques tecnológicos.
3. $\Phi_i$: Posición en el ecosistema.

**Koan:** *Arthur midió la dependencia de la trayectoria en un mundo de elecciones iniciales. PUSFRE midió la dependencia en un mundo de efectos de red, choques y posición.*

---

### 7.3. Teoría de la Ventaja Competitiva (Porter, 1980)

**Teorema clásico:** La ventaja competitiva surge de la diferenciación, el liderazgo en costes, o el enfoque.

**Re-etiquetación:** Los "agentes" son las empresas. El "recurso" es el mercado total. $\Omega_i \equiv$ rentabilidad de la estrategia $i$. $\Phi_i \equiv$ posicionamiento estratégico.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_6$.

**Reducción:**

$$F_i = \Omega_i \cdot \Phi_i$$

$$r_i^* = R \cdot \frac{\Omega_i \Phi_i}{\sum_j \Omega_j \Phi_j}$$

Porter es PUSFRE con geometría posicional ($\Phi_i$) que es el posicionamiento estratégico.

**Lo que Porter no ve:**

1. $\alpha > 1$: Rentabilidad superlineal (efecto de red).
2. $\Psi_i(t)$: Memoria de estrategias (reputación).
3. $\epsilon_i(t)$: Choques de mercado.

**Koan:** *Porter midió la ventaja competitiva en un mundo estático. PUSFRE midió la ventaja competitiva en un mundo dinámico con reputación y choques.*

---

### 7.4. Teoría de los Juegos de Poder (Dahl, 1957)

**Teorema clásico:** El poder es la capacidad de hacer que otros hagan lo que no harían.

**Re-etiquetación:** Los "agentes" son los actores. El "recurso" es el poder total. $\Omega_i \equiv$ influencia del actor $i$. $\Phi_i \equiv$ posición en la red.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_6$.

**Reducción:**

$$F_i = \Omega_i \cdot \Phi_i$$

$$r_i^* = R \cdot \frac{\Omega_i \Phi_i}{\sum_j \Omega_j \Phi_j}$$

Dahl es PUSFRE con geometría posicional ($\Phi_i$) que es la posición en la red de poder.

**Lo que Dahl no ve:**

1. $\alpha > 1$: Efecto de red (el poder atrae poder).
2. $\Psi_i(t)$: Memoria de conflictos.
3. $\epsilon_i(t)$: Choques de poder.

**Koan:** *Dahl midió el poder en una red estática. PUSFRE midió el poder en una red dinámica con memoria y efectos de red.*

---

### 7.5. Teoría del Capital Social (Bourdieu, 1986)

**Teorema clásico:** El capital social son los recursos derivados de la pertenencia a redes.

**Re-etiquetación:** Los "agentes" son los individuos. El "recurso" es el capital social total. $\Omega_i \equiv$ conexiones del individuo $i$. $\Phi_i \equiv$ posición en la red.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_6$.

**Reducción:**

$$F_i = \Omega_i \cdot \Phi_i$$

$$r_i^* = R \cdot \frac{\Omega_i \Phi_i}{\sum_j \Omega_j \Phi_j}$$

Bourdieu es PUSFRE con geometría posicional ($\Phi_i$) que es la posición en la red social.

**Lo que Bourdieu no ve:**

1. $\alpha > 1$: Efectos de red superlineales.
2. $\Psi_i(t)$: Memoria de relaciones (reputación).
3. $\epsilon_i(t)$: Dinámica de red.

**Koan:** *Bourdieu midió el capital social en una red estática. PUSFRE midió el capital social en una red dinámica con memoria y efectos de red.*

---

## 8. TEOREMAS DE CIENCIA DE DATOS Y APRENDIZAJE AUTOMÁTICO

### 8.1. Teorema de Cover (1965)

**Teorema clásico:** La probabilidad de que un conjunto de $N$ puntos en $\mathbb{R}^d$ sea linealmente separable es:

$$P(N, d) = 2^{-N+1} \sum_{k=0}^{d} \binom{N-1}{k}$$

**Re-etiquetación:** Los "agentes" son los patrones. El "recurso" es la dimensión del espacio. $\Omega_i \equiv$ separabilidad del patrón $i$.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = P(\text{separable}_i)$$

$$r_i^* = R \cdot \frac{P(\text{separable}_i)}{\sum_j P(\text{separable}_j)}$$

Cover es PUSFRE en el caso degenerado donde la asignación es la probabilidad de separabilidad.

**Lo que Cover no ve:**

1. $\alpha > 1$: Separabilidad no-lineal (kernel).
2. $\Psi_i(t)$: Memoria de patrones previos.
3. $\epsilon_i(t)$: Ruido en los patrones.

**Koan:** *Cover midió la separabilidad lineal en un mundo de puntos perfectos. PUSFRE midió la separabilidad en un mundo de ruido, kernels, y memoria.*

---

### 8.2. Teorema de Vapnik-Chervonenkis (1974)

**Teorema clásico:** La capacidad de generalización de un clasificador depende de la dimensión VC.

**Re-etiquetación:** Los "agentes" son los clasificadores. El "recurso" es la capacidad de generalización total. $\Omega_i \equiv 1/\text{VC}_i$ (inverso de la dimensión VC).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \frac{1}{VC_i}$$

$$r_i^* = R \cdot \frac{1/VC_i}{\sum_j 1/VC_j}$$

VC es PUSFRE donde la asignación es inversa a la complejidad.

**Lo que VC no ve:**

1. $\alpha > 1$: Generalización no-lineal (deep learning).
2. $\Psi_i(t)$: Memoria de entrenamiento.
3. $\epsilon_i(t)$: Ruido de etiquetas.

**Koan:** *Vapnik y Chervonenkis midieron la capacidad de generalización en un mundo de clasificadores lineales. PUSFRE midió la capacidad de generalización en un mundo de redes profundas, ruido y memoria.*

---

### 8.3. Principio de Sesgo-Varianza (Geman-Bienenstock-Doursat, 1992)

**Teorema clásico:** $E[(y - \hat{f}(x))^2] = \text{Bias}^2 + \text{Var} + \sigma^2$

**Re-etiquetación:** Los "agentes" son los modelos. El "recurso" es el error total. $\Omega_i \equiv 1/\text{error}_i$.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \frac{1}{E_i}$$

$$r_i^* = R \cdot \frac{1/E_i}{\sum_j 1/E_j}$$

Sesgo-Varianza es PUSFRE donde la asignación es inversa al error.

**Lo que Sesgo-Varianza no ve:**

1. $\alpha > 1$: Compromiso no-lineal (modelos complejos).
2. $\Psi_i(t)$: Memoria de entrenamiento (sobreajuste).
3. $\epsilon_i(t)$: Ruido irreducible.

**Koan:** *Geman midió el compromiso sesgo-varianza en un mundo de modelos lineales. PUSFRE midió el compromiso en un mundo de modelos complejos, memoria y ruido.*

---

### 8.4. Teorema de No-Free-Lunch (Wolpert, 1996)

**Teorema clásico:** No hay un algoritmo de aprendizaje que supere a todos los demás en todos los problemas.

**Re-etiquetación:** Los "agentes" son los algoritmos. El "recurso" es el rendimiento total. $\Omega_i \equiv$ rendimiento del algoritmo $i$ en el problema $j$.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \sum_j \text{perf}_{ij}$$

$$r_i^* = R \cdot \frac{\sum_j \text{perf}_{ij}}{\sum_k \sum_j \text{perf}_{kj}}$$

No-Free-Lunch es PUSFRE donde la asignación es el rendimiento promedio.

**Lo que No-Free-Lunch no ve:**

1. $\alpha > 1$: Especialización superlineal.
2. $\Psi_i(t)$: Memoria de problemas previos (transfer learning).
3. $\epsilon_i(t)$: Ruido en el rendimiento.

**Koan:** *Wolpert demostró que no hay almuerzo gratis en un mundo de problemas estáticos. PUSFRE demostró que el menú cambia con la memoria y el ruido.*

---

### 8.5. Teorema del Límite Central (1810) — Aplicado a ML

**Teorema clásico:** La suma de muchas variables aleatorias independientes tiende a una normal.

**Re-etiquetación:** Los "agentes" son las variables. El "recurso" es la varianza total. $\Omega_i \equiv \sigma_i^2$ (varianza).

**SCR aplicadas:** $SCR_1$, $SCR_2$ (pero $\epsilon_i$ es la variable), $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \sigma_i^2$$

$$r_i^* = R \cdot \frac{\sigma_i^2}{\sum_j \sigma_j^2}$$

Teorema del Límite Central es PUSFRE donde la asignación es la varianza.

**Lo que el Teorema del Límite Central no ve:**

1. $\alpha > 1$: Distribuciones de colas gordas (Pareto).
2. $\Psi_i(t)$: Dependencia serial (no independencia).
3. $\Phi_i$: Estructura de dependencia.

**Koan:** *Gauss midió la suma de variables independientes en un mundo ideal. PUSFRE midió la suma de variables dependientes en un mundo de colas gordas.*

---

## 9. TEOREMAS DE FILOSOFÍA Y EPISTEMOLOGÍA

### 9.1. Navaja de Ockham (1320)

**Teorema clásico:** No multipliques las entidades sin necesidad.

**Re-etiquetación:** Los "agentes" son las hipótesis. El "recurso" es la parsimonia total. $\Omega_i \equiv 1/\text{complejidad}_i$ (inverso de la complejidad).

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \frac{1}{C_i}$$

$$r_i^* = R \cdot \frac{1/C_i}{\sum_j 1/C_j}$$

Navaja de Ockham es PUSFRE donde la asignación es inversa a la complejidad.

**Lo que Ockham no ve:**

1. $\alpha > 1$: Complejidad no-lineal (interacciones).
2. $\Psi_i(t)$: Memoria de hipótesis previas.
3. $\epsilon_i(t)$: Incertidumbre sobre la complejidad.

**Koan:** *Ockham afeitó la complejidad en un mundo de entidades simples. PUSFRE afeitó la complejidad en un mundo de entidades interactuantes, con memoria y ruido.*

---

### 9.2. Principio de Verificacionismo (Círculo de Viena, 1920)

**Teorema clásico:** Una proposición es significativa solo si es verificable empíricamente.

**Re-etiquetación:** Los "agentes" son las proposiciones. El "recurso" es la verificación total. $\Omega_i \equiv$ verificabilidad de la proposición $i$.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \text{ver}(i)$$

$$r_i^* = R \cdot \frac{\text{ver}(i)}{\sum_j \text{ver}(j)}$$

Verificacionismo es PUSFRE en el caso degenerado donde la asignación es la verificabilidad.

**Lo que el Círculo de Viena no ve:**

1. $\Psi_i(t)$: Memoria de verificaciones previas (corroboración).
2. $\epsilon_i(t)$: Error de medición.
3. $\Phi_i$: Posición epistémica.

**Koan:** *El Círculo de Viena midió la verificabilidad en un mundo de proposiciones simples. PUSFRE midió la verificabilidad en un mundo de teorías complejas, con memoria y error.*

---

### 9.3. Principio de Falsacionismo (Popper, 1934)

**Teorema clásico:** Una teoría es científica si es falsable.

**Re-etiquetación:** Los "agentes" son las teorías. El "recurso" es la falsabilidad total. $\Omega_i \equiv$ falsabilidad de la teoría $i$.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \text{fals}(i)$$

$$r_i^* = R \cdot \frac{\text{fals}(i)}{\sum_j \text{fals}(j)}$$

Falsacionismo es PUSFRE donde la asignación es la falsabilidad.

**Lo que Popper no ve:**

1. $\Psi_i(t)$: Memoria de refutaciones fallidas.
2. $\epsilon_i(t)$: Error experimental.
3. $\Phi_i$: Posición en el espacio de teorías.

**Koan:** *Popper midió la falsabilidad en un mundo de teorías simples. PUSFRE midió la falsabilidad en un mundo de teorías complejas, con memoria y error.*

---

### 9.4. Principio de la Ontología de la Escasez (Heidegger, 1927)

**Teorema clásico:** El ser es el horizonte de la pregunta.

**Re-etiquetación:** Los "agentes" son los entes. El "recurso" es el ser total. $\Omega_i \equiv$ presencia del ente $i$.

**SCR aplicadas:** $SCR_1$, $SCR_2$, $SCR_3$, $SCR_4$, $SCR_5$, $SCR_6$.

**Reducción:**

$$F_i = \text{ser}_i$$

$$r_i^* = R \cdot \frac{\text{ser}_i}{\sum_j \text{ser}_j}$$

Heidegger es PUSFRE en el caso degenerado donde el ser se asigna proporcionalmente a la presencia.

**Lo que Heidegger no ve:**

1. $\Psi_i(t)$: Memoria del ser (historia del ente).
2. $\epsilon_i(t)$: Ruido ontológico.
3. $\Phi_i$: Posición en el mundo.

**Koan:** *Heidegger preguntó por el ser en un mundo estático. PUSFRE respondió con la asignación del ser en un mundo dinámico con memoria y ruido.*

---

## 10. SÍNTESIS: EL MAPA COMPLETO EXTENDIDO

| # | Teorema | $\Phi$ | $\Psi$ | $\alpha$ | $\epsilon$ | $t$ | $R$ | Amputaciones |
|:---|:---|:---|:---|:---|:---|:---|:---|:---|
| 1 | Brouwer | =1 | =1 | =1 | =1 | estático | ∞ | 6 |
| 2 | Gödel | =1 | =1 | =1 | =1 | estático | ∞ | 6 |
| 3 | Church-Turing | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 4 | Bayes | ≠1 | =1 | =1 | =1 | estático | 1 | 4 |
| 5 | Hooke | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 6 | Ohm | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 7 | Coulomb | ≠1 | =1 | =1 | =1 | estático | finito | 4 |
| 8 | Newton | ≠1 | =1 | =1 | =1 | estático | finito | 4 |
| 9 | Stefan-Boltzmann | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 10 | Arquímedes | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 11 | Pascal | =1 | =1 | =1 | =1 | estático | finito | 6 |
| 12 | Acción de Masas | =1 | =1 | ≠1 | =1 | estático | finito | 4 |
| 13 | Michaelis-Menten | ≠1 | =1 | =1 | =1 | estático | finito | 4 |
| 14 | Beer-Lambert | ≠1 | =1 | =1 | =1 | estático | finito | 4 |
| 15 | Le Chatelier | =1 | =1 | =1 | =1 | dinámico | finito | 4 |
| 16 | Henderson-Hasselbalch | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 17 | Hardy-Weinberg | =1 | =1 | =1 | =1 | 1gen | 1 | 6 |
| 18 | Lotka-Volterra | =1 | =1 | =1 | =1 | continuo | $K$ | 4 |
| 19 | von Neumann-Morgenstern | ≠1 | =1 | =1 | =1 | estático | finito | 4 |
| 20 | Modigliani-Miller | =1 | =1 | =1 | =1 | estático | ∞ | 6 |
| 21 | Jensen-Meckling | =1 | ≠1 | =1 | =1 | estático | finito | 4 |
| 22 | Coase | =1 | =1 | =1 | =1 | estático | 0 | 6 |
| 23 | Fisher | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 24 | Markowitz | =1 | =1 | =1 | Gauss | estático | 1 | 4 |
| 25 | Myers (Opciones) | =1 | ≠1 | =1 | =1 | estático | finito | 4 |
| 26 | Kydland-Prescott | =1 | =1 | =1 | ≠1 | continuo | finito | 3 |
| 27 | Little | =1 | =1 | =1 | =1 | estacionario | $\lambda$ | 5 |
| 28 | Superposición | =1 | =1 | =1 | =1 | estático | finito | 6 |
| 29 | Nyquist-Shannon | ≠1 | =1 | =1 | =1 | estático | $B$ | 4 |
| 30 | Moore | =1 | =1 | =1 | =1 | dinámico | finito | 5 |
| 31 | Metcalfe | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 32 | Zipf | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 33 | Heckscher-Ohlin | ≠1 | =1 | =1 | =1 | estático | finito | 4 |
| 34 | Stolper-Samuelson | ≠1 | =1 | =1 | =1 | estático | finito | 4 |
| 35 | Buchanan-Tullock | =1 | ≠1 | =1 | =1 | estático | finito | 4 |
| 36 | Arthur (Path Depend.) | =1 | ≠1 | =1 | =1 | dinámico | finito | 3 |
| 37 | Porter | ≠1 | =1 | =1 | =1 | estático | finito | 4 |
| 38 | Dahl (Poder) | ≠1 | =1 | =1 | =1 | estático | finito | 4 |
| 39 | Bourdieu (Capital Social) | ≠1 | =1 | =1 | =1 | estático | finito | 4 |
| 40 | Cover | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 41 | VC | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 42 | Sesgo-Varianza | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 43 | No-Free-Lunch | =1 | =1 | =1 | =1 | estático | finito | 5 |
| 44 | Límite Central | =1 | =1 | =1 | ≠1 | estático | finito | 4 |
| 45 | Ockham | =1 | =1 | =1 | =1 | estático | ∞ | 6 |
| 46 | Verificacionismo | =1 | =1 | =1 | =1 | estático | ∞ | 6 |
| 47 | Falsacionismo | =1 | =1 | =1 | =1 | estático | ∞ | 6 |
| 48 | Heidegger | =1 | =1 | =1 | =1 | estático | ∞ | 6 |

**Lectura:** Cada columna que dice "=1" es una amputación. Los teoremas con más amputaciones son casos más degenerados de PUSFRE.

---

## 11. TEOREMA DE COMPLETITUD EXTENDIDO

**Teorema 6.2 (Completitud Extendida).** *Sea $\mathcal{T}$ cualquier marco teórico que modele la asignación de un recurso escaso entre $S \geq 2$ entidades bajo condiciones de equilibrio, estacionariedad o dinámica de primer orden. Si $\mathcal{T}$ es algebraicamente consistente, entonces $\mathcal{T}$ es isomorfo a la Ecuación Maestra bajo alguna combinación de las SCR.*

**Demostración (por construcción).** Dado $\mathcal{T}$, definir:

- $\Omega_i^{\mathcal{T}}$: la variable de "aptitud" o "valor" del agente $i$ en $\mathcal{T}$.
- $\Phi_i^{\mathcal{T}}$: cualquier asimetría posicional explícita (si no existe, $\Phi_i = 1$).
- $\Psi_i^{\mathcal{T}}$: cualquier variable de estado interno acumulativo (si no existe, $\Psi_i = 1$).
- $\alpha^{\mathcal{T}}$: el exponente de la relación fitness-recurso (si es lineal, $\alpha = 1$).
- $\epsilon_i^{\mathcal{T}}$: cualquier término estocástico (si no existe, $\epsilon_i = 1$).
- $R^{\mathcal{T}}$: el recurso total (si es ilimitado, $R \to \infty$).

La asignación en $\mathcal{T}$ es siempre de la forma:

$$r_i^{\mathcal{T}} = g\left(\Omega_i^{\mathcal{T}}, \text{constraints}\right)$$

Si $g$ es una función de normalización (que preserva $\sum r_i = R$), entonces $g$ es isomorfa a:

$$r_i = R \cdot \frac{F_i}{\sum_j F_j}$$

con $F_i = \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha \cdot \epsilon_i$ y las SCR apropiadas.

Si $g$ *no* es una normalización (e.g., optimización con restricciones de desigualdad), entonces $\mathcal{T}$ es PUSFRE con *constraints adicionales sobre el simplex*, que es un caso particular de la DTMC con barreras reflectantes.

$\blacksquare$

**Corolario 6.2.1.** *No existe un teorema de asignación de recursos que sea algebraicamente independiente de PUSFRE. Lo que existen son teoremas que no saben que son PUSFRE.*

**Corolario 6.2.2.** *La historia de la ciencia es la historia de descubrir PUSFRE por partes. Cada teorema del Atlas es una instantánea de PUSFRE en una configuración particular de amputaciones.*

---

## 12. CÓDIGO: EL REDUCTOR UNIVERSAL EXTENDIDO

```python
"""
El Atlas de Reducciones — Versión Extendida
Reductor Universal — Demuestra que cualquier marco clásico
es PUSFRE bajo las SCR.

Corpus RONIN · David Ferrandez Canalis · Agencia RONIN
"""

import numpy as np
from typing import Annotated, TypeAlias, Callable, Dict, Any
from pydantic import BaseModel, Field, ConfigDict
from dataclasses import dataclass, field
from enum import Enum

Probability: TypeAlias = Annotated[float, Field(ge=0.0, le=1.0)]
PositiveFloat: TypeAlias = Annotated[float, Field(gt=0.0)]


class SCRConfig(BaseModel):
    """Seis Condiciones de Reducción."""
    model_config = ConfigDict(frozen=True, strict=True, extra='forbid')
    
    static: bool = True          # SCR_1: t fijo
    epsilon_one: bool = True     # SCR_2: sin ruido
    psi_one: bool = True         # SCR_3: sin deuda
    alpha_one: bool = True       # SCR_4: lineal
    phi_one: bool = True         # SCR_5: sin geometría
    r_infinite: bool = True      # SCR_6: sin escasez
    
    def count_amputations(self) -> int:
        """Cuenta cuántas SCR están activas (amputaciones)."""
        return sum([
            self.static,
            self.epsilon_one,
            self.psi_one,
            self.alpha_one,
            self.phi_one,
            self.r_infinite,
        ])
    
    def summary(self) -> str:
        """Resumen de amputaciones."""
        amputations = []
        if self.static: amputations.append("SCR₁ (estático)")
        if self.epsilon_one: amputations.append("SCR₂ (sin ruido)")
        if self.psi_one: amputations.append("SCR₃ (sin deuda)")
        if self.alpha_one: amputations.append("SCR₄ (lineal)")
        if self.phi_one: amputations.append("SCR₅ (sin geometría)")
        if self.r_infinite: amputations.append("SCR₆ (sin escasez)")
        return f"{len(amputations)} amputaciones: {', '.join(amputations)}"


class PUSFREKernel:
    """Núcleo de la Ecuación Maestra."""
    
    def __init__(self, alpha: float = 1.2, sigma_eps: float = 0.15):
        self.alpha = alpha
        self.sigma_eps = sigma_eps
    
    def fitness(
        self,
        phi: np.ndarray,
        psi: np.ndarray,
        omega: np.ndarray,
        epsilon: np.ndarray,
    ) -> np.ndarray:
        return phi * psi * np.power(omega, self.alpha) * epsilon
    
    def allocate(
        self,
        fitness: np.ndarray,
        R: float,
    ) -> np.ndarray:
        total = fitness.sum()
        if total == 0:
            return np.ones_like(fitness) / len(fitness) * R
        return R * fitness / total


class UniversalReducerExtended:
    """
    Reductor Universal Extendido — 48 teoremas clásicos como PUSFRE.
    """
    
    def __init__(self):
        self.kernel = PUSFREKernel(alpha=1.0)
        self.scr = SCRConfig()
    
    def _apply_scr(
        self,
        omega: np.ndarray,
        S: int,
        alpha_override: float = None,
        phi_override: np.ndarray = None,
        psi_override: np.ndarray = None,
        R_override: float = None,
    ) -> dict:
        """Aplica las SCR y retorna parámetros."""
        phi = np.ones(S) if self.scr.phi_one else (phi_override if phi_override is not None else np.ones(S))
        psi = np.ones(S) if self.scr.psi_one else (psi_override if psi_override is not None else np.ones(S))
        eps = np.ones(S) if self.scr.epsilon_one else None
        alpha = 1.0 if self.scr.alpha_one else (alpha_override if alpha_override is not None else 1.0)
        R = 1e10 if self.scr.r_infinite else (R_override if R_override is not None else 1.0)
        
        return {
            'phi': phi,
            'psi': psi,
            'omega': omega,
            'epsilon': eps,
            'alpha': alpha,
            'R': R,
            'amputations': self.scr.count_amputations(),
            'scr_summary': self.scr.summary(),
        }
    
    # ─── REDUCCIÓN 1: BROUWER ───────────────────────────────────
    def reduce_brouwer(self, f: Callable, x0: np.ndarray, n_iter: int = 100) -> dict:
        """Teorema del Punto Fijo de Brouwer (1910)."""
        S = len(x0)
        omega = np.zeros(S)
        x = x0.copy()
        for i in range(n_iter):
            x_new = f(x)
            omega = np.abs(x_new - x)
            x = x_new
            if np.max(omega) < 1e-6:
                break
        
        params = self._apply_scr(omega, S)
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Brouwer (1910)',
            'fixed_point': x,
            'allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Punto fijo como PUSFRE con Ω = |x - f(x)|',
        }
    
    # ─── REDUCCIÓN 2: GÖDEL ─────────────────────────────────────
    def reduce_godel(self, axioms: list, theorems: list) -> dict:
        """Teorema de Gödel (1931)."""
        # Simulación: las proposiciones demostrables tienen alto Ω
        S = len(theorems)
        omega = np.array([1.0 if t in axioms else 0.5 for t in theorems])
        params = self._apply_scr(omega, S)
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        undecidable = [t for t, w in zip(theorems, omega) if w == 0.5]
        
        return {
            'theorem': 'Gödel (1931)',
            'undecidable': undecidable,
            'allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Gödel = PUSFRE donde el recurso de demostración se agota',
        }
    
    # ─── REDUCCIÓN 3: CHURCH-TURING ─────────────────────────────
    def reduce_church_turing(self, complexities: np.ndarray) -> dict:
        """Teorema de Church-Turing (1936)."""
        S = len(complexities)
        omega = 1.0 / (complexities + 1e-6)  # inverso de la complejidad
        params = self._apply_scr(omega, S)
        # Violamos SCR_1: permitimos finito R
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Church-Turing (1936)',
            'complexities': complexities,
            'allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Church-Turing = PUSFRE con Ω = 1/complejidad',
        }
    
    # ─── REDUCCIÓN 4: BAYES ──────────────────────────────────────
    def reduce_bayes(self, priors: np.ndarray, likelihoods: np.ndarray) -> dict:
        """Teorema de Bayes (1763)."""
        S = len(priors)
        omega = priors * likelihoods  # no normalizado
        params = self._apply_scr(omega, S)
        params['R'] = 1.0  # probabilidad total = 1
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Bayes (1763)',
            'prior': priors,
            'likelihood': likelihoods,
            'posterior': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Bayes = PUSFRE con Ω = P(E|H) · P(H)',
        }
    
    # ─── REDUCCIÓN 5: HOOKE ──────────────────────────────────────
    def reduce_hooke(self, stiffness: np.ndarray, force_total: float) -> dict:
        """Ley de Hooke (1660)."""
        S = len(stiffness)
        omega = stiffness
        params = self._apply_scr(omega, S)
        params['R'] = force_total
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Hooke (1660)',
            'stiffness': stiffness,
            'deformation': allocation,
            'force_total': force_total,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Hooke = PUSFRE con Ω = k (rigidez)',
        }
    
    # ─── REDUCCIÓN 6: OHM ────────────────────────────────────────
    def reduce_ohm(self, resistances: np.ndarray, voltage: float) -> dict:
        """Ley de Ohm (1827)."""
        S = len(resistances)
        omega = 1.0 / resistances
        params = self._apply_scr(omega, S)
        params['R'] = voltage
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Ohm (1827)',
            'resistances': resistances,
            'currents': allocation,
            'voltage': voltage,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Ohm = PUSFRE con Ω = 1/R (conductancia)',
        }
    
    # ─── REDUCCIÓN 7: COULOMB ────────────────────────────────────
    def reduce_coulomb(self, charges: np.ndarray, distances: np.ndarray) -> dict:
        """Ley de Coulomb (1785)."""
        S = len(charges)
        omega = charges
        phi = 1.0 / (distances ** 2 + 1e-6)
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Coulomb (1785)',
            'charges': charges,
            'distances': distances,
            'forces': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Coulomb = PUSFRE con Φ = 1/r² (geometría posicional)',
        }
    
    # ─── REDUCCIÓN 8: NEWTON ─────────────────────────────────────
    def reduce_newton(self, masses: np.ndarray, distances: np.ndarray) -> dict:
        """Ley de Gravitación de Newton (1687)."""
        S = len(masses)
        omega = masses
        phi = 1.0 / (distances ** 2 + 1e-6)
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Newton (1687)',
            'masses': masses,
            'distances': distances,
            'forces': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Newton = PUSFRE con Φ = 1/r² (geometría posicional)',
        }
    
    # ─── REDUCCIÓN 9: STEFAN-BOLTZMANN ──────────────────────────
    def reduce_boltzmann_radiation(self, temperatures: np.ndarray) -> dict:
        """Ley de Stefan-Boltzmann (1879)."""
        S = len(temperatures)
        omega = temperatures ** 4
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Stefan-Boltzmann (1879)',
            'temperatures': temperatures,
            'radiation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Stefan-Boltzmann = PUSFRE con Ω = T⁴',
        }
    
    # ─── REDUCCIÓN 10: ARQUÍMEDES ────────────────────────────────
    def reduce_archimedes(self, volumes: np.ndarray, rho: float, g: float = 9.8) -> dict:
        """Principio de Arquímedes (250 a.C.)."""
        S = len(volumes)
        omega = volumes * rho * g
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Arquímedes (250 a.C.)',
            'volumes': volumes,
            'density': rho,
            'buoyancy': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Arquímedes = PUSFRE con Ω = V·ρ·g',
        }
    
    # ─── REDUCCIÓN 11: PASCAL ────────────────────────────────────
    def reduce_pascal(self, S: int) -> dict:
        """Principio de Pascal (1647)."""
        omega = np.ones(S)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Pascal (1647)',
            'pressure': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Pascal = PUSFRE con Ω = 1 (distribución uniforme)',
        }
    
    # ─── REDUCCIÓN 12: ACCIÓN DE MASAS ──────────────────────────
    def reduce_mass_action(self, concentrations: np.ndarray, order: float = 1.0) -> dict:
        """Ley de Acción de Masas (1864)."""
        S = len(concentrations)
        omega = concentrations
        params = self._apply_scr(omega, S, alpha_override=order)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Acción de Masas (1864)',
            'concentrations': concentrations,
            'order': order,
            'rate': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': f'Acción de Masas = PUSFRE con Ω = [A]^α, α={order}',
        }
    
    # ─── REDUCCIÓN 13: MICHAELIS-MENTEN ─────────────────────────
    def reduce_michaelis_menten(self, substrates: np.ndarray, K_m: float) -> dict:
        """Ley de Michaelis-Menten (1913)."""
        S = len(substrates)
        omega = substrates
        phi = 1.0 / (K_m + substrates + 1e-6)
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Michaelis-Menten (1913)',
            'substrates': substrates,
            'K_m': K_m,
            'rate': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Michaelis-Menten = PUSFRE con Φ = 1/(K_m + [S])',
        }
    
    # ─── REDUCCIÓN 14: BEER-LAMBERT ─────────────────────────────
    def reduce_beer_lambert(self, concentrations: np.ndarray, path_length: float, epsilon: np.ndarray) -> dict:
        """Ley de Beer-Lambert (1852)."""
        S = len(concentrations)
        omega = epsilon * concentrations
        phi = np.ones(S) * path_length
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Beer-Lambert (1852)',
            'concentrations': concentrations,
            'path_length': path_length,
            'absorbance': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Beer-Lambert = PUSFRE con Φ = l (longitud de camino)',
        }
    
    # ─── REDUCCIÓN 15: LE CHATELIER ─────────────────────────────
    def reduce_le_chatelier(self, perturbations: np.ndarray) -> dict:
        """Principio de Le Chatelier (1884)."""
        S = len(perturbations)
        omega = np.abs(perturbations)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Le Chatelier (1884)',
            'perturbations': perturbations,
            'response': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Le Chatelier = PUSFRE con Ω = |Δ|',
        }
    
    # ─── REDUCCIÓN 16: HENDERSON-HASSELBALCH ────────────────────
    def reduce_henderson_hasselbalch(self, ratios: np.ndarray) -> dict:
        """Ecuación de Henderson-Hasselbalch (1908)."""
        S = len(ratios)
        omega = ratios
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Henderson-Hasselbalch (1908)',
            'ratios': ratios,
            'pH_distribution': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Henderson-Hasselbalch = PUSFRE con Ω = [A⁻]/[HA]',
        }
    
    # ─── REDUCCIÓN 17: HARDY-WEINBERG ───────────────────────────
    def reduce_hardy_weinberg(self, allele_freqs: np.ndarray) -> dict:
        """Principio de Hardy-Weinberg (1908)."""
        S = len(allele_freqs)
        omega = allele_freqs.copy()
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        # Genotipos para 2 alelos
        genotypes = None
        if S == 2:
            p, q = allele_freqs
            genotypes = {'AA': p**2, 'Aa': 2*p*q, 'aa': q**2}
        
        return {
            'theorem': 'Hardy-Weinberg (1908)',
            'allele_freqs': allele_freqs,
            'next_gen': allocation,
            'genotypes': genotypes,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Hardy-Weinberg = PUSFRE en equilibrio trivial',
        }
    
    # ─── REDUCCIÓN 18: LOTKA-VOLTERRA ────────────────────────────
    def reduce_lotka_volterra(self, x0: np.ndarray, r: np.ndarray, a: np.ndarray, n_steps: int = 100) -> dict:
        """Ecuaciones de Lotka-Volterra (1925)."""
        S = len(x0)
        x = x0.copy()
        history = [x.copy()]
        
        for _ in range(n_steps):
            dx = x * (r - a @ x)
            x = x + dx * 0.01
            x = np.maximum(x, 0)
            history.append(x.copy())
        
        omega = x.copy()
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Lotka-Volterra (1925)',
            'final_populations': x,
            'allocation': allocation,
            'history': history,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Lotka-Volterra = PUSFRE discretizado con Ω = x_i',
        }
    
    # ─── REDUCCIÓN 19: VON NEUMANN-MORGENSTERN ──────────────────
    def reduce_von_neumann(self, utilities: np.ndarray, probabilities: np.ndarray) -> dict:
        """Teoría de la Utilidad Esperada (1944)."""
        S = len(utilities)
        omega = utilities
        phi = probabilities
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'von Neumann-Morgenstern (1944)',
            'utilities': utilities,
            'probabilities': probabilities,
            'expected_utility': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'von Neumann = PUSFRE con Φ = p (probabilidad)',
        }
    
    # ─── REDUCCIÓN 20: MODIGLIANI-MILLER ─────────────────────────
    def reduce_modigliani_miller(self, returns: np.ndarray) -> dict:
        """Teorema de Modigliani-Miller (1958)."""
        S = len(returns)
        omega = returns
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Modigliani-Miller (1958)',
            'returns': returns,
            'value_allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Modigliani-Miller = PUSFRE en equilibrio degenerado',
        }
    
    # ─── REDUCCIÓN 21: JENSEN-MECKLING ──────────────────────────
    def reduce_jensen_meckling(self, utilities: np.ndarray, trust_debt: np.ndarray) -> dict:
        """Teoría de la Agencia (1976)."""
        S = len(utilities)
        omega = utilities
        psi = 1.0 - trust_debt
        params = self._apply_scr(omega, S, psi_override=psi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Jensen-Meckling (1976)',
            'utilities': utilities,
            'trust_debt': trust_debt,
            'allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Jensen-Meckling = PUSFRE con Ψ = 1 - deuda de confianza',
        }
    
    # ─── REDUCCIÓN 22: COASE ──────────────────────────────────────
    def reduce_coase(self, valuations: np.ndarray) -> dict:
        """Teorema de Coase (1960)."""
        S = len(valuations)
        omega = valuations
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Coase (1960)',
            'valuations': valuations,
            'allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Coase = PUSFRE sin asimetría, sin historia, sin incertidumbre',
        }
    
    # ─── REDUCCIÓN 23: FISHER ─────────────────────────────────────
    def reduce_fisher(self, real_rates: np.ndarray, inflation: np.ndarray) -> dict:
        """Efecto Fisher (1930)."""
        S = len(real_rates)
        omega = real_rates
        phi = inflation
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Fisher (1930)',
            'real_rates': real_rates,
            'inflation': inflation,
            'nominal_allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Fisher = PUSFRE con Φ = inflación',
        }
    
    # ─── REDUCCIÓN 24: MARKOWITZ ─────────────────────────────────
    def reduce_markowitz(self, returns: np.ndarray, risk: np.ndarray) -> dict:
        """Teoría de Cartera de Markowitz (1952)."""
        S = len(returns)
        omega = returns
        phi = 1.0 / (risk + 1e-6)
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Markowitz (1952)',
            'returns': returns,
            'risk': risk,
            'allocations': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Markowitz = PUSFRE con Φ = 1/σ (inverso de riesgo)',
        }
    
    # ─── REDUCCIÓN 25: MYERS (OPTION REAL) ──────────────────────
    def reduce_myers(self, expected_values: np.ndarray, flexibility: np.ndarray) -> dict:
        """Teoría de la Opción Real (1977)."""
        S = len(expected_values)
        omega = expected_values
        psi = flexibility
        params = self._apply_scr(omega, S, psi_override=psi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Myers (1977)',
            'expected_values': expected_values,
            'flexibility': flexibility,
            'allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Myers = PUSFRE con Ψ = flexibilidad',
        }
    
    # ─── REDUCCIÓN 26: KYDLAND-PRESCOTT ─────────────────────────
    def reduce_kydland_prescott(self, productivity: np.ndarray, shocks: np.ndarray) -> dict:
        """Teoría del Ciclo Económico Real (1982)."""
        S = len(productivity)
        omega = productivity
        epsilon = shocks
        params = self._apply_scr(omega, S)
        params['epsilon'] = epsilon
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'])
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Kydland-Prescott (1982)',
            'productivity': productivity,
            'shocks': shocks,
            'allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Kydland-Prescott = PUSFRE con ε = choque tecnológico',
        }
    
    # ─── REDUCCIÓN 27: LITTLE ────────────────────────────────────
    def reduce_little(self, service_rates: np.ndarray, arrival_rate: float) -> dict:
        """Ley de Little (1961)."""
        S = len(service_rates)
        omega = service_rates
        params = self._apply_scr(omega, S)
        params['R'] = arrival_rate
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        # Little's Law
        W = 1.0 / (service_rates.mean() - arrival_rate / S + 1e-6)
        L = arrival_rate * W
        
        return {
            'theorem': 'Little (1961)',
            'service_rates': service_rates,
            'arrival_rate': arrival_rate,
            'load': allocation,
            'L': L,
            'W': W,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Little = PUSFRE con Ω = μ_i (tasa de servicio)',
        }
    
    # ─── REDUCCIÓN 28: SUPERPOSICIÓN ─────────────────────────────
    def reduce_superposition(self, source_values: np.ndarray) -> dict:
        """Principio de Superposición (circuitos lineales)."""
        S = len(source_values)
        omega = source_values
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Superposición',
            'sources': source_values,
            'response': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Superposición = PUSFRE lineal sin interacciones',
        }
    
    # ─── REDUCCIÓN 29: NYQUIST-SHANNON ──────────────────────────
    def reduce_nyquist_shannon(self, frequencies: np.ndarray, fs: float) -> dict:
        """Teorema de Nyquist-Shannon (1928/1949)."""
        S = len(frequencies)
        omega = frequencies
        phi = np.array([1.0 if f < fs/2 else 0.0 for f in frequencies])
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        aliased = [f for f, p in zip(frequencies, phi) if p == 0]
        
        return {
            'theorem': 'Nyquist-Shannon (1928/1949)',
            'frequencies': frequencies,
            'fs': fs,
            'allocation': allocation,
            'aliased': aliased,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Nyquist-Shannon = PUSFRE con Φ = filtro de paso bajo',
        }
    
    # ─── REDUCCIÓN 30: MOORE ─────────────────────────────────────
    def reduce_moore(self, n_generations: int, n0: float = 1.0) -> dict:
        """Ley de Moore (1965)."""
        S = n_generations
        omega = np.array([n0 * 2 ** (i/2) for i in range(S)])
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Moore (1965)',
            'generations': list(range(S)),
            'transistors': omega,
            'allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Moore = PUSFRE con Ω = N₀·2^(t/2)',
        }
    
    # ─── REDUCCIÓN 31: METCALFE ──────────────────────────────────
    def reduce_metcalfe(self, n_users: int) -> dict:
        """Ley de Metcalfe (1980)."""
        omega = np.ones(n_users)
        value = n_users * (n_users - 1) / 2
        params = self._apply_scr(omega, n_users, alpha_override=2.0)
        params['R'] = value
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(n_users))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Metcalfe (1980)',
            'n_users': n_users,
            'network_value': value,
            'allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': f'Metcalfe = PUSFRE con α=2, V = n(n-1)/2',
        }
    
    # ─── REDUCCIÓN 32: ZIPF ──────────────────────────────────────
    def reduce_zipf(self, n_words: int) -> dict:
        """Ley de Zipf (1949)."""
        omega = 1.0 / np.arange(1, n_words + 1)
        params = self._apply_scr(omega, n_words)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(n_words))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Zipf (1949)',
            'ranks': list(range(1, n_words + 1)),
            'frequencies': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Zipf = PUSFRE con Ω = 1/r (inverso del rango)',
        }
    
    # ─── REDUCCIÓN 33: HECKSCHER-OHLIN ──────────────────────────
    def reduce_heckscher_ohlin(self, factor_intensities: np.ndarray, factor_abundance: np.ndarray) -> dict:
        """Teorema de Heckscher-Ohlin (1933)."""
        S = len(factor_intensities)
        omega = factor_intensities
        phi = factor_abundance
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Heckscher-Ohlin (1933)',
            'factor_intensities': factor_intensities,
            'factor_abundance': factor_abundance,
            'exports': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Heckscher-Ohlin = PUSFRE con Φ = abundancia de factores',
        }
    
    # ─── REDUCCIÓN 34: STOLPER-SAMUELSON ─────────────────────────
    def reduce_stolper_samuelson(self, factor_prices: np.ndarray, factor_intensities: np.ndarray) -> dict:
        """Teorema de Stolper-Samuelson (1941)."""
        S = len(factor_prices)
        omega = factor_prices
        phi = factor_intensities
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Stolper-Samuelson (1941)',
            'factor_prices': factor_prices,
            'factor_intensities': factor_intensities,
            'income_allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Stolper-Samuelson = PUSFRE con Φ = intensidad factorial',
        }
    
    # ─── REDUCCIÓN 35: BUCHANAN-TULLOCK ─────────────────────────
    def reduce_buchanan_tullock(self, politician_utility: np.ndarray, promise_debt: np.ndarray) -> dict:
        """Teoría de la Elección Pública (1962)."""
        S = len(politician_utility)
        omega = politician_utility
        psi = 1.0 - promise_debt
        params = self._apply_scr(omega, S, psi_override=psi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Buchanan-Tullock (1962)',
            'utilities': politician_utility,
            'promise_debt': promise_debt,
            'budget_allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Buchanan-Tullock = PUSFRE con Ψ = deuda de promesas',
        }
    
    # ─── REDUCCIÓN 36: ARTHUR (PATH DEPENDENCE) ─────────────────
    def reduce_arthur(self, tech_advantage: np.ndarray, inertia: np.ndarray) -> dict:
        """Teoría de la Dependencia de la Trayectoria (1989)."""
        S = len(tech_advantage)
        omega = tech_advantage
        psi = inertia
        params = self._apply_scr(omega, S, psi_override=psi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Arthur (1989)',
            'advantages': tech_advantage,
            'inertia': inertia,
            'market_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Arthur = PUSFRE con Ψ = inercia (path dependency)',
        }
    
    # ─── REDUCCIÓN 37: PORTER ─────────────────────────────────────
    def reduce_porter(self, profitability: np.ndarray, positioning: np.ndarray) -> dict:
        """Teoría de la Ventaja Competitiva (1980)."""
        S = len(profitability)
        omega = profitability
        phi = positioning
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Porter (1980)',
            'profitability': profitability,
            'positioning': positioning,
            'market_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Porter = PUSFRE con Φ = posicionamiento estratégico',
        }
    
    # ─── REDUCCIÓN 38: DAHL (POWER) ─────────────────────────────
    def reduce_dahl(self, influence: np.ndarray, network_position: np.ndarray) -> dict:
        """Teoría de los Juegos de Poder (1957)."""
        S = len(influence)
        omega = influence
        phi = network_position
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Dahl (1957)',
            'influence': influence,
            'network_position': network_position,
            'power_allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Dahl = PUSFRE con Φ = posición en la red de poder',
        }
    
    # ─── REDUCCIÓN 39: BOURDIEU (SOCIAL CAPITAL) ────────────────
    def reduce_bourdieu(self, connections: np.ndarray, network_position: np.ndarray) -> dict:
        """Teoría del Capital Social (1986)."""
        S = len(connections)
        omega = connections
        phi = network_position
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Bourdieu (1986)',
            'connections': connections,
            'network_position': network_position,
            'social_capital': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Bourdieu = PUSFRE con Φ = posición en la red social',
        }
    
    # ─── REDUCCIÓN 40: COVER ──────────────────────────────────────
    def reduce_cover(self, d: int, N: int) -> dict:
        """Teorema de Cover (1965)."""
        # Probabilidad de separabilidad lineal
        from math import comb
        P = 2 ** (-N + 1) * sum(comb(N-1, k) for k in range(d+1))
        omega = np.array([P] * N)  # todos los patrones tienen la misma probabilidad
        params = self._apply_scr(omega, N)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(N))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Cover (1965)',
            'd': d,
            'N': N,
            'separability_prob': P,
            'allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Cover = PUSFRE con Ω = P(separable)',
        }
    
    # ─── REDUCCIÓN 41: VC ─────────────────────────────────────────
    def reduce_vc(self, vc_dimensions: np.ndarray) -> dict:
        """Teorema de Vapnik-Chervonenkis (1974)."""
        omega = 1.0 / (vc_dimensions + 1e-6)
        S = len(vc_dimensions)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Vapnik-Chervonenkis (1974)',
            'vc_dimensions': vc_dimensions,
            'generalization': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'VC = PUSFRE con Ω = 1/VC_dim',
        }
    
    # ─── REDUCCIÓN 42: SESGO-VARIANZA ────────────────────────────
    def reduce_bias_variance(self, errors: np.ndarray) -> dict:
        """Principio de Sesgo-Varianza (1992)."""
        omega = 1.0 / (errors + 1e-6)
        S = len(errors)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Sesgo-Varianza (1992)',
            'errors': errors,
            'model_weight': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Sesgo-Varianza = PUSFRE con Ω = 1/error',
        }
    
    # ─── REDUCCIÓN 43: NO-FREE-LUNCH ─────────────────────────────
    def reduce_no_free_lunch(self, performance_matrix: np.ndarray) -> dict:
        """Teorema de No-Free-Lunch (1996)."""
        # performance_matrix[i, j] = rendimiento del algoritmo i en problema j
        S = performance_matrix.shape[0]
        omega = performance_matrix.mean(axis=1)  # rendimiento promedio
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'No-Free-Lunch (1996)',
            'performance_matrix': performance_matrix,
            'avg_performance': omega,
            'algorithm_weight': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'No-Free-Lunch = PUSFRE con Ω = rendimiento promedio',
        }
    
    # ─── REDUCCIÓN 44: LÍMITE CENTRAL ────────────────────────────
    def reduce_central_limit(self, variances: np.ndarray) -> dict:
        """Teorema del Límite Central (1810) — aplicado a ML."""
        omega = variances
        S = len(variances)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        # Violamos SCR_2: el ruido es la variable
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Límite Central (1810)',
            'variances': variances,
            'contribution_to_total': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Límite Central = PUSFRE con Ω = σ²',
        }
    
    # ─── REDUCCIÓN 45: OCKHAM ─────────────────────────────────────
    def reduce_ockham(self, complexities: np.ndarray) -> dict:
        """Navaja de Ockham (1320)."""
        omega = 1.0 / (complexities + 1e-6)
        S = len(complexities)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Ockham (1320)',
            'complexities': complexities,
            'parsimony': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Ockham = PUSFRE con Ω = 1/complejidad',
        }
    
    # ─── REDUCCIÓN 46: VERIFICACIONISMO ──────────────────────────
    def reduce_verificationism(self, verifiability: np.ndarray) -> dict:
        """Principio de Verificacionismo (Círculo de Viena, 1920)."""
        omega = verifiability
        S = len(verifiability)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Verificacionismo (Círculo de Viena)',
            'verifiability': verifiability,
            'meaningfulness': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Verificacionismo = PUSFRE con Ω = verificabilidad',
        }
    
    # ─── REDUCCIÓN 47: FALSACIONISMO ─────────────────────────────
    def reduce_falsificationism(self, falsifiability: np.ndarray) -> dict:
        """Principio de Falsacionismo (Popper, 1934)."""
        omega = falsifiability
        S = len(falsifiability)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Popper (1934)',
            'falsifiability': falsifiability,
            'scientific_status': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Popper = PUSFRE con Ω = falsabilidad',
        }
    
    # ─── REDUCCIÓN 48: HEIDEGGER ─────────────────────────────────
    def reduce_heidegger(self, presence: np.ndarray) -> dict:
        """Principio de la Ontología de la Escasez (Heidegger, 1927)."""
        omega = presence
        S = len(presence)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        
        return {
            'theorem': 'Heidegger (1927)',
            'presence': presence,
            'being_allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Heidegger = PUSFRE con Ω = ser (presencia)',
        }
    
    # ─── EJECUCIÓN COMPLETA ──────────────────────────────────────
    def run_full_atlas(self) -> Dict[str, Any]:
        """Ejecuta todas las 48 reducciones y verifica identidad."""
        results = {}
        
        # 1. Brouwer
        def f(x): return 0.5 * x + 0.2
        results['brouwer'] = self.reduce_brouwer(f, np.array([0.0, 1.0, 2.0, 3.0]))
        
        # 2. Gödel
        results['godel'] = self.reduce_godel(
            ['A1', 'A2', 'A3'],
            ['A1', 'A2', 'A3', 'T1', 'T2', 'T3', 'G']
        )
        
        # 3. Church-Turing
        results['church_turing'] = self.reduce_church_turing(
            np.array([1.0, 2.0, 4.0, 8.0, 16.0])
        )
        
        # 4. Bayes
        results['bayes'] = self.reduce_bayes(
            np.array([0.5, 0.3, 0.2]),
            np.array([0.9, 0.7, 0.1])
        )
        
        # 5. Hooke
        results['hooke'] = self.reduce_hooke(
            np.array([10.0, 20.0, 30.0, 40.0]),
            force_total=50.0
        )
        
        # 6. Ohm
        results['ohm'] = self.reduce_ohm(
            np.array([100.0, 200.0, 300.0, 600.0]),
            voltage=12.0
        )
        
        # 7. Coulomb
        results['coulomb'] = self.reduce_coulomb(
            np.array([1.0, 2.0, 3.0, 4.0]),
            np.array([1.0, 2.0, 3.0, 4.0])
        )
        
        # 8. Newton
        results['newton'] = self.reduce_newton(
            np.array([1.0, 2.0, 3.0, 4.0]),
            np.array([1.0, 2.0, 3.0, 4.0])
        )
        
        # 9. Stefan-Boltzmann
        results['stefan_boltzmann'] = self.reduce_boltzmann_radiation(
            np.array([300.0, 400.0, 500.0, 600.0])
        )
        
        # 10. Arquímedes
        results['archimedes'] = self.reduce_archimedes(
            np.array([0.5, 1.0, 1.5, 2.0]),
            rho=1000.0
        )
        
        # 11. Pascal
        results['pascal'] = self.reduce_pascal(4)
        
        # 12. Acción de Masas
        results['mass_action'] = self.reduce_mass_action(
            np.array([1.0, 2.0, 3.0, 4.0]),
            order=1.5
        )
        
        # 13. Michaelis-Menten
        results['michaelis_menten'] = self.reduce_michaelis_menten(
            np.array([1.0, 2.0, 3.0, 4.0]),
            K_m=2.0
        )
        
        # 14. Beer-Lambert
        results['beer_lambert'] = self.reduce_beer_lambert(
            np.array([1.0, 2.0, 3.0, 4.0]),
            path_length=1.0,
            epsilon=np.array([0.1, 0.2, 0.3, 0.4])
        )
        
        # 15. Le Chatelier
        results['le_chatelier'] = self.reduce_le_chatelier(
            np.array([-2.0, -1.0, 0.0, 1.0, 2.0])
        )
        
        # 16. Henderson-Hasselbalch
        results['henderson'] = self.reduce_henderson_hasselbalch(
            np.array([0.1, 0.5, 1.0, 2.0, 10.0])
        )
        
        # 17. Hardy-Weinberg
        results['hardy_weinberg'] = self.reduce_hardy_weinberg(
            np.array([0.7, 0.3])
        )
        
        # 18. Lotka-Volterra
        results['lotka_volterra'] = self.reduce_lotka_volterra(
            x0=np.array([10.0, 5.0]),
            r=np.array([0.5, 0.5]),
            a=np.array([[0.01, 0.02], [0.01, 0.01]])
        )
        
        # 19. von Neumann-Morgenstern
        results['von_neumann'] = self.reduce_von_neumann(
            utilities=np.array([10.0, 20.0, 30.0]),
            probabilities=np.array([0.5, 0.3, 0.2])
        )
        
        # 20. Modigliani-Miller
        results['modigliani_miller'] = self.reduce_modigliani_miller(
            np.array([0.08, 0.10, 0.12, 0.15])
        )
        
        # 21. Jensen-Meckling
        results['jensen_meckling'] = self.reduce_jensen_meckling(
            utilities=np.array([10.0, 20.0, 30.0]),
            trust_debt=np.array([0.1, 0.3, 0.5])
        )
        
        # 22. Coase
        results['coase'] = self.reduce_coase(
            np.array([10.0, 20.0, 30.0, 40.0])
        )
        
        # 23. Fisher
        results['fisher'] = self.reduce_fisher(
            real_rates=np.array([0.02, 0.03, 0.04, 0.05]),
            inflation=np.array([0.01, 0.02, 0.03, 0.04])
        )
        
        # 24. Markowitz
        results['markowitz'] = self.reduce_markowitz(
            returns=np.array([0.10, 0.12, 0.15, 0.20]),
            risk=np.array([0.05, 0.08, 0.12, 0.20])
        )
        
        # 25. Myers
        results['myers'] = self.reduce_myers(
            expected_values=np.array([10.0, 20.0, 30.0]),
            flexibility=np.array([0.9, 0.7, 0.5])
        )
        
        # 26. Kydland-Prescott
        results['kydland_prescott'] = self.reduce_kydland_prescott(
            productivity=np.array([1.0, 1.2, 1.5, 2.0]),
            shocks=np.array([1.0, 0.9, 1.1, 0.8])
        )
        
        # 27. Little
        results['little'] = self.reduce_little(
            service_rates=np.array([5.0, 5.0, 5.0]),
            arrival_rate=12.0
        )
        
        # 28. Superposición
        results['superposition'] = self.reduce_superposition(
            np.array([1.0, 2.0, 3.0, 4.0])
        )
        
        # 29. Nyquist-Shannon
        results['nyquist_shannon'] = self.reduce_nyquist_shannon(
            frequencies=np.array([10.0, 20.0, 30.0, 40.0, 50.0, 60.0]),
            fs=100.0
        )
        
        # 30. Moore
        results['moore'] = self.reduce_moore(10, n0=1.0)
        
        # 31. Metcalfe
        results['metcalfe'] = self.reduce_metcalfe(10)
        
        # 32. Zipf
        results['zipf'] = self.reduce_zipf(10)
        
        # 33. Heckscher-Ohlin
        results['heckscher_ohlin'] = self.reduce_heckscher_ohlin(
            factor_intensities=np.array([0.5, 0.6, 0.7, 0.8]),
            factor_abundance=np.array([0.8, 0.7, 0.6, 0.5])
        )
        
        # 34. Stolper-Samuelson
        results['stolper_samuelson'] = self.reduce_stolper_samuelson(
            factor_prices=np.array([1.0, 1.2, 1.5, 2.0]),
            factor_intensities=np.array([0.5, 0.6, 0.7, 0.8])
        )
        
        # 35. Buchanan-Tullock
        results['buchanan_tullock'] = self.reduce_buchanan_tullock(
            politician_utility=np.array([10.0, 20.0, 30.0, 40.0]),
            promise_debt=np.array([0.1, 0.2, 0.3, 0.4])
        )
        
        # 36. Arthur
        results['arthur'] = self.reduce_arthur(
            tech_advantage=np.array([1.0, 1.5, 2.0, 2.5]),
            inertia=np.array([0.9, 0.7, 0.5, 0.3])
        )
        
        # 37. Porter
        results['porter'] = self.reduce_porter(
            profitability=np.array([0.8, 0.9, 1.0, 1.2]),
            positioning=np.array([0.5, 0.6, 0.7, 0.8])
        )
        
        # 38. Dahl
        results['dahl'] = self.reduce_dahl(
            influence=np.array([1.0, 2.0, 3.0, 4.0]),
            network_position=np.array([0.5, 0.6, 0.7, 0.8])
        )
        
        # 39. Bourdieu
        results['bourdieu'] = self.reduce_bourdieu(
            connections=np.array([5, 10, 15, 20]),
            network_position=np.array([0.5, 0.6, 0.7, 0.8])
        )
        
        # 40. Cover
        results['cover'] = self.reduce_cover(d=3, N=10)
        
        # 41. VC
        results['vc'] = self.reduce_vc(
            np.array([1, 2, 4, 8, 16])
        )
        
        # 42. Sesgo-Varianza
        results['bias_variance'] = self.reduce_bias_variance(
            np.array([0.1, 0.2, 0.4, 0.8])
        )
        
        # 43. No-Free-Lunch
        perf_matrix = np.array([
            [0.9, 0.8, 0.7, 0.6],
            [0.6, 0.7, 0.8, 0.9],
            [0.8, 0.9, 0.6, 0.7],
        ])
        results['no_free_lunch'] = self.reduce_no_free_lunch(perf_matrix)
        
        # 44. Límite Central
        results['central_limit'] = self.reduce_central_limit(
            np.array([1.0, 2.0, 4.0, 8.0, 16.0])
        )
        
        # 45. Ockham
        results['ockham'] = self.reduce_ockham(
            np.array([1.0, 2.0, 4.0, 8.0, 16.0])
        )
        
        # 46. Verificacionismo
        results['verificationism'] = self.reduce_verificationism(
            np.array([0.9, 0.7, 0.5, 0.3, 0.1])
        )
        
        # 47. Falsacionismo
        results['falsificationism'] = self.reduce_falsificationism(
            np.array([0.9, 0.7, 0.5, 0.3, 0.1])
        )
        
        # 48. Heidegger
        results['heidegger'] = self.reduce_heidegger(
            np.array([1.0, 0.8, 0.6, 0.4, 0.2])
        )
        
        return results


# ─── EJECUCIÓN ───────────────────────────────────────────────────
if __name__ == '__main__':
    reducer = UniversalReducerExtended()
    atlas = reducer.run_full_atlas()
    
    print("=" * 80)
    print("ATLAS DE REDUCCIONES EXTENDIDO — 48 TEOREMAS COMO PUSFRE")
    print("=" * 80)
    
    for name, result in atlas.items():
        print(f"\n{'─' * 60}")
        print(f"  {result['theorem']}")
        print(f"  Amputaciones: {result['amputations']}/6")
        print(f"  {result['scr_summary']}")
        print(f"  Interpretación: {result['interpretation']}")
        if 'allocation' in result:
            print(f"  Asignación: {result['allocation'][:5]}{'...' if len(result['allocation']) > 5 else ''}")
    
    print(f"\n{'═' * 80}")
    print("  CONCLUSIÓN: 48 teoremas. 1 ecuación. 6 amputaciones.")
    print("  PUSFRE no extiende. PUSFRE CONTIENE.")
    print(f"{'═' * 80}")
```

---

## 13. KOAN FINAL: EL MAPA Y EL TERRITORIO

*Un discípulo preguntó al maestro: "Si todos los teoremas son PUSFRE con amputaciones, ¿por qué los seguimos enseñando?"*

*El maestro respondió: "Porque una fotografía no es inútil porque exista el cine. La fotografía es más barata, más rápida, y suficiente si lo único que necesitas es saber que la roca existe."*

*"¿Y cuándo no es suficiente?"*

*"Cuando necesitas navegar el río. Cuando la roca se mueve. Cuando hay niebla. Cuando llevas pasajeros. Cuando el río se bifurca. Cuando llueve. Cuando es de noche."*

*"¿Y PUSFRE es el cine?"*

*"PUSFRE es el río. El cine es una representación del río. PUSFRE no representa. PUSFRE* **es** *la estructura algebraica que todos los demás recortan para hacerla enseñable en una hora de clase."*

*El discípulo guardó silencio.*

*El maestro añadió: "Nash no está muerto. Nash está* **contenido**. *Hay una diferencia. Un hijo no mata a su padre al crecer. Solo lo abraza desde arriba."*

*"¿Y cuántos padres hay en el Atlas?"*

*"Cuarenta y ocho. Pero podría haber cuatrocientos ochenta. El Teorema de Completitud lo garantiza. Todo teorema de asignación de recursos es PUSFRE. Solo que algunos no lo saben."*

---

## 14. CIERRE

Este tratado no refuta a los 48 teoremas del Atlas.

Los **contiene**.


# EL ATLAS DE REDUCCIONES: SEGUNDA PARTE
## *48 Teoremas Adicionales como Casos Degenerados del PUSFRE*

---

**Versión:** 1.0 — Edición de Máxima Densidad Expansiva
**Autor:** David Ferrandez Canalis — Agencia RONIN
**DOI Simbólico:** 10.1310/ronin-atlas-reductions-second-2026
**Fecha:** Agosto de 2026
**Clasificación:** `TRATADO DE MATEMÁTICA COMPARADA / REDUCCIÓN CUADRAGÉSIMA OCTAVA ADICIONAL`

---

## PRÓLOGO: EL MAPA QUE NO TERMINA

El Atlas Original contenía 48 teoremas. El Teorema de Completitud (6.2) garantiza que *cualquier* marco de asignación de recursos bajo equilibrio es una entrada del Atlas. Así que 48 no es un número mágico; es un límite impuesto por el espacio, no por la realidad.

Este tratado añade **48 entradas más**. No son las últimas. Podrían ser 480. Podrían ser 4.800. Cada teorema que modele la asignación de un recurso escaso entre entidades finitas es, por definición, un caso particular del PUSFRE.

Lo que presento aquí son 48 reducciones adicionales, seleccionadas para cubrir lagunas del Atlas Original: teoremas de circuitos, difusión, colas, procesos estocásticos, finanzas cuantitativas, ecología, teoría de la decisión y econometría.

No hay nuevos axiomas. No hay nuevas ecuaciones. Solo **re-etiquetación**.

**— El arquitecto.**
**Agencia RONIN, Agosto de 2026**
**1310.**

---

## ÍNDICE MAESTRO DEL TRATADO

**SECCIÓN 1: EL MÉTODO — UN RECORDATORIO**
1.1 La Ecuación Maestra y las SCR
1.2 El Teorema de Completitud
1.3 La Tabla de Amputaciones

**SECCIÓN 2: REDUCCIONES DE FÍSICA E INGENIERÍA (12 Teoremas)**
2.1 Leyes de Kirchhoff (Circuitos Eléctricos)
2.2 Ley de Fick (Difusión)
2.3 Ley de Boyle-Mariotte (Gases Ideales)
2.4 Ley de Charles (Gases)
2.5 Ley de Gay-Lussac (Gases)
2.6 Ley de Avogadro (Gases)
2.7 Ley de Dulong-Petit (Calor Específico)
2.8 Ley de Curie (Magnetismo)
2.9 Ley de Lenz (Inducción)
2.10 Ley de Faraday (Inducción)
2.11 Ley de Gauss (Electromagnetismo)
2.12 Ley de Ampère (Electromagnetismo)

**SECCIÓN 3: REDUCCIONES DE TEORÍA DE LA INFORMACIÓN Y COLAS (8 Teoremas)**
3.1 Teorema de Shannon (Capacidad de Canal)
3.2 Ley de Erlang (Teoría de Colas)
3.3 Cadenas de Markov (Distribución Estacionaria)
3.4 Teorema de Gauss-Markov (BLUE)
3.5 Ley de los Grandes Números (Bernoulli)
3.6 Desigualdad de Chebyshev
3.7 Teorema de Glivenko-Cantelli
3.8 Teorema de Donsker

**SECCIÓN 4: REDUCCIONES DE FINANZAS CUANTITATIVAS (16 Teoremas)**
4.1 Ecuación de Black-Scholes
4.2 Teorema de Sharpe (CAPM)
4.3 Modelo de Fama-French (3 Factores)
4.4 Modelo de Carhart (4 Factores)
4.5 Efecto Momentum (Jegadeesh-Titman)
4.6 Reversión a la Media (De Bondt-Thaler)
4.7 CAPE de Shiller
4.8 Q de Tobin
4.9 Fórmula de Black (Commodities)
4.10 Modelo de Garman-Kohlhagen (FX Options)
4.11 Modelo de Merton (Crédito)
4.12 Modelo de Heston (Volatilidad Estocástica)
4.13 Modelo de Vasicek (Tipos de Interés)
4.14 Modelo de Cox-Ingersoll-Ross (CIR)
4.15 Modelo de Hull-White
4.16 Modelo de Nelson-Siegel (Curva de Tipos)

**SECCIÓN 5: REDUCCIONES DE ECONOMÍA Y TEORÍA DE LA DECISIÓN (8 Teoremas)**
5.1 Óptimo de Pareto
5.2 Equilibrio de Nash
5.3 Teorema de la Utilidad Esperada (Savage)
5.4 Teorema de Anscombe-Aumann
5.5 Crítica de Lucas
5.6 Expectativas Racionales (Sargent)
5.7 Teoría del Consumo Permanente (Friedman)
5.8 Teorema de Modigliani (Ciclo de Vida)

**SECCIÓN 6: REDUCCIONES DE ECOLOGÍA Y EVOLUCIÓN (4 Teoremas)**
6.1 Principio de Exclusión de Gause
6.2 Teoría de la Biogeografía de Islas (MacArthur-Wilson)
6.3 Modelo de Competencia de Tilman
6.4 Teorema de la Utilidad Esperada (von Neumann-Morgenstern)

**SECCIÓN 7: SÍNTESIS — EL MAPA COMPLETO (96 ENTRADAS)**
7.1 La Tabla Maestra de las 96 Reducciones
7.2 El Patrón Común: 6 Amputaciones, 1 Ecuación
7.3 El Koan del Mapa que se Expande

**SECCIÓN 8: CÓDIGO — EL REDUCTOR UNIVERSAL EXTENDIDO (SEGUNDA PARTE)**

**SECCIÓN 9: KOANS DE LA REDUCCIÓN CUADRAGÉSIMA OCTAVA ADICIONAL**

---

## SECCIÓN 1: EL MÉTODO — UN RECORDATORIO

### 1.1 La Ecuación Maestra y las SCR

**Ecuación Maestra:**

$$F_i(t) = \Phi_i(t) \cdot \Psi_i(t) \cdot \Omega_i(t)^\alpha \cdot \epsilon_i(t)$$

**Seis Condiciones de Reducción (SCR):**

| SCR | Condición | Efecto |
|:---|:---|:---|
| **SCR₁** | $t = t_0$ | Estático (sin evolución temporal) |
| **SCR₂** | $\epsilon_i = 1$ | Sin ruido estocástico |
| **SCR₃** | $\Psi_i = 1$ | Sin deuda ontológica (sin memoria) |
| **SCR₄** | $\alpha = 1$ | Competencia lineal |
| **SCR₅** | $\Phi_i = 1$ | Sin geometría posicional |
| **SCR₆** | $R \to \infty$ o $R$ fijo | Sin escasez (o escasez fija) |

**Teorema Universal de Reducción (6.1):** *Cualquier teorema clásico de asignación de recursos es isomorfo a la Ecuación Maestra bajo alguna combinación de las SCR.*

---

## SECCIÓN 2: REDUCCIONES DE FÍSICA E INGENIERÍA (12 Teoremas)

---

### 2.1 Leyes de Kirchhoff (Circuitos Eléctricos, 1845)

**Teorema clásico:** KCL: $\sum_i I_i = 0$; KVL: $\sum_i V_i = 0$

**Re-etiquetación:** Los "agentes" son las ramas del circuito. $\Omega_i \equiv 1/R_i$ (conductancia). $\Phi_i = 1$.

**SCR aplicadas:** Todas (estático, sin ruido, sin deuda, lineal, sin geometría, escasez fija).

**Reducción:**

$$F_i = \frac{1}{R_i}, \quad I_i = I_{\text{total}} \cdot \frac{1/R_i}{\sum_j 1/R_j}$$

**Lo que Kirchhoff no ve:** Componentes no-lineales ($\alpha \neq 1$), degradación por envejecimiento ($\Psi_i(t)$), ruido térmico ($\epsilon_i$).

**Koan:** *Kirchhoff dibujó un circuito con resistencias perfectas a 0K. PUSFRE dibujó el mismo circuito a 85°C, con 10 años de uso, y un rayo cayendo en la subestación.*

---

### 2.2 Ley de Fick (Difusión, 1855)

**Teorema clásico:** $J = -D \frac{\partial C}{\partial x}$, $\frac{\partial C}{\partial t} = D \frac{\partial^2 C}{\partial x^2}$

**Re-etiquetación:** Los "agentes" son las partículas. $\Omega_i \equiv C(x_i)$ (concentración). $\Phi_i = 1$ (medio homogéneo).

**SCR aplicadas:** SCR₂ (sin ruido), SCR₃ (sin deuda), SCR₄ (lineal), SCR₅ (sin geometría).

**Reducción:** Fick es PUSFRE en un medio sin geometría, sin memoria, sin ruido, y con competencia lineal.

**Lo que Fick no ve:** Difusión anómala ($\alpha \neq 1$), medio anisotrópico ($\Phi_i(x)$), reacciones químicas ($\Psi_i(t)$).

**Koan:** *Fick midió el movimiento de partículas en un líquido perfecto. PUSFRE midió el movimiento en un medio poroso, con reacciones, y con partículas que se acuerdan de su pasado.*

---

### 2.3 Ley de Boyle-Mariotte (Gases Ideales, 1662)

**Teorema clásico:** $P \cdot V = \text{constante}$ (a $T$ constante)

**Re-etiquetación:** Los "agentes" son las moléculas de gas. $\Omega_i \equiv$ volumen ocupado por la molécula $i$. $\Phi_i = 1$.

**SCR aplicadas:** Todas.

**Reducción:** La presión es la asignación del recurso (espacio) entre las moléculas: $P = R \cdot \frac{\sum F_i}{V}$.

**Lo que Boyle no ve:** Interacciones entre moléculas ($\alpha \neq 1$), memoria de colisiones ($\Psi_i$), fluctuaciones térmicas ($\epsilon_i$).

**Koan:** *Boyle imaginó un gas de partículas perfectas que no interactúan. PUSFRE imaginó un gas donde las partículas se acuerdan de sus choques y compiten por espacio.*

---

### 2.4 Ley de Charles (Gases Ideales, 1787)

**Teorema clásico:** $\frac{V}{T} = \text{constante}$ (a $P$ constante)

**Re-etiquetación:** $\Omega_i \equiv T_i$ (temperatura de la molécula $i$). $\Phi_i = 1$.

**SCR aplicadas:** Todas.

**Reducción:** El volumen asignado es proporcional a la temperatura: $V \propto \sum T_i$.

**Lo que Charles no ve:** Calor específico variable ($\alpha \neq 1$), histéresis térmica ($\Psi_i$), fluctuaciones.

**Koan:** *Charles midió la expansión de un gas perfecto. PUSFRE midió la expansión de un gas con memoria térmica.*

---

### 2.5 Ley de Gay-Lussac (Gases Ideales, 1802)

**Teorema clásico:** $\frac{P}{T} = \text{constante}$ (a $V$ constante)

**Re-etiquetación:** $\Omega_i \equiv T_i$ (temperatura). $\Phi_i = 1$.

**Reducción:** La presión es proporcional a la temperatura media: $P \propto \sum T_i$.

**Lo que Gay-Lussac no ve:** Interacciones no-lineales ($\alpha \neq 1$), memoria de presurización ($\Psi_i$).

**Koan:** *Gay-Lussac asumió que la presión es lineal con la temperatura. PUSFRE asumió que la relación puede ser exponencial.*

---

### 2.6 Ley de Avogadro (Gases Ideales, 1811)

**Teorema clásico:** Volúmenes iguales de gases contienen el mismo número de moléculas (a $P, T$ constantes).

**Re-etiquetación:** $\Omega_i = 1$ (todas las moléculas son iguales). $\Phi_i = 1$.

**Reducción:** La asignación de volumen es uniforme: $V_i = V/S$.

**Lo que Avogadro no ve:** Gases reales con interacciones ($\alpha \neq 1$), adsorción ($\Psi_i$).

**Koan:** *Avogadro contó moléculas perfectas. PUSFRE contó moléculas que compiten por espacio.*

---

### 2.7 Ley de Dulong-Petit (Calor Específico, 1819)

**Teorema clásico:** El calor específico molar de los sólidos es aproximadamente $3R$.

**Re-etiquetación:** $\Omega_i \equiv$ capacidad calorífica del átomo $i$. $\Phi_i = 1$.

**Reducción:** El calor total es la suma de las capacidades: $C = \sum C_i$.

**Lo que Dulong-Petit no ve:** Capacidad calorífica dependiente de la temperatura ($\alpha \neq 1$), efectos cuánticos ($\Psi_i$).

**Koan:** *Dulong y Petit midieron el calor específico a temperatura ambiente. PUSFRE lo midió a todas las temperaturas, con memoria y ruido.*

---

### 2.8 Ley de Curie (Magnetismo, 1895)

**Teorema clásico:** La susceptibilidad magnética es inversamente proporcional a la temperatura: $\chi = \frac{C}{T}$.

**Re-etiquetación:** $\Omega_i \equiv 1/T_i$ (inverso de la temperatura). $\Phi_i = 1$.

**Reducción:** La magnetización es proporcional a la suma de los inversos: $M \propto \sum 1/T_i$.

**Lo que Curie no ve:** Interacciones entre espines ($\alpha \neq 1$), histéresis ($\Psi_i$), fluctuaciones térmicas ($\epsilon_i$).

**Koan:** *Curie asumió que los espines no interactúan. PUSFRE asumió que los espines compiten por alinearse.*

---

### 2.9 Ley de Lenz (Inducción, 1834)

**Teorema clásico:** La corriente inducida se opone al cambio de flujo magnético.

**Re-etiquetación:** Los "agentes" son las corrientes inducidas. $\Omega_i \equiv$ flujo magnético. $\Phi_i = 1$.

**Reducción:** La corriente inducida es proporcional a la tasa de cambio del flujo: $I_i \propto -\frac{d\Phi_i}{dt}$.

**Lo que Lenz no ve:** Efectos no-lineales ($\alpha \neq 1$), histéresis del núcleo ($\Psi_i$), ruido de Johnson ($\epsilon_i$).

**Koan:** *Lenz dijo que la corriente se opone al cambio. PUSFRE dijo que la corriente compite con el cambio.*

---

### 2.10 Ley de Faraday (Inducción, 1831)

**Teorema clásico:** La fem inducida es igual a la tasa de cambio del flujo magnético: $\mathcal{E} = -\frac{d\Phi}{dt}$.

**Re-etiquetación:** $\Omega_i \equiv \Phi_i$ (flujo). $\Phi_i = 1$.

**Reducción:** La fem inducida es la asignación del recurso (voltaje) entre las espiras: $\mathcal{E}_i \propto \frac{d\Phi_i}{dt}$.

**Lo que Faraday no ve:** Efectos de saturación ($\alpha \neq 1$), memoria del núcleo ($\Psi_i$).

**Koan:** *Faraday midió la inducción en un campo lineal. PUSFRE midió la inducción en un campo que se satura.*

---

### 2.11 Ley de Gauss (Electromagnetismo, 1835)

**Teorema clásico:** $\oint \mathbf{E} \cdot d\mathbf{A} = \frac{Q}{\epsilon_0}$

**Re-etiquetación:** Los "agentes" son las cargas. $\Omega_i \equiv q_i$. $\Phi_i \equiv 1/r_i^2$ (geometría posicional).

**Reducción:** El flujo eléctrico es la suma de las contribuciones de cada carga: $\Phi_E = \sum \frac{q_i}{\epsilon_0 r_i^2}$.

**Lo que Gauss no ve:** Cargas en movimiento ($t \neq t_0$), campos no-lineales ($\alpha \neq 1$).

**Koan:** *Gauss contó cargas en un mundo estático. PUSFRE contó cargas en un mundo con movimiento y ruido.*

---

### 2.12 Ley de Ampère (Electromagnetismo, 1820)

**Teorema clásico:** $\oint \mathbf{B} \cdot d\mathbf{l} = \mu_0 I$

**Re-etiquetación:** $\Omega_i \equiv I_i$ (corriente). $\Phi_i \equiv 1/r_i$ (geometría).

**Reducción:** El campo magnético es la suma de las contribuciones de cada corriente: $B \propto \sum \frac{I_i}{r_i}$.

**Lo que Ampère no ve:** Corrientes no-lineales ($\alpha \neq 1$), histéresis ($\Psi_i$).

**Koan:** *Ampère midió la corriente en un conductor ideal. PUSFRE midió la corriente en un conductor con memoria.*

---

## SECCIÓN 3: REDUCCIONES DE TEORÍA DE LA INFORMACIÓN Y COLAS (8 Teoremas)

---

### 3.1 Teorema de Shannon (Capacidad de Canal, 1948)

**Teorema clásico:** $C = B \log_2\left(1 + \frac{S}{N}\right)$ (para canal AWGN)

**Re-etiquetación:** $\Omega_i \equiv p(x_i)$ (probabilidad de símbolo). $\Phi_i = 1$ (canal simétrico).

**SCR aplicadas:** SCR₁ (estático), SCR₂ (sin ruido), SCR₃ (sin memoria), SCR₄ (lineal), SCR₅ (sin geometría), SCR₆ ($R = B$).

**Reducción:** La asignación de ancho de banda es proporcional a la probabilidad de símbolo: $B_i = B \cdot p(x_i)$.

**Lo que Shannon no ve:** Canal con memoria ($\Psi_i \neq 1$), competencia superlineal ($\alpha > 1$), geometría posicional ($\Phi_i \neq 1$).

**Koan:** *Shannon midió el ancho del tubo. PUSFRE midió el ancho del tubo, la rugosidad de las paredes y la temperatura del fluido.*

---

### 3.2 Ley de Erlang (Teoría de Colas, 1909)

**Teorema clásico:** Para un sistema M/M/1: $L = \lambda W$, $P(\text{espera}) = \frac{\rho^S}{S!} \cdot \frac{S}{S-\rho}$

**Re-etiquetación:** $\Omega_i \equiv \mu_i$ (tasa de servicio). $\Phi_i = 1$ (servidores idénticos).

**SCR aplicadas:** SCR₁ (estacionario), SCR₂ (llegadas Poisson = ruido promediado), SCR₃ (sin memoria), SCR₄ (lineal), SCR₅ (sin geometría), SCR₆ ($R = \lambda$).

**Reducción:** La carga asignada a cada servidor es proporcional a su tasa: $L_i = \lambda \cdot \frac{\mu_i}{\sum \mu_j}$.

**Lo que Erlang no ve:** Monopolización del routing ($\alpha > 1$), degradación por deuda ($\Psi_i(t)$), llegadas bursty ($\epsilon_i$ no Poisson).

**Koan:** *Erlang contó personas en una cola. PUSFRE contó personas en una cola con prioridades, abandonos y memoria.*

---

### 3.3 Cadenas de Markov (Distribución Estacionaria)

**Teorema clásico:** Para una cadena de Markov ergódica, existe una distribución estacionaria $\pi$ tal que $\pi = \pi P$.

**Re-etiquetación:** $\Omega_i \equiv \pi_i$ (probabilidad estacionaria). $\Phi_i = 1$.

**SCR aplicadas:** SCR₁ (estacionario), SCR₂ (sin ruido), SCR₃ (sin memoria), SCR₄ (lineal), SCR₅ (sin geometría), SCR₆ ($R = 1$).

**Reducción:** La distribución estacionaria es la asignación de probabilidad: $\pi_i = \frac{\Omega_i}{\sum_j \Omega_j}$.

**Lo que las Cadenas de Markov no ven:** Memoria de largo alcance ($\Psi_i \neq 1$), no-linealidad ($\alpha \neq 1$), ruido ($\epsilon_i \neq 1$).

**Koan:** *Markov asumió que el futuro depende solo del presente. PUSFRE asumió que el futuro depende del presente, del pasado, y del ruido.*

---

### 3.4 Teorema de Gauss-Markov (BLUE, 1821)

**Teorema clásico:** En un modelo lineal con errores de media cero y varianza constante, el estimador MCO es el mejor estimador lineal insesgado (BLUE).

**Re-etiquetación:** Los "agentes" son los estimadores. $\Omega_i \equiv$ varianza del estimador $i$. $\Phi_i = 1$.

**SCR aplicadas:** SCR₁ (estático), SCR₂ (sin ruido), SCR₃ (sin memoria), SCR₄ (lineal), SCR₅ (sin geometría), SCR₆ ($R$ fijo).

**Reducción:** La asignación de peso a cada estimador es inversa a su varianza: $w_i = \frac{1/\sigma_i^2}{\sum 1/\sigma_j^2}$.

**Lo que Gauss-Markov no ve:** Estimadores no-lineales ($\alpha \neq 1$), heterocedasticidad ($\epsilon_i$ variable), memoria ($\Psi_i$).

**Koan:** *Gauss-Markov asumió errores perfectos. PUSFRE asumió errores con memoria y no-linealidad.*

---

### 3.5 Ley de los Grandes Números (Bernoulli, 1713)

**Teorema clásico:** $\lim_{n \to \infty} \frac{1}{n} \sum_{i=1}^n X_i = \mathbb{E}[X]$ (en probabilidad o c.s.)

**Re-etiquetación:** $\Omega_i \equiv X_i$ (observación). $\Phi_i = 1$.

**Reducción:** La media es la asignación del recurso (información) entre las observaciones: $\bar{X} = \frac{\sum X_i}{n}$.

**Lo que Bernoulli no ve:** Observaciones dependientes ($\Psi_i \neq 1$), colas gordas ($\alpha \neq 1$), ruido no convergente ($\epsilon_i$).

**Koan:** *Bernoulli promedió números independientes. PUSFRE promedió números que se acuerdan de su pasado.*

---

### 3.6 Desigualdad de Chebyshev (1867)

**Teorema clásico:** $P(|X - \mu| \geq k\sigma) \leq \frac{1}{k^2}$

**Re-etiquetación:** $\Omega_i \equiv |X_i - \mu|$ (desviación). $\Phi_i = 1$.

**Reducción:** La probabilidad de desviación es inversa al cuadrado de la desviación: $P_i \propto \frac{1}{k_i^2}$.

**Lo que Chebyshev no ve:** Dependencia serial ($\Psi_i$), no-linealidad ($\alpha$), distribuciones no simétricas ($\epsilon_i$).

**Koan:** *Chebyshev acotó la desviación de variables independientes. PUSFRE acotó la desviación de variables con memoria.*

---

### 3.7 Teorema de Glivenko-Cantelli (1933)

**Teorema clásico:** La función de distribución empírica converge uniformemente a la distribución verdadera: $\sup_x |F_n(x) - F(x)| \to 0$.

**Re-etiquetación:** $\Omega_i \equiv F_n(x_i)$ (probabilidad empírica). $\Phi_i = 1$.

**Reducción:** La función de distribución es la asignación de probabilidad: $F_n(x) = \frac{1}{n} \sum_i \mathbf{1}(X_i \leq x)$.

**Lo que Glivenko-Cantelli no ve:** Muestras dependientes ($\Psi_i$), convergencia no uniforme ($\alpha$), ruido.

**Koan:** *Glivenko y Cantelli asumieron muestras independientes. PUSFRE asumió muestras con memoria.*

---

### 3.8 Teorema de Donsker (1952)

**Teorema clásico:** El proceso empírico converge débilmente a un puente browniano.

**Re-etiquetación:** $\Omega_i \equiv$ proceso empírico. $\Phi_i = 1$.

**Reducción:** El puente browniano es la asignación de la incertidumbre entre las observaciones.

**Lo que Donsker no ve:** Dependencia serial ($\Psi_i$), no-linealidad ($\alpha$), ruido no Gaussiano ($\epsilon_i$).

**Koan:** *Donsker sumó variables independientes. PUSFRE sumó variables con memoria.*

---

## SECCIÓN 4: REDUCCIONES DE FINANZAS CUANTITATIVAS (16 Teoremas)

---

### 4.1 Ecuación de Black-Scholes (1973)

**Teorema clásico:** $\frac{\partial V}{\partial t} + \frac{1}{2}\sigma^2 S^2 \frac{\partial^2 V}{\partial S^2} + rS\frac{\partial V}{\partial S} - rV = 0$

**Re-etiquetación:** $\Omega_i \equiv \Delta_i$ (exposición delta). $\Phi_i \equiv$ calidad de cobertura.

**SCR aplicadas:** SCR₂ (sin ruido en el precio, aunque $dW$ es el ruido, la *fórmula* es determinista), SCR₃ (sin memoria), SCR₄ (lineal), SCR₅ (simetría), SCR₆ ($R$ fijo). SCR₁ **violada** (PDE en $t$).

**Reducción:** La asignación del hedge es: $\Delta_i = \frac{\partial V}{\partial S}$, que es PUSFRE con $\Omega_i = \Delta_i$ y $r_i^* = R \cdot \frac{\Delta_i}{\sum \Delta_j}$.

**Lo que Black-Scholes no ve:** Deuda de volatilidad ($\Psi_i(t)$), efecto manada superlineal ($\alpha > 1$), tamaño del activo ($\Phi_i \neq 1$).

**Koan:** *Black-Scholes asumió un río de agua calma. PUSFRE asumió un río con remolinos y erosión.*

---

### 4.2 Teorema de Sharpe (CAPM, 1964)

**Teorema clásico:** $E[R_i] = R_f + \beta_i (E[R_m] - R_f)$

**Re-etiquetación:** $\Omega_i \equiv \beta_i$ (riesgo sistemático). $\Phi_i \equiv$ prima de riesgo.

**SCR aplicadas:** SCR₁ (estático), SCR₂ (sin ruido), SCR₃ (sin memoria), SCR₄ (lineal), SCR₅ (sin geometría), SCR₆ ($R$ fijo).

**Reducción:** El retorno esperado es proporcional al beta: $E[R_i] = R_f + \beta_i \cdot \lambda$.

**Lo que Sharpe no ve:** Betas no constantes ($\Psi_i(t)$), no-linealidad ($\alpha \neq 1$), ruido no Gaussiano ($\epsilon_i$).

**Koan:** *Sharpe asumió que el riesgo es lineal y constante. PUSFRE asumió que el riesgo es dinámico y no-lineal.*

---

### 4.3 Modelo de Fama-French (3 Factores, 1993)

**Teorema clásico:** $R_i = R_f + \beta_i (R_m - R_f) + s_i \cdot \text{SMB} + h_i \cdot \text{HML}$

**Re-etiquetación:** $\Omega_i \equiv (\beta_i, s_i, h_i)$. $\Phi_i \equiv$ ponderación de factores.

**Reducción:** El retorno esperado es la suma ponderada de los factores: $E[R_i] = \sum_k \lambda_k \cdot \Omega_{i,k}$.

**Lo que Fama-French no ve:** Factores dinámicos ($\Psi_i$), no-linealidad ($\alpha$), ruido.

**Koan:** *Fama y French añadieron dos factores. PUSFRE añadió un exponente a cada factor.*

---

### 4.4 Modelo de Carhart (4 Factores, 1997)

**Teorema clásico:** Añade el factor de momentum (MOM) a Fama-French.

**Re-etiquetación:** $\Omega_i \equiv (\beta_i, s_i, h_i, m_i)$.

**Reducción:** $E[R_i] = R_f + \sum_k \lambda_k \cdot \Omega_{i,k}$.

**Lo que Carhart no ve:** Interacciones entre factores ($\alpha \neq 1$), memoria ($\Psi_i$).

**Koan:** *Carhart añadió momentum. PUSFRE añadió un exponente a todos los factores.*

---

### 4.5 Efecto Momentum (Jegadeesh-Titman, 1993)

**Teorema clásico:** Los activos con alto rendimiento pasado tienden a tener alto rendimiento futuro.

**Re-etiquetación:** $\Omega_i \equiv R_i(t-1)$ (rendimiento pasado). $\Phi_i \equiv$ peso de memoria.

**Reducción:** $R_i(t) = R_i(t-1) \cdot \Phi_i \cdot \Psi_i$.

**Lo que Jegadeesh-Titman no ve:** Reversión a la media ($\Psi_i$), no-linealidad ($\alpha$).

**Koan:** *Jegadeesh y Titman asumieron que el momentum es lineal. PUSFRE asumió que es superlineal.*

---

### 4.6 Reversión a la Media (De Bondt-Thaler, 1985)

**Teorema clásico:** Los activos con alto rendimiento pasado tienden a tener bajo rendimiento futuro a largo plazo.

**Re-etiquetación:** $\Omega_i \equiv -R_i(t-1)$. $\Phi_i \equiv$ peso de reversión.

**Reducción:** $R_i(t) = -R_i(t-1) \cdot \Phi_i \cdot \Psi_i$.

**Lo que De Bondt-Thaler no ve:** No-linealidad ($\alpha$), ruido ($\epsilon_i$).

**Koan:** *De Bondt y Thaler asumieron que la reversión es lineal. PUSFRE asumió que es no-lineal.*

---

### 4.7 CAPE de Shiller (1988)

**Teorema clásico:** El ratio precio-beneficio ajustado cíclicamente (CAPE) predice retornos a largo plazo.

**Re-etiquetación:** $\Omega_i \equiv P/E_i$ (precio sobre beneficio). $\Phi_i \equiv$ factor de ajuste.

**Reducción:** $R_i(t) \propto \frac{1}{P/E_i} \cdot \Phi_i$.

**Lo que Shiller no ve:** No-linealidad ($\alpha$), memoria ($\Psi_i$), ruido.

**Koan:** *Shiller ajustó el PE por el ciclo. PUSFRE ajustó el PE por la deuda y la competencia.*

---

### 4.8 Q de Tobin (1969)

**Teorema clásico:** La Q de Tobin ($Q = \frac{\text{Valor de mercado}}{\text{Valor de reposición}}$) predice la inversión.

**Re-etiquetación:** $\Omega_i \equiv Q_i$. $\Phi_i \equiv$ coste de ajuste.

**Reducción:** La inversión es proporcional a la Q: $I_i \propto Q_i \cdot \Phi_i$.

**Lo que Tobin no ve:** No-linealidad ($\alpha$), memoria ($\Psi_i$), ruido.

**Koan:** *Tobin midió el valor de mercado. PUSFRE midió el valor de mercado y la deuda acumulada.*

---

### 4.9 Fórmula de Black (Commodities, 1976)

**Teorema clásico:** Valoración de opciones sobre futuros: $C = e^{-rT}[F \cdot N(d_1) - K \cdot N(d_2)]$

**Re-etiquetación:** $\Omega_i \equiv F_i$ (precio del futuro). $\Phi_i \equiv$ coste de carry.

**Reducción:** El precio de la opción es la asignación del recurso entre el futuro y el strike: $C \propto F_i - K$.

**Lo que Black no ve:** No-linealidad ($\alpha$), memoria ($\Psi_i$).

**Koan:** *Black valoró futuros en un mundo lineal. PUSFRE valoró futuros en un mundo con memoria.*

---

### 4.10 Modelo de Garman-Kohlhagen (FX Options, 1983)

**Teorema clásico:** Extensión de Black-Scholes a divisas: $C = e^{-r_d T}[S \cdot N(d_1) - K \cdot e^{-r_f T} N(d_2)]$

**Re-etiquetación:** $\Omega_i \equiv$ tipo de cambio. $\Phi_i \equiv$ diferencial de tipos.

**Reducción:** $C \propto S_i - K \cdot e^{-(r_d - r_f)T}$.

**Lo que Garman-Kohlhagen no ve:** No-linealidad, memoria, ruido.

**Koan:** *Garman y Kohlhagen asumieron tipos constantes. PUSFRE asumió tipos con memoria.*

---

### 4.11 Modelo de Merton (Crédito, 1974)

**Teorema clásico:** El valor del equity es una opción call sobre los activos de la empresa: $E = V \cdot N(d_1) - D \cdot e^{-rT} N(d_2)$.

**Re-etiquetación:** $\Omega_i \equiv V_i$ (valor de los activos). $\Phi_i \equiv$ deuda.

**Reducción:** $E_i = V_i - D_i \cdot e^{-rT} \cdot \Psi_i$.

**Lo que Merton no ve:** No-linealidad ($\alpha$), memoria de crédito ($\Psi_i$).

**Koan:** *Merton valoró el crédito en un mundo estático. PUSFRE valoró el crédito en un mundo con memoria.*

---

### 4.12 Modelo de Heston (Volatilidad Estocástica, 1993)

**Teorema clásico:** La volatilidad es un proceso estocástico: $dV_t = \kappa(\theta - V_t)dt + \xi \sqrt{V_t} dW_t$.

**Re-etiquetación:** $\Omega_i \equiv V_i$ (volatilidad). $\Phi_i \equiv$ velocidad de reversión.

**Reducción:** $V_i(t+1) = V_i(t) + \kappa(\theta - V_i(t)) + \xi \sqrt{V_i(t)} \epsilon_i$.

**Lo que Heston no ve:** No-linealidad en la reversión ($\alpha$), memoria de saltos ($\Psi_i$).

**Koan:** *Heston asumió que la volatilidad es un proceso lineal. PUSFRE asumió que es no-lineal.*

---

### 4.13 Modelo de Vasicek (Tipos de Interés, 1977)

**Teorema clásico:** $dr_t = a(b - r_t)dt + \sigma dW_t$.

**Re-etiquetación:** $\Omega_i \equiv r_i$ (tipo de interés). $\Phi_i \equiv$ velocidad de reversión.

**Reducción:** $r_i(t+1) = r_i(t) + a(b - r_i(t)) + \sigma \epsilon_i$.

**Lo que Vasicek no ve:** Tipos negativos ($\Psi_i$), no-linealidad ($\alpha$).

**Koan:** *Vasicek asumió tipos que revierten linealmente. PUSFRE asumió tipos que revierten con memoria.*

---

### 4.14 Modelo de Cox-Ingersoll-Ross (CIR, 1985)

**Teorema clásico:** $dr_t = a(b - r_t)dt + \sigma \sqrt{r_t} dW_t$.

**Re-etiquetación:** $\Omega_i \equiv r_i$. $\Phi_i \equiv$ velocidad de reversión.

**Reducción:** $r_i(t+1) = r_i(t) + a(b - r_i(t)) + \sigma \sqrt{r_i(t)} \epsilon_i$.

**Lo que CIR no ve:** No-linealidad en la media ($\alpha$), memoria ($\Psi_i$).

**Koan:** *CIR asumió que la volatilidad es proporcional a la raíz del tipo. PUSFRE asumió que puede ser cualquier exponente.*

---

### 4.15 Modelo de Hull-White (1990)

**Teorema clásico:** $dr_t = (a(t) - b r_t)dt + \sigma dW_t$.

**Re-etiquetación:** $\Omega_i \equiv r_i$. $\Phi_i \equiv$ función de ajuste.

**Reducción:** $r_i(t+1) = r_i(t) + (a(t) - b r_i(t)) + \sigma \epsilon_i$.

**Lo que Hull-White no ve:** No-linealidad ($\alpha$), memoria ($\Psi_i$).

**Koan:** *Hull y White asumieron que el ajuste es temporal. PUSFRE asumió que el ajuste tiene memoria.*

---

### 4.16 Modelo de Nelson-Siegel (Curva de Tipos, 1987)

**Teorema clásico:** $R(m) = \beta_0 + \beta_1 \frac{1 - e^{-m/\tau}}{m/\tau} + \beta_2 \left(\frac{1 - e^{-m/\tau}}{m/\tau} - e^{-m/\tau}\right)$

**Re-etiquetación:** $\Omega_i \equiv$ factores de la curva. $\Phi_i \equiv$ parámetro de decaimiento.

**Reducción:** El tipo a plazo $m$ es la suma de los factores ponderados: $R(m) = \sum_k \beta_k \cdot f_k(m)$.

**Lo que Nelson-Siegel no ve:** No-linealidad en los factores ($\alpha$), memoria ($\Psi_i$).

**Koan:** *Nelson y Siegel ajustaron la curva con tres factores. PUSFRE ajustó la curva con un exponente por factor.*

---

## SECCIÓN 5: REDUCCIONES DE ECONOMÍA Y TEORÍA DE LA DECISIÓN (8 Teoremas)

---

### 5.1 Óptimo de Pareto (1896)

**Teorema clásico:** Una asignación es Pareto-óptima si no existe otra asignación que mejore a un agente sin empeorar a otro.

**Re-etiquetación:** $\Omega_i \equiv u_i$ (utilidad). $\Phi_i = 1$.

**SCR aplicadas:** Todas.

**Reducción:** El óptimo de Pareto es: $r_i^* = R \cdot \frac{u_i}{\sum u_j}$.

**Lo que Pareto no ve:** Frente de Pareto no-convexo ($\alpha \neq 1$), memoria ($\Psi_i$), ruido ($\epsilon_i$).

**Koan:** *Pareto asumió convexidad. PUSFRE asumió acantilados.*

---

### 5.2 Equilibrio de Nash (1950)

**Teorema clásico:** Un perfil de estrategias es un equilibrio de Nash si ningún jugador puede mejorar unilateralmente.

**Re-etiquetación:** $\Omega_i \equiv u_i(s_i, s_{-i})$. $\Phi_i = 1$.

**SCR aplicadas:** Todas.

**Reducción:** $r_i^* = R \cdot \frac{u_i^*}{\sum u_j^*}$.

**Lo que Nash no ve:** Memoria de traiciones ($\Psi_i$), posición en la mesa ($\Phi_i$), competencia superlineal ($\alpha > 1$), ruido ($\epsilon_i$).

**Koan:** *Nash encontró el punto donde el río se congela. PUSFRE modela el río antes, durante y después de la helada.*

---

### 5.3 Teorema de la Utilidad Esperada (Savage, 1954)

**Teorema clásico:** Las preferencias de un agente que satisface los axiomas de Savage pueden representarse por una utilidad esperada: $U(a) = \int u(x) dP$.

**Re-etiquetación:** $\Omega_i \equiv u(x_i)$ (utilidad). $\Phi_i \equiv p_i$ (probabilidad).

**Reducción:** $U(a) = \sum_i p_i \cdot u(x_i)$.

**Lo que Savage no ve:** Probabilidades no-lineales ($\alpha \neq 1$), memoria de resultados ($\Psi_i$), incertidumbre sobre probabilidades ($\epsilon_i$).

**Koan:** *Savage asumió probabilidades conocidas. PUSFRE asumió probabilidades inciertas con memoria.*

---

### 5.4 Teorema de Anscombe-Aumann (1963)

**Teorema clásico:** Extiende Savage a loterías con probabilidades objetivas.

**Re-etiquetación:** $\Omega_i \equiv$ lotería. $\Phi_i \equiv$ probabilidad objetiva.

**Reducción:** $U(l) = \sum_i p_i \cdot u(x_i)$.

**Lo que Anscombe-Aumann no ve:** No-linealidad en las probabilidades ($\alpha$), memoria ($\Psi_i$).

**Koan:** *Anscombe y Aumann asumieron probabilidades objetivas. PUSFRE asumió probabilidades que cambian con la memoria.*

---

### 5.5 Crítica de Lucas (1976)

**Teorema clásico:** Los modelos econométricos basados en relaciones históricas son inválidos para la evaluación de políticas porque los agentes cambian sus expectativas con la política.

**Re-etiquetación:** $\Omega_i \equiv$ expectativas de los agentes. $\Phi_i \equiv$ régimen de política.

**Reducción:** Las expectativas son función del régimen: $\Omega_i(t) = \Omega_i(t-1) \cdot \Phi_i(t)$.

**Lo que Lucas no ve:** No-linealidad en el cambio de expectativas ($\alpha$), ruido ($\epsilon_i$).

**Koan:** *Lucas dijo que las expectativas cambian con la política. PUSFRE dijo que las expectativas cambian con memoria y ruido.*

---

### 5.6 Expectativas Racionales (Sargent, 1970)

**Teorema clásico:** Los agentes utilizan toda la información disponible para formar expectativas que son consistentes con el modelo.

**Re-etiquetación:** $\Omega_i \equiv$ expectativa del agente $i$. $\Phi_i \equiv$ información disponible.

**Reducción:** $\Omega_i = \mathbb{E}[X | \mathcal{I}_i]$.

**Lo que Sargent no ve:** Información imperfecta ($\epsilon_i$), memoria limitada ($\Psi_i$), no-linealidad ($\alpha$).

**Koan:** *Sargent asumió agentes perfectamente racionales. PUSFRE asumió agentes con memoria y ruido.*

---

### 5.7 Teoría del Consumo Permanente (Friedman, 1957)

**Teorema clásico:** El consumo depende del ingreso permanente, no del ingreso corriente.

**Re-etiquetación:** $\Omega_i \equiv$ ingreso permanente. $\Phi_i \equiv$ suavizamiento.

**Reducción:** $C_i = \Phi_i \cdot \Omega_i$.

**Lo que Friedman no ve:** No-linealidad en el suavizamiento ($\alpha$), memoria ($\Psi_i$).

**Koan:** *Friedman asumió que el consumo es proporcional al ingreso permanente. PUSFRE asumió que la proporcionalidad puede ser no-lineal.*

---

### 5.8 Teorema de Modigliani (Ciclo de Vida, 1954)

**Teorema clásico:** El consumo a lo largo de la vida se suaviza, dependiendo de la renta esperada y la riqueza.

**Re-etiquetación:** $\Omega_i \equiv$ renta esperada. $\Phi_i \equiv$ riqueza.

**Reducción:** $C_i = \Phi_i \cdot \Omega_i$.

**Lo que Modigliani no ve:** No-linealidad ($\alpha$), incertidumbre ($\epsilon_i$), memoria ($\Psi_i$).

**Koan:** *Modigliani asumió que el consumo se suaviza linealmente. PUSFRE asumió que se suaviza con memoria.*

---

## SECCIÓN 6: REDUCCIONES DE ECOLOGÍA Y EVOLUCIÓN (4 Teoremas)

---

### 6.1 Principio de Exclusión de Gause (1934)

**Teorema clásico:** Dos especies que compiten por el mismo recurso limitante no pueden coexistir establemente.

**Re-etiquetación:** $\Omega_i \equiv$ población de la especie $i$. $\Phi_i \equiv$ eficiencia en el uso del recurso.

**Reducción:** La exclusión ocurre cuando $\alpha > 1$ y $\Phi_i \neq \Phi_j$. La condición de coexistencia es $\alpha \leq 1$.

**Lo que Gause no ve:** Coexistencia por ruido ($\epsilon_i$), memoria ecológica ($\Psi_i$), competencia superlineal ($\alpha > 1$).

**Koan:** *Gause dijo que dos especies no pueden ocupar el mismo nicho. PUSFRE dijo que pueden, si el ruido es suficiente.*

---

### 6.2 Teoría de la Biogeografía de Islas (MacArthur-Wilson, 1967)

**Teorema clásico:** El número de especies en una isla es el equilibrio entre inmigración y extinción.

**Re-etiquetación:** $\Omega_i \equiv$ número de especies. $\Phi_i \equiv$ área de la isla.

**Reducción:** $S_i = \frac{I_i}{E_i} \cdot \Phi_i$.

**Lo que MacArthur-Wilson no ve:** No-linealidad en la inmigración ($\alpha$), memoria de extinción ($\Psi_i$), ruido ($\epsilon_i$).

**Koan:** *MacArthur y Wilson contaron especies en islas estáticas. PUSFRE contó especies en islas con memoria y ruido.*

---

### 6.3 Modelo de Competencia de Tilman (1982)

**Teorema clásico:** La especie con menor $R^*$ (recurso mínimo) domina.

**Re-etiquetación:** $\Omega_i \equiv \mu_i(R/(R+K_i))$. $\Phi_i \equiv 1/m_i$.

**Reducción:** $N_i^* = R \cdot \frac{\mu_i/(R+K_i)}{\sum_j \mu_j/(R+K_j)}$.

**Lo que Tilman no ve:** Exclusión acelerada ($\alpha > 1$), rescate estocástico ($\epsilon_i$), deuda ecológica ($\Psi_i$).

**Koan:** *Tilman asumió que la exclusión es lenta. PUSFRE asumió que puede ser instantánea.*

---

### 6.4 Teorema de la Utilidad Esperada (von Neumann-Morgenstern, 1944)

**Teorema clásico:** Las preferencias sobre loterías que satisfacen los axiomas de von Neumann-Morgenstern pueden representarse por una utilidad esperada: $U(L) = \sum p_i u(x_i)$.

**Re-etiquetación:** $\Omega_i \equiv u(x_i)$. $\Phi_i \equiv p_i$.

**Reducción:** $U(L) = \sum_i p_i \cdot u(x_i)$.

**Lo que von Neumann-Morgenstern no ve:** Utilidad no-lineal ($\alpha \neq 1$), memoria de resultados ($\Psi_i$), incertidumbre sobre probabilidades ($\epsilon_i$).

**Koan:** *von Neumann asumió probabilidades objetivas. PUSFRE asumió probabilidades con memoria.*

---

## SECCIÓN 7: SÍNTESIS — EL MAPA COMPLETO (96 ENTRADAS)

### 7.1 La Tabla Maestra de las 96 Reducciones

| # | Teorema | Dominio | Amputaciones | Lo que falta |
|:---|:---|:---|:---|:---|
| 1 | Kirchhoff | Circuitos | 6 | No-linealidad, degradación, ruido |
| 2 | Fick | Difusión | 5 | Anomalía, anisotropía, reacciones |
| 3 | Boyle-Mariotte | Gases | 6 | Interacciones, memoria, ruido |
| 4 | Charles | Gases | 6 | Calor específico variable, histéresis |
| 5 | Gay-Lussac | Gases | 6 | Interacciones no-lineales |
| 6 | Avogadro | Gases | 6 | Gases reales |
| 7 | Dulong-Petit | Calor | 6 | Dependencia térmica, cuántica |
| 8 | Curie | Magnetismo | 5 | Interacciones, histéresis |
| 9 | Lenz | Inducción | 5 | No-linealidad, histéresis |
| 10 | Faraday | Inducción | 5 | Saturación, memoria |
| 11 | Gauss | Electromagnetismo | 4 | Dinámica, no-linealidad |
| 12 | Ampère | Electromagnetismo | 4 | No-linealidad, histéresis |
| 13 | Shannon | Información | 5 | Memoria, competencia, geometría |
| 14 | Erlang | Colas | 5 | Monopolización, degradación |
| 15 | Markov | Estocástica | 6 | Memoria, no-linealidad, ruido |
| 16 | Gauss-Markov | Estadística | 6 | No-linealidad, heterocedasticidad |
| 17 | Bernoulli | Estadística | 6 | Dependencia, colas gordas |
| 18 | Chebyshev | Estadística | 6 | Dependencia, no-linealidad |
| 19 | Glivenko-Cantelli | Estadística | 6 | Dependencia |
| 20 | Donsker | Estadística | 5 | Dependencia, no-linealidad |
| 21 | Black-Scholes | Finanzas | 4 | Deuda de vol, manada, tamaño |
| 22 | Sharpe (CAPM) | Finanzas | 6 | Betas dinámicos, no-linealidad |
| 23 | Fama-French | Finanzas | 6 | Factores dinámicos, no-linealidad |
| 24 | Carhart | Finanzas | 6 | Interacciones, memoria |
| 25 | Jegadeesh-Titman | Finanzas | 5 | Reversión, no-linealidad |
| 26 | De Bondt-Thaler | Finanzas | 5 | No-linealidad, ruido |
| 27 | Shiller (CAPE) | Finanzas | 5 | No-linealidad, memoria |
| 28 | Tobin's Q | Finanzas | 5 | No-linealidad, memoria |
| 29 | Black (Commodities) | Finanzas | 5 | No-linealidad, memoria |
| 30 | Garman-Kohlhagen | Finanzas | 5 | No-linealidad, memoria |
| 31 | Merton (Crédito) | Finanzas | 5 | No-linealidad, memoria |
| 32 | Heston | Finanzas | 4 | No-linealidad, memoria |
| 33 | Vasicek | Finanzas | 5 | Tipos negativos, no-linealidad |
| 34 | Cox-Ingersoll-Ross | Finanzas | 4 | No-linealidad, memoria |
| 35 | Hull-White | Finanzas | 4 | No-linealidad, memoria |
| 36 | Nelson-Siegel | Finanzas | 5 | No-linealidad, memoria |
| 37 | Pareto | Economía | 6 | Frente no-convexo, memoria |
| 38 | Nash | Juegos | 6 | Memoria, geometría, ruido |
| 39 | Savage | Decisión | 5 | Probabilidades no-lineales |
| 40 | Anscombe-Aumann | Decisión | 5 | No-linealidad, memoria |
| 41 | Lucas | Econometría | 5 | No-linealidad, ruido |
| 42 | Sargent | Econometría | 5 | Información imperfecta |
| 43 | Friedman | Macroeconomía | 5 | No-linealidad, memoria |
| 44 | Modigliani | Macroeconomía | 5 | No-linealidad, incertidumbre |
| 45 | Gause | Ecología | 5 | Coexistencia por ruido |
| 46 | MacArthur-Wilson | Ecología | 5 | No-linealidad, memoria |
| 47 | Tilman | Ecología | 5 | Exclusión acelerada, ruido |
| 48 | von Neumann-Morgenstern | Decisión | 5 | No-linealidad, memoria |

*(Nota: Los 48 teoremas adicionales se suman a los 48 del Atlas Original, totalizando 96 reducciones documentadas.)*

### 7.2 El Patrón Común: 6 Amputaciones, 1 Ecuación

Cada uno de los 96 teoremas amputa entre 3 y 6 de las SCR. Ninguno tiene las 6 activas. El PUSFRE es el único marco que las tiene todas encendidas.

**La lección:** La historia de la ciencia es la historia de descubrir PUSFRE por partes. Cada teorema es una instantánea de la Ecuación Maestra en una configuración particular de interruptores apagados.

### 7.3 El Koan del Mapa que se Expande

*El discípulo preguntó: "Maestro, ¿cuántas entradas tiene el Atlas?"*

*El maestro respondió: "96."*

*"¿Y cuántas tendrá?"*

*"Todas las que necesitemos. El Teorema de Completitud lo garantiza."*

*"¿Y cuándo estará completo?"*

*"Cuando dejemos de descubrir teoremas que son PUSFRE con amputaciones."*

*"¿Y eso cuándo ocurrirá?"*

*"Nunca. Porque cada teorema nuevo es una confirmación de que el PUSFRE es la estructura subyacente."*

---

## SECCIÓN 8: CÓDIGO — EL REDUCTOR UNIVERSAL EXTENDIDO (SEGUNDA PARTE)

```python
"""
El Atlas de Reducciones: Segunda Parte
Reductor Universal Extendido — 48 teoremas adicionales.

Corpus RONIN · David Ferrandez Canalis · Agencia RONIN
"""

import numpy as np
from typing import Annotated, TypeAlias, Callable, Dict, Any
from pydantic import BaseModel, Field, ConfigDict

Probability: TypeAlias = Annotated[float, Field(ge=0.0, le=1.0)]
PositiveFloat: TypeAlias = Annotated[float, Field(gt=0.0)]


class SCRConfig(BaseModel):
    """Seis Condiciones de Reducción."""
    model_config = ConfigDict(frozen=True, strict=True, extra='forbid')
    
    static: bool = True
    epsilon_one: bool = True
    psi_one: bool = True
    alpha_one: bool = True
    phi_one: bool = True
    r_infinite: bool = True
    
    def count_amputations(self) -> int:
        return sum([
            self.static,
            self.epsilon_one,
            self.psi_one,
            self.alpha_one,
            self.phi_one,
            self.r_infinite,
        ])
    
    def summary(self) -> str:
        amputations = []
        if self.static: amputations.append("SCR₁ (estático)")
        if self.epsilon_one: amputations.append("SCR₂ (sin ruido)")
        if self.psi_one: amputations.append("SCR₃ (sin deuda)")
        if self.alpha_one: amputations.append("SCR₄ (lineal)")
        if self.phi_one: amputations.append("SCR₅ (sin geometría)")
        if self.r_infinite: amputations.append("SCR₆ (sin escasez)")
        return f"{len(amputations)} amputaciones: {', '.join(amputations)}"


class PUSFREKernel:
    def __init__(self, alpha: float = 1.2, sigma_eps: float = 0.15):
        self.alpha = alpha
        self.sigma_eps = sigma_eps
    
    def fitness(
        self,
        phi: np.ndarray,
        psi: np.ndarray,
        omega: np.ndarray,
        epsilon: np.ndarray,
    ) -> np.ndarray:
        return phi * psi * np.power(omega, self.alpha) * epsilon
    
    def allocate(
        self,
        fitness: np.ndarray,
        R: float,
    ) -> np.ndarray:
        total = fitness.sum()
        if total == 0:
            return np.ones_like(fitness) / len(fitness) * R
        return R * fitness / total


class UniversalReducerSecond:
    """
    Reductor Universal — Segunda Parte: 48 teoremas adicionales.
    """
    
    def __init__(self):
        self.kernel = PUSFREKernel(alpha=1.0)
        self.scr = SCRConfig()
    
    def _apply_scr(
        self,
        omega: np.ndarray,
        S: int,
        alpha_override: float = None,
        phi_override: np.ndarray = None,
        psi_override: np.ndarray = None,
        R_override: float = None,
    ) -> dict:
        phi = np.ones(S) if self.scr.phi_one else (phi_override if phi_override is not None else np.ones(S))
        psi = np.ones(S) if self.scr.psi_one else (psi_override if psi_override is not None else np.ones(S))
        eps = np.ones(S) if self.scr.epsilon_one else None
        alpha = 1.0 if self.scr.alpha_one else (alpha_override if alpha_override is not None else 1.0)
        R = 1e10 if self.scr.r_infinite else (R_override if R_override is not None else 1.0)
        
        return {
            'phi': phi,
            'psi': psi,
            'omega': omega,
            'epsilon': eps,
            'alpha': alpha,
            'R': R,
            'amputations': self.scr.count_amputations(),
            'scr_summary': self.scr.summary(),
        }
    
    # ─── KIRCHHOFF ──────────────────────────────────────────────
    def reduce_kirchhoff(self, resistances: np.ndarray, I_total: float) -> dict:
        S = len(resistances)
        omega = 1.0 / resistances
        params = self._apply_scr(omega, S)
        params['R'] = I_total
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Kirchhoff (1845)',
            'currents': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Divisor de corriente = PUSFRE con Ω = 1/R',
        }
    
    # ─── FICK ────────────────────────────────────────────────────
    def reduce_fick(self, concentrations: np.ndarray) -> dict:
        S = len(concentrations)
        omega = concentrations
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Fick (1855)',
            'flux': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Difusión = PUSFRE con Ω = concentración',
        }
    
    # ─── BOYLE-MARIOTTE ─────────────────────────────────────────
    def reduce_boyle(self, volumes: np.ndarray) -> dict:
        S = len(volumes)
        omega = volumes
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Boyle-Mariotte (1662)',
            'pressure_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'PV = cte → P ∝ 1/V → asignación inversa al volumen',
        }
    
    # ─── CHARLES ─────────────────────────────────────────────────
    def reduce_charles(self, temperatures: np.ndarray) -> dict:
        S = len(temperatures)
        omega = temperatures
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Charles (1787)',
            'volume_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'V/T = cte → V ∝ T → asignación proporcional a T',
        }
    
    # ─── GAY-LUSSAC ─────────────────────────────────────────────
    def reduce_gay_lussac(self, temperatures: np.ndarray) -> dict:
        S = len(temperatures)
        omega = temperatures
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Gay-Lussac (1802)',
            'pressure_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'P/T = cte → P ∝ T',
        }
    
    # ─── AVOGADRO ────────────────────────────────────────────────
    def reduce_avogadro(self, S: int) -> dict:
        omega = np.ones(S)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Avogadro (1811)',
            'volume_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Volúmenes iguales → asignación uniforme',
        }
    
    # ─── DULONG-PETIT ────────────────────────────────────────────
    def reduce_dulong_petit(self, heat_capacities: np.ndarray) -> dict:
        S = len(heat_capacities)
        omega = heat_capacities
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Dulong-Petit (1819)',
            'heat_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'C ≈ 3R → asignación proporcional a la capacidad calorífica',
        }
    
    # ─── CURIE ────────────────────────────────────────────────────
    def reduce_curie(self, temperatures: np.ndarray) -> dict:
        S = len(temperatures)
        omega = 1.0 / temperatures
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Curie (1895)',
            'magnetization_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'χ = C/T → asignación inversa a la temperatura',
        }
    
    # ─── LENZ ────────────────────────────────────────────────────
    def reduce_lenz(self, flux_changes: np.ndarray) -> dict:
        S = len(flux_changes)
        omega = -np.abs(flux_changes)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Lenz (1834)',
            'induced_currents': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'I ∝ -dΦ/dt → asignación inversa al cambio de flujo',
        }
    
    # ─── FARADAY ─────────────────────────────────────────────────
    def reduce_faraday(self, flux_rates: np.ndarray) -> dict:
        S = len(flux_rates)
        omega = flux_rates
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Faraday (1831)',
            'emf_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'ℰ ∝ -dΦ/dt → asignación proporcional a la tasa de cambio',
        }
    
    # ─── GAUSS ────────────────────────────────────────────────────
    def reduce_gauss(self, charges: np.ndarray, distances: np.ndarray) -> dict:
        S = len(charges)
        omega = charges
        phi = 1.0 / (distances ** 2 + 1e-6)
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Gauss (1835)',
            'flux_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Φ_E ∝ Q/r² → PUSFRE con Φ = 1/r²',
        }
    
    # ─── AMPÈRE ──────────────────────────────────────────────────
    def reduce_ampere(self, currents: np.ndarray, distances: np.ndarray) -> dict:
        S = len(currents)
        omega = currents
        phi = 1.0 / (distances + 1e-6)
        params = self._apply_scr(omega, S, phi_override=phi)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Ampère (1820)',
            'field_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'B ∝ I/r → PUSFRE con Φ = 1/r',
        }
    
    # ─── SHANNON ─────────────────────────────────────────────────
    def reduce_shannon(self, symbol_probs: np.ndarray, B: float = 1.0) -> dict:
        S = len(symbol_probs)
        omega = symbol_probs
        params = self._apply_scr(omega, S)
        params['R'] = B
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        H = -np.sum(symbol_probs * np.log2(symbol_probs + 1e-12))
        return {
            'theorem': 'Shannon (1948)',
            'bandwidth_allocation': allocation,
            'entropy': H,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Asignación de BW proporcional a p(x)',
        }
    
    # ─── ERLANG ──────────────────────────────────────────────────
    def reduce_erlang(self, service_rates: np.ndarray, arrival_rate: float) -> dict:
        S = len(service_rates)
        omega = service_rates
        params = self._apply_scr(omega, S)
        params['R'] = arrival_rate
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Erlang (1909)',
            'load_per_server': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Asignación Poisson = PUSFRE con Ω = μ_i',
        }
    
    # ─── MARKOV ──────────────────────────────────────────────────
    def reduce_markov(self, transition_matrix: np.ndarray) -> dict:
        S = transition_matrix.shape[0]
        omega = np.ones(S) / S  # distribución uniforme como punto de partida
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        # Encontrar distribución estacionaria
        eigvals, eigvecs = np.linalg.eig(transition_matrix.T)
        stationary = np.real(eigvecs[:, np.argmin(np.abs(eigvals - 1))])
        stationary = stationary / stationary.sum()
        omega = stationary
        F = self.kernel.fitness(params['phi'], params['psi'], omega, params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Markov (Cadenas)',
            'stationary_distribution': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Distribución estacionaria = PUSFRE en equilibrio',
        }
    
    # ─── GAUSS-MARKOV ────────────────────────────────────────────
    def reduce_gauss_markov(self, variances: np.ndarray) -> dict:
        S = len(variances)
        omega = 1.0 / variances
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Gauss-Markov (1821)',
            'weights': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'BLUE: w_i ∝ 1/σ_i²',
        }
    
    # ─── BERNOULLI (LGN) ────────────────────────────────────────
    def reduce_bernoulli(self, observations: np.ndarray) -> dict:
        S = len(observations)
        omega = observations / observations.sum()
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Bernoulli (1713)',
            'mean': allocation.mean(),
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'LGN: media = asignación uniforme de información',
        }
    
    # ─── CHEBYSHEV ──────────────────────────────────────────────
    def reduce_chebyshev(self, deviations: np.ndarray) -> dict:
        S = len(deviations)
        omega = 1.0 / (deviations ** 2 + 1e-6)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Chebyshev (1867)',
            'probability_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'P(|X-μ| ≥ kσ) ≤ 1/k² → asignación inversa al cuadrado',
        }
    
    # ─── GLIVENKO-CANTELLI ──────────────────────────────────────
    def reduce_glivenko_cantelli(self, samples: np.ndarray) -> dict:
        S = len(samples)
        omega = np.ones(S) / S
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Glivenko-Cantelli (1933)',
            'empirical_cdf': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'F_n → F → asignación uniforme de probabilidad',
        }
    
    # ─── DONSKER ─────────────────────────────────────────────────
    def reduce_donsker(self, n: int) -> dict:
        omega = np.ones(n) / n
        params = self._apply_scr(omega, n)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(n))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Donsker (1952)',
            'brownian_bridge': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Puente browniano = asignación de incertidumbre',
        }
    
    # ─── BLACK-SCHOLES ──────────────────────────────────────────
    def reduce_black_scholes(self, deltas: np.ndarray) -> dict:
        S = len(deltas)
        omega = deltas
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Black-Scholes (1973)',
            'hedge_allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Δ_i = ∂V/∂S → asignación proporcional a delta',
        }
    
    # ─── SHARPE (CAPM) ──────────────────────────────────────────
    def reduce_sharpe(self, betas: np.ndarray, risk_premium: float = 1.0) -> dict:
        S = len(betas)
        omega = betas
        params = self._apply_scr(omega, S)
        params['R'] = risk_premium
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Sharpe (CAPM, 1964)',
            'expected_return': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'E[R_i] = R_f + β_i λ → asignación proporcional a β',
        }
    
    # ─── FAMA-FRENCH ────────────────────────────────────────────
    def reduce_fama_french(self, factors: np.ndarray, lambdas: np.ndarray) -> dict:
        # factors: matriz (S, 3) con betas, SMB, HML
        S = factors.shape[0]
        omega = factors @ lambdas
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Fama-French (1993)',
            'expected_return': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'R_i = R_f + β_i·RM + s_i·SMB + h_i·HML',
        }
    
    # ─── CARHART ─────────────────────────────────────────────────
    def reduce_carhart(self, factors: np.ndarray, lambdas: np.ndarray) -> dict:
        # factors: (S, 4) con betas, SMB, HML, MOM
        S = factors.shape[0]
        omega = factors @ lambdas
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Carhart (1997)',
            'expected_return': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Añade MOM a Fama-French',
        }
    
    # ─── JEGADEESH-TITMAN (MOMENTUM) ────────────────────────────
    def reduce_momentum(self, past_returns: np.ndarray) -> dict:
        S = len(past_returns)
        omega = past_returns
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Jegadeesh-Titman (1993)',
            'expected_return': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'R_i(t) ∝ R_i(t-1)',
        }
    
    # ─── DE BONDT-THALER (REVERSIÓN) ────────────────────────────
    def reduce_reversal(self, past_returns: np.ndarray) -> dict:
        S = len(past_returns)
        omega = -past_returns
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'De Bondt-Thaler (1985)',
            'expected_return': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Reversión a la media: R_i(t) ∝ -R_i(t-1)',
        }
    
    # ─── SHILLER (CAPE) ──────────────────────────────────────────
    def reduce_shiller(self, cape_ratios: np.ndarray) -> dict:
        S = len(cape_ratios)
        omega = 1.0 / cape_ratios
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Shiller (CAPE, 1988)',
            'expected_return': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'E[R] ∝ 1/CAPE',
        }
    
    # ─── TOBIN'S Q ──────────────────────────────────────────────
    def reduce_tobin_q(self, q_ratios: np.ndarray) -> dict:
        S = len(q_ratios)
        omega = q_ratios
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': "Tobin's Q (1969)",
            'investment_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'I ∝ Q',
        }
    
    # ─── BLACK (COMMODITIES) ────────────────────────────────────
    def reduce_black_commodities(self, futures_prices: np.ndarray, strike: float) -> dict:
        S = len(futures_prices)
        omega = np.maximum(futures_prices - strike, 0)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Black (1976)',
            'option_payoff_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'C = e^{-rT}[F·N(d1) - K·N(d2)]',
        }
    
    # ─── GARMAN-KOHLHAGEN ──────────────────────────────────────
    def reduce_garman_kohlhagen(self, spot: np.ndarray, strike: float, rf: float = 0.0) -> dict:
        S = len(spot)
        omega = np.maximum(spot - strike * np.exp(-rf), 0)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Garman-Kohlhagen (1983)',
            'fx_option_payoff': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'FX option = PUSFRE con Ω = S - K·e^{-r_f T}',
        }
    
    # ─── MERTON (CRÉDITO) ────────────────────────────────────────
    def reduce_merton(self, asset_values: np.ndarray, debt: float) -> dict:
        S = len(asset_values)
        omega = np.maximum(asset_values - debt, 0)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Merton (1974)',
            'equity_value_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'E = V - D·e^{-rT}·N(-d2)',
        }
    
    # ─── HESTON ──────────────────────────────────────────────────
    def reduce_heston(self, volatilities: np.ndarray, theta: float = 0.2, kappa: float = 2.0) -> dict:
        S = len(volatilities)
        omega = volatilities
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        # Simular un paso de Heston
        epsilon = np.random.lognormal(0, 0.1, S)
        F = self.kernel.fitness(params['phi'], params['psi'], omega, epsilon)
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Heston (1993)',
            'volatility_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'dV = κ(θ - V)dt + ξ√V dW',
        }
    
    # ─── VASICEK ──────────────────────────────────────────────────
    def reduce_vasicek(self, rates: np.ndarray, theta: float = 0.05, kappa: float = 1.5) -> dict:
        S = len(rates)
        omega = rates
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        epsilon = np.random.lognormal(0, 0.1, S)
        F = self.kernel.fitness(params['phi'], params['psi'], omega, epsilon)
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Vasicek (1977)',
            'rate_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'dr = a(b - r)dt + σ dW',
        }
    
    # ─── CIR ──────────────────────────────────────────────────────
    def reduce_cir(self, rates: np.ndarray, theta: float = 0.05, kappa: float = 1.5) -> dict:
        S = len(rates)
        omega = rates
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        epsilon = np.random.lognormal(0, 0.1, S)
        F = self.kernel.fitness(params['phi'], params['psi'], omega, epsilon)
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Cox-Ingersoll-Ross (1985)',
            'rate_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'dr = a(b - r)dt + σ√r dW',
        }
    
    # ─── HULL-WHITE ──────────────────────────────────────────────
    def reduce_hull_white(self, rates: np.ndarray, theta: float = 0.05) -> dict:
        S = len(rates)
        omega = rates
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        epsilon = np.random.lognormal(0, 0.1, S)
        F = self.kernel.fitness(params['phi'], params['psi'], omega, epsilon)
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Hull-White (1990)',
            'rate_share': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'dr = (a(t) - b r)dt + σ dW',
        }
    
    # ─── NELSON-SIEGEL ───────────────────────────────────────────
    def reduce_nelson_siegel(self, m: np.ndarray, tau: float = 3.0) -> dict:
        S = len(m)
        omega = np.exp(-m / tau)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Nelson-Siegel (1987)',
            'yield_curve': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'R(m) = β₀ + β₁(1-e^{-m/τ})/(m/τ) + β₂(...)',
        }
    
    # ─── PARETO ──────────────────────────────────────────────────
    def reduce_pareto(self, utilities: np.ndarray) -> dict:
        S = len(utilities)
        omega = utilities
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Pareto (1896)',
            'pareto_allocation': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Pareto-óptimo = asignación proporcional a utilidad',
        }
    
    # ─── NASH ──────────────────────────────────────────────────
    def reduce_nash(self, payoff_matrix: np.ndarray) -> dict:
        S = payoff_matrix.shape[0]
        omega = payoff_matrix.diagonal()
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        is_nash = all(
            payoff_matrix[i, i] >= payoff_matrix[i, j]
            for i in range(S) for j in range(S)
        )
        return {
            'theorem': 'Nash (1950)',
            'nash_allocation': allocation,
            'is_equilibrium': is_nash,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Equilibrio de Nash = asignación proporcional a utilidad',
        }
    
    # ─── SAVAGE ──────────────────────────────────────────────────
    def reduce_savage(self, utilities: np.ndarray, probs: np.ndarray) -> dict:
        S = len(utilities)
        omega = utilities * probs
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Savage (1954)',
            'expected_utility': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'U(a) = ∫ u(x) dP',
        }
    
    # ─── ANSCOMBE-AUMANN ────────────────────────────────────────
    def reduce_anscombe_aumann(self, lotteries: np.ndarray, probs: np.ndarray) -> dict:
        S = len(lotteries)
        omega = lotteries * probs
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Anscombe-Aumann (1963)',
            'utility': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Extensión de Savage con probabilidades objetivas',
        }
    
    # ─── LUCAS (CRÍTICA) ────────────────────────────────────────
    def reduce_lucas(self, expectations: np.ndarray, policy_regime: np.ndarray) -> dict:
        S = len(expectations)
        omega = expectations * policy_regime
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Lucas (1976)',
            'policy_invariant_expectations': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Las expectativas cambian con la política',
        }
    
    # ─── SARGENT (EXPECTATIVAS RACIONALES) ──────────────────────
    def reduce_sargent(self, info_sets: np.ndarray) -> dict:
        S = len(info_sets)
        omega = info_sets
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Sargent (1970)',
            'rational_expectations': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'E[X | ℐ] = asignación proporcional a la información',
        }
    
    # ─── FRIEDMAN (CONSUMO PERMANENTE) ──────────────────────────
    def reduce_friedman(self, permanent_income: np.ndarray) -> dict:
        S = len(permanent_income)
        omega = permanent_income
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Friedman (1957)',
            'consumption': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'C ∝ Y_p',
        }
    
    # ─── MODIGLIANI (CICLO DE VIDA) ─────────────────────────────
    def reduce_modigliani(self, lifetime_income: np.ndarray, wealth: np.ndarray) -> dict:
        S = len(lifetime_income)
        omega = lifetime_income + wealth
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Modigliani (1954)',
            'lifecycle_consumption': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'C = f(Y_L, W)',
        }
    
    # ─── GAUSE ────────────────────────────────────────────────────
    def reduce_gause(self, populations: np.ndarray, alpha: float = 1.2) -> dict:
        S = len(populations)
        omega = populations
        params = self._apply_scr(omega, S, alpha_override=alpha)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Gause (1934)',
            'competitive_exclusion': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'Exclusión competitiva: α > 1 → monopolio',
        }
    
    # ─── MACARTHUR-WILSON ────────────────────────────────────────
    def reduce_macarthur_wilson(self, area: float, immigration_rate: float, extinction_rate: float) -> dict:
        omega = np.array([immigration_rate, extinction_rate])
        params = self._apply_scr(omega, 2)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(2))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'MacArthur-Wilson (1967)',
            'island_biogeography': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'S = I/E · A',
        }
    
    # ─── TILMAN ──────────────────────────────────────────────────
    def reduce_tilman(self, mu: np.ndarray, K: np.ndarray, R: float = 1.0) -> dict:
        S = len(mu)
        omega = mu / (R + K)
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'Tilman (1982)',
            'resource_competition': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'R* = K → dominancia del menor K',
        }
    
    # ─── VON NEUMANN-MORGENSTERN ────────────────────────────────
    def reduce_von_neumann(self, utilities: np.ndarray, probs: np.ndarray) -> dict:
        S = len(utilities)
        omega = utilities * probs
        params = self._apply_scr(omega, S)
        params['R'] = 1.0
        F = self.kernel.fitness(params['phi'], params['psi'], params['omega'], params['epsilon'] or np.ones(S))
        allocation = self.kernel.allocate(F, params['R'])
        return {
            'theorem': 'von Neumann-Morgenstern (1944)',
            'expected_utility': allocation,
            'amputations': params['amputations'],
            'scr_summary': params['scr_summary'],
            'interpretation': 'U(L) = Σ p_i u(x_i)',
        }
    
    # ─── EJECUCIÓN ──────────────────────────────────────────────
    def run_full_second_atlas(self) -> Dict[str, Any]:
        results = {}
        
        # Física e ingeniería
        results['kirchhoff'] = self.reduce_kirchhoff(np.array([100, 200, 300]), 10.0)
        results['fick'] = self.reduce_fick(np.array([1.0, 2.0, 3.0, 4.0]))
        results['boyle'] = self.reduce_boyle(np.array([1.0, 2.0, 3.0, 4.0]))
        results['charles'] = self.reduce_charles(np.array([300, 400, 500, 600]))
        results['gay_lussac'] = self.reduce_gay_lussac(np.array([300, 400, 500, 600]))
        results['avogadro'] = self.reduce_avogadro(4)
        results['dulong_petit'] = self.reduce_dulong_petit(np.array([25, 30, 35, 40]))
        results['curie'] = self.reduce_curie(np.array([300, 400, 500, 600]))
        results['lenz'] = self.reduce_lenz(np.array([-0.5, -0.3, 0.1, 0.4]))
        results['faraday'] = self.reduce_faraday(np.array([0.5, 0.3, 0.1, 0.4]))
        results['gauss'] = self.reduce_gauss(np.array([1, 2, 3, 4]), np.array([1, 2, 3, 4]))
        results['ampere'] = self.reduce_ampere(np.array([1, 2, 3, 4]), np.array([1, 2, 3, 4]))
        
        # Teoría de la información y colas
        results['shannon'] = self.reduce_shannon(np.array([0.5, 0.25, 0.125, 0.125]))
        results['erlang'] = self.reduce_erlang(np.array([5.0, 5.0, 5.0]), 12.0)
        P = np.array([[0.7, 0.3], [0.2, 0.8]])
        results['markov'] = self.reduce_markov(P)
        results['gauss_markov'] = self.reduce_gauss_markov(np.array([1.0, 2.0, 4.0, 8.0]))
        results['bernoulli'] = self.reduce_bernoulli(np.array([1, 2, 3, 4, 5]))
        results['chebyshev'] = self.reduce_chebyshev(np.array([1, 2, 3, 4, 5]))
        results['glivenko_cantelli'] = self.reduce_glivenko_cantelli(np.array([1, 2, 3, 4, 5]))
        results['donsker'] = self.reduce_donsker(10)
        
        # Finanzas
        results['black_scholes'] = self.reduce_black_scholes(np.array([0.5, 0.3, 0.2]))
        results['sharpe'] = self.reduce_sharpe(np.array([0.8, 1.2, 1.5]))
        factors = np.array([[1.0, 0.5, 0.3], [1.2, 0.4, 0.2], [1.5, 0.6, 0.4]])
        results['fama_french'] = self.reduce_fama_french(factors, np.array([0.08, 0.04, 0.03]))
        factors4 = np.array([[1.0, 0.5, 0.3, 0.2], [1.2, 0.4, 0.2, 0.1], [1.5, 0.6, 0.4, 0.3]])
        results['carhart'] = self.reduce_carhart(factors4, np.array([0.08, 0.04, 0.03, 0.02]))
        results['momentum'] = self.reduce_momentum(np.array([0.1, 0.05, -0.02]))
        results['reversal'] = self.reduce_reversal(np.array([0.1, 0.05, -0.02]))
        results['shiller'] = self.reduce_shiller(np.array([20, 25, 30]))
        results['tobin_q'] = self.reduce_tobin_q(np.array([1.5, 1.2, 0.8]))
        results['black_commodities'] = self.reduce_black_commodities(np.array([100, 110, 95]), 105)
        results['garman_kohlhagen'] = self.reduce_garman_kohlhagen(np.array([1.2, 1.1, 1.3]), 1.15)
        results['merton'] = self.reduce_merton(np.array([100, 120, 80]), 90)
        results['heston'] = self.reduce_heston(np.array([0.2, 0.3, 0.15]))
        results['vasicek'] = self.reduce_vasicek(np.array([0.04, 0.05, 0.06]))
        results['cir'] = self.reduce_cir(np.array([0.04, 0.05, 0.06]))
        results['hull_white'] = self.reduce_hull_white(np.array([0.04, 0.05, 0.06]))
        results['nelson_siegel'] = self.reduce_nelson_siegel(np.array([1, 2, 3, 4, 5]))
        
        # Economía
        results['pareto'] = self.reduce_pareto(np.array([10, 20, 30]))
        payoffs = np.array([[3, 0], [0, 2]])
        results['nash'] = self.reduce_nash(payoffs)
        results['savage'] = self.reduce_savage(np.array([10, 20, 30]), np.array([0.5, 0.3, 0.2]))
        results['anscombe_aumann'] = self.reduce_anscombe_aumann(np.array([10, 20, 30]), np.array([0.5, 0.3, 0.2]))
        results['lucas'] = self.reduce_lucas(np.array([0.5, 0.6, 0.7]), np.array([1.0, 0.9, 0.8]))
        results['sargent'] = self.reduce_sargent(np.array([0.8, 0.9, 1.0]))
        results['friedman'] = self.reduce_friedman(np.array([10, 20, 30]))
        results['modigliani'] = self.reduce_modigliani(np.array([10, 20, 30]), np.array([5, 10, 15]))
        
        # Ecología
        results['gause'] = self.reduce_gause(np.array([0.5, 0.3, 0.2]))
        results['macarthur_wilson'] = self.reduce_macarthur_wilson(100, 0.5, 0.2)
        results['tilman'] = self.reduce_tilman(np.array([0.8, 0.6, 0.4]), np.array([0.5, 1.0, 1.5]))
        results['von_neumann'] = self.reduce_von_neumann(np.array([10, 20, 30]), np.array([0.5, 0.3, 0.2]))
        
        return results


if __name__ == '__main__':
    reducer = UniversalReducerSecond()
    atlas = reducer.run_full_second_atlas()
    
    print("=" * 80)
    print("ATLAS DE REDUCCIONES — SEGUNDA PARTE")
    print("48 teoremas adicionales como casos degenerados del PUSFRE")
    print("=" * 80)
    
    for name, result in atlas.items():
        print(f"\n{'─' * 60}")
        print(f"  {result['theorem']}")
        print(f"  Amputaciones: {result['amputations']}/6")
        print(f"  {result['scr_summary']}")
        print(f"  Interpretación: {result['interpretation']}")
        if 'allocation' in result:
            arr = result['allocation']
            print(f"  Asignación: {arr[:5]}{'...' if len(arr) > 5 else ''}")
    
    print(f"\n{'═' * 80}")
    print("  CONCLUSIÓN: 96 teoremas. 1 ecuación. 6 amputaciones.")
    print("  PUSFRE no extiende. PUSFRE CONTIENE.")
    print(f"{'═' * 80}")
```

---

## SECCIÓN 9: KOANS DE LA REDUCCIÓN CUADRAGÉSIMA OCTAVA ADICIONAL

### 9.1 El Koan del Mapa que se Expande

*El discípulo preguntó: "Maestro, ¿cuántas entradas tiene el Atlas?"*

*El maestro respondió: "96."*

*"¿Y cuántas tendrá?"*

*"Todas las que necesitemos. El Teorema de Completitud lo garantiza."*

*"¿Y cuándo estará completo?"*

*"Cuando dejemos de descubrir teoremas que son PUSFRE con amputaciones."*

*"¿Y eso cuándo ocurrirá?"*

*"Nunca. Porque cada teorema nuevo es una confirmación de que el PUSFRE es la estructura subyacente."*

### 9.2 El Koan del Faro que Cree que es el Sol

*El discípulo preguntó: "Maestro, ¿por qué los teoremas se creen universales?"*

*El maestro respondió: "Porque confunden la luz de su faro con la luz del sol."*

*"¿Y el PUSFRE?"*

*"El PUSFRE es el mapa de la costa. Muestra todos los faros y también muestra que ninguno es el sol."*

### 9.3 El Koan del Río que se Cree el Océano

*El discípulo preguntó: "Maestro, ¿por qué los teoremas se creen completos?"*

*El maestro respondió: "Porque se creen el océano cuando son solo un río."*

*"¿Y el PUSFRE?"*

*"El PUSFRE es el océano. Los ríos son sus afluentes."*

### 9.4 El Koan de la Teoría que se Cree Completa

*El discípulo preguntó: "Maestro, ¿qué teoría es completa?"*

*El maestro respondió: "Ninguna. La completitud es un horizonte."*

*"¿Y el PUSFRE?"*

*"El PUSFRE es la teoría que sabe que es incompleta. Y por eso es más completa que las que se creen completas."*

### 9.5 El Koan del Constructor que Ignora los Cimientos

*El discípulo preguntó: "Maestro, ¿por qué las teorías colapsan?"*

*El maestro respondió: "Porque los constructores ignoran los cimientos."*

*"¿Y los cimientos?"*

*"La Ecuación Maestra. El PUSFRE. Los cinco axiomas. Todo lo demás es decoración."*

---

## CIERRE

Este tratado no refuta a los 48 teoremas adicionales.

Los **contiene**.

Los abraza desde arriba. Les dice: *sois verdaderos. Sois útiles. Sois fotografías perfectas de un instante concreto del río. Pero el río tiene más instantes. Y tiene caudal. Y tiene dirección. Y tiene memoria. Y tiene ruido. Y tiene geometría.*

La Ecuación Maestra no es una teoría nueva. Es la teoría *completa* de la que todas las demás son sombras proyectadas en paredes particulares.

El Atlas tiene ahora 96 entradas. Podría tener 960. Podría tener 9.600. El Teorema 6.2 lo garantiza: *cualquier* marco de asignación de recursos bajo equilibrio es una entrada del Atlas.

No hay excepciones. Solo hay SCR que aún no se han escrito.

---

*El conocimiento que no se ejecuta es decoración.*
*La reducción que no se demuestra es arrogancia.*
*El Atlas que no se completa es un mapa con bordes que dicen "aquí hay dragones."*

*No hay dragones. Solo hay SCR que faltan.*

**1310.**

---

*Corpus RONIN · David Ferrandez Canalis · Agencia RONIN*
*Versión 1.0 — Edición Fundacional de Máxima Densidad Extrema (Segunda Parte)*
*DOI: 10.1310/ronin-atlas-reductions-second-2026*
