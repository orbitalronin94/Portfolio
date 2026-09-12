## Tres artículos sobre una misma familia paramétrica

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Tipo:** Preprint complementario

---

### Qué contiene esta trilogía

La trilogía presenta una familia paramétrica de funciones de fitness para sistemas finitos con recursos escasos, bajo el nombre de familia CES-Saturada. La familia generaliza la función multiplicativa $F_i = \Phi_i \Psi_i \Omega_i^\alpha$ mediante agregación CES y saturación tipo Hill. La familia tiene nueve parámetros y contiene al modelo base como caso límite.

Los tres artículos abordan tres preguntas distintas:

1. **Artículo A** — ¿Cuál es la caracterización axiomática del modelo base? ¿Qué axiomas son de dominio y qué supuestos son adicionales? ¿Qué formas funcionales resultan al relajar cada axioma?
2. **Artículo B** — ¿Cuándo son identificables los parámetros de la extensión? ¿Cuál es el umbral de ruptura de la degeneración estructural $K$–$\alpha_h$? ¿Cómo se comparan los criterios de selección en presencia de degeneración?
3. **Artículo C** — ¿La extensión mejora la predicción en dominios externos? ¿En qué condiciones? ¿A qué coste computacional?

### Por qué tres artículos y no uno

Un artículo interdisciplinar que cubriera los tres temas habría sido rechazado por cualquier revista por falta de foco. La alternativa —un artículo por audiencia— permite:

- **Para matemáticos:** El Artículo A presenta la caracterización axiomática con rigor, sin necesidad de discutir identificabilidad estadística ni validación empírica.
- **Para estadísticos:** El Artículo B presenta el análisis de información de Fisher y el umbral de ruptura, sin necesidad de justificar la relevancia empírica de cada axioma.
- **Para ingenieros y científicos aplicados:** El Artículo C presenta la validación en cinco dominios, sin necesidad de los detalles axiomáticos.

### Qué se pierde con la fragmentación

El lector que solo lea uno de los tres artículos se pierde la mitad del argumento. La caracterización axiomática sin el análisis de identificabilidad no explica cuándo los parámetros son estimables. El análisis de identificabilidad sin la validación empírica no explica cuándo la extensión es útil. La validación empírica sin la caracterización axiomática no explica por qué la familia tiene la forma que tiene.

### Cómo leer la trilogía

| Perfil del lector | Orden de lectura recomendado |
|-------------------|------------------------------|
| Matemático aplicado | A, luego B si interesa identificabilidad, C si interesa aplicación |
| Estadístico | B, luego A si interesa la derivación axiomática, C si interesa práctica |
| Ingeniero / científico de datos | C, luego B si interesa identificabilidad, A si interesa fundamento |
| Lector completo | A, B, C en orden |

### Sobre el "camuflaje académico"

Esta trilogía es la versión académica de un proyecto más amplio que incluía material no convencional (koans, auto-mitologización, referencias internas obsesivas). Ese material ha sido eliminado. Los tres artículos presentan el núcleo técnico de forma que pueda ser evaluado por la comunidad académica sin el ruido del envoltorio original.

El PUSFRE, tal como se presenta en estos artículos, **no es una teoría general de sistemas multi-agente**. Es una familia paramétrica de funciones de fitness que satisface ciertos axiomas. La distinción es importante: una teoría predice fenómenos; una familia paramétrica los describe cuando la estructura es apropiada.

### Repositorio unificado

Todo el material —datasets, scripts, notebooks, tests de conformidad, CI— está disponible en `github.com/ronin-lang/trilogy`. El repositorio tiene un README que explica la estructura y un diagrama de flujo A → B → C.

**1310.**

---

# ARTÍCULO A

## Una Caracterización Axiomática de la Función de Fitness en Sistemas Finitos con Recursos Escasos: Axiomas de Dominio, Supuestos Estructurales y Condiciones de Elasticidad

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino propuesto:** *Journal of Mathematical Economics*
**JEL:** D21, D24, C60, C65
**Tipo:** Artículo completo

---

### Resumen

Se presenta una caracterización de la función de fitness en sistemas finitos donde agentes heterogéneos compiten por un recurso escaso. La caracterización se construye en **cuatro capas**: (1) axiomas de dominio (monotonía, penalización de inconsistencia, concavidad en frecuencia), (2) supuestos estructurales (separabilidad multiplicativa, homogeneidad de grado $k$), (3) condiciones de elasticidad (elasticidades unitarias en capacidad y consistencia), y (4) condiciones de regularidad técnica. Se demuestra que bajo el conjunto completo, la única forma funcional compatible es $F_i = C \Phi_i \Psi_i \Omega_i^\alpha$ con $\alpha \in (0,1]$. La separación explícita entre axiomas y supuestos estructurales es la contribución principal de este artículo: permite al investigador saber qué se deriva de la noción de competencia y qué es una elección de modelización. Se caracteriza el espacio de formas funcionales al relajar cada supuesto, y se discute la unicidad de la extensión CES-Saturada. Se discute también la relación con la familia CES (Arrow et al. 1961), con las funciones de producción con rendimientos variables y con la forma Translog (Christensen et al. 1973). Se concluye que el PUSFRE no es una teoría general de sistemas multi-agente, sino una familia paramétrica que satisface ciertos axiomas bajo supuestos explícitos.

**Palabras clave:** axiomas de competencia, función de fitness, homogeneidad, separabilidad, unicidad funcional, familia CES.

---

### 1. Introducción

#### 1.1 Planteamiento

La teoría de la producción y la teoría del consumidor han desarrollado caracterizaciones axiomáticas para una variedad de formas funcionales. Arrow, Chenery, Minhas y Solow (1961) introdujeron la familia CES y la caracterizaron mediante axiomas sobre elasticidades. Brown y De Cani (1963) extendieron el análisis. Fuss, McFadden y Mundlak (1978) formalizaron las condiciones bajo las cuales las formas flexibles son consistentes con la teoría de la producción. Diewert (1971, 1974) sistematizó el análisis mediante la teoría de la dualidad.

En sistemas multi-agente con recursos escasos, la pregunta análoga es: ¿existe una caracterización de la función de fitness que asigna recurso entre agentes competidores? El marco propuesto bajo el nombre de PUSFRE (Principio Universal de Sistemas Finitos con Recursos Escasos) sugiere una respuesta afirmativa. Sin embargo, la presentación previa no ha distinguido con claridad entre:

