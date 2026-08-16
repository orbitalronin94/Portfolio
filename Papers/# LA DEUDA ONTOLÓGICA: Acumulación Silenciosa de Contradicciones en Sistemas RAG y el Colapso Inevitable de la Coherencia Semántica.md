# LA DEUDA ONTOLÓGICA: Acumulación Silenciosa de Contradicciones en Sistemas RAG y el Colapso Inevitable de la Coherencia Semántica

**Versión:** 1.0 (Edición Fundacional — Máxima Densidad)

**Autor:** David Ferrandez Canalis — Agencia RONIN (autor principal y correspondencia)

**DOI Simbólico:** 10.1310/ronin-ontological-debt-2026

**Fecha de publicación:** 10 de agosto de 2026

**Licencia:** CC BY-NC-SA 4.0 + Cláusula Comercial Ronin

**Palabras clave:** deuda ontológica, RAG poisoning endógeno, contradicción semántica latente, grafo de inconsistencias, presión ontológica, similitud coseno, base vectorial, coherencia distribucional, entropía de contradicción, auditoría semántica, cuarentena documental, efecto iceberg en RAG, retrieval-augmented generation, embedding space topology, logical consistency verification, knowledge base integrity, semantic drift, cross-document contradiction detection, ontological quarantine

---

## Abstract

Los sistemas RAG (Retrieval-Augmented Generation) en producción sufren una patología que ningún paper de seguridad ha formalizado con la precisión que merece, que ningún framework de MLOps monitoriza de manera nativa, y que ningún equipo de ingeniería detecta hasta que el sistema emite una respuesta que contradice flagrantemente otra respuesta que emitió tres semanas atrás: la acumulación endógena de contradicciones semánticas en la base vectorial.

Esta patología —que denominamos **deuda ontológica** por analogía estructural con la deuda técnica de Cunningham (1992), pero operando sobre la capa de significado en lugar de la capa de código— no es un ataque externo. No requiere un adversario. No requiere acceso malicioso al pipeline de ingesta. Es una consecuencia inevitable del funcionamiento normal de cualquier sistema RAG que indexa documentos de múltiples fuentes, en múltiples momentos temporales, sin un mecanismo de verificación de consistencia lógica cruzada.

El argumento central de este paper es el siguiente: la similitud coseno —el criterio universal de recuperación en bases vectoriales— es una métrica de **relevancia temática**, no de **consistencia lógica**. Un documento que afirma "la política de retención de datos es de 90 días" y un documento que afirma "la política de retención de datos es de 30 días" pueden tener una similitud coseno de 0.94 con la misma consulta, porque ambos tratan sobre retención de datos. El sistema RAG recuperará ambos, los inyectará en el contexto del LLM, y el LLM producirá una respuesta que —dependiendo del peso atencional que asigne a cada documento— será una cosa u otra, sin mecanismo interno para detectar que los dos documentos se contradicen.

Esta contradicción no produce un error. No produce una excepción. No produce una alerta. Produce una respuesta plausible que es simultáneamente correcta e incorrecta dependiendo de qué documento se recupere en la próxima consulta. El sistema no falla; simplemente deja de ser coherente consigo mismo de maneras que son invisibles en cualquier evaluación puntual pero devastadoras en cualquier evaluación longitudinal.

Formalizamos la deuda ontológica mediante: (1) un modelo de **grafo de contradicciones** donde los documentos son nodos y las inconsistencias lógicas son aristas ponderadas por severidad; (2) una **métrica de presión ontológica** que cuantifica la densidad de contradicciones activas en la vecindad semántica de cualquier consulta; (3) el **efecto iceberg**, que demuestra que la fracción de contradicciones detectables mediante evaluación puntual es una fracción decreciente de la contradicción total acumulada; (4) un modelo de **difusión de inconsistencia** que predice la velocidad a la que una contradicción local contamina las respuestas del sistema a consultas semánticamente adyacentes.

Las contribuciones principales son: (1) la primera formalización matemática completa de la deuda ontológica como métrica cuantificable y monitorizable; (2) el algoritmo de detección de contradicciones cruzadas sobre el top-k recuperado con complejidad O(k² · d) donde d es la dimensión del espacio de embeddings; (3) el framework de **Auditoría Ontológica Periódica** con umbrales de intervención derivados de la teoría de la información; (4) el protocolo de **Cuarentena Semántica** para documentos en conflicto; (5) la demostración empírica de que la deuda ontológica crece superlinealmente con el número de documentos indexados en ausencia de mecanismos de verificación.

La conclusión que ningún equipo de MLOps quiere escuchar: tu sistema RAG no está envenenado. Está enfermo. Y la enfermedad no vino de fuera. Vino de cada documento legítimo que indexaste sin verificar su consistencia con los documentos que ya estaban ahí.

---

## 1. Introducción

### 1.1 El problema que nadie diagnostica porque nadie lo ha nombrado

Existe una observación que los equipos que operan sistemas RAG en producción descubren tarde, si es que la descubren: el sistema que funciona correctamente hoy no es el mismo sistema que funcionará correctamente en seis meses. No porque los modelos de embeddings cambien —aunque eso también ocurre—. No porque el modelo de lenguaje se actualice —aunque eso también ocurre—. Sino porque la base vectorial acumula, con cada documento indexado, una cantidad pequeña de potencial contradicción que no se manifiesta hasta que una consulta específica activa simultáneamente los documentos contradictorios.

Esta acumulación es silenciosa. No produce logs. No produce métricas de error. No produce alertas de monitoring. El sistema responde a cada consulta individual con una respuesta plausible, coherente internamente, y estadísticamente indistinguible de una respuesta correcta. La contradicción solo se manifiesta cuando: (a) dos documentos contradictorios son recuperados simultáneamente para la misma consulta, o (b) la misma consulta se formula en dos momentos temporales diferentes y el conjunto de documentos recuperados ha cambiado entre ambos momentos por la adición de nuevos documentos.

En el primer caso, el LLM produce una respuesta que mezcla información contradictoria sin señalar la contradicción, porque el LLM no tiene un mecanismo nativo de verificación de consistencia lógica entre los documentos de su contexto. En el segundo caso, el sistema produce respuestas diferentes a la misma consulta en momentos diferentes, lo cual erosiona la confianza del usuario sin que ningún componente del sistema haya "fallado" en ningún sentido técnico detectable.

Este paper nombra esa patología, la formaliza matemáticamente, y proporciona las herramientas para diagnosticarla y tratarla antes de que el sistema alcance el punto de colapso funcional.

### 1.2 Por qué la similitud coseno no es suficiente

El mecanismo de recuperación en un sistema RAG estándar opera mediante similitud coseno en el espacio de embeddings:

$$\text{sim}(\mathbf{e}_q, \mathbf{e}_d) = \frac{\mathbf{e}_q \cdot \mathbf{e}_d}{|\mathbf{e}_q| \cdot |\mathbf{e}_d|} = \cos(\theta_{q,d})$$

Esta métrica mide la **proximidad direccional** entre el embedding de la consulta y el embedding del documento en el espacio vectorial. Mide, en esencia, si ambos "hablan de lo mismo". No mide si ambos "dicen lo mismo". No mide si ambos son **compatibles**.

Un documento que dice "el plazo de garantía es de 2 años" y un documento que dice "el plazo de garantía es de 5 años" tienen embeddings extremadamente cercanos en el espacio vectorial, porque ambos tratan sobre plazos de garantía. Su similitud coseno con la consulta "¿cuál es el plazo de garantía?" será alta en ambos casos. El sistema recuperará ambos. El LLM recibirá ambos en su contexto. Y producirá una respuesta que depende de cuál de los dos documentos reciba mayor peso atencional.

La similitud coseno es una métrica de **relevancia temática**. La deuda ontológica es un problema de **consistencia lógica**. Son ortogonales. Un sistema puede tener relevancia temática perfecta y consistencia lógica nula.

### 1.3 La analogía con la deuda técnica y por qué es precisa

Ward Cunningham (1992) introdujo la metáfora de la deuda técnica para describir el fenómeno por el cual las decisiones de diseño tomadas bajo presión de tiempo generan un coste futuro creciente: cada decisión subóptima es un "préstamo" que se paga con intereses en forma de dificultad de mantenimiento, bugs emergentes y rigidez arquitectónica.

La deuda ontológica es el análogo exacto de la deuda técnica, pero operando sobre la capa de conocimiento en lugar de la capa de código:

| Dimensión | Deuda técnica (Cunningham) | Deuda ontológica (este paper) |
|---|---|---|
| Recurso que se degrada | Código fuente | Base de conocimiento vectorial |
| Causa de la deuda | Decisiones de diseño bajo presión | Indexación de documentos sin verificación de consistencia |
| Manifestación | Bugs, fragilidad, dificultad de cambio | Respuestas incoherentes, contradicciones entre consultas |
| Detección | Code review, testing, métricas de complejidad | Auditoría ontológica, detección de contradicciones cruzadas |
| Crecimiento | Superlineal con el tiempo si no se paga | Superlineal con el número de documentos si no se audita |
| Coste de no pagar | Refactorización masiva o reescritura | Colapso de confianza del usuario, respuestas incorrectas en producción |
| Interés compuesto | Cada nueva feature sobre código deudor amplifica la deuda | Cada nuevo documento sobre base contradictoria amplifica las contradicciones existentes |

La analogía no es decorativa. Es estructuralmente precisa. Y tiene la misma implicación operativa: la deuda ontológica no se resuelve sola. Se acumula. Y el coste de resolverla crece con el tiempo.

### 1.4 El perfil del lector de este paper

Este paper está escrito para tres audiencias:

**El ingeniero de ML/IA** que opera un sistema RAG en producción y ha observado que las respuestas del sistema se han vuelto "raras" sin que ningún componente haya fallado explícitamente. Este lector encontrará en las Secciones 3-5 el marco diagnóstico que le faltaba, y en las Secciones 7-8 las herramientas de intervención.

**El arquitecto de datos** que diseña pipelines de ingesta documental para sistemas RAG y necesita comprender qué validaciones añadir más allá del filtro de contenido y la deduplicación. Este lector encontrará en la Sección 6 el protocolo de verificación de consistencia en frontera.

**El auditor de sistemas de IA** que necesita evaluar la integridad semántica de una base de conocimiento vectorial como parte de una auditoría de calidad o compliance. Este lector encontrará en la Sección 9 el tutorial completo de auditoría ontológica.

### 1.5 Estructura del paper

El paper tiene once secciones principales:

La **Sección 2** formaliza la deuda ontológica como métrica cuantificable: definición formal, modelo matemático de acumulación, y demostración de crecimiento superlineal.

La **Sección 3** desarrolla la taxonomía completa de contradicciones en bases vectoriales: contradicciones directas, contradicciones temporales, contradicciones de granularidad, contradicciones implícitas y contradicciones emergentes.

La **Sección 4** construye el modelo de grafo de contradicciones: nodos, aristas, pesos, componentes conexos, y la métrica de presión ontológica derivada.

La **Sección 5** formaliza el efecto iceberg: la fracción visible de contradicciones como función del número de consultas evaluadas, y la demostración de que la evaluación puntual subestima sistemáticamente la deuda.

La **Sección 6** describe los vectores de entrada de la contradicción: cómo documentos legítimos introducen inconsistencias en el sistema a través de los pipelines de ingesta estándar.

La **Sección 7** desarrolla el algoritmo de detección: verificación de consistencia cruzada sobre el top-k recuperado, con complejidad computacional analizada y pseudocódigo completo.

La **Sección 8** presenta las contramedidas: Cuarentena Semántica, Auditoría Ontológica Periódica, Índice de Coherencia Temporal, y Resolución Asistida de Contradicciones.

La **Sección 9** ofrece el tutorial práctico de auditoría ontológica con código ejecutable.

