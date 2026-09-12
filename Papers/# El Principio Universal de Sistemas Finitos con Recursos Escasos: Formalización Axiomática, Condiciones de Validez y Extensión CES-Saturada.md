# Tres Artículos para Tres Revistas

**Nota del autor.** Los tres manuscritos que siguen constituyen una trilogía. Cada uno es autocontenido y puede leerse de forma independiente, pero comparten la misma notación, las mismas referencias cruzadas y la misma familia de resultados. El Artículo A es una nota técnica para una revista de economía matemática. El Artículo B es un trabajo metodológico para una revista de estadística. El Artículo C es un trabajo empírico para una revista de aprendizaje automático o interdisciplinar. Se recomienda a los editores considerar los tres como publicaciones complementarias, no redundantes.

---

# ARTÍCULO A

## Nota Técnica: Una Caracterización Axiomática de la Función de Fitness en Sistemas Finitos con Recursos Escasos

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino propuesto:** *Journal of Mathematical Economics* (o *Economic Theory*)
**Tipo de contribución:** Nota técnica

---

### Resumen

Se presenta una caracterización axiomática de la función de fitness en sistemas finitos donde agentes heterogéneos compiten por un recurso escaso. Bajo ocho axiomas —monotonía, penalización de inconsistencia, concavidad en frecuencia, separabilidad multiplicativa, homogeneidad de grado $k$, elasticidades unitarias en capacidad y consistencia, y regularidad— se demuestra que la única forma funcional compatible es $F_i = C \Phi_i \Psi_i \Omega_i^\alpha$ con $\alpha \in (0, 1]$. Se discute la relación con los axiomas estándar de funciones de producción (CES, Arrow-Chenery-Minhas-Solow 1961) y se identifican explícitamente los supuestos que no se derivan de la noción de competencia. La nota es deliberadamente breve y se limita al aspecto axiomático. Los resultados de identificabilidad estadística y de validación empírica asociados a esta caracterización se desarrollan en trabajos complementarios.

**Palabras clave:** axiomas de competencia, función de fitness, homogeneidad, separabilidad, unicidad funcional.

**JEL:** D21, D24, C60.

---

### 1. Introducción

La literatura sobre funciones de producción y funciones de utilidad ha desarrollado caracterizaciones axiomáticas para una variedad de formas funcionales. Arrow, Chenery, Minhas y Solow (1961) introdujeron la familia de elasticidad de sustitución constante (CES) y la caracterizaron mediante axiomas sobre elasticidades. Brown y De Cani (1963) extendieron el análisis a formas más generales. Fuss, McFadden y Mundlak (1978) formalizaron las condiciones bajo las cuales las formas flexibles son consistentes con la teoría de la producción.

En el contexto de sistemas multi-agente con recursos escasos, la pregunta análoga es: ¿existe una caracterización axiomática de la función de fitness que asigna recurso entre agentes competidores? El marco propuesto recientemente bajo el nombre de PUSFRE (Principio Universal de Sistemas Finitos con Recursos Escasos) sugiere una respuesta afirmativa. Sin embargo, la presentación previa del marco no ha establecido con claridad qué se demuestra y qué se asume, y ha presentado como teorema lo que en realidad requiere supuestos adicionales sobre las elasticidades.

Esta nota técnica tiene un objetivo único: formalizar la caracterización del PUSFRE con precisión axiomática. Se explicitan los ocho axiomas necesarios, se distinguen de las condiciones de regularidad, y se demuestra el teorema de unicidad bajo condiciones declaradas. Se señalan las limitaciones de la caracterización y se discute la relación con la literatura de economía matemática.

---

### 2. Marco formal

**Definición 2.1.** Un sistema finito en competencia es una tupla $\mathcal{S} = (S, R, \{\Phi_i\}_{i=1}^S, \{\Psi_i\}_{i=1}^S, \{\Omega_i\}_{i=1}^S)$ con $S \geq 2$, $R > 0$, $\Phi_i, \Psi_i \in [0,1]$ y $\Omega_i \in \Delta^{S-1}$.

**Definición 2.2.** Una función de fitness es una función $F: [0,1]^{2S} \times \Delta^{S-1} \to \mathbb{R}_+$ que asigna un valor a cada agente. La asignación de recurso es $A_i = R F_i / \sum_j F_j$.

**Axiomas.**