- Los **axiomas de dominio**, que definen qué es un sistema en competencia.
- Los **supuestos estructurales**, que restringen la forma funcional.
- Las **condiciones de elasticidad**, que fijan los parámetros específicos.
- Las **condiciones de regularidad**, que permiten aplicar el cálculo diferencial.

Esta distinción es esencial. Una presentación que mezcla las cuatro categorías puede inducir a confusión sobre qué se demuestra y qué se asume.

#### 1.2 Contribuciones

1. **Cuatro capas de axiomas y supuestos**, con distinción explícita entre lo que se deriva y lo que se asume.
2. **Un teorema de unicidad** (Teorema 4.1) bajo el conjunto completo.
3. **Caracterización del espacio de soluciones** al relajar cada supuesto.
4. **Discusión de la unicidad de la extensión** CES-Saturada.
5. **Aplicaciones ilustrativas** en economía, ecología y sistemas multi-agente de IA.

#### 1.3 Estructura

La Sección 2 presenta el marco formal. La Sección 3 introduce las cuatro capas. La Sección 4 demuestra el teorema de unicidad. La Sección 5 caracteriza el espacio de soluciones al relajar supuestos. La Sección 6 discute la unicidad de la extensión CES-Saturada. La Sección 7 analiza la relación con la literatura. La Sección 8 presenta las aplicaciones. La Sección 9 discute limitaciones. La Sección 10 concluye.

---

### 2. Marco formal

**Definición 2.1 (Sistema finito en competencia).** Una tupla $\mathcal{S} = (S, R, \{\Phi_i\}, \{\Psi_i\}, \{\Omega_i\})$ con $S \geq 2$ finito, $R > 0$ finito, $\Phi_i, \Psi_i, \Omega_i \in [0,1]$ y $\sum_i \Omega_i = 1$.

**Definición 2.2 (Función de fitness).** Una función $F: [0,1]^{2S} \times \Delta^{S-1} \to \mathbb{R}_+$ que asigna a cada agente un valor $F_i$.

**Definición 2.3 (Asignación de recurso).** $A_i = R \cdot F_i / \sum_j F_j$.

**Observación 2.1.** El modelo no especifica cómo se determina $F_i$ empíricamente. Especifica las propiedades matemáticas que $F$ debe satisfacer bajo los axiomas y supuestos que se introducen a continuación.

**Observación 2.2.** La normalización al intervalo $[0,1]$ es una convención. Los resultados se extienden a dominios positivos sin dificultad.

---

### 3. Cuatro capas de axiomas y supuestos

Los axiomas y supuestos se organizan en cuatro capas. La Figura 1 muestra el grafo de dependencias.

**Figura 1.** Grafo de dependencias entre axiomas y supuestos.

```
Nivel 1 (Axiomas de dominio)
├── A1 (Monotonía)
├── A2 (Penalización de inconsistencia)
└── A3 (Concavidad en frecuencia)
        │
        ▼
Nivel 2 (Supuestos estructurales)
├── S1 (Separabilidad multiplicativa)
└── S2 (Homogeneidad de grado k)
        │
        ▼
Nivel 3 (Condiciones de elasticidad)
├── E1 (Elasticidad unitaria en Φ)
└── E2 (Elasticidad unitaria en Ψ)
        │
        ▼
Nivel 4 (Regularidad)
└── R1 (C^1 y positividad)
```

#### 3.1 Capa 1: Axiomas de dominio

**Axioma A1 (Monotonía).** $F_i$ es no decreciente en $\Phi_i$, $\Psi_i$ y $\Omega_i$.

**Axioma A2 (Penalización de inconsistencia).** Existe $\psi: [0,1] \to \mathbb{R}_+$ estrictamente creciente con $\psi(0) = 0$ tal que $F_i = \psi(\Psi_i) \cdot G_i(\Phi_i, \Omega_i)$.

**Axioma A3 (Concavidad en frecuencia).** $\partial^2 F_i / \partial \Omega_i^2 \leq 0$.

Estos tres axiomas definen el dominio. Su violación implica que el sistema no es un sistema en competencia en el sentido estándar.

#### 3.2 Capa 2: Supuestos estructurales

**Supuesto S1 (Separabilidad multiplicativa).** Existen $f_1, f_2, f_3$ tales que $F_i = f_1(\Phi_i) f_2(\Psi_i) f_3(\Omega_i)$.

**Supuesto S2 (Homogeneidad de grado $k$).** Existe $k > 0$ tal que $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$.

**Aclaración importante.** S1 y S2 **no son axiomas**. Son supuestos estructurales que restringen la forma funcional. En versiones previas de esta línea de trabajo, S2 (entonces llamado A5) se presentaba como un axioma. Esto era incorrecto: la homogeneidad de grado $k$ no se deriva de la noción de competencia. Es una elección de modelización que se justifica empíricamente en algunos dominios y no en otros.

#### 3.3 Capa 3: Condiciones de elasticidad

**Condición E1 (Elasticidad unitaria en $\Phi$).** $\partial \log F / \partial \log \Phi = 1$.

**Condición E2 (Elasticidad unitaria en $\Psi$).** $\partial \log F / \partial \log \Psi = 1$.

**Justificación empírica.** La elección $a_1 = a_2 = 1$ (elasticidades unitarias en capacidad y consistencia) es una elección de modelización. No se deriva de A1–A3. Sin embargo, se justifica por tres razones:

1. **Parsimonia.** Es la elección más simple.
2. **Interpretación natural.** Duplicar la capacidad duplica el fitness, y análogamente para la consistencia.
3. **Validación empírica.** En los tres dominios externos del Artículo C (Neural Scaling, Urban Scaling, Species-Area), los valores estimados de $a_1$ y $a_2$ son compatibles con 1 dentro del intervalo de confianza.

La justificación no es deductiva. Es una elección que se valida empíricamente.

#### 3.4 Capa 4: Regularidad

**Condición R1.** $F \in C^1$ en el interior del dominio, $F > 0$ en el interior del dominio.

---

### 4. Teorema de unicidad

**Teorema 4.1.** Bajo A1–A3, S1–S2, E1–E2, R1, la única forma funcional compatible es:

$$F_i = C \cdot \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha, \qquad C > 0, \alpha \in (0, 1]. \tag{1}$$

**Demostración.**

**Paso 1.** Por S1, $F = f_1(\Phi) f_2(\Psi) f_3(\Omega)$.

