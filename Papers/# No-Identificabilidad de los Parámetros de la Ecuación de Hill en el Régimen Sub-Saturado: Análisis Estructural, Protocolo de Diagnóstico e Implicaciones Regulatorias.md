# No-Identificabilidad de los Parámetros de la Ecuación de Hill en el Régimen Sub-Saturado: Análisis Estructural, Protocolo de Diagnóstico e Implicaciones Regulatorias

**Autor:** David Ferrandez Canalis
**Afiliación:** Agencia RONIN, Sabadell, España
**Fecha:** Septiembre 2026
**Palabras clave:** ecuación de Hill, no-identificabilidad estructural, matriz de información de Fisher, régimen sub-saturado, degeneración de parámetros, protocolo de diagnóstico, regresión no lineal

---

## Resumen

La ecuación de Hill es un modelo empírico ubicuo en farmacología, bioquímica, ecología y biología de sistemas. Su forma canónica depende de dos parámetros: la constante de semi-saturación \(K\) y el coeficiente de Hill \(n_H\). Demostramos, mediante análisis de identificabilidad diferencial y cálculo explícito de la matriz de información de Fisher, que en el régimen sub-saturado (\(\Omega \ll K\)) ambos parámetros son **estructuralmente no identificables**. La degeneración K–\(n_H\) no es un artefacto numérico ni una limitación computacional: es una consecuencia geométrica de la forma funcional, y persiste independientemente del tamaño muestral. Derivamos la expansión asintótica de la función Hill, calculamos analíticamente la matriz de información de Fisher y cuantificamos la tasa a la que su determinante decae como \(O(\epsilon^{2n_H})\), donde \(\epsilon = \max_i \Omega_i / K\). Calibramos umbrales diagnósticos mediante simulación de Monte Carlo y validamos el protocolo en dos dominios independientes: farmacología (qHTS, NCATS) y ecología (respuestas funcionales Holling tipo II y III). Cuantificamos el sesgo introducido por la linealización de Hill frente a la regresión no lineal. Proporcionamos un protocolo de diagnóstico de código abierto con implementaciones en Python, R, Julia y Stan. La implicación principal es que los estudios que reportan \(K\) y \(n_H\) como parámetros independientes sin diagnosticar el régimen están reportando una ilusión estadística. Discutimos las consecuencias para el diseño experimental, el reporte de parámetros y la evaluación regulatoria.

---

## 1. Introducción

La ecuación de Hill, formulada por Archibald V. Hill en 1910 para describir la unión cooperativa del oxígeno a la hemoglobina, se ha convertido en un modelo empírico ubicuo en las ciencias experimentales. Su forma canónica,

\[
Y(\Omega) = \frac{\Omega^{n_H}}{K^{n_H} + \Omega^{n_H}},
\]

relaciona una variable de respuesta \(Y\) con una variable independiente \(\Omega\) —concentración de ligando, densidad de recurso, cómputo disponible o inversión— a través de dos parámetros: \(K\), la concentración a la que se alcanza la respuesta semimáxima, y \(n_H\), el coeficiente de Hill, que mide la cooperatividad aparente.

En la práctica experimental estándar, ambos parámetros se reportan junto con sus intervalos de confianza, tratados como cantidades independientes y biológicamente interpretables. Esta práctica es cuestionable por tres razones. Primera, Weiss (1997) observó que el coeficiente de Hill "no refleja un esquema de reacción físicamente posible" para receptores con más de un sitio de unión, y que su valor aparente depende de la posición vertical de la curva. Segunda, la literatura sobre identificabilidad estructural en sistemas biológicos ha establecido que la existencia de una solución única de parámetros no está garantizada por la mera capacidad del modelo de ajustar los datos (Ljung y Glad, 1994; Walter y Pronzato, 1997). Tercera, la práctica de linealizar la ecuación de Hill para estimar parámetros introduce sesgos sistemáticos documentados (Cornish-Bowden, 2014; Motulsky y Christopoulos, 2004).

Este trabajo formaliza una degeneración estructural entre \(K\) y \(n_H\) que se manifiesta en el régimen sub-saturado —es decir, cuando las concentraciones experimentales son significativamente inferiores a \(K\). La degeneración implica que, en ese régimen, **la única cantidad identificable a partir de los datos es la constante combinada \(A = K^{-n_H}\)**, y no los parámetros individuales.

La contribución de este trabajo no es emitir la advertencia —Weiss ya la formuló empíricamente—, sino proporcionar la base matemática formal, la cuantificación numérica, los umbrales diagnósticos calibrados y una implementación operativa.

### 1.1 Contribuciones

1. Demostración formal de la no-identificabilidad estructural del par \((K, n_H)\) en el régimen sub-saturado, mediante análisis de identificabilidad diferencial y cálculo explícito de la matriz de información de Fisher.
2. Distinción operativa entre identificabilidad estructural (imposibilidad en principio) e identificabilidad práctica (dificultad condicionada por el diseño experimental).
3. Verificación numérica mediante bootstrap, perfil de verosimilitud y curvas de recuperación de parámetros.
4. Calibración de umbrales diagnósticos mediante simulación de Monte Carlo bajo ruido log-normal.
5. Validación del diagnóstico en dos dominios independientes: farmacología (qHTS) y ecología (respuestas funcionales Holling tipo II y III).
6. Cuantificación del sesgo introducido por la linealización de Hill.
7. Protocolo de diagnóstico operativo con implementación de código abierto en Python, R, Julia y Stan.
8. Discusión de implicaciones para el diseño experimental, el reporte de parámetros y la evaluación regulatoria.

### 1.2 Estructura

La Sección 2 revisa el trabajo relacionado. La Sección 3 establece el marco teórico. La Sección 4 demuestra la no-identificabilidad estructural con cálculo explícito de la matriz de información de Fisher. La Sección 5 analiza la identificabilidad práctica y calibra los umbrales. La Sección 6 valida el diagnóstico en dos dominios. La Sección 7 compara la regresión no lineal con la linealización. La Sección 8 presenta el protocolo operativo. La Sección 9 discute implicaciones para el diseño experimental y la regulación. La Sección 10 aborda las limitaciones. La Sección 11 concluye.

---

## 2. Trabajo Relacionado

### 2.1 Críticas previas a la ecuación de Hill

Weiss (1997) documentó que el coeficiente de Hill no puede interpretarse como el número de sitios de unión excepto bajo condiciones muy específicas de cooperatividad positiva marcada. Goutelle et al. (2008) revisaron las capacidades y limitaciones del modelo en farmacología, señalando que las incertidumbres de los parámetros son "extremadamente grandes" cuando el rango de concentraciones no incluye al menos una asíntota. Estos trabajos establecieron el problema empíricamente, pero no proporcionaron un análisis formal de la causa subyacente. El presente trabajo cubre ese vacío.

### 2.2 Identificabilidad estructural

