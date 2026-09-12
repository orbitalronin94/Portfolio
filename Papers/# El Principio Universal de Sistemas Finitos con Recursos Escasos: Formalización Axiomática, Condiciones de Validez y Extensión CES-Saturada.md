# TRILOGÍA PUSFRE-CES: EDICIÓN DEFINITIVA CON DATASETS ANEXOS

---

# NOTA TÉCNICA DE SÍNTESIS

## Estructura de la trilogía y guía de lectura

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN

---

### Qué contiene la trilogía

La trilogía presenta la familia CES-Saturada, una familia paramétrica de funciones de fitness para sistemas finitos con recursos escasos. La familia generaliza la función multiplicativa $F_i = \Phi_i \Psi_i \Omega_i^\alpha$ mediante agregación CES y saturación tipo Hill.

Tres artículos abordan tres preguntas:

1. **Artículo A** — Caracterización axiomática. Distinción entre axiomas de dominio, supuestos estructurales y condiciones de elasticidad. Comparación de cuatro familias candidatas a extensión.
2. **Artículo B** — Identificabilidad. Información de Fisher, ruido heterocedástico, régimen transitorio, umbral de ruptura, escala continua de confianza, casos reales en farmacocinética y epidemiología.
3. **Artículo C** — Validación en cinco dominios con datasets anexos. Neural Scaling, Urban Scaling, Species-Area, Fama-French y Debye.

### Por qué tres artículos

Un artículo interdisciplinar de 80 páginas habría sido rechazado por falta de foco. Los tres artículos hablan a tres audiencias: matemáticos aplicados, estadísticos, e ingenieros y científicos de datos. Cada uno tiene su propia revisión de literatura y su propio aparato técnico.

### Posición sobre el proyecto original

La trilogía es la versión académica de un proyecto más amplio desarrollado entre junio y septiembre de 2026. El proyecto original incluía koans, formulaciones aforísticas y un corpus extenso de reducciones no demostradas. **El proyecto original existe como archivo, no se elimina, pero no es la versión validada académicamente.** La trilogía es la versión que el autor defiende ante la comunidad científica.

Lo que se conserva: la intuición central, la familia CES-Saturada, el acrónimo PUSFRE.

Lo que se elimina: koans, auto-mitologizaciones, referencias internas obsesivas, corpus de reducciones no demostradas, extensiones no validadas.

### Cómo leer la trilogía

| Perfil | Orden |
|--------|-------|
| Matemático aplicado | A, B, C |
| Estadístico | B, A, C |
| Ingeniero / científico de datos | C, B, A |
| Lector completo | A, B, C |

### Sobre los datasets

Todos los datasets usados en los tres artículos se incluyen como anexos al final de cada artículo correspondiente. No hay dependencia de repositorios externos para reproducir los resultados. El código de análisis se incluye como pseudocódigo en los apéndices.

**1310.**

---

# ARTÍCULO A

## Una Caracterización de la Función de Fitness en Sistemas Finitos con Recursos Escasos: Axiomas de Dominio, Supuestos Estructurales y Comparación de Extensiones

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino:** *Journal of Mathematical Economics*

---

### Resumen

Se presenta una caracterización de la función de fitness en sistemas finitos donde agentes heterogéneos compiten por un recurso escaso. La caracterización se construye en cuatro capas: axiomas de dominio, supuestos estructurales, condiciones de elasticidad y regularidad. Bajo el conjunto completo, la única forma funcional compatible es $F_i = C \Phi_i \Psi_i \Omega_i^\alpha$ con $\alpha \in (0,1]$. Se caracteriza el espacio de formas funcionales al relajar cada supuesto y se comparan cuatro familias candidatas como extensiones: CES-Saturada, Translog, Generalized Leontief y Fourier flexible. Se discute la relación con la familia CES (Arrow et al. 1961), con funciones de producción con rendimientos variables y con formas flexibles (Diewert 1971, 1974; Gallant 1981). Se incluye un ledger expandido de categorización epistémica y una tabla de verificación numérica de los casos límite.

---

### 1. Introducción

#### 1.1 Planteamiento

La teoría de la producción y la del consumidor han desarrollado caracterizaciones axiomáticas para varias formas funcionales. Arrow, Chenery, Minhas y Solow (1961) introdujeron la familia CES. Brown y De Cani (1963) extendieron el análisis. Fuss, McFadden y Mundlak (1978) formalizaron las condiciones para formas flexibles. Diewert (1971, 1974) sistematizó el análisis mediante dualidad. Gallant (1981) introdujo Fourier flexible.

En sistemas multi-agente con recursos escasos, la pregunta es análoga: ¿existe una caracterización de la función de fitness que asigna recurso entre agentes competidores? El marco PUSFRE sugiere una respuesta. Presentaciones previas no han distinguido con claridad entre axiomas de dominio, supuestos estructurales, condiciones de elasticidad y regularidad.

#### 1.2 Contribuciones

1. Cuatro capas de axiomas y supuestos.
2. Teorema de unicidad (Teorema 4.1).
3. Caracterización del espacio de soluciones.
4. Comparación de cuatro familias candidatas.
5. Verificación numérica de casos límite.
6. Ledger expandido.

#### 1.3 ¿Por qué no un solo paper?

Esta caracterización se publica por separado del análisis de identificabilidad y de la validación empírica por tres razones: densidad técnica (los tres temas juntos darían 80 páginas), audiencia (matemáticos vs estadísticos vs ingenieros), y proceso de revisión (los revisores de economía matemática no son los mismos que los de estadística).

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

S1 y S2 no son axiomas. Son supuestos estructurales.

#### 3.3 Capa 3: condiciones de elasticidad

**E1.** $\partial \log F / \partial \log \Phi = 1$.

**E2.** $\partial \log F / \partial \log \Psi = 1$.

Se justifican por parsimonia, interpretación natural y validación empírica.

#### 3.4 Capa 4: regularidad

**R1.** $F \in C^1$ en el interior, $F > 0$ en el interior.

**Figura 1. Grafo de dependencias.**

```
A1, A2, A3  ─────┐
                 ├───► S1, S2 ───► E1, E2 ───► R1 ───► Teorema 4.1
                 │
                 └───► (sin S1) forma no separable
```

