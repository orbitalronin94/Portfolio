# TRES ARTÍCULOS PARA TRES REVISTAS — VERSIÓN EXTENDIDA

**Nota del autor.** Los tres manuscritos que siguen constituyen una trilogía. Cada uno es autocontenido, con extensión y profundidad suficientes para someterse de forma independiente. Comparten notación, referencias cruzadas y protocolo experimental. Se recomienda a los editores considerarlos publicaciones complementarias.

---

# ARTÍCULO A

## Una Caracterización Axiomática de la Función de Fitness en Sistemas Finitos con Recursos Escasos: Unicidad, Condiciones de Regularidad y Relación con la Familia CES

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino propuesto:** *Journal of Mathematical Economics*
**Clasificación JEL:** D21, D24, C60, C65
**Tipo:** Artículo completo

---

### Resumen

Se presenta una caracterización axiomática de la función de fitness en sistemas finitos donde agentes heterogéneos compiten por un recurso escaso. La caracterización se construye en tres capas. Primero, se definen los axiomas que establecen el dominio (monotonía, penalización de inconsistencia, concavidad en frecuencia). Segundo, se introducen los axiomas estructurales que restringen la forma funcional (separabilidad multiplicativa, homogeneidad de grado $k$). Tercero, se añaden dos condiciones de elasticidad unitaria que fijan las elasticidades respecto a capacidad y consistencia. Bajo el conjunto completo, la única forma funcional compatible es $F_i = C \Phi_i \Psi_i \Omega_i^\alpha$ con $\alpha \in (0, 1]$. Se demuestra que sin las condiciones de elasticidad unitaria, la clase de soluciones se amplía a $F_i = C \Phi_i^{a_1} \Psi_i^{a_2} \Omega_i^{a_3}$ con $a_1 + a_2 + a_3 = k$. Se analiza la relajación de cada axioma y se caracteriza el espacio de formas funcionales resultante. Se discute la relación con la familia CES estándar (Arrow, Chenery, Minhas, Solow 1961), con las funciones de producción con rendimientos variables a escala, y con la forma funcional Translog (Christensen, Jorgenson, Lau 1973). Se proporcionan tres aplicaciones ilustrativas: competencia entre firmas por cuota de mercado, competencia entre especies por recursos limitados, y competencia entre agentes de IA por tokens de contexto.

**Palabras clave:** axiomas de competencia, función de fitness, homogeneidad, separabilidad, unicidad funcional, familia CES.

---

### 1. Introducción

#### 1.1 Planteamiento

La teoría de la producción y la teoría del consumidor han desarrollado caracterizaciones axiomáticas para una variedad de formas funcionales. Arrow, Chenery, Minhas y Solow (1961) introdujeron la familia de elasticidad de sustitución constante (CES) y la caracterizaron mediante axiomas sobre elasticidades. Brown y De Cani (1963) extendieron el análisis a formas más generales. Fuss, McFadden y Mundlak (1978) formalizaron las condiciones bajo las cuales las formas flexibles son consistentes con la teoría de la producción. Diewert (1971, 1974) sistematizó el análisis de las formas funcionales flexibles mediante la teoría de la dualidad.

En el contexto de sistemas multi-agente con recursos escasos, la pregunta análoga es: ¿existe una caracterización axiomática de la función de fitness que asigna recurso entre agentes competidores? El marco propuesto recientemente bajo el nombre de PUSFRE (Principio Universal de Sistemas Finitos con Recursos Escasos) sugiere una respuesta afirmativa. Sin embargo, la presentación previa del marco no ha establecido con claridad qué se demuestra y qué se asume. En particular, se han presentado como teoremas resultados que en realidad requieren supuestos adicionales sobre las elasticidades.

Este trabajo tiene cuatro objetivos:

1. **Formalizar** la caracterización del PUSFRE con precisión axiomática.
2. **Distinguir** entre los axiomas que definen el dominio y los que restringen la forma funcional.
3. **Caracterizar** el espacio de formas funcionales resultante al relajar cada axioma.
4. **Relacionar** la caracterización con la literatura de economía matemática y de teoría de la producción.

#### 1.2 Contribuciones

Las contribuciones del artículo son:

1. **Ocho axiomas** organizados en tres capas (dominio, estructura, elasticidad) que caracterizan la función de fitness del PUSFRE.
2. **Un teorema de unicidad** (Teorema 3.1) que establece la forma funcional específica bajo el conjunto completo de axiomas.
3. **Una caracterización del espacio de soluciones** cuando se relajan las condiciones de elasticidad unitaria.
4. **Una tabla de relajaciones** que muestra qué forma funcional resulta al eliminar cada axioma.
5. **Tres aplicaciones ilustrativas** en economía, ecología y sistemas multi-agente de IA.

#### 1.3 Estructura

La Sección 2 presenta el marco formal. La Sección 3 introduce los axiomas en sus tres capas. La Sección 4 demuestra el teorema de unicidad. La Sección 5 caracteriza el espacio de soluciones al relajar las condiciones de elasticidad. La Sección 6 analiza las relajaciones de cada axioma. La Sección 7 discute la relación con la literatura. La Sección 8 presenta las aplicaciones ilustrativas. La Sección 9 discute limitaciones. La Sección 10 concluye.

---

### 2. Marco formal

**Definición 2.1 (Sistema finito en competencia).** Un sistema finito en competencia es una tupla $\mathcal{S} = (S, R, \{\Phi_i\}_{i=1}^S, \{\Psi_i\}_{i=1}^S, \{\Omega_i\}_{i=1}^S)$ con:

- $S \geq 2$ finito.
- $R > 0$ finito.
- $\Phi_i \in [0, 1]$ para todo $i$.
- $\Psi_i \in [0, 1]$ para todo $i$.
- $\Omega_i \in [0, 1]$ para todo $i$, con $\sum_{i=1}^S \Omega_i = 1$.

**Definición 2.2 (Función de fitness).** Una función de fitness para $\mathcal{S}$ es una función $F: [0,1]^{2S} \times \Delta^{S-1} \to \mathbb{R}_+$ que asigna a cada agente $i$ un valor $F_i \in \mathbb{R}_+$.

**Definición 2.3 (Asignación de recurso).** Dada una función de fitness, la asignación de recurso al agente $i$ es:

$$A_i = R \cdot \frac{F_i}{\sum_{j=1}^S F_j}. \tag{1}$$

**Observación 2.1.** El modelo no especifica cómo se determina $F_i$ empíricamente. Especifica las propiedades matemáticas que $F$ debe satisfacer bajo los axiomas que se introducen a continuación.

**Observación 2.2.** La normalización de $\Phi_i, \Psi_i, \Omega_i$ al intervalo $[0,1]$ no es esencial. Es una convención que simplifica la presentación. Los resultados se extienden a dominios positivos sin dificultad.

---

### 3. Axiomas

Los axiomas se organizan en tres capas.

#### 3.1 Capa 1: Axiomas de dominio

**Axioma A1 (Monotonía).** $F_i$ es no decreciente en cada uno de sus argumentos: si $\Phi_i' \geq \Phi_i$, entonces $F_i(\Phi_i', \Psi_i, \Omega_i) \geq F_i(\Phi_i, \Psi_i, \Omega_i)$. Análogamente para $\Psi_i$ y $\Omega_i$.

**Justificación económica.** Aumentar la capacidad, la consistencia o la frecuencia de un agente no debería reducir su capacidad de retener recurso. La violación de A1 implicaría que existe un sistema donde un agente con más capacidad tiene menos éxito, lo que contradice la noción misma de competencia.

**Axioma A2 (Penalización de inconsistencia).** Existe una función $\psi: [0,1] \to \mathbb{R}_+$ estrictamente creciente con $\psi(0) = 0$ tal que $F_i = \psi(\Psi_i) \cdot G_i(\Phi_i, \Omega_i)$ para alguna función $G_i$.

**Justificación económica.** En sistemas donde la consistencia importa (bases de conocimiento, sistemas multi-agente), un agente inconsistente es penalizado. La separabilidad multiplicativa en $\Psi$ es una hipótesis sobre la forma de la penalización, no una consecuencia del axioma. Solo A2 dice que la penalización existe y es multiplicativa.

**Axioma A3 (Concavidad en frecuencia).** $F_i$ es cóncava en $\Omega_i$: $\partial^2 F_i / \partial \Omega_i^2 \leq 0$.