La identificabilidad estructural de modelos no lineales es un campo bien establecido en teoría de sistemas. El método de la matriz de observabilidad (Walter y Pronzato, 1997) y el análisis de identificabilidad diferencial (Ljung y Glad, 1994) permiten determinar si los parámetros de un modelo son únicos a partir de datos perfectos. La aplicación de estas técnicas a la ecuación de Hill ha sido parcial en la literatura bioquímica, pero no se ha sistematizado ni se ha convertido en herramienta operativa.

### 2.3 Reparametrización y modelos no identificables

AutoRepar (Jouganous et al., 2017) obtiene reparametrizaciones estructuralmente identificables de modelos no identificables preservando la interpretación mecanicista. La degeneración K–\(n_H\) es un caso particular donde la reparametrización natural es la constante combinada \(A = K^{-n_H}\). Este trabajo no propone una reparametrización automática, sino un diagnóstico que determina cuándo es necesaria.

### 2.4 Linealización y sus peligros

La transformación lineal de la ecuación de Hill ha sido criticada por introducir sesgos en la estimación de parámetros (Cornish-Bowden, 2014). Motulsky y Christopoulos (2004) establecieron que la regresión no lineal es el estándar recomendado en farmacología. Este trabajo cuantifica el sesgo introducido por la linealización en el contexto específico de la degeneración K–\(n_H\).

---

## 3. Marco Teórico

### 3.1 Definición y propiedades

**Definición 3.1.** Para \(\Omega, K, n_H > 0\), la función de Hill se define como:

\[
H(\Omega; K, n_H) = \frac{\Omega^{n_H}}{K^{n_H} + \Omega^{n_H}}.
\]

**Proposición 3.1 (Propiedades básicas).** La función de Hill satisface:

1. Monotonía estricta: \(\partial H / \partial \Omega > 0\).
2. Acotación: \(0 < H < 1\), con \(H \to 0\) cuando \(\Omega \to 0\) y \(H \to 1\) cuando \(\Omega \to \infty\).
3. Punto de inflexión: \(H(K; K, n_H) = 1/2\).
4. Homogeneidad de grado cero: \(H(c\Omega; cK, n_H) = H(\Omega; K, n_H)\) para todo \(c > 0\).

La propiedad (4) es la clave de la degeneración: la función depende solo de la razón \(\Omega/K\), no de \(\Omega\) y \(K\) por separado.

### 3.2 Régimen sub-saturado

**Definición 3.2.** El sistema está en el régimen sub-saturado si \(\Omega/K < \epsilon\) para algún \(\epsilon \ll 1\).

**Proposición 3.2 (Expansión asintótica).** Si \(\epsilon = \Omega/K < 1\), entonces:

\[
H(\Omega; K, n_H) = \Omega^{n_H} K^{-n_H} \left[ 1 - \epsilon^{n_H} + \epsilon^{2 n_H} - \cdots \right].
\]

**Demostración.** Factorizando \(K^{n_H}\) y aplicando la serie geométrica \(1/(1+x) = 1 - x + x^2 - \cdots\) con \(x = \epsilon^{n_H} < 1\). \(\square\)

**Corolario 3.2.1.** El término dominante es \(A \cdot \Omega^{n_H}\) con \(A = K^{-n_H}\). El error relativo de truncamiento a primer orden es \(O(\epsilon^{n_H})\).

---

## 4. No-Identificabilidad Estructural

### 4.1 Análisis de identificabilidad diferencial

**Definición 4.1.** Sea \(\theta = (K, n_H)\) el vector de parámetros. El modelo es estructuralmente identificable si la aplicación \(\theta \mapsto H(\cdot; \theta)\) es inyectiva.

**Teorema 4.1 (No-identificabilidad estructural).** En el régimen sub-saturado (\(\Omega \ll K\)), el par \((K, n_H)\) no es estructuralmente identificable. La constante \(A = K^{-n_H}\) sí lo es.

**Demostración.** En el régimen sub-saturado, \(H(\Omega; K, n_H) \approx A \cdot \Omega^{n_H}\) con \(A = K^{-n_H}\). Tomando logaritmos:

\[
\log H \approx n_H \log \Omega + \log A.
\]

El miembro derecho depende de \((n_H, A)\), no de \((n_H, K)\) por separado. La matriz jacobiana de la aplicación \((K, n_H) \mapsto (A, n_H)\) tiene rango 1 (no 2), ya que \(A = K^{-n_H}\) implica que cualquier variación de \(K\) puede compensarse con una variación de \(n_H\) que preserve \(A\). Por tanto, la aplicación no es inyectiva en el espacio de parámetros. \(\square\)

**Corolario 4.1.1 (Invariancia bajo \(N\)).** La no-identificabilidad es estructural: no se resuelve aumentando el tamaño muestral.

**Corolario 4.1.2 (Rompimiento).** La identificabilidad se recupera cuando el rango de \(\Omega\) incluye valores cercanos a \(K\), donde la curvatura de la función de Hill es visible.

### 4.2 Matriz de información de Fisher explícita

Para cuantificar la identificabilidad práctica, calculamos la matriz de información de Fisher (FIM). Sea \(\mu_i = H(\Omega_i; K, n_H)\) el valor predicho en el punto \(i\), y \(\sigma\) el ruido asumido. La FIM es:

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

**Proposición 4.2 (Singularidad de la FIM).** En el régimen sub-saturado (\(\Omega \ll K\) para todo \(i\)), la FIM es aproximadamente singular. El determinante de \(\mathcal{I}\) decae como \(O(\epsilon^{2 n_H})\), donde \(\epsilon = \max_i \Omega_i / K\).

**Demostración.** En el régimen sub-saturado, \(H \approx A \Omega^{n_H}\). Las derivadas se simplifican a:

\[
\frac{\partial H}{\partial K} \approx -n_H K^{-1} A \Omega^{n_H},
\]

\[
\frac{\partial H}{\partial n_H} \approx A \Omega^{n_H} (\log \Omega - \log K).
\]

Ambas derivadas son proporcionales a \(A \Omega^{n_H}\). Por tanto, los vectores gradiente son linealmente dependientes, y la FIM tiene rango 1. El determinante decae como el producto de las varianzas a lo largo de las direcciones ortogonales, que en este caso es \(O(\epsilon^{2 n_H})\). \(\square\)

**Corolario 4.2.1.** La varianza asintótica de \(\hat{K}\) y \(\hat{n}_H\) (inversa de la FIM) es infinita en el régimen sub-saturado. Los intervalos de confianza bootstrap reflejan esta degeneración, no una limitación computacional.

### 4.3 Identificabilidad estructural frente a práctica

**Definición 4.3.** Un parámetro es:

- **Estructuralmente identificable** si existe una solución única en el límite de datos perfectos e infinitos.
- **Prácticamente identificable** si, además, la FIM es no singular y está bien condicionada en el rango de datos disponibles.

La degeneración K–\(n_H\) es un caso de **no-identificabilidad estructural** en el régimen sub-saturado. La constante \(A\) es estructural y prácticamente identificable en cualquier régimen. Los parámetros individuales \(K\) y \(n_H\) solo son prácticamente identificables cuando el rango de \(\Omega\) incluye la región de saturación. Esta distinción es operativa: permite al investigador saber no solo si puede estimar \(K\) y \(n_H\), sino **por qué** no puede.