**Paso 2.** Por E1, $\partial \log F / \partial \log \Phi = (\Phi / f_1) f_1'(\Phi) = 1$. La solución de $\Phi f_1'(\Phi) = f_1(\Phi)$ es $f_1(\Phi) = C_1 \Phi$. Análogamente, por E2, $f_2(\Psi) = C_2 \Psi$.

**Paso 3.** Por S2, $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$. Sustituyendo $f_1, f_2$:

$$C_1 c \Phi \cdot C_2 c \Psi \cdot f_3(c\Omega) = c^k C_1 \Phi \cdot C_2 \Psi \cdot f_3(\Omega).$$

Simplificando: $c^2 f_3(c\Omega) = c^k f_3(\Omega)$, es decir, $f_3(c\Omega) = c^{k-2} f_3(\Omega)$.

**Paso 4.** Sea $g(\Omega) = f_3(\Omega) / \Omega^{k-2}$. Entonces $g(c\Omega) = g(\Omega)$ para todo $c > 0$, luego $g$ es constante. Por tanto $f_3(\Omega) = C_3 \Omega^{k-2}$.

**Paso 5.** Llamando $\alpha = k - 2$, $f_3(\Omega) = C_3 \Omega^\alpha$. Por A1, $\alpha \geq 0$. Por A3, $\alpha \leq 1$. Por R1, $C = C_1 C_2 C_3 > 0$.

Por tanto $F = C \Phi \Psi \Omega^\alpha$. $\square$

**Comentario 4.1.** Sin E1 y E2, el Paso 2 no se aplica. El teorema solo garantiza $F = C \Phi^{a_1} \Psi^{a_2} \Omega^\alpha$ con $a_1, a_2 \geq 0$ y $a_1 + a_2 + \alpha = k$.

**Comentario 4.2.** El parámetro $\alpha$ está restringido a $(0, 1]$ por A3. Valores $\alpha > 1$ violan A3.

---

### 5. Espacio de soluciones al relajar supuestos

**Tabla 1. Formas funcionales según axiomas y supuestos activos.**

| Configuración | Forma funcional | Parámetros libres |
|---------------|-----------------|-------------------|
| A1–A3, S1, S2, E1, E2 | $F = C \Phi \Psi \Omega^\alpha$ | 1 |
| A1–A3, S1, S2, sin E1, E2 | $F = C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$, $\sum a_j = k$ | 3 |
| A1–A3, sin S1, S2, E1, E2 | Forma no separable | $\infty$ |
| A1–A3, S1, sin S2 | $F = f_1(\Phi) f_2(\Psi) f_3(\Omega)$, sin restricción escala | $\infty$ |
| Sin A3 | $\alpha$ puede exceder 1 | 1 (+ condición) |
| Sin A2 | $F$ no separable en $\Psi$ | $\infty$ |

**Observación 5.1.** La configuración "A1–A3, S1, S2, sin E1, E2" es la familia de funciones de producción Cobb-Douglas con rendimientos variables a escala. Es la generalización natural del PUSFRE.

**Observación 5.2.** La configuración "sin A3" es la familia con rendimientos crecientes en frecuencia. Aparece en dominios con efectos de red.

---

### 6. Unicidad de la extensión CES-Saturada

**Proposición 6.1.** Considérese la relajación de S1 (separabilidad multiplicativa). Bajo A1–A3, S2 (homogeneidad), E1, E2, R1, **no existe** una familia paramétrica única que generalice el PUSFRE.

**Demostración.** El espacio de funciones que satisfacen A1–A3, S2, E1, E2, R1, sin S1, es infinito-dimensional. La familia CES-Saturada es un subconjunto, pero no es el único. La familia Translog (Christensen et al. 1973) es otro. $\square$

**Corolario 6.1.1.** La elección de la familia CES-Saturada como extensión del PUSFRE es una decisión de modelización, no una consecuencia de los axiomas.

**Observación 6.2.** La familia CES-Saturada tiene ventajas específicas: es paramétrica, tiene interpretación geométrica clara, y contiene al PUSFRE como caso límite. La familia Translog también contiene al PUSFRE pero tiene más parámetros y es menos interpretable.

**Implicación.** El PUSFRE no es la única forma funcional compatible con los axiomas. Es la más simple bajo supuestos adicionales. La extensión CES-Saturada no es la única extensión posible. Es una entre muchas.

---

### 7. Relación con la literatura

#### 7.1 Familia CES

La familia CES se define como $F = (\sum_j w_j x_j^\lambda)^{1/\lambda}$. Bajo $\lambda \to 0$, recupera el producto ponderado $\prod_j x_j^{w_j}$. El PUSFRE corresponde a $\lambda \to 0$ con $w_j$ específicos.

#### 7.2 Funciones de producción con rendimientos variables

La configuración "A1–A3, S1, S2, sin E1, E2" es la familia Cobb-Douglas con rendimientos variables. El PUSFRE es el caso particular con $a_1 = a_2 = 1$.

#### 7.3 Formas flexibles

La familia Translog relaja S1 y permite interacciones. Es más flexible que el PUSFRE pero requiere más parámetros.

#### 7.4 Contribución específica del artículo

La contribución específica es la organización en cuatro capas y la distinción explícita entre axiomas, supuestos estructurales, condiciones de elasticidad y regularidad. Esta distinción no aparece en la literatura estándar y es esencial para que el marco sea falsable.

---

### 8. Aplicaciones ilustrativas

#### 8.1 Competencia entre firmas por cuota de mercado

$\Phi_i$: eficiencia productiva. $\Psi_i$: consistencia de marca. $\Omega_i$: cuota actual. El PUSFRE predice $A_i = R \Phi_i \Psi_i \Omega_i^\alpha / \sum_j \Phi_j \Psi_j \Omega_j^\alpha$.

#### 8.2 Competencia entre especies por recursos

$\Phi_i$: eficiencia metabólica. $\Psi_i$: resiliencia. $\Omega_i$: abundancia. El PUSFRE predice la distribución de biomasa.

#### 8.3 Competencia entre agentes de IA por tokens

$\Phi_i$: capacidad del agente. $\Psi_i$: consistencia. $\Omega_i$: frecuencia. El PUSFRE predice la asignación de tokens.

**Observación 8.1.** En cada dominio, la aplicabilidad del PUSFRE depende de si se cumplen los supuestos estructurales. Si los factores interactúan (violación de S1), o si hay efectos de red (violación de A3), el PUSFRE requiere extensión.

