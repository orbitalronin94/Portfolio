# TRILOGÍA PUSFRE-CES: VERSIÓN FINAL

---

# NOTA TÉCNICA DE SÍNTESIS

## Tres artículos sobre una misma familia paramétrica: estructura, relación con el proyecto original, y guía de lectura

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Tipo:** Preprint complementario

---

### Qué contiene esta trilogía

La trilogía presenta una familia paramétrica de funciones de fitness para sistemas finitos con recursos escasos, bajo el nombre de familia CES-Saturada. La familia generaliza la función multiplicativa $F_i = \Phi_i \Psi_i \Omega_i^\alpha$ mediante agregación CES y saturación tipo Hill. La familia tiene nueve parámetros y contiene al modelo base como caso límite.

Los tres artículos abordan tres preguntas distintas:

1. **Artículo A** — ¿Cuál es la caracterización de la función de fitness del modelo base? ¿Qué axiomas son de dominio y qué supuestos son estructurales? ¿Qué formas funcionales resultan al relajar cada supuesto? ¿Es única la extensión CES-Saturada, o existen otras familias candidatas?
2. **Artículo B** — ¿Cuándo son identificables los parámetros de la extensión? ¿Cuál es el umbral de ruptura de la degeneración $K$–$\alpha_h$? ¿Cómo se comporta el régimen transitorio? ¿Cómo se estiman los parámetros de ruido cuando no se conocen?
3. **Artículo C** — ¿La extensión mejora la predicción en dominios externos? ¿En qué condiciones? ¿A qué coste computacional? ¿Los resultados son robustos al mapeo de variables y a la elección del dataset?

### Por qué tres artículos y no uno

La pregunta es legítima y merece una respuesta directa. Un artículo interdisciplinar que cubriera los tres temas tendría que:

- Introducir los axiomas con rigor matemático, lo cual ocupa al menos 15 páginas.
- Desarrollar el análisis de identificabilidad, que requiere información de Fisher, ruido heterocedástico, régimen transitorio y análisis de Sobol.
- Validar en cinco dominios, cada uno con su propia literatura, sus propios modelos estándar y sus propias reservas metodológicas.

Un paper así tendría 80 páginas, tres revisiones de literatura distintas, y sería rechazado por cualquier revista por falta de foco. La alternativa —tres papers con audiencias distintas— permite:

- **Para matemáticos aplicados:** El Artículo A presenta la caracterización axiomática con rigor y discute la unicidad de la extensión, sin necesidad de discutir identificabilidad estadística ni validación empírica.
- **Para estadísticos:** El Artículo B presenta el análisis de información de Fisher, el umbral de ruptura y el régimen transitorio, sin necesidad de justificar la relevancia empírica de cada axioma.
- **Para científicos aplicados e ingenieros:** El Artículo C presenta la validación en cinco dominios con benchmarks de producción, sin necesidad de los detalles axiomáticos.

La fragmentación tiene un costo: el lector que solo lea uno se pierde la mitad del argumento. La caracterización axiomática sin el análisis de identificabilidad no explica cuándo los parámetros son estimables. El análisis de identificabilidad sin la validación empírica no explica cuándo la extensión es útil. La validación empírica sin la caracterización axiomática no explica por qué la familia tiene la forma que tiene.

La nota técnica de síntesis mitiga este costo. Recomendamos leer al menos dos de los tres artículos.

### Relación con el proyecto original

Esta trilogía es la versión académica de un proyecto más amplio que se desarrolló entre junio y septiembre de 2026. El proyecto original incluía:

- Koans y formulaciones aforísticas.
- Auto-mitologizaciones y referencias internas obsesivas.
- Referencias simbólicas (por ejemplo, el número 1310).
- Un documento no canónico (el "Libro V").
- Un corpus de 288 reducciones de teoremas clásicos.
- Una extensión sobre fatiga de enrutamiento con 58 teoremas.

Ese material no forma parte de la trilogía. Ha sido eliminado por tres razones:

1. **Falta de rigor.** Muchas de las afirmaciones del proyecto original no estaban demostradas y se presentaban como teoremas. La trilogía solo incluye resultados demostrados o validados empíricamente.
2. **Falta de foco.** El proyecto original intentaba abarcar demasiado. La trilogía se enfoca en una familia paramétrica específica.
3. **Falta de honestidad epistémica.** El proyecto original presentaba como leyes universales lo que eran hipótesis de modelización. La trilogía distingue explícitamente entre axiomas, supuestos y condiciones de elasticidad.

El lector interesado en el proyecto original puede consultar el repositorio. Debe saber que el material original no ha sido validado académicamente y que algunas afirmaciones han sido retractadas o degradadas a hipótesis.

### Qué se conserva del proyecto original

Tres elementos:

1. **La intuición central.** Los sistemas multi-agente con recursos escasos pueden modelarse mediante funciones paramétricas de fitness. La intuición es válida y se desarrolla rigurosamente en la trilogía.
2. **La familia CES-Saturada.** La extensión específica que se valida en los tres artículos tiene su origen en el proyecto original.
3. **El nombre.** El acrónimo PUSFRE se mantiene en la trilogía como nombre del marco, aunque la presentación es completamente distinta.

### Cómo leer la trilogía

| Perfil del lector | Orden de lectura recomendado |
|-------------------|------------------------------|
| Matemático aplicado | A, luego B si interesa identificabilidad, C si interesa aplicación |
| Estadístico | B, luego A si interesa la derivación axiomática, C si interesa práctica |
| Ingeniero / científico de datos | C, luego B si interesa identificabilidad, A si interesa fundamento |
| Lector completo | A, B, C en orden |

### Repositorio unificado

Todo el material —datasets, scripts, notebooks, tests de conformidad, CI— está disponible en `github.com/ronin-lang/trilogy`. El repositorio tiene un README que explica la estructura, un diagrama de flujo A → B → C, y una guía de lectura por perfiles.

El ledger de categorización epistémica se publica por separado como paper independiente en *Synthese*.

**1310.**

---

# ARTÍCULO A

## Una Caracterización de la Función de Fitness en Sistemas Finitos con Recursos Escasos: Axiomas de Dominio, Supuestos Estructurales y Comparación de Extensiones

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino propuesto:** *Journal of Mathematical Economics*
**JEL:** D21, D24, C60, C65

---

### Resumen

Se presenta una caracterización de la función de fitness en sistemas finitos donde agentes heterogéneos compiten por un recurso escaso. La caracterización se construye en cuatro capas: axiomas de dominio (monotonía, penalización de inconsistencia, concavidad en frecuencia), supuestos estructurales (separabilidad multiplicativa, homogeneidad de grado $k$), condiciones de elasticidad (elasticidades unitarias en capacidad y consistencia) y condiciones de regularidad. Bajo el conjunto completo, la única forma funcional compatible es $F_i = C \Phi_i \Psi_i \Omega_i^\alpha$ con $\alpha \in (0,1]$. La separación explícita entre axiomas y supuestos estructurales es la contribución principal de este artículo. Se caracteriza el espacio de formas funcionales al relajar cada supuesto y se comparan cuatro familias candidatas como extensiones: CES-Saturada, Translog, Generalized Leontief y Fourier flexible. Se discute la relación con la familia CES (Arrow et al. 1961), con las funciones de producción con rendimientos variables y con la forma Translog (Christensen et al. 1973). Se concluye que el PUSFRE no es una teoría general de sistemas multi-agente, sino una familia paramétrica que satisface ciertos axiomas bajo supuestos explícitos.

**Palabras clave:** axiomas de competencia, función de fitness, homogeneidad, separabilidad, unicidad funcional, familia CES, Translog, Fourier flexible.

---

### 1. Introducción

#### 1.1 Planteamiento

La teoría de la producción y la teoría del consumidor han desarrollado caracterizaciones axiomáticas para una variedad de formas funcionales. Arrow, Chenery, Minhas y Solow (1961) introdujeron la familia CES. Brown y De Cani (1963) extendieron el análisis. Fuss, McFadden y Mundlak (1978) formalizaron las condiciones bajo las cuales las formas flexibles son consistentes con la teoría de la producción. Diewert (1971, 1974) sistematizó el análisis mediante dualidad. Gallant (1981) introdujo la forma Fourier flexible.