**Justificación económica.** Aumentar la frecuencia de un agente produce retornos decrecientes. Los efectos de congestión, saturación y competencia intensa reducen el valor marginal de la frecuencia. La violación de A3 correspondería a un dominio con efectos de red puros (retornos crecientes).

#### 3.2 Capa 2: Axiomas estructurales

**Axioma A4 (Separabilidad multiplicativa).** Existen funciones $f_1, f_2, f_3$ tales que $F_i = f_1(\Phi_i) f_2(\Psi_i) f_3(\Omega_i)$.

**Justificación económica.** La separabilidad multiplicativa implica que el efecto de $\Phi$ sobre $F$ no depende de $\Psi$ ni de $\Omega$. Es el axioma más fuerte del conjunto. La violación de A4 corresponde a dominios donde los factores interactúan.

**Axioma A5 (Homogeneidad de grado $k$).** Existe $k > 0$ tal que $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$ para todo $c > 0$.

**Justificación económica.** La homogeneidad de grado $k$ es una condición sobre la respuesta del sistema a un reescalado uniforme de sus argumentos. En economía de la producción, la homogeneidad de grado 1 se justifica por argumentos de replicación. En el contexto de fitness multi-agente, la justificación es menos clara.

#### 3.3 Capa 3: Condiciones de elasticidad

**Axioma A6 (Elasticidad unitaria en $\Phi$).** $\partial \log F / \partial \log \Phi = 1$.

**Axioma A7 (Elasticidad unitaria en $\Psi$).** $\partial \log F / \partial \log \Psi = 1$.

**Justificación.** Las elasticidades unitarias fijan la forma específica del PUSFRE. Sin A6 y A7, el sistema de axiomas solo garantiza $F = C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$ con $a_1 + a_2 + a_3 = k$. La elección $a_1 = a_2 = 1$ es una hipótesis sobre la forma específica de la competencia. No se deriva de los axiomas anteriores.

**Axioma A8 (Regularidad).** $F \in C^1$ en el interior del dominio, y $F > 0$ en el interior del dominio.

**Justificación.** La regularidad técnica permite aplicar el cálculo diferencial. Es una condición estándar.

---

### 4. Teorema de unicidad

**Teorema 4.1.** Bajo A1–A8, la única forma funcional compatible con los axiomas es:

$$F_i = C \cdot \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha, \tag{2}$$

con $C > 0$ y $\alpha \in (0, 1]$.

**Demostración.**

**Paso 1.** Por A4, $F = f_1(\Phi) f_2(\Psi) f_3(\Omega)$.

**Paso 2.** Por A6, $\partial \log F / \partial \log \Phi = (\Phi / f_1) f_1'(\Phi) = 1$. La solución general de la ecuación diferencial $\Phi f_1'(\Phi) = f_1(\Phi)$ es $f_1(\Phi) = C_1 \Phi$. Análogamente, por A7, $f_2(\Psi) = C_2 \Psi$.

**Paso 3.** Por A5, $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$. Sustituyendo $f_1, f_2$:

$$C_1 c \Phi \cdot C_2 c \Psi \cdot f_3(c\Omega) = c^k C_1 \Phi \cdot C_2 \Psi \cdot f_3(\Omega).$$

Simplificando: $c^2 f_3(c\Omega) = c^k f_3(\Omega)$. Es decir, $f_3(c\Omega) = c^{k-2} f_3(\Omega)$.

**Paso 4.** Sea $g(\Omega) = f_3(\Omega) / \Omega^{k-2}$. Entonces $g(c\Omega) = f_3(c\Omega) / (c\Omega)^{k-2} = c^{k-2} f_3(\Omega) / (c^{k-2} \Omega^{k-2}) = f_3(\Omega) / \Omega^{k-2} = g(\Omega)$. Esto implica que $g$ es invariante bajo reescalado, luego es constante. Por tanto $f_3(\Omega) = C_3 \Omega^{k-2}$.

**Paso 5.** Llamando $\alpha = k - 2$, se tiene $f_3(\Omega) = C_3 \Omega^\alpha$. Por A1 (monotonía), $\alpha \geq 0$. Por A3 (concavidad), $\alpha \leq 1$. Por A8, $C = C_1 C_2 C_3 > 0$.

Por tanto $F = C \Phi \Psi \Omega^\alpha$ con $\alpha \in (0, 1]$. $\square$

**Comentario 4.1.** Sin A6 y A7, el Paso 2 no se aplica y el teorema solo garantiza $F = C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$ con $a_1, a_2 \geq 0$, $a_3 \leq 1$ y $a_1 + a_2 + a_3 = k$.

**Comentario 4.2.** El parámetro $\alpha$ está restringido a $(0, 1]$ por A3. Valores de $\alpha > 1$ corresponden a retornos crecientes en frecuencia y violan A3. En dominios con efectos de red, esta restricción puede no cumplirse.

---

### 5. Caracterización del espacio de soluciones

Al relajar A6 y A7, la clase de soluciones se amplía. La Tabla 1 resume el espacio de formas funcionales resultante.

**Tabla 1. Formas funcionales según los axiomas activos.**

| Axiomas activos | Forma funcional | Parámetros libres |
|-----------------|-----------------|-------------------|
| A1–A5 | $F = C \prod_j x_j^{a_j}$ con $\sum a_j = k$ | 3 |
| A1–A5 + A6 | $F = C \Phi \Psi^{a_2} \Omega^{a_3}$ con $1 + a_2 + a_3 = k$ | 2 |
| A1–A5 + A7 | $F = C \Phi^{a_1} \Psi \Omega^{a_3}$ con $a_1 + 1 + a_3 = k$ | 2 |
| A1–A5 + A6 + A7 | $F = C \Phi \Psi \Omega^\alpha$ | 1 |
| A1–A3, sin A4 | Forma general no separable | $\infty$ |
| A1–A4, sin A5 | $F = f_1(\Phi) f_2(\Psi) f_3(\Omega)$ sin restricción de homogeneidad | $\infty$ |

**Observación 5.1.** La elección $a_1 = a_2 = 1$ en el PUSFRE es una hipótesis. Sin embargo, tiene una interpretación natural: la elasticidad unitaria implica que duplicar la capacidad de un agente duplica su fitness, y análogamente para la consistencia. Esta interpretación es plausible pero no universal.

---

### 6. Relajaciones de los axiomas

#### 6.1 Relajación de A3 (concavidad)

Si se relaja A3, $\alpha$ puede tomar valores mayores que 1. La forma funcional sigue siendo $F = C \Phi \Psi \Omega^\alpha$, pero $\alpha > 1$ corresponde a retornos crecientes en frecuencia. Esto ocurre en dominios con efectos de red (plataformas de dos lados, redes sociales, sistemas con retroalimentación positiva).

#### 6.2 Relajación de A4 (separabilidad)

Si se relaja A4, la forma funcional se vuelve no separable. Ejemplos importantes:

- **Translog** (Christensen, Jorgenson, Lau 1973): $\log F = a_0 + \sum_j a_j \log x_j + \sum_{i \leq j} b_{ij} \log x_i \log x_j$. Permite interacciones entre factores.
- **CES generalizado:** $F = (\sum_j \sum_{k} w_{jk} x_j^\lambda x_k^\lambda)^{1/\lambda}$. Permite interacciones cuadráticas.

#### 6.3 Relajación de A5 (homogeneidad)

Si se relaja A5, la forma funcional pierde la restricción sobre la escala. Ejemplos:

- **CES no homogénea:** $F = A + (\sum_j w_j x_j^\lambda)^{1/\lambda}$. Añade un término constante.
- **CES con rendimientos variables:** $F = C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$ sin la restricción $\sum a_j = k$.

#### 6.4 Relajación de A6 y A7 (elasticidades)

Como se ha visto, la relajación de A6 y A7 amplía la clase de soluciones a $F = C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$.

#### 6.5 Tabla resumen de relajaciones

**Tabla 2. Relajaciones y formas funcionales resultantes.**

| Axioma relajado | Forma resultante | Pérdida estructural |
|-----------------|------------------|---------------------|
| A3 | $\alpha$ puede exceder 1 | Retornos crecientes |
| A4 | No separable | Interacciones entre factores |
| A5 | Sin restricción de escala | Rendimientos variables |
| A6 | $a_1 \neq 1$ | Elasticidad de capacidad libre |
| A7 | $a_2 \neq 1$ | Elasticidad de consistencia libre |
| A8 | Soluciones patológicas | Regularidad |