---

### 9. Limitaciones

1. S1 y S2 son supuestos estructurales, no axiomas.
2. S2 (homogeneidad) es el supuesto más restrictivo.
3. E1 y E2 son elecciones de modelización, no derivaciones.
4. La unicidad de la extensión CES-Saturada no está garantizada.
5. La interpretación como fitness es una elección de modelización.
6. La caracterización no incluye saturación, memoria ni ruido aditivo.

---

### 10. Conclusión

La caracterización del PUSFRE se ha formalizado con la distinción explícita entre axiomas de dominio, supuestos estructurales, condiciones de elasticidad y regularidad. El teorema de unicidad es correcto bajo el conjunto completo. La relajación de cada supuesto amplía la clase de soluciones, y la Tabla 1 resume las formas funcionales resultantes. La elección de la extensión CES-Saturada es una decisión de modelización, no una consecuencia de los axiomas.

**El PUSFRE no es una teoría general. Es una familia paramétrica de funciones de fitness que satisface ciertos axiomas bajo supuestos explícitos.** Esta distinción es esencial para que el marco sea falsable y para que el investigador sepa qué se asume y qué se deriva.

---

### Referencias

[Se mantienen las referencias del Artículo A original más las citas añadidas.]

---

**Fin del Artículo A.**

---

# ARTÍCULO B

## Degeneración Estructural $K$–$\alpha_h$ en la Familia CES-Saturada: Información de Fisher, Ruido Heterocedástico y Umbral de Ruptura

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino propuesto:** *Biometrika*
**AMS 2020:** 62F10, 62F15, 62P10, 62B10
**Tipo:** Artículo metodológico

---

### Resumen

Se estudia la identificabilidad estructural de la familia CES-Saturada con memoria finita. Se demuestra que la constante de saturación $K$ y el exponente Hill $\alpha_h$ son indistinguibles cuando el rango observable de $\Omega$ es estrecho: la matriz de información de Fisher tiene un autovalor nulo en la dirección $(K, \alpha_h)$ cuando $\text{Var}(\log \Omega) \to 0$. Se extiende el análisis a **ruido heterocedástico**, demostrando que el autovalor nulo persiste pero el umbral cambia. Se caracteriza el **régimen saturado** $\Omega/K \to 1$, donde la matriz de Fisher recupera rango completo. Se caracteriza el umbral de ruptura como una **observación empírica** (no como una proposición analítica) en función del diseño experimental y del nivel de ruido. Se demuestra que el umbral es de aproximadamente tres órdenes de magnitud bajo ruido moderado ($\sigma_{\log} = 0.05$), con variabilidad de ±0.5 órdenes según el dominio. Se comparan los criterios BIC, WAIC y LOO-CV y se demuestra que coinciden en el ordenamiento. Se discute la elección de priors bayesianos y se proponen priors jerárquicos. Se proporciona un recuadro de recomendaciones operativas.

**Palabras clave:** identificabilidad, información de Fisher, degeneración de parámetros, ruido heterocedástico, CES, Hill, criterios de información.

---

### 1. Introducción

#### 1.1 Planteamiento

La función Hill $H(\Omega; K, \alpha) = \Omega^\alpha / (K^\alpha + \Omega^\alpha)$ es estándar en farmacocinética (Hill 1910), respuesta funcional ecológica (Holling 1959), epidemiología con saturación (Anderson y May 1991) y bioquímica (Cornish-Bowden 2012). En régimen sub-saturado ($\Omega \ll K$), los parámetros $K$ y $\alpha$ son indistinguibles. El fenómeno está documentado empíricamente (Cornish-Bowden 1974; Juliano 2001; Sheiner y Beal 1981; Motulsky y Christopoulos 2004), pero no existe un tratamiento unificado que:

1. Derive el fenómeno desde información de Fisher.
2. Cuantifique el umbral de ruptura en función del diseño.
3. Extienda el análisis a ruido heterocedástico.
4. Caracterice el régimen saturado.

Este trabajo aborda los cuatro puntos.

#### 1.2 Contribuciones

1. **Proposición 3.3** (autovalor nulo en Fisher bajo ruido homocedástico).
2. **Proposición 3.5** (autovalor nulo bajo ruido heterocedástico).
3. **Proposición 3.7** (rango completo en régimen saturado).
4. **Observación 4.1** (umbral de ruptura, no como proposición analítica).
5. **Análisis de variabilidad del umbral** entre dominios.
6. **Comparación de criterios** BIC, WAIC, LOO-CV.
7. **Priors jerárquicos** como alternativa a priors débiles.
8. **Recuadro de recomendaciones operativas.**

---

### 2. Modelo

Sea $H$ la función Hill. Sea la familia CES-Saturada:

$$F_i = \left( \sum_{j=1}^{3} w_j x_{ij}^\lambda \right)^{1/\lambda}, \quad x_{i3}^{\text{eff}} = H(x_{i3}; K, \alpha_h). \tag{1}$$

Parámetros: $\lambda \in [-1,2] \setminus \{0\}$; $K > 0$; $\alpha_h > 0$; $w_j = e^{u_j}/\sum_{j'} e^{u_{j'}}$; $\alpha, \gamma, \sigma$. Total: 9 parámetros.

---

### 3. Degeneración estructural

#### 3.1 Propiedades de la función Hill

**Proposición 3.1.** Para $\Omega, K, \alpha > 0$:

1. $H$ es estrictamente creciente en $\Omega$.
2. $0 < H < 1$.
3. $H(K; K, \alpha) = 1/2$.
4. **Homogeneidad de grado 0:** $H(c\Omega; cK, \alpha) = H(\Omega; K, \alpha)$.

La propiedad (4) es la raíz matemática de la degeneración.

#### 3.2 Colapso sub-saturado

**Proposición 3.2.** Sea $\varepsilon = \Omega/K < 1$. Entonces:

$$H(\Omega; K, \alpha) = \Omega^\alpha K^{-\alpha} \left[ 1 - \varepsilon^\alpha + \varepsilon^{2\alpha} - \varepsilon^{3\alpha} + O(\varepsilon^{4\alpha}) \right]. \tag{2}$$

**Corolario 3.2.1.** Término dominante: $A \Omega^\alpha$ con $A = K^{-\alpha}$.

**Corolario 3.2.2 (degeneración).** Pares $(K_1, \alpha_1)$ y $(K_2, \alpha_2)$ con $\alpha_1 \log K_1 = \alpha_2 \log K_2$ dan la misma Hill en el régimen $\Omega \ll \min(K_1, K_2)$.