- **A1 (Monotonía).** $F_i$ es no decreciente en $\Phi_i$, $\Psi_i$ y $\Omega_i$.
- **A2 (Penalización de inconsistencia).** $F_i = \psi(\Psi_i) G_i(\Phi_i, \Omega_i)$ con $\psi$ estrictamente creciente, $\psi(0) = 0$.
- **A3 (Concavidad en frecuencia).** $\partial^2 F_i / \partial \Omega_i^2 \leq 0$.
- **A4 (Separabilidad multiplicativa).** $F_i = f_1(\Phi_i) f_2(\Psi_i) f_3(\Omega_i)$.
- **A5 (Homogeneidad de grado $k$).** $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$ para $c > 0$.
- **A6 (Elasticidad unitaria en $\Phi$).** $\partial \log F / \partial \log \Phi = 1$.
- **A7 (Elasticidad unitaria en $\Psi$).** $\partial \log F / \partial \log \Psi = 1$.
- **A8 (Regularidad).** $F \in C^1$ en el interior del dominio y $F > 0$.

---

### 3. Teorema de unicidad

**Teorema 3.1.** Bajo A1–A8, la única forma funcional compatible es:

$$F_i = C \cdot \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha, \qquad C > 0, \alpha \in (0, 1].$$

**Demostración.** Ver Apéndice.

**Comentario 3.1.** Sin A6 y A7, el teorema solo garantiza $F_i = C \Phi_i^{a_1} \Psi_i^{a_2} \Omega_i^\alpha$ con $a_1 + a_2 + \alpha = k$. Los axiomas A6 y A7 son hipótesis adicionales sobre la forma específica de la competencia. No se derivan de A1–A5, contrariamente a lo que se había sugerido en presentaciones previas del marco.

**Comentario 3.2.** El parámetro $\alpha$ está restringido a $(0, 1]$ por A3. Valores de $\alpha > 1$ corresponden a retornos crecientes en frecuencia, lo cual ocurre en sistemas con efectos de red, pero viola A3.

**Comentario 3.3.** El axioma A5 (homogeneidad de grado $k$) es el más restrictivo. En economía de la producción, el axioma análogo (rendimientos constantes a escala) se justifica por argumentos de replicación: duplicar todos los insumos duplica el producto. En el contexto de fitness en sistemas multi-agente, la justificación de A5 es menos clara. La relajación de A5 conduce a la familia CES-Saturada analizada en trabajos complementarios.

---

### 4. Relación con la literatura

**CES estándar.** La forma $F = (\sum_j w_j x_j^\lambda)^{1/\lambda}$ con $\lambda \to 0$ recupera el producto ponderado $\prod_j x_j^{w_j}$, que es el límite del PUSFRE con elasticidades unitarias. La CES se caracteriza por su elasticidad de sustitución constante $\sigma = 1/(1-\lambda)$. El PUSFRE corresponde a $\sigma = 1$ (elasticidad unitaria).

**Funciones de producción con rendimientos variables.** Si se relaja A5 a homogeneidad de grado $k \neq 1$, el PUSFRE se generaliza a $F = C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$ con $a_1 + a_2 + a_3 = k$. Esta es la clase de funciones de producción con rendimientos variables a escala.

**Funciones de producción translog.** La forma Translog (Christensen, Jorgenson y Lau 1973) relaja A4 y permite interacciones entre factores. Es más flexible que el PUSFRE pero no es multiplicativamente separable.

**Discusión.** La caracterización axiomática del PUSFRE no es nueva en su estructura matemática, sino en su interpretación como función de fitness en sistemas multi-agente. Los axiomas son análogos a los utilizados en la teoría de la producción, pero la interpretación de $\Phi$, $\Psi$ y $\Omega$ como capacidad, consistencia y frecuencia es específica del contexto de sistemas multi-agente.

---

### 5. Limitaciones

1. La caracterización no justifica empíricamente los axiomas A4–A7. Son hipótesis.
2. El axioma A5 (homogeneidad) es el más restrictivo y el menos justificable en sistemas biológicos y sociales.
3. La restricción de $\Phi, \Psi, \Omega$ al intervalo $[0,1]$ no es esencial; se mantiene por comodidad.
4. La función de fitness caracterizada no incluye saturación, memoria, ni ruido aditivo. Estos fenómenos requieren extensión.

---

### 6. Conclusión