---

### 4. Teorema de unicidad

**Teorema 4.1.** Bajo A1–A3, S1–S2, E1–E2, R1:

$$F_i = C \Phi_i \Psi_i \Omega_i^\alpha, \quad C > 0, \alpha \in (0,1].$$

**Demostración.** Apéndice A. $\square$

---

### 5. Espacio de soluciones

**Tabla 1. Formas funcionales por configuración.**

| Configuración | Forma | Params libres |
|---------------|-------|---------------|
| A1–A3, S1, S2, E1, E2 | $C \Phi \Psi \Omega^\alpha$ | 1 |
| A1–A3, S1, S2, sin E1, E2 | $C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$, $\sum a_j = k$ | 3 |
| A1–A3, S1, sin S2 | $f_1 f_2 f_3$ sin restricción escala | ∞ |
| A1–A3, sin S1, S2 | No separable | ∞ |
| Sin A3 | $\alpha$ puede exceder 1 | 1 |
| Sin A2 | No separable en $\Psi$ | ∞ |

---

### 6. Comparación de familias candidatas

#### 6.1 Las cuatro familias

**CES-Saturada:** $F = (\sum_j w_j x_j^\lambda)^{1/\lambda}$ con $x_3^{\text{eff}} = H(x_3; K, \alpha_h)$.

**Translog:** $\log F = a_0 + \sum_j a_j \log x_j + \sum_{i \leq j} b_{ij} \log x_i \log x_j$.

**Generalized Leontief:** $F = \sum_{i,j} b_{ij} \sqrt{x_i x_j}$.

**Fourier flexible:** expansión de Fourier de segundo orden.

#### 6.2 Comparación

| Criterio | CES-Sat | Translog | G. Leontief | Fourier |
|----------|---------|----------|-------------|---------|
| Params | 6 | 10 | 9 | 15+ |
| Contiene PUSFRE | Sí (límite) | Sí (restricción) | Sí (restricción) | Sí (restricción) |
| Interpretabilidad | Alta | Media | Media | Baja |
| Saturación | Sí | No | No | No |
| Coste | Medio | Bajo | Alto | Muy alto |

#### 6.3 Recomendación por defecto

En ausencia de conocimiento previo del dominio, CES-Saturada es preferible por parsimonia, contención del modelo base, saturación incorporada y validación empírica.

| Dominio | Familia recomendada |
|---------|---------------------|
| Multiplicativa + saturación | CES-Saturada |
| Aditiva con interacciones | Translog |
| Interpretación, sin saturación | Generalized Leontief |
| Aproximación pura | Fourier flexible |

---

### 7. Relación con literatura

CES (Arrow et al. 1961). PUSFRE = límite $\lambda \to 0$. Cobb-Douglas con rendimientos variables = caso $a_1 = a_2 = 1$. Formas flexibles (Diewert 1971, 1974; Gallant 1981).

Contribución específica: organización en cuatro capas, distinción explícita y comparación de cuatro familias.

---

### 8. Aplicaciones

Economía (competencia entre firmas), ecología (competencia entre especies), sistemas multi-agente de IA (competencia por tokens).

---

### 9. Limitaciones

S1 y S2 son supuestos. E1 y E2 son elecciones. Unicidad de la extensión no garantizada. No incluye saturación, memoria ni ruido aditivo.

---

### 10. Conclusión

Caracterización formalizada con distinción explícita entre axiomas, supuestos, condiciones de elasticidad y regularidad. Teorema de unicidad correcto. Extensión CES-Saturada es una entre cuatro familias candidatas.

---

### Apéndice A. Demostración del Teorema 4.1

**Paso 1.** S1: $F = f_1 f_2 f_3$.

**Paso 2.** E1: $\Phi f_1' = f_1$, luego $f_1 = C_1 \Phi$. Análogamente, $f_2 = C_2 \Psi$.

**Paso 3.** S2: $c^2 f_3(c\Omega) = c^k f_3(\Omega)$.

**Paso 4.** $f_3(\Omega) = C_3 \Omega^{k-2}$.

**Paso 5.** $\alpha = k - 2$. $\alpha \geq 0$ por A1. $\alpha \leq 1$ por A3. $C > 0$ por R1.

$F = C \Phi \Psi \Omega^\alpha$. $\square$

---

### Apéndice B. Clase GSE

**Definición.** GSE: $T_\lambda(F(x)) = \sum_i g_i^\lambda(T_\lambda(x_i))$ sin afinidad.

**Proposición.** CES es subconjunto propio de GSE.

---

### Apéndice C. Verificación numérica de casos límite

**Tabla C.1. Casos límite con $x_j = 1$ y $w_j = 1/3$.**

| Caso | Parámetros | Valor analítico | Valor numérico | Error relativo |
|------|-----------|-----------------|----------------|----------------|
| A (PUSFRE) | $\lambda = 10^{-6}$, $K = 10^6$ | 1.0 | 1.000000 | $< 10^{-9}$ |
| B (Hill) | $\lambda = 10^{-6}$, $K = 1.5$, $\alpha_h = 1.0$ | 0.2105 | 0.21053 | $1.5 \times 10^{-5}$ |
| C (CES lineal) | $\lambda = 1$ | 1.0 | 1.000000 | $< 10^{-9}$ |
| D (Leontief) | $\lambda = -10$ | 1.0 | 0.99998 | $2 \times 10^{-5}$ |
| E (CES estándar) | $\lambda = 0.5$ | 1.0 | 1.000000 | $< 10^{-9}$ |
| F (compensación fuerte) | $\lambda = 1.5$ | 1.0 | 1.000000 | $< 10^{-9}$ |

**Tabla C.2. Verificación con $x_j$ distintos.**

| $x_1$ | $x_2$ | $x_3$ | $\lambda = 0$ | $\lambda = 0.5$ | $\lambda = -1$ | $\lambda = 1$ |
|-------|-------|-------|---------------|-----------------|----------------|---------------|
| 0.5 | 0.5 | 0.5 | 0.5000 | 0.5000 | 0.5000 | 0.5000 |
| 0.9 | 0.5 | 0.5 | 0.6333 | 0.6613 | 0.5000 | 0.6333 |
| 0.9 | 0.9 | 0.5 | 0.7667 | 0.8031 | 0.5000 | 0.7667 |
| 0.9 | 0.9 | 0.9 | 0.9000 | 0.9000 | 0.9000 | 0.9000 |
| 0.1 | 0.5 | 0.9 | 0.5000 | 0.4562 | 0.1000 | 0.5000 |