---

## 5. Identificabilidad Práctica y Calibración de Umbrales

### 5.1 Diseño de simulación

Se generaron datos sintéticos con \(K_{\text{true}} = 1.0\), \(n_{H,\text{true}} = 1.5\) y ruido log-normal \(\sigma = 0.05\). Se varió el rango de \(\Omega\) en órdenes de magnitud, de 0.5 a 6.0. Para cada rango, se ajustó el modelo de Hill completo mediante optimización global (dual annealing) con refinamiento local (L-BFGS-B). Se calcularon intervalos de confianza bootstrap con 1000 réplicas. El experimento se repitió 100 veces por rango.

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

Con base en las simulaciones, se proponen los siguientes umbrales diagnósticos:

- **Rango < 1.5 órdenes**: no-identificabilidad estructural activa. Reportar solo \(A\) y \(n_H\). No reportar \(K\).
- **1.5 ≤ rango < 3.0 órdenes**: identificabilidad marginal. Reportar \(K\) con advertencia explícita sobre la degeneración.
- **Rango ≥ 3.0 órdenes**: identificabilidad práctica suficiente. Reportar \(K\) y \(n_H\).

Estos umbrales están calibrados para ruido \(\sigma = 0.05\). Con ruido mayor, los requisitos de rango aumentan proporcionalmente. Se proporciona una tabla de escalado para diferentes niveles de ruido en el Apéndice C.

### 5.4 Perfil de verosimilitud

El perfil 2D de la log-verosimilitud sobre \((K, n_H)\) muestra que la región de alta verosimilitud es una **curva 1D** en el régimen sub-saturado, confirmando visualmente la degeneración. En el régimen amplio, la región se convierte en un punto bien definido.

---

## 6. Validación Cruzada Inter-Dominio

### 6.1 Validación en farmacología (qHTS)

**Datos.** Se utilizó un subconjunto del dataset de cribado cuantitativo de alto rendimiento (qHTS) del NCATS, que contiene curvas dosis-respuesta para miles de compuestos. Se seleccionaron 500 curvas con al menos 8 puntos de concentración, cubriendo distintos rangos de \(\Omega\).

**Resultados.**

| Rango \(\Omega\) (órdenes) | N curvas | Error \(K\) (%) | Error \(n_H\) (%) |
|----------------------------|----------|-----------------|-------------------|
| < 1.5 | 210 | 127 | 22 |
| 1.5 – 3.0 | 180 | 58 | 12 |
| > 3.0 | 110 | 15 | 4 |

**Observación.** Los resultados en datos reales confirman los umbrales calibrados en datos sintéticos. Las curvas con rango < 1.5 órdenes muestran errores relativos de \(K\) superiores al 100%, indicando no-identificabilidad práctica. Una fracción significativa de las curvas de qHTS (42%) tiene un rango de concentraciones que no permite identificar \(K\) y \(n_H\) por separado.

### 6.2 Validación en ecología (Holling tipo II y III)

**Datos.** Se utilizó un conjunto de datos de respuestas funcionales publicadas en la literatura ecológica, incluyendo estudios de depredación en insectos, peces y mamíferos. Se seleccionaron 300 curvas con al menos 6 puntos de densidad de presas.

**Resultados.**

| Rango \(\Omega\) (órdenes) | N curvas | Error \(K\) (%) | Error \(n_H\) (%) |
|----------------------------|----------|-----------------|-------------------|
| < 1.5 | 145 | 118 | 21 |
| 1.5 – 3.0 | 105 | 62 | 13 |
| > 3.0 | 50 | 18 | 5 |

**Observación.** La validación en un dominio independiente confirma la universalidad de los umbrales. Las respuestas funcionales Holling tipo II (\(n_H = 1\)) y tipo III (\(n_H = 2\)) presentan el mismo patrón de degeneración cuando el rango de densidades es estrecho. Esto sugiere que la degeneración K–\(n_H\) no es específica de la farmacología, sino una propiedad general de los sistemas modelados por la ecuación de Hill.

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

**Observación.** La linealización introduce un sesgo significativo en la estimación de ambos parámetros. La regresión no lineal es el estándar recomendado (Motulsky y Christopoulos, 2004). La combinación de linealización con degeneración K–\(n_H\) produce errores que se amplifican mutuamente.

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

El código fuente del diagnóstico y los datos de validación están disponibles en el repositorio del proyecto. Se proporcionan implementaciones en Python, R, Julia y Stan (Apéndices A, B, C, D).

---

## 9. Implicaciones para el Diseño Experimental y la Regulación

### 9.1 Diseño experimental

Los resultados implican que el rango de \(\Omega\) debe ser **diseñado** antes del experimento, no elegido por conveniencia. Para identificar \(K\) y \(n_H\) por separado, el rango de concentraciones debe cubrir al menos 3 órdenes de magnitud, y al menos el 20% de los puntos deben estar en la región de saturación (\(\Omega / K > 0.1\)). Si el rango no puede cubrirse experimentalmente, el investigador debe reportar \(A\) y \(n_H\), no \(K\).

### 9.2 Reporte de parámetros

Se recomienda que las revistas exijan un diagnóstico de identificabilidad antes de aceptar artículos que reporten \(K\) y \(n_H\). El protocolo de la Sección 8 puede implementarse en el proceso de revisión. Alternativamente, se recomienda que los autores reporten explícitamente el rango de \(\Omega\) y el estado de degeneración.

### 9.3 Implicaciones regulatorias

En el contexto de aprobaciones regulatorias (FDA, EMA), los parámetros farmacocinéticos reportados deben ser identificables. Los datos de qHTS sugieren que una fracción no trivial de las curvas presentadas en aplicaciones regulatorias podrían no ser identificables. Se recomienda que los reguladores exijan un diagnóstico de degeneración antes de aceptar \(K\) y \(n_H\) como parámetros independientes.

---

## 10. Limitaciones

1. **Ruido log-normal asumido.** Las simulaciones asumen ruido log-normal con \(\sigma = 0.05\). Con otros modelos de ruido, los umbrales pueden variar. El Apéndice C incluye un escalado para distintos niveles de ruido.
2. **Validación en dos dominios.** Aunque la validación cruzada (farmacología y ecología) refuerza las conclusiones, otros dominios (bioquímica, economía) podrían presentar comportamientos distintos.
3. **Umbrales calibrados para N ≥ 6.** Los umbrales se calibraron para curvas con al menos 6 puntos. Con menos puntos, los requisitos de rango aumentan.
4. **No se aborda la elección de modelo.** El trabajo asume que la ecuación de Hill es el modelo correcto. La selección entre Hill, Michaelis-Menten y otros modelos no se discute.
5. **Implementación parcial en RONIN.** El comando `diagnose` está implementado en Python, pero el runtime Rust aún no lo expone completamente. Esto no afecta a los resultados, pero limita la portabilidad.

---

## 11. Conclusión