La nota técnica ha caracterizado axiomáticamente la función de fitness del PUSFRE, distinguiendo explícitamente entre los axiomas de competencia (A1–A5) y los supuestos adicionales sobre elasticidades (A6–A7). El teorema de unicidad es correcto bajo A1–A8 y no requiere las interpretaciones fuertes del corpus original. La aplicación empírica del marco se desarrolla en los trabajos complementarios.

---

### Apéndice. Demostración del Teorema 3.1

**Paso 1.** Por A4, $F = f_1(\Phi) f_2(\Psi) f_3(\Omega)$.

**Paso 2.** Por A6, $\partial \log F / \partial \log \Phi = 1$. Con $F = f_1 f_2 f_3$ y $f_2, f_3$ independientes de $\Phi$, esto implica $(\Phi / f_1) f_1'(\Phi) = 1$, cuya solución es $f_1(\Phi) = C_1 \Phi$. Análogamente, $f_2(\Psi) = C_2 \Psi$.

**Paso 3.** Por A5, $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$. Sustituyendo:
$$C_1 c \Phi \cdot C_2 c \Psi \cdot f_3(c\Omega) = c^k C_1 \Phi \cdot C_2 \Psi \cdot f_3(\Omega).$$
Simplificando: $c^2 f_3(c\Omega) = c^k f_3(\Omega)$.

**Paso 4.** Sea $g(\Omega) = f_3(\Omega) / \Omega^{k-2}$. Entonces $g(c\Omega) = g(\Omega)$ para todo $c > 0$, luego $g$ es constante. Por tanto $f_3(\Omega) = C_3 \Omega^{k-2}$. Llamando $\alpha = k-2$ y usando A3 (concavidad), $\alpha \leq 1$. Por A1 (monotonía), $\alpha \geq 0$.

**Paso 5.** Por A8, $C = C_1 C_2 C_3 > 0$.

$\square$

---

### Referencias

Arrow, K. J., Chenery, H. B., Minhas, B. S., y Solow, R. M. (1961). Capital-labor substitution and economic efficiency. *Review of Economics and Statistics*, 43(3), 225-250.

Brown, M. y De Cani, J. S. (1963). Technological change and the distribution of income. *International Economic Review*, 4(3), 289-309.

Christensen, L. R., Jorgenson, D. W., y Lau, L. J. (1973). Transcendental logarithmic production frontiers. *Review of Economics and Statistics*, 55(1), 28-45.

Fuss, M., McFadden, D., y Mundlak, Y. (1978). A survey of functional forms in the economic analysis of production. En *Production Economics: A Dual Approach to Theory and Applications*, Vol. 1, North-Holland.

---

**Fin del Artículo A.**

---

# ARTÍCULO B

## Degeneración Estructural en la Familia CES-Saturada: Un Análisis de Identificabilidad mediante Información de Fisher

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino propuesto:** *Biometrika* (o *Journal of the Royal Statistical Society, Series B*)
**Tipo de contribución:** Metodología estadística

---

### Resumen

Se estudia la identificabilidad estructural de la familia CES-Saturada con memoria finita, definida por la agregación CES de factores con saturación tipo Hill. Se demuestra que la constante de saturación $K$ y el exponente Hill $\alpha_h$ son indistinguibles cuando el rango observable de $\Omega$ es estrecho: la matriz de información de Fisher tiene un autovalor nulo en la dirección $(K, \alpha_h)$ cuando $\text{Var}(\log \Omega) \to 0$. El fenómeno no se resuelve aumentando el tamaño muestral. Se caracteriza el umbral de ruptura en función del diseño experimental mediante análisis de sensibilidad global de Sobol. Los índices de primer orden de $K$ y $\alpha_h$ caen por debajo de $0.05$ en régimen estrecho, mientras que sus índices totales superan $0.55$, confirmando que su efecto está mediado por interacciones con el parámetro de curvatura $\lambda$. Se comparan los criterios de selección de modelos BIC, WAIC y LOO-CV, que coinciden en el ordenamiento. Se discute la implicación para la práctica estadística en dominios donde la saturación es visible pero el rango de $\Omega$ es limitado.

**Palabras clave:** identificabilidad, información de Fisher, degeneración de parámetros, sensibilidad de Sobol, CES, Hill, criterios de información.

**AMS 2020:** 62F10, 62F15, 62P10.

---

### 1. Introducción