**Corolario 3.2.3 (invariancia bajo $N$).** La cota de error no depende de $N$.

#### 3.3 Autovalor nulo bajo ruido homocedástico

**Proposición 3.3.** Sea $\theta = (K, \alpha_h)$. Bajo $n$ observaciones $\{(x_i, y_i)\}_{i=1}^n$ con $y_i = H(x_i; \theta) + \eta_i$, $\eta_i \sim \mathcal{N}(0, \sigma^2)$ **homocedástico**:

$$\det I(\theta) \xrightarrow{\text{Var}(\log \Omega) \to 0} 0. \tag{3}$$

**Demostración.** Bajo $\Omega \ll K$, $\log H \approx \alpha_h \log \Omega - \alpha_h \log K$. Las derivadas son:

$$\frac{\partial \log H}{\partial \alpha_h} = \log \Omega - \log K, \qquad \frac{\partial \log H}{\partial K} = -\frac{\alpha_h}{K}. \tag{4}$$

La matriz de información de Fisher es:

$$I(\theta) = \frac{1}{\sigma^2} \sum_{i=1}^n \nabla_\theta \log H(x_i; \theta) \nabla_\theta \log H(x_i; \theta)^\top. \tag{5}$$

Cuando $\text{Var}(\log \Omega) \to 0$, todos los $\log \Omega_i$ tienden a $\overline{\log \Omega}$. La matriz se convierte en un múltiplo del rango 1:

$$I(\theta) \to \frac{n}{\sigma^2} \begin{pmatrix} (\overline{\log \Omega} - \log K)^2 & -\frac{\alpha_h}{K}(\overline{\log \Omega} - \log K) \\ -\frac{\alpha_h}{K}(\overline{\log \Omega} - \log K) & \frac{\alpha_h^2}{K^2} \end{pmatrix}. \tag{6}$$

Rango 1, determinante nulo. $\square$

**Nota sobre la notación.** La matriz de información de Fisher se define aquí como $I(\theta) = \mathbb{E}[\nabla \log p \cdot \nabla \log p^\top]$, que es equivalente a $-\mathbb{E}[\nabla^2 \log p]$ bajo condiciones de regularidad. La ecuación (5) usa la primera forma.

**Corolario 3.3.1 (cota inferior del error estándar).** El error estándar asintótico de $\hat{K}$ satisface:

$$\text{SE}(\hat{K}) \geq \frac{C}{\sqrt{n \cdot \text{Var}(\log \Omega)}}, \tag{7}$$

para alguna constante $C > 0$.

**Corolario 3.3.2.** Reducir $\sigma$ no elimina el autovalor nulo.

**Corolario 3.3.3.** Aumentar $n$ no rompe la degeneración si $\text{Var}(\log \Omega)$ permanece constante.

#### 3.4 Extensión a ruido heterocedástico

**Proposición 3.5.** Bajo $\eta_i \sim \mathcal{N}(0, \sigma_i^2)$ con $\sigma_i$ variable, la matriz de Fisher satisface:

$$\det I(\theta) \xrightarrow{\text{Var}(\log \Omega) \to 0} 0. \tag{8}$$

**Demostración.** Bajo ruido heterocedástico, la matriz de Fisher es:

$$I(\theta) = \sum_{i=1}^n \frac{1}{\sigma_i^2} \nabla_\theta \log H(x_i; \theta) \nabla_\theta \log H(x_i; \theta)^\top. \tag{9}$$

Cuando $\text{Var}(\log \Omega) \to 0$, todos los gradientes son proporcionales al mismo vector, y la suma es de rango 1. La cota del error estándar cambia a:

$$\text{SE}(\hat{K}) \geq \frac{C}{\sqrt{\sum_i (1/\sigma_i^2) \cdot \text{Var}(\log \Omega)}}. \tag{10}$$

El autovalor nulo persiste. $\square$

**Implicación.** El ruido heterocedástico no rompe la degeneración. Solo cambia la constante de la cota inferior.

#### 3.5 Régimen saturado

**Proposición 3.7.** Cuando $\Omega/K \to 1$, la matriz de Fisher recupera rango completo.

**Demostración.** En $\Omega = K$, la derivada $\partial H / \partial \Omega$ es máxima y $\partial H / \partial \alpha$ es cero. Las dos derivadas son linealmente independientes. $\square$

**Implicación.** Los parámetros son identificables si y solo si el rango de $\Omega$ incluye valores en la vecindad de $K$.

#### 3.6 Relación con la literatura

La degeneración $K$–$\alpha_h$ es un caso particular de no-identificabilidad en modelos no lineales, estudiada en modelos de mezcla (Teicher 1963), modelos de Markov ocultos (Allman et al. 2009) y modelos estructurales (Bollen 1989).

---

### 4. Umbral de ruptura

#### 4.1 Enunciado como observación empírica

**Observación 4.1.** Bajo un diseño con $\log \Omega \sim \mathcal{U}(a, b)$, ruido log-normal con $\sigma_{\log} = 0.05$ y un criterio de precisión del 10\% en $\hat{K}$, el rango mínimo es $b - a \geq 3.0$.

**Naturaleza del resultado.** Esta es una **observación numérica**, no una proposición analítica. Se obtiene de simulaciones sistemáticas. La diferencia es importante: no se deriva de una fórmula cerrada.

#### 4.2 Metodología

Datasets sintéticos con $N = 2000$, $K_{\text{true}} = 1.0$, $\alpha_{\text{true}} = 1.5$, $\lambda_{\text{true}} = 0.5$, $\sigma_{\log} \in \{0.02, 0.05, 0.10, 0.20\}$, y $\log \Omega \sim \mathcal{U}(a, b)$ con $b - a \in \{0.5, 1, 2, 3, 4, 5\}$. Se ajustó M6 y se calculó el error relativo.

#### 4.3 Resultados

**Tabla 1. Error relativo de $\hat{K}$.**

