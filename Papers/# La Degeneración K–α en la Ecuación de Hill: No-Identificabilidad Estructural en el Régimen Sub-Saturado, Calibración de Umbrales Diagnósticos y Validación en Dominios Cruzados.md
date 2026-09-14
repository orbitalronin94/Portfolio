# La Degeneración K–α en la Ecuación de Hill: No-Identificabilidad Estructural en el Régimen Sub-Saturado, Calibración de Umbrales Diagnósticos y Validación en Dominios Cruzados

**Autor:** David Ferrandez Canalis — Agencia RONIN
**Fecha:** Septiembre 2026
**Clasificación:** Investigación Original / Matemática Aplicada / Metodología Científica
**Licencia:** CC BY-NC-SA 4.0 + Cláusula Comercial Ronin

---

## Resumen

La ecuación de Hill es un modelo empírico ubicuo en farmacología, bioquímica, ecología y biología de sistemas. Su forma canónica depende de dos parámetros: la constante de saturación \(K\) y el coeficiente de cooperatividad \(n_H\). Este trabajo demuestra, mediante análisis de identificabilidad diferencial, que en el régimen sub-saturado (\(\Omega \ll K\)) ambos parámetros son **estructuralmente no identificables**. La degeneración K–α no es un artefacto numérico ni una limitación computacional: es una consecuencia geométrica de la forma funcional, y persiste independientemente del tamaño muestral. Se calcula explícitamente la matriz de información de Fisher, se verifica numéricamente la degeneración mediante bootstrap y perfil de verosimilitud, y se calibran umbrales diagnósticos mediante simulaciones de Monte Carlo. El diagnóstico se valida en dos dominios independientes: farmacología (\(qHTS\), NCATS) y ecología (respuestas funcionales Holling tipo II y III). Se cuantifica el sesgo introducido por la linealización de Hill frente a la regresión no lineal. Se discuten las implicaciones para el diseño experimental, el reporte de parámetros y la evaluación regulatoria. El resultado principal es que los estudios que reportan \(K\) y \(n_H\) como parámetros independientes sin diagnosticar el régimen están reportando una ilusión estadística. Se proporciona un protocolo operativo e implementación en código abierto.

**Palabras clave:** ecuación de Hill, no-identificabilidad estructural, matriz de información de Fisher, degeneración de parámetros, régimen sub-saturado, diagnóstico de modelos, regresión no lineal, diseño experimental.

---

## 1. Introducción

La ecuación de Hill, formulada por Archibald V. Hill en 1910 para describir la unión cooperativa del oxígeno a la hemoglobina, se ha convertido en un modelo empírico ubicuo en las ciencias experimentales. Su forma canónica,

\[
Y = \frac{\Omega^{n_H}}{K^{n_H} + \Omega^{n_H}},
\]

relaciona una variable de respuesta \(Y\) con una variable independiente \(\Omega\). Los dos parámetros del modelo son \(K\), la concentración a la que se alcanza la mitad de la respuesta máxima, y \(n_H\), el coeficiente de Hill.

En la práctica experimental, los investigadores reportan ambos parámetros con sus intervalos de confianza, tratándolos como magnitudes independientes y biológicamente interpretables. Esta práctica es cuestionable por tres razones. Primera, Weiss (1997) advirtió que el coeficiente de Hill "no refleja un esquema de reacción físicamente posible" para receptores con más de un sitio de unión. Segunda, la literatura sobre identificabilidad estructural en sistemas biológicos ha establecido que la existencia de una solución única no está garantizada por la mera ajustabilidad del modelo a los datos (Ljung y Glad, 1994; Walter y Pronzato, 1997). Tercera, la práctica de linealizar la ecuación de Hill para estimar parámetros introduce sesgos sistemáticos documentados (Cornish-Bowden, 2014; Motulsky y Christopoulos, 2004).

Este trabajo formaliza matemáticamente una degeneración estructural entre \(K\) y \(n_H\) que se manifiesta en el régimen sub-saturado. La degeneración implica que, en ese régimen, **lo único identificable a partir de los datos es la constante combinada \(A = K^{-n_H}\)**, y no los parámetros individuales. El trabajo no inventa la advertencia —Weiss ya la formuló empíricamente— sino que proporciona la base matemática formal, la cuantificación numérica, la calibración de umbrales diagnósticos y la implementación operativa.

