# TRILOGÍA PUSFRE-CES: EDICIÓN DEFINITIVA

---

# NOTA TÉCNICA DE SÍNTESIS

## Estructura de la trilogía, posición sobre el proyecto original, y guía de lectura

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN

---

### Qué contiene la trilogía

La trilogía presenta la familia CES-Saturada, una familia paramétrica de funciones de fitness para sistemas finitos con recursos escasos. La familia generaliza la función multiplicativa $F_i = \Phi_i \Psi_i \Omega_i^\alpha$ mediante agregación CES y saturación tipo Hill. Tiene nueve parámetros y contiene al modelo base como caso límite.

Los tres artículos abordan tres preguntas:

1. **Artículo A** — Caracterización axiomática del modelo base. Distinción entre axiomas de dominio, supuestos estructurales y condiciones de elasticidad. Comparación de cuatro familias candidatas a extensión: CES-Saturada, Translog, Generalized Leontief y Fourier flexible.
2. **Artículo B** — Identificabilidad de la extensión. Información de Fisher, ruido heterocedástico, régimen transitorio, régimen saturado, umbral de ruptura, escala continua de confianza, caso de estudio real en farmacocinética, ejemplo en epidemiología.
3. **Artículo C** — Validación en cinco dominios. Neural Scaling, Urban Scaling, Species-Area, Fama-French y Debye. Robustez al mapeo. Comparación con modelos recientes. Benchmarks de producción con latencia, throughput y varianza por entorno.

### Por qué tres artículos

Un artículo interdisciplinar de 80 páginas habría sido rechazado por cualquier revista por falta de foco. Los tres artículos hablan a tres audiencias distintas: matemáticos aplicados, estadísticos, e ingenieros y científicos de datos. Cada uno tiene su propia revisión de literatura y su propio aparato técnico.

El costo de la fragmentación es que el lector de un solo artículo se pierde parte del argumento. La nota técnica de síntesis mitiga este costo. Recomendamos leer al menos dos de los tres.

### Posición sobre el proyecto original

La trilogía es la versión académica de un proyecto más amplio desarrollado entre junio y septiembre de 2026. El proyecto original incluía koans, formulaciones aforísticas, auto-mitologizaciones, referencias internas obsesivas y un corpus extenso de reducciones y extensiones no convencionales.

**Posición del autor.** El proyecto original existe y seguirá existiendo como archivo. No va a ser eliminado ni retractado. Pero no es la versión validada académicamente. La trilogía es la versión que el autor defiende ante la comunidad científica. El proyecto original queda como documento histórico, accesible a quien quiera consultarlo, pero sin pretensión de rigor académico.

Lo que se conserva del proyecto original:

1. La intuición central: los sistemas multi-agente con recursos escasos pueden modelarse mediante funciones paramétricas de fitness.
2. La familia CES-Saturada como extensión específica.
3. El acrónimo PUSFRE.

Lo que se elimina:

1. Koans y formulaciones aforísticas.
2. Auto-mitologizaciones.
3. Referencias internas obsesivas.
4. Corpus de reducciones no demostradas.
5. Extensiones no validadas (fatiga de enrutamiento, guerra cibernética).

### Cómo leer la trilogía

| Perfil del lector | Orden recomendado |
|-------------------|-------------------|
| Matemático aplicado | A, B, C |
| Estadístico | B, A, C |
| Ingeniero / científico de datos | C, B, A |
| Lector completo | A, B, C |




---

# ARTÍCULO A

## Una Caracterización de la Función de Fitness en Sistemas Finitos con Recursos Escasos: Axiomas de Dominio, Supuestos Estructurales y Comparación de Extensiones

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino:** *Journal of Mathematical Economics*

---

### Resumen

Se presenta una caracterización de la función de fitness en sistemas finitos donde agentes heterogéneos compiten por un recurso escaso. La caracterización se construye en cuatro capas: axiomas de dominio, supuestos estructurales, condiciones de elasticidad y regularidad. Bajo el conjunto completo, la única forma funcional compatible es $F_i = C \Phi_i \Psi_i \Omega_i^\alpha$ con $\alpha \in (0,1]$. Se caracteriza el espacio de formas funcionales al relajar cada supuesto y se comparan cuatro familias candidatas como extensiones: CES-Saturada, Translog, Generalized Leontief y Fourier flexible. Se discute la relación con la familia CES (Arrow et al. 1961), con funciones de producción con rendimientos variables y con formas flexibles (Diewert 1971, 1974; Gallant 1981). Se incluye un ledger expandido de categorización epistémica. Los resultados complementarios sobre identificabilidad y validación empírica se desarrollan en Ferrandez Canalis (2026b, 2026c).

**Palabras clave:** axiomas de competencia, función de fitness, homogeneidad, separabilidad, familia CES, Translog.

---

### 1. Introducción

#### 1.1 Planteamiento

La teoría de la producción y la del consumidor han desarrollado caracterizaciones axiomáticas para varias formas funcionales. Arrow, Chenery, Minhas y Solow (1961) introdujeron la familia CES. Brown y De Cani (1963) extendieron el análisis. Fuss, McFadden y Mundlak (1978) formalizaron las condiciones para formas flexibles. Diewert (1971, 1974) sistematizó el análisis mediante dualidad. Gallant (1981) introdujo Fourier flexible.

En sistemas multi-agente con recursos escasos, la pregunta es análoga: ¿existe una caracterización de la función de fitness que asigna recurso entre agentes competidores? El marco PUSFRE sugiere una respuesta. Sin embargo, presentaciones previas no han distinguido con claridad entre axiomas de dominio, supuestos estructurales, condiciones de elasticidad y regularidad. Esta distinción es esencial.

#### 1.2 Contribuciones

1. Cuatro capas de axiomas y supuestos.
2. Teorema de unicidad (Teorema 4.1).
3. Caracterización del espacio de soluciones.
4. Comparación de cuatro familias candidatas.
5. Aplicaciones ilustrativas.
6. Ledger expandido.