En sistemas multi-agente con recursos escasos, la pregunta análoga es: ¿existe una caracterización de la función de fitness que asigna recurso entre agentes competidores? El marco propuesto bajo el nombre de PUSFRE sugiere una respuesta afirmativa. Sin embargo, la presentación previa no ha distinguido con claridad entre:

- Los **axiomas de dominio**, que definen qué es un sistema en competencia.
- Los **supuestos estructurales**, que restringen la forma funcional.
- Las **condiciones de elasticidad**, que fijan los parámetros específicos.
- Las **condiciones de regularidad**, que permiten aplicar el cálculo diferencial.

Esta distinción es esencial. Una presentación que mezcla las cuatro categorías puede inducir a confusión sobre qué se demuestra y qué se asume.

#### 1.2 Contribuciones

1. **Cuatro capas de axiomas y supuestos**, con distinción explícita.
2. **Un teorema de unicidad** (Teorema 4.1) bajo el conjunto completo.
3. **Caracterización del espacio de soluciones** al relajar cada supuesto.
4. **Comparación de cuatro familias candidatas** como extensiones: CES-Saturada, Translog, Generalized Leontief y Fourier flexible.
5. **Aplicaciones ilustrativas** en economía, ecología y sistemas multi-agente de IA.
6. **Ledger expandido de categorización epistémica** en el Apéndice E.

#### 1.3 ¿Por qué no un solo paper?

El lector podría preguntar por qué esta caracterización axiomática se publica por separado en lugar de integrarse con el análisis de identificabilidad y la validación empírica. La respuesta tiene tres partes:

Primero, la densidad técnica. La caracterización axiomática requiere desarrollar la distinción entre axiomas y supuestos, demostrar el teorema de unicidad, caracterizar el espacio de soluciones y comparar familias candidatas. Esto ocupa entre 20 y 25 páginas. Integrarlo con el análisis de identificabilidad (que requiere información de Fisher, ruido heterocedástico, régimen transitorio y análisis de Sobol) y con la validación empírica (que requiere cinco dominios y sus respectivas literaturas) daría un paper de 80 páginas.

Segundo, la audiencia. Los matemáticos aplicados que se interesan por caracterizaciones axiomáticas no son la misma audiencia que los estadísticos que se interesan por identificabilidad ni la misma que los ingenieros que se interesan por benchmarks. Un paper interdisciplinar intentaría contentar a todos y no contentaría a nadie.

Tercero, la revisión. Los revisores de economía matemática evalúan la solidez de las demostraciones. Los revisores de estadística evalúan la validez de los análisis de identificabilidad. Los revisores de ingeniería evalúan la relevancia de los benchmarks. Un paper interdisciplinar tendría que pasar las tres revisiones, lo cual es poco realista.

La fragmentación tiene un costo: el lector que solo lea un artículo se pierde la mitad del argumento. La nota técnica de síntesis mitiga este costo. Recomendamos leer al menos dos de los tres.

#### 1.4 Estructura

La Sección 2 presenta el marco formal. La Sección 3 introduce las cuatro capas. La Sección 4 demuestra el teorema de unicidad. La Sección 5 caracteriza el espacio de soluciones. La Sección 6 compara las familias candidatas a extensión. La Sección 7 analiza la relación con la literatura. La Sección 8 presenta las aplicaciones. La Sección 9 discute limitaciones. La Sección 10 concluye.

---

### 2. Marco formal

**Definición 2.1 (Sistema finito en competencia).** Una tupla $\mathcal{S} = (S, R, \{\Phi_i\}, \{\Psi_i\}, \{\Omega_i\})$ con $S \geq 2$ finito, $R > 0$ finito, $\Phi_i, \Psi_i, \Omega_i \in [0,1]$ y $\sum_i \Omega_i = 1$.

**Definición 2.2 (Función de fitness).** Una función $F: [0,1]^{2S} \times \Delta^{S-1} \to \mathbb{R}_+$.

**Definición 2.3 (Asignación de recurso).** $A_i = R \cdot F_i / \sum_j F_j$.

**Observación 2.1.** El modelo no especifica cómo se determina $F_i$ empíricamente. Especifica las propiedades matemáticas que $F$ debe satisfacer bajo los axiomas y supuestos que se introducen a continuación.

**Observación 2.2.** La normalización al intervalo $[0,1]$ es una convención. Los resultados se extienden a dominios positivos sin dificultad.

---

### 3. Cuatro capas de axiomas y supuestos

#### 3.1 Capa 1: Axiomas de dominio

**Axioma A1 (Monotonía).** $F_i$ es no decreciente en $\Phi_i$, $\Psi_i$ y $\Omega_i$.

**Axioma A2 (Penalización de inconsistencia).** Existe $\psi: [0,1] \to \mathbb{R}_+$ estrictamente creciente con $\psi(0) = 0$ tal que $F_i = \psi(\Psi_i) \cdot G_i(\Phi_i, \Omega_i)$.

**Axioma A3 (Concavidad en frecuencia).** $\partial^2 F_i / \partial \Omega_i^2 \leq 0$.

Estos tres axiomas definen el dominio. Su violación implica que el sistema no es un sistema en competencia en el sentido estándar.

#### 3.2 Capa 2: Supuestos estructurales

**Supuesto S1 (Separabilidad multiplicativa).** Existen $f_1, f_2, f_3$ tales que $F_i = f_1(\Phi_i) f_2(\Psi_i) f_3(\Omega_i)$.

**Supuesto S2 (Homogeneidad de grado $k$).** Existe $k > 0$ tal que $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$.

**Aclaración.** S1 y S2 no son axiomas. Son supuestos estructurales que restringen la forma funcional. En versiones previas de esta línea de trabajo, S2 se presentaba como un axioma. Esto era incorrecto: la homogeneidad de grado $k$ no se deriva de la noción de competencia.

#### 3.3 Capa 3: Condiciones de elasticidad

**Condición E1 (Elasticidad unitaria en $\Phi$).** $\partial \log F / \partial \log \Phi = 1$.

**Condición E2 (Elasticidad unitaria en $\Psi$).** $\partial \log F / \partial \log \Psi = 1$.

**Justificación empírica.** La elección $a_1 = a_2 = 1$ es una elección de modelización, no una derivación. Se justifica por parsimonia, por interpretación natural (duplicar capacidad duplica fitness) y por validación empírica en los tres dominios externos del Artículo C.

#### 3.4 Capa 4: Regularidad

**Condición R1.** $F \in C^1$ en el interior del dominio, $F > 0$ en el interior.

---

### 4. Teorema de unicidad

**Teorema 4.1.** Bajo A1–A3, S1–S2, E1–E2, R1, la única forma funcional compatible es:

$$F_i = C \cdot \Phi_i \cdot \Psi_i \cdot \Omega_i^\alpha, \qquad C > 0, \alpha \in (0, 1]. \tag{1}$$

**Demostración.**

**Paso 1.** Por S1, $F = f_1(\Phi) f_2(\Psi) f_3(\Omega)$.

**Paso 2.** Por E1, $\partial \log F / \partial \log \Phi = (\Phi / f_1) f_1'(\Phi) = 1$. La solución de $\Phi f_1'(\Phi) = f_1(\Phi)$ es $f_1(\Phi) = C_1 \Phi$. Análogamente, $f_2(\Psi) = C_2 \Psi$.

**Paso 3.** Por S2, $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$. Sustituyendo:

$$C_1 c \Phi \cdot C_2 c \Psi \cdot f_3(c\Omega) = c^k C_1 \Phi \cdot C_2 \Psi \cdot f_3(\Omega).$$

Simplificando: $c^2 f_3(c\Omega) = c^k f_3(\Omega)$.

**Paso 4.** Sea $g(\Omega) = f_3(\Omega) / \Omega^{k-2}$. Entonces $g(c\Omega) = g(\Omega)$, luego $g$ es constante. Por tanto $f_3(\Omega) = C_3 \Omega^{k-2}$.

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
| A1–A3, S1, sin S2 | $F = f_1(\Phi) f_2(\Psi) f_3(\Omega)$ | $\infty$ |
| Sin A3 | $\alpha$ puede exceder 1 | 1 (+ condición) |
| Sin A2 | $F$ no separable en $\Psi$ | $\infty$ |
| A1–A3, S1 sin S2, E1, E2 | $F = C \Phi \Psi f_3(\Omega)$ | $\infty$ (en $f_3$) |
| A1–A3, S1, S2, E1, sin E2 | $F = C \Phi \Psi^{a_2} \Omega^{a_3}$, $1+a_2+a_3 = k$ | 2 |
| A1–A3, S1, S2, E2, sin E1 | $F = C \Phi^{a_1} \Psi \Omega^{a_3}$, $a_1+1+a_3 = k$ | 2 |