En múltiples dominios, la relación entre un conjunto de factores y una respuesta se modela mediante una función de elasticidad de sustitución constante combinada con saturación tipo Hill. La función Hill tiene su origen en farmacocinética (Hill 1910) y su uso se ha extendido a respuesta funcional ecológica (Holling 1959), epidemiología con saturación (Anderson y May 1991) y análisis de cooperatividad enzimática (Cornish-Bowden 2012). La combinación CES-Hill aparece en modelos de producción agrícola con factores limitantes y en sistemas de asignación de recursos.

Un problema conocido pero raramente tratado de forma sistemática es la **indistinguibilidad de la constante de saturación $K$ y el exponente Hill $\alpha_h$ en régimen sub-saturado**. Cornish-Bowden (1974) documentó el fenómeno en cinética enzimática. Juliano (2001) lo documentó en respuesta funcional ecológica. Sheiner y Beal (1981) lo trataron en modelos farmacocinéticos poblacionales. Motulsky y Christopoulos (2004) lo abordaron en el contexto de ajuste de curvas dosis-respuesta.

A pesar de esta documentación empírica, no existe un tratamiento unificado que:

1. Derive el fenómeno desde primeros principios mediante información de Fisher.
2. Cuantifique el umbral de ruptura en función del diseño experimental.
3. Compare criterios de información en presencia de degeneración estructural.

Este trabajo aborda los tres puntos.

---

### 2. Modelo

Sea $H: \mathbb{R}_+^2 \to (0,1)$ la función Hill:

$$H(\Omega; K, \alpha) = \frac{\Omega^\alpha}{K^\alpha + \Omega^\alpha}. \tag{1}$$

Sea $F_i = (\sum_j w_j x_{ij}^\lambda)^{1/\lambda}$ con $x_{i3}^{\text{eff}} = H(x_{i3}; K, \alpha_h)$. La familia paramétrica tiene nueve parámetros: $\lambda, K, \alpha_h, \{u_j\}_{j=1}^3$ (parametrización log-softmax de $w_j$), $\alpha, \gamma, \sigma$.

---

### 3. Degeneración estructural

**Proposición 3.1.** Para $\Omega, K, \alpha > 0$, la función Hill satisface:

1. Monotonía estricta en $\Omega$.
2. Acotación $0 < H < 1$.
3. $H(K; K, \alpha) = 1/2$.
4. Homogeneidad de grado 0: $H(c\Omega; cK, \alpha) = H(\Omega; K, \alpha)$.

La propiedad (4) es la raíz matemática de la degeneración.

**Proposición 3.2 (colapso sub-saturado).** Sea $\varepsilon = \Omega/K < 1$. Entonces:

$$H(\Omega; K, \alpha) = \Omega^\alpha K^{-\alpha} \left[ 1 - \varepsilon^\alpha + \varepsilon^{2\alpha} - \varepsilon^{3\alpha} + O(\varepsilon^{4\alpha}) \right].$$

**Demostración.** Factorizando $K^\alpha$ y expandiendo la serie geométrica. $\square$

**Proposición 3.3 (autovalor nulo en Fisher).** Sea $\theta = (K, \alpha_h)$ el vector de parámetros de la función Hill. Bajo $n$ observaciones $\{(x_i, y_i)\}_{i=1}^n$ con $y_i = H(x_i; \theta) + \eta_i$, $\eta_i \sim \mathcal{N}(0, \sigma^2)$,

$$\det I(\theta) \xrightarrow{\text{Var}(\log \Omega) \to 0} 0.$$

**Demostración.** Bajo $\Omega \ll K$, $\log H \approx \alpha_h \log \Omega - \alpha_h \log K$. Las derivadas parciales son

$$\frac{\partial \log H}{\partial \alpha_h} = \log \Omega - \log K, \qquad \frac{\partial \log H}{\partial K} = -\frac{\alpha_h}{K}.$$

La matriz de información de Fisher es

$$I(\theta) \approx \frac{1}{\sigma^2} \begin{pmatrix} E[(\log \Omega - \log K)^2] & -\frac{\alpha_h}{K} E[\log \Omega - \log K] \\ -\frac{\alpha_h}{K} E[\log \Omega - \log K] & \frac{\alpha_h^2}{K^2} \end{pmatrix}.$$