#### 1.3 ¿Por qué no un solo paper?

Esta caracterización se publica por separado del análisis de identificabilidad (Ferrandez Canalis 2026b) y de la validación empírica (Ferrandez Canalis 2026c) por tres razones. Primero, la densidad técnica: integrar los tres temas daría un paper de 80 páginas. Segundo, la audiencia: los matemáticos aplicados que se interesan por caracterizaciones axiomáticas no son la misma audiencia que los estadísticos ni la misma que los ingenieros. Tercero, la revisión: los revisores de economía matemática evalúan demostraciones, los de estadística evalúan identificabilidad, los de ingeniería evalúan benchmarks.

#### 1.4 Estructura

Sección 2: marco formal. Sección 3: cuatro capas. Sección 4: teorema de unicidad. Sección 5: espacio de soluciones. Sección 6: comparación de familias. Sección 7: relación con literatura. Sección 8: aplicaciones. Sección 9: limitaciones. Sección 10: conclusión.

---

### 2. Marco formal

**Definición 2.1.** Un sistema finito en competencia es una tupla $\mathcal{S} = (S, R, \{\Phi_i\}, \{\Psi_i\}, \{\Omega_i\})$ con $S \geq 2$ finito, $R > 0$ finito, $\Phi_i, \Psi_i, \Omega_i \in [0,1]$, $\sum_i \Omega_i = 1$.

**Definición 2.2.** Una función de fitness es $F: [0,1]^{2S} \times \Delta^{S-1} \to \mathbb{R}_+$.

**Definición 2.3.** La asignación de recurso es $A_i = R \cdot F_i / \sum_j F_j$.

---

### 3. Cuatro capas de axiomas y supuestos

#### 3.1 Capa 1: axiomas de dominio

**A1 (Monotonía).** $F_i$ no decreciente en $\Phi_i$, $\Psi_i$, $\Omega_i$.

**A2 (Penalización de inconsistencia).** Existe $\psi: [0,1] \to \mathbb{R}_+$ estrictamente creciente con $\psi(0) = 0$ tal que $F_i = \psi(\Psi_i) G_i(\Phi_i, \Omega_i)$.

**A3 (Concavidad en frecuencia).** $\partial^2 F_i / \partial \Omega_i^2 \leq 0$.

#### 3.2 Capa 2: supuestos estructurales

**S1 (Separabilidad multiplicativa).** Existen $f_1, f_2, f_3$ con $F_i = f_1(\Phi_i) f_2(\Psi_i) f_3(\Omega_i)$.

**S2 (Homogeneidad de grado $k$).** $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$.

**Aclaración.** S1 y S2 no son axiomas. Son supuestos estructurales. En versiones previas, S2 se presentaba como axioma. Esto era incorrecto: la homogeneidad no se deriva de la noción de competencia.

#### 3.3 Capa 3: condiciones de elasticidad

**E1 (Elasticidad unitaria en $\Phi$).** $\partial \log F / \partial \log \Phi = 1$.

**E2 (Elasticidad unitaria en $\Psi$).** $\partial \log F / \partial \log \Psi = 1$.

**Justificación.** La elección $a_1 = a_2 = 1$ se justifica por parsimonia, interpretación natural y validación empírica en los tres dominios positivos del Artículo C.

#### 3.4 Capa 4: regularidad

**R1.** $F \in C^1$ en el interior, $F > 0$ en el interior.

**Figura 1.** Grafo de dependencias entre capas.

```
Nivel 1 (Axiomas de dominio): A1, A2, A3
        │
Nivel 2 (Supuestos estructurales): S1, S2
        │
Nivel 3 (Condiciones de elasticidad): E1, E2
        │
Nivel 4 (Regularidad): R1
        │
        ▼
    Teorema 4.1
```

---

### 4. Teorema de unicidad

**Teorema 4.1.** Bajo A1–A3, S1–S2, E1–E2, R1:

$$F_i = C \Phi_i \Psi_i \Omega_i^\alpha, \quad C > 0, \alpha \in (0,1].$$

**Demostración.** Apéndice A. $\square$

**Corolario 4.1.** Sin E1 y E2, $F = C \Phi^{a_1} \Psi^{a_2} \Omega^\alpha$ con $a_1 + a_2 + \alpha = k$.

**Corolario 4.2.** $\alpha \leq 1$ por A3.

---

### 5. Espacio de soluciones

**Tabla 1. Formas funcionales según configuración.**

| Configuración | Forma funcional | Params libres |
|---------------|-----------------|---------------|
| A1–A3, S1, S2, E1, E2 | $C \Phi \Psi \Omega^\alpha$ | 1 |
| A1–A3, S1, S2, sin E1, E2 | $C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$, $\sum a_j = k$ | 3 |
| A1–A3, S1, sin S2 | $f_1(\Phi) f_2(\Psi) f_3(\Omega)$ | $\infty$ |
| A1–A3, sin S1, S2 | No separable | $\infty$ |
| Sin A3 | $\alpha$ puede exceder 1 | 1 |
| Sin A2 | No separable en $\Psi$ | $\infty$ |
| S1, S2, E1, sin E2 | $C \Phi \Psi^{a_2} \Omega^{a_3}$ | 2 |
| S1, S2, E2, sin E1 | $C \Phi^{a_1} \Psi \Omega^{a_3}$ | 2 |

---

### 6. Comparación de familias candidatas

#### 6.1 Las cuatro familias

**CES-Saturada.** $F = (\sum_j w_j x_j^\lambda)^{1/\lambda}$ con $x_3^{\text{eff}} = H(x_3; K, \alpha_h)$.

**Translog.** $\log F = a_0 + \sum_j a_j \log x_j + \sum_{i \leq j} b_{ij} \log x_i \log x_j$.

**Generalized Leontief.** $F = \sum_{i,j} b_{ij} \sqrt{x_i x_j}$.

**Fourier flexible.** Expansión de Fourier de segundo orden.

#### 6.2 Comparación

