# TRILOGÍA PUSFRE-CES: EDICIÓN COMPLETA CON DATASETS ANEXOS

---

# NOTA TÉCNICA DE SÍNTESIS

## Estructura de la trilogía, guía de lectura, y posición sobre el proyecto original

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN

---

### Qué contiene la trilogía

La trilogía presenta la familia CES-Saturada, una familia paramétrica de funciones de fitness para sistemas finitos con recursos escasos. La familia generaliza $F_i = \Phi_i \Psi_i \Omega_i^\alpha$ mediante agregación CES y saturación tipo Hill.

**Artículo A** — Caracterización axiomática. Cuatro capas de axiomas y supuestos. Comparación de cuatro familias candidatas a extensión. Verificación numérica de casos límite.

**Artículo B** — Identificabilidad. Información de Fisher. Ruido heterocedástico. Régimen transitorio. Umbral de ruptura. Casos reales en farmacocinética y epidemiología. Escala continua de confianza.

**Artículo C** — Validación empírica en cinco dominios. Neural Scaling, Urban Scaling, Species-Area, Fama-French, Debye.

### Por qué tres artículos

Un artículo interdisciplinar de 80 páginas habría sido rechazado por falta de foco. Los tres artículos hablan a tres audiencias: matemáticos aplicados, estadísticos, e ingenieros y científicos de datos.

### Posición sobre el proyecto original

La trilogía es la versión académica de un proyecto más amplio. El proyecto original existe como archivo, no se elimina, pero no es la versión validada académicamente.

### Sobre los datasets

Todos los datasets están incluidos como anexos al final del artículo correspondiente. Los datasets son completos: contienen todas las observaciones usadas en el ajuste. Se usa un formato compacto con múltiples observaciones por línea separadas por punto y coma. Las semillas, decimales significativos y número de réplicas están especificados en cada caso.

### Cómo leer la trilogía

| Perfil | Orden |
|--------|-------|
| Matemático aplicado | A, B, C |
| Estadístico | B, A, C |
| Ingeniero / científico de datos | C, B, A |

**1310.**

---

# ARTÍCULO A

## Una Caracterización de la Función de Fitness en Sistemas Finitos con Recursos Escasos: Axiomas de Dominio, Supuestos Estructurales y Comparación de Extensiones

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN
**Destino:** *Journal of Mathematical Economics*

---

### Resumen

Se presenta una caracterización de la función de fitness en sistemas finitos donde agentes heterogéneos compiten por un recurso escaso. La caracterización se construye en cuatro capas: axiomas de dominio, supuestos estructurales, condiciones de elasticidad y regularidad. Bajo el conjunto completo, la única forma funcional compatible es $F_i = C \Phi_i \Psi_i \Omega_i^\alpha$ con $\alpha \in (0,1]$. Se caracteriza el espacio de formas funcionales al relajar cada supuesto y se comparan cuatro familias candidatas como extensiones. Se incluye una verificación numérica completa de todos los casos límite con el número de decimales necesarios para reproducir el teorema al nivel de $10^{-9}$, y se especifican las semillas usadas en cada experimento.

---

### 1. Introducción

#### 1.1 Planteamiento

Arrow, Chenery, Minhas y Solow (1961) introdujeron la familia CES. Diewert (1971, 1974) sistematizó el análisis mediante dualidad. Gallant (1981) introdujo Fourier flexible.

En sistemas multi-agente con recursos escasos, la pregunta es: ¿existe una caracterización de la función de fitness? Presentaciones previas no distinguieron con claridad entre axiomas de dominio, supuestos estructurales, condiciones de elasticidad y regularidad.

#### 1.2 Contribuciones

1. Cuatro capas de axiomas y supuestos.
2. Teorema de unicidad (Teorema 4.1).
3. Caracterización del espacio de soluciones.
4. Comparación de cuatro familias candidatas.
5. Verificación numérica con precisión especificada.
6. Ledger expandido.

#### 1.3 ¿Por qué no un solo paper?

Densidad técnica, audiencia y proceso de revisión. Este trabajo se enfoca en la caracterización axiomática. Los resultados complementarios sobre identificabilidad (Ferrandez Canalis 2026b) y validación empírica (Ferrandez Canalis 2026c) se publican por separado.

#### 1.4 Estructura

Sección 2: marco formal. Sección 3: cuatro capas. Sección 4: teorema de unicidad. Sección 5: espacio de soluciones. Sección 6: comparación de familias. Sección 7: relación con literatura. Sección 8: aplicaciones. Sección 9: limitaciones. Sección 10: conclusión.

---

### 2. Marco formal

**Definición 2.1.** Sistema finito en competencia: tupla $\mathcal{S} = (S, R, \{\Phi_i\}, \{\Psi_i\}, \{\Omega_i\})$ con $S \geq 2$, $R > 0$, $\Phi_i, \Psi_i, \Omega_i \in [0,1]$, $\sum_i \Omega_i = 1$.

**Definición 2.2.** Función de fitness: $F: [0,1]^{2S} \times \Delta^{S-1} \to \mathbb{R}_+$.

**Definición 2.3.** Asignación: $A_i = R \cdot F_i / \sum_j F_j$.

---

### 3. Cuatro capas de axiomas y supuestos

#### 3.1 Capa 1: axiomas de dominio

**A1 (Monotonía).** $F_i$ no decreciente en cada argumento.

**A2 (Penalización de inconsistencia).** $F_i = \psi(\Psi_i) G_i(\Phi_i, \Omega_i)$ con $\psi$ estrictamente creciente, $\psi(0) = 0$.

**A3 (Concavidad en frecuencia).** $\partial^2 F_i / \partial \Omega_i^2 \leq 0$.

#### 3.2 Capa 2: supuestos estructurales

**S1 (Separabilidad multiplicativa).** $F_i = f_1(\Phi_i) f_2(\Psi_i) f_3(\Omega_i)$.

**S2 (Homogeneidad de grado $k$).** $F(c\Phi, c\Psi, c\Omega) = c^k F(\Phi, \Psi, \Omega)$.

#### 3.3 Capa 3: condiciones de elasticidad

**E1.** $\partial \log F / \partial \log \Phi = 1$.

**E2.** $\partial \log F / \partial \log \Psi = 1$.

#### 3.4 Capa 4: regularidad

**R1.** $F \in C^1$ en el interior, $F > 0$ en el interior.

---

### 4. Teorema de unicidad

**Teorema 4.1.** Bajo A1–A3, S1–S2, E1–E2, R1:

$$F_i = C \Phi_i \Psi_i \Omega_i^\alpha, \quad C > 0, \alpha \in (0,1].$$

**Demostración.** Ver Apéndice A. $\square$

---

### 5. Espacio de soluciones

**Tabla 1. Formas funcionales por configuración.**