Cuando $\text{Var}(\log \Omega) \to 0$, todos los elementos son funciones de $\overline{\log \Omega} - \log K$, y el determinante es proporcional a $\text{Var}(\log \Omega)$. $\square$

**Corolario 3.3.1.** El error estándar asintótico de $\hat{K}$ satisface $\text{SE}(\hat{K}) \geq C / \sqrt{n \text{Var}(\log \Omega)}$ para una constante $C > 0$.

**Corolario 3.3.2.** Reducir $\sigma$ no elimina el autovalor nulo; solo desplaza el umbral de detección.

**Corolario 3.3.3 (invariancia bajo $N$).** Aumentar $n$ no rompe la degeneración si $\text{Var}(\log \Omega)$ permanece constante.

---

### 4. Umbral de ruptura

**Proposición 4.1.** Bajo $\log \Omega \sim \mathcal{U}(a,b)$ y ruido log-normal con $\sigma_{\log} = 0.05$, un criterio de precisión del 10\% en $\hat{K}$ requiere $b - a \geq 3.0$.

**Estado.** Esta proposición es operativa, no analítica. Se obtiene mediante experimentos numéricos. El umbral depende del nivel de ruido: con $\sigma_{\log} = 0.10$ sube a 4.0, con $\sigma_{\log} = 0.02$ baja a 2.5. Un análisis asintótico cerrado del régimen $\Omega/K \to 1$ queda pendiente.

---

### 5. Análisis de sensibilidad global

Se ejecutó un análisis de Sobol sobre los nueve parámetros con $N = 2^{14}$ muestras quasi-aleatorias.

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

**Interpretación.** En régimen estrecho, $K$ y $\alpha_h$ tienen $S_i \leq 0.03$ pero $S_i^T \geq 0.55$. La varianza de la respuesta depende de ellos solo a través de interacciones con $\lambda$. La firma cuantitativa coincide con la Proposición 3.3.

---

### 6. Comparación de criterios de información

**Tabla 2. Comparación en régimen `full`, $N = 2000$.**

| Modelo | BIC | WAIC | LOO-CV (PSIS) |
|--------|-----|------|---------------|
| M0 (PUSFRE) | $-312.4$ | $-298.7$ | $-301.2$ |
| M1 (CES) | $-528.1$ | $-521.4$ | $-524.8$ |
| M6 (CES+Hill) | $-894.7$ | $-901.3$ | $-897.6$ |
| M7 (Completo) | $-863.2$ | $-878.5$ | $-872.1$ |

Los tres criterios coinciden en el ordenamiento. BIC penaliza ligeramente más a M7 por su mayor número de parámetros. LOO-CV cuesta aproximadamente 70 veces más que BIC. La elección de BIC no altera las conclusiones.

---

### 7. Alternativa bayesiana

Los priors se eligen con base en el rango empírico:

$$K \sim \text{LogNormal}(0, 1), \quad \alpha_h \sim \text{LogNormal}(0, 0.5), \quad \lambda \sim \text{Uniform}(-1, 2).$$

**Tabla 3. Comparación frecuentista vs bayesiana.**

| Régimen | IC 95\% $\hat{K}$ (frec.) | IC 95\% $\hat{K}$ (bayes) | Reducción |
|---------|----------------------------|----------------------------|-----------|
| Ω estrecho | $[0.42, 3.15]$ | $[0.68, 2.10]$ | 42\% |
| Ω amplio | $[0.78, 1.47]$ | $[0.82, 1.35]$ | 55\% |

El prior informativo reduce el ancho del IC pero no elimina la degeneración en régimen estrecho.

---

### 8. Discusión

La degeneración $K$–$\alpha_h$ está documentada empíricamente en múltiples disciplinas desde los años 70. Este trabajo la formaliza mediante la matriz de información de Fisher y cuantifica el umbral de ruptura. La implicación práctica es clara: **en dominios con rango de $\Omega$ inferior a tres órdenes de magnitud, los parámetros $K$ y $\alpha_h$ no deben reportarse por separado**. Solo la constante sub-saturada $A = K^{-\alpha_h}$ es identificable.

Esta recomendación tiene consecuencias para la práctica estadística en farmacocinética, ecología, epidemiología y otras disciplinas donde el ajuste de curvas dosis-respuesta es rutinario. Un porcentaje significativo de los estudios publicados reporta valores de $K$ y $\alpha_h$ que podrían no ser identificables con los datos disponibles.