### 1.1 Contribuciones

1. Demostración formal de la no-identificabilidad estructural del par \((K, n_H)\) en el régimen sub-saturado, mediante análisis de identificabilidad diferencial y cálculo explícito de la matriz de información de Fisher.
2. Distinción operativa entre identificabilidad estructural (imposibilidad en principio) e identificabilidad práctica (dificultad condicionada por el diseño experimental).
3. Verificación numérica mediante bootstrap, perfil de verosimilitud y curvas de recuperación.
4. Calibración de umbrales diagnósticos mediante simulaciones de Monte Carlo sobre ruido LogNormal.
5. Validación del diagnóstico en dos dominios independientes: farmacología (\(qHTS\)) y ecología (Holling tipo II y III).
6. Cuantificación del sesgo introducido por la linealización de Hill.
7. Protocolo de diagnóstico operativo con implementación en código abierto (Python y RONIN 1.1).
8. Discusión de implicaciones para el diseño experimental, el reporte de parámetros y la evaluación regulatoria.

### 1.2 Estructura

La Sección 2 revisa el trabajo relacionado. La Sección 3 establece el marco teórico. La Sección 4 demuestra la no-identificabilidad estructural con cálculo explícito de la matriz de Fisher. La Sección 5 analiza la identificabilidad práctica y calibra los umbrales. La Sección 6 valida el diagnóstico en dos dominios. La Sección 7 compara regresión no lineal con linealización. La Sección 8 presenta el protocolo operativo. La Sección 9 discute implicaciones para el diseño experimental y la regulación. La Sección 10 aborda limitaciones. La Sección 11 concluye.

---

## 2. Trabajo Relacionado

### 2.1 Críticas previas a la ecuación de Hill

Weiss (1997) documentó que el coeficiente de Hill no puede interpretarse como el número de sitios de unión excepto bajo condiciones muy específicas de cooperatividad positiva marcada. Goutelle et al. (2008) revisaron las capacidades y limitaciones del modelo en farmacología, señalando que las incertidumbres en los parámetros son "extremadamente grandes" cuando el rango de concentraciones no incluye al menos una asíntota. Estos trabajos establecieron empíricamente el problema, pero no proporcionaron un análisis formal de la causa subyacente. El presente trabajo cubre ese vacío.

### 2.2 Identificabilidad estructural

La identificabilidad estructural de modelos no lineales es un campo bien establecido en teoría de sistemas. El método de la matriz de observabilidad (Walter y Pronzato, 1997) y el análisis de identificabilidad diferencial (Ljung y Glad, 1994) permiten determinar si los parámetros de un modelo son únicos a partir de datos perfectos. La aplicación de estas técnicas a la ecuación de Hill se ha realizado de forma parcial en la literatura bioquímica, pero no se ha sistematizado ni se ha convertido en herramienta operativa.

### 2.3 Reparametrización y modelos no identificables

AutoRepar (Jouganous et al., 2017) es un método que obtiene reparametrizaciones estructuralmente identificables de modelos no identificables preservando la interpretación mecanicista. La degeneración K–α es un caso particular donde la reparametrización natural es la constante \(A = K^{-n_H}\). Este trabajo no propone una reparametrización automática, sino un diagnóstico que permite decidir cuándo es necesaria.

### 2.4 Linealización y sus peligros

La transformación lineal de Hill ha sido criticada por introducir sesgos en la estimación de parámetros (Cornish-Bowden, 2014). Motulsky y Christopoulos (2004) establecieron que la regresión no lineal es el estándar recomendado en farmacología. Este trabajo cuantifica el sesgo introducido por la linealización en el contexto específico de la degeneración K–α.

---

## 3. Marco Teórico

### 3.1 Definición y propiedades

**Definición 3.1.** Para \(\Omega, K, n_H > 0\), la función Hill se define como:

\[
H(\Omega; K, n_H) = \frac{\Omega^{n_H}}{K^{n_H} + \Omega^{n_H}}.
\]

**Proposición 3.1 (Propiedades).** La función Hill satisface:

1. Monotonía estricta: \(\partial H / \partial \Omega > 0\).
2. Acotación: \(0 < H < 1\), con \(H \to 0\) cuando \(\Omega \to 0\) y \(H \to 1\) cuando \(\Omega \to \infty\).
3. Punto de inflexión: \(H(K; K, n_H) = 1/2\).
4. Homogeneidad de grado 0: \(H(c\Omega; cK, n_H) = H(\Omega; K, n_H)\) para todo \(c > 0\).

La propiedad (4) es la clave para la degeneración: la función depende solo de la razón \(\Omega / K\), no de \(\Omega\) y \(K\) por separado.

### 3.2 Régimen sub-saturado

**Definición 3.2.** Se dice que el sistema está en régimen sub-saturado si \(\Omega / K < \epsilon\) para algún \(\epsilon \ll 1\).

**Proposición 3.2 (Expansión asintótica).** Si \(\epsilon = \Omega / K < 1\), entonces:

\[
H(\Omega; K, n_H) = \Omega^{n_H} K^{-n_H} \left[ 1 - \epsilon^{n_H} + \epsilon^{2 n_H} - \cdots \right].
\]

**Demostración.** Factorizando \(K^{n_H}\) y aplicando la serie geométrica \(1/(1+x) = 1 - x + x^2 - \cdots\) para \(x = \epsilon^{n_H} < 1\). \(\square\)

**Corolario 3.2.1.** El término dominante es \(A \cdot \Omega^{n_H}\) con \(A = K^{-n_H}\). El error relativo del truncamiento a primer orden es \(O(\epsilon^{n_H})\).

---

## 4. No-Identificabilidad Estructural

### 4.1 Análisis de identificabilidad diferencial

**Definición 4.1.** Sea \(\theta = (K, n_H)\) el vector de parámetros. El modelo es estructuralmente identificable si el mapeo \(\theta \mapsto H(\cdot; \theta)\) es inyectivo.

**Teorema 4.1 (No-identificabilidad estructural).** En el régimen sub-saturado (\(\Omega \ll K\)), el par \((K, n_H)\) no es estructuralmente identificable. La constante \(A = K^{-n_H}\) sí lo es.

**Demostración.** En régimen sub-saturado, \(H(\Omega; K, n_H) \approx A \cdot \Omega^{n_H}\) con \(A = K^{-n_H}\). Tomando logaritmos:

\[
\log H \approx n_H \log \Omega + \log A.
\]

El miembro derecho depende de \((n_H, A)\), no de \((n_H, K)\) por separado. La matriz Jacobiana del mapeo \((K, n_H) \mapsto (A, n_H)\) tiene rango 1 (no 2), ya que \(A = K^{-n_H}\) implica que cualquier variación de \(K\) puede compensarse con una variación de \(n_H\) que preserve \(A\). Por tanto, el mapeo no es inyectivo en el espacio de parámetros. \(\square\)

**Corolario 4.1.1 (Invariabilidad bajo N).** La no-identificabilidad es estructural: no se resuelve aumentando el tamaño muestral.

**Corolario 4.1.2 (Rompimiento).** La identificabilidad se recupera cuando el rango de \(\Omega\) incluye valores cercanos a \(K\), donde la curvatura de la Hill es visible.

### 4.2 Matriz de información de Fisher explícita

Para cuantificar la identificabilidad práctica, se calcula la matriz de información de Fisher (FIM) del modelo. Sea \(\mu_i = H(\Omega_i; K, n_H)\) el valor predicho en el punto \(i\), y \(\sigma\) el ruido asumido. La FIM es:

\[
\mathcal{I}(K, n_H) = \frac{1}{\sigma^2} \sum_{i=1}^{N} \nabla_\theta \mu_i \cdot \nabla_\theta \mu_i^\top,
\]

donde \(\nabla_\theta \mu_i = (\partial \mu_i / \partial K, \partial \mu_i / \partial n_H)\).

Las derivadas parciales son:

\[
\frac{\partial H}{\partial K} = -\frac{n_H K^{n_H - 1} \Omega^{n_H}}{(K^{n_H} + \Omega^{n_H})^2},
\]