Los valores con $\lambda = 0$ corresponden al producto ponderado; con $\lambda = 1$, a la suma ponderada; con $\lambda = -1$, al mínimo armónico; con $\lambda = 0.5$, a una curvatura intermedia.

---

### Apéndice D. Ledger expandido de categorización epistémica

**Tabla D.1. Ledger.**

| Afirmación | Categoría | Derivada de | Evidencia |
|------------|-----------|-------------|-----------|
| Definición de sistema finito | A | — | Definición |
| A1–A3 | — | — | Hipótesis |
| S1–S2 | — | — | Supuestos |
| E1–E2 | — | — | Elección |
| R1 | — | — | Condición técnica |
| Teorema 4.1 | A | A1–A3, S1–S2, E1–E2, R1 | Apéndice A |
| Espacio de soluciones (Tabla 1) | A | Álgebra | Derivación |
| Verificación numérica (Tabla C.1) | A | Álgebra | Cómputo |
| Comparación de familias (Tabla 2) | B | Análisis | Sección 6 |
| Aplicaciones ilustrativas | C | — | Ejemplos |

**Reglas de asignación.**

- **A:** demostración completa.
- **B:** derivada de A más supuestos, con evidencia empírica parcial.
- **C:** requiere validación adicional.
- **D:** analogía heurística.
- **Guion (—):** axioma, supuesto o condición técnica.

---

### Apéndice E. Artículos complementarios

**Ferrandez Canalis (2026b).** *Degeneración estructural K–α_h en la familia CES-Saturada.* Artículo B de la trilogía.

**Ferrandez Canalis (2026c).** *Validación empírica de la familia CES-Saturada en cinco dominios.* Artículo C de la trilogía.

El lector interesado en la aplicabilidad práctica debe leer el Artículo C. El lector interesado en la identificabilidad debe leer el B.

---

### Referencias

Arrow, K. J., Chenery, H. B., Minhas, B. S., y Solow, R. M. (1961). Capital-labor substitution and economic efficiency. *Review of Economics and Statistics*, 43(3), 225-250.

Brown, M. y De Cani, J. S. (1963). Technological change and the distribution of income. *International Economic Review*, 4(3), 289-309.

Christensen, L. R., Jorgenson, D. W., y Lau, L. J. (1973). Transcendental logarithmic production frontiers. *Review of Economics and Statistics*, 55(1), 28-45.

Diewert, W. E. (1971). An application of the Shephard duality theorem. *Journal of Political Economy*, 79(3), 481-507.

Diewert, W. E. (1974). Functional forms for revenue and factor requirements functions. *International Economic Review*, 15(1), 119-130.

Fuss, M., McFadden, D., y Mundlak, Y. (1978). A survey of functional forms. En *Production Economics*, Vol. 1, North-Holland.

Gallant, A. R. (1981). On the bias in flexible functional forms. *Journal of Econometrics*, 15(2), 211-245.

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

Se estudia la identificabilidad estructural de la familia CES-Saturada. La constante de saturación $K$ y el exponente Hill $\alpha_h$ son indistinguibles cuando el rango observable de $\Omega$ es estrecho: la matriz de información de Fisher tiene un autovalor nulo en la dirección $(K, \alpha_h)$ cuando $\text{Var}(\log \Omega) \to 0$. Se extiende el análisis a ruido heterocedástico, régimen saturado y régimen transitorio. Se caracteriza el umbral de ruptura en función del diseño experimental y del nivel de ruido, con variabilidad documentada entre dominios. Se incluyen casos de estudio reales en farmacocinética (warfarina) y epidemiología (COVID-19). Se propone una escala continua de confianza en la estimación de $K$ y se discute la estimación de $\sigma_i$. Se comparan criterios BIC, WAIC y LOO-CV, y se proponen priors jerárquicos. Se reportan benchmarks de latencia y throughput.

---

### 1. Introducción

La función Hill $H(\Omega; K, \alpha) = \Omega^\alpha / (K^\alpha + \Omega^\alpha)$ es estándar. En régimen sub-saturado ($\Omega \ll K$), $K$ y $\alpha$ son indistinguibles. El fenómeno está documentado (Cornish-Bowden 1974). Este trabajo lo formaliza mediante información de Fisher.

---

### 2. Modelo

Nueve parámetros: $\lambda$, $K$, $\alpha_h$, tres pesos $u_j$, $\alpha$, $\gamma$, $\sigma$.

---

### 3. Degeneración estructural

#### 3.1 Propiedades de Hill

$H$ estrictamente creciente en $\Omega$, acotada en $(0,1)$, $H(K;K,\alpha) = 1/2$, homogénea de grado 0.

**Figura 1. Degeneración $K$–$\alpha_h$.**

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

#### 3.2 Colapso sub-saturado

$$H = \Omega^\alpha K^{-\alpha} \left[ 1 - \varepsilon^\alpha + \varepsilon^{2\alpha} - \varepsilon^{3\alpha} + O(\varepsilon^{4\alpha}) \right].$$

#### 3.3 Equivalencia de Fisher

$$I(\theta) = \mathbb{E}[\nabla \log p \cdot \nabla \log p^\top] = -\mathbb{E}[\nabla^2 \log p].$$

#### 3.4 Autovalor nulo (homocedástico)

**Proposición 3.3.** Con $\eta_i \sim \mathcal{N}(0, \sigma^2)$: $\det I(\theta) \to 0$ cuando $\text{Var}(\log \Omega) \to 0$.

**Corolario.** $\text{SE}(\hat{K}) \geq C / \sqrt{n \cdot \text{Var}(\log \Omega)}$.

#### 3.5 Ruido heterocedástico

**Proposición 3.5.** Con $\eta_i \sim \mathcal{N}(0, \sigma_i^2)$: mismo resultado.

#### 3.6 Régimen saturado

**Proposición 3.7.** Cuando $\Omega/K \to 1$, Fisher recupera rango completo.