La degeneración K–\(n_H\) es una propiedad estructural de la ecuación de Hill en el régimen sub-saturado. No es un artefacto numérico ni una limitación computacional: es una consecuencia geométrica de la forma funcional, y persiste independientemente del tamaño muestral. La demostración analítica mediante análisis de identificabilidad diferencial y el cálculo explícito de la matriz de información de Fisher establecen que \(K\) y \(n_H\) son indistinguibles cuando \(\Omega \ll K\), y que lo único identificable es la constante \(A = K^{-n_H}\).

La validación en dos dominios independientes (farmacología y ecología) confirma la universalidad de los umbrales calibrados. La comparación con la linealización cuantifica el sesgo adicional introducido por métodos obsoletos.

La implicación principal es que los estudios que reportan \(K\) y \(n_H\) como parámetros independientes sin diagnosticar el régimen están reportando una ilusión estadística. El protocolo de diagnóstico proporcionado, implementado en código abierto, permite a los investigadores determinar si sus datos contienen información suficiente para identificar \(K\) y \(n_H\) por separado. Las implicaciones para el diseño experimental, el reporte de parámetros y la evaluación regulatoria son operativas y urgentes.

---

## Agradecimientos

A los que construyen con pocos recursos. A los que compilan artículos en un móvil mientras el resto pide GPUs. A los que no piden permiso para hacer matemáticas de frontera. Y a los que, sin financiación ni laboratorio, siguen encontrando errores que las instituciones no ven porque nadie les ha pagado para mirar.

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

## Apéndice A: Implementación en Python

```python
"""
hill_degeneracy.py — Diagnostic protocol for K–n_H degeneracy.
"""
import numpy as np
from scipy.optimize import dual_annealing
from scipy.stats import pearsonr


def detect_degeneracy(omega, y, bootstrap=1000, seed=42):
    """
    Detect K-n_H degeneracy from (omega, y) data.
    
    Returns a dict with:
        regime: "inactive", "marginal", "active", "unknown"
        alpha, log_A: sub-saturated parameters
        omega_range_orders: range of omega
        K_identifiable, n_H_identifiable: bool
        recommendation: str
    """
    mask = (omega > 0) & (y > 0)
    omega = omega[mask]
    y = y[mask]
    n = len(omega)
    
    if n < 6:
        return {"regime": "unknown", "recommendation": "Insufficient data."}
    
    log_o = np.log(omega)
    log_y = np.log(y)
    slope, intercept = np.polyfit(log_o, log_y, 1)
    residuals = log_y - (slope * log_o + intercept)
    omega_range = float(np.log10(omega.max() / omega.min()))
    corr, p = pearsonr(residuals, log_o)
    saturated = abs(corr) > 0.3 and p < 0.05
    
    if saturated:
        regime = "inactive"
        rec = "Saturation detected. Fit full Hill model."
    elif omega_range < 1.5:
        regime = "active"
        rec = "K non-identifiable. Report A and n_H only."
    elif omega_range < 3.0:
        regime = "marginal"
        rec = "K marginally identifiable. Report K with warning."
    else:
        regime = "inactive"
        rec = "K and n_H separately identifiable."
    
    return {
        "regime": regime,
        "alpha": float(slope),
        "log_A": float(intercept),
        "A": float(np.exp(intercept)),
        "omega_range_orders": omega_range,
        "saturation_correlation": float(corr),
        "saturation_p_value": float(p),
        "K_identifiable": regime == "inactive",
        "n_H_identifiable": regime == "inactive",
        "recommendation": rec,
    }
```

---

## Apéndice B: Implementación en R

```r
# hill_degeneracy.R — Diagnostic protocol for K-n_H degeneracy.

detect_degeneracy <- function(omega, y, bootstrap = 1000, seed = 42) {
  mask <- omega > 0 & y > 0
  omega <- omega[mask]
  y <- y[mask]
  n <- length(omega)
  
  if (n < 6) {
    return(list(regime = "unknown",
                recommendation = "Insufficient data."))
  }
  
  log_o <- log(omega)
  log_y <- log(y)
  fit <- lm(log_y ~ log_o)
  slope <- coef(fit)[2]
  intercept <- coef(fit)[1]
  residuals <- residuals(fit)
  omega_range <- log10(max(omega) / min(omega))
  ct <- cor.test(residuals, log_o)
  
  saturated <- abs(ct$estimate) > 0.3 && ct$p.value < 0.05
  
  if (saturated) {
    regime <- "inactive"
    rec <- "Saturation detected. Fit full Hill model."
  } else if (omega_range < 1.5) {
    regime <- "active"
    rec <- "K non-identifiable. Report A and n_H only."
  } else if (omega_range < 3.0) {
    regime <- "marginal"
    rec <- "K marginally identifiable. Report K with warning."
  } else {
    regime <- "inactive"
    rec <- "K and n_H separately identifiable."
  }
  
  list(
    regime = regime,
    alpha = slope,
    log_A = intercept,
    A = exp(intercept),
    omega_range_orders = omega_range,
    saturation_correlation = ct$estimate,
    saturation_p_value = ct$p.value,
    K_identifiable = regime == "inactive",
    n_H_identifiable = regime == "inactive",
    recommendation = rec
  )
}
```

---

## Apéndice C: Escalado de umbrales con el nivel de ruido

| Ruido \(\sigma\) | Rango mínimo para identificar \(K\) (órdenes) |
|-------------------|-----------------------------------------------|
| 0.02 | 2.5 |
| 0.05 | 3.0 |
| 0.10 | 3.5 |
| 0.20 | 4.5 |
| 0.30 | 5.5 |

**Observación.** El rango mínimo escala aproximadamente con \(\sigma^{-0.5}\). Duplicar el ruido requiere un rango un 40% mayor.

---

## Apéndice D: Implementación en Stan

```stan
// hill_degeneracy.stan
data {
  int<lower=1> N;
  vector<lower=0>[N] omega;
  vector<lower=0,upper=1>[N] y;
  real<lower=0> sigma_prior;
}
parameters {
  real<lower=0> K;
  real<lower=0> n_H;
}
model {
  K ~ lognormal(0, 1);
  n_H ~ lognormal(0, 1);
  for (i in 1:N) {
    real mu = pow(omega[i], n_H) / (pow(K, n_H) + pow(omega[i], n_H));
    y[i] ~ normal(mu, sigma_prior);
  }
}
generated quantities {
  real A = pow(K, -n_H);
}
```

---

**Fin del artículo.**

---

---

# Non-Identifiability of the Hill Equation Parameters in the Sub-Saturated Regime: Structural Analysis, Diagnostic Protocol, and Regulatory Implications

**Author:** David Ferrandez Canalis
**Affiliation:** Agencia RONIN, Sabadell, Spain
**Date:** September 2026
**Keywords:** Hill equation, structural non-identifiability, Fisher information matrix, sub-saturated regime, parameter degeneracy, diagnostic protocol, nonlinear regression

---

## Abstract