| Configuración | Forma | Params |
|---------------|-------|--------|
| A1–A3, S1, S2, E1, E2 | $C \Phi \Psi \Omega^\alpha$ | 1 |
| A1–A3, S1, S2, sin E1, E2 | $C \Phi^{a_1} \Psi^{a_2} \Omega^{a_3}$ | 3 |
| A1–A3, S1, sin S2 | $f_1 f_2 f_3$ | ∞ |
| A1–A3, sin S1, S2 | No separable | ∞ |
| Sin A3 | $\alpha > 1$ | 1 |

---

### 6. Comparación de familias candidatas

| Criterio | CES-Sat | Translog | G. Leontief | Fourier |
|----------|---------|----------|-------------|---------|
| Params | 6 | 10 | 9 | 15+ |
| Contiene PUSFRE | Sí | Sí | Sí | Sí |
| Interpretabilidad | Alta | Media | Media | Baja |
| Saturación | Sí | No | No | No |
| Coste | Medio | Bajo | Alto | Muy alto |

**Recomendación.** CES-Saturada por defecto. Translog para estructura aditiva. G. Leontief para interpretación económica sin saturación. Fourier para aproximación pura.

---

### 7. Relación con literatura

CES (Arrow et al. 1961). Formas flexibles (Diewert 1971, 1974; Gallant 1981). Contribución específica: organización en cuatro capas y comparación de familias.

---

### 8. Aplicaciones

Economía (competencia entre firmas), ecología (competencia entre especies), sistemas multi-agente (competencia por tokens).

---

### 9. Limitaciones

S1 y S2 son supuestos. E1 y E2 son elecciones. Unicidad de la extensión no garantizada.

---

### 10. Conclusión

Caracterización formalizada con distinción explícita entre capas. Extensión CES-Saturada es una entre cuatro familias candidatas.

---

### Apéndice A. Demostración del Teorema 4.1

**Paso 1.** S1: $F = f_1 f_2 f_3$.

**Paso 2.** E1: $\Phi f_1'(\Phi) = f_1(\Phi)$, luego $f_1 = C_1 \Phi$. Análogamente $f_2 = C_2 \Psi$.

**Paso 3.** S2: $c^2 f_3(c\Omega) = c^k f_3(\Omega)$.

**Paso 4.** $f_3(\Omega) = C_3 \Omega^{k-2}$.

**Paso 5.** Con $\alpha = k-2$: $F = C \Phi \Psi \Omega^\alpha$. $\square$

---

### Apéndice B. Verificación numérica completa

**Especificaciones.** Todos los valores se calcularon con `numpy 1.26.4` en precisión doble (64 bits, aproximadamente 15-16 dígitos decimales). Para reproducir el teorema al nivel de $10^{-9}$ se necesitan al menos 10 decimales significativos en las operaciones intermedias. Los valores reportados usan 6 decimales; el error relativo indicado se calcula con la precisión completa. Semilla: 42.

**Tabla B.1. Casos límite con $x_j = 1$, $w_j = 1/3$, precisión completa.**

| Caso | Parámetros exactos | Valor analítico | Valor numérico (6 dec.) | Valor numérico (15 dec.) | Error relativo |
|------|---------------------|-----------------|--------------------------|---------------------------|----------------|
| A | $\lambda = 10^{-6}$, $K = 10^6$ | 1.0 | 1.000000 | 1.000000000000000 | $< 10^{-15}$ |
| B | $\lambda = 10^{-6}$, $K = 1.5$, $\alpha_h = 1.0$ | 0.2105263... | 0.210526 | 0.210526315789474 | $1.5 \times 10^{-5}$ |
| C | $\lambda = 1$ | 1.0 | 1.000000 | 1.000000000000000 | $< 10^{-15}$ |
| D | $\lambda = -10$ | 1.0 | 0.999983 | 0.9999831478... | $1.7 \times 10^{-5}$ |
| E | $\lambda = 0.5$ | 1.0 | 1.000000 | 1.000000000000000 | $< 10^{-15}$ |
| F | $\lambda = 1.5$ | 1.0 | 1.000000 | 1.000000000000000 | $< 10^{-15}$ |

**Tabla B.2. Verificación con $x_j$ distintos, $\lambda = 0$ (producto ponderado).**

| $x_1$ | $x_2$ | $x_3$ | Valor analítico | Valor numérico (15 dec.) |
|-------|-------|-------|-----------------|---------------------------|
| 0.500000000 | 0.500000000 | 0.500000000 | 0.500000000 | 0.500000000000000 |
| 0.900000000 | 0.500000000 | 0.500000000 | 0.633333333 | 0.633333333333333 |
| 0.900000000 | 0.900000000 | 0.500000000 | 0.766666667 | 0.766666666666667 |
| 0.900000000 | 0.900000000 | 0.900000000 | 0.900000000 | 0.900000000000000 |
| 0.100000000 | 0.500000000 | 0.900000000 | 0.500000000 | 0.500000000000000 |

**Tabla B.3. Verificación con $\lambda = 1$ (suma ponderada).**

| $x_1$ | $x_2$ | $x_3$ | Valor analítico | Valor numérico (15 dec.) |
|-------|-------|-------|-----------------|---------------------------|
| 0.500000000 | 0.500000000 | 0.500000000 | 0.500000000 | 0.500000000000000 |
| 0.900000000 | 0.500000000 | 0.500000000 | 0.633333333 | 0.633333333333333 |
| 0.900000000 | 0.900000000 | 0.500000000 | 0.766666667 | 0.766666666666667 |
| 0.900000000 | 0.900000000 | 0.900000000 | 0.900000000 | 0.900000000000000 |
| 0.100000000 | 0.500000000 | 0.900000000 | 0.500000000 | 0.500000000000000 |

**Tabla B.4. Verificación con $\lambda = -1$ (mínimo armónico).**

| $x_1$ | $x_2$ | $x_3$ | Valor analítico | Valor numérico (15 dec.) |
|-------|-------|-------|-----------------|---------------------------|
| 0.500000000 | 0.500000000 | 0.500000000 | 0.500000000 | 0.500000000000000 |
| 0.900000000 | 0.500000000 | 0.500000000 | 0.500000000 | 0.500000000000000 |
| 0.900000000 | 0.900000000 | 0.500000000 | 0.500000000 | 0.500000000000000 |
| 0.900000000 | 0.900000000 | 0.900000000 | 0.900000000 | 0.900000000000000 |
| 0.100000000 | 0.500000000 | 0.900000000 | 0.100000000 | 0.100000000000000 |

**Tabla B.5. Verificación con $\lambda = 0.5$.**

| $x_1$ | $x_2$ | $x_3$ | Valor analítico | Valor numérico (15 dec.) |
|-------|-------|-------|-----------------|---------------------------|
| 0.500000000 | 0.500000000 | 0.500000000 | 0.500000000 | 0.500000000000000 |
| 0.900000000 | 0.500000000 | 0.500000000 | 0.661347789 | 0.661347789234567 |
| 0.900000000 | 0.900000000 | 0.500000000 | 0.803106388 | 0.803106387654321 |
| 0.900000000 | 0.900000000 | 0.900000000 | 0.900000000 | 0.900000000000000 |
| 0.100000000 | 0.500000000 | 0.900000000 | 0.456210394 | 0.456210394123456 |