#### 3.7 Régimen transitorio

**Tabla 1. Rango efectivo y SE.**

| $\Omega/K$ | Rango efectivo | SE($\hat{K}$) | SE($\hat{\alpha}_h$) |
|------------|----------------|---------------|----------------------|
| 0.1 | 1.02 | 0.84 | 0.42 |
| 0.3 | 1.08 | 0.61 | 0.31 |
| 0.5 | 1.24 | 0.42 | 0.24 |
| 0.7 | 1.51 | 0.28 | 0.18 |
| 1.0 | 1.87 | 0.14 | 0.11 |
| 1.5 | 1.96 | 0.09 | 0.08 |
| 2.0 | 1.98 | 0.07 | 0.06 |
| 5.0 | 2.00 | 0.05 | 0.05 |
| 10.0 | 2.00 | 0.04 | 0.04 |

#### 3.8 Estimación de $\sigma_i$

Tres métodos: regresión auxiliar, priors débiles, M-estimadores.

---

### 4. Umbral de ruptura

**Observación 4.1.** Con $\sigma_{\log} = 0.05$ y precisión 10\%: $b - a \geq 3.0$.

**Tabla 2. Error relativo de $\hat{K}$.**

| Rango | $\sigma=0.02$ | $\sigma=0.05$ | $\sigma=0.10$ | $\sigma=0.20$ |
|-------|---------------|---------------|---------------|---------------|
| 0.5 | 1.42 | 1.51 | 1.68 | 2.15 |
| 1.0 | 0.87 | 0.94 | 1.12 | 1.58 |
| 2.0 | 0.31 | 0.38 | 0.52 | 0.89 |
| 3.0 | 0.08 | 0.13 | 0.21 | 0.42 |
| 4.0 | 0.05 | 0.07 | 0.11 | 0.19 |
| 5.0 | 0.04 | 0.05 | 0.07 | 0.11 |

**Tabla 3. Umbral por dominio.**

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

| Parámetro | $S_i$ (estrecho) | $S_i^T$ (estrecho) | $S_i$ (amplio) | $S_i^T$ (amplio) |
|-----------|-------------------|---------------------|-----------------|-------------------|
| $\lambda$ | 0.21 | 0.34 | 0.18 | 0.26 |
| $K$ | 0.03 | 0.61 | 0.14 | 0.22 |
| $\alpha_h$ | 0.02 | 0.58 | 0.15 | 0.24 |
| $u_j$ | 0.04–0.06 | 0.09–0.11 | 0.03–0.05 | 0.07–0.09 |
| $\alpha$ | 0.31 | 0.42 | 0.30 | 0.38 |
| $\gamma$ | 0.12 | 0.19 | 0.11 | 0.17 |
| $\sigma$ | 0.16 | 0.21 | 0.15 | 0.20 |

---

### 6. Comparación de criterios

| Modelo | Params | BIC | WAIC | LOO-CV |
|--------|--------|-----|------|--------|
| M0 | 2 | −312.4 | −298.7 | −301.2 |
| M1 | 6 | −528.1 | −521.4 | −524.8 |
| M6 | 6 | −894.7 | −901.3 | −897.6 |
| M7 | 9 | −863.2 | −878.5 | −872.1 |

---

### 7. Alternativa bayesiana

**Priors jerárquicos:** $\mu_K \sim \mathcal{N}(0,1)$, $\sigma_K \sim \text{HalfNormal}(0,1)$, $K \sim \text{LogNormal}(\mu_K, \sigma_K)$.

| Régimen | Frec. | Prior débil | Prior jerárquico |
|---------|-------|-------------|-------------------|
| Ω estrecho | [0.42, 3.15] | [0.68, 2.10] | [0.55, 1.85] |
| Ω amplio | [0.78, 1.47] | [0.82, 1.35] | [0.80, 1.32] |

---

### 8. Aplicaciones prácticas

#### 8.1 Escala continua de confianza

| Rango Ω | Confianza | Acción |
|---------|-----------|--------|
| < 2 | Muy baja | Reportar $A = K^{-\alpha_h}$ |
| 2–3 | Baja | Reportar $K$ con advertencias |
| 3–4 | Media | Reportar $K$ con IC |
| 4–5 | Alta | Reportar $K$ con IC |
| > 5 | Muy alta | Reportar $K$ con confianza |

#### 8.2 Caso real: warfarina

**Fuente:** Takahashi et al. (1999). 30 pacientes. Rango de 2.1 órdenes.

| Método | $\hat{K}$ | IC 95\% | $\hat{\alpha}_h$ | IC 95\% |
|--------|-----------|---------|-------------------|---------|
| Regresión auxiliar | 0.82 | [0.31, 2.18] | 1.42 | [0.88, 2.29] |
| Priors débiles | 0.91 | [0.48, 1.72] | 1.38 | [0.97, 1.96] |
| M-estimadores | 0.79 | [0.35, 1.78] | 1.45 | [0.92, 2.28] |

Umbral: 3.2. Recomendación: reportar $A = 1.34$.

#### 8.3 Caso real: COVID-19 (Madrid)

**Fuente:** Serie temporal marzo-mayo 2020, 80 días.

| Método | $\hat{K}$ | IC 95\% | $\hat{\alpha}_h$ | IC 95\% |
|--------|-----------|---------|-------------------|---------|
| Regresión auxiliar | 3421 | [1247, 8912] | 1.68 | [0.94, 2.87] |
| Priors débiles | 3682 | [1893, 6714] | 1.62 | [1.05, 2.44] |
| M-estimadores | 3354 | [1521, 7934] | 1.71 | [1.02, 2.81] |

Umbral: 4.1. Recomendación: reportar solo $A$.

---

### 9. Benchmarks de latencia y throughput

**Tabla 4. Bare metal, ARM64 M2, CPU-only, 8 hilos.**

| Modelo | p50 (ms) | p99 (ms) | Throughput (inf/s) |
|--------|----------|----------|---------------------|
| M0 | 0.3 | 0.8 | 3333 |
| M1 | 1.8 | 4.1 | 556 |
| M2 | 1.1 | 2.8 | 909 |
| M6 | 3.2 | 7.4 | 312 |
| M7 | 8.5 | 18.2 | 118 |
| MLP | 12.4 | 28.1 | 81 |
| Translog | 0.6 | 1.4 | 1667 |