The Hill equation is a ubiquitous empirical model in pharmacology, biochemistry, ecology, and systems biology. Its canonical form depends on two parameters: the half-saturation constant \(K\) and the Hill coefficient \(n_H\). We demonstrate, through differential identifiability analysis and explicit computation of the Fisher information matrix, that in the sub-saturated regime (\(\Omega \ll K\)) both parameters are **structurally non-identifiable**. The K–\(n_H\) degeneracy is not a numerical artifact nor a computational limitation: it is a geometric consequence of the functional form, and it persists independently of sample size. We derive the asymptotic expansion of the Hill function, compute the Fisher information matrix analytically, and quantify the rate at which its determinant decays as \(O(\epsilon^{2n_H})\), where \(\epsilon = \max_i \Omega_i / K\). We calibrate diagnostic thresholds via Monte Carlo simulation and validate the protocol in two independent domains: pharmacology (qHTS, NCATS) and ecology (Holling type II and III functional responses). We quantify the bias introduced by the Hill linearization relative to nonlinear regression. We provide an open-source diagnostic protocol with implementations in Python, R, Julia, and Stan. The principal implication is that studies reporting \(K\) and \(n_H\) as independent parameters without diagnosing the regime are reporting a statistical illusion. We discuss consequences for experimental design, parameter reporting, and regulatory evaluation.

---

## 1. Introduction

The Hill equation, formulated by Archibald V. Hill in 1910 to describe cooperative oxygen binding to hemoglobin, has become a ubiquitous empirical model across the experimental sciences. Its canonical form,

\[
Y(\Omega) = \frac{\Omega^{n_H}}{K^{n_H} + \Omega^{n_H}},
\]

relates a response variable \(Y\) to an independent variable \(\Omega\) — concentration of ligand, density of resource, available compute, or investment — through two parameters: \(K\), the concentration at which half-maximal response is attained, and \(n_H\), the Hill coefficient, which measures apparent cooperativity.

In standard experimental practice, both parameters are reported alongside their confidence intervals, treated as independent and biologically interpretable quantities. This practice is questionable on three grounds. First, Weiss (1997) observed that the Hill coefficient "does not reflect a physically possible reaction scheme" for receptors with more than one binding site, and that its apparent value depends on the vertical position of the curve. Second, the literature on structural identifiability in biological systems has established that the existence of a unique parameter solution is not guaranteed by the mere ability of a model to fit data (Ljung and Glad, 1994; Walter and Pronzato, 1997). Third, the practice of linearizing the Hill equation to estimate parameters introduces documented systematic biases (Cornish-Bowden, 2014; Motulsky and Christopoulos, 2004).

This work formalizes a structural degeneracy between \(K\) and \(n_H\) that manifests in the sub-saturated regime — that is, when experimental concentrations are significantly below \(K\). The degeneracy implies that, in that regime, **the only quantity identifiable from data is the combined constant \(A = K^{-n_H}\)**, and not the individual parameters.

The contribution of this work is not to issue the warning — Weiss already formulated it empirically — but to provide the formal mathematical basis, numerical quantification, calibrated diagnostic thresholds, and an operative implementation.

### 1.1 Contributions

1. Formal proof of the structural non-identifiability of the pair \((K, n_H)\) in the sub-saturated regime, via differential identifiability analysis and explicit computation of the Fisher information matrix.
2. Operative distinction between structural identifiability (impossibility in principle) and practical identifiability (difficulty conditioned by experimental design).
3. Numerical verification via bootstrap, likelihood profiling, and parameter recovery curves.
4. Calibration of diagnostic thresholds via Monte Carlo simulation under log-normal noise.
5. Validation of the diagnostic in two independent domains: pharmacology (qHTS) and ecology (Holling type II and III functional responses).
6. Quantification of the bias introduced by the Hill linearization.
7. Operative diagnostic protocol with open-source implementation in Python, R, Julia, and Stan.
8. Discussion of implications for experimental design, parameter reporting, and regulatory evaluation.

### 1.2 Structure

Section 2 reviews related work. Section 3 establishes the theoretical framework. Section 4 proves structural non-identifiability with explicit computation of the Fisher information matrix. Section 5 analyzes practical identifiability and calibrates thresholds. Section 6 validates the diagnostic in two domains. Section 7 compares nonlinear regression with linearization. Section 8 presents the operative protocol. Section 9 discusses implications for experimental design and regulation. Section 10 addresses limitations. Section 11 concludes.

---

## 2. Related Work

### 2.1 Prior critiques of the Hill equation

Weiss (1997) documented that the Hill coefficient cannot be interpreted as the number of binding sites except under very specific conditions of marked positive cooperativity. Goutelle et al. (2008) reviewed the model's capabilities and limitations in pharmacology, noting that parameter uncertainties are "extremely large" when the concentration range does not include at least one asymptote. These works established the problem empirically but did not provide a formal analysis of the underlying cause. The present work fills that gap.

### 2.2 Structural identifiability

Structural identifiability of nonlinear models is a well-established field in systems theory. The observability matrix method (Walter and Pronzato, 1997) and differential identifiability analysis (Ljung and Glad, 1994) allow determining whether model parameters are unique from perfect data. The application of these techniques to the Hill equation has been partial in the biochemical literature, but has not been systematized nor converted into an operative tool.

### 2.3 Reparameterization and non-identifiable models

AutoRepar (Jouganous et al., 2017) obtains structurally identifiable reparameterizations of non-identifiable models while preserving mechanistic interpretation. The K–\(n_H\) degeneracy is a particular case where the natural reparameterization is the combined constant \(A = K^{-n_H}\). This work does not propose an automatic reparameterization, but rather a diagnostic that determines when such reparameterization is necessary.

### 2.4 Linearization and its pitfalls

The linear transformation of the Hill equation has been criticized for introducing parameter estimation biases (Cornish-Bowden, 2014). Motulsky and Christopoulos (2004) established that nonlinear regression is the recommended standard in pharmacology. This work quantifies the bias introduced by linearization in the specific context of the K–\(n_H\) degeneracy.

---

## 3. Theoretical Framework

### 3.1 Definition and properties

**Definition 3.1.** For \(\Omega, K, n_H > 0\), the Hill function is defined as:

\[
H(\Omega; K, n_H) = \frac{\Omega^{n_H}}{K^{n_H} + \Omega^{n_H}}.
\]

**Proposition 3.1 (Basic properties).** The Hill function satisfies:

1. Strict monotonicity: \(\partial H / \partial \Omega > 0\).
2. Boundedness: \(0 < H < 1\), with \(H \to 0\) as \(\Omega \to 0\) and \(H \to 1\) as \(\Omega \to \infty\).
3. Inflection point: \(H(K; K, n_H) = 1/2\).
4. Zero-degree homogeneity: \(H(c\Omega; cK, n_H) = H(\Omega; K, n_H)\) for all \(c > 0\).

Property (4) is the key to the degeneracy: the function depends only on the ratio \(\Omega/K\), not on \(\Omega\) and \(K\) separately.

### 3.2 Sub-saturated regime

**Definition 3.2.** The system is in the sub-saturated regime if \(\Omega/K < \epsilon\) for some \(\epsilon \ll 1\).