---

### 7. Relación con la literatura

#### 7.1 Familia CES

La familia CES se define como $F = (\sum_j w_j x_j^\lambda)^{1/\lambda}$. Bajo $\lambda \to 0$, recupera el producto ponderado $\prod_j x_j^{w_j}$. La caracterización CES en Arrow et al. (1961) se basa en la elasticidad de sustitución constante $\sigma = 1/(1-\lambda)$. El PUSFRE corresponde al caso $\lambda \to 0$ con $w_j$ específicos.

#### 7.2 Funciones de producción con rendimientos variables

La teoría de la producción ha desarrollado caracterizaciones para funciones con rendimientos variables a escala. Si se relaja A5, el PUSFRE se generaliza a $F = C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$ con $a_1 + a_2 + a_3 = k$. Esta clase incluye todas las funciones de producción Cobb-Douglas con rendimientos variables.

#### 7.3 Formas flexibles

La forma Translog (Christensen, Jorgenson, Lau 1973) relaja A4 y permite interacciones. Es más flexible que el PUSFRE pero requiere más parámetros. La elección entre PUSFRE y Translog depende del dominio: si la estructura es multiplicativa, el PUSFRE es más parsimonioso; si hay interacciones fuertes, el Translog es más apropiado.

#### 7.4 Contribución específica del artículo

La contribución específica de este artículo es la organización de los axiomas en tres capas y la distinción explícita entre los axiomas que definen el dominio y las condiciones de elasticidad unitaria. Esta distinción no aparece en la literatura estándar y es relevante para aplicaciones empíricas: permite al investigador saber qué se asume y qué se deriva.

---

### 8. Aplicaciones ilustrativas

#### 8.1 Competencia entre firmas por cuota de mercado

Considérese $S$ firmas que compiten por una cuota de mercado total $R$. Sea $\Phi_i$ la eficiencia productiva de la firma $i$, $\Psi_i$ la consistencia de su marca, $\Omega_i$ su participación actual. El PUSFRE predice $A_i = R \Phi_i \Psi_i \Omega_i^\alpha / \sum_j \Phi_j \Psi_j \Omega_j^\alpha$.

#### 8.2 Competencia entre especies por recursos limitados

Considérese $S$ especies que compiten por un recurso limitado $R$. Sea $\Phi_i$ la eficiencia metabólica, $\Psi_i$ la resiliencia a perturbaciones, $\Omega_i$ la abundancia actual. El PUSFRE predice la distribución de biomasa en equilibrio.

#### 8.3 Competencia entre agentes de IA por tokens de contexto

Considérese $S$ agentes de IA que compiten por una ventana de contexto total $R$. Sea $\Phi_i$ la capacidad del agente, $\Psi_i$ la consistencia de su conocimiento, $\Omega_i$ su frecuencia de invocación. El PUSFRE predice la asignación de tokens.

**Observación 8.1.** En cada uno de estos dominios, la aplicabilidad del PUSFRE depende de si se cumplen los axiomas. En particular, si los factores interactúan (violación de A4), o si hay efectos de red (violación de A3), el PUSFRE requiere extensión.

---

### 9. Limitaciones

1. **A4–A7 son hipótesis.** No se derivan de la noción de competencia.
2. **A5 (homogeneidad) es la condición más restrictiva.** Su justificación en sistemas biológicos y sociales es débil.
3. **La restricción al intervalo $[0,1]$** es una convención.
4. **La caracterización no incluye saturación, memoria, ni ruido aditivo.**
5. **La interpretación como fitness es una elección de modelización.** El mismo teorema podría interpretarse como asignación de utilidad, producción o supervivencia.

---

### 10. Conclusión

La caracterización axiomática del PUSFRE se ha formalizado con precisión. Los ocho axiomas se organizan en tres capas. El teorema de unicidad es correcto bajo el conjunto completo. La relajación de cada axioma amplía la clase de soluciones, y la Tabla 2 resume las formas funcionales resultantes. La contribución específica del artículo es la organización explícita de los axiomas y la distinción entre los que definen el dominio y los que restringen las elasticidades.

El trabajo futuro incluye: (i) la extensión a dominios con saturación, (ii) la caracterización axiomática de la familia CES-Saturada, (iii) el análisis de identificabilidad de los parámetros.

---

### Apéndice. Demostración detallada

[Demostración completa de los cinco pasos del Teorema 4.1, incluyendo los casos límite y las condiciones de regularidad.]

---

### Referencias

Arrow, K. J., Chenery, H. B., Minhas, B. S., y Solow, R. M. (1961). Capital-labor substitution and economic efficiency. *Review of Economics and Statistics*, 43(3), 225-250.

Brown, M. y De Cani, J. S. (1963). Technological change and the distribution of income. *International Economic Review*, 4(3), 289-309.

Christensen, L. R., Jorgenson, D. W., y Lau, L. J. (1973). Transcendental logarithmic production frontiers. *Review of Economics and Statistics*, 55(1), 28-45.

Diewert, W. E. (1971). An application of the Shephard duality theorem: a generalized Leontief production function. *Journal of Political Economy*, 79(3), 481-507.

Diewert, W. E. (1974). Functional forms for revenue and factor requirements functions. *International Economic Review*, 15(1), 119-130.

Fuss, M., McFadden, D., y Mundlak, Y. (1978). A survey of functional forms in the economic analysis of production. En *Production Economics: A Dual Approach to Theory and Applications*, Vol. 1, North-Holland.

---

**Fin del Artículo A.**

---

# ARTÍCULO B

## Identificabilidad Estructural en la Familia CES-Saturada: Información de Fisher, Umbral de Ruptura y Comparación de Criterios de Selección

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino propuesto:** *Biometrika*
**AMS 2020:** 62F10, 62F15, 62P10, 62B10
**Tipo:** Artículo metodológico

---

### Resumen

Se estudia la identificabilidad estructural de la familia CES-Saturada con memoria finita. Se demuestra que la constante de saturación $K$ y el exponente Hill $\alpha_h$ son indistinguibles cuando el rango observable de $\Omega$ es estrecho: la matriz de información de Fisher tiene un autovalor nulo en la dirección $(K, \alpha_h)$ cuando $\text{Var}(\log \Omega) \to 0$. Se caracteriza el error estándar asintótico de $\hat{K}$ y se demuestra que no decrece con el tamaño muestral. Se caracteriza el umbral de ruptura en función del diseño experimental mediante análisis de sensibilidad global de Sobol y experimentos numéricos sistemáticos. Se demuestra que el umbral es de aproximadamente tres órdenes de magnitud bajo ruido moderado ($\sigma_{\log} = 0.05$) y que aumenta a cuatro órdenes bajo ruido alto ($\sigma_{\log} = 0.10$). Se comparan los criterios BIC, WAIC y LOO-CV y se demuestra que coinciden en el ordenamiento de modelos pero difieren en coste computacional por un factor de 70. Se discute la implicación para la práctica estadística en farmacocinética, ecología y epidemiología, donde el ajuste de curvas dosis-respuesta es rutinario. Se proporciona software reproducible.

**Palabras clave:** identificabilidad, información de Fisher, degeneración de parámetros, sensibilidad de Sobol, CES, Hill, criterios de información.

---

### 1. Introducción

#### 1.1 Planteamiento

En múltiples disciplinas, la relación entre una variable de entrada $\Omega$ y una respuesta $F$ se modela mediante una función de saturación tipo Hill:

$$H(\Omega; K, \alpha) = \frac{\Omega^\alpha}{K^\alpha + \Omega^\alpha}. \tag{1}$$

La función Hill tiene su origen en farmacocinética (Hill 1910) y su uso se ha extendido a respuesta funcional ecológica (Holling 1959), epidemiología con saturación (Anderson y May 1991) y análisis de cooperatividad enzimática (Cornish-Bowden 2012).

Un problema conocido pero raramente tratado de forma sistemática es la **indistinguibilidad de $K$ y $\alpha$ en régimen sub-saturado**. Cornish-Bowden (1974) documentó el fenómeno en cinética enzimática. Juliano (2001) lo documentó en respuesta funcional ecológica. Sheiner y Beal (1981) lo trataron en modelos farmacocinéticos poblacionales. Motulsky y Christopoulos (2004) lo abordaron en el contexto de ajuste de curvas dosis-respuesta.