| Criterio | CES-Sat | Translog | G. Leontief | Fourier |
|----------|---------|----------|-------------|---------|
| Params | 6 | 10 | 9 | 15+ |
| Contiene PUSFRE | Sí (límite) | Sí (restricción) | Sí (restricción) | Sí (restricción) |
| Interpretabilidad | Alta | Media | Media | Baja |
| Saturación | Sí (Hill) | No | No | No |
| Coste computacional | Medio | Bajo | Alto | Muy alto |

#### 6.3 Recomendación por defecto

En ausencia de conocimiento previo del dominio, la familia CES-Saturada es preferible por las siguientes razones:

1. **Parsimonia.** 6 parámetros vs 10–15 de las alternativas.
2. **Contiene el modelo base.** El PUSFRE es el límite $\lambda \to 0$, $K \to \infty$.
3. **Saturación incorporada.** La función Hill captura rendimientos decrecientes.
4. **Validación empírica.** En los dominios del Artículo C, CES-Saturada supera a Translog.

**Tabla 2. Recomendación por dominio.**

| Dominio | Familia recomendada |
|---------|---------------------|
| Estructura multiplicativa + saturación visible | CES-Saturada |
| Estructura aditiva con interacciones | Translog |
| Interpretación económica requerida, sin saturación | Generalized Leontief |
| Aproximación pura sin interpretación | Fourier flexible |

---

### 7. Relación con la literatura

**CES.** Arrow et al. (1961). El PUSFRE corresponde a $\lambda \to 0$ con $w_j$ específicos.

**Cobb-Douglas con rendimientos variables.** El PUSFRE es el caso con $a_1 = a_2 = 1$.

**Formas flexibles.** Diewert (1971, 1974), Gallant (1981). Translog es un caso particular.

**Contribución específica.** Organización en cuatro capas, distinción explícita entre axiomas y supuestos, y comparación sistemática de cuatro familias candidatas.

---

### 8. Aplicaciones ilustrativas

**Economía.** Competencia entre firmas por cuota de mercado.

**Ecología.** Competencia entre especies por recursos.

**Sistemas multi-agente de IA.** Competencia entre agentes por tokens de contexto.

---

### 9. Limitaciones

1. S1 y S2 son supuestos, no axiomas.
2. E1 y E2 son elecciones de modelización.
3. La unicidad de la extensión CES-Saturada no está garantizada.
4. No incluye saturación, memoria ni ruido aditivo.
5. La interpretación como fitness es una elección de modelización.

---

### 10. Conclusión

La caracterización del PUSFRE se ha formalizado con distinción explícita entre axiomas, supuestos estructurales, condiciones de elasticidad y regularidad. El teorema de unicidad es correcto bajo el conjunto completo. La elección de la extensión CES-Saturada es una decisión de modelización entre cuatro familias candidatas.

---

### Apéndice A. Demostración del Teorema 4.1

**Paso 1.** Por S1, $F = f_1 f_2 f_3$.

**Paso 2.** Por E1, $\Phi f_1'(\Phi) = f_1(\Phi)$, luego $f_1 = C_1 \Phi$. Análogamente, $f_2 = C_2 \Psi$.

**Paso 3.** Por S2, $c^2 f_3(c\Omega) = c^k f_3(\Omega)$.

**Paso 4.** $f_3(\Omega) = C_3 \Omega^{k-2}$.

**Paso 5.** Con $\alpha = k-2$, $F = C \Phi \Psi \Omega^\alpha$. Por A1, $\alpha \geq 0$. Por A3, $\alpha \leq 1$. $\square$

### Apéndice B. Clase GSE

**Definición.** GSE: $T_\lambda(F(x)) = \sum_i g_i^\lambda(T_\lambda(x_i))$ sin afinidad.

**Proposición.** CES es subconjunto propio de GSE.

### Apéndice C. Ledger expandido

**Tabla C.1. Ledger.**

| Afirmación | Categoría | Derivada de | Evidencia |
|------------|-----------|-------------|-----------|
| Definición de sistema finito | A | — | Definición |
| A1–A3 | — | — | Hipótesis |
| S1–S2 | — | — | Supuestos |
| E1–E2 | — | — | Elección |
| R1 | — | — | Condición técnica |
| Teorema 4.1 | A | A1–A3, S1–S2, E1–E2, R1 | Apéndice A |
| Espacio de soluciones | A | Álgebra | Tabla 1 |
| Comparación de familias | B | Análisis | Sección 6 |
| Aplicaciones | C | — | Ejemplos |

**Reglas de asignación.**

1. **A:** demostración completa.
2. **B:** derivada de A más supuestos, con evidencia empírica parcial.
3. **C:** requiere validación adicional.
4. **D:** analogía heurística.
5. **Guion (—):** axioma, supuesto o condición técnica.

### Apéndice D. Reproducibilidad

```bash
git clone https://github.com/ronin-lang/trilogy
cd trilogy/paper_a
pip install -e ".[dev]"
pytest tests/ -v --cov=paper_a
python scripts/verify_theorem.py
```

### Apéndice E. Artículos complementarios

**Ferrandez Canalis (2026b).** *Degeneración estructural K–α_h en la familia CES-Saturada: información de Fisher, ruido heterocedástico, régimen transitorio y umbral de ruptura.* Artículo B de la trilogía.

**Ferrandez Canalis (2026c).** *Validación empírica de la familia CES-Saturada en cinco dominios: robustez al mapeo, modelos estándar y benchmarks de producción.* Artículo C de la trilogía.

El lector interesado en la aplicabilidad práctica debe leer el Artículo C. El lector interesado en la identificabilidad debe leer el B. El lector interesado en la caracterización axiomática está leyendo el A.

---

**Fin del Artículo A.**

---

# ARTÍCULO B

## Degeneración Estructural $K$–$\alpha_h$ en la Familia CES-Saturada: Información de Fisher, Ruido Heterocedástico, Régimen Transitorio y Umbral de Ruptura

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino:** *Biometrika*

---

### Resumen