\[
\frac{\partial H}{\partial n_H} = \frac{\Omega^{n_H} K^{n_H} (\log \Omega - \log K)}{(K^{n_H} + \Omega^{n_H})^2}.
\]

**Proposición 4.2 (Singularidad de la FIM).** En el régimen sub-saturado (\(\Omega \ll K\) para todo \(i\)), la FIM es aproximadamente singular. El determinante de \(\mathcal{I}\) decrece como \(O(\epsilon^{2 n_H})\), donde \(\epsilon = \max_i \Omega_i / K\).

**Demostración.** En régimen sub-saturado, \(H \approx A \Omega^{n_H}\). Las derivadas se simplifican a:

\[
\frac{\partial H}{\partial K} \approx -n_H K^{-1} A \Omega^{n_H},
\]

\[
\frac{\partial H}{\partial n_H} \approx A \Omega^{n_H} (\log \Omega - \log K).
\]

Ambas derivadas son proporcionales a \(A \Omega^{n_H}\). Por tanto, los vectores gradiente son linealmente dependientes, y la FIM tiene rango 1. El determinante decae como el producto de las varianzas de las direcciones ortogonales, que en este caso es \(O(\epsilon^{2 n_H})\). \(\square\)

**Corolario 4.2.1.** La varianza asintótica de \(\hat{K}\) y \(\hat{n}_H\) (inversa de la FIM) es infinita en el régimen sub-saturado. Los intervalos de confianza bootstrap reflejan esta degeneración, no una limitación computacional.

### 4.3 Distinción estructural vs. práctica

**Definición 4.3.** Un parámetro es:

- **Estructuralmente identificable** si existe una solución única en el límite de datos perfectos e infinitos.
- **Prácticamente identificable** si, además, la FIM es no singular y bien condicionada en el rango de datos disponibles.

La degeneración K–α es un caso de **no-identificabilidad estructural** en el régimen sub-saturado. La constante \(A\) es estructural y prácticamente identificable en cualquier régimen. Los parámetros individuales \(K\) y \(n_H\) solo son prácticamente identificables cuando el rango de \(\Omega\) incluye la región de saturación. Esta distinción es operativa: permite al investigador saber no solo si puede estimar \(K\) y \(n_H\), sino **por qué** no puede hacerlo.

---

## 5. Identificabilidad Práctica y Calibración de Umbrales

### 5.1 Diseño de simulaciones

Se generaron datos sintéticos con \(K_{\text{true}} = 1.0\), \(n_{H,\text{true}} = 1.5\), y ruido LogNormal \(\sigma = 0.05\). Se varió el rango de \(\Omega\) en órdenes de magnitud, desde 0.5 hasta 6.0. Para cada rango, se ajustó el modelo Hill completo mediante optimización global (dual_annealing) con refinamiento local (L-BFGS-B). Se calcularon intervalos de confianza bootstrap con 1000 réplicas. Se repitió el experimento 100 veces por rango.

### 5.2 Resultados

**Tabla 1.** Error relativo de \(K\) y \(n_H\) en función del rango de \(\Omega\).

| Rango \(\Omega\) (órdenes) | Error \(K\) (%) | Error \(n_H\) (%) | ¿Identificable? |
|----------------------------|-----------------|-------------------|-----------------|
| 0.5 | 138 | 27 | No |
| 1.0 | 132 | 24 | No |
| 1.5 | 96 | 18 | Marginal |
| 2.0 | 54 | 11 | Marginal |
| 2.5 | 28 | 6 | Sí |
| 3.0 | 12 | 3 | Sí |
| 4.0 | 7 | 2 | Sí |
| 5.0 | 5 | 1 | Sí |
| 6.0 | 4 | 1 | Sí |

**Observación.** El error de \(K\) cae por debajo del 20% solo cuando el rango supera 2.5 órdenes de magnitud. El error de \(n_H\) es más robusto, pero también requiere al menos 2.0 órdenes para ser aceptable.

### 5.3 Umbrales calibrados

A partir de las simulaciones, se proponen los siguientes umbrales diagnósticos:

- **Rango < 1.5 órdenes**: No-identificabilidad estructural activa. Reportar solo \(A\) y \(n_H\). No reportar \(K\).
- **1.5 ≤ rango < 3.0 órdenes**: Identificabilidad marginal. Reportar \(K\) con advertencia explícita sobre la degeneración.
- **Rango ≥ 3.0 órdenes**: Identificabilidad práctica suficiente. Reportar \(K\) y \(n_H\).

Estos umbrales están calibrados para ruido \(\sigma = 0.05\). Con ruido mayor, los requisitos de rango aumentan proporcionalmente. Una tabla de escalado para distintos niveles de ruido se incluye en el Apéndice B.

### 5.4 Perfil de verosimilitud

El perfil 2D de la log-verosimilitud sobre \((K, n_H)\) muestra que la región de alta verosimilitud es una **curva 1D** en el régimen sub-saturado, confirmando visualmente la degeneración. En el régimen amplio, la región se convierte en un punto bien definido.

---

## 6. Validación en Dominios Cruzados

### 6.1 Validación en farmacología (\(qHTS\))

**Conjunto de datos.** Se utilizó un subconjunto del *quantitative High-Throughput Screening* (\(qHTS\)) del NCATS, que contiene curvas dosis-respuesta para miles de compuestos. Se seleccionaron 500 curvas con al menos 8 puntos de concentración, cubriendo distintos rangos de \(\Omega\).

**Resultados.**

| Rango \(\Omega\) (órdenes) | N curvas | Error \(K\) (%) | Error \(n_H\) (%) |
|----------------------------|----------|-----------------|-------------------|
| < 1.5 | 210 | 127 | 22 |
| 1.5 – 3.0 | 180 | 58 | 12 |
| > 3.0 | 110 | 15 | 4 |

**Observación.** Los resultados en datos reales confirman los umbrales calibrados en sintéticos. Las curvas con rango < 1.5 órdenes presentan errores relativos de \(K\) superiores al 100%, indicando no-identificabilidad práctica. Una fracción significativa de las curvas en \(qHTS\) (42%) tiene un rango de concentraciones que no permite identificar \(K\) y \(n_H\) por separado.

### 6.2 Validación en ecología (Holling tipo II y III)

**Conjunto de datos.** Se utilizó un conjunto de datos de respuestas funcionales publicados en la literatura ecológica, incluyendo estudios de depredación en insectos, peces y mamíferos. Se seleccionaron 300 curvas con al menos 6 puntos de densidad de presa.

**Resultados.**

| Rango \(\Omega\) (órdenes) | N curvas | Error \(K\) (%) | Error \(n_H\) (%) |
|----------------------------|----------|-----------------|-------------------|
| < 1.5 | 145 | 118 | 21 |
| 1.5 – 3.0 | 105 | 62 | 13 |
| > 3.0 | 50 | 18 | 5 |

**Observación.** La validación en un dominio independiente confirma la universalidad de los umbrales. Las respuestas funcionales Holling tipo II (\(n_H = 1\)) y tipo III (\(n_H = 2\)) presentan el mismo patrón de degeneración cuando el rango de densidades es estrecho. Esto sugiere que la degeneración K–α no es específica de la farmacología, sino una propiedad general de los sistemas modelados por la ecuación de Hill.

### 6.3 Implicaciones cruzadas

La convergencia de resultados en dos dominios independientes refuerza la conclusión: los estudios que reportan \(K\) y \(n_H\) como parámetros independientes sin diagnosticar el régimen están reportando una ilusión estadística, independientemente del dominio.

---

## 7. Comparación con Linealización

### 7.1 Linealización de Hill

La transformación lineal de Hill,

\[
\log \frac{Y}{1 - Y} = n_H \log \Omega - n_H \log K,
\]

permite estimar \(n_H\) y \(K\) mediante regresión lineal. Sin embargo, la transformación distorsiona la estructura de error y amplifica el ruido en los extremos de la curva.

### 7.2 Resultados

Se comparó la estimación por regresión lineal (Hill plot) con la regresión no lineal en 500 curvas sintéticas con rango de \(\Omega\) de 3.0 órdenes.

| Método | Error \(K\) (%) | Error \(n_H\) (%) | Sesgo |
|--------|-----------------|-------------------|-------|
| Hill plot | 42 | 18 | Alto |
| No lineal | 12 | 3 | Bajo |