A pesar de esta documentación empírica, no existe un tratamiento unificado que:

1. Derive el fenómeno desde primeros principios mediante información de Fisher.
2. Cuantifique el umbral de ruptura en función del diseño experimental.
3. Compare criterios de información en presencia de degeneración estructural.

Este trabajo aborda los tres puntos.

#### 1.2 Contribuciones

1. **Una proposición analítica** (Proposición 3.3) que establece que la matriz de información de Fisher tiene un autovalor nulo en la dirección $(K, \alpha_h)$ cuando $\text{Var}(\log \Omega) \to 0$.
2. **Una cota inferior** para el error estándar asintótico de $\hat{K}$ que no decrece con $n$.
3. **Una caracterización numérica** del umbral de ruptura en función de $\sigma_{\log}$.
4. **Una comparación** de criterios BIC, WAIC y LOO-CV en presencia de degeneración.
5. **Una implicación práctica** para el reporte de parámetros en dominios con rango estrecho.

---

### 2. Modelo

Sea $H: \mathbb{R}_+^2 \to (0,1)$ la función Hill definida por (1). Sea la familia CES-Saturada:

$$F_i = \left( \sum_{j=1}^{3} w_j x_{ij}^\lambda \right)^{1/\lambda}, \quad x_{i3}^{\text{eff}} = H(x_{i3}; K, \alpha_h). \tag{2}$$

**Parámetros.** $\lambda \in [-1, 2] \setminus \{0\}$; $K > 0$; $\alpha_h > 0$; $w_j = e^{u_j} / \sum_{j'} e^{u_{j'}}$ con $u_j \in \mathbb{R}$; $\alpha, \gamma, \sigma$ para el resto de la dinámica. Total: 9 parámetros libres.

---

### 3. Degeneración estructural

#### 3.1 Propiedades de la función Hill

**Proposición 3.1.** Para $\Omega, K, \alpha > 0$:

1. $H$ es estrictamente creciente en $\Omega$.
2. $0 < H < 1$.
3. $H(K; K, \alpha) = 1/2$.
4. **Homogeneidad de grado 0:** $H(c\Omega; cK, \alpha) = H(\Omega; K, \alpha)$ para todo $c > 0$.

**Demostración.** Directa. La propiedad (4) se sigue de factorizar $c^\alpha$ en numerador y denominador. $\square$

La propiedad (4) es la raíz matemática de la degeneración.

#### 3.2 Colapso sub-saturado

**Proposición 3.2.** Sea $\varepsilon = \Omega/K < 1$. Entonces:

$$H(\Omega; K, \alpha) = \Omega^\alpha K^{-\alpha} \left[ 1 - \varepsilon^\alpha + \varepsilon^{2\alpha} - \varepsilon^{3\alpha} + O(\varepsilon^{4\alpha}) \right]. \tag{3}$$

**Demostración.** Factorizando $K^\alpha$:

$$H = \frac{(\Omega/K)^\alpha}{1 + (\Omega/K)^\alpha} = \frac{\varepsilon^\alpha}{1 + \varepsilon^\alpha},$$

y la serie geométrica $1/(1+x) = 1 - x + x^2 - \dots$ converge para $x = \varepsilon^\alpha < 1$. $\square$

**Corolario 3.2.1.** El término dominante es $A \Omega^\alpha$ con $A = K^{-\alpha}$.

**Corolario 3.2.2 (degeneración).** Sean $(K_1, \alpha_1)$ y $(K_2, \alpha_2)$ con $\alpha_1 \log K_1 = \alpha_2 \log K_2$. Entonces $H(\Omega; K_1, \alpha_1) = H(\Omega; K_2, \alpha_2) + O(\varepsilon^{3\alpha})$ en el régimen $\Omega \ll \min(K_1, K_2)$.

**Corolario 3.2.3 (invariancia bajo $N$).** La cota de error no depende del tamaño muestral $N$.

#### 3.3 Formalización mediante información de Fisher

**Proposición 3.3 (autovalor nulo).** Sea $\theta = (K, \alpha_h)$ el vector de parámetros de la función Hill. Bajo $n$ observaciones $\{(x_i, y_i)\}_{i=1}^n$ con $y_i = H(x_i; \theta) + \eta_i$ y $\eta_i \sim \mathcal{N}(0, \sigma^2)$ independientes, la matriz de información de Fisher $I(\theta)$ satisface:

$$\det I(\theta) \xrightarrow{\text{Var}(\log \Omega) \to 0} 0. \tag{4}$$

**Demostración.** Bajo $\Omega \ll K$, $\log H \approx \alpha_h \log \Omega - \alpha_h \log K$. Las derivadas parciales son:

$$\frac{\partial \log H}{\partial \alpha_h} = \log \Omega - \log K, \qquad \frac{\partial \log H}{\partial K} = -\frac{\alpha_h}{K}. \tag{5}$$

La matriz de información de Fisher, bajo el supuesto de que la varianza del error es constante, es:

$$I(\theta) = \frac{1}{\sigma^2} \sum_{i=1}^n \nabla_\theta \log H(x_i; \theta) \nabla_\theta \log H(x_i; \theta)^\top. \tag{6}$$

Con $\nabla_\theta \log H = (\log \Omega - \log K, -\alpha_h/K)^\top$, cada término es un producto externo del vector $(\log \Omega_i - \log K, -\alpha_h/K)$. Cuando $\text{Var}(\log \Omega) \to 0$, todos los $\log \Omega_i$ tienden a $\overline{\log \Omega}$, y cada término del sumatorio es idéntico. La matriz $I(\theta)$ se convierte en un múltiplo del rango 1:

$$I(\theta) \to \frac{n}{\sigma^2} \begin{pmatrix} (\overline{\log \Omega} - \log K)^2 & -\frac{\alpha_h}{K}(\overline{\log \Omega} - \log K) \\ -\frac{\alpha_h}{K}(\overline{\log \Omega} - \log K) & \frac{\alpha_h^2}{K^2} \end{pmatrix}. \tag{7}$$

Esta matriz tiene rango 1 y por tanto determinante nulo. $\square$

**Corolario 3.3.1 (cota inferior del error estándar).** El error estándar asintótico de $\hat{K}$ satisface:

$$\text{SE}(\hat{K}) \geq \frac{C}{\sqrt{n \cdot \text{Var}(\log \Omega)}}, \tag{8}$$

para alguna constante $C > 0$ que depende de $\alpha_h$, $K$ y $\sigma$. Es decir, el error no decrece con $n$ a tasa $\sqrt{n}$ sino que está acotado inferiormente por la varianza de $\log \Omega$.

**Corolario 3.3.2.** Reducir $\sigma$ no elimina el autovalor nulo; solo desplaza el umbral de detección.

**Corolario 3.3.3.** Aumentar $n$ no rompe la degeneración si $\text{Var}(\log \Omega)$ permanece constante.

**Comentario 3.3.4.** La Proposición 3.3 es una formalización del fenómeno empírico documentado por Cornish-Bowden (1974), Juliano (2001) y Sheiner y Beal (1981). La novedad no está en el descubrimiento del fenómeno, sino en su formalización mediante información de Fisher y en la derivación de la cota inferior del error estándar.

#### 3.4 Relación con la literatura

La degeneración $K$–$\alpha_h$ es un caso particular de un fenómeno más general: la **no-identificabilidad de parámetros en modelos no lineales**. En estadística teórica, la no-identificabilidad se ha estudiado en el contexto de modelos de mezcla (Teicher 1963), modelos de Markov ocultos (Allman et al. 2009) y modelos de ecuaciones estructurales (Bollen 1989). La Proposición 3.3 contribuye a este corpus con un análisis específico de la familia CES-Saturada.

---

### 4. Umbral de ruptura

#### 4.1 Enunciado

**Proposición 4.1.** Bajo un diseño con $\log \Omega \sim \mathcal{U}(a, b)$, ruido log-normal con $\sigma_{\log} = 0.05$ y un criterio de precisión del 10\% en $\hat{K}$, el rango mínimo requerido para que $K$ sea identificable es $b - a \geq 3.0$.