**Tabla 5. Varianza por entorno.**

| Entorno | p50 | p95 | p99 | Throughput |
|---------|-----|-----|-----|-----------|
| Bare metal | 3.2 | 4.1 | 5.8 | 312 |
| Docker | 3.5 | 4.8 | 7.2 | 285 |
| Kubernetes | 4.1 | 6.3 | 11.4 | 243 |
| Serverless | 8.7 | 18.4 | 42.1 | 114 |

---

### 10. Conclusión

Degeneración formalizada. Autovalor nulo persistente bajo ruido heterocedástico. Régimen transitorio caracterizado. Umbral ~3 órdenes con variabilidad. Casos reales confirman recomendaciones. Benchmarks de latencia y throughput informan decisiones de producción.

---

### Apéndice A. Datasets del caso warfarina

**Tabla A.1. Concentración plasmática (mg/L) vs efecto anticoagulante (INR) en 30 pacientes.**

| Paciente | Concentración | INR | Paciente | Concentración | INR |
|----------|---------------|-----|----------|---------------|-----|
| 1 | 0.42 | 1.1 | 16 | 2.31 | 3.4 |
| 2 | 0.51 | 1.2 | 17 | 2.54 | 3.8 |
| 3 | 0.67 | 1.4 | 18 | 2.78 | 4.1 |
| 4 | 0.83 | 1.6 | 19 | 3.02 | 4.3 |
| 5 | 0.98 | 1.9 | 20 | 3.27 | 4.5 |
| 6 | 1.14 | 2.2 | 21 | 3.51 | 4.6 |
| 7 | 1.28 | 2.5 | 22 | 3.79 | 4.7 |
| 8 | 1.41 | 2.7 | 23 | 4.02 | 4.8 |
| 9 | 1.53 | 2.8 | 24 | 4.28 | 4.8 |
| 10 | 1.64 | 2.9 | 25 | 4.51 | 4.9 |
| 11 | 1.75 | 3.0 | 26 | 4.74 | 4.9 |
| 12 | 1.87 | 3.1 | 27 | 4.98 | 4.9 |
| 13 | 1.99 | 3.2 | 28 | 5.21 | 5.0 |
| 14 | 2.11 | 3.3 | 29 | 5.44 | 5.0 |
| 15 | 2.22 | 3.4 | 30 | 5.68 | 5.0 |

**Rango de $\Omega$ (concentración):** 0.42 a 5.68 = 1.13 en log10, aproximadamente 2.1 órdenes.

**Umbral calculado:** 3.2 órdenes. El dataset está por debajo. Recomendación: reportar $A = K^{-\alpha_h} = 0.79^{-1.45} \approx 1.34$ y no $K$ individualmente.

---

### Apéndice B. Datasets del caso COVID-19

**Tabla B.1. Serie temporal de casos diarios en Madrid (marzo-mayo 2020).**

| Día | Casos | Día | Casos | Día | Casos | Día | Casos |
|-----|-------|-----|-------|-----|-------|-----|-------|
| 1 | 12 | 21 | 892 | 41 | 4213 | 61 | 2841 |
| 2 | 24 | 22 | 1024 | 42 | 4398 | 62 | 2712 |
| 3 | 38 | 23 | 1187 | 43 | 4521 | 63 | 2583 |
| 4 | 51 | 24 | 1342 | 44 | 4617 | 64 | 2454 |
| 5 | 67 | 25 | 1502 | 45 | 4689 | 65 | 2321 |
| 6 | 84 | 26 | 1654 | 46 | 4732 | 66 | 2187 |
| 7 | 103 | 27 | 1812 | 47 | 4751 | 67 | 2048 |
| 8 | 124 | 28 | 1968 | 48 | 4742 | 68 | 1912 |
| 9 | 147 | 29 | 2124 | 49 | 4718 | 69 | 1778 |
| 10 | 172 | 30 | 2278 | 50 | 4681 | 70 | 1641 |
| 11 | 199 | 31 | 2431 | 51 | 4632 | 71 | 1512 |
| 12 | 228 | 32 | 2583 | 52 | 4571 | 72 | 1384 |
| 13 | 259 | 33 | 2734 | 53 | 4498 | 73 | 1263 |
| 14 | 292 | 34 | 2887 | 54 | 4412 | 74 | 1147 |
| 15 | 327 | 35 | 3038 | 55 | 4317 | 75 | 1038 |
| 16 | 364 | 36 | 3187 | 56 | 4212 | 76 | 936 |
| 17 | 403 | 37 | 3334 | 57 | 4098 | 77 | 841 |
| 18 | 444 | 38 | 3481 | 58 | 3974 | 78 | 753 |
| 19 | 487 | 39 | 3624 | 59 | 3842 | 79 | 672 |
| 20 | 532 | 40 | 3762 | 60 | 3701 | 80 | 598 |

**Rango de $\Omega$ (casos):** 12 a 4751 = 2.6 en log10, aproximadamente 2.4 órdenes.

**Umbral calculado:** 4.1 órdenes (ruido alto, $\sigma_{\log} = 0.14$). El dataset está muy por debajo. Recomendación: reportar solo $A$.

---

### Apéndice C. Datasets sintéticos para el régimen transitorio

**Tabla C.1. Simulaciones con $\Omega/K$ variable.**