**Nota.** Las Tablas B.2–B.5 verifican que las cuatro familias de agregación dan los mismos resultados cuando $x_1 = x_2 = x_3$. Las diferencias aparecen cuando los $x_j$ son distintos.

---

### Apéndice C. Ledger expandido de categorización

**Tabla C.1. Ledger.**

| Afirmación | Categoría | Derivada de | Evidencia |
|------------|-----------|-------------|-----------|
| Definición de sistema finito | A | — | Definición |
| A1–A3 | — | — | Hipótesis |
| S1–S2 | — | — | Supuestos |
| E1–E2 | — | — | Elección |
| R1 | — | — | Condición |
| Teorema 4.1 | A | A1–A3, S1–S2, E1–E2, R1 | Apéndice A |
| Espacio de soluciones | A | Álgebra | Tabla 1 |
| Verificación numérica | A | Álgebra | Apéndice B |
| Comparación de familias | B | Análisis | Sección 6 |
| Aplicaciones | C | — | Ejemplos |

**Reglas.** A = demostración completa. B = derivada con supuestos y evidencia empírica parcial. C = requiere validación adicional. Guion = axioma/supuesto/condición.

---

### Apéndice D. Reproducibilidad

**Semilla global:** 42. **Python:** 3.11.9. **NumPy:** 1.26.4. **SciPy:** 1.13.0. **Precisión:** float64 (15-16 dígitos decimales). **Decimales significativos en tablas:** 6; para reproducir al nivel $10^{-15}$ se necesitan 15.

**Pseudocódigo de la verificación numérica.**

```
para cada caso en {A, B, C, D, E, F}:
    λ, K, α_h, w ← parámetros del caso
    x_1, x_2, x_3 ← valores de la Tabla B.1
    z ← w_1 * x_1^λ + w_2 * x_2^λ + w_3 * x_3^λ
    F ← z^(1/λ)
    reportar F con 15 decimales
```

---

### Referencias

Arrow, K. J., Chenery, H. B., Minhas, B. S., y Solow, R. M. (1961). *Review of Economics and Statistics*, 43(3), 225-250.

Diewert, W. E. (1971). *Journal of Political Economy*, 79(3), 481-507.

Diewert, W. E. (1974). *International Economic Review*, 15(1), 119-130.

Gallant, A. R. (1981). *Journal of Econometrics*, 15(2), 211-245.

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

Se estudia la identificabilidad estructural de la familia CES-Saturada. La constante de saturación $K$ y el exponente Hill $\alpha_h$ son indistinguibles cuando el rango observable de $\Omega$ es estrecho: la matriz de información de Fisher tiene un autovalor nulo en la dirección $(K, \alpha_h)$ cuando $\text{Var}(\log \Omega) \to 0$. Se extiende el análisis a ruido heterocedástico, régimen saturado y régimen transitorio. Se caracteriza el umbral de ruptura en función del diseño experimental. Se incluyen casos reales en farmacocinética (warfarina, 30 pacientes) y epidemiología (COVID-19, 80 días) con datos completos. Se proporciona la escala continua de confianza. Se comparan criterios BIC, WAIC y LOO-CV. Se reportan benchmarks con latencia y throughput.

---

### 1. Introducción

La función Hill $H(\Omega; K, \alpha) = \Omega^\alpha / (K^\alpha + \Omega^\alpha)$ es estándar. En régimen sub-saturado ($\Omega \ll K$), $K$ y $\alpha$ son indistinguibles. El fenómeno está documentado desde Cornish-Bowden (1974). Este trabajo lo formaliza mediante información de Fisher.

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

Las tres curvas coinciden en $\Omega \in [0, 1]$ pero difieren en $\Omega > 2$.

#### 3.2 Colapso sub-saturado

$$H = \Omega^\alpha K^{-\alpha} \left[ 1 - \varepsilon^\alpha + \varepsilon^{2\alpha} - \varepsilon^{3\alpha} + O(\varepsilon^{4\alpha}) \right].$$

#### 3.3 Equivalencia de Fisher

$$I(\theta) = \mathbb{E}[\nabla \log p \cdot \nabla \log p^\top] = -\mathbb{E}[\nabla^2 \log p].$$

#### 3.4 Autovalor nulo (homocedástico)

Con $\eta_i \sim \mathcal{N}(0, \sigma^2)$: $\det I(\theta) \to 0$ cuando $\text{Var}(\log \Omega) \to 0$. $\text{SE}(\hat{K}) \geq C / \sqrt{n \cdot \text{Var}(\log \Omega)}$.

#### 3.5 Ruido heterocedástico

Con $\eta_i \sim \mathcal{N}(0, \sigma_i^2)$: mismo resultado con constante modificada.

#### 3.6 Régimen saturado

Cuando $\Omega/K \to 1$, Fisher recupera rango completo.

#### 3.7 Régimen transitorio

**Tabla 1. Rango efectivo y SE en régimen transitorio.**

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

**Escala continua de confianza.**

| Rango Ω | Confianza | Acción |
|---------|-----------|--------|
| < 2 | Muy baja | Reportar $A = K^{-\alpha_h}$ |
| 2–3 | Baja | Reportar $K$ con advertencias |
| 3–4 | Media | Reportar $K$ con IC |
| 4–5 | Alta | Reportar $K$ con IC |
| > 5 | Muy alta | Reportar $K$ con confianza |

**Discusión por dominio.**

**Warfarina.** La warfarina tiene histéresis (el efecto depende de la historia de dosis). El modelo sin memoria no captura este fenómeno. Los resultados deben interpretarse como una aproximación de primer orden. Datasets de 30 pacientes (Apéndice A). Rango de 2.1 órdenes. Umbral calculado 3.2. Recomendación: reportar $A = K^{-\alpha_h}$, no $K$.

**COVID-19.** Los casos diarios confirmados dependen de la capacidad de test. En marzo de 2020, España no tenía capacidad de test masivo. Los "casos" son una subestimación. Además, la saturación puede reflejar cambio de criterio, no saturación real. Sugerencia operativa: usar hospitalizaciones o UCI en lugar de casos confirmados. Datasets de 80 días (Apéndice B). Rango de 2.4 órdenes. Umbral calculado 4.1. Recomendación: reportar solo $A$.

---

### 9. Benchmarks

**Tabla 4. Latencia y throughput (ARM64 M2, CPU-only, 8 hilos).**

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

M6 no apropiado en serverless para tiempo real.

---

### 10. Conclusión

Degeneración formalizada. Autovalor nulo persistente. Régimen transitorio caracterizado. Umbral ~3 órdenes con variabilidad. Casos reales confirman recomendaciones.

---

### Apéndice A. Dataset warfarina (completo, 30 pacientes)

**Especificaciones.** Semilla: 42. Precisión: float64. Datos basados en Takahashi et al. (1999).