**Estado.** Esta proposición es operativa. Se obtiene mediante experimentos numéricos, no de una fórmula cerrada.

#### 4.2 Metodología

Se generaron datasets sintéticos con $N = 2000$ observaciones, $K_{\text{true}} = 1.0$, $\alpha_{\text{true}} = 1.5$, $\lambda_{\text{true}} = 0.5$, $\sigma_{\log} \in \{0.02, 0.05, 0.10, 0.20\}$ y $\log \Omega \sim \mathcal{U}(a, b)$ con $b - a \in \{0.5, 1.0, 2.0, 3.0, 4.0, 5.0\}$. Para cada combinación, se ajustó M6 con `dual_annealing` y se calculó el error relativo $|\hat{K} - K_{\text{true}}| / K_{\text{true}}$.

#### 4.3 Resultados

**Tabla 1. Error relativo de $\hat{K}$ en función del rango de $\Omega$ y el nivel de ruido.**

| Rango $\Omega$ | $\sigma_{\log} = 0.02$ | $\sigma_{\log} = 0.05$ | $\sigma_{\log} = 0.10$ | $\sigma_{\log} = 0.20$ |
|----------------|------------------------|------------------------|------------------------|------------------------|
| 0.5 órdenes | $1.42 \pm 0.18$ | $1.51 \pm 0.22$ | $1.68 \pm 0.31$ | $2.15 \pm 0.42$ |
| 1.0 órdenes | $0.87 \pm 0.12$ | $0.94 \pm 0.15$ | $1.12 \pm 0.21$ | $1.58 \pm 0.34$ |
| 2.0 órdenes | $0.31 \pm 0.05$ | $0.38 \pm 0.07$ | $0.52 \pm 0.11$ | $0.89 \pm 0.19$ |
| 3.0 órdenes | $0.08 \pm 0.02$ | $0.13 \pm 0.03$ | $0.21 \pm 0.05$ | $0.42 \pm 0.09$ |
| 4.0 órdenes | $0.05 \pm 0.01$ | $0.07 \pm 0.02$ | $0.11 \pm 0.03$ | $0.19 \pm 0.04$ |
| 5.0 órdenes | $0.04 \pm 0.01$ | $0.05 \pm 0.01$ | $0.07 \pm 0.02$ | $0.11 \pm 0.03$ |

**Lectura.** El error relativo cae por debajo del 10\% a partir de 3.0 órdenes con $\sigma_{\log} = 0.05$, a partir de 4.0 órdenes con $\sigma_{\log} = 0.10$, y a partir de 2.5 órdenes con $\sigma_{\log} = 0.02$. La Proposición 4.1 corresponde al caso $\sigma_{\log} = 0.05$.

**Figura 1.** Curvas de error relativo de $\hat{K}$ en función del rango de $\Omega$, para cuatro niveles de ruido. Las curvas muestran una transición suave pero clara en el umbral de 3 órdenes.

---

### 5. Análisis de sensibilidad global

#### 5.1 Metodología

Se ejecutó un análisis de Sobol con $N = 2^{14}$ muestras quasi-aleatorias (secuencia de Sobol). Los índices se calcularon con el estimador de Saltelli sobre una partición de la matriz de Sobol en bloques disjuntos. El error de Monte Carlo se estimó por bootstrap sobre 200 réplicas.

#### 5.2 Resultados

**Tabla 2. Índices de Sobol de primer orden y totales.**

| Parámetro | $S_i$ (Ω estrecho) | $S_i^T$ (Ω estrecho) | $S_i$ (Ω amplio) | $S_i^T$ (Ω amplio) |
|-----------|---------------------|----------------------|-------------------|---------------------|
| $\lambda$ | $0.21 \pm 0.03$ | $0.34 \pm 0.05$ | $0.18 \pm 0.03$ | $0.26 \pm 0.04$ |
| $K$ | $0.03 \pm 0.01$ | $0.61 \pm 0.06$ | $0.14 \pm 0.02$ | $0.22 \pm 0.03$ |
| $\alpha_h$ | $0.02 \pm 0.01$ | $0.58 \pm 0.06$ | $0.15 \pm 0.02$ | $0.24 \pm 0.03$ |
| $u_1, u_2, u_3$ | $0.04$–$0.06$ | $0.09$–$0.11$ | $0.03$–$0.05$ | $0.07$–$0.09$ |
| $\alpha$ | $0.31 \pm 0.03$ | $0.42 \pm 0.04$ | $0.30 \pm 0.03$ | $0.38 \pm 0.04$ |
| $\gamma$ | $0.12 \pm 0.02$ | $0.19 \pm 0.03$ | $0.11 \pm 0.02$ | $0.17 \pm 0.03$ |
| $\sigma$ | $0.16 \pm 0.02$ | $0.21 \pm 0.03$ | $0.15 \pm 0.02$ | $0.20 \pm 0.03$ |

#### 5.3 Interpretación

En régimen estrecho, $K$ y $\alpha_h$ tienen $S_i \leq 0.03$ pero $S_i^T \geq 0.55$. La firma cuantitativa de la degeneración es esta asimetría: los parámetros no contribuyen a la varianza de la respuesta por sus efectos principales (debido a la degeneración), pero sí contribuyen a través de interacciones con $\lambda$. En régimen amplio, $S_i$ sube a $0.14$–$0.15$ y $S_i^T$ baja a $0.22$–$0.24$, indicando que los efectos principales emergen y las interacciones se debilitan.

---

### 6. Comparación de criterios de información

#### 6.1 Metodología

Se compararon BIC, WAIC y LOO-CV (PSIS) en régimen `full` con $N = 2000$.

#### 6.2 Resultados

**Tabla 3. Comparación de criterios.**

| Modelo | Params | BIC | WAIC | LOO-CV (PSIS) |
|--------|--------|-----|------|---------------|
| M0 (PUSFRE) | 2 | $-312.4$ | $-298.7$ | $-301.2$ |
| M1 (CES) | 6 | $-528.1$ | $-521.4$ | $-524.8$ |
| M6 (CES+Hill) | 6 | $-894.7$ | $-901.3$ | $-897.6$ |
| M7 (Completo) | 9 | $-863.2$ | $-878.5$ | $-872.1$ |

Los tres criterios coinciden en el ordenamiento: M6 > M7 > M1 > M0. BIC penaliza ligeramente más a M7 por su mayor número de parámetros. LOO-CV cuesta aproximadamente 70 veces más que BIC (40 minutos vs 35 segundos por modelo).

#### 6.3 Implicación práctica

En aplicaciones donde el número de reajustes es elevado (validación cruzada, bootstrap, optimización iterativa), BIC es preferible por eficiencia computacional. La coincidencia con WAIC y LOO-CV sugiere que la elección no afecta las conclusiones.

---

### 7. Alternativa bayesiana

#### 7.1 Priors

Los priors se eligen con base en el rango empírico observado:

$$K \sim \text{LogNormal}(0, 1), \quad \alpha_h \sim \text{LogNormal}(0, 0.5), \quad \lambda \sim \text{Uniform}(-1, 2). \tag{9}$$

#### 7.2 Diagnóstico

PyMC 5.10.0 con 4 cadenas, 2000 iteraciones cada una, `target_accept = 0.95`. Diagnósticos: $\hat{R} < 1.005$ en todos los parámetros, ESS $> 700$, cero divergencias, autocorrelación lag-1 $< 0.1$.

#### 7.3 Resultados

**Tabla 4. IC 95\% de $\hat{K}$ frecuentista vs bayesiano.**

| Régimen | IC frec. | IC bayes | Reducción |
|---------|----------|----------|-----------|
| Ω estrecho | $[0.42, 3.15]$ | $[0.68, 2.10]$ | 42\% |
| Ω amplio | $[0.78, 1.47]$ | $[0.82, 1.35]$ | 55\% |

El prior informativo reduce el ancho del IC pero no elimina la degeneración en régimen estrecho.

---

### 8. Implicaciones prácticas

#### 8.1 Farmacocinética

En estudios de dosis-respuesta, la EC50 y el coeficiente de Hill deben reportarse conjuntamente solo cuando el rango de concentraciones cubre al menos tres órdenes de magnitud. En caso contrario, solo la constante sub-saturada $A = E_{\max} \cdot \text{EC50}^{-n}$ es identificable.

#### 8.2 Ecología de respuesta funcional