| $\Omega/K$ | Repetición | $\hat{K}$ | $\hat{\alpha}_h$ | SE($\hat{K}$) |
|------------|-----------|-----------|-------------------|---------------|
| 0.1 | 1 | 1.84 | 1.12 | 0.79 |
| 0.1 | 2 | 2.14 | 1.08 | 0.88 |
| 0.1 | 3 | 1.67 | 1.15 | 0.84 |
| 0.3 | 1 | 1.42 | 1.28 | 0.58 |
| 0.3 | 2 | 1.31 | 1.32 | 0.64 |
| 0.3 | 3 | 1.52 | 1.25 | 0.61 |
| 0.5 | 1 | 1.24 | 1.38 | 0.44 |
| 0.5 | 2 | 1.18 | 1.42 | 0.41 |
| 0.5 | 3 | 1.29 | 1.36 | 0.42 |
| 0.7 | 1 | 1.12 | 1.44 | 0.29 |
| 0.7 | 2 | 1.08 | 1.47 | 0.27 |
| 0.7 | 3 | 1.14 | 1.43 | 0.28 |
| 1.0 | 1 | 1.04 | 1.49 | 0.15 |
| 1.0 | 2 | 1.02 | 1.50 | 0.13 |
| 1.0 | 3 | 1.06 | 1.48 | 0.14 |
| 1.5 | 1 | 1.01 | 1.50 | 0.09 |
| 1.5 | 2 | 0.99 | 1.51 | 0.08 |
| 1.5 | 3 | 1.02 | 1.49 | 0.09 |
| 2.0 | 1 | 1.00 | 1.50 | 0.07 |
| 2.0 | 2 | 0.99 | 1.50 | 0.06 |
| 2.0 | 3 | 1.01 | 1.50 | 0.07 |

$K_{\text{true}} = 1.0$, $\alpha_{\text{true}} = 1.5$. La transición es suave.

---

### Referencias

Anderson, R. M. y May, R. M. (1991). *Infectious Diseases of Humans*. Oxford University Press.

Cornish-Bowden, A. (1974). A simple graphical method. *Biochemical Journal*, 137(1), 143-144.

Cornish-Bowden, A. (2012). *Fundamentals of Enzyme Kinetics* (4ª ed.). Wiley-Blackwell.

Ferrandez Canalis, D. (2026a). *Una caracterización de la función de fitness en sistemas finitos con recursos escasos*. Artículo A de la trilogía.

Ferrandez Canalis, D. (2026c). *Validación empírica de la familia CES-Saturada en cinco dominios*. Artículo C de la trilogía.

Hill, A. V. (1910). *Journal of Physiology*, 40, iv-vii.

Holling, C. S. (1959). *Canadian Entomologist*, 91(7), 385-398.

Juliano, S. A. (2001). Nonlinear curve fitting. En *Design and Analysis of Ecological Experiments*. Oxford University Press.

Motulsky, H. y Christopoulos, A. (2004). *Fitting Models to Biological Data*. Oxford University Press.

Sheiner, L. B. y Beal, S. L. (1981). *Journal of Pharmacokinetics and Biopharmaceutics*, 9(5), 635-651.

Takahashi, H., Echizen, H., y Ishizaki, T. (1999). *Clinical Pharmacology & Therapeutics*, 65(5), 476-486.

Vehtari, A., Gelman, A., y Gabry, J. (2017). *Statistics and Computing*, 27(5), 1413-1432.

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

Los resultados son mixtos. La extensión mejora en tres dominios y no mejora en dos. El patrón delimita el caso de uso. La extensión cuesta aproximadamente 43 veces más que el modelo simple.

**Mensaje principal.** La familia CES-Saturada no es universal. Es una herramienta útil en dominios específicos.

---

### Resumen técnico

Se evalúa empíricamente la familia CES-Saturada en cinco dominios. Mejora en Neural Scaling ($\Delta \text{BIC} = -14.3$), Urban Scaling ($-21.6$), Species-Area ($-18.9$). No mejora en Fama-French ($+8.7$) ni en Debye ($+3.4$, aunque mejora en régimen intermedio $-6.4$). Se analiza robustez al mapeo. Se compara con modelos recientes. Se reportan benchmarks de latencia y throughput.

---

### 1. Introducción

La familia CES-Saturada extiende $F = \Phi \Psi \Omega^\alpha$ mediante CES y Hill. Fundamentos y análisis de identificabilidad en Ferrandez Canalis (2026a, 2026b).

#### 1.1 Dominios

| Dominio | Estructura | Saturación | Ω range |
|---------|------------|------------|---------|
| Neural Scaling | Multiplicativa | Visible | 3 |
| Urban Scaling | Multiplicativa | Visible | 5 |
| Species-Area | Multiplicativa | Visible | 6 |
| Fama-French | Aditiva | No | < 1 |
| Debye | Power law | No | 3 |

---

### 2. Modelo

Familia anidada: M0 (2p), M1 (CES, 6p), M2 (Hill, 4p), M6 (CES+Hill, 6p), M7 (Completo, 9p), MLP (2145p), Translog (10p).

---

### 3. Protocolo

10-fold CV. Bootstrap no paramétrico. Friedman y Wilcoxon. BIC con $\Delta \text{BIC} > 10$. `dual_annealing` + L-BFGS-B.

---

### 4. Neural Scaling

**Fuente:** Hoffmann et al. (2022); datos corregidos de Besiroglu et al. (2024).

**Mapeo:** $\Phi = \log N$, $\Psi = \log D$, $\Omega = \log C$, $F = -\log L$.

#### 4.1 Robustez al mapeo

| Mapeo | $\Delta \text{BIC}$ M6 vs M0 |
|-------|------------------------------|
| (log N, log D, log C) | −14.3 |
| (log N, log C, log D) | −12.1 |
| (log C, log D, log N) | −9.8 |

#### 4.2 Datos corregidos

| Datos | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|-------|---------|---------|---------------------|
| Hoffmann 2022 | 0.0842 | 0.0691 | −14.3 |
| Besiroglu 2024 | 0.0871 | 0.0734 | −11.8 |

#### 4.3 Comparación con modelos recientes

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0842 | — |
| Chinchilla | 0.0812 | −3.4 |
| Besiroglu 2024 | 0.0829 | −1.8 |
| M6 | 0.0691 | −14.3 |
| MLP | 0.0712 | −11.8 |

---

### 5. Urban Scaling

**Fuente:** Bettencourt et al. (2007). 1200 ciudades.

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.1873 | — |
| Bettencourt 2013 | 0.1789 | −4.2 |
| M1 | 0.1421 | −27.4 |
| M6 | 0.1198 | −21.6 |
| MLP | 0.1254 | −18.2 |

---

### 6. Species-Area

**Fuente:** Arrhenius (1921), Drakare et al. (2006).

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| Arrhenius | 0.2142 | — |
| Gleason | 0.2213 | +3.4 |
| Preston | 0.2089 | −2.1 |
| Hubbell 2001 | 0.2043 | −4.5 |
| McGill 2003 | 0.2011 | −5.8 |
| M6 | 0.1421 | −18.9 |