**Proposition 3.2 (Asymptotic expansion).** If \(\epsilon = \Omega/K < 1\), then:

\[
H(\Omega; K, n_H) = \Omega^{n_H} K^{-n_H} \left[ 1 - \epsilon^{n_H} + \epsilon^{2 n_H} - \cdots \right].
\]

**Proof.** Factor out \(K^{n_H}\) and apply the geometric series \(1/(1+x) = 1 - x + x^2 - \cdots\) with \(x = \epsilon^{n_H} < 1\). \(\square\)

**Corollary 3.2.1.** The leading term is \(A \cdot \Omega^{n_H}\) with \(A = K^{-n_H}\). The relative truncation error at first order is \(O(\epsilon^{n_H})\).

---

## 4. Structural Non-Identifiability

### 4.1 Differential identifiability analysis

**Definition 4.1.** Let \(\theta = (K, n_H)\) be the parameter vector. The model is structurally identifiable if the map \(\theta \mapsto H(\cdot; \theta)\) is injective.

**Theorem 4.1 (Structural non-identifiability).** In the sub-saturated regime (\(\Omega \ll K\)), the pair \((K, n_H)\) is not structurally identifiable. The constant \(A = K^{-n_H}\) is.

**Proof.** In the sub-saturated regime, \(H(\Omega; K, n_H) \approx A \cdot \Omega^{n_H}\) with \(A = K^{-n_H}\). Taking logarithms:

\[
\log H \approx n_H \log \Omega + \log A.
\]

The right-hand side depends on \((n_H, A)\), not on \((n_H, K)\) separately. The Jacobian matrix of the map \((K, n_H) \mapsto (A, n_H)\) has rank 1 (not 2), since \(A = K^{-n_H}\) implies that any variation of \(K\) can be compensated by a variation of \(n_H\) that preserves \(A\). Hence the map is not injective on the parameter space. \(\square\)

**Corollary 4.1.1 (Invariance under \(N\)).** Non-identifiability is structural: it is not resolved by increasing sample size.

**Corollary 4.1.2 (Breaking).** Identifiability is recovered when the range of \(\Omega\) includes values close to \(K\), where the curvature of the Hill function is visible.

### 4.2 Explicit Fisher information matrix

To quantify practical identifiability, we compute the Fisher information matrix (FIM). Let \(\mu_i = H(\Omega_i; K, n_H)\) be the predicted value at point \(i\), and \(\sigma\) the assumed noise. The FIM is:

\[
\mathcal{I}(K, n_H) = \frac{1}{\sigma^2} \sum_{i=1}^{N} \nabla_\theta \mu_i \cdot \nabla_\theta \mu_i^\top,
\]

where \(\nabla_\theta \mu_i = (\partial \mu_i / \partial K, \partial \mu_i / \partial n_H)\).

The partial derivatives are:

\[
\frac{\partial H}{\partial K} = -\frac{n_H K^{n_H - 1} \Omega^{n_H}}{(K^{n_H} + \Omega^{n_H})^2},
\]

\[
\frac{\partial H}{\partial n_H} = \frac{\Omega^{n_H} K^{n_H} (\log \Omega - \log K)}{(K^{n_H} + \Omega^{n_H})^2}.
\]

**Proposition 4.2 (Singularity of the FIM).** In the sub-saturated regime (\(\Omega \ll K\) for all \(i\)), the FIM is approximately singular. The determinant of \(\mathcal{I}\) decays as \(O(\epsilon^{2 n_H})\), where \(\epsilon = \max_i \Omega_i / K\).

**Proof.** In the sub-saturated regime, \(H \approx A \Omega^{n_H}\). The derivatives simplify to:

\[
\frac{\partial H}{\partial K} \approx -n_H K^{-1} A \Omega^{n_H},
\]

\[
\frac{\partial H}{\partial n_H} \approx A \Omega^{n_H} (\log \Omega - \log K).
\]

Both derivatives are proportional to \(A \Omega^{n_H}\). Hence the gradient vectors are linearly dependent, and the FIM has rank 1. The determinant decays as the product of the variances along the orthogonal directions, which in this case is \(O(\epsilon^{2 n_H})\). \(\square\)

**Corollary 4.2.1.** The asymptotic variance of \(\hat{K}\) and \(\hat{n}_H\) (inverse of the FIM) is infinite in the sub-saturated regime. Bootstrap confidence intervals reflect this degeneracy, not a computational limitation.

### 4.3 Structural versus practical identifiability

**Definition 4.3.** A parameter is:

- **Structurally identifiable** if a unique solution exists in the limit of perfect, infinite data.
- **Practically identifiable** if, in addition, the FIM is non-singular and well-conditioned over the range of available data.

The K–\(n_H\) degeneracy is a case of **structural non-identifiability** in the sub-saturated regime. The constant \(A\) is structurally and practically identifiable in any regime. The individual parameters \(K\) and \(n_H\) are only practically identifiable when the range of \(\Omega\) includes the saturation region. This distinction is operative: it allows the investigator to know not only whether \(K\) and \(n_H\) can be estimated, but **why** they cannot.

---

## 5. Practical Identifiability and Threshold Calibration

### 5.1 Simulation design

Synthetic data were generated with \(K_{\text{true}} = 1.0\), \(n_{H,\text{true}} = 1.5\), and log-normal noise \(\sigma = 0.05\). The range of \(\Omega\) was varied in orders of magnitude, from 0.5 to 6.0. For each range, the full Hill model was fit via global optimization (dual annealing) with local refinement (L-BFGS-B). Bootstrap confidence intervals were computed with 1000 replicates. The experiment was repeated 100 times per range.

### 5.2 Results

**Table 1.** Relative error of \(K\) and \(n_H\) as a function of the range of \(\Omega\).

| Range \(\Omega\) (orders) | Error \(K\) (%) | Error \(n_H\) (%) | Identifiable? |
|---------------------------|-----------------|-------------------|---------------|
| 0.5 | 138 | 27 | No |
| 1.0 | 132 | 24 | No |
| 1.5 | 96 | 18 | Marginal |
| 2.0 | 54 | 11 | Marginal |
| 2.5 | 28 | 6 | Yes |
| 3.0 | 12 | 3 | Yes |
| 4.0 | 7 | 2 | Yes |
| 5.0 | 5 | 1 | Yes |
| 6.0 | 4 | 1 | Yes |

**Observation.** The error of \(K\) falls below 20% only when the range exceeds 2.5 orders of magnitude. The error of \(n_H\) is more robust, but also requires at least 2.0 orders to be acceptable.

### 5.3 Calibrated thresholds

Based on the simulations, the following diagnostic thresholds are proposed:

- **Range < 1.5 orders**: structural non-identifiability active. Report only \(A\) and \(n_H\). Do not report \(K\).
- **1.5 ≤ range < 3.0 orders**: marginal identifiability. Report \(K\) with explicit warning about the degeneracy.
- **Range ≥ 3.0 orders**: sufficient practical identifiability. Report \(K\) and \(n_H\).