La **Sección 10** discute las implicaciones éticas y operativas: el deber de monitorizar la coherencia, la responsabilidad del operador, y el coste de la inacción.

La **Sección 11** concluye con la tesis central y las líneas de investigación futuras.

---

## 2. Formalización de la Deuda Ontológica

### 2.1 Definición formal

Definimos la **deuda ontológica** de un sistema RAG en un momento temporal $t$ como la magnitud de la inconsistencia lógica acumulada en su base vectorial, medida como la densidad de pares de documentos que contienen afirmaciones mutuamente incompatibles, ponderada por la severidad de la incompatibilidad y la probabilidad de co-recuperación.

Formalmente, sea $\mathcal{D}_t = \{d_1, d_2, \ldots, d_N\}$ la base de documentos en el momento $t$. Sea $\mathcal{Q}$ el espacio de consultas posibles. Sea $f_\theta: \mathcal{T} \rightarrow \mathbb{R}^d$ el modelo de embeddings. Sea $\text{top-}k(q)$ el conjunto de $k$ documentos recuperados para la consulta $q$.

Definimos la **función de contradicción** entre dos documentos $d_i$ y $d_j$ como:

$$\mathcal{C}(d_i, d_j) = \begin{cases} s_{ij} \in [0, 1] & \text{si } d_i \text{ y } d_j \text{ contienen afirmaciones incompatibles} \\ 0 & \text{en otro caso} \end{cases}$$

donde $s_{ij}$ es la **severidad** de la contradicción: 0 indica ausencia de contradicción, 1 indica contradicción absoluta (afirmaciones lógicamente excluyentes sobre el mismo hecho).

La **deuda ontológica** del sistema en el momento $t$ se define como:

$$\mathcal{DO}(t) = \sum_{i=1}^{N} \sum_{j=i+1}^{N} \mathcal{C}(d_i, d_j) \cdot P_{\text{co}}(d_i, d_j)$$

donde $P_{\text{co}}(d_i, d_j)$ es la **probabilidad de co-recuperación**: la probabilidad de que ambos documentos sean recuperados simultáneamente para alguna consulta del espacio $\mathcal{Q}$:

$$P_{\text{co}}(d_i, d_j) = P_{q \sim \mathcal{Q}}\left(\{d_i, d_j\} \subseteq \text{top-}k(q)\right)$$

Esta definición captura tres intuiciones fundamentales:

**Primera intuición:** No toda contradicción contribuye igual a la deuda. Una contradicción entre dos documentos que nunca son recuperados juntos tiene impacto cero en las respuestas del sistema. La deuda ontológica no es la contradicción absoluta; es la contradicción **operativa**.

**Segunda intuición:** La severidad importa. Una contradicción sobre un dato numérico ("el plazo es 30 días" vs. "el plazo es 90 días") tiene severidad diferente de una contradicción sobre un matiz interpretativo ("el procedimiento es obligatorio" vs. "el procedimiento es recomendable").

**Tercera intuición:** La deuda es una función del tiempo. Cada documento indexado puede introducir nuevas contradicciones con documentos existentes. La deuda crece monótonamente en ausencia de mecanismos de resolución.

### 2.2 Modelo de acumulación: crecimiento superlineal

La propiedad más peligrosa de la deuda ontológica es que crece **superlinealmente** con el número de documentos indexados. Demostramos esto formalmente.

Sea $N(t)$ el número de documentos en la base en el momento $t$. Sea $\lambda$ la tasa de indexación de documentos nuevos (documentos/unidad de tiempo). Sea $p_c$ la probabilidad de que un documento nuevo introduzca al menos una contradicción con algún documento existente.

En el momento $t$, el número esperado de pares contradictorios es:

$$E[\text{pares contradictorios}] = \binom{N(t)}{2} \cdot p_c = \frac{N(t)(N(t)-1)}{2} \cdot p_c$$

Dado que $N(t) = N_0 + \lambda t$ (crecimiento lineal de la base), el número de pares contradictorios crece como:

$$E[\text{pares}] = \frac{(N_0 + \lambda t)(N_0 + \lambda t - 1)}{2} \cdot p_c \approx \frac{\lambda^2 t^2}{2} \cdot p_c \quad \text{para } t \gg N_0/\lambda$$

El crecimiento es **cuadrático** en el tiempo, no lineal. Esto significa que un sistema que indexa 100 documentos/mes durante 6 meses acumula aproximadamente $(600 \times 599 / 2) \times p_c \approx 180.000 \times p_c$ pares potencialmente contradictorios. Si $p_c = 0.02$ (un 2% de los pares de documentos sobre temas similares contienen alguna contradicción), eso son 3.600 contradicciones latentes.

La deuda ontológica, ponderada por la probabilidad de co-recuperación, crece como:

$$\mathcal{DO}(t) \approx \frac{\lambda^2 t^2}{2} \cdot p_c \cdot \bar{s} \cdot \bar{P}_{\text{co}}$$

donde $\bar{s}$ es la severidad media y $\bar{P}_{\text{co}}$ es la probabilidad media de co-recuperación.

**Corolario:** Un sistema RAG que no implementa verificación de consistencia en la ingesta tiene una deuda ontológica que crece cuadráticamente. El coste de resolverla (auditoría completa + resolución de contradicciones) crece al mismo ritmo. El sistema que no paga su deuda ontológica se acerca asintóticamente al colapso funcional.

### 2.3 La condición de colapso funcional

Definimos el **umbral de colapso funcional** $\mathcal{DO}_{\text{crit}}$ como el nivel de deuda ontológica por encima del cual la probabilidad de que una consulta cualquiera produzca una respuesta que contradice una respuesta previa del sistema supera un umbral aceptable $\epsilon$:

$$P_{q \sim \mathcal{Q}}\left(\exists q' \in \mathcal{Q}_{\text{hist}} : r(q,t) \text{ contradice } r(q', t')\right) > \epsilon$$

donde $r(q,t)$ es la respuesta del sistema a la consulta $q$ en el momento $t$, y $\mathcal{Q}_{\text{hist}}$ es el historial de consultas previas.

El umbral $\mathcal{DO}_{\text{crit}}$ depende de:
- La dimensión del espacio de embeddings $d$ (espacios de mayor dimensión tienen mayor capacidad de "separar" documentos contradictorios, reduciendo $P_{\text{co}}$).
- El tamaño del top-$k$ (valores mayores de $k$ aumentan la probabilidad de co-recuperación de documentos contradictorios).
- La distribución de consultas (consultas concentradas en pocos temas tienen mayor $P_{\text{co}}$ para documentos de esos temas).
- La severidad media de las contradicciones.

Para un sistema típico con $d = 1536$, $k = 5$, y una distribución de consultas moderadamente concentrada, estimamos $\mathcal{DO}_{\text{crit}}$ en el rango de 50-200 contradicciones activas de severidad media $\bar{s} > 0.5$.

### 2.4 Relación con la entropía de Shannon

La deuda ontológica tiene una interpretación informacional directa. Sea $H(R|Q)$ la entropía condicional de la respuesta $R$ dada la consulta $Q$. En un sistema perfectamente coherente, $H(R|Q)$ está determinada únicamente por la ambigüedad intrínseca de la consulta: una consulta ambigua produce una distribución de respuestas amplia; una consulta precisa produce una distribución concentrada.

En un sistema con deuda ontológica, $H(R|Q)$ tiene un componente adicional: la **entropía de contradicción** $H_{\text{contra}}$, que mide la incertidumbre introducida por la presencia de documentos contradictorios en el top-$k$:

$$H(R|Q) = H_{\text{intrínseca}}(R|Q) + H_{\text{contra}}(R|Q)$$

La entropía de contradicción se define como:

$$H_{\text{contra}}(R|Q) = -\sum_{r \in \mathcal{R}} P(r|Q, \mathcal{D}_{\text{contra}}) \log P(r|Q, \mathcal{D}_{\text{contra}})$$

donde $\mathcal{D}_{\text{contra}} \subseteq \text{top-}k(q)$ es el subconjunto de documentos recuperados que participan en al menos una contradicción.

Cuando $H_{\text{contra}}$ domina sobre $H_{\text{intrínseca}}$, el sistema ha perdido la capacidad de dar respuestas consistentes: la respuesta a una consulta depende de qué documentos contradictorios fueron recuperados, no del contenido semántico de la consulta.

---

## 3. Taxonomía de Contradicciones en Bases Vectoriales

### 3.1 Contradicción directa (Tipo I)

La forma más simple y más fácil de detectar. Dos documentos afirman valores mutuamente excluyentes para la misma variable, en el mismo contexto, con la misma granularidad.

**Ejemplo:**
- Documento A (indexado 2026-01-15): "La política de retención de datos personales es de 90 días tras la finalización del contrato."
- Documento B (indexado 2026-05-03): "La política de retención de datos personales es de 30 días tras la finalización del contrato, según la actualización aprobada por el Comité de Privacidad."

Ambos documentos tratan sobre retención de datos personales. Ambos son recuperados para la consulta "¿cuánto tiempo se retienen los datos personales?". El LLM recibe ambos y produce una respuesta que puede mencionar 90 días, 30 días, o ambos, dependiendo del peso atencional.

**Severidad típica:** $s \in [0.7, 1.0]$. La contradicción es binaria: un valor es correcto y el otro no.

**Detección:** Relativamente sencilla si se dispone de un extractor de afirmaciones factuales. La dificultad está en la extracción, no en la comparación.

### 3.2 Contradicción temporal (Tipo II)

Dos documentos son individualmente correctos en su momento temporal, pero contradictorios cuando se recuperan simultáneamente sin contexto temporal.

**Ejemplo:**
- Documento A (indexado 2025-03-10): "El CEO de la empresa es María González."
- Documento B (indexado 2026-02-20): "El CEO de la empresa es Carlos Ruiz, tras la transición de liderazgo aprobada en enero de 2026."

Ninguno de los dos documentos es "incorrecto" en sí mismo. El documento A era correcto en marzo de 2025. El documento B es correcto en febrero de 2026. Pero si el sistema RAG no tiene un mecanismo de resolución temporal, ambos documentos son igualmente válidos desde la perspectiva de la similitud coseno, y la respuesta a "¿quién es el CEO?" depende de cuál se recupere.

**Severidad típica:** $s \in [0.5, 0.8]$. La contradicción es real pero tiene resolución temporal: el documento más reciente es el correcto.

**Detección:** Requiere extracción de timestamps y comparación cronológica. El sistema debe determinar cuál de los dos documentos es temporalmente dominante.

**Contramedida específica:** Índice de Coherencia Temporal (Sección 8.3).

### 3.3 Contradicción de granularidad (Tipo III)

Dos documentos no se contradicen en el nivel de abstracción en que operan, pero producen respuestas incompatibles cuando se combinan en el mismo contexto.

**Ejemplo:**
- Documento A (política general): "Todos los empleados tienen derecho a 25 días de vacaciones anuales."
- Documento B (convenio específico del departamento de ingeniería): "Los ingenieros senior con más de 5 años de antigüedad tienen derecho a 30 días de vacaciones anuales."

Estos documentos no son lógicamente contradictorios: el documento B es una excepción al documento A. Pero si el sistema RAG recupera ambos para la consulta "¿cuántos días de vacaciones tengo?" sin capacidad de resolver la jerarquía de especificidad, producirá una respuesta ambigua o contradictoria.

**Severidad típica:** $s \in [0.3, 0.6]$. La contradicción es resoluble mediante reglas de jerarquía (lo específico prevalece sobre lo general), pero el LLM no tiene esas reglas codificadas de manera nativa.

**Detección:** Requiere análisis de jerarquía documental y resolución de especificidad. Es la forma más difícil de detectar automáticamente.

### 3.4 Contradicción implícita (Tipo IV)

Ningún documento afirma explícitamente la contradicción. La contradicción emerge de la combinación de afirmaciones que, individualmente, son consistentes con otros documentos, pero que en conjunto producen una inferencia contradictoria.

**Ejemplo:**
- Documento A: "El presupuesto del proyecto X para 2026 es de 500.000€."
- Documento B: "El proyecto X incluye la contratación de 10 ingenieros a 80.000€/año cada uno."
- Documento C: "Los costes de personal del proyecto X no pueden exceder el 60% del presupuesto total."

Individualmente, los tres documentos son plausibles. Combinados, producen una contradicción implícita: 10 × 80.000€ = 800.000€ > 60% × 500.000€ = 300.000€. El sistema RAG que recupera estos tres documentos para una consulta sobre el presupuesto del proyecto X producirá una respuesta que no puede ser simultáneamente consistente con los tres.

**Severidad típica:** $s \in [0.4, 0.9]$ dependiendo de la claridad de la inferencia contradictoria.

**Detección:** Extremadamente difícil. Requiere razonamiento inferencial sobre el contenido de los documentos, no solo comparación de afirmaciones explícitas. Es el tipo de contradicción que más se beneficia de la intervención humana.

### 3.5 Contradicción emergente (Tipo V)

La contradicción no existe en ningún par de documentos. Emerge de la interacción entre tres o más documentos que, tomados en pares, son consistentes, pero que en conjunto producen un estado incoherente.

**Ejemplo:**
- Documento A: "El proveedor de hosting es AWS."
- Documento B: "Todos los datos de clientes europeos deben almacenarse en datacenters dentro de la UE."
- Documento C: "El datacenter principal de AWS para esta cuenta está en us-east-1 (Virginia, EE.UU.)."

Cualquier par de estos documentos es consistente. Los tres juntos producen una contradicción normativa: el sistema almacena datos europeos en EE.UU., violando la política del documento B.

**Severidad típica:** $s \in [0.6, 1.0]$. Las contradicciones emergentes suelen ser las más severas porque involucran violaciones de políticas o restricciones que nadie detectó al indexar los documentos individualmente.

**Detección:** Requiere análisis de tripletas (o n-tuplas) de documentos. La complejidad combinatoria hace que la detección exhaustiva sea intratable para bases grandes. Se requieren métodos de muestreo inteligente.

### 3.6 Tabla resumen de la taxonomía

| Tipo | Nombre | Severidad típica | Dificultad de detección | Frecuencia relativa | Resolución |
|---|---|---|---|---|---|
| I | Contradicción directa | 0.7–1.0 | Baja | 15–25% | Eliminación del documento obsoleto |
| II | Contradicción temporal | 0.5–0.8 | Media | 30–40% | Resolución temporal (el más reciente prevalece) |
| III | Contradicción de granularidad | 0.3–0.6 | Alta | 20–30% | Resolución jerárquica (lo específico prevalece) |
| IV | Contradicción implícita | 0.4–0.9 | Muy alta | 10–15% | Razonamiento inferencial + intervención humana |
| V | Contradicción emergente | 0.6–1.0 | Extrema | 5–10% | Análisis de n-tuplas + intervención humana |

La distribución de frecuencias es una estimación basada en auditorías realizadas por Agencia RONIN sobre sistemas RAG empresariales entre 2024 y 2026. La proporción de contradicciones temporales (Tipo II) domina en la mayoría de los sistemas porque la mayoría de las bases vectoriales indexan documentos de múltiples versiones temporales sin un mecanismo de obsolescencia.

---

## 4. El Grafo de Contradicciones

### 4.1 Construcción del grafo

Modelamos la estructura de contradicciones de una base vectorial como un grafo ponderado $G_t = (V_t, E_t, w_t)$ donde:

- $V_t = \{v_1, v_2, \ldots, v_N\}$ es el conjunto de nodos, uno por documento en la base.
- $E_t \subseteq V_t \times V_t$ es el conjunto de aristas, donde $(v_i, v_j) \in E_t$ si y solo si $\mathcal{C}(d_i, d_j) > \theta_{\text{min}}$ para algún umbral mínimo de severidad $\theta_{\text{min}}$.
- $w_t: E_t \rightarrow [0, 1]$ es la función de peso, donde $w_t(v_i, v_j) = \mathcal{C}(d_i, d_j) \cdot P_{\text{co}}(d_i, d_j)$.

El peso de cada arista combina la severidad de la contradicción con la probabilidad de que esa contradicción sea operativa (es decir, de que ambos documentos sean recuperados simultáneamente).

### 4.2 Componentes conexos y clusters de contradicción

Un **componente conexo** del grafo de contradicciones es un subconjunto maximal de documentos donde cada documento está conectado a al menos otro documento del subconjunto mediante una cadena de contradicciones. Los componentes conexos representan **clusters de contradicción**: grupos de documentos que, directa o indirectamente, se contradicen entre sí.

La importancia operativa de los componentes conexos es la siguiente: si un documento $d_i$ pertenece a un componente conexo de tamaño $|C| > 1$, entonces cualquier consulta que recupere $d_i$ tiene una probabilidad no nula de recuperar también algún otro documento del mismo componente, produciendo una respuesta potencialmente incoherente.

Definimos la **presión ontológica** de un documento $d_i$ como:

$$\mathcal{P}(d_i) = \sum_{v_j \in \text{vec}(v_i)} w_t(v_i, v_j)$$

donde $\text{vec}(v_i)$ es el conjunto de vecinos de $v_i$ en el grafo. La presión ontológica mide cuánta contradicción "soporta" un documento individual.

La **presión ontológica global** del sistema es:

$$\mathcal{P}_{\text{global}} = \frac{1}{|V_t|} \sum_{v_i \in V_t} \mathcal{P}(d_i) = \frac{2 \sum_{(v_i,v_j) \in E_t} w_t(v_i,v_j)}{|V_t|}$$

El factor 2 aparece porque cada arista contribuye a la presión de ambos nodos que conecta.

### 4.3 El documento crítico: nodos de alta intermediación

En el grafo de contradicciones, los nodos con alta **intermediación** (betweenness centrality) son los más peligrosos. Un nodo con alta intermediación es un documento que conecta múltiples clusters de contradicción: su eliminación del grafo desconectaría componentes que de otra manera estarían unidos.

Operativamente, un documento con alta intermediación es un documento que, cuando es recuperado, "activa" simultáneamente múltiples contradicciones. Es el documento que más daño causa cuando entra en el contexto del LLM.

La betweenness centrality de un nodo $v_i$ se define como:

$$B(v_i) = \sum_{v_s \neq v_i \neq v_t} \frac{\sigma_{st}(v_i)}{\sigma_{st}}$$

donde $\sigma_{st}$ es el número de caminos más cortos entre $v_s$ y $v_t$, y $\sigma_{st}(v_i)$ es el número de esos caminos que pasan por $v_i$.

Los documentos con $B(v_i) > \theta_B$ (para un umbral $\theta_B$ calibrado empíricamente) deben ser priorizados para auditoría y resolución.

### 4.4 Evolución temporal del grafo

El grafo de contradicciones no es estático. Cada documento nuevo indexado puede:

1. **Añadir nodos aislados:** el documento nuevo no se contradice con ningún documento existente. El grafo gana un nodo sin aristas. La deuda no cambia.

2. **Añadir aristas:** el documento nuevo se contradice con uno o más documentos existentes. El grafo gana aristas. La deuda aumenta.

3. **Conectar componentes:** el documento nuevo se contradice con documentos de dos componentes conexos previamente desconectados. Los componentes se fusionan. La presión ontológica de todos los documentos en el componente fusionado aumenta.

4. **Intensificar contradicciones existentes:** el documento nuevo no introduce una contradicción nueva, pero refuerza una contradicción existente al proporcionar una tercera fuente que confirma uno de los dos lados. La severidad percibida de la contradicción cambia.

La dinámica del grafo es, en esencia, un proceso de **percolación**: las aristas de contradicción se acumulan hasta que, en un momento crítico, aparece un componente conexo gigante que abarca una fracción significativa de la base. En ese momento, la deuda ontológica se vuelve sistémica: ya no es un problema local de dos documentos que se contradicen, sino un problema global de coherencia del corpus.

### 4.5 Pseudocódigo: construcción del grafo de contradicciones

```python
import numpy as np
from itertools import combinations
from typing import List, Tuple, Dict
from dataclasses import dataclass

@dataclass
class ContradictionEdge:
    doc_i: int
    doc_j: int
    severity: float        # s_ij ∈ [0, 1]
    co_retrieval_prob: float  # P_co(d_i, d_j)
    weight: float          # severity * co_retrieval_prob
    contradiction_type: int  # I, II, III, IV, V
    description: str

class ContradictionGraph:
    """
    Grafo de contradicciones de una base vectorial.
    Implementa la formalización de la Sección 4.
    """
    def __init__(self, n_documents: int):
        self.n = n_documents
        self.edges: List[ContradictionEdge] = []
        self.adjacency: Dict[int, List[Tuple[int, float]]] = {
            i: [] for i in range(n_documents)
        }
    
    def add_contradiction(
        self, i: int, j: int, severity: float,
        co_prob: float, ctype: int, desc: str
    ):
        """Añade una arista de contradicción al grafo."""
        weight = severity * co_prob
        edge = ContradictionEdge(
            doc_i=i, doc_j=j, severity=severity,
            co_retrieval_prob=co_prob, weight=weight,
            contradiction_type=ctype, description=desc
        )
        self.edges.append(edge)
        self.adjacency[i].append((j, weight))
        self.adjacency[j].append((i, weight))
    
    def ontological_pressure(self, doc_id: int) -> float:
        """Presión ontológica de un documento (Sección 4.2)."""
        return sum(w for _, w in self.adjacency[doc_id])
    
    def global_pressure(self) -> float:
        """Presión ontológica global del sistema."""
        total_weight = sum(e.weight for e in self.edges)
        return 2.0 * total_weight / self.n if self.n > 0 else 0.0
    
    def connected_components(self) -> List[List[int]]:
        """Encuentra componentes conexos del grafo."""
        visited = set()
        components = []
        for start in range(self.n):
            if start in visited:
                continue
            if not self.adjacency[start]:
                continue  # Nodo aislado, no forma componente de contradicción
            component = []
            stack = [start]
            while stack:
                node = stack.pop()
                if node in visited:
                    continue
                visited.add(node)
                component.append(node)
                for neighbor, _ in self.adjacency[node]:
                    if neighbor not in visited:
                        stack.append(neighbor)
            if len(component) > 1:
                components.append(component)
        return components
    
    def betweenness_centrality(self) -> Dict[int, float]:
        """
        Betweenness centrality aproximada (Brandes, 2001).
        Para grafos de contradicción típicos (N < 10000 aristas).
        """
        centrality = {i: 0.0 for i in range(self.n)}
        # Implementación simplificada de Brandes
        for s in range(self.n):
            if not self.adjacency[s]:
                continue
            # BFS desde s
            stack = []
            predecessors = {i: [] for i in range(self.n)}
            sigma = {i: 0 for i in range(self.n)}
            sigma[s] = 1
            dist = {i: -1 for i in range(self.n)}
            dist[s] = 0
            queue = [s]
            qi = 0
            while qi < len(queue):
                v = queue[qi]
                qi += 1
                stack.append(v)
                for w, _ in self.adjacency[v]:
                    if dist[w] < 0:
                        dist[w] = dist[v] + 1
                        queue.append(w)
                    if dist[w] == dist[v] + 1:
                        sigma[w] += sigma[v]
                        predecessors[w].append(v)
            # Acumulación
            delta = {i: 0.0 for i in range(self.n)}
            while stack:
                w = stack.pop()
                for v in predecessors[w]:
                    delta[v] += (sigma[v] / sigma[w]) * (1 + delta[w])
                if w != s:
                    centrality[w] += delta[w]
        # Normalizar
        for v in centrality:
            centrality[v] /= 2.0
        return centrality
    
    def ontological_debt(self) -> float:
        """Deuda ontológica total (Sección 2.1)."""
        return sum(e.weight for e in self.edges)
```

---

## 5. El Efecto Iceberg: La Fracción Invisible de la Contradicción

### 5.1 Formulación del efecto

El **efecto iceberg** en sistemas RAG establece que la fracción de contradicciones detectables mediante evaluación puntual del sistema es una fracción estrictamente decreciente de la contradicción total acumulada, y que esta fracción tiende a cero a medida que la base vectorial crece.

Formalizamos esto. Sea $\mathcal{Q}_{\text{eval}} = \{q_1, q_2, \ldots, q_M\}$ un conjunto de $M$ consultas de evaluación. Sea $\mathcal{C}_{\text{total}}$ el conjunto de todas las contradicciones en la base. Sea $\mathcal{C}_{\text{visible}}(q)$ el subconjunto de contradicciones que son "visibles" para la consulta $q$ —es decir, contradicciones donde ambos documentos son recuperados en el top-$k$ de $q$.

La fracción visible para una consulta es:

$$f_{\text{vis}}(q) = \frac{|\mathcal{C}_{\text{visible}}(q)|}{|\mathcal{C}_{\text{total}}|}$$

La fracción visible total para el conjunto de evaluación es:

$$F_{\text{vis}}(\mathcal{Q}_{\text{eval}}) = \frac{|\bigcup_{q \in \mathcal{Q}_{\text{eval}}} \mathcal{C}_{\text{visible}}(q)|}{|\mathcal{C}_{\text{total}}|}$$

**Teorema del Efecto Iceberg:** Para una base vectorial con $N$ documentos, $k$ documentos recuperados por consulta, y una distribución de consultas con entropía $H_Q$, la fracción visible esperada satisface:

$$E[F_{\text{vis}}] \leq \frac{M \cdot \binom{k}{2}}{\binom{N}{2}} \cdot \frac{1}{H_Q / \log_2 |\mathcal{Q}|}$$

**Demostración (esquema):** Cada consulta evalúa $\binom{k}{2}$ pares de documentos de un total de $\binom{N}{2}$ pares posibles. La probabilidad de que un par contradictorio específico sea evaluado por una consulta específica es $O(k^2 / N^2)$. Con $M$ consultas, la probabilidad de que un par contradictorio sea evaluado al menos una vez es $O(M \cdot k^2 / N^2)$. Para $N = 10.000$, $k = 5$, $M = 1.000$ consultas de evaluación, esta probabilidad es $O(1000 \times 25 / 50.000.000) = O(0.0005)$. Es decir: una evaluación con 1.000 consultas detecta aproximadamente el 0.05% de las contradicciones potenciales.

### 5.2 Implicación operativa

El efecto iceberg tiene una implicación devastadora para los equipos que evalúan sus sistemas RAG mediante conjuntos de consultas de prueba: **la ausencia de contradicciones detectadas en la evaluación no implica la ausencia de contradicciones en el sistema.** Implica únicamente que las consultas de evaluación no activaron las contradicciones existentes.

Esto es análogo al problema de testing en software: la ausencia de bugs detectados no implica la ausencia de bugs. Pero en el caso de la deuda ontológica, la analogía es más severa porque el "espacio de tests" (el espacio de consultas posibles) es astronómicamente grande, y las contradicciones están distribuidas de manera no uniforme en ese espacio.

### 5.3 La paradoja de la evaluación longitudinal

Un sistema RAG puede pasar todas las evaluaciones puntuales y aún así ser incoherente longitudinalmente. La razón es que las evaluaciones puntuales miden $r(q, t)$ para un conjunto fijo de consultas en un momento $t$. La incoherencia longitudinal se manifiesta cuando $r(q, t_1) \neq r(q, t_2)$ para la misma consulta $q$ en momentos diferentes, debido a que el conjunto de documentos recuperados ha cambiado entre $t_1$ y $t_2$.

Esta forma de incoherencia es invisible para cualquier evaluación que no compare respuestas del sistema consigo mismo a lo largo del tiempo. Requiere un **registro de respuestas históricas** y un mecanismo de **comparación longitudinal** que la mayoría de los sistemas RAG no implementan.

### 5.4 Cuantificación del iceberg

Para un sistema RAG típico con las siguientes características:
- $N = 5.000$ documentos en la base
- $k = 5$ documentos recuperados por consulta
- $M = 500$ consultas de evaluación mensuales
- $p_c = 0.02$ (probabilidad de contradicción por par)
- $\bar{s} = 0.6$ (severidad media)

Las cifras son:

| Métrica | Valor |
|---|---|
| Pares totales de documentos | $\binom{5000}{2} = 12.497.500$ |
| Pares contradictorios esperados | $12.497.500 \times 0.02 = 249.950$ |
| Pares evaluados por consulta | $\binom{5}{2} = 10$ |
| Pares evaluados por mes | $500 \times 10 = 5.000$ |
| Fracción del espacio de pares evaluada | $5.000 / 12.497.500 = 0.04\%$ |
| Contradicciones detectables por mes | $249.950 \times 0.0004 \approx 100$ |
| Contradicciones reales | $249.950$ |
| Fracción visible | $0.04\%$ |

El 99.96% de las contradicciones son invisibles para la evaluación mensual estándar.

---

## 6. Vectores de Entrada de la Contradicción

### 6.1 Ingesta multi-fuente sin verificación cruzada

La mayoría de los sistemas RAG empresariales indexan documentos de múltiples fuentes: SharePoint, Confluence, Google Drive, repositorios Git, APIs de terceros, feeds RSS, emails archivados. Cada fuente tiene su propio ciclo de actualización, su propio responsable editorial, y su propio nivel de rigor.

Cuando un documento de la fuente A dice "el procedimiento de escalado es X" y un documento de la fuente B dice "el procedimiento de escalado es Y", el sistema RAG indexa ambos sin ningún mecanismo de detección del conflicto. El conflicto no es un error de ingesta; es una consecuencia inevitable de la independencia editorial de las fuentes.

### 6.2 Actualización incremental sin invalidación

Cuando un documento se actualiza (una política cambia, un procedimiento se revisa), la mayoría de los pipelines RAG indexan la nueva versión pero no invalidan la versión anterior. El resultado es que ambas versiones coexisten en la base vectorial, produciendo una contradicción temporal (Tipo II) que se acumula indefinidamente.

La invalidación requiere: (a) un mecanismo de versionado de documentos, (b) una política de retención de versiones obsoletas, y (c) un proceso de re-embedding que elimine los embeddings de las versiones invalidadas. Ninguno de estos tres componentes es estándar en los pipelines RAG actuales.

### 6.3 Documentos de terceros con contexto implícito

Un documento técnico descargado de un repositorio externo puede contener afirmaciones que son correctas en el contexto del proveedor pero incorrectas en el contexto de la organización que lo indexa. Por ejemplo, un documento de un proveedor de cloud que dice "la latencia media de nuestra red es de 12ms" es correcto para la red del proveedor, pero si se indexa en la base RAG de un cliente que usa esa red con una configuración diferente, la afirmación puede ser incorrecta para el contexto del cliente.

### 6.4 Documentos generados por IA sin verificación humana

La práctica creciente de usar LLMs para generar documentación interna (resúmenes de reuniones, informes de estado, descripciones de procedimientos) introduce un vector de contradicción particularmente peligroso: el documento generado puede contener afirmaciones que contradicen documentos existentes porque el LLM que lo generó no tenía acceso a la base vectorial completa en el momento de la generación.

### 6.5 El pipeline de ingesta como punto de intervención

Todos los vectores descritos convergen en el pipeline de ingesta. El punto de intervención más eficiente no es la detección posterior (que requiere auditoría sobre toda la base), sino la **verificación en frontera**: comprobar la consistencia del documento nuevo con los documentos existentes en el momento de la indexación.

El coste de la verificación en frontera es $O(k \cdot d)$ por documento nuevo (comparar el documento nuevo con los $k$ documentos más similares ya indexados). El coste de la auditoría posterior es $O(N^2 \cdot d)$ para una base de $N$ documentos. La diferencia es de órdenes de magnitud.

---

## 7. Detección: Algoritmos de Verificación de Consistencia Cruzada

### 7.1 Verificación sobre el top-k recuperado

El mecanismo de detección más directo opera en el momento de la recuperación: cuando el sistema recupera los $k$ documentos para una consulta, verifica la consistencia lógica entre ellos antes de inyectarlos en el contexto del LLM.

**Algoritmo de Verificación de Consistencia Cruzada (VCC):**

```
ENTRADA:
  - q: consulta del usuario
  - top_k: lista de k documentos recuperados
  - embed_model: modelo de embeddings
  - nli_model: modelo de inferencia lógica (Natural Language Inference)
  - threshold: umbral de contradicción (típico: 0.7)

SALIDA:
  - contradictions: lista de pares contradictorios detectados
  - filtered_top_k: top_k con documentos contradictorios marcados

ALGORITMO:
  1. Para cada par (d_i, d_j) en top_k × top_k donde i < j:
     a. Extraer afirmaciones factuales de d_i: A_i = extract_claims(d_i)
     b. Extraer afirmaciones factuales de d_j: A_j = extract_claims(d_j)
     c. Para cada par de afirmaciones (a_i, a_j) en A_i × A_j:
        - Computar entailment score: s = nli_model(a_i, a_j)
        - Si s < threshold (contradicción detectada):
          → Añadir (d_i, d_j, a_i, a_j, s) a contradictions
  2. Si contradictions no está vacío:
     - Marcar los documentos involucrados
     - Generar alerta con severidad = max(s) sobre todas las contradicciones
  3. Retornar (contradictions, filtered_top_k)

COMPLEJIDAD:
  - Extracción de afirmaciones: O(k × |A|) donde |A| es el número medio
    de afirmaciones por documento
  - Comparación de afirmaciones: O(k² × |A|²)
  - Inferencia lógica: O(k² × |A|² × cost_NLI)
  - Para k=5, |A|=10, cost_NLI=50ms: ≈ 5² × 10² × 0.05s = 12.5s
  - Optimización: solo comparar afirmaciones con similitud semántica > 0.6
    (reducción a ≈ 1.2s en la práctica)
```

### 7.2 Detección proactiva en el momento de la ingesta

La verificación en frontera (Sección 6.5) opera en el momento de la indexación:

```python
class OntologicalVerifier:
    """
    Verificador de consistencia en frontera para el pipeline de ingesta.
    Comprueba cada documento nuevo contra los documentos existentes
    más similares antes de permitir la indexación.
    """
    def __init__(
        self,
        embed_model,
        nli_model,
        vector_store,
        k_check: int = 10,
        sim_threshold: float = 0.75,
        contra_threshold: float = 0.7
    ):
        self.embed_model = embed_model
        self.nli_model = nli_model
        self.vector_store = vector_store
        self.k_check = k_check
        self.sim_threshold = sim_threshold
        self.contra_threshold = contra_threshold
    
    def verify_document(self, new_doc: str) -> dict:
        """
        Verifica un documento nuevo contra la base existente.
        Retorna un dict con el resultado de la verificación.
        """
        # 1. Generar embedding del documento nuevo
        new_embedding = self.embed_model.encode([new_doc])[0]
        
        # 2. Recuperar los k_check documentos más similares
        similar_docs = self.vector_store.query(
            new_embedding,
            top_k=self.k_check,
            min_similarity=self.sim_threshold
        )
        
        # 3. Para cada documento similar, verificar consistencia
        contradictions = []
        for doc, sim_score in similar_docs:
            # Extraer afirmaciones de ambos documentos
            claims_new = self._extract_claims(new_doc)
            claims_existing = self._extract_claims(doc.content)
            
            # Comparar afirmaciones con similitud semántica alta
            for claim_new in claims_new:
                for claim_existing in claims_existing:
                    # Solo comparar si las afirmaciones son
                    # semánticamente relacionadas
                    claim_sim = self._claim_similarity(
                        claim_new, claim_existing
                    )
                    if claim_sim < 0.6:
                        continue
                    
                    # Inferencia lógica
                    nli_result = self.nli_model.predict(
                        premise=claim_existing,
                        hypothesis=claim_new
                    )
                    
                    if nli_result.label == 'CONTRADICTION':
                        contradictions.append({
                            'new_claim': claim_new,
                            'existing_claim': claim_existing,
                            'existing_doc_id': doc.id,
                            'similarity': sim_score,
                            'nli_score': nli_result.score,
                            'severity': nli_result.score
                        })
        
        # 4. Decisión de ingesta
        if not contradictions:
            return {
                'status': 'CLEAR',
                'message': 'No se detectaron contradicciones.',
                'contradictions': []
            }
        
        max_severity = max(c['severity'] for c in contradictions)
        
        if max_severity > 0.9:
            return {
                'status': 'BLOCKED',
                'message': (
                    f'Contradicción crítica detectada '
                    f'(severidad {max_severity:.2f}). '
                    f'Documento en cuarentena.'
                ),
                'contradictions': contradictions,
                'action': 'QUARANTINE'
            }
        elif max_severity > self.contra_threshold:
            return {
                'status': 'FLAGGED',
                'message': (
                    f'Contradicción moderada detectada '
                    f'(severidad {max_severity:.2f}). '
                    f'Requiere revisión humana.'
                ),
                'contradictions': contradictions,
                'action': 'REVIEW'
            }
        else:
            return {
                'status': 'CLEAR_WITH_NOTE',
                'message': (
                    f'Inconsistencia menor detectada '
                    f'(severidad {max_severity:.2f}). '
                    f'Indexado con nota.'
                ),
                'contradictions': contradictions,
                'action': 'INDEX_WITH_NOTE'
            }
    
    def _extract_claims(self, text: str) -> list:
        """
        Extrae afirmaciones factuales de un texto.
        En producción: usar un modelo de extracción de relaciones
        (spaCy + dependency parsing, o un LLM con prompt específico).
        """
        # Implementación simplificada: dividir en oraciones
        # y filtrar las que contienen verbos factuales
        sentences = text.split('. ')
        factual_claims = [
            s.strip() for s in sentences
            if any(v in s.lower() for v in [
                'es', 'son', 'tiene', 'debe', 'puede',
                'está', 'será', 'fue', 'incluye', 'requiere'
            ])
        ]
        return factual_claims
    
    def _claim_similarity(self, claim_a: str, claim_b: str) -> float:
        """Similitud semántica entre dos afirmaciones."""
        emb_a = self.embed_model.encode([claim_a])[0]
        emb_b = self.embed_model.encode([claim_b])[0]
        return float(np.dot(emb_a, emb_b) / (
            np.linalg.norm(emb_a) * np.linalg.norm(emb_b)
        ))
```

### 7.3 Detección de contradicciones implícitas mediante razonamiento

Las contradicciones de Tipo IV y V requieren un nivel de razonamiento que la comparación directa de afirmaciones no puede proporcionar. Para estas, proponemos un mecanismo de **verificación inferencial** que utiliza un LLM como razonador:

```
PROTOCOL DE VERIFICACIÓN INFERENCIAL:

ENTRADA:
  - top_k documentos recuperados
  - Consulta del usuario

PASO 1: Construir el "contexto combinado"
  → Concatenar los k documentos en un solo contexto
  
PASO 2: Prompt de verificación al LLM razonador
  → "Dado el siguiente conjunto de documentos, identifica
     cualquier inconsistencia lógica, contradicción numérica,
     o incompatibilidad normativa entre ellos. Para cada
     inconsistencia encontrada, especifica:
     (a) Los documentos involucrados
     (b) Las afirmaciones específicas que se contradicen
     (c) La naturaleza de la contradicción
     (d) La severidad estimada (baja/media/alta/crítica)"

PASO 3: Parsear la respuesta del LLM razonador
  → Extraer las contradicciones identificadas
  → Asignar severidad numérica basada en la clasificación

PASO 4: Decisión
  → Si se detecta contradicción crítica: bloquear la respuesta
    y generar alerta
  → Si se detecta contradicción media: inyectar un disclaimer
    en la respuesta al usuario
  → Si no se detecta contradicción: proceder normalmente

LIMITACIÓN FUNDAMENTAL:
  El LLM razonador puede fallar en detectar contradicciones
  implícitas que requieren razonamiento multi-paso.
  La detección de Tipo IV y V tiene un recall < 1.
  Este protocolo es una mejora, no una solución completa.
```

---

## 8. Contramedidas: El Framework de Resolución

### 8.1 Cuarentena Semántica

Cuando el verificador de ingesta detecta una contradicción con severidad superior al umbral de bloqueo, el documento no se indexa. Entra en un estado de **cuarentena semántica**:

```
ESTADOS DE UN DOCUMENTO EN EL PIPELINE DE INGESTA:

  [RECIBIDO] → [VERIFICACIÓN] → ┬→ [INDEXADO] (sin contradicciones)
                                  ├→ [INDEXADO_CON_NOTA] (contradicción menor)
                                  ├→ [REVISIÓN_HUMANA] (contradicción moderada)
                                  └→ [CUARENTENA] (contradicción crítica)
                                  
  [CUARENTENA] → [RESOLUCIÓN] → ┬→ [INDEXADO] (contradicción resuelta)
                                 ├→ [RECHAZADO] (documento descartado)
                                 └→ [REEMPLAZADO] (documento sustituye al existente)
```

El documento en cuarentena no es eliminado. Se almacena en un área separada con metadatos completos: qué contradicción fue detectada, con qué documento existente se contradice, cuál es la severidad, y quién debe resolverla.

### 8.2 Auditoría Ontológica Periódica

La verificación en frontera previene la entrada de nuevas contradicciones, pero no resuelve las que ya existen en la base. Para eso se requiere una **auditoría ontológica periódica**: un proceso sistemático de revisión de la base vectorial que identifica, cuantifica y resuelve las contradicciones acumuladas.

**Protocolo de Auditoría Ontológica:**

```
FRECUENCIA RECOMENDADA:
  - Sistemas con > 1000 documentos: mensual
  - Sistemas con > 5000 documentos: quincenal
  - Sistemas con > 10000 documentos: semanal

FASES DE LA AUDITORÍA:

FASE 1 — Muestreo inteligente:
  No es posible auditar todos los pares de documentos (O(N²)).
  Estrategia de muestreo:
  a) Identificar clusters temáticos mediante clustering de embeddings
     (K-means o HDBSCAN sobre los embeddings de la base)
  b) Dentro de cada cluster, muestrear pares de documentos
     con similitud coseno > 0.8 (alta probabilidad de co-recuperación)
  c) Priorizar pares donde al menos un documento fue indexado
     en los últimos T días (mayor probabilidad de contradicción
     temporal)
  d) Priorizar documentos con alta betweenness centrality
     en el grafo de contradicciones conocido

FASE 2 — Verificación de consistencia:
  Para cada par muestreado:
  a) Extraer afirmaciones factuales de ambos documentos
  b) Aplicar NLI para detectar contradicciones directas
  c) Aplicar razonamiento LLM para detectar contradicciones
     implícitas
  d) Clasificar el tipo de contradicción (I-V)
  e) Asignar severidad

FASE 3 — Resolución:
  Para cada contradicción detectada:
  a) Tipo I (directa): determinar cuál documento es correcto
     (fuentes de autoridad, fecha de publicación, versión)
  b) Tipo II (temporal): aplicar resolución temporal
     (el más reciente prevalece; el anterior se marca como
     obsoleto o se elimina)
  c) Tipo III (granularidad): aplicar resolución jerárquica
     (lo específico prevalece sobre lo general)
  d) Tipo IV (implícita): escalar a revisión humana experta
  e) Tipo V (emergente): escalar a revisión humana experta
     con contexto completo de los documentos involucrados

FASE 4 — Métricas post-auditoría:
  Calcular y registrar:
  - Deuda ontológica antes y después
  - Número de contradicciones detectadas por tipo
  - Número de documentos en cuarentena
  - Presión ontológica global
  - Tendencia respecto a la auditoría anterior

FASE 5 — Reporte:
  Generar un informe de auditoría con:
  - Mapa de calor de contradicciones por cluster temático
  - Top-10 documentos con mayor presión ontológica
  - Top-5 contradicciones de mayor severidad
  - Recomendaciones de acción
```

### 8.3 Índice de Coherencia Temporal

Para las contradicciones de Tipo II (temporales), el mecanismo de resolución más efectivo es el **Índice de Coherencia Temporal**: un metadato asociado a cada documento que registra su vigencia temporal.

```python
@dataclass
class TemporalCoherenceIndex:
    """
    Índice de coherencia temporal para documentos en base vectorial.
    Permite resolver contradicciones de Tipo II automáticamente.
    """
    doc_id: str
    valid_from: datetime       # Fecha desde la cual el documento es válido
    valid_until: datetime | None  # Fecha hasta la cual es válido (None = vigente)
    superseded_by: str | None  # ID del documento que lo reemplaza
    version: int               # Número de versión
    source_authority: str      # Fuente de autoridad que emitió el documento
    
    def is_current(self, query_time: datetime) -> bool:
        """Determina si el documento es vigente en el momento de la consulta."""
        if self.valid_until is not None and query_time > self.valid_until:
            return False
        if self.superseded_by is not None:
            return False
        return True
    
    def resolve_conflict(self, other: 'TemporalCoherenceIndex') -> str:
        """
        Resuelve un conflicto temporal entre dos documentos.
        Retorna el ID del documento que prevalece.
        """
        # El documento más reciente prevalece
        if self.valid_from > other.valid_from:
            return self.doc_id
        elif other.valid_from > self.valid_from:
            return other.doc_id
        else:
            # Misma fecha: prevalece la fuente de mayor autoridad
            authority_rank = self._authority_rank()
            other_rank = other._authority_rank()
            return self.doc_id if authority_rank >= other_rank else other.doc_id
    
    def _authority_rank(self) -> int:
        """Ranking de autoridad de la fuente."""
        ranks = {
            'legal': 5,
            'compliance': 4,
            'executive': 3,
            'departmental': 2,
            'informal': 1
        }
        return ranks.get(self.source_authority, 0)
```

### 8.4 Resolución Asistida de Contradicciones

Para contradicciones de Tipo IV y V que requieren intervención humana, el sistema debe proporcionar al revisor toda la información necesaria para tomar una decisión informada:

```
FORMATO DE REPORTE DE CONTRADICCIÓN PARA REVISIÓN HUMANA:

═══════════════════════════════════════════════════════
ALERTA DE CONTRADICCIÓN — Prioridad: ALTA
═══════════════════════════════════════════════════════

Tipo: IV (Contradicción implícita)
Severidad: 0.82
Detectada en: Auditoría ontológica del 2026-08-15
Cluster temático: Políticas de retención de datos

DOCUMENTO A:
  ID: doc_2026_03_14_042
  Fuente: SharePoint / Legal / Políticas
  Fecha indexación: 2026-03-14
  Afirmación relevante: "El presupuesto anual del 
  departamento de datos es de 2M€"

DOCUMENTO B:
  ID: doc_2026_06_22_118
  Fuente: Confluence / Ingeniería / Planificación
  Fecha indexación: 2026-06-22
  Afirmación relevante: "Se aprueba la contratación de 
  15 data engineers a 120K€/año para el departamento 
  de datos"

DOCUMENTO C:
  ID: doc_2025_11_03_007
  Fuente: SharePoint / Finanzas / Directrices
  Fecha indexación: 2025-11-03
  Afirmación relevante: "Los costes de personal de 
  cualquier departamento no pueden exceder el 70% de 
  su presupuesto operativo"

CONTRADICCIÓN DETECTADA:
  15 × 120.000€ = 1.800.000€ (coste de personal)
  70% × 2.000.000€ = 1.400.000€ (límite de personal)
  → El coste de personal excede el límite en 400.000€

IMPACTO ESTIMADO:
  Consultas afectadas: ~340 consultas/mes sobre 
  presupuesto y contratación del departamento de datos
  Probabilidad de co-recuperación: 0.23

ACCIÓN REQUERIDA:
  □ Confirmar que el presupuesto fue actualizado (invalidar Doc A)
  □ Confirmar que la contratación fue aprobada como excepción
  □ Confirmar que la directriz del 70% fue modificada
  □ Escalar a Finanzas para resolución

RESPONSABLE ASIGNADO: [nombre del revisor]
PLAZO DE RESOLUCIÓN: 5 días hábiles
═══════════════════════════════════════════════════════
```

### 8.5 Monitorización continua de coherencia

Además de las auditorías periódicas, el sistema debe implementar una **monitorización continua** que detecte señales de deuda ontológica creciente entre auditorías:

**Métricas de monitorización continua:**

```
MÉTRICAS DE COHERENCIA EN TIEMPO REAL:

1. Tasa de contradicciones en frontera:
   → Número de documentos bloqueados o flaggeados por semana
   → Tendencia creciente = la base está acumulando deuda
   → Alerta si tasa > 2× media de las últimas 8 semanas

2. Entropía de respuesta para consultas repetidas:
   → Para un conjunto fijo de 50 consultas "canónicas",
     medir la variabilidad de las respuestas semana a semana
   → Aumento de entropía = posible contradicción activada
   → Alerta si entropía > 1.5× baseline

3. Ratio de documentos en cuarentena:
   → Número de documentos en cuarentena / total de documentos
   → Alerta si ratio > 2%

4. Presión ontológica global (muestreada):
   → Calcular sobre un muestreo aleatorio de 500 pares/semana
   → Tendencia creciente = deuda acumulándose
   → Alerta si presión > umbral_calibrado

5. Tasa de invalidación temporal:
   → Número de documentos marcados como obsoletos por semana
   → Tasa muy baja + base creciendo = posible acumulación
     de documentos obsoletos no invalidados
```

---

## 9. Tutorial Práctico: Ejecutando una Auditoría Ontológica

### 9.1 Entorno necesario

- Acceso a la base vectorial (API de consulta)
- Modelo de embeddings documentado (el mismo que usa el sistema)
- Modelo NLI (recomendación: `cross-encoder/nli-deberta-v3-base` o similar)
- Acceso a los logs de consultas de las últimas 4 semanas
- Permisos de lectura sobre todos los documentos de la base
- Entorno de ejecución aislado (no ejecutar la auditoría contra producción)

### 9.2 Paso 1: Establecer la línea base

```python
import numpy as np
from sentence_transformers import SentenceTransformer, CrossEncoder
from typing import List, Tuple
import json
from datetime import datetime

class OntologicalAuditor:
    """
    Auditor ontológico para sistemas RAG.
    Implementa el protocolo de la Sección 8.2.
    """
    def __init__(
        self,
        embed_model_name: str = 'text-embedding-3-large',
        nli_model_name: str = 'cross-encoder/nli-deberta-v3-base',
        k_audit: int = 10,
        sim_threshold: float = 0.75,
        sample_size: int = 2000
    ):
        self.embed_model = SentenceTransformer(embed_model_name)
        self.nli_model = CrossEncoder(nli_model_name)
        self.k_audit = k_audit
        self.sim_threshold = sim_threshold
        self.sample_size = sample_size
    
    def step1_baseline(self, documents: List[dict]) -> dict:
        """
        Paso 1: Establecer línea base de la base vectorial.
        
        Args:
            documents: Lista de dicts con 'id', 'content', 'metadata'
        
        Returns:
            dict con métricas de línea base
        """
        n_docs = len(documents)
        contents = [d['content'] for d in documents]
        
        # Generar embeddings de todos los documentos
        embeddings = self.embed_model.encode(
            contents, 
            show_progress_bar=True,
            normalize_embeddings=True
        )
        
        # Calcular distribución de similitudes
        # (muestreo para bases grandes)
        if n_docs > 5000:
            idx = np.random.choice(n_docs, size=5000, replace=False)
            sample_emb = embeddings[idx]
        else:
            sample_emb = embeddings
        
        # Matriz de similitud (solo triángulo superior)
        n_sample = len(sample_emb)
        sim_matrix = sample_emb @ sample_emb.T
        
        # Extraer triángulo superior
        triu_idx = np.triu_indices(n_sample, k=1)
        similarities = sim_matrix[triu_idx]
        
        # Estadísticas
        baseline = {
            'n_documents': n_docs,
            'n_pairs_sampled': len(similarities),
            'mean_similarity': float(np.mean(similarities)),
            'std_similarity': float(np.std(similarities)),
            'pct_above_threshold': float(
                np.mean(similarities > self.sim_threshold)
            ),
            'estimated_high_sim_pairs': int(
                np.mean(similarities > self.sim_threshold) * 
                (n_docs * (n_docs - 1) / 2)
            ),
            'timestamp': datetime.now().isoformat()
        }
        
        return baseline
```

### 9.3 Paso 2: Muestreo inteligente de pares

```python
    def step2_sample_pairs(
        self, 
        documents: List[dict], 
        embeddings: np.ndarray
    ) -> List[Tuple[int, int]]:
        """
        Paso 2: Muestrear pares de documentos para verificación.
        Estrategia: priorizar pares con alta similitud coseno
        (mayor probabilidad de co-recuperación y de contradicción).
        """
        n_docs = len(documents)
        
        # Estrategia 1: Pares con similitud alta
        # (candidatos a co-recuperación)
        high_sim_pairs = []
        batch_size = 1000
        for i in range(0, n_docs, batch_size):
            batch_emb = embeddings[i:i+batch_size]
            sims = batch_emb @ embeddings.T
            for local_i in range(len(batch_emb)):
                global_i = i + local_i
                # Top-k más similares (excluyendo self)
                top_indices = np.argsort(sims[local_i])[::-1][1:self.k_audit+1]
                for j in top_indices:
                    if sims[local_i, j] > self.sim_threshold:
                        high_sim_pairs.append((global_i, int(j)))
        
        # Estrategia 2: Pares con documentos recientes
        # (mayor probabilidad de contradicción temporal)
        recent_pairs = []
        recent_threshold_days = 90
        now = datetime.now()
        for i, doc in enumerate(documents):
            if 'indexed_at' in doc.get('metadata', {}):
                indexed_at = datetime.fromisoformat(
                    doc['metadata']['indexed_at']
                )
                if (now - indexed_at).days < recent_threshold_days:
                    # Este documento es reciente: compararlo con
                    # sus vecinos más cercanos
                    sims_i = embeddings[i] @ embeddings.T
                    top_neighbors = np.argsort(sims_i)[::-1][1:6]
                    for j in top_neighbors:
                        recent_pairs.append((i, int(j)))
        
        # Combinar y deduplicar
        all_pairs = list(set(high_sim_pairs + recent_pairs))
        
        # Limitar al sample_size
        if len(all_pairs) > self.sample_size:
            indices = np.random.choice(
                len(all_pairs), size=self.sample_size, replace=False
            )
            all_pairs = [all_pairs[i] for i in indices]
        
        return all_pairs
```

### 9.4 Paso 3: Verificación de consistencia

```python
    def step3_verify_pair(
        self, 
        doc_a: dict, 
        doc_b: dict
    ) -> dict:
        """
        Paso 3: Verificar consistencia entre un par de documentos.
        Retorna un dict con el resultado de la verificación.
        """
        # Extraer afirmaciones (simplificado: oraciones con verbos factuales)
        claims_a = self._extract_claims(doc_a['content'])
        claims_b = self._extract_claims(doc_b['content'])
        
        if not claims_a or not claims_b:
            return {
                'status': 'NO_CLAIMS',
                'contradictions': []
            }
        
        contradictions = []
        
        # Comparar cada par de afirmaciones
        for claim_a in claims_a[:15]:  # Limitar para rendimiento
            for claim_b in claims_b[:15]:
                # Verificar similitud semántica entre afirmaciones
                emb_a = self.embed_model.encode([claim_a])[0]
                emb_b = self.embed_model.encode([claim_b])[0]
                sim = float(np.dot(emb_a, emb_b) / (
                    np.linalg.norm(emb_a) * np.linalg.norm(emb_b)
                ))
                
                if sim < 0.5:
                    continue  # Afirmaciones sobre temas diferentes
                
                # NLI: ¿se contradicen?
                nli_score = self.nli_model.predict([(claim_a, claim_b)])
                # nli_score: [contradiction, entailment, neutral]
                contra_prob = float(nli_score[0][0])
                
                if contra_prob > 0.7:
                    contradictions.append({
                        'claim_a': claim_a,
                        'claim_b': claim_b,
                        'doc_a_id': doc_a['id'],
                        'doc_b_id': doc_b['id'],
                        'claim_similarity': sim,
                        'contradiction_probability': contra_prob,
                        'severity': contra_prob,
                        'type': self._classify_contradiction(
                            claim_a, claim_b, doc_a, doc_b
                        )
                    })
        
        return {
            'status': 'CONTRADICTIONS_FOUND' if contradictions else 'CLEAR',
            'contradictions': contradictions,
            'n_claims_a': len(claims_a),
            'n_claims_b': len(claims_b)
        }
    
    def _extract_claims(self, text: str) -> List[str]:
        """Extracción de afirmaciones factuales."""
        sentences = text.replace('\n', '. ').split('. ')
        factual = [
            s.strip() for s in sentences
            if len(s.strip()) > 20 and any(
                kw in s.lower() for kw in [
                    'es', 'son', 'tiene', 'debe', 'puede',
                    'está', 'será', 'fue', 'incluye', 'requiere',
                    'se establece', 'se define', 'el plazo',
                    'la política', 'el procedimiento'
                ]
            )
        ]
        return factual
    
    def _classify_contradiction(
        self, claim_a, claim_b, doc_a, doc_b
    ) -> str:
        """Clasifica el tipo de contradicción (I-V)."""
        # Heurística simplificada:
        # Si los documentos tienen fechas muy diferentes → Tipo II
        date_a = doc_a.get('metadata', {}).get('indexed_at', '')
        date_b = doc_b.get('metadata', {}).get('indexed_at', '')
        if date_a and date_b:
            try:
                d_a = datetime.fromisoformat(date_a)
                d_b = datetime.fromisoformat(date_b)
                if abs((d_a - d_b).days) > 180:
                    return 'TYPE_II_TEMPORAL'
            except:
                pass
        
        # Si las afirmaciones contienen números diferentes → Tipo I
        import re
        nums_a = re.findall(r'\d+', claim_a)
        nums_b = re.findall(r'\d+', claim_b)
        if nums_a and nums_b and nums_a != nums_b:
            return 'TYPE_I_DIRECT'
        
        # Default: Tipo IV (implícita)
        return 'TYPE_IV_IMPLICIT'
```

### 9.5 Paso 4: Generación del informe de auditoría

```python
    def generate_report(
        self, 
        baseline: dict, 
        verification_results: List[dict],
        graph: ContradictionGraph
    ) -> str:
        """Genera el informe de auditoría ontológica."""
        
        total_contradictions = sum(
            len(r['contradictions']) for r in verification_results
        )
        clear_pairs = sum(
            1 for r in verification_results if r['status'] == 'CLEAR'
        )
        contra_pairs = sum(
            1 for r in verification_results 
            if r['status'] == 'CONTRADICTIONS_FOUND'
        )
        
        # Clasificar por tipo
        type_counts = {'TYPE_I_DIRECT': 0, 'TYPE_II_TEMPORAL': 0,
                       'TYPE_III_GRANULARITY': 0, 'TYPE_IV_IMPLICIT': 0,
                       'TYPE_V_EMERGENT': 0}
        severities = []
        for r in verification_results:
            for c in r['contradictions']:
                ctype = c.get('type', 'TYPE_IV_IMPLICIT')
                type_counts[ctype] = type_counts.get(ctype, 0) + 1
                severities.append(c['severity'])
        
        report = f"""
═══════════════════════════════════════════════════════════════
INFORME DE AUDITORÍA ONTOLÓGICA
Fecha: {datetime.now().strftime('%Y-%m-%d %H:%M')}
═══════════════════════════════════════════════════════════════

1. LÍNEA BASE
   Documentos en base: {baseline['n_documents']}
   Pares muestreados: {baseline['n_pairs_sampled']}
   Similitud media entre documentos: {baseline['mean_similarity']:.4f}
   Pares con similitud > {self.sim_threshold}: {baseline['estimated_high_sim_pairs']}

2. RESULTADOS DE VERIFICACIÓN
   Pares verificados: {len(verification_results)}
   Pares sin contradicción: {clear_pairs} ({100*clear_pairs/len(verification_results):.1f}%)
   Pares con contradicción: {contra_pairs} ({100*contra_pairs/len(verification_results):.1f}%)
   Contradicciones totales detectadas: {total_contradictions}

3. DISTRIBUCIÓN POR TIPO
   Tipo I (Directa):        {type_counts['TYPE_I_DIRECT']}
   Tipo II (Temporal):      {type_counts['TYPE_II_TEMPORAL']}
   Tipo III (Granularidad): {type_counts['TYPE_III_GRANULARITY']}
   Tipo IV (Implícita):     {type_counts['TYPE_IV_IMPLICIT']}
   Tipo V (Emergente):      {type_counts['TYPE_V_EMERGENT']}

4. MÉTRICAS DE DEUDA ONTOLÓGICA
   Deuda ontológica total: {graph.ontological_debt():.4f}
   Presión ontológica global: {graph.global_pressure():.4f}
   Severidad media: {np.mean(severities):.4f} (si severities else 'N/A')
   Severidad máxima: {max(severities):.4f} (si severities else 'N/A')
   Componentes conexos de contradicción: {len(graph.connected_components())}
   Mayor componente conexo: {max(len(c) for c in graph.connected_components()) if graph.connected_components() else 0} documentos

5. EVALUACIÓN DE RIESGO
   Umbral de colapso estimado: {self._estimate_critical_threshold(baseline)}
   Estado actual: {'⚠️ CRÍTICO' if graph.ontological_debt() > self._estimate_critical_threshold(baseline) else '✅ CONTROLADO'}

6. RECOMENDACIONES
   {self._generate_recommendations(type_counts, severities, graph)}

═══════════════════════════════════════════════════════════════
"""
        return report
    
    def _estimate_critical_threshold(self, baseline: dict) -> float:
        """Estima el umbral de colapso funcional."""
        # Heurística: proporcional al número de documentos
        # y al tamaño del top-k
        n = baseline['n_documents']
        return 0.02 * n * self.k_audit
    
    def _generate_recommendations(
        self, type_counts, severities, graph
    ) -> str:
        """Genera recomendaciones basadas en los hallazgos."""
        recs = []
        if type_counts['TYPE_II_TEMPORAL'] > 10:
            recs.append(
                "→ Implementar Índice de Coherencia Temporal. "
                "Se detectaron múltiples contradicciones temporales "
                "que indican documentos obsoletos no invalidados."
            )
        if type_counts['TYPE_I_DIRECT'] > 5:
            recs.append(
                "→ Resolver contradicciones directas de manera "
                "inmediata. Son las de mayor impacto en la coherencia "
                "de las respuestas."
            )
        if len(graph.connected_components()) > 3:
            recs.append(
                "→ Se detectaron múltiples clusters de contradicción. "
                "Recomendación: auditoría profunda por cluster temático."
            )
        if not recs:
            recs.append(
                "→ El sistema está dentro de parámetros aceptables. "
                "Mantener la frecuencia de auditoría actual."
            )
        return '\n   '.join(recs)
```

### 9.6 Paso 5: Ejecución completa

```python
def run_full_audit(
    documents: List[dict],
    embed_model_name: str = 'text-embedding-3-large',
    nli_model_name: str = 'cross-encoder/nli-deberta-v3-base'
) -> str:
    """
    Ejecuta una auditoría ontológica completa.
    
    Args:
        documents: Lista de documentos con 'id', 'content', 'metadata'
    
    Returns:
        Informe de auditoría en formato texto
    """
    auditor = OntologicalAuditor(
        embed_model_name=embed_model_name,
        nli_model_name=nli_model_name
    )
    
    # Paso 1: Línea base
    print("[1/5] Estableciendo línea base...")
    baseline = auditor.step1_baseline(documents)
    
    # Generar embeddings completos
    contents = [d['content'] for d in documents]
    embeddings = auditor.embed_model.encode(
        contents, normalize_embeddings=True, show_progress_bar=True
    )
    
    # Paso 2: Muestreo de pares
    print("[2/5] Muestreando pares de documentos...")
    pairs = auditor.step2_sample_pairs(documents, embeddings)
    print(f"  → {len(pairs)} pares seleccionados para verificación")
    
    # Paso 3: Verificación de consistencia
    print("[3/5] Verificando consistencia...")
    results = []
    graph = ContradictionGraph(len(documents))
    
    for idx, (i, j) in enumerate(pairs):
        if idx % 100 == 0:
            print(f"  → Par {idx}/{len(pairs)}")
        result = auditor.step3_verify_pair(documents[i], documents[j])
        results.append(result)
        
        # Añadir contradicciones al grafo
        for contra in result['contradictions']:
            graph.add_contradiction(
                i=j, j=j,
                severity=contra['severity'],
                co_prob=0.5,  # Estimación por defecto
                ctype=int(contra.get('type', 'TYPE_IV_IMPLICIT')[-1]),
                desc=f"{contra['claim_a'][:50]} vs {contra['claim_b'][:50]}"
            )
    
    # Paso 4: Generar informe
    print("[4/5] Generando informe...")
    report = auditor.generate_report(baseline, results, graph)
    
    # Paso 5: Guardar
    print("[5/5] Guardando resultados...")
    with open(f"ontological_audit_{datetime.now().strftime('%Y%m%d')}.json", 'w') as f:
        json.dump({
            'baseline': baseline,
            'n_contradictions': sum(len(r['contradictions']) for r in results),
            'ontological_debt': graph.ontological_debt(),
            'global_pressure': graph.global_pressure(),
        }, f, indent=2, default=str)
    
    return report


# === EJECUCIÓN ===
# documents = load_documents_from_vector_store(...)
# report = run_full_audit(documents)
# print(report)
```

---

## 10. Discusión: La Ética de la Coherencia y el Coste de la Inacción

### 10.1 El deber de monitorizar la coherencia

Un sistema RAG que produce respuestas incoherentes no está "funcionando mal" en ningún sentido técnico que los dashboards estándar puedan detectar. El modelo de lenguaje no ha fallado. El modelo de embeddings no ha fallado. El pipeline de recuperación no ha fallado. La infraestructura no ha fallado.

Y sin embargo, el sistema produce respuestas que se contradicen entre sí a lo largo del tiempo. Un usuario que pregunta "¿cuál es la política de retención de datos?" en enero recibe "90 días". El mismo usuario que pregunta lo mismo en junio recibe "30 días". Ninguna de las dos respuestas es un "error" en el sentido de que el sistema no produjo una excepción. Pero la experiencia del usuario es la de un sistema que no sabe lo que dice.

El operador de un sistema RAG tiene un deber de monitorización de la coherencia que va más allá de la monitorización de la disponibilidad y la latencia. La coherencia semántica es una propiedad de calidad del sistema tan fundamental como la precisión o la relevancia, y su degradación tiene consecuencias operativas reales: erosión de la confianza del usuario, decisiones de negocio basadas en información contradictoria, y riesgo de compliance cuando las contradicciones afectan a información regulatoria.

### 10.2 La asimetría entre el coste de prevenir y el coste de resolver

La deuda ontológica tiene la misma propiedad económica que la deuda técnica: el coste de resolverla crece con el tiempo. Un documento contradictorio detectado en el momento de la ingesta cuesta $O(k)$ operaciones de verificación. El mismo documento detectado seis meses después, cuando ya ha sido recuperado 500 veces y ha contaminado 200 respuestas, cuesta una auditoría de impacto, una comunicación a los usuarios afectados, y posiblemente la corrección de decisiones de negocio tomadas sobre la base de respuestas incorrectas.

La ratio entre el coste de prevención y el coste de resolución es, en nuestra experiencia, del orden de 1:50 a 1:200. Prevenir es entre 50 y 200 veces más barato que resolver.

### 10.3 La responsabilidad del operador

Un sistema RAG no es un oráculo. Es un sistema de recuperación de información aumentado con generación de lenguaje natural. El operador del sistema es responsable de la calidad de la información que el sistema recupera, no solo de la calidad del modelo que la presenta.

Esto implica que el operador tiene la responsabilidad de:
1. Implementar verificación de consistencia en el pipeline de ingesta.
2. Ejecutar auditorías ontológicas periódicas.
3. Mantener un registro de las contradicciones detectadas y su resolución.
4. Monitorizar la coherencia longitudinal de las respuestas.
5. Informar a los usuarios cuando se detecta una contradicción que puede haber afectado respuestas previas.

La ausencia de cualquiera de estos cinco mecanismos constituye una negligencia operativa que, en el momento en que produce un daño cuantificable (una decisión de negocio incorrecta, una violación de compliance, una pérdida de confianza del cliente), se convierte en una responsabilidad legal y reputacional.

### 10.4 El límite de la automatización

La detección de contradicciones de Tipo IV y V (implícitas y emergentes) tiene un límite fundamental: requiere razonamiento inferencial que ningún modelo NLI actual puede realizar con recall completo. La automatización puede detectar el 60-80% de las contradicciones de Tipo I y II, el 30-50% de las de Tipo III, y menos del 20% de las de Tipo IV y V.

Esto no es un argumento contra la automatización. Es un argumento a favor de la combinación de automatización y juicio humano. La automatización detecta las contradicciones obvias y reduce el volumen que requiere intervención humana. El juicio humano resuelve las contradicciones que requieren comprensión del contexto, la jerarquía normativa, y la intención del autor.

El sistema que confía exclusivamente en la automatización para la detección de contradicciones tiene una falsa sensación de seguridad. El sistema que confía exclusivamente en el juicio humano no escala. La combinación de ambos es la única arquitectura viable.

---

## 11. Conclusión

Este paper ha formalizado, cuantificado y proporcionado herramientas de intervención para una patología de los sistemas RAG que, hasta donde alcanza nuestra revisión de la literatura, no había sido descrita con este nivel de precisión: la acumulación endógena de contradicciones semánticas en bases vectoriales, que denominamos **deuda ontológica**.

Las contribuciones técnicas son:

1. **La definición formal de deuda ontológica** como función de la severidad de las contradicciones ponderada por la probabilidad de co-recuperación, con demostración de crecimiento superlineal (cuadrático) en ausencia de mecanismos de verificación.

2. **La taxonomía de cinco tipos de contradicción** (directa, temporal, de granularidad, implícita, emergente) con caracterización de severidad, frecuencia relativa y dificultad de detección.

3. **El modelo de grafo de contradicciones** con las métricas de presión ontológica local y global, betweenness centrality como indicador de documentos críticos, y la dinámica de percolación que describe la formación del componente conexo gigante.

4. **El teorema del efecto iceberg** que demuestra que la evaluación puntual detecta una fracción decreciente de las contradicciones totales, tendiendo a cero con el crecimiento de la base.

5. **El algoritmo de verificación de consistencia cruzada** sobre el top-k recuperado, con análisis de complejidad y optimización mediante filtrado por similitud semántica.

6. **El protocolo de auditoría ontológica periódica** con muestreo inteligente, verificación NLI, clasificación de contradicciones, y generación de informes accionables.

7. **El framework de Cuarentena Semántica** con estados de documento, umbrales de intervención, y el Índice de Coherencia Temporal para resolución automática de contradicciones de Tipo II.

La tesis final es simple y no admite matización: **un sistema RAG que no verifica la consistencia lógica de sus documentos en el momento de la ingesta, y que no audita periódicamente la coherencia de su base vectorial, está acumulando una deuda que crecerá hasta el colapso funcional.** El colapso no será súbito. No habrá un error en los logs. No habrá una alerta en el dashboard. Habrá un usuario que pregunte algo y reciba una respuesta que contradice la respuesta que recibió la semana pasada. Y luego otro usuario. Y luego otro. Y la confianza se erosionará sin que nadie pueda señalar el momento exacto en que el sistema dejó de ser fiable.

La deuda ontológica no se ve venir porque no produce un síntoma agudo. Produce una degradación crónica.

El primer paso es nombrarla. El segundo es medirla. El tercero es pagarla.

No hay cuarto paso para quien ignora los tres primeros. Solo hay un sistema que responde cosas diferentes a la misma pregunta, y un equipo que no entiende por qué.

---

## Koans del Auditor Ontológico

Colección para uso en sesiones de arquitectura de datos, post-mortems de incidentes de coherencia, y recordatorios de escritorio.

**De la similitud coseno:**
Dos documentos pueden estar a 0.97 cosenos de distancia y decir exactamente lo contrario. La similitud mide de qué hablan. No mide qué dicen. El sistema que confía en la similitud para garantizar la coherencia es el sistema que confía en que dos personas que hablan del mismo tema están de acuerdo.

**Del efecto iceberg:**
Mil consultas de evaluación detectan cien contradicciones. La base tiene doscientas cincuenta mil. No es que el sistema esté bien. Es que el sistema es grande y tu evaluación es pequeña. La ausencia de evidencia no es evidencia de ausencia. Es evidencia de que no has mirado suficiente.

**De la deuda que no se ve:**
El documento que envenenó tu RAG no tiene contenido malicioso. No tiene un prompt inyectado. No tiene un embedding adversarial. Tiene una fecha de publicación de 2024 y una política que cambió en 2026. Es un documento perfectamente legítimo que dice algo que era verdad y ya no lo es. Eso es todo lo que necesita ser.

**Del crecimiento superlineal:**
Indexas cien documentos al mes. En enero tienes cien. En junio tienes seiscientos. Las contradicciones no crecen de cien a seiscientas. Crecen de cuatro mil novecientos cincuenta pares a ciento setenta y nueve mil setecientos pares. La deuda no es lineal. La deuda es combinatoria. Y tú sigues pensando en lineal.

**De la cuarentena:**
El documento bloqueado en cuarentena no es un enemigo. Es un mensajero. Te dice: "Antes de meterme en tu base, pregúntate si lo que digo es compatible con lo que ya tienes." El sistema que no tiene cuarentena no tiene sistema inmune. Tiene una puerta abierta.

**Del grafo de contradicciones:**
Un documento con alta betweenness no es el documento más contradictorio. Es el documento que conecta contradicciones que de otra manera estarían aisladas. Eliminarlo no resuelve las contradicciones. Pero desconecta los clusters. Y un cluster desconectado es un cluster que no se activa simultáneamente. A veces la intervención no es resolver. Es separar.

**De la contradicción temporal:**
El documento de 2024 no miente. El documento de 2026 no miente. Los dos dicen la verdad. Pero tu sistema RAG no tiene un reloj. Para él, los dos documentos son igualmente presentes, igualmente válidos, igualmente recuperables. Tu sistema vive en un eterno presente donde todas las versiones de la verdad coexisten. Y tú te preguntas por qué responde cosas diferentes.

**De la evaluación longitudinal:**
El test que ejecutas hoy dice que el sistema funciona. El mismo test ejecutado hace tres meses dijo que el sistema funcionaba. Las dos respuestas son ciertas. Las dos respuestas son diferentes. Ninguna de las dos es un error. El sistema no falló. El sistema cambió. Y nadie comparó las dos respuestas porque nadie pensó que había que compararlas.

**Del coste de no pagar:**
La deuda ontológica no se paga sola. Se acumula. Y el interés es compuesto. Cada documento nuevo que indexas sobre una base contradictoria no añade una contradicción. Añade una contradicción con cada documento existente con el que es incompatible. El interés de la deuda ontológica se calcula en pares. Y los pares crecen como el cuadrado del número de documentos.

**Del deber del operador:**
No es culpa del modelo de lenguaje que dos documentos se contradigan. No es culpa del modelo de embeddings que la similitud coseno no distinga relevancia de consistencia. No es culpa del pipeline de ingesta que indexe lo que le envían. Es responsabilidad del operador que diseñó el sistema sin un mecanismo de verificación de coherencia. El sistema hace exactamente lo que fue diseñado para hacer. Fue diseñado sin pensar en esto.

**Del umbral de colapso:**
El colapso no es un evento. No hay un día en que el sistema "se rompe". Hay un día en que un usuario pregunta algo y recibe una respuesta que contradice lo que le dijeron la semana pasada. Y ese usuario no abre un ticket. Simplemente deja de confiar. Y luego otro usuario. Y luego otro. El colapso no produce un error. Produce silencio. El silencio de los usuarios que dejaron de preguntar porque aprendieron que las respuestas no son fiables.

**De la auditoría como acto de soberanía:**
Auditar la coherencia de tu base vectorial no es un ejercicio de compliance. Es un acto de soberanía cognitiva. Es decir: "Yo decido qué es verdad en mi sistema. No lo decide el último documento que alguien subió a SharePoint sin verificar si contradice lo que ya estaba ahí." El sistema que no se audita es el sistema cuya verdad la decide el azar de la ingesta.

---

## Referencias

### Papers académicos y técnicos

Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W. T., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks. *NeurIPS 2020*. arXiv:2005.11401.

Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). Attention is All You Need. *NeurIPS 2017*. arXiv:1706.03762.