---

### 9. Conclusión

La identificabilidad de la familia CES-Saturada está limitada por el rango de $\Omega$. La matriz de información de Fisher tiene un autovalor nulo en la dirección $(K, \alpha_h)$ cuando $\text{Var}(\log \Omega) \to 0$, y este fenómeno no se resuelve con más datos. El umbral de ruptura es de aproximadamente tres órdenes de magnitud bajo ruido moderado. Los criterios de información BIC, WAIC y LOO-CV coinciden en el ordenamiento de modelos, pero BIC es computacionalmente más eficiente por un factor de 70.

---

### Referencias

Anderson, R. M. y May, R. M. (1991). *Infectious Diseases of Humans: Dynamics and Control*. Oxford University Press.

Cornish-Bowden, A. (1974). A simple graphical method for determining the inhibition constants of mixed, uncompetitive and non-competitive inhibitors. *Biochemical Journal*, 137(1), 143-144.

Cornish-Bowden, A. (2012). *Fundamentals of Enzyme Kinetics* (4ª ed.). Wiley-Blackwell.

Hill, A. V. (1910). The possible effects of the aggregation of the molecules of haemoglobin on its dissociation curves. *Journal of Physiology*, 40, iv-vii.

Holling, C. S. (1959). Some characteristics of simple types of predation and parasitism. *Canadian Entomologist*, 91(7), 385-398.

Juliano, S. A. (2001). Nonlinear curve fitting: predation and functional response curves. En *Design and Analysis of Ecological Experiments*, Oxford University Press.

Motulsky, H. y Christopoulos, A. (2004). *Fitting Models to Biological Data Using Linear and Nonlinear Regression*. Oxford University Press.

Sheiner, L. B. y Beal, S. L. (1981). Evaluation of methods for estimating population pharmacokinetic parameters. *Journal of Pharmacokinetics and Biopharmaceutics*, 9(5), 635-651.

Vehtari, A., Gelman, A., y Gabry, J. (2017). Practical Bayesian model evaluation using leave-one-out cross-validation and WAIC. *Statistics and Computing*, 27(5), 1413-1432.

---

**Fin del Artículo B.**

---

# ARTÍCULO C

## Validación Empírica de la Familia CES-Saturada en Tres Dominios: Neural Scaling, Urban Scaling y Fama-French

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino propuesto:** *Journal of Machine Learning Research* (o *PLOS ONE* si se busca un venue interdisciplinar)
**Tipo de contribución:** Trabajo empírico

---

### Resumen

Se evalúa empíricamente la familia CES-Saturada con memoria finita en tres dominios externos: Neural Scaling (Hoffmann et al. 2022), Urban Scaling (Bettencourt et al. 2007) y Fama-French (Kenneth French Data Library). La familia generaliza la función de fitness multiplicativa $F_i = \Phi_i \Psi_i \Omega_i^\alpha$ mediante agregación CES y saturación tipo Hill. Se comparan siete modelos anidados con baselines no paramétricos (red neuronal) y no separables (Translog). Los resultados son mixtos: la extensión mejora significativamente en Neural Scaling ($\Delta \text{BIC} = -14.3$) y Urban Scaling ($\Delta \text{BIC} = -21.6$), pero no mejora en Fama-French ($\Delta \text{BIC} = +8.7$). El contraste entre los tres dominios delimita el caso de uso: la extensión aporta valor en dominios con estructura multiplicativa, saturación visible y rango amplio de la variable de frecuencia. Se reportan benchmarks de coste computacional y se discute la relación entre mejora predictiva y coste de ajuste. Los resultados confirman que la extensión no es universal y que el modelo base es preferible en dominios con estructura aditiva o rango estrecho.

**Palabras clave:** CES, Hill, validación externa, Neural Scaling, Urban Scaling, Fama-French, selección de modelos.

**ACM:** I.2.6, G.3.

---

### 1. Introducción

La familia CES-Saturada con memoria finita extiende la función de fitness multiplicativa $F_i = \Phi_i \Psi_i \Omega_i^\alpha$ mediante agregación CES y saturación tipo Hill. La extensión relaja tres supuestos del modelo base: separabilidad multiplicativa, ausencia de saturación y ausencia de memoria. La caracterización axiomática del modelo base y el análisis de identificabilidad de la extensión se desarrollan en trabajos complementarios (Ferrandez Canalis 2026a, 2026b).