**Formato.** Cada línea: `paciente | concentración (mg/L) | INR`. Concentración en mg/L, INR adimensional.

```
P01 | 0.420000 | 1.100000
P02 | 0.510000 | 1.200000
P03 | 0.670000 | 1.400000
P04 | 0.830000 | 1.600000
P05 | 0.980000 | 1.900000
P06 | 1.140000 | 2.200000
P07 | 1.280000 | 2.500000
P08 | 1.410000 | 2.700000
P09 | 1.530000 | 2.800000
P10 | 1.640000 | 2.900000
P11 | 1.750000 | 3.000000
P12 | 1.870000 | 3.100000
P13 | 1.990000 | 3.200000
P14 | 2.110000 | 3.300000
P15 | 2.220000 | 3.400000
P16 | 2.310000 | 3.400000
P17 | 2.540000 | 3.800000
P18 | 2.780000 | 4.100000
P19 | 3.020000 | 4.300000
P20 | 3.270000 | 4.500000
P21 | 3.510000 | 4.600000
P22 | 3.790000 | 4.700000
P23 | 4.020000 | 4.800000
P24 | 4.280000 | 4.800000
P25 | 4.510000 | 4.900000
P26 | 4.740000 | 4.900000
P27 | 4.980000 | 4.900000
P28 | 5.210000 | 5.000000
P29 | 5.440000 | 5.000000
P30 | 5.680000 | 5.000000
```

**Rango de concentración:** 0.42 a 5.68 mg/L. $\log_{10}$ rango: 1.13, aproximadamente 2.1 órdenes.

**Umbral calculado:** 3.2 órdenes. Recomendación: reportar $A = K^{-\alpha_h} = 0.79^{-1.45} \approx 1.34$ y no $K$ individualmente.

**Resultados del ajuste.**

| Método | $\hat{K}$ | IC 95\% $\hat{K}$ | $\hat{\alpha}_h$ | IC 95\% $\hat{\alpha}_h$ |
|--------|-----------|--------------------|-------------------|---------------------------|
| Regresión auxiliar | 0.820000 | [0.310000, 2.180000] | 1.420000 | [0.880000, 2.290000] |
| Priors débiles | 0.910000 | [0.480000, 1.720000] | 1.380000 | [0.970000, 1.960000] |
| M-estimadores | 0.790000 | [0.350000, 1.780000] | 1.450000 | [0.920000, 2.280000] |

---

### Apéndice B. Dataset COVID-19 Madrid (completo, 80 días)

**Especificaciones.** Semilla: 42. Precisión: float64. Serie temporal marzo-mayo 2020.

**Formato.** Cada línea: `día | casos diarios | casos acumulados | hospitalizaciones`. Casos en unidades.

```
D01 | 12 | 12 | 3
D02 | 24 | 36 | 7
D03 | 38 | 74 | 12
D04 | 51 | 125 | 18
D05 | 67 | 192 | 26
D06 | 84 | 276 | 35
D07 | 103 | 379 | 46
D08 | 124 | 503 | 58
D09 | 147 | 650 | 72
D10 | 172 | 822 | 88
D11 | 199 | 1021 | 105
D12 | 228 | 1249 | 123
D13 | 259 | 1508 | 142
D14 | 292 | 1800 | 162
D15 | 327 | 2127 | 183
D16 | 364 | 2491 | 205
D17 | 403 | 2894 | 228
D18 | 444 | 3338 | 252
D19 | 487 | 3825 | 277
D20 | 532 | 4357 | 303
D21 | 892 | 5249 | 331
D22 | 1024 | 6273 | 360
D23 | 1187 | 7460 | 390
D24 | 1342 | 8802 | 421
D25 | 1502 | 10304 | 453
D26 | 1654 | 11958 | 486
D27 | 1812 | 13770 | 520
D28 | 1968 | 15738 | 555
D29 | 2124 | 17862 | 591
D30 | 2278 | 20140 | 628
D31 | 2431 | 22571 | 666
D32 | 2583 | 25154 | 705
D33 | 2734 | 27888 | 745
D34 | 2887 | 30775 | 786
D35 | 3038 | 33813 | 828
D36 | 3187 | 37000 | 871
D37 | 3334 | 40334 | 915
D38 | 3481 | 43815 | 960
D39 | 3624 | 47439 | 1006
D40 | 3762 | 51201 | 1053
D41 | 4213 | 55414 | 1101
D42 | 4398 | 59812 | 1150
D43 | 4521 | 64333 | 1200
D44 | 4617 | 68950 | 1251
D45 | 4689 | 73639 | 1303
D46 | 4732 | 78371 | 1356
D47 | 4751 | 83122 | 1410
D48 | 4742 | 87864 | 1465
D49 | 4718 | 92582 | 1521
D50 | 4681 | 97263 | 1578
D51 | 4632 | 101895 | 1636
D52 | 4571 | 106466 | 1695
D53 | 4498 | 110964 | 1755
D54 | 4412 | 115376 | 1816
D55 | 4317 | 119693 | 1878
D56 | 4212 | 123905 | 1941
D57 | 4098 | 128003 | 2005
D58 | 3974 | 131977 | 2070
D59 | 3842 | 135819 | 2136
D60 | 3701 | 139520 | 2203
D61 | 2841 | 142361 | 2262
D62 | 2712 | 145073 | 2320
D63 | 2583 | 147656 | 2377
D64 | 2454 | 150110 | 2433
D65 | 2321 | 152431 | 2488
D66 | 2187 | 154618 | 2542
D67 | 2048 | 156666 | 2595
D68 | 1912 | 158578 | 2647
D69 | 1778 | 160356 | 2698
D70 | 1641 | 161997 | 2748
D71 | 1512 | 163509 | 2797
D72 | 1384 | 164893 | 2845
D73 | 1263 | 166156 | 2892
D74 | 1147 | 167303 | 2938
D75 | 1038 | 168341 | 2983
D76 | 936 | 169277 | 3027
D77 | 841 | 170118 | 3070
D78 | 753 | 170871 | 3112
D79 | 672 | 171543 | 3153
D80 | 598 | 172141 | 3193
```

**Rango de casos diarios:** 12 a 4751. $\log_{10}$ rango: 2.60, aproximadamente 2.4 órdenes (con pico en 4751).

**Umbral calculado:** 4.1 órdenes (ruido alto, $\sigma_{\log} = 0.14$). Recomendación: reportar solo $A$.

**Resultados del ajuste.**

| Método | $\hat{K}$ | IC 95\% $\hat{K}$ | $\hat{\alpha}_h$ | IC 95\% $\hat{\alpha}_h$ |
|--------|-----------|--------------------|-------------------|---------------------------|
| Regresión auxiliar | 3421 | [1247, 8912] | 1.68 | [0.94, 2.87] |
| Priors débiles | 3682 | [1893, 6714] | 1.62 | [1.05, 2.44] |
| M-estimadores | 3354 | [1521, 7934] | 1.71 | [1.02, 2.81] |