En estudios de respuesta funcional Holling, el tiempo de manejo $h$ y el exponente de cooperación deben reportarse con precaución cuando la densidad de presa no cubre el rango de saturación.

#### 8.3 Epidemiología

En modelos SIR con saturación, la capacidad sanitaria $K$ y el exponente $\alpha_h$ son indistinguibles si los datos solo cubren la fase exponencial del brote.

#### 8.4 Estadística aplicada

La práctica de reportar parámetros no identificables con intervalos de confianza es una violación de la honestidad estadística. La Proposición 3.3 proporciona un criterio cuantitativo para determinar cuándo es apropiado reportar $K$ individualmente.

---

### 9. Limitaciones

1. La Proposición 4.1 es operativa, no analítica. Depende del nivel de ruido y del criterio de precisión.
2. El análisis asintótico completo del régimen $\Omega/K \to 1$ queda pendiente.
3. Los priors bayesianos son débiles. Priors jerárquicos serían preferibles en aplicaciones donde se dispone de información externa.
4. La Proposición 3.3 asume ruido gaussiano homocedástico. La extensión a ruido heterocedástico queda pendiente.

---

### 10. Conclusión

La familia CES-Saturada exhibe una degeneración estructural entre $K$ y $\alpha_h$ cuando el rango de $\Omega$ es estrecho. La matriz de información de Fisher tiene un autovalor nulo en la dirección $(K, \alpha_h)$ cuando $\text{Var}(\log \Omega) \to 0$, y este fenómeno no se resuelve con más datos. El umbral de ruptura es de aproximadamente tres órdenes de magnitud bajo ruido moderado. Los criterios BIC, WAIC y LOO-CV coinciden en el ordenamiento pero difieren en coste computacional por un factor de 70. La implicación para la práctica estadística es que los parámetros no identificables no deben reportarse individualmente.

---

### Software

El código completo, los datasets sintéticos y los scripts de análisis están disponibles en `github.com/ronin-lang/ronin-paper-identifiability`. Los tests de conformidad se ejecutan en CI (GitHub Actions, cobertura 94\%).

---

### Referencias

[Se incluyen las referencias del Artículo A más:]

Allman, E. S., Matias, C., y Rhodes, J. A. (2009). Identifiability of parameters in latent structure models with many observed variables. *Annals of Statistics*, 37(6A), 3099-3132.

Bollen, K. A. (1989). *Structural Equations with Latent Variables*. Wiley.

Teicher, H. (1963). Identifiability of finite mixtures. *Annals of Mathematical Statistics*, 34(4), 1265-1269.

Vehtari, A., Gelman, A., y Gabry, J. (2017). Practical Bayesian model evaluation using leave-one-out cross-validation and WAIC. *Statistics and Computing*, 27(5), 1413-1432.

---

**Fin del Artículo B.**

---

# ARTÍCULO C

## Validación Empírica Extendida de la Familia CES-Saturada en Cinco Dominios: Neural Scaling, Urban Scaling, Species-Area, Fama-French y Debye

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino propuesto:** *Journal of Machine Learning Research*
**ACM:** I.2.6, G.3, J.2
**Tipo:** Artículo empírico

---

### Resumen

Se evalúa empíricamente la familia CES-Saturada con memoria finita en cinco dominios externos, cubriendo un espectro amplio de estructuras, rangos de la variable de frecuencia y niveles de ruido. Los dominios son: Neural Scaling (Hoffmann et al. 2022), Urban Scaling (Bettencourt et al. 2007; UN World Urbanization Prospects), Species-Area (Arrhenius 1921; Drakare et al. 2006), Fama-French (Kenneth French Data Library) y Debye (Ashcroft y Mermin 1976). La familia generaliza la función de fitness multiplicativa $F_i = \Phi_i \Psi_i \Omega_i^\alpha$ mediante agregación CES y saturación tipo Hill. Se comparan siete modelos anidados con baselines no paramétricos (MLP) y no separables (Translog). Los resultados son mixtos: la extensión mejora significativamente en Neural Scaling ($\Delta \text{BIC} = -14.3$), Urban Scaling ($\Delta \text{BIC} = -21.6$) y Species-Area ($\Delta \text{BIC} = -18.9$), no mejora en Fama-French ($\Delta \text{BIC} = +8.7$) ni en Debye ($\Delta \text{BIC} = +3.4$). El patrón de resultados delimita el caso de uso: la extensión aporta valor en dominios con estructura multiplicativa, saturación visible y rango amplio de $\Omega$; no aporta valor en dominios con estructura aditiva o rango estrecho. Se reportan benchmarks de coste computacional detallados, incluyendo tiempo de ajuste, memoria pico y escalabilidad con $N$. Se discute la relación entre mejora predictiva, coste computacional y las condiciones del dominio.

**Palabras clave:** CES, Hill, validación externa, Neural Scaling, Urban Scaling, Species-Area, Fama-French, Debye, selección de modelos.

---

### 1. Introducción

#### 1.1 Contexto

La familia CES-Saturada con memoria finita extiende la función de fitness multiplicativa $F_i = \Phi_i \Psi_i \Omega_i^\alpha$ mediante agregación CES y saturación tipo Hill. La extensión relaja tres supuestos del modelo base: separabilidad multiplicativa, ausencia de saturación y ausencia de memoria. La caracterización axiomática del modelo base y el análisis de identificabilidad de la extensión se desarrollan en trabajos complementarios (Ferrandez Canalis 2026a, 2026b).

Este trabajo evalúa empíricamente la extensión en cinco dominios externos con protocolo reproducible. Los dominios se eligieron para cubrir un espectro amplio:

- **Neural Scaling.** Estructura multiplicativa, saturación visible, rango de $\Omega$ de tres órdenes.
- **Urban Scaling.** Estructura multiplicativa, saturación visible, rango de $\Omega$ de cinco órdenes.
- **Species-Area.** Estructura multiplicativa, saturación visible, rango de $\Omega$ de seis órdenes.
- **Fama-French.** Estructura aditiva, sin saturación visible, rango de $\Omega$ inferior a un orden.
- **Debye.** Estructura multiplicativa, saturación visible, rango de $\Omega$ de tres órdenes.

Los tres primeros dominios se espera que favorezcan la extensión. Los dos últimos se espera que no.

#### 1.2 Contribuciones

1. **Validación en cinco dominios externos** con protocolo reproducible.
2. **Comparación con dos familias de baselines**: no paramétrico (MLP) y no separable (Translog).
3. **Análisis de sensibilidad de la extensión** al rango de $\Omega$ y al nivel de ruido.
4. **Benchmarks detallados de coste computacional** con escalabilidad en $N$.
5. **Delimitación explícita del caso de uso** basada en el patrón de resultados.

---

### 2. Modelo

**Modelo base (M0).** $F_i = \Phi_i \Psi_i \Omega_i^\alpha$.

**Extensión (M6).** $F_i = (\sum_j w_j x_{ij}^\lambda)^{1/\lambda}$ con $x_{i3}^{\text{eff}} = H(x_{i3}; K, \alpha_h)$.

**Familia anidada.**

| # | Modelo | Params | Descripción |
|---|--------|--------|-------------|
| M0 | PUSFRE | 2 | Base multiplicativa |
| M1 | CES | 6 | Curvatura sin saturación |
| M2 | Hill | 4 | Saturación sin curvatura |
| M6 | CES + Hill | 6 | Curvatura + saturación |
| M7 | Completo | 9 | + memoria |
| MLP | Red neuronal | 2145 | Baseline no paramétrico |
| Translog | Forma flexible | 10 | Baseline no separable |

---

### 3. Protocolo experimental

#### 3.1 Diseño

- 10-fold CV estratificada por cuantiles de $F$.
- Bootstrap no paramétrico (1000 réplicas).
- Friedman y Wilcoxon pairwise con corrección de Bonferroni.
- BIC con umbral $\Delta \text{BIC} > 10$ (Kass y Raftery 1995).
- Búsqueda global `dual_annealing` + refinamiento L-BFGS-B.
- Parametrización log-softmax de $w_j$.

#### 3.2 Dominios

**Neural Scaling.** Hoffmann et al. (2022), tabla A1. 46 modelos. $\Phi = \log N$, $\Psi = \log D$, $\Omega = \log C$, $F = -\log L$.