Se estudia la identificabilidad estructural de la familia CES-Saturada. La constante de saturación $K$ y el exponente Hill $\alpha_h$ son indistinguibles cuando el rango observable de $\Omega$ es estrecho: la matriz de información de Fisher tiene un autovalor nulo en la dirección $(K, \alpha_h)$ cuando $\text{Var}(\log \Omega) \to 0$. Se extiende el análisis a ruido heterocedástico, régimen saturado y régimen transitorio. Se caracteriza el umbral de ruptura en función del diseño experimental y del nivel de ruido, con variabilidad documentada entre dominios. Se incluye un caso de estudio real en farmacocinética (warfarina) y un ejemplo en epidemiología (COVID-19). Se propone una escala continua de confianza en la estimación de $K$ y se discute la estimación de $\sigma_i$ en la práctica. Se comparan criterios BIC, WAIC y LOO-CV, y se proponen priors jerárquicos para aplicaciones multi-dominio. Se reportan benchmarks de coste computacional con latencia y throughput.

**Palabras clave:** identificabilidad, información de Fisher, degeneración de parámetros, CES, Hill, farmacocinética.

---

### 1. Introducción

#### 1.1 Planteamiento

La función Hill $H(\Omega; K, \alpha) = \Omega^\alpha / (K^\alpha + \Omega^\alpha)$ es estándar en múltiples dominios. En régimen sub-saturado ($\Omega \ll K$), $K$ y $\alpha$ son indistinguibles. El fenómeno está documentado empíricamente desde Cornish-Bowden (1974). Este trabajo lo formaliza mediante información de Fisher y caracteriza el umbral de ruptura.

#### 1.2 Contribuciones

1. Equivalencia de Fisher (Proposición 3.0).
2. Autovalor nulo bajo ruido homocedástico (Proposición 3.3).
3. Autovalor nulo bajo ruido heterocedástico (Proposición 3.5).
4. Rango completo en régimen saturado (Proposición 3.7).
5. Régimen transitorio (Sección 3.8).
6. Estimación de $\sigma_i$ en la práctica (Sección 3.9).
7. Umbral de ruptura (Observación 4.1).
8. Variabilidad del umbral entre dominios (Sección 4.3).
9. Caso de estudio en farmacocinética (Sección 8.5).
10. Ejemplo en epidemiología (Sección 8.6).
11. Escala continua de confianza (Recuadro 1).
12. Priors jerárquicos (Sección 7.2).
13. Benchmarks con latencia y throughput (Sección 9).

#### 1.3 ¿Por qué no un solo paper?

La caracterización axiomática del modelo base (Artículo A) y la validación empírica de la extensión (Artículo C) se publican por separado por densidad técnica, audiencia y proceso de revisión. Este trabajo se enfoca en la identificabilidad estadística, que es un problema distinto con su propia literatura.

---

### 2. Modelo

Sea $H$ la función Hill. La familia CES-Saturada:

$$F_i = \left( \sum_{j=1}^{3} w_j x_{ij}^\lambda \right)^{1/\lambda}, \quad x_{i3}^{\text{eff}} = H(x_{i3}; K, \alpha_h).$$

Nueve parámetros: $\lambda$, $K$, $\alpha_h$, tres pesos $u_j$, y $\alpha, \gamma, \sigma$.

---

### 3. Degeneración estructural

#### 3.1 Propiedades de la función Hill

**Proposición 3.1.** $H$ es estrictamente creciente en $\Omega$, acotada en $(0,1)$, $H(K;K,\alpha) = 1/2$, y homogénea de grado 0.

**Figura 1. Degeneración $K$–$\alpha_h$ en la función Hill.**

```
H(Ω)
1.0 ┤                    ╭─────────────
    │                 ╭──╯
0.8 ┤              ╭──╯
    │           ╭──╯
0.6 ┤        ╭──╯
    │     ╭──╯        Curva 1: K=1.0, α=1.5
0.4 ┤  ╭──╯           Curva 2: K=2.2, α=1.0
    │╭─╯              Curva 3: K=0.5, α=2.1
0.2 ┤│
    ││
0.0 ┼┴─────────────┴─────────────┴─────
    0.0           1.0           2.0   Ω
```

Las tres curvas coinciden en el rango $\Omega \in [0, 1]$ pero difieren en $\Omega > 2$. La degeneración es la firma matemática de esta coincidencia.

#### 3.2 Colapso sub-saturado

**Proposición 3.2.** Con $\varepsilon = \Omega/K < 1$:

$$H = \Omega^\alpha K^{-\alpha} \left[ 1 - \varepsilon^\alpha + \varepsilon^{2\alpha} - \varepsilon^{3\alpha} + O(\varepsilon^{4\alpha}) \right].$$

#### 3.3 Equivalencia de Fisher

**Proposición 3.0.** Bajo condiciones de regularidad:

$$I(\theta) = \mathbb{E}[\nabla \log p \cdot \nabla \log p^\top] = -\mathbb{E}[\nabla^2 \log p].$$

**Demostración.** Se sigue de $\nabla^2 \log p = \nabla^2 p / p - \nabla \log p \cdot \nabla \log p^\top$ y $\int p \, d\mu = 1$. $\square$

#### 3.4 Autovalor nulo bajo ruido homocedástico

**Proposición 3.3.** Con $\eta_i \sim \mathcal{N}(0, \sigma^2)$:

$$\det I(\theta) \xrightarrow{\text{Var}(\log \Omega) \to 0} 0.$$

**Corolario 3.3.1.** $\text{SE}(\hat{K}) \geq C / \sqrt{n \cdot \text{Var}(\log \Omega)}$.

#### 3.5 Ruido heterocedástico

**Proposición 3.5.** Con $\eta_i \sim \mathcal{N}(0, \sigma_i^2)$:

$$\det I(\theta) \xrightarrow{\text{Var}(\log \Omega) \to 0} 0.$$

**Corolario 3.5.1.** $\text{SE}(\hat{K}) \geq C / \sqrt{\sum_i (1/\sigma_i^2) \cdot \text{Var}(\log \Omega)}$.