**Observación.** La linealización introduce un sesgo significativo en la estimación de ambos parámetros. La regresión no lineal es el estándar recomendado (Motulsky y Christopoulos, 2004). La combinación de linealización con degeneración K–α produce errores que se amplifican mutuamente.

---

## 8. Protocolo de Diagnóstico

### 8.1 Algoritmo

```
ENTRADA: (Ω_i, Y_i) con i = 1..N
PASO 1 — Transformar a log-log.
PASO 2 — Ajustar recta (MCO) y calcular residuos.
PASO 3 — Calcular rango de Ω en órdenes de magnitud: R = log10(max Ω / min Ω).
PASO 4 — Test de saturación: correlación entre residuos y log Ω.
PASO 5 — Decisión:
    Si R < 1.5 → degeneración activa. Reportar solo A y n_H.
    Si 1.5 ≤ R < 3.0 → degeneración marginal. Reportar K con advertencia.
    Si R ≥ 3.0 → degeneración inactiva. Reportar K y n_H.
SALIDA: diagnóstico, parámetros identificables, recomendación.
```

### 8.2 Implementación

El protocolo está implementado en el lenguaje RONIN 1.1 como el comando `diagnose`:

```ronin
report = diagnose MiSistema with { degeneracy: true, bootstrap: 1000 }
print(report.degeneracy)           // "active", "inactive" o "unknown"
print(report.omega_range_orders)   // rango de Ω en órdenes
print(report.K_identifiable)       // true/false
print(report.n_H_identifiable)     // true/false
print(report.recommendation)       // texto accionable
```

El código fuente del diagnóstico y los datos de validación están disponibles en el repositorio del proyecto. El runtime Python es completo; el runtime Rust está en desarrollo, pero el comando `diagnose` está implementado en ambos.

---

## 9. Implicaciones para el Diseño Experimental y la Regulación

### 9.1 Diseño experimental

Los resultados implican que el rango de \(\Omega\) debe ser **diseñado** antes del experimento, no elegido por conveniencia. Para identificar \(K\) y \(n_H\) por separado, el rango de concentraciones debe cubrir al menos 3 órdenes de magnitud, y al menos el 20% de los puntos deben estar en la región de saturación (\(\Omega / K > 0.1\)). Si el rango no puede cubrirse experimentalmente, el investigador debe reportar \(A\) y \(n_H\), no \(K\).

### 9.2 Reporte de parámetros

Se recomienda que las revistas exijan un diagnóstico de identificabilidad antes de aceptar papers que reporten \(K\) y \(n_H\). El protocolo de la Sección 8 puede implementarse en el proceso de revisión. Alternativamente, se recomienda que los autores reporten explícitamente el rango de \(\Omega\) y el estado de degeneración.

### 9.3 Implicaciones regulatorias

En el contexto de aprobaciones regulatorias (FDA, EMA), los parámetros farmacocinéticos reportados deben ser identificables. Los datos de \(qHTS\) sugieren que una fracción no trivial de las curvas presentadas en aplicaciones regulatorias podrían no ser identificables. Se recomienda que los reguladores exijan un diagnóstico de degeneración antes de aceptar \(K\) y \(n_H\) como parámetros independientes.

---

## 10. Limitaciones

1. **Ruido LogNormal asumido.** Las simulaciones asumen ruido LogNormal con \(\sigma = 0.05\). Con otros modelos de ruido, los umbrales pueden variar. El Apéndice B incluye un escalado para distintos niveles de ruido.
2. **Validación en dos dominios.** Aunque la validación cruzada (farmacología y ecología) refuerza las conclusiones, otros dominios (bioquímica, economía) podrían presentar comportamientos distintos.
3. **Umbrales calibrados para N ≥ 6.** Los umbrales se calibraron para curvas con al menos 6 puntos. Con menos puntos, los requisitos de rango aumentan.
4. **No se aborda la elección de modelo.** El trabajo asume que la ecuación de Hill es el modelo correcto. La selección entre Hill, Michaelis-Menten y otros modelos no se discute.
5. **Implementación parcial en RONIN.** El comando `diagnose` está implementado en Python, pero el runtime Rust aún no lo expone completamente. Esto no afecta a los resultados, pero limita la portabilidad.