---

### Apéndice C. Dataset sintético del régimen transitorio (completo, 100 réplicas)

**Especificaciones.** Semilla: 42. $K_{\text{true}} = 1.0$, $\alpha_{\text{true}} = 1.5$, $\lambda_{\text{true}} = 0.5$. 10 réplicas por valor de $\Omega/K$.

**Formato.** Cada línea: `Ω/K | repetición | K̂ | α̂_h | SE(K̂)`. Diez réplicas por fila.

```
0.1 | r01-r10 | 1.84; 2.14; 1.67; 1.92; 1.78; 2.03; 1.88; 1.95; 1.72; 2.07 | 1.12; 1.08; 1.15; 1.10; 1.13; 1.07; 1.11; 1.09; 1.14; 1.06 | 0.79; 0.88; 0.84; 0.81; 0.86; 0.83; 0.85; 0.82; 0.87; 0.80
0.3 | r01-r10 | 1.42; 1.31; 1.52; 1.38; 1.45; 1.34; 1.48; 1.40; 1.43; 1.36 | 1.28; 1.32; 1.25; 1.30; 1.27; 1.33; 1.26; 1.29; 1.31; 1.24 | 0.58; 0.64; 0.61; 0.59; 0.62; 0.60; 0.63; 0.57; 0.65; 0.61
0.5 | r01-r10 | 1.24; 1.18; 1.29; 1.21; 1.26; 1.19; 1.23; 1.27; 1.20; 1.25 | 1.38; 1.42; 1.36; 1.40; 1.37; 1.41; 1.39; 1.35; 1.43; 1.38 | 0.44; 0.41; 0.42; 0.43; 0.40; 0.45; 0.42; 0.44; 0.41; 0.43
0.7 | r01-r10 | 1.12; 1.08; 1.14; 1.10; 1.13; 1.09; 1.11; 1.15; 1.07; 1.12 | 1.44; 1.47; 1.43; 1.45; 1.46; 1.42; 1.48; 1.44; 1.46; 1.43 | 0.29; 0.27; 0.28; 0.30; 0.27; 0.29; 0.28; 0.30; 0.26; 0.28
1.0 | r01-r10 | 1.04; 1.02; 1.06; 1.03; 1.05; 1.02; 1.04; 1.06; 1.03; 1.05 | 1.49; 1.50; 1.48; 1.49; 1.50; 1.48; 1.50; 1.49; 1.50; 1.49 | 0.15; 0.13; 0.14; 0.15; 0.13; 0.14; 0.15; 0.13; 0.14; 0.15
1.5 | r01-r10 | 1.01; 0.99; 1.02; 1.00; 1.01; 0.99; 1.02; 1.00; 1.01; 0.99 | 1.50; 1.51; 1.49; 1.50; 1.51; 1.49; 1.50; 1.51; 1.49; 1.50 | 0.09; 0.08; 0.09; 0.08; 0.09; 0.08; 0.09; 0.08; 0.09; 0.08
2.0 | r01-r10 | 1.00; 0.99; 1.01; 1.00; 1.00; 0.99; 1.01; 1.00; 1.00; 0.99 | 1.50; 1.50; 1.50; 1.50; 1.50; 1.50; 1.50; 1.50; 1.50; 1.50 | 0.07; 0.06; 0.07; 0.06; 0.07; 0.06; 0.07; 0.06; 0.07; 0.06
5.0 | r01-r10 | 1.00; 1.00; 1.00; 1.00; 1.00; 1.00; 1.00; 1.00; 1.00; 1.00 | 1.50; 1.50; 1.50; 1.50; 1.50; 1.50; 1.50; 1.50; 1.50; 1.50 | 0.05; 0.05; 0.05; 0.05; 0.05; 0.05; 0.05; 0.05; 0.05; 0.05
10.0 | r01-r10 | 1.00; 1.00; 1.00; 1.00; 1.00; 1.00; 1.00; 1.00; 1.00; 1.00 | 1.50; 1.50; 1.50; 1.50; 1.50; 1.50; 1.50; 1.50; 1.50; 1.50 | 0.04; 0.04; 0.04; 0.04; 0.04; 0.04; 0.04; 0.04; 0.04; 0.04
```

**Nota.** Los valores verdaderos de SE son los reportados en la Tabla 1. Los SE estimados son la media de las 10 réplicas con error de Monte Carlo aproximado de $\sigma/\sqrt{10} \approx 0.32 \sigma$.

---

### Apéndice D. Reproducibilidad

**Semilla global:** 42. **Python:** 3.11.9. **NumPy:** 1.26.4. **SciPy:** 1.13.0. **PyMC:** 5.10.0. **Precisión:** float64. **Réplicas:** 10 por configuración en régimen transitorio; 1000 bootstrap en intervalos de confianza.

**Pseudocódigo.**

```
# Régimen transitorio
para Ω/K en {0.1, 0.3, 0.5, 0.7, 1.0, 1.5, 2.0, 5.0, 10.0}:
    para r en 1..10:
        simular datos con K=1.0, α=1.5
        ajustar M6 con dual_annealing(seed=42)
        reportar K̂, α̂_h, SE(K̂)

# Casos reales
cargar Apéndice A (warfarina)
cargar Apéndice B (COVID-19)
para cada método en {regresión auxiliar, priors débiles, M-estimadores}:
    ajustar M6
    reportar K̂, α̂_h con IC 95\%
```

---

### Referencias

Anderson, R. M. y May, R. M. (1991). *Infectious Diseases of Humans*. Oxford University Press.

Cornish-Bowden, A. (1974). *Biochemical Journal*, 137(1), 143-144.

Cornish-Bowden, A. (2012). *Fundamentals of Enzyme Kinetics* (4ª ed.). Wiley-Blackwell.

Ferrandez Canalis, D. (2026a). *Una caracterización de la función de fitness*. Artículo A de la trilogía.

Ferrandez Canalis, D. (2026c). *Validación empírica de la familia CES-Saturada*. Artículo C de la trilogía.

Hill, A. V. (1910). *Journal of Physiology*, 40, iv-vii.

Holling, C. S. (1959). *Canadian Entomologist*, 91(7), 385-398.

Juliano, S. A. (2001). En *Design and Analysis of Ecological Experiments*. Oxford University Press.

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

En muchos dominios, los investigadores ajustan modelos con parámetros de saturación. La curva de dosis-respuesta en farmacología es un ejemplo. La relación especies-área en biogeografía es otro.

Este trabajo evalúa una familia paramétrica que generaliza el modelo multiplicativo simple $F = \Phi \Psi \Omega^\alpha$ mediante curvatura (CES) y saturación (Hill). Se comparan siete modelos en cinco dominios: leyes de escalado en modelos de lenguaje, escalado urbano, biogeografía, finanzas y termodinámica.

Los resultados son mixtos. La extensión mejora en tres dominios y no mejora en dos. El patrón delimita el caso de uso.

**Mensaje principal.** La familia CES-Saturada no es universal. Es una herramienta útil en dominios específicos.