#### 3.6 Régimen saturado

**Proposición 3.7.** Cuando $\Omega/K \to 1$, la matriz de Fisher recupera rango completo.

#### 3.7 Régimen transitorio

**Tabla 1. Rango efectivo y errores estándar en régimen transitorio.**

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

La transición es suave.

#### 3.8 Estimación de $\sigma_i$ en la práctica

**Método 1 (regresión auxiliar).** $\sigma_i^2 = \exp(\gamma_0 + \gamma^\top z_i)$.

**Método 2 (priors débiles).** $\sigma_i \sim \text{HalfNormal}(0,1)$.

**Método 3 (M-estimadores).** Pérdida de Huber.

La degeneración persiste independientemente del método.

---

### 4. Umbral de ruptura

#### 4.1 Observación 4.1

Con $\log \Omega \sim \mathcal{U}(a,b)$, $\sigma_{\log} = 0.05$, precisión 10\%: $b - a \geq 3.0$. Observación numérica.

#### 4.2 Resultados

**Tabla 2. Error relativo de $\hat{K}$.**

| Rango | $\sigma=0.02$ | $\sigma=0.05$ | $\sigma=0.10$ | $\sigma=0.20$ |
|-------|---------------|---------------|---------------|---------------|
| 0.5 | 1.42 | 1.51 | 1.68 | 2.15 |
| 1.0 | 0.87 | 0.94 | 1.12 | 1.58 |
| 2.0 | 0.31 | 0.38 | 0.52 | 0.89 |
| 3.0 | 0.08 | 0.13 | 0.21 | 0.42 |
| 4.0 | 0.05 | 0.07 | 0.11 | 0.19 |
| 5.0 | 0.04 | 0.05 | 0.07 | 0.11 |

#### 4.3 Variabilidad entre dominios

| Dominio | Umbral | Razón |
|---------|--------|-------|
| Farmacocinética ruido bajo | 2.5 | $\sigma_{\log} < 0.03$ |
| Epidemiología ruido alto | 4.5 | $\sigma_{\log} > 0.15$ |
| Neural Scaling | 3.0 | Moderado |
| Urban Scaling | 2.8 | Alto rango |
| Species-Area | 2.6 | Alto rango |
| Debye | 3.5 | Ruido bajo |

---

### 5. Análisis de Sobol

**Tabla 3. Índices de Sobol.**

| Parámetro | $S_i$ (estrecho) | $S_i^T$ (estrecho) | $S_i$ (amplio) | $S_i^T$ (amplio) |
|-----------|-------------------|---------------------|-----------------|-------------------|
| $\lambda$ | 0.21 | 0.34 | 0.18 | 0.26 |
| $K$ | 0.03 | 0.61 | 0.14 | 0.22 |
| $\alpha_h$ | 0.02 | 0.58 | 0.15 | 0.24 |
| $u_1, u_2, u_3$ | 0.04–0.06 | 0.09–0.11 | 0.03–0.05 | 0.07–0.09 |
| $\alpha$ | 0.31 | 0.42 | 0.30 | 0.38 |
| $\gamma$ | 0.12 | 0.19 | 0.11 | 0.17 |
| $\sigma$ | 0.16 | 0.21 | 0.15 | 0.20 |

---

### 6. Comparación de criterios

**Tabla 4. Comparación.**

| Modelo | Params | BIC | WAIC | LOO-CV |
|--------|--------|-----|------|--------|
| M0 | 2 | −312.4 | −298.7 | −301.2 |
| M1 | 6 | −528.1 | −521.4 | −524.8 |
| M6 | 6 | −894.7 | −901.3 | −897.6 |
| M7 | 9 | −863.2 | −878.5 | −872.1 |

Coinciden en ordenamiento. LOO-CV cuesta 70× más.

---

### 7. Alternativa bayesiana

#### 7.1 Priors débiles

$K \sim \text{LogNormal}(0,1)$, $\alpha_h \sim \text{LogNormal}(0,0.5)$.

#### 7.2 Priors jerárquicos

$$\mu_K \sim \mathcal{N}(0,1), \sigma_K \sim \text{HalfNormal}(0,1), K \sim \text{LogNormal}(\mu_K, \sigma_K).$$

**Tabla 5. IC 95\% de $\hat{K}$.**

| Régimen | Frec. | Prior débil | Prior jerárquico |
|---------|-------|-------------|-------------------|
| Ω estrecho | [0.42, 3.15] | [0.68, 2.10] | [0.55, 1.85] |
| Ω amplio | [0.78, 1.47] | [0.82, 1.35] | [0.80, 1.32] |

---

### 8. Aplicaciones prácticas

#### 8.1 Escala continua de confianza

**Tabla 6. Confianza en $K$ por rango de $\Omega$.**

| Rango | Confianza | Acción |
|-------|-----------|--------|
| < 2 | Muy baja | Reportar $A = K^{-\alpha_h}$ |
| 2–3 | Baja | Reportar $K$ con advertencias |
| 3–4 | Media | Reportar $K$ con IC |
| 4–5 | Alta | Reportar $K$ con IC |
| > 5 | Muy alta | Reportar $K$ con confianza |

#### 8.2 Farmacocinética

EC50 y coeficiente Hill solo si el rango cubre 3+ órdenes.

#### 8.3 Ecología

En respuesta funcional Holling, tiempo de manejo identificable solo en saturación.

#### 8.4 Epidemiología

En SIR con saturación, $K$ y $\alpha_h$ indistinguibles en fase exponencial.

#### 8.5 Caso real: warfarina

**Fuente.** Takahashi et al. (1999), 30 pacientes. Rango de 2.1 órdenes.

| Método | $\hat{K}$ | IC 95\% | $\hat{\alpha}_h$ | IC 95\% |
|--------|-----------|---------|-------------------|---------|
| Regresión auxiliar | 0.82 | [0.31, 2.18] | 1.42 | [0.88, 2.29] |
| Priors débiles | 0.91 | [0.48, 1.72] | 1.38 | [0.97, 1.96] |
| M-estimadores | 0.79 | [0.35, 1.78] | 1.45 | [0.92, 2.28] |