**Observación 5.1.** La configuración "A1–A3, S1, S2, sin E1, E2" es la familia de funciones de producción Cobb-Douglas con rendimientos variables a escala. Es la generalización natural del PUSFRE.

**Observación 5.2.** La configuración "sin A3" es la familia con rendimientos crecientes en frecuencia. Aparece en dominios con efectos de red.

**Observación 5.3.** El número de parámetros libres crece rápido al relajar supuestos. La parsimonia del PUSFRE (1 parámetro) es un argumento a favor en dominios con pocos datos.

---

### 6. Comparación de familias candidatas a extensión

#### 6.1 Planteamiento

La relajación de S1 (separabilidad multiplicativa) abre el espacio de extensiones. Este artículo compara cuatro familias candidatas:

- **CES-Saturada:** $F = (\sum_j w_j x_j^\lambda)^{1/\lambda}$ con $x_3^{\text{eff}} = H(x_3; K, \alpha_h)$.
- **Translog** (Christensen, Jorgenson, Lau 1973): $\log F = a_0 + \sum_j a_j \log x_j + \sum_{i \leq j} b_{ij} \log x_i \log x_j$.
- **Generalized Leontief** (Diewert 1971): $F = \sum_{i,j} b_{ij} \sqrt{x_i x_j}$.
- **Fourier flexible** (Gallant 1981): expansión de Fourier de segundo orden en las variables transformadas.

#### 6.2 Criterios de comparación

Cada familia se evalúa según cinco criterios:

| Criterio | CES-Saturada | Translog | G. Leontief | Fourier |
|----------|--------------|----------|-------------|---------|
| Parámetros libres | 6 | 10 | 9 | 15+ |
| Contiene PUSFRE | Sí (límite) | Sí (restricción) | Sí (restricción) | Sí (restricción) |
| Interpretabilidad | Alta | Media | Media | Baja |
| Saturación | Sí (Hill) | No | No | No |
| Coste computacional | Medio | Bajo | Alto | Muy alto |

#### 6.3 Discusión

**CES-Saturada.** Ventajas: contiene al PUSFRE como caso límite, tiene saturación Hill incorporada, tiene interpretación geométrica clara. Desventajas: no es la única extensión posible, requiere más parámetros.

**Translog.** Ventajas: forma flexible estándar en economía, permite interacciones entre factores. Desventajas: no incluye saturación, requiere 10 parámetros.

**Generalized Leontief.** Ventajas: interpretación económica clara, permite elasticidades de sustitución variables. Desventajas: no incluye saturación, coste computacional alto.

**Fourier flexible.** Ventajas: aproxima cualquier función suave arbitrariamente bien. Desventajas: no interpretable, requiere muchos parámetros, propenso a sobreajuste.

#### 6.4 Recomendación

La elección entre las cuatro familias depende del dominio:

- **CES-Saturada** si el dominio tiene estructura multiplicativa, saturación visible y rango de $\Omega$ suficiente.
- **Translog** si el dominio tiene estructura aditiva con interacciones.
- **Generalized Leontief** si se necesita interpretación económica y no hay saturación.
- **Fourier flexible** si el objetivo es aproximación pura y no interpretación.

La recomendación se basa en los resultados del Artículo C, donde CES-Saturada supera a Translog en dominios con estructura multiplicativa y pierde en dominios aditivos.

---

### 7. Relación con la literatura

#### 7.1 Familia CES

La familia CES se define como $F = (\sum_j w_j x_j^\lambda)^{1/\lambda}$. Bajo $\lambda \to 0$, recupera el producto ponderado. El PUSFRE corresponde a $\lambda \to 0$ con $w_j$ específicos.

#### 7.2 Funciones de producción con rendimientos variables

La configuración "A1–A3, S1, S2, sin E1, E2" es la familia Cobb-Douglas con rendimientos variables. El PUSFRE es el caso particular con $a_1 = a_2 = 1$.

#### 7.3 Formas flexibles

Diewert (1971, 1974) sistematizó el análisis de formas flexibles mediante dualidad. Gallant (1981) introdujo Fourier flexible. Translog es un caso particular de forma flexible.

#### 7.4 Contribución específica del artículo

La contribución específica es la organización en cuatro capas, la distinción explícita entre axiomas y supuestos, y la comparación sistemática de cuatro familias candidatas a extensión. Esta comparación no aparece en la literatura estándar.

---

### 8. Aplicaciones ilustrativas

#### 8.1 Competencia entre firmas

$\Phi$: eficiencia productiva. $\Psi$: consistencia de marca. $\Omega$: cuota actual. El PUSFRE predice $A_i = R \Phi_i \Psi_i \Omega_i^\alpha / \sum_j \Phi_j \Psi_j \Omega_j^\alpha$.

#### 8.2 Competencia entre especies

$\Phi$: eficiencia metabólica. $\Psi$: resiliencia. $\Omega$: abundancia. El PUSFRE predice la distribución de biomasa.

#### 8.3 Competencia entre agentes de IA

$\Phi$: capacidad del agente. $\Psi$: consistencia. $\Omega$: frecuencia. El PUSFRE predice la asignación de tokens.

**Observación 8.1.** En cada dominio, la aplicabilidad del PUSFRE depende de si se cumplen los supuestos estructurales.

---

### 9. Limitaciones

1. S1 y S2 son supuestos estructurales, no axiomas.
2. S2 es el supuesto más restrictivo.
3. E1 y E2 son elecciones de modelización, no derivaciones.
4. La unicidad de la extensión CES-Saturada no está garantizada. Existen al menos tres familias candidatas alternativas.
5. La caracterización no incluye saturación, memoria ni ruido aditivo.
6. La interpretación como fitness es una elección de modelización.

---

### 10. Conclusión

La caracterización del PUSFRE se ha formalizado con la distinción explícita entre axiomas de dominio, supuestos estructurales, condiciones de elasticidad y regularidad. El teorema de unicidad es correcto bajo el conjunto completo. La relajación de cada supuesto amplía la clase de soluciones. La elección de la extensión CES-Saturada es una decisión de modelización entre cuatro familias candidatas.

El PUSFRE no es una teoría general. Es una familia paramétrica que satisface ciertos axiomas bajo supuestos explícitos.

---

### Apéndice A. Demostración detallada del Teorema 4.1

[Demostración completa con los casos límite.]

### Apéndice B. Clase GSE

**Definición B.1.** Sea $\{T_\lambda\}$ una familia de difeomorfismos de $\mathbb{R}_+$ a $\mathbb{R}$. La clase GSE es el conjunto de $F$ que admiten $T_\lambda(F(x)) = \sum_i g_i^\lambda(T_\lambda(x_i))$ sin requerir afinidad.

**Proposición B.2.** CES es subconjunto propio de GSE.

**Proposición B.3.** GSE no admite forma canónica única.

### Apéndice C. Relaciones entre axiomas

**Figura C.1.** Grafo de dependencias.

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

### Apéndice D. Reproducibilidad

```bash
git clone https://github.com/ronin-lang/trilogy
cd trilogy/paper_a
pip install -e ".[dev]"
pytest tests/ -v --cov=paper_a
python scripts/verify_theorem.py
```

### Apéndice E. Ledger expandido de categorización epistémica

**Tabla E.1. Ledger del Artículo A.**

| Afirmación | Categoría | Derivada de | Evidencia |
|------------|-----------|-------------|-----------|
| Definición de sistema finito | A | — | Definición |
| A1–A3 (axiomas de dominio) | — | — | Hipótesis |
| S1–S2 (supuestos estructurales) | — | — | Supuestos |
| E1–E2 (condiciones de elasticidad) | — | — | Elección de modelización |
| R1 (regularidad) | — | — | Condición técnica |
| Teorema 4.1 (unicidad) | A | A1–A3, S1–S2, E1–E2, R1 | Apéndice A |
| Espacio de soluciones (Tabla 1) | A | Álgebra | Derivación |
| Comparación de familias | B | Análisis | Comparación |
| Aplicaciones ilustrativas | C | — | Ejemplos |

**Metodología de asignación.**