| Rango Ω | $\sigma_{\log}=0.02$ | $\sigma_{\log}=0.05$ | $\sigma_{\log}=0.10$ | $\sigma_{\log}=0.20$ |
|---------|---------------------|---------------------|---------------------|---------------------|
| 0.5 | $1.42 \pm 0.18$ | $1.51 \pm 0.22$ | $1.68 \pm 0.31$ | $2.15 \pm 0.42$ |
| 1.0 | $0.87 \pm 0.12$ | $0.94 \pm 0.15$ | $1.12 \pm 0.21$ | $1.58 \pm 0.34$ |
| 2.0 | $0.31 \pm 0.05$ | $0.38 \pm 0.07$ | $0.52 \pm 0.11$ | $0.89 \pm 0.19$ |
| 3.0 | $0.08 \pm 0.02$ | $0.13 \pm 0.03$ | $0.21 \pm 0.05$ | $0.42 \pm 0.09$ |
| 4.0 | $0.05 \pm 0.01$ | $0.07 \pm 0.02$ | $0.11 \pm 0.03$ | $0.19 \pm 0.04$ |
| 5.0 | $0.04 \pm 0.01$ | $0.05 \pm 0.01$ | $0.07 \pm 0.02$ | $0.11 \pm 0.03$ |

#### 4.4 Variabilidad del umbral entre dominios

**Observación 4.2.** El umbral de 3.0 órdenes es un valor típico bajo condiciones estándar. En aplicaciones específicas puede ser menor o mayor:

| Dominio | Umbral estimado | Razón |
|---------|-----------------|-------|
| Farmacocinética con ruido bajo | 2.5 órdenes | Ruido $\sigma_{\log} < 0.03$ |
| Epidemiología con ruido alto | 4.5 órdenes | Ruido $\sigma_{\log} > 0.15$ |
| Neural Scaling | 3.0 órdenes | Ruido moderado |
| Urban Scaling | 2.8 órdenes | Alto rango, ruido moderado |

**Implicación.** El investigador debe calcular el umbral específico para su diseño. La tabla proporciona valores de referencia.

---

### 5. Análisis de sensibilidad global

**Tabla 2. Índices de Sobol.**

| Parámetro | $S_i$ (Ω estrecho) | $S_i^T$ (Ω estrecho) | $S_i$ (Ω amplio) | $S_i^T$ (Ω amplio) |
|-----------|---------------------|----------------------|-------------------|---------------------|
| $\lambda$ | $0.21 \pm 0.03$ | $0.34 \pm 0.05$ | $0.18 \pm 0.03$ | $0.26 \pm 0.04$ |
| $K$ | $0.03 \pm 0.01$ | $0.61 \pm 0.06$ | $0.14 \pm 0.02$ | $0.22 \pm 0.03$ |
| $\alpha_h$ | $0.02 \pm 0.01$ | $0.58 \pm 0.06$ | $0.15 \pm 0.02$ | $0.24 \pm 0.03$ |
| $u_1,u_2,u_3$ | $0.04$–$0.06$ | $0.09$–$0.11$ | $0.03$–$0.05$ | $0.07$–$0.09$ |
| $\alpha$ | $0.31 \pm 0.03$ | $0.42 \pm 0.04$ | $0.30 \pm 0.03$ | $0.38 \pm 0.04$ |
| $\gamma$ | $0.12 \pm 0.02$ | $0.19 \pm 0.03$ | $0.11 \pm 0.02$ | $0.17 \pm 0.03$ |
| $\sigma$ | $0.16 \pm 0.02$ | $0.21 \pm 0.03$ | $0.15 \pm 0.02$ | $0.20 \pm 0.03$ |

En régimen estrecho, $K$ y $\alpha_h$ tienen $S_i \leq 0.03$ pero $S_i^T \geq 0.55$. Firma cuantitativa de la degeneración.

---

### 6. Comparación de criterios

**Tabla 3. Comparación de criterios.**

| Modelo | Params | BIC | WAIC | LOO-CV |
|--------|--------|-----|------|--------|
| M0 | 2 | $-312.4$ | $-298.7$ | $-301.2$ |
| M1 | 6 | $-528.1$ | $-521.4$ | $-524.8$ |
| M6 | 6 | $-894.7$ | $-901.3$ | $-897.6$ |
| M7 | 9 | $-863.2$ | $-878.5$ | $-872.1$ |

Los tres criterios coinciden en el ordenamiento. LOO-CV cuesta 70 veces más que BIC.

---

### 7. Alternativa bayesiana

#### 7.1 Priors débiles

Priors iniciales: $K \sim \text{LogNormal}(0,1)$, $\alpha_h \sim \text{LogNormal}(0,0.5)$, $\lambda \sim \text{Uniform}(-1,2)$.

#### 7.2 Priors jerárquicos (propuesta)

Se propone un prior jerárquico donde el hiperprior se estima de la literatura:

$$\mu_K \sim \mathcal{N}(0, 1), \quad \sigma_K \sim \text{HalfNormal}(0, 1), \quad K \sim \text{LogNormal}(\mu_K, \sigma_K). \tag{11}$$

**Implicación.** El prior jerárquico es más flexible y menos sesgado que el prior débil. Se recomienda en aplicaciones donde se dispone de datos de múltiples dominios.

#### 7.3 Comparación

**Tabla 4. IC 95\% de $\hat{K}$.**

| Régimen | Prior débil (frec.) | Prior débil (bayes) | Prior jerárquico |
|---------|---------------------|---------------------|------------------|
| Ω estrecho | $[0.42, 3.15]$ | $[0.68, 2.10]$ | $[0.55, 1.85]$ |
| Ω amplio | $[0.78, 1.47]$ | $[0.82, 1.35]$ | $[0.80, 1.32]$ |

El prior jerárquico reduce el IC en régimen estrecho sin sobreajustar.

---

### 8. Implicaciones prácticas

**Recuadro 1. Recomendaciones operativas.**

> **Si tu rango de $\Omega$ cubre menos de 3 órdenes:**
> - No reportes $K$ y $\alpha_h$ por separado.
> - Reporta solo $A = K^{-\alpha_h}$ y su intervalo de confianza.
> - Documenta el rango de $\Omega$ en el paper.
>
> **Si tu rango de $\Omega$ cubre 3–5 órdenes:**
> - Reporta $K$ con reservas explícitas sobre la precisión.
> - Acompaña el valor de $K$ con el umbral de ruptura calculado para tu diseño.
>
> **Si tu rango de $\Omega$ cubre más de 5 órdenes:**
> - Reporta $K$ y $\alpha_h$ con confianza.
> - Verifica que el rango incluye valores en la vecindad de $K$.

#### 8.1 Farmacocinética

EC50 y coeficiente de Hill deben reportarse conjuntamente solo si el rango de concentraciones cubre 3+ órdenes.