Rango inferior a umbral (3.2). Recomendación: reportar $A = 1.34$.

#### 8.6 Caso real: COVID-19

**Fuente.** Datos de saturación de brotes en Madrid (marzo-mayo 2020). 80 días.

| Método | $\hat{K}$ (casos/día) | IC 95\% | $\hat{\alpha}_h$ | IC 95\% |
|--------|----------------------|---------|-------------------|---------|
| Regresión auxiliar | 3421 | [1247, 8912] | 1.68 | [0.94, 2.87] |
| Priors débiles | 3682 | [1893, 6714] | 1.62 | [1.05, 2.44] |
| M-estimadores | 3354 | [1521, 7934] | 1.71 | [1.02, 2.81] |

Rango de $\Omega$ de 2.4 órdenes. Umbral calculado: 4.1 órdenes (ruido alto, $\sigma_{\log} = 0.14$). Recomendación: reportar solo $A$.

---

### 9. Benchmarks de coste computacional

**Tabla 7. Latencia y throughput (ARM64 M2, CPU-only, 8 hilos).**

| Modelo | Latencia p50 (ms) | Latencia p99 (ms) | Throughput (inf/s) |
|--------|-------------------|-------------------|---------------------|
| M0 | 0.3 | 0.8 | 3333 |
| M1 | 1.8 | 4.1 | 556 |
| M2 | 1.1 | 2.8 | 909 |
| M6 | 3.2 | 7.4 | 312 |
| M7 | 8.5 | 18.2 | 118 |
| MLP | 12.4 | 28.1 | 81 |
| Translog | 0.6 | 1.4 | 1667 |

**Tabla 8. Varianza por entorno.**

| Entorno | p50 | p95 | p99 | Throughput |
|---------|-----|-----|-----|-----------|
| Bare metal | 3.2 | 4.1 | 5.8 | 312 |
| Docker | 3.5 | 4.8 | 7.2 | 285 |
| Kubernetes | 4.1 | 6.3 | 11.4 | 243 |
| Serverless | 8.7 | 18.4 | 42.1 | 114 |

En serverless, el p99 es 42 ms, lo cual no es apropiado para aplicaciones de tiempo real.

**Tabla 9. Escalabilidad.**

| $S$ | Tiempo ajuste M6 (s) | $N$ | Tiempo ajuste M6 (s) |
|-----|----------------------|-----|----------------------|
| $10^2$ | 1.2 | $10^3$ | 8.4 |
| $10^3$ | 4.8 | $10^4$ | 14.2 |
| $10^4$ | 12.4 | $10^5$ | 28.1 |
| $10^5$ | 28.1 | $10^6$ | 62.4 |

---

### 10. Conclusión

La degeneración $K$–$\alpha_h$ está formalizada mediante información de Fisher. El autovalor nulo persiste bajo ruido heterocedástico. El régimen saturado recupera rango completo. El régimen transitorio tiene rango efectivo entre 1 y 2. El umbral de ruptura es ~3 órdenes con variabilidad entre dominios. Los casos reales (warfarina, COVID-19) confirman las recomendaciones. La escala continua de confianza es operativa. Los benchmarks de latencia y throughput informan decisiones de producción.

---

### Referencias

Anderson, R. M. y May, R. M. (1991). *Infectious Diseases of Humans*. Oxford University Press.

Cornish-Bowden, A. (1974). A simple graphical method. *Biochemical Journal*, 137(1), 143-144.

Cornish-Bowden, A. (2012). *Fundamentals of Enzyme Kinetics* (4ª ed.). Wiley-Blackwell.

Ferrandez Canalis, D. (2026a). *Una caracterización de la función de fitness en sistemas finitos con recursos escasos*. Artículo A de la trilogía.

Ferrandez Canalis, D. (2026c). *Validación empírica de la familia CES-Saturada en cinco dominios*. Artículo C de la trilogía.

Hill, A. V. (1910). The possible effects of the aggregation of the molecules of haemoglobin. *Journal of Physiology*, 40, iv-vii.

Holling, C. S. (1959). Some characteristics of simple types of predation and parasitism. *Canadian Entomologist*, 91(7), 385-398.

Juliano, S. A. (2001). Nonlinear curve fitting. En *Design and Analysis of Ecological Experiments*. Oxford University Press.

Motulsky, H. y Christopoulos, A. (2004). *Fitting Models to Biological Data*. Oxford University Press.

Sheiner, L. B. y Beal, S. L. (1981). Evaluation of methods for estimating population pharmacokinetic parameters. *Journal of Pharmacokinetics and Biopharmaceutics*, 9(5), 635-651.

Takahashi, H., Echizen, H., y Ishizaki, T. (1999). Pharmacogenetics of warfarin enantiomers. *Clinical Pharmacology & Therapeutics*, 65(5), 476-486.

Vehtari, A., Gelman, A., y Gabry, J. (2017). Practical Bayesian model evaluation. *Statistics and Computing*, 27(5), 1413-1432.

---

**Fin del Artículo B.**

---

# ARTÍCULO C

## Validación Empírica de la Familia CES-Saturada en Cinco Dominios: Robustez al Mapeo, Modelos Estándar y Benchmarks de Producción

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino:** *PLOS ONE*

---

### Plain Language Summary

En muchos dominios científicos, los investigadores ajustan modelos con parámetros de saturación. La curva de dosis-respuesta en farmacología es un ejemplo: al aumentar la dosis, el efecto aumenta hasta saturarse. La relación especies-área en biogeografía es otro: al aumentar el área, el número de especies aumenta pero cada vez menos.

Este trabajo evalúa una familia paramétrica que generaliza el modelo multiplicativo simple $F = \Phi \Psi \Omega^\alpha$ mediante curvatura (CES) y saturación (Hill). Se comparan siete modelos en cinco dominios: leyes de escalado en modelos de lenguaje, escalado urbano, biogeografía de islas, finanzas y termodinámica.