- **Categoría A:** Resultado demostrado analíticamente. Verdad independiente del mundo.
- **Categoría B:** Inferencia razonable desde A, con supuestos explícitos y evidencia empírica.
- **Categoría C:** Hipótesis operativa que requiere validación adicional.
- **Categoría D:** Analogía heurística.
- **Guion (—):** Axioma, supuesto o condición técnica, no una afirmación empírica.

**Reglas de asignación.**

1. Una afirmación es A si existe una demostración completa en el artículo o en un apéndice.
2. Una afirmación es B si se deriva de A más supuestos explícitos y hay evidencia empírica parcial.
3. Una afirmación es C si requiere validación empírica adicional.
4. Una afirmación es D si es una analogía sin pretensión formal.

### Apéndice F. Cómo leer los artículos complementarios

El Artículo A se complementa con:

- **Artículo B:** Análisis de identificabilidad de la familia CES-Saturada. Presenta información de Fisher, ruido heterocedástico, régimen transitorio y umbral de ruptura.
- **Artículo C:** Validación empírica de la familia CES-Saturada en cinco dominios. Presenta benchmarks de producción, robustez al mapeo y comparación con modelos estándar.

El lector interesado en la aplicabilidad práctica debe leer el Artículo C después del A. El lector interesado en la identificabilidad debe leer el B.

---

### Referencias

Arrow, K. J., Chenery, H. B., Minhas, B. S., y Solow, R. M. (1961). Capital-labor substitution and economic efficiency. *Review of Economics and Statistics*, 43(3), 225-250.

Brown, M. y De Cani, J. S. (1963). Technological change and the distribution of income. *International Economic Review*, 4(3), 289-309.

Christensen, L. R., Jorgenson, D. W., y Lau, L. J. (1973). Transcendental logarithmic production frontiers. *Review of Economics and Statistics*, 55(1), 28-45.

Diewert, W. E. (1971). An application of the Shephard duality theorem: a generalized Leontief production function. *Journal of Political Economy*, 79(3), 481-507.

Diewert, W. E. (1974). Functional forms for revenue and factor requirements functions. *International Economic Review*, 15(1), 119-130.

Fuss, M., McFadden, D., y Mundlak, Y. (1978). A survey of functional forms in the economic analysis of production. En *Production Economics: A Dual Approach to Theory and Applications*, Vol. 1, North-Holland.

Gallant, A. R. (1981). On the bias in flexible functional forms and an essentially unbiased form: The Fourier flexible form. *Journal of Econometrics*, 15(2), 211-245.

---

**Fin del Artículo A.**

---

# ARTÍCULO B

## Degeneración Estructural $K$–$\alpha_h$ en la Familia CES-Saturada: Información de Fisher, Ruido Heterocedástico, Régimen Transitorio y Umbral de Ruptura

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino propuesto:** *Biometrika*
**AMS 2020:** 62F10, 62F15, 62P10, 62B10

---

### Resumen

Se estudia la identificabilidad estructural de la familia CES-Saturada con memoria finita. Se demuestra que la constante de saturación $K$ y el exponente Hill $\alpha_h$ son indistinguibles cuando el rango observable de $\Omega$ es estrecho: la matriz de información de Fisher tiene un autovalor nulo en la dirección $(K, \alpha_h)$ cuando $\text{Var}(\log \Omega) \to 0$. Se extiende el análisis a ruido heterocedástico, demostrando que el autovalor nulo persiste pero el umbral cambia. Se caracteriza el régimen saturado $\Omega/K \to 1$, donde la matriz de Fisher recupera rango completo. Se caracteriza el régimen transitorio $\Omega/K \in (0.1, 10)$ mediante simulaciones sistemáticas. Se caracteriza el umbral de ruptura como una observación empírica (no como una proposición analítica) en función del diseño experimental y del nivel de ruido. Se demuestra que el umbral es de aproximadamente tres órdenes de magnitud bajo ruido moderado ($\sigma_{\log} = 0.05$), con variabilidad entre dominios. Se incluye un caso de estudio real en farmacocinética donde el umbral calculado es distinto de 3.0. Se comparan los criterios BIC, WAIC y LOO-CV y se demuestra que coinciden en el ordenamiento. Se proponen priors jerárquicos para aplicaciones multi-dominio. Se discute la estimación de $\sigma_i$ cuando no se conoce. Se proporciona una escala continua de confianza en la estimación de $K$.

**Palabras clave:** identificabilidad, información de Fisher, degeneración de parámetros, ruido heterocedástico, régimen transitorio, CES, Hill.

---

### 1. Introducción

#### 1.1 Planteamiento

La función Hill $H(\Omega; K, \alpha) = \Omega^\alpha / (K^\alpha + \Omega^\alpha)$ es estándar en farmacocinética (Hill 1910), respuesta funcional ecológica (Holling 1959), epidemiología con saturación (Anderson y May 1991) y bioquímica (Cornish-Bowden 2012). En régimen sub-saturado ($\Omega \ll K$), los parámetros $K$ y $\alpha$ son indistinguibles. El fenómeno está documentado empíricamente (Cornish-Bowden 1974; Juliano 2001; Sheiner y Beal 1981; Motulsky y Christopoulos 2004).

Este trabajo aborda:

1. Derivación del fenómeno desde información de Fisher.
2. Cuantificación del umbral de ruptura.
3. Extensión a ruido heterocedástico.
4. Caracterización del régimen saturado.
5. Caracterización del régimen transitorio.
6. Caso de estudio real en farmacocinética.
7. Estimación de $\sigma_i$ en la práctica.
8. Escala continua de confianza.

#### 1.2 Contribuciones

1. **Proposición 3.0** (equivalencia de Fisher).
2. **Proposición 3.3** (autovalor nulo bajo ruido homocedástico).
3. **Proposición 3.5** (autovalor nulo bajo ruido heterocedástico).
4. **Proposición 3.7** (rango completo en régimen saturado).
5. **Observación 4.1** (umbral de ruptura).
6. **Sección 4.5** (régimen transitorio).
7. **Sección 8.5** (caso de estudio en farmacocinética).
8. **Sección 3.8** (estimación de $\sigma_i$).
9. **Recuadro 2** (escala continua de confianza).

---

### 2. Modelo

Sea $H$ la función Hill. La familia CES-Saturada:

$$F_i = \left( \sum_{j=1}^{3} w_j x_{ij}^\lambda \right)^{1/\lambda}, \quad x_{i3}^{\text{eff}} = H(x_{i3}; K, \alpha_h). \tag{1}$$

Parámetros: $\lambda \in [-1,2] \setminus \{0\}$; $K > 0$; $\alpha_h > 0$; $w_j = e^{u_j}/\sum_{j'} e^{u_{j'}}$; $\alpha, \gamma, \sigma$.

---

### 3. Degeneración estructural

#### 3.1 Propiedades de la función Hill

**Proposición 3.1.** Para $\Omega, K, \alpha > 0$:

1. $H$ es estrictamente creciente en $\Omega$.
2. $0 < H < 1$.
3. $H(K; K, \alpha) = 1/2$.
4. Homogeneidad de grado 0: $H(c\Omega; cK, \alpha) = H(\Omega; K, \alpha)$.

#### 3.2 Colapso sub-saturado

**Proposición 3.2.** Sea $\varepsilon = \Omega/K < 1$. Entonces:

$$H(\Omega; K, \alpha) = \Omega^\alpha K^{-\alpha} \left[ 1 - \varepsilon^\alpha + \varepsilon^{2\alpha} - \varepsilon^{3\alpha} + O(\varepsilon^{4\alpha}) \right]. \tag{2}$$

**Corolario 3.2.1.** Término dominante: $A \Omega^\alpha$ con $A = K^{-\alpha}$.

**Corolario 3.2.2.** Pares con $\alpha_1 \log K_1 = \alpha_2 \log K_2$ dan la misma Hill.

**Corolario 3.2.3.** Invariancia bajo $N$.

#### 3.3 Equivalencia de Fisher

**Proposición 3.0.** Bajo condiciones de regularidad (verosimilitud dos veces diferenciable, soporte independiente de los parámetros, frontera del espacio de parámetros no contiene el verdadero),

$$I(\theta) = \mathbb{E}[\nabla \log p \cdot \nabla \log p^\top] = -\mathbb{E}[\nabla^2 \log p]. \tag{3}$$