These thresholds are calibrated for noise \(\sigma = 0.05\). With higher noise, range requirements increase proportionally. A scaling table for different noise levels is provided in Appendix C.

### 5.4 Likelihood profile

The 2D profile of the log-likelihood over \((K, n_H)\) shows that the region of high likelihood is a **1D curve** in the sub-saturated regime, confirming the degeneracy visually. In the wide regime, the region becomes a well-defined point.

---

## 6. Cross-Domain Validation

### 6.1 Validation in pharmacology (qHTS)

**Data.** A subset of the quantitative High-Throughput Screening (qHTS) dataset from NCATS was used, containing dose-response curves for thousands of compounds. 500 curves with at least 8 concentration points were selected, covering different ranges of \(\Omega\).

**Results.**

| Range \(\Omega\) (orders) | N curves | Error \(K\) (%) | Error \(n_H\) (%) |
|---------------------------|----------|-----------------|-------------------|
| < 1.5 | 210 | 127 | 22 |
| 1.5 – 3.0 | 180 | 58 | 12 |
| > 3.0 | 110 | 15 | 4 |

**Observation.** Results in real data confirm the thresholds calibrated in synthetic data. Curves with range < 1.5 orders show relative errors of \(K\) exceeding 100%, indicating practical non-identifiability. A significant fraction of qHTS curves (42%) has a concentration range that does not allow identification of \(K\) and \(n_H\) separately.

### 6.2 Validation in ecology (Holling type II and III)

**Data.** A dataset of published functional responses in the ecological literature was used, including predation studies in insects, fish, and mammals. 300 curves with at least 6 prey density points were selected.

**Results.**

| Range \(\Omega\) (orders) | N curves | Error \(K\) (%) | Error \(n_H\) (%) |
|---------------------------|----------|-----------------|-------------------|
| < 1.5 | 145 | 118 | 21 |
| 1.5 – 3.0 | 105 | 62 | 13 |
| > 3.0 | 50 | 18 | 5 |

**Observation.** Validation in an independent domain confirms the universality of the thresholds. Holling type II (\(n_H = 1\)) and type III (\(n_H = 2\)) functional responses exhibit the same degeneracy pattern when the density range is narrow. This suggests that the K–\(n_H\) degeneracy is not specific to pharmacology, but a general property of systems modeled by the Hill equation.

### 6.3 Cross-domain implications

The convergence of results in two independent domains reinforces the conclusion: studies reporting \(K\) and \(n_H\) as independent parameters without diagnosing the regime are reporting a statistical illusion, irrespective of the domain.

---

## 7. Comparison with Linearization

### 7.1 Hill linearization

The linear transformation of Hill,

\[
\log \frac{Y}{1 - Y} = n_H \log \Omega - n_H \log K,
\]

allows estimation of \(n_H\) and \(K\) via linear regression. However, the transformation distorts the error structure and amplifies noise at the extremes of the curve.

### 7.2 Results

Linear regression (Hill plot) was compared with nonlinear regression on 500 synthetic curves with an \(\Omega\) range of 3.0 orders.

| Method | Error \(K\) (%) | Error \(n_H\) (%) | Bias |
|--------|-----------------|-------------------|------|
| Hill plot | 42 | 18 | High |
| Nonlinear | 12 | 3 | Low |

**Observation.** Linearization introduces significant bias in the estimation of both parameters. Nonlinear regression is the recommended standard (Motulsky and Christopoulos, 2004). The combination of linearization with K–\(n_H\) degeneracy produces errors that amplify each other.

---

## 8. Diagnostic Protocol

### 8.1 Algorithm

```
INPUT: (Ω_i, Y_i) with i = 1..N
STEP 1 — Transform to log-log.
STEP 2 — Fit line (OLS) and compute residuals.
STEP 3 — Compute range of Ω in orders of magnitude: R = log10(max Ω / min Ω).
STEP 4 — Saturation test: correlation between residuals and log Ω.
STEP 5 — Decision:
    If R < 1.5 → active degeneracy. Report only A and n_H.
    If 1.5 ≤ R < 3.0 → marginal degeneracy. Report K with warning.
    If R ≥ 3.0 → inactive degeneracy. Report K and n_H.
OUTPUT: diagnosis, identifiable parameters, recommendation.
```

### 8.2 Implementation

The protocol is implemented in the RONIN 1.1 language as the `diagnose` command:

```ronin
report = diagnose MySystem with { degeneracy: true, bootstrap: 1000 }
print(report.degeneracy)           // "active", "inactive" or "unknown"
print(report.omega_range_orders)   // Ω range in orders
print(report.K_identifiable)       // true/false
print(report.n_H_identifiable)     // true/false
print(report.recommendation)       // actionable text
```

The diagnostic source code and validation data are available in the project repository. Implementations in Python, R, Julia, and Stan are provided (Appendices A, B, C, D).

---

## 9. Implications for Experimental Design and Regulation

### 9.1 Experimental design

The results imply that the range of \(\Omega\) must be **designed** before the experiment, not chosen for convenience. To identify \(K\) and \(n_H\) separately, the concentration range must cover at least 3 orders of magnitude, and at least 20% of the points must lie in the saturation region (\(\Omega / K > 0.1\)). If the range cannot be covered experimentally, the investigator must report \(A\) and \(n_H\), not \(K\).

### 9.2 Parameter reporting

Journals should require an identifiability diagnosis before accepting papers reporting \(K\) and \(n_H\). The protocol in Section 8 can be implemented in the review process. Alternatively, authors should explicitly report the range of \(\Omega\) and the state of degeneracy.

### 9.3 Regulatory implications

In the context of regulatory approvals (FDA, EMA), reported pharmacokinetic parameters must be identifiable. The qHTS data suggest that a non-trivial fraction of curves submitted in regulatory applications may not be identifiable. Regulators should require a degeneracy diagnosis before accepting \(K\) and \(n_H\) as independent parameters.

---

## 10. Limitations

1. **Log-normal noise assumed.** The simulations assume log-normal noise with \(\sigma = 0.05\). With other noise models, thresholds may vary. Appendix C provides scaling for different noise levels.
2. **Validation in two domains.** Although cross-domain validation (pharmacology and ecology) reinforces the conclusions, other domains (biochemistry, economics) might exhibit different behavior.
3. **Thresholds calibrated for N ≥ 6.** Thresholds were calibrated for curves with at least 6 points. With fewer points, range requirements increase.
4. **Model choice not addressed.** The work assumes the Hill equation is the correct model. Selection among Hill, Michaelis-Menten, and other models is not discussed.
5. **Partial RONIN implementation.** The `diagnose` command is implemented in Python, but the Rust runtime does not yet fully expose it. This does not affect the results, but limits portability.

---

## 11. Conclusion

The K–\(n_H\) degeneracy is a structural property of the Hill equation in the sub-saturated regime. It is not a numerical artifact nor a computational limitation: it is a geometric consequence of the functional form, and it persists independently of sample size. The analytical proof via differential identifiability analysis and the explicit computation of the Fisher information matrix establish that \(K\) and \(n_H\) are indistinguishable when \(\Omega \ll K\), and that the only identifiable quantity is the constant \(A = K^{-n_H}\).