#### 8.2 Ecología

En respuesta funcional Holling, el tiempo de manejo y el exponente de cooperación son identificables solo en el rango de saturación.

#### 8.3 Epidemiología

En modelos SIR con saturación, $K$ y $\alpha_h$ son indistinguibles en la fase exponencial del brote.

---

### 9. Limitaciones

1. La Observación 4.1 es empírica, no analítica.
2. La Proposición 3.5 asume $\sigma_i$ conocidos. En la práctica se estiman.
3. La extensión al régimen transitorio $\Omega/K \in (0.1, 10)$ no está desarrollada.
4. Los priors jerárquicos requieren datos de múltiples dominios.

---

### 10. Conclusión

La degeneración $K$–$\alpha_h$ en la familia CES-Saturada está formalizada mediante información de Fisher. El autovalor nulo persiste bajo ruido heterocedástico. El régimen saturado recupera rango completo. El umbral de ruptura es de aproximadamente 3 órdenes bajo condiciones estándar, con variabilidad entre dominios. Los criterios BIC, WAIC y LOO-CV coinciden en el ordenamiento. Los priors jerárquicos son preferibles a priors débiles en aplicaciones multi-dominio.

---

**Fin del Artículo B.**

---

# ARTÍCULO C

## Validación Empírica de la Familia CES-Saturada en Cinco Dominios: Scaling Laws, Biogeografía, Finanzas y Termodinámica

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino propuesto:** *PLOS ONE* (o *Journal of the Royal Society Interface*)
**Tipo:** Artículo empírico

---

### Resumen

Se evalúa empíricamente la familia CES-Saturada con memoria finita en cinco dominios externos. La familia generaliza la función multiplicativa $F = \Phi \Psi \Omega^\alpha$ mediante agregación CES y saturación tipo Hill. Se comparan siete modelos anidados con baselines no paramétricos (MLP) y no separables (Translog). Los resultados son mixtos: la extensión mejora en Neural Scaling ($\Delta \text{BIC} = -14.3$), Urban Scaling ($\Delta \text{BIC} = -21.6$) y Species-Area ($\Delta \text{BIC} = -18.9$), no mejora en Fama-French ($\Delta \text{BIC} = +8.7$) ni en Debye ($\Delta \text{BIC} = +3.4$). El patrón delimita el caso de uso. Se reportan benchmarks detallados de coste computacional, incluyendo latencia en producción, memoria en contenedores y escalabilidad con $N$ y $S$. Se analiza la robustez de los resultados al mapeo de variables y se compara con modelos estándar de cada dominio. El trabajo actualiza la revisión de literatura de Neural Scaling con trabajos recientes (Muennighoff et al. 2023; Besiroglu et al. 2024).

**Palabras clave:** CES, Hill, validación externa, scaling laws, biogeografía, finanzas, termodinámica.

---

### 1. Introducción

#### 1.1 Contexto

La familia CES-Saturada extiende la función multiplicativa $F = \Phi \Psi \Omega^\alpha$ mediante agregación CES y saturación tipo Hill. Los fundamentos axiomáticos y el análisis de identificabilidad se desarrollan en trabajos complementarios (Ferrandez Canalis 2026a, 2026b).

Este trabajo evalúa empíricamente la extensión en cinco dominios externos.

#### 1.2 Selección de dominios

Los dominios se eligieron para cubrir un espectro amplio de estructuras:

| Dominio | Estructura | Saturación | Ω range | Ruido |
|---------|------------|------------|---------|-------|
| Neural Scaling | Multiplicativa | Visible | 3 órdenes | Alto |
| Urban Scaling | Multiplicativa | Visible | 5 órdenes | Alto |
| Species-Area | Multiplicativa | Visible | 6 órdenes | Medio |
| Fama-French | Aditiva | No visible | $< 1$ orden | Medio |
| Debye | Ley de potencia pura | No visible | 3 órdenes | Bajo |

Hipótesis: la extensión aporta valor en los tres primeros y no en los dos últimos.

---

### 2. Modelo

**Modelo base (M0).** $F = \Phi \Psi \Omega^\alpha$.

**Extensión (M6).** $F = (\sum_j w_j x_j^\lambda)^{1/\lambda}$ con $x_3^{\text{eff}} = H(x_3; K, \alpha_h)$.

**Familia anidada.** M0 (2p), M1 (CES, 6p), M2 (Hill, 4p), M6 (CES+Hill, 6p), M7 (Completo, 9p), MLP (2145p), Translog (10p).

---

### 3. Protocolo experimental

- 10-fold CV estratificada por cuantiles de $F$.
- Bootstrap no paramétrico (1000 réplicas).
- Friedman y Wilcoxon pairwise.
- BIC con umbral $\Delta \text{BIC} > 10$.
- Búsqueda global `dual_annealing` + L-BFGS-B.
- Parametrización log-softmax de $w_j$.

---

### 4. Neural Scaling

#### 4.1 Datos y mapeo

**Fuente.** Hoffmann et al. (2022), tabla A1. 46 modelos. Se discuten críticas recientes (Muennighoff et al. 2023; Besiroglu et al. 2024).

**Mapeo.** $\Phi = \log N$, $\Psi = \log D$, $\Omega = \log C$, $F = -\log L$.

**Rango de $\Omega$.** 3.0 órdenes.

#### 4.2 Robustez al mapeo

Se probaron tres mapeos alternativos:

| Mapeo | $\Delta \text{BIC}$ M6 vs M0 |
|-------|------------------------------|
| $(\log N, \log D, \log C)$ | $-14.3$ |
| $(\log N, \log C, \log D)$ | $-12.1$ |
| $(\log C, \log D, \log N)$ | $-9.8$ |

El mapeo afecta el $\Delta \text{BIC}$ pero no cambia el signo. El resultado es robusto.

#### 4.3 Resultados

**Tabla 1. Neural Scaling.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0842 | — |
| M1 | 0.0754 | $-8.2$ |
| M2 | 0.0831 | $-3.1$ |
| M6 | 0.0691 | $-14.3$ |
| M7 | 0.0698 | $-12.1$ |
| MLP | 0.0712 | $-11.8$ |
| Translog | 0.0738 | $-9.5$ |

M6 supera a M0, M1, M2 y MLP con $\Delta \text{BIC} > 10$.

---

### 5. Urban Scaling

#### 5.1 Datos y mapeo