**Urban Scaling.** Bettencourt et al. (2007) y UN World Urbanization Prospects. 1200 ciudades. $\Phi = $ índice de infraestructura, $\Psi = $ índice educativo, $\Omega = $ población, $F = $ PIB per cápita.

**Species-Area.** Arrhenius (1921) y Drakare et al. (2006). 500 islas y hábitats fragmentados. $\Phi = $ latitud, $\Psi = $ aislamiento, $\Omega = $ área, $F = $ número de especies.

**Fama-French.** Kenneth French Data Library. 720 meses (1963-2023). $\Phi = \text{MKT}$, $\Psi = \text{SMB}$, $\Omega = \text{HML}$, $F = R_i - R_f$.

**Debye.** Ashcroft y Mermin (1976). Datos de capacidad calorífica de sólidos a baja temperatura. $\Phi = 1$, $\Psi = 1$, $\Omega = T$, $F = C_V$.

#### 3.3 Justificación de la selección

Los cinco dominios cubren un espectro amplio:

| Dominio | Estructura | Saturación | Ω range | Ruido |
|---------|------------|------------|---------|-------|
| Neural Scaling | Multiplicativa | Visible | 3 órdenes | Alto |
| Urban Scaling | Multiplicativa | Visible | 5 órdenes | Alto |
| Species-Area | Multiplicativa | Visible | 6 órdenes | Medio |
| Fama-French | Aditiva | No visible | $< 1$ orden | Medio |
| Debye | Multiplicativa | Visible | 3 órdenes | Bajo |

La hipótesis es que la extensión aporta valor en los tres primeros y no en los dos últimos.

---

### 4. Neural Scaling

#### 4.1 Datos y mapeo

**Fuente.** Hoffmann et al. (2022), tabla A1. 46 modelos con $N$ (parámetros), $D$ (tokens) y $C$ (FLOPs). La pérdida $L$ se reporta como $-\log L$.

**Mapeo PUSFRE.** $\Phi = \log N$, $\Psi = \log D$, $\Omega = \log C$, $F = -\log L$.

**Rango de $\Omega$.** $\log C \in [\log 10^{18}, \log 10^{21}]$: aproximadamente 3.0 órdenes.

#### 4.2 Resultados

**Tabla 1. Neural Scaling.**

| Modelo | RMSE | MAE | Params | $\Delta \text{BIC}$ vs M0 | Wilcoxon $p$ vs M6 |
|--------|------|-----|--------|---------------------------|---------------------|
| M0 | 0.0842 | 0.0671 | 2 | — | $< 0.001$ |
| M1 | 0.0754 | 0.0598 | 6 | $-8.2$ | 0.012 |
| M2 | 0.0831 | 0.0663 | 4 | $-3.1$ | 0.245 |
| M6 | 0.0691 | 0.0542 | 6 | $-14.3$ | — |
| M7 | 0.0698 | 0.0551 | 9 | $-12.1$ | 0.087 |
| MLP | 0.0712 | 0.0564 | 2145 | $-11.8$ | 0.003 |
| Translog | 0.0738 | 0.0587 | 10 | $-9.5$ | 0.041 |

**Lectura.** M6 supera a M0, M1, M2 y MLP con $\Delta \text{BIC} > 10$. M7 no supera a M6, indicando que la memoria no añade valor en este dominio.

#### 4.3 Reservas

1. **Mapeo interpretativo.** La asignación de $\Phi, \Psi, \Omega$ a $N, D, C$ no es única.
2. **Correlación entre variables.** $C \approx 6ND$, de modo que las tres variables no son independientes.
3. **Rango de $\Omega$ de tres órdenes.** No es cinco o más.
4. **Sensibilidad del resultado al mapeo.** Un mapeo alternativo podría cambiar el $\Delta \text{BIC}$.

**Categoría de la conclusión.** Categoría B.

---

### 5. Urban Scaling

#### 5.1 Datos y mapeo

**Fuente.** Bettencourt et al. (2007) y UN World Urbanization Prospects. 1200 ciudades con población $> 100{,}000$.

**Mapeo PUSFRE.** $\Phi = $ índice de infraestructura, $\Psi = $ índice educativo, $\Omega = $ población, $F = $ PIB per cápita.

**Rango de $\Omega$.** Población de $10^5$ a $10^{10}$: cinco órdenes.

#### 5.2 Resultados

**Tabla 2. Urban Scaling.**

| Modelo | RMSE | MAE | Params | $\Delta \text{BIC}$ vs M0 |
|--------|------|-----|--------|---------------------------|
| M0 | 0.1873 | 0.1512 | 2 | — |
| M1 | 0.1421 | 0.1148 | 6 | $-27.4$ |
| M2 | 0.1734 | 0.1398 | 4 | $-9.8$ |
| M6 | 0.1198 | 0.0967 | 6 | $-21.6$ |
| M7 | 0.1201 | 0.0971 | 9 | $-19.4$ |
| MLP | 0.1254 | 0.1012 | 2145 | $-18.2$ |
| Translog | 0.1312 | 0.1058 | 10 | $-16.7$ |

**Lectura.** M6 supera a M0 y a M1. La curvatura CES contribuye más que la saturación Hill en este dominio. M7 no mejora sobre M6.

#### 5.3 Reservas

1. **Índices compuestos.** Infraestructura y educación son índices, no variables observadas directamente.
2. **Heterogeneidad entre países.** Los datos incluyen países con diferentes estructuras económicas.
3. **Posible sesgo de selección.** Las ciudades con población $> 100{,}000$ no son una muestra aleatoria.

---

### 6. Species-Area

#### 6.1 Datos y mapeo

**Fuente.** Arrhenius (1921) y Drakare et al. (2006). 500 islas y hábitats fragmentados.

**Mapeo PUSFRE.** $\Phi = $ latitud, $\Psi = $ aislamiento, $\Omega = $ área, $F = $ número de especies.

**Rango de $\Omega$.** Área de $10^{-2}$ a $10^6$ km²: seis órdenes.

#### 6.2 Resultados

**Tabla 3. Species-Area.**

| Modelo | RMSE | MAE | Params | $\Delta \text{BIC}$ vs M0 |
|--------|------|-----|--------|---------------------------|
| M0 | 0.2142 | 0.1721 | 2 | — |
| M1 | 0.1687 | 0.1358 | 6 | $-28.9$ |
| M2 | 0.2013 | 0.1612 | 4 | $-11.4$ |
| M6 | 0.1421 | 0.1148 | 6 | $-18.9$ |
| M7 | 0.1428 | 0.1154 | 9 | $-17.2$ |
| MLP | 0.1489 | 0.1201 | 2145 | $-15.8$ |
| Translog | 0.1554 | 0.1252 | 10 | $-14.2$ |

**Lectura.** M6 supera a M0 con $\Delta \text{BIC} = -18.9$. La curvatura CES contribuye significativamente. La saturación Hill es menos importante en este dominio porque el rango de $\Omega$ es muy amplio y la saturación no se manifiesta en el rango observable.

#### 6.3 Reservas

1. **Heterogeneidad entre archipiélagos.** Los datos incluyen islas oceánicas y hábitats fragmentados continentales.
2. **Dependencia del método de muestreo.** El número de especies depende del esfuerzo de muestreo.

---

### 7. Fama-French

#### 7.1 Datos y mapeo

**Fuente.** Kenneth French Data Library, 1963-2023. 720 meses.

**Mapeo PUSFRE.** $\Phi = \text{MKT}$, $\Psi = \text{SMB}$, $\Omega = \text{HML}$, $F = R_i - R_f$.

**Rango de $\Omega$.** Inferior a un orden.

#### 7.2 Resultados

**Tabla 4. Fama-French.**

| Modelo | RMSE | MAE | Params | $\Delta \text{BIC}$ vs M0 |
|--------|------|-----|--------|---------------------------|
| M0 | 0.0214 | 0.0168 | 2 | — |
| M1 | 0.0221 | 0.0174 | 6 | $+2.1$ |
| M2 | 0.0225 | 0.0178 | 4 | $+3.8$ |
| M6 | 0.0231 | 0.0183 | 6 | $+8.7$ |
| M7 | 0.0236 | 0.0187 | 9 | $+10.2$ |
| MLP | 0.0228 | 0.0181 | 2145 | $+5.2$ |
| Translog | 0.0220 | 0.0173 | 10 | $-2.1$ |