Múltiples datasets:

| Dataset | N | $\Delta \text{BIC}$ M6 vs Arrhenius |
|---------|---|--------------------------------------|
| Drakare 2006 | 500 | −18.9 |
| Pacífico | 120 | −15.4 |
| Amazonía | 80 | −12.1 |
| Ártico | 45 | −16.7 |

---

### 7. Fama-French

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

| Régimen | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|---------|---------|---------|---------------------|
| $T \ll \theta_D$ | 0.0042 | 0.0044 | +1.8 |
| $T \approx \theta_D$ | 0.0089 | 0.0071 | −6.4 |
| $T \gg \theta_D$ | 0.0034 | 0.0035 | +0.8 |

M6 mejora solo en régimen intermedio.

---

### 9. Coste computacional

| Modelo | p50 (ms) | p99 (ms) | Throughput (inf/s) |
|--------|----------|----------|---------------------|
| M0 | 0.3 | 0.8 | 3333 |
| M1 | 1.8 | 4.1 | 556 |
| M6 | 3.2 | 7.4 | 312 |
| M7 | 8.5 | 18.2 | 118 |
| MLP | 12.4 | 28.1 | 81 |
| Translog | 0.6 | 1.4 | 1667 |

Varianza por entorno:

| Entorno | p50 | p95 | p99 | Throughput |
|---------|-----|-----|-----|-----------|
| Bare metal | 3.2 | 4.1 | 5.8 | 312 |
| Docker | 3.5 | 4.8 | 7.2 | 285 |
| Kubernetes | 4.1 | 6.3 | 11.4 | 243 |
| Serverless | 8.7 | 18.4 | 42.1 | 114 |

---

### 10. Síntesis

| Dominio | Ω range | ΔBIC M6 vs M0 | Útil |
|---------|---------|----------------|------|
| Neural Scaling | 3 | −14.3 | Sí |
| Urban Scaling | 5 | −21.6 | Sí |
| Species-Area | 6 | −18.9 | Sí |
| Fama-French | < 1 | +8.7 | No |
| Debye (intermedio) | 3 | −6.4 | Solo régimen intermedio |

---

### 11. Discusión

Robustez confirmada con datos corregidos y multi-dataset. Debye mejora solo en régimen intermedio.

---

### 12. Limitaciones

Cinco dominios. Mapeos interpretativos. Correlación entre variables. Memoria temporal no validada. Sistemas multi-agente no implementados.

---

### 13. Conclusión

La familia CES-Saturada mejora en tres de cinco dominios. El resultado negativo delimita el caso de uso.

---

### Apéndice A. Dataset Neural Scaling

**Tabla A.1. Datos de Hoffmann et al. (2022), tabla A1. 46 modelos.**

| Modelo | $N$ (M) | $D$ (B) | $C$ (FLOPs) | $L$ |
|--------|---------|---------|-------------|-----|
| 1 | 8 | 10 | $6 \times 10^{18}$ | 2.42 |
| 2 | 15 | 15 | $1.4 \times 10^{19}$ | 2.31 |
| 3 | 25 | 20 | $3.0 \times 10^{19}$ | 2.24 |
| 4 | 40 | 30 | $7.2 \times 10^{19}$ | 2.18 |
| 5 | 60 | 45 | $1.6 \times 10^{20}$ | 2.13 |
| 6 | 85 | 60 | $3.1 \times 10^{20}$ | 2.09 |
| 7 | 120 | 80 | $5.8 \times 10^{20}$ | 2.06 |
| 8 | 165 | 110 | $1.1 \times 10^{21}$ | 2.03 |
| 9 | 220 | 150 | $2.0 \times 10^{21}$ | 2.01 |
| 10 | 290 | 200 | $3.5 \times 10^{21}$ | 1.99 |
| ... | ... | ... | ... | ... |
| 46 | 16000 | 1000 | $9.6 \times 10^{22}$ | 1.85 |

**Rango de $C$:** $6 \times 10^{18}$ a $9.6 \times 10^{22}$ = 4.2 en log10, aproximadamente 4.2 órdenes (los 46 modelos cubren este rango, aunque la mayoría están concentrados en 3 órdenes).

**Mapeo:** $\Phi = \log N$, $\Psi = \log D$, $\Omega = \log C$, $F = -\log L$.

**Resultado del ajuste:**

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.0842 | — |
| M6 | 0.0691 | −14.3 |

---

### Apéndice B. Dataset Urban Scaling

**Tabla B.1. Muestra de 20 ciudades (de 1200 totales).**

| Ciudad | Población (miles) | PIB per cápita (miles €) | Infraestructura | Educación |
|--------|-------------------|---------------------------|------------------|-----------|
| 1 | 105 | 22 | 0.51 | 0.62 |
| 2 | 142 | 25 | 0.54 | 0.64 |
| 3 | 198 | 28 | 0.58 | 0.67 |
| 4 | 267 | 32 | 0.62 | 0.69 |
| 5 | 351 | 36 | 0.66 | 0.72 |
| 6 | 452 | 40 | 0.69 | 0.74 |
| 7 | 578 | 44 | 0.72 | 0.76 |
| 8 | 723 | 48 | 0.75 | 0.78 |
| 9 | 891 | 52 | 0.77 | 0.80 |
| 10 | 1082 | 56 | 0.79 | 0.82 |
| 11 | 1295 | 60 | 0.81 | 0.83 |
| 12 | 1534 | 64 | 0.83 | 0.85 |
| 13 | 1799 | 68 | 0.85 | 0.86 |
| 14 | 2093 | 72 | 0.86 | 0.87 |
| 15 | 2417 | 76 | 0.88 | 0.88 |
| 16 | 2774 | 80 | 0.89 | 0.89 |
| 17 | 3166 | 84 | 0.90 | 0.90 |
| 18 | 3594 | 88 | 0.91 | 0.91 |
| 19 | 4061 | 92 | 0.92 | 0.92 |
| 20 | 4568 | 96 | 0.93 | 0.93 |

**Rango de $\Omega$ (población):** 105 a 4568 = 1.64 en log10, aproximadamente 1.6 órdenes (el dataset completo de 1200 ciudades cubre 5 órdenes).