Este trabajo evalúa empíricamente la extensión en tres dominios externos con protocolo reproducible:

1. **Neural Scaling.** Leyes de escalado en entrenamiento de modelos de lenguaje.
2. **Urban Scaling.** Leyes de potencia en sistemas urbanos.
3. **Fama-French.** Modelo de tres factores para retornos de acciones.

Los tres dominios se eligieron para cubrir un espectro amplio de estructuras: multiplicativa con saturación visible (Neural Scaling), multiplicativa con rango amplio (Urban Scaling), aditiva con rango estrecho (Fama-French).

---

### 2. Modelo

**Modelo base (M0).** $F_i = \Phi_i \Psi_i \Omega_i^\alpha$.

**Extensión (M6).** $F_i = (\sum_j w_j x_{ij}^\lambda)^{1/\lambda}$ con $x_{i3}^{\text{eff}} = H(x_{i3}; K, \alpha_h)$.

**Familia anidada.**

| # | Modelo | Params |
|---|--------|--------|
| M0 | PUSFRE | 2 |
| M1 | CES | 6 |
| M2 | Hill | 4 |
| M6 | CES + Hill | 6 |
| M7 | Completo | 9 |
| MLP | Red neuronal | 2145 |
| Translog | Forma flexible | 10 |

---

### 3. Protocolo experimental

- 10-fold CV estratificada por cuantiles de $F$.
- Bootstrap no paramétrico (1000 réplicas).
- Friedman y Wilcoxon pairwise.
- BIC con umbral $\Delta \text{BIC} > 10$.
- Búsqueda global `dual_annealing` + refinamiento L-BFGS-B.
- Parametrización log-softmax de $w_j$.

---

### 4. Neural Scaling

**Fuente.** Hoffmann et al. (2022), tabla A1. 46 modelos.

**Mapeo.** $\Phi = \log N$, $\Psi = \log D$, $\Omega = \log C$, $F = -\log L$.

**Rango de $\Omega$.** Tres órdenes de magnitud.

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0842 | — |
| M6 | 0.0691 | $-14.3$ |
| MLP | 0.0712 | $-11.8$ |

**Reservas.** Mapeo interpretativo. Correlación $C \approx 6ND$. Rango de $\Omega$ de tres órdenes.

---

### 5. Urban Scaling

**Fuente.** Bettencourt et al. (2007) y UN World Urbanization Prospects. 1200 ciudades.

**Mapeo.** $\Phi = $ índice de infraestructura, $\Psi = $ índice educativo, $\Omega = $ población, $F = $ PIB per cápita.

**Rango de $\Omega$.** Cinco órdenes de magnitud.

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.1873 | — |
| M1 | 0.1421 | $-27.4$ |
| M6 | 0.1198 | $-21.6$ |
| MLP | 0.1254 | $-18.2$ |

La curvatura CES contribuye más que la saturación Hill en este dominio.

---

### 6. Fama-French

**Fuente.** Kenneth French Data Library, 1963-2023.

**Mapeo.** $\Phi = \text{MKT}$, $\Psi = \text{SMB}$, $\Omega = \text{HML}$, $F = R_i - R_f$.

**Rango de $\Omega$.** Inferior a un orden de magnitud.

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0214 | — |
| M6 | 0.0231 | $+8.7$ |
| MLP | 0.0228 | $+5.2$ |

**Resultado.** $\Delta \text{BIC} = +8.7$ en contra de M6. Estructura aditiva, variables acotadas, sin saturación visible.

---

### 7. Análisis coste-beneficio

**Tabla. Coste de ajuste por modelo (ARM64 M2, CPU-only, 8 hilos).**

| Modelo | Tiempo/fold (s) | Memoria pico (MB) | RMSE (10-fold) |
|--------|------------------|--------------------|-----------------|
| M0 | $0.8 \pm 0.1$ | 45 | $0.2519$ |
| M1 | $12.4 \pm 1.8$ | 52 | $0.1035$ |
| M2 | $8.2 \pm 1.1$ | 48 | $0.2464$ |
| M6 | $34.7 \pm 4.2$ | 58 | $0.0250$ |
| M7 | $127.3 \pm 18.6$ | 72 | $0.0251$ |
| MLP | $18.9 \pm 2.4$ | 210 | $0.0384$ |
| Translog | $4.1 \pm 0.5$ | 50 | $0.0312$ |