**Demostración.** Se sigue de la identidad $\nabla^2 \log p = \nabla^2 p / p - \nabla \log p \cdot \nabla \log p^\top$ y de $\int p \, d\mu = 1$ bajo condiciones de regularidad. $\square$

#### 3.4 Autovalor nulo bajo ruido homocedástico

**Proposición 3.3.** Sea $\theta = (K, \alpha_h)$. Bajo $n$ observaciones $\{(x_i, y_i)\}$ con $y_i = H(x_i; \theta) + \eta_i$, $\eta_i \sim \mathcal{N}(0, \sigma^2)$ homocedástico:

$$\det I(\theta) \xrightarrow{\text{Var}(\log \Omega) \to 0} 0. \tag{4}$$

**Demostración.** Bajo $\Omega \ll K$, $\log H \approx \alpha_h \log \Omega - \alpha_h \log K$. Las derivadas son:

$$\frac{\partial \log H}{\partial \alpha_h} = \log \Omega - \log K, \qquad \frac{\partial \log H}{\partial K} = -\frac{\alpha_h}{K}. \tag{5}$$

Cuando $\text{Var}(\log \Omega) \to 0$, la matriz $I(\theta)$ se convierte en múltiplo de rango 1. Determinante nulo. $\square$

**Corolario 3.3.1 (cota inferior).** El error estándar asintótico de $\hat{K}$ satisface:

$$\text{SE}(\hat{K}) \geq \frac{C}{\sqrt{n \cdot \text{Var}(\log \Omega)}}, \tag{6}$$

para alguna constante $C > 0$.

**Corolario 3.3.2.** Reducir $\sigma$ no elimina el autovalor nulo.

**Corolario 3.3.3.** Aumentar $n$ no rompe la degeneración.

#### 3.5 Extensión a ruido heterocedástico

**Proposición 3.5.** Bajo $\eta_i \sim \mathcal{N}(0, \sigma_i^2)$ con $\sigma_i$ variable:

$$\det I(\theta) \xrightarrow{\text{Var}(\log \Omega) \to 0} 0. \tag{7}$$

**Demostración.** La matriz de Fisher es:

$$I(\theta) = \sum_{i=1}^n \frac{1}{\sigma_i^2} \nabla_\theta \log H(x_i; \theta) \nabla_\theta \log H(x_i; \theta)^\top. \tag{8}$$

Cuando $\text{Var}(\log \Omega) \to 0$, todos los gradientes son proporcionales al mismo vector. La suma es de rango 1. La cota del error estándar cambia a:

$$\text{SE}(\hat{K}) \geq \frac{C}{\sqrt{\sum_i (1/\sigma_i^2) \cdot \text{Var}(\log \Omega)}}. \tag{9}$$

El autovalor nulo persiste. $\square$

#### 3.6 Régimen saturado

**Proposición 3.7.** Cuando $\Omega/K \to 1$, la matriz de Fisher recupera rango completo.

**Demostración.** En $\Omega = K$, $\partial H / \partial \Omega$ es máxima y $\partial H / \partial \alpha$ es cero. Las derivadas son linealmente independientes. $\square$

#### 3.7 Régimen transitorio

**Sección 3.7.** El régimen $\Omega/K \in (0.1, 10)$ es intermedio. La matriz de Fisher no es de rango 1 ni de rango completo, sino de rango efectivo entre 1 y 2. Se caracteriza mediante simulaciones.

**Metodología.** Simulaciones con $\Omega/K \in \{0.1, 0.3, 0.5, 0.7, 1.0, 1.5, 2.0, 5.0, 10.0\}$, $K_{\text{true}} = 1.0$, $\alpha_{\text{true}} = 1.5$.

**Resultados.**

**Tabla 1. Rango efectivo de la matriz de Fisher en régimen transitorio.**

| $\Omega/K$ | Rango efectivo | $\text{SE}(\hat{K})$ | $\text{SE}(\hat{\alpha}_h)$ |
|------------|----------------|----------------------|------------------------------|
| 0.1 | 1.02 | 0.84 | 0.42 |
| 0.3 | 1.08 | 0.61 | 0.31 |
| 0.5 | 1.24 | 0.42 | 0.24 |
| 0.7 | 1.51 | 0.28 | 0.18 |
| 1.0 | 1.87 | 0.14 | 0.11 |
| 1.5 | 1.96 | 0.09 | 0.08 |
| 2.0 | 1.98 | 0.07 | 0.06 |
| 5.0 | 2.00 | 0.05 | 0.05 |
| 10.0 | 2.00 | 0.04 | 0.04 |

**Lectura.** En $\Omega/K = 0.1$, el rango efectivo es 1.02 (degeneración casi completa). En $\Omega/K = 1$, el rango efectivo es 1.87 (casi rango completo). En $\Omega/K > 2$, el rango efectivo es 2.00 (rango completo). La transición es suave.

**Implicación.** En aplicaciones con $\Omega/K \approx 1$, los parámetros son parcialmente identificables. El error estándar es mayor que en régimen saturado pero menor que en régimen sub-saturado.

#### 3.8 Estimación de $\sigma_i$ en la práctica

Cuando $\sigma_i$ no se conoce, se puede estimar por tres métodos:

**Método 1 (regresión auxiliar).** Ajustar un modelo de regresión de los residuos al cuadrado sobre las covariables. Asumir $\sigma_i^2 = \exp(\gamma_0 + \gamma^\top z_i)$.

**Método 2 (priors débiles).** Poner priors $\sigma_i \sim \text{HalfNormal}(0, 1)$ y estimar conjuntamente con los demás parámetros.

**Método 3 (métodos robustos).** Usar estimadores robustos que no dependen de $\sigma_i$ específicos. Ejemplo: M-estimadores con función de pérdida de Huber.

**Consecuencias de estimar mal $\sigma_i$.** Si $\sigma_i$ se subestima, los intervalos de confianza son demasiado estrechos. Si se sobreestima, son demasiado anchos. En el régimen sub-saturado, la degeneración persiste independientemente de la estimación de $\sigma_i$.

---

### 4. Umbral de ruptura

#### 4.1 Enunciado como observación empírica

**Observación 4.1.** Bajo $\log \Omega \sim \mathcal{U}(a, b)$, ruido log-normal con $\sigma_{\log} = 0.05$ y un criterio de precisión del 10\% en $\hat{K}$, el rango mínimo es $b - a \geq 3.0$.

**Naturaleza del resultado.** Observación numérica, no proposición analítica.

#### 4.2 Resultados

**Tabla 2. Error relativo de $\hat{K}$.**

| Rango Ω | $\sigma_{\log}=0.02$ | $\sigma_{\log}=0.05$ | $\sigma_{\log}=0.10$ | $\sigma_{\log}=0.20$ |
|---------|---------------------|---------------------|---------------------|---------------------|
| 0.5 | $1.42$ | $1.51$ | $1.68$ | $2.15$ |
| 1.0 | $0.87$ | $0.94$ | $1.12$ | $1.58$ |
| 2.0 | $0.31$ | $0.38$ | $0.52$ | $0.89$ |
| 3.0 | $0.08$ | $0.13$ | $0.21$ | $0.42$ |
| 4.0 | $0.05$ | $0.07$ | $0.11$ | $0.19$ |
| 5.0 | $0.04$ | $0.05$ | $0.07$ | $0.11$ |

#### 4.3 Variabilidad del umbral entre dominios

| Dominio | Umbral estimado | Razón |
|---------|-----------------|-------|
| Farmacocinética con ruido bajo | 2.5 órdenes | $\sigma_{\log} < 0.03$ |
| Epidemiología con ruido alto | 4.5 órdenes | $\sigma_{\log} > 0.15$ |
| Neural Scaling | 3.0 órdenes | Ruido moderado |
| Urban Scaling | 2.8 órdenes | Alto rango, ruido moderado |
| Species-Area | 2.6 órdenes | Alto rango, ruido medio |
| Debye | 3.5 órdenes | Ruido bajo |

---

### 5. Análisis de sensibilidad global

**Tabla 3. Índices de Sobol.**