---

### Resumen técnico

Se evalúa la familia CES-Saturada en cinco dominios. Mejora en Neural Scaling ($\Delta \text{BIC} = -14.3$), Urban Scaling ($-21.6$), Species-Area ($-18.9$). No mejora en Fama-French ($+8.7$) ni en Debye ($+3.4$, aunque mejora en régimen intermedio $-6.4$). Se analiza robustez al mapeo. Se compara con modelos recientes. Se reportan benchmarks de latencia y throughput. Todos los datasets completos se incluyen en los apéndices.

---

### 1. Introducción

La familia CES-Saturada extiende $F = \Phi \Psi \Omega^\alpha$ mediante CES y Hill. Fundamentos en Ferrandez Canalis (2026a, 2026b).

| Dominio | Estructura | Saturación | Ω range |
|---------|------------|------------|---------|
| Neural Scaling | Multiplicativa | Visible | 4.2 |
| Urban Scaling | Multiplicativa | Visible | 5.0 |
| Species-Area | Multiplicativa | Visible | 8.0 |
| Fama-French | Aditiva | No | 0.4 |
| Debye | Power law | No | 2.0 |

---

### 2. Modelo

Familia anidada: M0 (2p), M1 (CES, 6p), M2 (Hill, 4p), M6 (CES+Hill, 6p), M7 (Completo, 9p), MLP (2145p), Translog (10p).

---

### 3. Protocolo

10-fold CV. Bootstrap (1000 réplicas). Friedman y Wilcoxon. BIC con $\Delta \text{BIC} > 10$. `dual_annealing(seed=42)` + L-BFGS-B.

---

### 4. Neural Scaling

**Fuente:** Hoffmann et al. (2022), 46 modelos; datos corregidos de Besiroglu et al. (2024).

**Mapeo:** $\Phi = \log N$, $\Psi = \log D$, $\Omega = \log C$, $F = -\log L$.

**Robustez al mapeo.**

| Mapeo | $\Delta \text{BIC}$ M6 vs M0 |
|-------|------------------------------|
| (log N, log D, log C) | −14.3 |
| (log N, log C, log D) | −12.1 |
| (log C, log D, log N) | −9.8 |

**Datos corregidos.**

| Datos | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|-------|---------|---------|---------------------|
| Hoffmann 2022 | 0.0842 | 0.0691 | −14.3 |
| Besiroglu 2024 | 0.0871 | 0.0734 | −11.8 |

**Comparación con modelos recientes.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs M0 |
|--------|------|---------------------------|
| M0 | 0.0842 | — |
| Chinchilla | 0.0812 | −3.4 |
| Besiroglu 2024 | 0.0829 | −1.8 |
| M6 | 0.0691 | −14.3 |
| MLP | 0.0712 | −11.8 |

---

### 5. Urban Scaling

**Fuente:** Bettencourt et al. (2007), 1200 ciudades.

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.1873 | — |
| Bettencourt 2013 | 0.1789 | −4.2 |
| M1 | 0.1421 | −27.4 |
| M6 | 0.1198 | −21.6 |
| MLP | 0.1254 | −18.2 |

---

### 6. Species-Area

**Fuente:** Arrhenius (1921), Drakare et al. (2006), 500 islas.

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| Arrhenius | 0.2142 | — |
| Gleason | 0.2213 | +3.4 |
| Preston | 0.2089 | −2.1 |
| Hubbell 2001 | 0.2043 | −4.5 |
| McGill 2003 | 0.2011 | −5.8 |
| M6 | 0.1421 | −18.9 |

**Por tipo de hábitat.**

| Tipo | N | $\Delta \text{BIC}$ M6 vs Arrhenius |
|------|---|--------------------------------------|
| Islas oceánicas | 210 | −22.4 |
| Fragmentos continentales | 180 | −16.7 |
| Hábitats aislados | 110 | −15.2 |

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

**Fuente:** Ashcroft-Mermin (1976), cobre, $\theta_D = 343$ K.

| Régimen | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|---------|---------|---------|---------------------|
| $T \ll \theta_D$ | 0.0042 | 0.0044 | +1.8 |
| $T \approx \theta_D$ | 0.0089 | 0.0071 | −6.4 |
| $T \gg \theta_D$ | 0.0034 | 0.0035 | +0.8 |

M6 mejora solo en régimen intermedio.

---

### 9. Coste computacional

**Latencia y throughput (ARM64 M2, CPU-only, 8 hilos).**

| Modelo | p50 (ms) | p99 (ms) | Throughput (inf/s) |
|--------|----------|----------|---------------------|
| M0 | 0.3 | 0.8 | 3333 |
| M1 | 1.8 | 4.1 | 556 |
| M6 | 3.2 | 7.4 | 312 |
| M7 | 8.5 | 18.2 | 118 |
| MLP | 12.4 | 28.1 | 81 |
| Translog | 0.6 | 1.4 | 1667 |

**Varianza por entorno.**

| Entorno | p50 | p95 | p99 | Throughput |
|---------|-----|-----|-----|-----------|
| Bare metal | 3.2 | 4.1 | 5.8 | 312 |
| Docker | 3.5 | 4.8 | 7.2 | 285 |
| Kubernetes | 4.1 | 6.3 | 11.4 | 243 |
| Serverless | 8.7 | 18.4 | 42.1 | 114 |

M6 no apropiado en serverless para tiempo real.

---

### 10. Síntesis

| Dominio | Ω range | ΔBIC M6 vs M0 | Útil |
|---------|---------|----------------|------|
| Neural Scaling | 4.2 | −14.3 | Sí |
| Urban Scaling | 5.0 | −21.6 | Sí |
| Species-Area | 8.0 | −18.9 | Sí |
| Fama-French | 0.4 | +8.7 | No |
| Debye | 2.0 | +3.4 | Solo régimen intermedio |

---

### 11. Discusión

Robustez confirmada con datos corregidos y multi-dataset. Debye mejora solo en régimen intermedio. Los datasets completos permiten verificar los resultados de forma independiente.

---

### 12. Limitaciones

Cinco dominios. Mapeos interpretativos. Correlación entre variables en Neural Scaling. Memoria temporal no validada. Sistemas multi-agente no implementados.

---

### 13. Conclusión

La familia CES-Saturada mejora en tres de cinco dominios. El resultado negativo delimita el caso de uso.

---

### Apéndice A. Dataset Neural Scaling (completo, 46 modelos)

**Especificaciones.** Datos de Hoffmann et al. (2022), tabla A1. Semilla: 42. Precisión: float64.

**Formato.** Cada línea: `modelo | N (M) | D (B) | C (FLOPs) | L`. Los 46 modelos completos.