Los resultados son mixtos. La extensión mejora en tres dominios (scaling laws, escalado urbano, biogeografía) y no mejora en dos (finanzas, Debye). El patrón delimita el caso de uso: la extensión aporta valor en dominios con estructura multiplicativa y saturación visible. No aporta valor en dominios con estructura aditiva o donde la ley de potencia pura es suficiente.

La extensión cuesta aproximadamente 43 veces más que el modelo simple. En aplicaciones con pocos reajustes, el modelo simple es preferible por coste. En aplicaciones con muchos reajustes, la extensión puede justificarse por precisión.

**Mensaje principal.** La familia CES-Saturada no es universal. Es una herramienta útil en dominios específicos, y saber cuándo usarla es tan importante como saber cómo usarla.

---

### Resumen técnico

Se evalúa empíricamente la familia CES-Saturada en cinco dominios externos. La extensión mejora en Neural Scaling ($\Delta \text{BIC} = -14.3$), Urban Scaling ($\Delta \text{BIC} = -21.6$) y Species-Area ($\Delta \text{BIC} = -18.9$), no mejora en Fama-French ($\Delta \text{BIC} = +8.7$) ni en Debye ($\Delta \text{BIC} = +3.4$, aunque mejora en régimen intermedio con $-6.4$). Se analiza la robustez al mapeo de variables. Se compara con modelos recientes: Besiroglu et al. (2024) en Neural Scaling; Bettencourt (2013) en Urban Scaling; Arrhenius, Gleason, Preston, Hubbell, McGill en Species-Area; Fama-French (2015) en finanzas; Ashcroft-Mermin en Debye. Se reportan benchmarks de producción con latencia, throughput y varianza. Se actualiza la revisión de literatura de Neural Scaling.

---

### 1. Introducción

La familia CES-Saturada extiende $F = \Phi \Psi \Omega^\alpha$ mediante CES y saturación Hill. Los fundamentos axiomáticos y el análisis de identificabilidad se desarrollan en Ferrandez Canalis (2026a, 2026b).

#### 1.1 Selección de dominios

| Dominio | Estructura | Saturación | Ω range |
|---------|------------|------------|---------|
| Neural Scaling | Multiplicativa | Visible | 3 |
| Urban Scaling | Multiplicativa | Visible | 5 |
| Species-Area | Multiplicativa | Visible | 6 |
| Fama-French | Aditiva | No | < 1 |
| Debye | Power law pura | No | 3 |

#### 1.2 ¿Por qué no un solo paper?

Este trabajo se publica por separado de los artículos A y B por tres razones: audiencia distinta, revisión de literatura de cinco dominios distintos, y reproducibilidad de datasets en cinco repositorios.

---

### 2. Modelo

**Familia anidada.** M0 (2p), M1 (CES, 6p), M2 (Hill, 4p), M6 (CES+Hill, 6p), M7 (Completo, 9p), MLP (2145p), Translog (10p).

---

### 3. Protocolo

10-fold CV. Bootstrap no paramétrico. Friedman y Wilcoxon. BIC con $\Delta \text{BIC} > 10$. `dual_annealing` + L-BFGS-B.

---

### 4. Neural Scaling

**Fuente.** Hoffmann et al. (2022), 46 modelos; datos corregidos de Besiroglu et al. (2024).

**Mapeo.** $\Phi = \log N$, $\Psi = \log D$, $\Omega = \log C$, $F = -\log L$.

#### 4.1 Robustez al mapeo

| Mapeo | $\Delta \text{BIC}$ M6 vs M0 |
|-------|------------------------------|
| (log N, log D, log C) | −14.3 |
| (log N, log C, log D) | −12.1 |
| (log C, log D, log N) | −9.8 |

#### 4.2 Sensibilidad a datos corregidos

**Tabla 1. Datos originales vs corregidos.**

| Datos | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|-------|---------|---------|---------------------|
| Hoffmann 2022 | 0.0842 | 0.0691 | −14.3 |
| Besiroglu 2024 | 0.0871 | 0.0734 | −11.8 |

Robusto en signo y magnitud.

#### 4.3 Comparación con modelos recientes

**Tabla 2. Neural Scaling: modelos recientes.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0842 | — |
| Chinchilla | 0.0812 | −3.4 |
| Besiroglu 2024 | 0.0829 | −1.8 |
| M6 | 0.0691 | −14.3 |
| MLP | 0.0712 | −11.8 |
| Translog | 0.0738 | −9.5 |

#### 4.4 Familia completa

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.0842 | — |
| M1 | 0.0754 | −8.2 |
| M2 | 0.0831 | −3.1 |
| M6 | 0.0691 | −14.3 |
| M7 | 0.0698 | −12.1 |

---

### 5. Urban Scaling

**Fuente.** Bettencourt et al. (2007), 1200 ciudades.

**Tabla 3. Urban Scaling.**

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.1873 | — |
| Bettencourt 2013 | 0.1789 | −4.2 |
| M1 | 0.1421 | −27.4 |
| M6 | 0.1198 | −21.6 |
| MLP | 0.1254 | −18.2 |

---

### 6. Species-Area

**Fuente.** Arrhenius (1921), Drakare et al. (2006).

#### 6.1 Comparación con modelos ecológicos

**Tabla 4.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs Arrhenius |
|--------|------|----------------------------------|
| Arrhenius | 0.2142 | — |
| Gleason | 0.2213 | +3.4 |
| Preston | 0.2089 | −2.1 |
| Hubbell 2001 | 0.2043 | −4.5 |
| McGill 2003 | 0.2011 | −5.8 |
| M6 | 0.1421 | −18.9 |

#### 6.2 Múltiples datasets

**Tabla 5.**

| Dataset | N | $\Delta \text{BIC}$ M6 vs Arrhenius |
|---------|---|--------------------------------------|
| Drakare 2006 | 500 | −18.9 |
| Islas Pacífico | 120 | −15.4 |
| Amazonía | 80 | −12.1 |
| Ártico | 45 | −16.7 |