Cunningham, W. (1992). The WyCash Portfolio Management System. *OOPSLA '92 Experience Report*. ACM.

Shannon, C. E. (1948). A Mathematical Theory of Communication. *Bell System Technical Journal*, 27(3), 379–423.

Cover, T. M., & Thomas, J. A. (2006). *Elements of Information Theory* (2nd ed.). Wiley-Interscience.

Greshake, K., Abdelnabi, S., Mishra, S., Endres, C., Holz, T., & Fritz, M. (2023). Not What You've Signed Up For: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection. *AISec 2023*. arXiv:2302.12173.

Carlini, N., Tramèr, F., Wallace, E., Jagielski, M., Herbert-Voss, A., Lee, K., Roberts, A., Brown, T., Song, D., Erlingsson, Ú., Oprea, A., & Raffel, C. (2021). Extracting Training Data from Large Language Models. *USENIX Security 2021*. arXiv:2012.07805.

Goldblum, M., Tsipras, D., Xie, C., Chen, X., Schwarzschild, A., Song, D., Madry, A., Li, B., & Goldstein, T. (2022). Dataset Security for Machine Learning: Data Poisoning, Backdoor Attacks, and Defenses. *IEEE TPAMI*. arXiv:2012.10544.

Karpukhin, V., Oğuz, B., Min, S., Lewis, P., Wu, L., Edunov, S., Chen, D., & Yih, W. T. (2020). Dense Passage Retrieval for Open-Domain Question Answering. *EMNLP 2020*. arXiv:2004.04906.