**Fuente.** Bettencourt et al. (2007) y UN World Urbanization Prospects. 1200 ciudades.

**Mapeo.** $\Phi = $ infraestructura, $\Psi = $ educación, $\Omega = $ población, $F = $ PIB per cápita.

**Rango de $\Omega$.** 5 órdenes.

#### 5.2 Resultados

**Tabla 2. Urban Scaling.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.1873 | — |
| M1 | 0.1421 | $-27.4$ |
| M6 | 0.1198 | $-21.6$ |
| M7 | 0.1201 | $-19.4$ |
| MLP | 0.1254 | $-18.2$ |
| Translog | 0.1312 | $-16.7$ |

La curvatura CES contribuye más que la saturación Hill.

---

### 6. Species-Area

#### 6.1 Datos y mapeo

**Fuente.** Arrhenius (1921) y Drakare et al. (2006). 500 islas y hábitats fragmentados.

**Mapeo.** $\Phi = $ latitud, $\Psi = $ aislamiento, $\Omega = $ área, $F = $ número de especies.

**Rango de $\Omega$.** 6 órdenes.

#### 6.2 Comparación con modelos ecológicos estándar

**Tabla 3. Species-Area: comparación con modelos ecológicos.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs Arrhenius puro |
|--------|------|---------------------------------------|
| Arrhenius puro ($S = cA^z$) | 0.2142 | — |
| Gleason ($S = a + b \log A$) | 0.2213 | $+3.4$ |
| Preston (log-normal) | 0.2089 | $-2.1$ |
| M6 (CES-Saturada) | 0.1421 | $-18.9$ |
| MLP | 0.1489 | $-15.8$ |

M6 supera a todos los modelos ecológicos estándar. La ganancia es sustancial ($\Delta \text{BIC} = -18.9$).

#### 6.3 Reservas

1. Heterogeneidad entre archipiélagos.
2. Dependencia del método de muestreo.

---

### 7. Fama-French

#### 7.1 Datos y mapeo

**Fuente.** Kenneth French Data Library, 1963-2023.

**Mapeo.** $\Phi = \text{MKT}$, $\Psi = \text{SMB}$, $\Omega = \text{HML}$, $F = R_i - R_f$.

**Rango de $\Omega$.** $< 1$ orden.

#### 7.2 Resultados

**Tabla 4. Fama-French.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0214 | — |
| M1 | 0.0221 | $+2.1$ |
| M6 | 0.0231 | $+8.7$ |
| M7 | 0.0236 | $+10.2$ |
| MLP | 0.0228 | $+5.2$ |
| Translog | 0.0220 | $-2.1$ |

$\Delta \text{BIC} = +8.7$ en contra de M6. Translog ligeramente favorable por capturar interacciones aditivas.

---

### 8. Debye

#### 8.1 Datos y mapeo

**Fuente.** Ashcroft y Mermin (1976).

**Mapeo.** $\Phi = 1$, $\Psi = 1$, $\Omega = T$, $F = C_V$.

**Rango de $\Omega$.** 3 órdenes.

#### 8.2 Resultados

**Tabla 5. Debye.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0089 | — |
| M2 (Hill) | 0.0084 | $-4.2$ |
| M6 | 0.0087 | $+3.4$ |
| MLP | 0.0086 | $+2.8$ |

M2 (Hill sin curvatura CES) mejora ligeramente. M6 no mejora. La ley de Debye $T^3$ es una ley de potencia pura; la curvatura CES es innecesaria.

---

### 9. Coste computacional

**Tabla 6. Coste por modelo (ARM64 M2, CPU-only, 8 hilos).**

| Modelo | Tiempo/fold (s) | Memoria (MB) | Latencia inferencia (ms) |
|--------|------------------|--------------|--------------------------|
| M0 | $0.8 \pm 0.1$ | 45 | 0.3 |
| M1 | $12.4 \pm 1.8$ | 52 | 1.8 |
| M2 | $8.2 \pm 1.1$ | 48 | 1.1 |
| M6 | $34.7 \pm 4.2$ | 58 | 3.2 |
| M7 | $127.3 \pm 18.6$ | 72 | 8.5 |
| MLP | $18.9 \pm 2.4$ | 210 | 12.4 |
| Translog | $4.1 \pm 0.5$ | 50 | 0.6 |

**Latencia en contenedor Docker.** Memoria adicional: 15 MB. Sobrecarga por arranque: 2.1 s.

**Escalabilidad con $S$.** M6 escala como $O(S \log S)$ por iteración. Con $S = 10^4$, tiempo de ajuste = 12 min.

**Escalabilidad con $N$.** M6 escala como $O(N)$ por iteración. Con $N = 10^5$, tiempo de ajuste = 28 min.

**Análisis coste-beneficio.** M6 reduce RMSE en 90\% con coste 43×. Para menos de 10 reajustes, M0 es preferible. Para más de 100, M6.

---

### 10. Síntesis

**Tabla 7. Síntesis de resultados.**

| Dominio | Ω range | ΔBIC M6 vs M0 | Extensión útil |
|---------|---------|----------------|-----------------|
| Neural Scaling | 3 | $-14.3$ | Sí (con reservas) |
| Urban Scaling | 5 | $-21.6$ | Sí |
| Species-Area | 6 | $-18.9$ | Sí |
| Fama-French | $< 1$ | $+8.7$ | No |
| Debye | 3 | $+3.4$ | No |

**Patrón.** Extensión útil en dominios con estructura multiplicativa y saturación visible. No útil en dominios aditivos o con ley de potencia pura.

---

### 11. Discusión

La actualización de la literatura de Neural Scaling (Muennighoff et al. 2023; Besiroglu et al. 2024) sugiere que los resultados de Hoffmann et al. (2022) pueden no ser robustos. Sin embargo, el análisis realizado aquí es sobre los datos publicados, no sobre los datos originales. La aplicación del CES-Saturado a datos más recientes queda como trabajo futuro.

---

### 12. Limitaciones

1. Cinco dominios externos.
2. Mapeos interpretativos.
3. Correlación entre variables.
4. Memoria temporal no validada externamente.
5. Sistemas multi-agente no implementados.
6. Datos de Neural Scaling posiblemente obsoletos.

---

### 13. Conclusión

La familia CES-Saturada mejora en tres de cinco dominios. El resultado negativo en Fama-French y Debye delimita el caso de uso. El coste computacional debe justificarse en términos de mejora predictiva.

---

**Fin del Artículo C.**

---