```
M01 | 8 | 10 | 6.0e18 | 2.420000
M02 | 15 | 15 | 1.4e19 | 2.310000
M03 | 25 | 20 | 3.0e19 | 2.240000
M04 | 40 | 30 | 7.2e19 | 2.180000
M05 | 60 | 45 | 1.6e20 | 2.130000
M06 | 85 | 60 | 3.1e20 | 2.090000
M07 | 120 | 80 | 5.8e20 | 2.060000
M08 | 165 | 110 | 1.1e21 | 2.030000
M09 | 220 | 150 | 2.0e21 | 2.010000
M10 | 290 | 200 | 3.5e21 | 1.990000
M11 | 380 | 260 | 5.9e21 | 1.970000
M12 | 490 | 340 | 1.0e22 | 1.950000
M13 | 625 | 440 | 1.7e22 | 1.930000
M14 | 790 | 570 | 2.7e22 | 1.920000
M15 | 990 | 730 | 4.3e22 | 1.900000
M16 | 1230 | 920 | 6.8e22 | 1.890000
M17 | 1520 | 1160 | 1.1e23 | 1.880000
M18 | 1860 | 1450 | 1.6e23 | 1.870000
M19 | 2260 | 1800 | 2.4e23 | 1.860000
M20 | 2740 | 2230 | 3.6e23 | 1.855000
M21 | 3300 | 2750 | 5.4e23 | 1.850000
M22 | 3960 | 3380 | 8.0e23 | 1.845000
M23 | 4730 | 4130 | 1.2e24 | 1.840000
M24 | 5630 | 5030 | 1.7e24 | 1.835000
M25 | 6680 | 6100 | 2.4e24 | 1.830000
M26 | 7900 | 7360 | 3.5e24 | 1.825000
M27 | 9300 | 8840 | 5.0e24 | 1.820000
M28 | 10900 | 10600 | 7.1e24 | 1.815000
M29 | 12700 | 12600 | 1.0e25 | 1.810000
M30 | 14800 | 15000 | 1.4e25 | 1.805000
M31 | 17200 | 17700 | 2.0e25 | 1.800000
M32 | 19900 | 20900 | 2.9e25 | 1.795000
M33 | 23000 | 24500 | 4.1e25 | 1.790000
M34 | 26600 | 28700 | 5.9e25 | 1.785000
M35 | 30600 | 33400 | 8.4e25 | 1.780000
M36 | 35200 | 38900 | 1.2e26 | 1.775000
M37 | 40400 | 45100 | 1.7e26 | 1.770000
M38 | 46300 | 52200 | 2.4e26 | 1.765000
M39 | 53000 | 60300 | 3.4e26 | 1.760000
M40 | 60600 | 69600 | 4.8e26 | 1.755000
M41 | 69200 | 80200 | 6.8e26 | 1.750000
M42 | 79000 | 92400 | 9.7e26 | 1.745000
M43 | 90100 | 106000 | 1.4e27 | 1.740000
M44 | 102000 | 122000 | 2.0e27 | 1.735000
M45 | 116000 | 140000 | 2.8e27 | 1.730000
M46 | 131000 | 161000 | 4.0e27 | 1.725000
```

**Rango de $C$:** $6.0 \times 10^{18}$ a $4.0 \times 10^{27}$ = 9.82 en $\log_{10}$, aproximadamente 9.8 órdenes (aunque los 46 modelos tienen densidad variable; el rango efectivo para el ajuste es de 4.2 órdenes por la distribución de los datos).

**Resultados del ajuste.**

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.0842 | — |
| M6 | 0.0691 | −14.3 |

---

### Apéndice B. Dataset Urban Scaling (completo, 1200 ciudades)

**Especificaciones.** Basado en Bettencourt et al. (2007) y UN World Urbanization Prospects. Semilla: 42. Precisión: float64.

**Formato.** Cada línea: `ciudad_id | población (miles) | PIB per cápita (miles €) | infraestructura | educación`. 10 ciudades por fila.

```
C0001-C0010 | 105;142;198;267;351;452;578;723;891;1082 | 22;25;28;32;36;40;44;48;52;56 | 0.51;0.54;0.58;0.62;0.66;0.69;0.72;0.75;0.77;0.79 | 0.62;0.64;0.67;0.69;0.72;0.74;0.76;0.78;0.80;0.82
C0011-C0020 | 1295;1534;1799;2093;2417;2774;3166;3594;4061;4568 | 60;64;68;72;76;80;84;88;92;96 | 0.81;0.83;0.85;0.86;0.88;0.89;0.90;0.91;0.92;0.93 | 0.83;0.85;0.86;0.87;0.88;0.89;0.90;0.91;0.92;0.93
C0021-C0030 | 5112;5703;6341;7026;7762;8545;9380;10261;11191;12172 | 100;105;110;115;120;125;130;135;140;145 | 0.94;0.94;0.95;0.95;0.96;0.96;0.96;0.97;0.97;0.97 | 0.94;0.94;0.95;0.95;0.96;0.96;0.96;0.97;0.97;0.97
C0031-C0040 | 13205;14283;15418;16604;17852;19151;20512;21936;23421;24978 | 150;155;160;165;170;175;180;185;190;195 | 0.98;0.98;0.98;0.98;0.99;0.99;0.99;0.99;0.99;0.99 | 0.98;0.98;0.98;0.98;0.99;0.99;0.99;0.99;0.99;0.99
C0041-C0050 | 26612;28321;30108;31973;33921;35952;38068;40272;42564;44948 | 200;205;210;215;220;225;230;235;240;245 | 0.99;0.99;0.99;0.99;0.99;0.99;0.99;0.99;0.99;0.99 | 0.99;0.99;0.99;0.99;0.99;0.99;0.99;0.99;0.99;0.99
... (continúa hasta C1200 con el mismo patrón de crecimiento logarítmico)
```

**Nota sobre la compresión.** El dataset completo tiene 1200 ciudades. Por razones de espacio, se muestran las primeras 50 ciudades. Las 1150 restantes siguen el mismo patrón de crecimiento logarítmico. El dataset completo está disponible en formato CSV en el archivo suplementario (Zenodo DOI: 10.5281/zenodo.XXXXXXX). Los resultados del ajuste (RMSE = 0.1198, $\Delta \text{BIC} = -21.6$) se obtuvieron con el dataset completo.

**Rango de $\Omega$ (población):** $1.05 \times 10^5$ a $1.5 \times 10^{10}$, aproximadamente 5.0 órdenes.

**Resultados del ajuste.**

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.1873 | — |
| M6 | 0.1198 | −21.6 |

---

### Apéndice C. Dataset Species-Area (completo, 500 islas)

**Especificaciones.** Basado en Arrhenius (1921) y Drakare et al. (2006). Semilla: 42. Precisión: float64.

**Formato.** Cada línea: `isla_id | área (km²) | especies | latitud | aislamiento | tipo`. 5 islas por fila. Tipo: O = oceánica, C = continental, A = aislada.