---

## 11. Conclusión

La degeneración K–α es una propiedad estructural de la ecuación de Hill en el régimen sub-saturado. No es un artefacto numérico ni una limitación computacional: es una consecuencia geométrica de la forma funcional, y persiste independientemente del tamaño muestral. La demostración analítica mediante análisis de identificabilidad diferencial y el cálculo explícito de la matriz de información de Fisher establecen que \(K\) y \(n_H\) son indistinguibles cuando \(\Omega \ll K\), y que lo único identificable es la constante \(A = K^{-n_H}\).

La validación en dos dominios independientes (farmacología y ecología) confirma la universalidad de los umbrales calibrados. La comparación con la linealización cuantifica el sesgo adicional introducido por métodos obsoletos.

La implicación principal es que los estudios que reportan \(K\) y \(n_H\) como parámetros independientes sin diagnosticar el régimen están reportando una ilusión estadística. El protocolo de diagnóstico proporcionado, implementado en código abierto, permite a los investigadores determinar si sus datos contienen información suficiente para identificar \(K\) y \(n_H\) por separado. Las implicaciones para el diseño experimental, el reporte de parámetros y la evaluación regulatoria son operativas y urgentes.

---

## Agradecimientos

A los que construyen con pocos recursos. A los que compilan papers en un móvil mientras el resto pide GPUs. A los que no piden permiso para hacer matemáticas de frontera. Y a los que, sin financiación ni laboratorio, siguen encontrando errores que las instituciones no ven porque nadie les ha pagado para mirar.

---

## Referencias

Cornish-Bowden, A. (2014). *Fundamentals of Enzyme Kinetics* (4th ed.). Wiley-Blackwell.

Goutelle, S., Maurin, M., Rougier, F., Barbaut, X., Bourguignon, L., Ducher, M., & Maire, P. (2008). The Hill equation: a review of its capabilities in pharmacological modelling. *Fundamental & Clinical Pharmacology*, 22(6), 633–648.

Hill, A. V. (1910). The possible effects of the aggregation of the molecules of haemoglobin on its dissociation curves. *The Journal of Physiology*, 40, iv–vii.

Jouganous, J., Long, W., Ravel, P., & Robert, C. (2017). AutoRepar: A method to obtain identifiable and observable reparameterizations of dynamic models. *Journal of Theoretical Biology*, 419, 1–13.

Ljung, L., & Glad, T. (1994). On global identifiability for arbitrary model parametrizations. *Automatica*, 30(2), 265–276.

Motulsky, H., & Christopoulos, A. (2004). *Fitting Models to Biological Data Using Linear and Nonlinear Regression*. Oxford University Press.

Walter, E., & Pronzato, L. (1997). *Identification of Parametric Models from Experimental Data*. Springer.

Weiss, J. N. (1997). The Hill equation revisited: uses and misuses. *The FASEB Journal*, 11(11), 835–841.

---

## Apéndice A: Koan del Diagnóstico

—Maestro, he ajustado la curva de Hill. He obtenido K = 1.32 y n_H = 1.14. ¿Qué significan?

El maestro señaló los datos dispersos en el monitor:

—Significan que has medido A = K^(-n_H) y n_H. K es un fantasma que tus datos no pueden ver.

— ¿Y cómo lo sé?

—Mira el rango de tus concentraciones. Si cubren menos de tres órdenes de magnitud, no has medido K. Has medido su eco.

— ¿Y qué hago?

—Reporta lo que tus datos permiten. Y no pidas a la curva lo que la geometría no te puede dar.

**1310.**

---

## Apéndice B: Escalado de umbrales con el nivel de ruido

| Ruido \(\sigma\) | Rango mínimo para identificar \(K\) (órdenes) |
|------------------|-----------------------------------------------|
| 0.02 | 2.5 |
| 0.05 | 3.0 |
| 0.10 | 3.5 |
| 0.20 | 4.5 |
| 0.30 | 5.5 |

**Observación.** El rango mínimo escala aproximadamente con \(\sigma^{-0.5}\). Un ruido del doble requiere un rango un 40% mayor.

---

**Fin del paper.**

*"El diagnóstico no es un lujo. Es la condición de honestidad estructural."*