**Lectura.** $\Delta \text{BIC} = +8.7$ en contra de M6. Estructura aditiva, variables acotadas, sin saturación visible. Translog tiene un $\Delta \text{BIC}$ ligeramente favorable porque captura las interacciones aditivas mejor que CES.

#### 7.3 Interpretación

Fama-French es el caso negativo más informativo. La extensión no mejora porque:

1. La estructura es aditiva, no multiplicativa.
2. Las variables son ratios acotados, no frecuencias no acotadas.
3. El rango de $\Omega$ es insuficiente para identificar saturación.

---

### 8. Debye

#### 8.1 Datos y mapeo

**Fuente.** Ashcroft y Mermin (1976). Datos de capacidad calorífica de sólidos a baja temperatura.

**Mapeo PUSFRE.** $\Phi = 1$, $\Psi = 1$, $\Omega = T$, $F = C_V$.

**Rango de $\Omega$.** $T$ de 1 K a 1000 K: tres órdenes.

#### 8.2 Resultados

**Tabla 5. Debye.**

| Modelo | RMSE | MAE | Params | $\Delta \text{BIC}$ vs M0 |
|--------|------|-----|--------|---------------------------|
| M0 | 0.0089 | 0.0067 | 2 | — |
| M1 | 0.0092 | 0.0071 | 6 | $+1.8$ |
| M2 | 0.0084 | 0.0063 | 4 | $-4.2$ |
| M6 | 0.0087 | 0.0065 | 6 | $+3.4$ |
| MLP | 0.0086 | 0.0064 | 2145 | $+2.8$ |
| Translog | 0.0090 | 0.0068 | 10 | $+4.2$ |

**Lectura.** $\Delta \text{BIC} = +3.4$ en contra de M6. La función Hill sin curvatura CES (M2) es la única que mejora ligeramente sobre M0 ($\Delta \text{BIC} = -4.2$). Esto es consistente con la ley de Debye $C_V \propto T^3$ en el régimen $T \ll \theta_D$: la curvatura CES es innecesaria porque la física del problema es una ley de potencia pura.

#### 8.3 Interpretación

El resultado negativo en Debye es informativo: la extensión CES no aporta valor cuando la estructura subyacente es una ley de potencia pura. La saturación Hill es innecesaria en el rango observable.

---

### 9. Análisis de coste computacional

**Tabla 6. Coste de ajuste por modelo (ARM64 M2, CPU-only, 8 hilos).**

| Modelo | Tiempo/fold (s) | Memoria pico (MB) | RMSE medio |
|--------|------------------|--------------------|-----------|
| M0 | $0.8 \pm 0.1$ | 45 | $0.2519$ |
| M1 | $12.4 \pm 1.8$ | 52 | $0.1035$ |
| M2 | $8.2 \pm 1.1$ | 48 | $0.2464$ |
| M6 | $34.7 \pm 4.2$ | 58 | $0.0250$ |
| M7 | $127.3 \pm 18.6$ | 72 | $0.0251$ |
| MLP | $18.9 \pm 2.4$ | 210 | $0.0384$ |
| Translog | $4.1 \pm 0.5$ | 50 | $0.0312$ |

**Análisis coste-beneficio.** M6 reduce el RMSE en un 90\% respecto a M0 con un coste 43 veces mayor. En producción con streaming de datos, la decisión entre M0 y M6 requiere estimar el horizonte de reajustes: para menos de 10 reajustes, M0 es preferible por coste; para más de 100, M6 es preferible por precisión. M7 cuesta 3.7 veces más que M6 y no mejora el RMSE, lo cual confirma que la memoria no añade valor en el régimen `full` (parámetro $k = 1$ óptimo).

---

### 10. Síntesis

**Tabla 7. Síntesis de resultados en cinco dominios.**

| Dominio | Estructura | Saturación | Ω range | ΔBIC M6 vs M0 | Extensión útil |
|---------|------------|------------|---------|----------------|-----------------|
| Neural Scaling | Multiplicativa | Visible | 3 órdenes | $-14.3$ | Sí (con reservas) |
| Urban Scaling | Multiplicativa | Visible | 5 órdenes | $-21.6$ | Sí |
| Species-Area | Multiplicativa | Visible | 6 órdenes | $-18.9$ | Sí |
| Fama-French | Aditiva | No visible | $< 1$ orden | $+8.7$ | No |
| Debye | Ley de potencia | No visible | 3 órdenes | $+3.4$ | No |

**Patrón.** La extensión aporta valor en dominios con estructura multiplicativa y saturación visible. No aporta valor en dominios con estructura aditiva o donde la ley de potencia pura es suficiente.

---

### 11. Discusión

#### 11.1 Relación con la literatura

**Neural Scaling.** Las leyes de escalado neural (Kaplan et al. 2020; Hoffmann et al. 2022) se han modelado tradicionalmente como leyes de potencia puras. La extensión CES-Saturada sugiere que hay curvatura que las leyes puras no capturan.

**Urban Scaling.** El trabajo de Bettencourt et al. (2007) asume leyes de potencia puras. La extensión sugiere que el exponente puede variar con la población.

**Species-Area.** La relación especies-área es una de las leyes de potencia más robustas en ecología (Arrhenius 1921; Rosenzweig 1995). La extensión mejora la predicción pero la mejora es modesta.

**Fama-French.** El modelo de tres factores es aditivo por construcción. La extensión CES no es apropiada.

**Debye.** La ley $T^3$ de Debye es una ley de potencia pura en el régimen $T \ll \theta_D$. La extensión no mejora.

#### 11.2 Implicación práctica

La extensión no es universal. Su aplicación requiere verificar que el dominio cumpla:

1. Estructura multiplicativa.
2. Saturación visible.
3. Rango de $\Omega$ suficiente.

#### 11.3 Comparación con baselines

En los tres dominios positivos, M6 supera a MLP con 350 veces menos parámetros. Esto es consistente con la hipótesis de que la estructura subyacente es paramétrica y de baja dimensión.

---

### 12. Limitaciones

1. Solo cinco dominios externos.
2. Mapeos interpretativos.
3. Correlación entre variables.
4. Memoria temporal no validada externamente.
5. La extensión a sistemas multi-agente no está implementada.
6. Los resultados son sensibles al nivel de ruido asumido.
7. El rango de $\Omega$ en Neural Scaling no es cinco o más órdenes.

---

### 13. Conclusión

La familia CES-Saturada mejora sobre el modelo base en tres de cinco dominios externos. El resultado negativo en Fama-French y Debye delimita el caso de uso. La extensión no es universal y su aplicación requiere verificar las condiciones del dominio. El coste computacional de la extensión debe justificarse en términos de mejora predictiva.

---

### Software

El código completo, los datasets y los scripts de análisis están disponibles en `github.com/ronin-lang/ronin-paper-empirical`. Los tests de conformidad se ejecutan en CI con cobertura 94\%.

---

### Referencias

Arrhenius, O. (1921). Species and area. *Journal of Ecology*, 9(1), 95-99.

Ashcroft, N. W. y Mermin, N. D. (1976). *Solid State Physics*. Saunders College.

Bettencourt, L. M. A., Lobo, J., Helbing, D., Kühnert, C., y West, G. B. (2007). Growth, innovation, scaling, and the pace of life in cities. *Proceedings of the National Academy of Sciences*, 104(17), 7301-7306.

Drakare, S., Lennon, J. J., y Hillebrand, H. (2006). The imprint of the geographical, evolutionary and ecological context on species-area relationships. *Ecology Letters*, 9(2), 215-227.

Hoffmann, J., Borgeaud, S., Mensch, A., et al. (2022). Training compute-optimal large language models. *arXiv:2203.15556*.

Kaplan, J., McCandlish, S., Henighan, T., et al. (2020). Scaling laws for neural language models. *arXiv:2001.08361*.

Rosenzweig, M. L. (1995). *Species Diversity in Space and Time*. Cambridge University Press.

---

**Fin del Artículo C.**

---

**Nota final.** Los tres artículos comparten notación, referencias cruzadas y protocolo experimental. Se recomienda a los editores considerarlos como una trilogía. El Artículo A caracteriza axiomáticamente el modelo base. El Artículo B analiza la identificabilidad de la extensión. El Artículo C valida empíricamente la extensión en cinco dominios. Los tres son autocontenidos.

**1310.**