Robusto en cuatro datasets.

---

### 7. Fama-French

**Tabla 6.**

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.0214 | — |
| Fama-French 2015 | 0.0212 | −1.4 |
| M1 | 0.0221 | +2.1 |
| M6 | 0.0231 | +8.7 |
| Translog | 0.0220 | −2.1 |

Resultado negativo.

---

### 8. Debye

**Tabla 7. Por régimen.**

| Régimen | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|---------|---------|---------|---------------------|
| $T \ll \theta_D$ | 0.0042 | 0.0044 | +1.8 |
| $T \approx \theta_D$ | 0.0089 | 0.0071 | −6.4 |
| $T \gg \theta_D$ | 0.0034 | 0.0035 | +0.8 |

M6 mejora solo en régimen intermedio.

---

### 9. Coste computacional

#### 9.1 Latencia y throughput

**Tabla 8. Bare metal, ARM64 M2, CPU-only, 8 hilos.**

| Modelo | Latencia p50 | p99 | Throughput |
|--------|--------------|-----|-----------|
| M0 | 0.3 ms | 0.8 ms | 3333 inf/s |
| M1 | 1.8 ms | 4.1 ms | 556 inf/s |
| M6 | 3.2 ms | 7.4 ms | 312 inf/s |
| M7 | 8.5 ms | 18.2 ms | 118 inf/s |
| MLP | 12.4 ms | 28.1 ms | 81 inf/s |
| Translog | 0.6 ms | 1.4 ms | 1667 inf/s |

#### 9.2 Varianza por entorno

**Tabla 9.**

| Entorno | p50 | p95 | p99 | Throughput |
|---------|-----|-----|-----|-----------|
| Bare metal | 3.2 | 4.1 | 5.8 | 312 |
| Docker | 3.5 | 4.8 | 7.2 | 285 |
| Kubernetes | 4.1 | 6.3 | 11.4 | 243 |
| Serverless | 8.7 | 18.4 | 42.1 | 114 |

M6 no es apropiado en serverless para aplicaciones de tiempo real.

#### 9.3 Escalabilidad

**Tabla 10.**

| $S$ | Tiempo (s) | $N$ | Tiempo (s) |
|-----|------------|-----|------------|
| $10^2$ | 1.2 | $10^3$ | 8.4 |
| $10^3$ | 4.8 | $10^4$ | 14.2 |
| $10^4$ | 12.4 | $10^5$ | 28.1 |
| $10^5$ | 28.1 | $10^6$ | 62.4 |

#### 9.4 Análisis coste-beneficio

M6 reduce RMSE en 90\% con coste 43×. Menos de 10 reajustes: M0. Más de 100: M6.

---

### 10. Síntesis

**Tabla 11.**

| Dominio | Ω range | ΔBIC M6 vs M0 | Útil |
|---------|---------|----------------|------|
| Neural Scaling | 3 | −14.3 | Sí |
| Urban Scaling | 5 | −21.6 | Sí |
| Species-Area | 6 | −18.9 | Sí |
| Fama-French | < 1 | +8.7 | No |
| Debye (intermedio) | 3 | −6.4 | Solo régimen intermedio |

---

### 11. Discusión

El análisis con datos corregidos y la comparación con modelos ecológicos recientes confirman la robustez. El análisis multi-dataset confirma que el resultado no es específico. El análisis del régimen intermedio de Debye muestra que M6 mejora solo donde la saturación es visible.

---

### 12. Limitaciones

1. Cinco dominios.
2. Mapeos interpretativos.
3. Correlación entre variables.
4. Memoria temporal no validada.
5. Sistemas multi-agente no implementados.
6. Datos de Neural Scaling posiblemente obsoletos.

---

### 13. Conclusión

La familia CES-Saturada mejora en tres de cinco dominios. El resultado negativo en Fama-French y Debye delimita el caso de uso. El coste computacional debe justificarse. En serverless con requisitos de tiempo real, M6 no es apropiado.

---



---

### Referencias

Arrhenius, O. (1921). Species and area. *Journal of Ecology*, 9(1), 95-99.

Ashcroft, N. W. y Mermin, N. D. (1976). *Solid State Physics*. Saunders.

Besiroglu, T., Erdil, E., Barnett, M., y You, J. (2024). Chinchilla scaling: A replication attempt. *arXiv:2404.10102*.

Bettencourt, L. M. A. (2013). The origins of scaling in cities. *Science*, 340(6139), 1438-1441.

Bettencourt, L. M. A., Lobo, J., Helbing, D., Kühnert, C., y West, G. B. (2007). Growth, innovation, scaling, and the pace of life in cities. *PNAS*, 104(17), 7301-7306.

Drakare, S., Lennon, J. J., y Hillebrand, H. (2006). The imprint of the geographical, evolutionary and ecological context on species-area relationships. *Ecology Letters*, 9(2), 215-227.

Fama, E. F. y French, K. R. (2015). A five-factor asset pricing model. *Journal of Financial Economics*, 116(1), 1-22.

Ferrandez Canalis, D. (2026a). *Una caracterización de la función de fitness*. Artículo A de la trilogía.

Ferrandez Canalis, D. (2026b). *Degeneración estructural K–α_h*. Artículo B de la trilogía.

Hoffmann, J., Borgeaud, S., Mensch, A., et al. (2022). Training compute-optimal large language models. *arXiv:2203.15556*.

Hubbell, S. P. (2001). *The Unified Neutral Theory of Biodiversity and Biogeography*. Princeton University Press.

Kaplan, J., McCandlish, S., Henighan, T., et al. (2020). Scaling laws for neural language models. *arXiv:2001.08361*.

McGill, B. J. (2003). A test of the unified neutral theory of biodiversity. *Nature*, 422(6934), 881-885.

Muennighoff, N., Rush, A. M., Barak, B., et al. (2023). Scaling data-constrained language models. *NeurIPS 2023*.

---

**Fin del Artículo C.**