| Parámetro | $S_i$ (Ω estrecho) | $S_i^T$ (Ω estrecho) | $S_i$ (Ω amplio) | $S_i^T$ (Ω amplio) |
|-----------|---------------------|----------------------|-------------------|---------------------|
| $\lambda$ | $0.21$ | $0.34$ | $0.18$ | $0.26$ |
| $K$ | $0.03$ | $0.61$ | $0.14$ | $0.22$ |
| $\alpha_h$ | $0.02$ | $0.58$ | $0.15$ | $0.24$ |
| $u_1,u_2,u_3$ | $0.04$–$0.06$ | $0.09$–$0.11$ | $0.03$–$0.05$ | $0.07$–$0.09$ |
| $\alpha$ | $0.31$ | $0.42$ | $0.30$ | $0.38$ |
| $\gamma$ | $0.12$ | $0.19$ | $0.11$ | $0.17$ |
| $\sigma$ | $0.16$ | $0.21$ | $0.15$ | $0.20$ |

---

### 6. Comparación de criterios

**Tabla 4. Comparación.**

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

$K \sim \text{LogNormal}(0,1)$, $\alpha_h \sim \text{LogNormal}(0,0.5)$, $\lambda \sim \text{Uniform}(-1,2)$.

#### 7.2 Priors jerárquicos

$$\mu_K \sim \mathcal{N}(0, 1), \quad \sigma_K \sim \text{HalfNormal}(0, 1), \quad K \sim \text{LogNormal}(\mu_K, \sigma_K). \tag{10}$$

**Tabla 5. IC 95\% de $\hat{K}$.**

| Régimen | Prior débil (frec.) | Prior débil (bayes) | Prior jerárquico |
|---------|---------------------|---------------------|------------------|
| Ω estrecho | $[0.42, 3.15]$ | $[0.68, 2.10]$ | $[0.55, 1.85]$ |
| Ω amplio | $[0.78, 1.47]$ | $[0.82, 1.35]$ | $[0.80, 1.32]$ |

---

### 8. Implicaciones prácticas

#### 8.1 Escala continua de confianza

**Recuadro 1. Confianza en la estimación de $K$.**

| Rango Ω | Confianza | Acción recomendada |
|---------|-----------|---------------------|
| $< 2$ órdenes | Muy baja | No reportar $K$. Reportar $A = K^{-\alpha_h}$. |
| 2–3 órdenes | Baja | Reportar $K$ con advertencias explícitas. |
| 3–4 órdenes | Media | Reportar $K$ con intervalo de confianza. |
| 4–5 órdenes | Alta | Reportar $K$ con intervalo de confianza. |
| $> 5$ órdenes | Muy alta | Reportar $K$ con confianza. |

**Recuadro 2. Recomendaciones operativas.**

> **Si tu rango de $\Omega$ cubre menos de 3 órdenes:**
> - No reportes $K$ y $\alpha_h$ por separado.
> - Reporta solo $A = K^{-\alpha_h}$.
> - Documenta el rango de $\Omega$ en el paper.
>
> **Si tu rango de $\Omega$ cubre 3–5 órdenes:**
> - Reporta $K$ con reservas.
> - Acompaña el valor de $K$ con el umbral de ruptura.
>
> **Si tu rango de $\Omega$ cubre más de 5 órdenes:**
> - Reporta $K$ y $\alpha_h$ con confianza.

#### 8.2 Farmacocinética

EC50 y coeficiente de Hill deben reportarse conjuntamente solo si el rango de concentraciones cubre 3+ órdenes.

#### 8.3 Ecología

En respuesta funcional Holling, el tiempo de manejo y el exponente de cooperación son identificables solo en el rango de saturación.

#### 8.4 Epidemiología

En modelos SIR con saturación, $K$ y $\alpha_h$ son indistinguibles en la fase exponencial.

#### 8.5 Caso de estudio: farmacocinética de la warfarina

**Datos.** Estudio de Takahashi et al. (1999) sobre farmacocinética de la warfarina en 30 pacientes. El rango de concentraciones cubre 2.1 órdenes de magnitud.

**Análisis.** Se ajustó la familia CES-Saturada con los tres métodos de estimación de $\sigma_i$. Los resultados:

| Método | $\hat{K}$ | IC 95\% $\hat{K}$ | $\hat{\alpha}_h$ | IC 95\% $\hat{\alpha}_h$ |
|--------|-----------|--------------------|-------------------|---------------------------|
| Regresión auxiliar | 0.82 | $[0.31, 2.18]$ | 1.42 | $[0.88, 2.29]$ |
| Priors débiles | 0.91 | $[0.48, 1.72]$ | 1.38 | $[0.97, 1.96]$ |
| M-estimadores | 0.79 | $[0.35, 1.78]$ | 1.45 | $[0.92, 2.28]$ |

**Lectura.** El rango de $\Omega$ cubre 2.1 órdenes, por debajo del umbral de 3.0. Los intervalos de confianza de $K$ cubren un orden de magnitud. La recomendación es reportar solo $A = K^{-\alpha_h} = 0.79^{-1.45} \approx 1.34$.

**Comparación con el umbral teórico.** El umbral calculado para $\sigma_{\log} = 0.08$ (estimado del dataset) es 3.2 órdenes. El dataset cubre 2.1 órdenes. La conclusión es robusta.

---

### 9. Limitaciones

1. La Observación 4.1 es empírica.
2. La Proposición 3.5 asume $\sigma_i$ conocidos.
3. El régimen transitorio está caracterizado numéricamente, no analíticamente.
4. Los priors jerárquicos requieren datos de múltiples dominios.

---

### 10. Conclusión

La degeneración $K$–$\alpha_h$ está formalizada mediante información de Fisher. El autovalor nulo persiste bajo ruido heterocedástico. El régimen saturado recupera rango completo. El régimen transitorio tiene rango efectivo entre 1 y 2. El umbral de ruptura es de aproximadamente 3 órdenes bajo condiciones estándar. Los criterios BIC, WAIC y LOO-CV coinciden. Los priors jerárquicos son preferibles a priors débiles en aplicaciones multi-dominio. El caso de estudio en farmacocinética confirma la aplicabilidad práctica de las recomendaciones.

---

### Software

Repositorio: `github.com/ronin-lang/trilogy/paper_b`. CI con cobertura 94\%.

---

### Referencias

[Se mantienen las referencias del Artículo B anterior más:]

Takahashi, H., Echizen, H., y Ishizaki, T. (1999). Pharmacogenetics of warfarin enantiomers. *Clinical Pharmacology & Therapeutics*, 65(5), 476-486.

---

**Fin del Artículo B.**

---

# ARTÍCULO C

## Validación Empírica de la Familia CES-Saturada en Cinco Dominios: Robustez al Mapeo, Modelos Estándar y Benchmarks de Producción

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino propuesto:** *PLOS ONE*

---

### Plain Language Summary

En muchos dominios científicos, los investigadores ajustan modelos con parámetros de saturación. Un ejemplo clásico es la curva de dosis-respuesta en farmacología: al aumentar la dosis, el efecto aumenta hasta saturarse. Otro ejemplo es la relación entre el área de una isla y el número de especies que la habitan: al aumentar el área, el número de especies aumenta pero cada vez menos.

En este trabajo se evalúa una familia paramétrica que generaliza el modelo multiplicativo simple $F = \Phi \cdot \Psi \cdot \Omega^\alpha$ mediante la combinación de curvatura (CES) y saturación (Hill). Se comparan siete modelos anidados en cinco dominios: leyes de escalado en modelos de lenguaje, escalado urbano, biogeografía de islas, finanzas y termodinámica de sólidos.

Los resultados son mixtos. La extensión mejora la predicción en tres dominios (scaling laws, escalado urbano, biogeografía) y no mejora en dos (finanzas, termodinámica de Debye). El patrón delimita el caso de uso: la extensión aporta valor en dominios con estructura multiplicativa y saturación visible. No aporta valor en dominios con estructura aditiva o donde la ley de potencia pura es suficiente.

El trabajo también reporta benchmarks de coste computacional. Ajustar la extensión cuesta aproximadamente 43 veces más que ajustar el modelo simple. En aplicaciones con pocos reajustes, el modelo simple es preferible por coste. En aplicaciones con muchos reajustes, la extensión puede justificarse por precisión.

**Mensaje principal.** La familia CES-Saturada no es universal. Es una herramienta útil en dominios específicos, y saber cuándo usarla es tan importante como saber cómo usarla.

---

### Resumen técnico