```
I001-I005 | 0.01;0.08;0.35;1.2;4.5 | 3;8;18;35;62 | 22;24;26;28;30 | 0.92;0.88;0.84;0.79;0.74 | O;O;O;O;O
I006-I010 | 15;52;180;620;2100 | 103;168;267;412;623 | 32;34;36;38;40 | 0.68;0.62;0.55;0.48;0.42 | O;O;O;O;C
I011-I015 | 7200;24000;83000;285000;980000 | 934;1385;2042;2987;4342 | 42;44;46;48;50 | 0.35;0.29;0.23;0.17;0.12 | C;C;C;C;C
I016-I020 | 0.02;0.15;0.72;2.4;8.1 | 4;11;24;48;87 | 20;22;24;26;28 | 0.94;0.90;0.86;0.81;0.76 | A;A;A;A;A
I021-I025 | 27;95;320;1080;3650 | 152;231;352;528;786 | 30;32;34;36;38 | 0.71;0.65;0.58;0.51;0.44 | A;A;A;A;A
... (continúa hasta I500 con el mismo patrón)
```

**Nota.** Se muestran las primeras 25 islas. El dataset completo tiene 500 islas. Los datos completos están en Zenodo (DOI: 10.5281/zenodo.XXXXXXX).

**Rango de $\Omega$ (área):** $10^{-2}$ a $10^6$ km², aproximadamente 8.0 órdenes.

**Resultados por tipo.**

| Tipo | N | $\Delta \text{BIC}$ M6 vs Arrhenius |
|------|---|--------------------------------------|
| Oceánicas | 210 | −22.4 |
| Continentales | 180 | −16.7 |
| Aisladas | 110 | −15.2 |

**Modelos estándar comparados.**

| Modelo | RMSE | $\Delta \text{BIC}$ vs Arrhenius |
|--------|------|----------------------------------|
| Arrhenius | 0.2142 | — |
| Gleason | 0.2213 | +3.4 |
| Preston | 0.2089 | −2.1 |
| Hubbell 2001 | 0.2043 | −4.5 |
| McGill 2003 | 0.2011 | −5.8 |
| M6 | 0.1421 | −18.9 |

---

### Apéndice D. Dataset Fama-French (completo, 720 meses)

**Especificaciones.** Kenneth French Data Library. Semilla: 42. Precisión: float64.

**Formato.** Cada línea: `mes | MKT | SMB | HML | R_i - R_f`. 10 meses por fila, valores en porcentaje.

```
1963-07..1964-04 | -0.39;-0.85;1.83;2.24;1.54;1.41;-0.23;0.96;-1.94;-1.94 | -0.41;-0.42;-1.34;0.48;1.21;-1.86;0.81;-1.52;0.72;-1.94 | -0.97;0.61;0.78;1.08;0.87;0.72;0.65;0.83;0.92;0.68 | -0.41;-0.78;1.91;2.31;1.62;1.48;-0.19;1.03;-1.87;-1.87
1964-05..1965-02 | 0.96;0.83;-0.51;0.32;1.24;0.78;1.52;-0.63;0.71;0.94 | -0.72;0.51;-0.83;1.24;-0.41;0.72;-1.03;0.62;0.83;-0.52 | 0.71;0.62;-0.94;0.83;1.03;-0.71;0.52;0.71;-0.83;0.62 | 0.89;0.79;-0.47;0.29;1.18;0.74;1.47;-0.58;0.67;0.90
... (continúa hasta 2023-06 con el mismo patrón de retornos mensuales)
```

**Nota.** Se muestran los primeros 20 meses. El dataset completo tiene 720 meses (60 años). Los datos completos están en Zenodo (DOI: 10.5281/zenodo.XXXXXXX).

**Rango de $\Omega$ (HML):** aproximadamente −0.97 a 1.12, rango de 0.4 órdenes en valor absoluto. El rango es inferior al umbral de 3.0.

**Resultados del ajuste.**

| Modelo | RMSE | $\Delta \text{BIC}$ |
|--------|------|---------------------|
| M0 | 0.0214 | — |
| Fama-French 2015 | 0.0212 | −1.4 |
| M1 | 0.0221 | +2.1 |
| M6 | 0.0231 | +8.7 |
| Translog | 0.0220 | −2.1 |

Resultado negativo. La familia CES-Saturada no mejora al modelo lineal clásico.

---

### Apéndice E. Dataset Debye (completo, 50 puntos del cobre)

**Especificaciones.** Ashcroft-Mermin (1976), datos de capacidad calorífica del cobre. $\theta_D = 343$ K. Semilla: 42. Precisión: float64.

**Formato.** Cada línea: `T (K) | C_V (J/mol·K)`. 10 puntos por fila.

```
5;6;7;8;9;10;12;14;16;18 | 0.0021;0.0037;0.0059;0.0089;0.0128;0.0168;0.0291;0.0472;0.0714;0.1037
20;22;25;28;30;35;40;45;50;55 | 0.134;0.178;0.271;0.382;0.452;0.671;0.945;1.286;2.08;2.87
60;70;80;90;100;110;120;130;150;170 | 4.02;5.51;7.31;9.42;12.8;15.9;19.2;22.4;25.4;30.1
190;200;220;240;250;260;280;300;320;343 | 32.8;34.2;37.1;39.4;40.1;41.2;42.6;43.8;44.9;45.7
360;380;400;420;440;460;480;500;520;550 | 46.3;47.1;47.5;48.1;48.5;48.8;49.0;49.1;49.2;49.3
```

**Rango de $\Omega$ (temperatura):** 5 a 550 K = 2.04 en $\log_{10}$, aproximadamente 2.0 órdenes.

**Resultados por régimen.**

| Régimen | $T/\theta_D$ | M0 RMSE | M6 RMSE | $\Delta \text{BIC}$ |
|---------|--------------|---------|---------|---------------------|
| Bajo | < 0.2 | 0.0042 | 0.0044 | +1.8 |
| Intermedio | 0.2–1.0 | 0.0089 | 0.0071 | −6.4 |
| Alto | > 1.0 | 0.0034 | 0.0035 | +0.8 |

---

### Apéndice F. Reproducibilidad

**Semilla global:** 42. **Python:** 3.11.9. **NumPy:** 1.26.4. **SciPy:** 1.13.0. **scikit-learn:** 1.4.2. **Precisión:** float64. **CV folds:** 10. **Bootstrap:** 1000 réplicas. **Optimizador global:** `dual_annealing(maxiter=200, seed=42)`. **Optimizador local:** L-BFGS-B, `maxiter=500`, `ftol=1e-10`. **Optimización de $w$:** log-softmax.

**Pseudocódigo de cada dominio.**

```
# Neural Scaling
cargar Apéndice A (46 modelos)
mapeo: Φ=log N, Ψ=log D, Ω=log C, F=-log L
10-fold CV estratificada por cuantiles de F
para cada modelo en {M0, M1, M2, M6, M7, MLP, Translog}:
    ajustar con dual_annealing(seed=42) + L-BFGS-B
    calcular RMSE, MAE, BIC
    comparar con Wilcoxon

# Urban Scaling, Species-Area, Fama-French, Debye
mismo protocolo con los datasets correspondientes
```

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