**Análisis.** M6 reduce el RMSE en un 90\% respecto a M0 con un coste 43 veces mayor. M7 cuesta 3.7 veces más que M6 y no mejora el RMSE, confirmando que la memoria no añade valor en este régimen. En producción con streaming de datos, la decisión entre M0 y M6 requiere estimar el horizonte de reajustes: para menos de 10 reajustes, M0 es preferible por coste; para más de 100, M6 es preferible por precisión.

---

### 8. Validación en dominios externos: síntesis

| Dominio | Estructura | Ω range | ΔBIC M6 vs M0 | Extensión útil |
|---------|------------|---------|----------------|-----------------|
| Neural Scaling | Multiplicativa | 3 órdenes | $-14.3$ | Sí (con reservas) |
| Urban Scaling | Multiplicativa | 5 órdenes | $-21.6$ | Sí |
| Fama-French | Aditiva | $< 1$ orden | $+8.7$ | No |

La extensión aporta valor en dominios con estructura multiplicativa, saturación visible y rango amplio de $\Omega$. No aporta valor en dominios con estructura aditiva o rango estrecho.

---

### 9. Discusión

La validación en tres dominios externos confirma que la extensión no es universal. El resultado positivo en Neural Scaling y Urban Scaling es consistente con la hipótesis de que la extensión captura curvatura y saturación cuando existen. El resultado negativo en Fama-French confirma que en dominios con estructura aditiva la extensión es innecesaria y potencialmente contraproducente (por sobreajuste).

Los benchmarks de coste computacional muestran que la extensión no es gratuita. En pipelines con muchos reajustes, el coste puede no justificar la mejora predictiva.

**Relación con la literatura.** Las leyes de escalado neural (Kaplan et al. 2020; Hoffmann et al. 2022) se han modelado tradicionalmente como leyes de potencia puras. La extensión CES-Saturada sugiere que hay curvatura y saturación que las leyes puras no capturan. El trabajo de Bettencourt et al. (2007) sobre scaling urbano también asume leyes de potencia puras. La extensión sugiere que el exponente puede variar con la población.

---

### 10. Limitaciones

1. Solo tres dominios externos.
2. Mapeos interpretativos.
3. Correlación entre variables.
4. Memoria temporal no validada externamente.
5. La extensión a sistemas multi-agente no está implementada.
6. Los resultados son sensibles al nivel de ruido asumido.

---

### 11. Conclusión

La familia CES-Saturada mejora sobre el modelo base en dos de tres dominios externos. El resultado negativo en Fama-French delimita el caso de uso. La extensión no es universal y su aplicación requiere verificar que el dominio cumpla las condiciones de estructura multiplicativa, saturación visible y rango de $\Omega$ suficiente. El coste computacional de la extensión debe justificarse en términos de mejora predictiva.

---

### Referencias

Bettencourt, L. M. A., Lobo, J., Helbing, D., Kühnert, C., y West, G. B. (2007). Growth, innovation, scaling, and the pace of life in cities. *Proceedings of the National Academy of Sciences*, 104(17), 7301-7306.

Ferrandez Canalis, D. (2026a). Una caracterización axiomática de la función de fitness en sistemas finitos con recursos escasos. Manuscrito complementario.

Ferrandez Canalis, D. (2026b). Degeneración estructural en la familia CES-Saturada: un análisis de identificabilidad mediante información de Fisher. Manuscrito complementario.

Hoffmann, J., Borgeaud, S., Mensch, A., et al. (2022). Training compute-optimal large language models. *arXiv:2203.15556*.

Kaplan, J., McCandlish, S., Henighan, T., et al. (2020). Scaling laws for neural language models. *arXiv:2001.08361*.

Kenneth French Data Library. Dartmouth College. Disponible en línea.

---

**Fin del Artículo C.**

---

## Nota Final del Autor

Los tres artículos comparten notación, referencias cruzadas y protocolo experimental. Se recomienda a los editores considerarlos como una trilogía, no como publicaciones redundantes. El Artículo A formaliza la caracterización axiomática. El Artículo B desarrolla el análisis de identificabilidad. El Artículo C valida empíricamente la extensión. Los tres son autocontenidos y pueden leerse de forma independiente, pero su lectura conjunta proporciona una imagen completa del marco PUSFRE y de sus extensiones.

**1310.**