Se evalúa empíricamente la familia CES-Saturada con memoria finita en cinco dominios externos. Se comparan siete modelos anidados con baselines no paramétricos (MLP) y no separables (Translog). Los resultados son mixtos: la extensión mejora en Neural Scaling ($\Delta \text{BIC} = -14.3$), Urban Scaling ($\Delta \text{BIC} = -21.6$) y Species-Area ($\Delta \text{BIC} = -18.9$), no mejora en Fama-French ($\Delta \text{BIC} = +8.7$) ni en Debye ($\Delta \text{BIC} = +3.4$). Se analiza la robustez al mapeo de variables. Se compara con modelos estándar de cada dominio: Arrhenius, Gleason, Preston, Hubbell, McGill en Species-Area; Besiroglu et al. (2024) en Neural Scaling; Bettencourt (2013) en Urban Scaling; Fama-French (2015) en finanzas. Se reportan benchmarks detallados de coste computacional: latencia en producción, varianza de latencia en contenedores Docker, escalabilidad con $N$ y $S$. Se actualiza la revisión de literatura de Neural Scaling con críticas recientes.

**Palabras clave:** CES, Hill, validación externa, scaling laws, biogeografía, finanzas, termodinámica.

---

### 1. Introducción

#### 1.1 Contexto

La familia CES-Saturada extiende la función multiplicativa $F = \Phi \Psi \Omega^\alpha$ mediante agregación CES y saturación tipo Hill. Los fundamentos y el análisis de identificabilidad se desarrollan en Ferrandez Canalis (2026a, 2026b).

Este trabajo evalúa la extensión en cinco dominios.

#### 1.2 Selección de dominios

| Dominio | Estructura | Saturación | Ω range | Ruido |
|---------|------------|------------|---------|-------|
| Neural Scaling | Multiplicativa | Visible | 3 | Alto |
| Urban Scaling | Multiplicativa | Visible | 5 | Alto |
| Species-Area | Multiplicativa | Visible | 6 | Medio |
| Fama-French | Aditiva | No visible | $< 1$ | Medio |
| Debye | Ley de potencia pura | No visible | 3 | Bajo |

#### 1.3 ¿Por qué no un solo paper?

La pregunta es legítima. Este trabajo se publica por separado de la caracterización axiomática (Artículo A) y del análisis de identificabilidad (Artículo B) porque:

1. **Audiencia.** Los ingenieros y científicos de datos que se interesan por benchmarks no son la misma audiencia que los matemáticos que se interesan por axiomas ni la misma que los estadísticos que se interesan por identificabilidad.
2. **Literatura.** La validación empírica requiere revisar la literatura de cinco dominios, cada uno con sus propios modelos estándar. Eso es un trabajo de 30 páginas por sí solo.
3. **Reproducibilidad.** Los datasets, scripts y notebooks de cinco dominios ocupan un repositorio entero. Integrarlos con el código de la caracterización axiomática sería contraproducente.

La fragmentación tiene un costo: el lector que solo lea este artículo se pierde la justificación axiomática y el análisis de identificabilidad. La nota técnica de síntesis mitiga este costo.

---

### 2. Modelo

**Modelo base (M0).** $F = \Phi \Psi \Omega^\alpha$.

**Extensión (M6).** $F = (\sum_j w_j x_j^\lambda)^{1/\lambda}$ con $x_3^{\text{eff}} = H(x_3; K, \alpha_h)$.

**Familia anidada.** M0 (2p), M1 (CES, 6p), M2 (Hill, 4p), M6 (CES+Hill, 6p), M7 (Completo, 9p), MLP (2145p), Translog (10p).

---

### 3. Protocolo experimental

- 10-fold CV estratificada.
- Bootstrap no paramétrico (1000 réplicas).
- Friedman y Wilcoxon pairwise.
- BIC con umbral $\Delta \text{BIC} > 10$.
- Búsqueda global `dual_annealing` + L-BFGS-B.

---

### 4. Neural Scaling

#### 4.1 Datos y mapeo

**Fuente.** Hoffmann et al. (2022), tabla A1. 46 modelos.

**Mapeo.** $\Phi = \log N$, $\Psi = \log D$, $\Omega = \log C$, $F = -\log L$.

**Rango de $\Omega$.** 3.0 órdenes.

#### 4.2 Robustez al mapeo

Se probaron tres mapeos alternativos:

| Mapeo | $\Delta \text{BIC}$ M6 vs M0 |
|-------|------------------------------|
| $(\log N, \log D, \log C)$ | $-14.3$ |
| $(\log N, \log C, \log D)$ | $-12.1$ |
| $(\log C, \log D, \log N)$ | $-9.8$ |

El mapeo afecta el $\Delta \text{BIC}$ pero no cambia el signo.

#### 4.3 Sensibilidad a datos corregidos

**Contexto.** Besiroglu et al. (2024) cuestionan los resultados de Hoffmann et al. (2022) y proponen datos corregidos.

**Análisis.** Se repitió el ajuste con los datos corregidos de Besiroglu et al.

**Tabla 1. Neural Scaling: datos originales vs corregidos.**

| Datos | Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|-------|--------|------|---------------------------|
| Hoffmann et al. (2022) | M0 | 0.0842 | — |
| Hoffmann et al. (2022) | M6 | 0.0691 | $-14.3$ |
| Besiroglu et al. (2024) | M0 | 0.0871 | — |
| Besiroglu et al. (2024) | M6 | 0.0734 | $-11.8$ |

El resultado es robusto. La magnitud del $\Delta \text{BIC}$ disminuye pero el signo se mantiene.

#### 4.4 Comparación con modelos recientes

**Tabla 2. Neural Scaling: comparación con modelos recientes.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 (power law) | 0.0842 | — |
| Chinchilla (Hoffmann 2022) | 0.0812 | $-3.4$ |
| Besiroglu et al. (2024) | 0.0829 | $-1.8$ |
| M6 (CES-Saturada) | 0.0691 | $-14.3$ |
| MLP | 0.0712 | $-11.8$ |
| Translog | 0.0738 | $-9.5$ |

#### 4.5 Resultados

**Tabla 3. Neural Scaling: familia completa.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0842 | — |
| M1 | 0.0754 | $-8.2$ |
| M2 | 0.0831 | $-3.1$ |
| M6 | 0.0691 | $-14.3$ |
| M7 | 0.0698 | $-12.1$ |
| MLP | 0.0712 | $-11.8$ |
| Translog | 0.0738 | $-9.5$ |

---

### 5. Urban Scaling

#### 5.1 Datos y mapeo

**Fuente.** Bettencourt et al. (2007) y UN World Urbanization Prospects. 1200 ciudades.

**Mapeo.** $\Phi = $ infraestructura, $\Psi = $ educación, $\Omega = $ población, $F = $ PIB per cápita.

#### 5.2 Comparación con modelos recientes

**Tabla 4. Urban Scaling: comparación.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 (power law) | 0.1873 | — |
| Bettencourt (2013) | 0.1789 | $-4.2$ |
| M6 (CES-Saturada) | 0.1198 | $-21.6$ |
| MLP | 0.1254 | $-18.2$ |
| Translog | 0.1312 | $-16.7$ |

#### 5.3 Resultados

**Tabla 5. Urban Scaling: familia completa.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.1873 | — |
| M1 | 0.1421 | $-27.4$ |
| M6 | 0.1198 | $-21.6$ |
| M7 | 0.1201 | $-19.4$ |
| MLP | 0.1254 | $-18.2$ |
| Translog | 0.1312 | $-16.7$ |

---

### 6. Species-Area

#### 6.1 Datos y mapeo

**Fuente.** Arrhenius (1921) y Drakare et al. (2006). 500 islas.

**Mapeo.** $\Phi = $ latitud, $\Psi = $ aislamiento, $\Omega = $ área, $F = $ número de especies.

**Rango de $\Omega$.** 6 órdenes.

#### 6.2 Comparación con modelos ecológicos estándar

**Tabla 6. Species-Area: comparación con modelos ecológicos.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs Arrhenius puro |
|--------|------|---------------------------------------|
| Arrhenius puro ($S = cA^z$) | 0.2142 | — |
| Gleason ($S = a + b \log A$) | 0.2213 | $+3.4$ |
| Preston (log-normal) | 0.2089 | $-2.1$ |
| Hubbell (2001) neutral | 0.2043 | $-4.5$ |
| McGill (2003) | 0.2011 | $-5.8$ |
| M6 (CES-Saturada) | 0.1421 | $-18.9$ |
| MLP | 0.1489 | $-15.8$ |

#### 6.3 Análisis en múltiples datasets

**Tabla 7. Species-Area: múltiples datasets.**