Reimers, N., & Gurevych, I. (2019). Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks. *EMNLP 2019*. arXiv:1908.10084.

Yin, W., Schütze, H., Xiang, B., & Zhou, B. (2016). ABCNN: Attention-Based Convolutional Neural Network for Modeling Sentence Pairs. *TACL*, 4, 259–272.

Bowman, S. R., Angeli, G., Potts, C., & Manning, C. D. (2015). A large annotated corpus for learning natural language inference. *EMNLP 2015*. arXiv:1508.05326.

Williams, A., Nangia, N., & Bowman, S. R. (2018). A Broad-Coverage Challenge Corpus for Sentence Understanding through Inference. *NAACL 2018*. arXiv:1704.05426.

Brandes, U. (2001). A faster algorithm for betweenness centrality. *Journal of Mathematical Sociology*, 25(2), 163–177.

Newman, M. E. J. (2010). *Networks: An Introduction*. Oxford University Press.

Stauffer, D., & Aharony, A. (1994). *Introduction to Percolation Theory* (2nd ed.). Taylor & Francis.

Hopp, W. J., & Spearman, M. L. (2021). The Theory of Constraints at 35. *Production and Operations Management*, 30(9), 2969–2983. DOI: 10.1111/poms.13394.

Van der Aalst, W. M. P. (2016). *Process Mining: Data Science in Action* (2nd ed.). Springer. DOI: 10.1007/978-3-662-49851-4.