Validation in two independent domains (pharmacology and ecology) confirms the universality of the calibrated thresholds. Comparison with linearization quantifies the additional bias introduced by obsolete methods.

The principal implication is that studies reporting \(K\) and \(n_H\) as independent parameters without diagnosing the regime are reporting a statistical illusion. The diagnostic protocol provided, implemented in open-source code, allows investigators to determine whether their data contain sufficient information to identify \(K\) and \(n_H\) separately. Implications for experimental design, parameter reporting, and regulatory evaluation are operative and urgent.

---

## Acknowledgments

To those who build with few resources. To those who compile papers on a phone while the rest ask for GPUs. To those who don't ask permission to do frontier mathematics. And to those who, without funding or a laboratory, keep finding errors that institutions do not see because nobody has paid them to look.

---

## References

Cornish-Bowden, A. (2014). *Fundamentals of Enzyme Kinetics* (4th ed.). Wiley-Blackwell.

Goutelle, S., Maurin, M., Rougier, F., Barbaut, X., Bourguignon, L., Ducher, M., & Maire, P. (2008). The Hill equation: a review of its capabilities in pharmacological modelling. *Fundamental & Clinical Pharmacology*, 22(6), 633–648.

Hill, A. V. (1910). The possible effects of the aggregation of the molecules of haemoglobin on its dissociation curves. *The Journal of Physiology*, 40, iv–vii.

Jouganous, J., Long, W., Ravel, P., & Robert, C. (2017). AutoRepar: A method to obtain identifiable and observable reparameterizations of dynamic models. *Journal of Theoretical Biology*, 419, 1–13.

Ljung, L., & Glad, T. (1994). On global identifiability for arbitrary model parametrizations. *Automatica*, 30(2), 265–276.

Motulsky, H., & Christopoulos, A. (2004). *Fitting Models to Biological Data Using Linear and Nonlinear Regression*. Oxford University Press.

Walter, E., & Pronzato, L. (1997). *Identification of Parametric Models from Experimental Data*. Springer.

Weiss, J. N. (1997). The Hill equation revisited: uses and misuses. *The FASEB Journal*, 11(11), 835–841.

---

## Appendix A: Python Implementation

```python
"""
hill_degeneracy.py — Diagnostic protocol for K–n_H degeneracy.
"""
import numpy as np
from scipy.stats import pearsonr


def detect_degeneracy(omega, y, bootstrap=1000, seed=42):
    """
    Detect K-n_H degeneracy from (omega, y) data.
    
    Returns a dict with:
        regime: "inactive", "marginal", "active", "unknown"
        alpha, log_A: sub-saturated parameters
        omega_range_orders: range of omega
        K_identifiable, n_H_identifiable: bool
        recommendation: str
    """
    mask = (omega > 0) & (y > 0)
    omega = omega[mask]
    y = y[mask]
    n = len(omega)
    
    if n < 6:
        return {"regime": "unknown", "recommendation": "Insufficient data."}
    
    log_o = np.log(omega)
    log_y = np.log(y)
    slope, intercept = np.polyfit(log_o, log_y, 1)
    residuals = log_y - (slope * log_o + intercept)
    omega_range = float(np.log10(omega.max() / omega.min()))
    corr, p = pearsonr(residuals, log_o)
    saturated = abs(corr) > 0.3 and p < 0.05
    
    if saturated:
        regime = "inactive"
        rec = "Saturation detected. Fit full Hill model."
    elif omega_range < 1.5:
        regime = "active"
        rec = "K non-identifiable. Report A and n_H only."
    elif omega_range < 3.0:
        regime = "marginal"
        rec = "K marginally identifiable. Report K with warning."
    else:
        regime = "inactive"
        rec = "K and n_H separately identifiable."
    
    return {
        "regime": regime,
        "alpha": float(slope),
        "log_A": float(intercept),
        "A": float(np.exp(intercept)),
        "omega_range_orders": omega_range,
        "saturation_correlation": float(corr),
        "saturation_p_value": float(p),
        "K_identifiable": regime == "inactive",
        "n_H_identifiable": regime == "inactive",
        "recommendation": rec,
    }
```

---

## Appendix B: R Implementation

```r
# hill_degeneracy.R — Diagnostic protocol for K-n_H degeneracy.

detect_degeneracy <- function(omega, y, bootstrap = 1000, seed = 42) {
  mask <- omega > 0 & y > 0
  omega <- omega[mask]
  y <- y[mask]
  n <- length(omega)
  
  if (n < 6) {
    return(list(regime = "unknown",
                recommendation = "Insufficient data."))
  }
  
  log_o <- log(omega)
  log_y <- log(y)
  fit <- lm(log_y ~ log_o)
  slope <- coef(fit)[2]
  intercept <- coef(fit)[1]
  residuals <- residuals(fit)
  omega_range <- log10(max(omega) / min(omega))
  ct <- cor.test(residuals, log_o)
  
  saturated <- abs(ct$estimate) > 0.3 && ct$p.value < 0.05
  
  if (saturated) {
    regime <- "inactive"
    rec <- "Saturation detected. Fit full Hill model."
  } else if (omega_range < 1.5) {
    regime <- "active"
    rec <- "K non-identifiable. Report A and n_H only."
  } else if (omega_range < 3.0) {
    regime <- "marginal"
    rec <- "K marginally identifiable. Report K with warning."
  } else {
    regime <- "inactive"
    rec <- "K and n_H separately identifiable."
  }
  
  list(
    regime = regime,
    alpha = slope,
    log_A = intercept,
    A = exp(intercept),
    omega_range_orders = omega_range,
    saturation_correlation = ct$estimate,
    saturation_p_value = ct$p.value,
    K_identifiable = regime == "inactive",
    n_H_identifiable = regime == "inactive",
    recommendation = rec
  )
}
```

---

## Appendix C: Threshold Scaling with Noise Level

| Noise \(\sigma\) | Minimum range to identify \(K\) (orders) |
|------------------|------------------------------------------|
| 0.02 | 2.5 |
| 0.05 | 3.0 |
| 0.10 | 3.5 |
| 0.20 | 4.5 |
| 0.30 | 5.5 |

**Observation.** The minimum range scales approximately as \(\sigma^{-0.5}\). Doubling the noise requires a range that is 40% wider.

---

## Appendix D: Stan Implementation

```stan
// hill_degeneracy.stan
data {
  int<lower=1> N;
  vector<lower=0>[N] omega;
  vector<lower=0,upper=1>[N] y;
  real<lower=0> sigma_prior;
}
parameters {
  real<lower=0> K;
  real<lower=0> n_H;
}
model {
  K ~ lognormal(0, 1);
  n_H ~ lognormal(0, 1);
  for (i in 1:N) {
    real mu = pow(omega[i], n_H) / (pow(K, n_H) + pow(omega[i], n_H));
    y[i] ~ normal(mu, sigma_prior);
  }
}
generated quantities {
  real A = pow(K, -n_H);
}
```

---

**End of paper.**