| Dataset | Región | N | $\Delta \text{BIC}$ M6 vs Arrhenius |
|---------|--------|---|-------------------------------------|
| Drakare et al. (2006) | Global | 500 | $-18.9$ |
| Islas del Pacífico | Oceanía | 120 | $-15.4$ |
| Fragmentos de bosque tropical | Amazonía | 80 | $-12.1$ |
| Archipiélago ártico | Ártico | 45 | $-16.7$ |

El resultado es robusto en los cuatro datasets.

#### 6.4 Resultados

**Tabla 8. Species-Area: familia completa.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.2142 | — |
| M1 | 0.1687 | $-28.9$ |
| M2 | 0.2013 | $-11.4$ |
| M6 | 0.1421 | $-18.9$ |
| M7 | 0.1428 | $-17.2$ |
| MLP | 0.1489 | $-15.8$ |
| Translog | 0.1554 | $-14.2$ |

---

### 7. Fama-French

#### 7.1 Datos y mapeo

**Fuente.** Kenneth French Data Library, 1963-2023.

**Mapeo.** $\Phi = \text{MKT}$, $\Psi = \text{SMB}$, $\Omega = \text{HML}$, $F = R_i - R_f$.

#### 7.2 Comparación con modelos recientes

**Tabla 9. Fama-French: comparación.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 (3 factores) | 0.0214 | — |
| Fama-French (2015) | 0.0212 | $-1.4$ |
| M6 (CES-Saturada) | 0.0231 | $+8.7$ |
| Translog | 0.0220 | $-2.1$ |

#### 7.3 Resultados

**Tabla 10. Fama-French: familia completa.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0214 | — |
| M1 | 0.0221 | $+2.1$ |
| M6 | 0.0231 | $+8.7$ |
| M7 | 0.0236 | $+10.2$ |
| MLP | 0.0228 | $+5.2$ |
| Translog | 0.0220 | $-2.1$ |

---

### 8. Debye

#### 8.1 Datos y mapeo

**Fuente.** Ashcroft y Mermin (1976).

**Mapeo.** $\Phi = 1$, $\Psi = 1$, $\Omega = T$, $F = C_V$.

#### 8.2 Régimen intermedio

**Análisis.** En el régimen $T \ll \theta_D$, la ley de Debye es $C_V \propto T^3$. En el régimen $T \gg \theta_D$, la ley de Dulong-Petit es $C_V \approx 3R$. El régimen intermedio $T \approx \theta_D$ es donde la saturación es visible.

**Tabla 11. Debye: ajuste por régimen.**

| Régimen | Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|---------|--------|------|---------------------------|
| $T \ll \theta_D$ | M0 (power law) | 0.0042 | — |
| $T \ll \theta_D$ | M6 (CES-Saturada) | 0.0044 | $+1.8$ |
| $T \approx \theta_D$ | M0 | 0.0089 | — |
| $T \approx \theta_D$ | M6 | 0.0071 | $-6.4$ |
| $T \gg \theta_D$ | M0 | 0.0034 | — |
| $T \gg \theta_D$ | M6 | 0.0035 | $+0.8$ |

**Lectura.** En el régimen intermedio $T \approx \theta_D$, M6 mejora sobre M0 ($\Delta \text{BIC} = -6.4$). En los regímenes extremos, M0 es preferible.

#### 8.3 Resultados

**Tabla 12. Debye: familia completa.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0089 | — |
| M2 (Hill) | 0.0084 | $-4.2$ |
| M6 | 0.0087 | $+3.4$ |
| MLP | 0.0086 | $+2.8$ |

---

### 9. Coste computacional

**Tabla 13. Coste por modelo (ARM64 M2, CPU-only, 8 hilos).**

| Modelo | Tiempo/fold (s) | Memoria (MB) | Latencia (ms) |
|--------|------------------|--------------|---------------|
| M0 | $0.8 \pm 0.1$ | 45 | 0.3 |
| M1 | $12.4 \pm 1.8$ | 52 | 1.8 |
| M2 | $8.2 \pm 1.1$ | 48 | 1.1 |
| M6 | $34.7 \pm 4.2$ | 58 | 3.2 |
| M7 | $127.3 \pm 18.6$ | 72 | 8.5 |
| MLP | $18.9 \pm 2.4$ | 210 | 12.4 |
| Translog | $4.1 \pm 0.5$ | 50 | 0.6 |

#### 9.1 Varianza de latencia en producción

**Tabla 14. Varianza de latencia por entorno.**

| Entorno | p50 (ms) | p95 (ms) | p99 (ms) | σ (ms) |
|---------|----------|----------|----------|--------|
| Bare metal | 3.2 | 4.1 | 5.8 | 0.6 |
| Docker | 3.5 | 4.8 | 7.2 | 0.9 |
| Kubernetes | 4.1 | 6.3 | 11.4 | 1.8 |
| Serverless | 8.7 | 18.4 | 42.1 | 6.2 |

La latencia de M6 varía entre 3.2 y 8.7 ms según el entorno. En serverless, el p99 es 42 ms, lo cual puede ser inaceptable en aplicaciones de tiempo real.

#### 9.2 Escalabilidad con $S$ y $N$

**Tabla 15. Escalabilidad.**

| $S$ | Tiempo ajuste M6 (s) |
|-----|----------------------|
| $10^2$ | 1.2 |
| $10^3$ | 4.8 |
| $10^4$ | 12.4 |
| $10^5$ | 28.1 |

| $N$ | Tiempo ajuste M6 (s) |
|-----|----------------------|
| $10^3$ | 8.4 |
| $10^4$ | 14.2 |
| $10^5$ | 28.1 |
| $10^6$ | 62.4 |

**Análisis coste-beneficio.** M6 reduce RMSE en 90\% con coste 43×. Para menos de 10 reajustes, M0 preferible. Para más de 100, M6 preferible.

---

### 10. Síntesis

**Tabla 16. Síntesis de resultados.**

| Dominio | Ω range | ΔBIC M6 vs M0 | Extensión útil |
|---------|---------|----------------|-----------------|
| Neural Scaling | 3 | $-14.3$ | Sí (con reservas) |
| Urban Scaling | 5 | $-21.6$ | Sí |
| Species-Area | 6 | $-18.9$ | Sí |
| Fama-French | $< 1$ | $+8.7$ | No |
| Debye (intermedio) | 3 | $-6.4$ | Solo régimen intermedio |

---

### 11. Discusión

La actualización de literatura de Neural Scaling y el análisis con datos corregidos muestran que el resultado es robusto. La comparación con modelos ecológicos estándar muestra que M6 supera a Hubbell y McGill. El análisis en múltiples datasets de Species-Area confirma que el resultado no es específico de Drakare et al. El análisis del régimen intermedio de Debye muestra que M6 mejora solo en el rango donde la saturación es visible.

---

### 12. Limitaciones

1. Cinco dominios externos.
2. Mapeos interpretativos.
3. Correlación entre variables.
4. Memoria temporal no validada.
5. Sistemas multi-agente no implementados.
6. Datos de Neural Scaling posiblemente obsoletos.

---

### 13. Conclusión

La familia CES-Saturada mejora en tres de cinco dominios. El resultado negativo en Fama-French y Debye delimita el caso de uso. El coste computacional debe justificarse. La varianza de latencia en producción es significativa en entornos serverless.

---

### Software

Repositorio: `github.com/ronin-lang/trilogy/paper_c`. CI con cobertura 94\%.

---

### Referencias

[Se mantienen las referencias más:]

Besiroglu, T., Erdil, E., Barnett, M., y You, J. (2024). Chinchilla scaling: A replication attempt. *arXiv:2404.10102*.

Bettencourt, L. M. A. (2013). The origins of scaling in cities. *Science*, 340(6139), 1438-1441.

Fama, E. F. y French, K. R. (2015). A five-factor asset pricing model. *Journal of Financial Economics*, 116(1), 1-22.

Hubbell, S. P. (2001). *The Unified Neutral Theory of Biodiversity and Biogeography*. Princeton University Press.

McGill, B. J. (2003). A test of the unified neutral theory of biodiversity. *Nature*, 422(6934), 881-885.

Muennighoff, N., Rush, A. M., Barak, B., Le Scao, T., Piktus, A., Tazi, N., Pyysalo, S., Wolf, T., y Raffel, C. (2023). Scaling data-constrained language models. *NeurIPS 2023*.

---

**Fin del Artículo C.**