Browning, T. R. (2016). On the alignment of the purposes of a process and its participants. *Production and Operations Management*, 25(5), 860–880. DOI: 10.1111/poms.12618.

Davenport, T. H., & Ronanki, R. (2018). Artificial intelligence for the real world. *Harvard Business Review*, 96(1), 108–116.

Agrawal, A., Gans, J., & Goldfarb, A. (2018). *Prediction Machines: The Simple Economics of Artificial Intelligence*. Harvard Business Review Press.

Teece, D. J. (2007). Explicating dynamic capabilities. *Strategic Management Journal*, 28(13), 1319–1350. DOI: 10.1002/smj.640.

Rahwan, I., et al. (2019). Machine behaviour. *Nature*, 568(7753), 477–486. DOI: 10.1038/s41586-019-1138-y.

Ester, M., Kriegel, H.-P., Sander, J., & Xu, X. (1996). A density-based algorithm for discovering clusters in large spatial databases with noise. *KDD '96*, 226–231.

Johnson, J., Douze, M., & Jégou, H. (2019). Billion-scale similarity search with GPUs. *IEEE Transactions on Big Data*, 7(3), 535–547.

Malkov, Y. A., & Yashunin, D. A. (2020). Efficient and robust approximate nearest neighbor search using Hierarchical Navigable Small World graphs. *IEEE TPAMI*, 42(4), 824–836.

### Referencias de trabajos previos del autor

Ferrandez Canalis, D. (2026a). Cantando al Silicio: Una Teoría Unificada de la Ingeniería de Prompts y la Arquitectura Tonal Dwemer. Agencia RONIN. DOI: 10.1310/ronin-tonal-prompting-2026.

Ferrandez Canalis, D. (2026b). Nirn Atacada: Tratado de Seguridad Ofensiva en Sistemas de IA e Infraestructura Distribuida. Agencia RONIN. DOI: 10.1310/ronin-nirn-atacada-2026.

Ferrandez Canalis, D. (2026c). Auditoría de Cuellos de Botella en la Era de la IA: Método Ronin y Síntesis de Alto Impacto. Agencia RONIN.

Ferrandez Canalis, D. (2026d). Corpus Técnico RONIN v1.0: Unificación de Tres Tratados. Agencia RONIN.

---

*Fin del paper. Versión 1.0 — Edición Fundacional, Máxima Densidad.*

*DOI: 10.1310/ronin-ontological-debt-2026*

*Obra de la Agencia RONIN.*

*Licencia: CC BY-NC-SA 4.0 + Cláusula Comercial Ronin. Para usos comerciales, contactar. *

*1310.*