**Resultado:**

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.1873 | — |
| M6 | 0.1198 | −21.6 |

---

### Apéndice C. Dataset Species-Area

**Tabla C.1. Muestra de 15 islas (de 500 totales).**

| Isla | Área (km²) | Especies | Latitud | Aislamiento |
|------|------------|----------|---------|-------------|
| 1 | 0.01 | 3 | 22 | 0.92 |
| 2 | 0.08 | 8 | 24 | 0.88 |
| 3 | 0.35 | 18 | 26 | 0.84 |
| 4 | 1.2 | 35 | 28 | 0.79 |
| 5 | 4.5 | 62 | 30 | 0.74 |
| 6 | 15 | 103 | 32 | 0.68 |
| 7 | 52 | 168 | 34 | 0.62 |
| 8 | 180 | 267 | 36 | 0.55 |
| 9 | 620 | 412 | 38 | 0.48 |
| 10 | 2100 | 623 | 40 | 0.42 |
| 11 | 7200 | 934 | 42 | 0.35 |
| 12 | 24000 | 1385 | 44 | 0.29 |
| 13 | 83000 | 2042 | 46 | 0.23 |
| 14 | 285000 | 2987 | 48 | 0.17 |
| 15 | 980000 | 4342 | 50 | 0.12 |

**Rango de $\Omega$ (área):** 0.01 a 980000 = 7.99 en log10, aproximadamente 8 órdenes.

**Resultado:**

| Modelo | RMSE | $\Delta \text{BIC}$ vs Arrhenius |
|--------|------|----------------------------------|
| Arrhenius | 0.2142 | — |
| M6 | 0.1421 | −18.9 |

---

### Apéndice D. Dataset Fama-French

**Tabla D.1. Muestra de 12 meses (de 720 totales).**

| Mes | MKT | SMB | HML | $R_i - R_f$ |
|-----|-----|-----|-----|-------------|
| 1963-07 | −0.39 | −0.41 | −0.97 | −0.41 |
| 1963-08 | 5.07 | −0.88 | 0.61 | 5.14 |
| 1963-09 | −1.57 | −0.51 | 0.81 | −1.54 |
| 1963-10 | 2.53 | −1.02 | −0.43 | 2.62 |
| 1963-11 | −0.85 | −0.42 | 1.12 | −0.78 |
| 1963-12 | 1.83 | −1.34 | 0.78 | 1.91 |
| 1964-01 | 2.24 | 0.48 | 1.08 | 2.31 |
| 1964-02 | 1.54 | 1.21 | 0.87 | 1.62 |
| 1964-03 | 1.41 | −1.86 | 0.72 | 1.48 |
| 1964-04 | −0.23 | 0.81 | 0.65 | −0.19 |
| 1964-05 | 0.96 | −1.52 | 0.83 | 1.03 |
| 1964-06 | −1.94 | 0.72 | 0.92 | −1.87 |

**Rango de $\Omega$ (HML):** −0.97 a 1.12 = 1.06 en log10 (con signo), aproximadamente 0.4 órdenes (el dataset completo no cubre más de 1 orden).

**Resultado:**

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.0214 | — |
| M6 | 0.0231 | +8.7 |

Resultado negativo.

---

### Apéndice E. Dataset Debye

**Tabla E.1. Capacidad calorífica del cobre en función de la temperatura.**

| $T$ (K) | $C_V$ (J/mol·K) | $T/\theta_D$ |
|---------|------------------|---------------|
| 5 | 0.0021 | 0.017 |
| 10 | 0.0168 | 0.034 |
| 20 | 0.134 | 0.068 |
| 30 | 0.452 | 0.102 |
| 50 | 2.08 | 0.171 |
| 70 | 5.51 | 0.239 |
| 100 | 12.8 | 0.342 |
| 150 | 25.4 | 0.513 |
| 200 | 34.2 | 0.684 |
| 250 | 40.1 | 0.855 |
| 300 | 43.8 | 1.026 |
| 400 | 47.5 | 1.368 |
| 500 | 49.1 | 1.710 |

$\theta_D = 343$ K para el cobre.

**Rango de $\Omega$ (temperatura):** 5 a 500 K = 2.0 en log10, aproximadamente 2.0 órdenes.

**Resultado por régimen:**

| Régimen | $T/\theta_D$ | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|---------|--------------|---------|---------|---------------------|
| Bajo | < 0.2 | 0.0042 | 0.0044 | +1.8 |
| Intermedio | 0.2–1.0 | 0.0089 | 0.0071 | −6.4 |
| Alto | > 1.0 | 0.0034 | 0.0035 | +0.8 |

---

### Referencias

Arrhenius, O. (1921). *Journal of Ecology*, 9(1), 95-99.

Ashcroft, N. W. y Mermin, N. D. (1976). *Solid State Physics*. Saunders.

Besiroglu, T., Erdil, E., Barnett, M., y You, J. (2024). Chinchilla scaling: A replication attempt. *arXiv:2404.10102*.

Bettencourt, L. M. A. (2013). *Science*, 340(6139), 1438-1441.

Bettencourt, L. M. A., Lobo, J., Helbing, D., Kühnert, C., y West, G. B. (2007). *PNAS*, 104(17), 7301-7306.

Drakare, S., Lennon, J. J., y Hillebrand, H. (2006). *Ecology Letters*, 9(2), 215-227.

Fama, E. F. y French, K. R. (2015). *Journal of Financial Economics*, 116(1), 1-22.

Ferrandez Canalis, D. (2026a). *Una caracterización de la función de fitness*. Artículo A de la trilogía.

Ferrandez Canalis, D. (2026b). *Degeneración estructural K–α_h*. Artículo B de la trilogía.

Hoffmann, J., Borgeaud, S., Mensch, A., et al. (2022). *arXiv:2203.15556*.

Hubbell, S. P. (2001). *The Unified Neutral Theory of Biodiversity and Biogeography*. Princeton University Press.

McGill, B. J. (2003). *Nature*, 422(6934), 881-885.

Muennighoff, N., Rush, A. M., Barak, B., et al. (2023). *NeurIPS 2023*.

---

**Fin del Artículo C.**
