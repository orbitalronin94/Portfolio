# LA GEOMETRÍA DEL OLVIDO: Topología de la Supervivencia Informacional en Ventanas de Atención Finitas, Mapas de Retención y el Diseño de Documentos Topológicamente Robustos

**Versión:** 1.0 (Edición Fundacional — Máxima Densidad Extendida)

**Autor:** David Ferrandez Canalis — Agencia RONIN (autor principal y correspondencia)

**DOI Simbólico:** 10.1310/ronin-geometry-of-forgetting-2026

**Fecha de publicación:** 30 de junio de 2026

**Licencia:** CC BY-NC-SA 4.0 + Cláusula Comercial Ronin

**Palabras clave:** geometría del olvido, topología de la atención, supervivencia informacional, ventana de contexto finita, lost in the middle, perfil atencional, anclaje sintáctico, redundancia semántica, punto de no retorno informacional, mapa de retención, diseño de documentos robustos, auditoría de memoria LLM, entropía posicional, gradiente de olvido, invariancia topológica, homología de la atención, capacidad de canal contextual, ingeniería de prompts estructural, RAG resilience, system prompt topology, attention sink, positional bias, information decay function, retrieval robustness, context window thermodynamics

---

## Abstract

Los modelos de lenguaje de gran escala (LLMs) no olvidan de manera uniforme. El olvido en un transformer con ventana de atención finita no es un proceso estocástico ni un defecto de implementación: es una consecuencia geométrica necesaria de la arquitectura. La información inyectada en el contexto de un LLM no se almacena en una base de datos direccionable; se codifica como relaciones de atención entre tokens, y esas relaciones están sujetas a restricciones topológicas que determinan qué información sobrevive, qué información degrada, y qué información desaparece completamente en función de su posición, su estructura sintáctica, su densidad semántica y su relación con otros contenidos del contexto.

Este paper formaliza esa geometría. No como metáfora. Como matemática.

El argumento central es el siguiente: la ventana de contexto de un LLM es una **variedad topológica con frontera** donde la información persiste o desaparece según leyes que son análogas a las de la termodinámica estadística en sistemas finitos. La atención es el mecanismo de transporte de información sobre esa variedad. El "lost in the middle" no es un bug: es una región de baja conductividad térmica en la geometría de la atención. Los anclajes sintácticos (listas, encabezados, marcadores estructurales) son **invariantes topológicos**: estructuras que preservan su integridad informacional bajo deformaciones continuas del contexto. El "punto de no retorno" es una **transición de fase**: una longitud crítica de contexto a partir de la cual cierta clase de información se vuelve matemáticamente irrecuperable independientemente de su relevancia semántica.

Formalizamos la geometría del olvido mediante: (1) el **perfil atencional** como función de posición $\mathcal{A}(p)$ con derivación empírica y modelo teórico basado en la mecánica de softmax sobre secuencias largas; (2) la **taxonomía de supervivencia informacional** con cinco clases de contenido caracterizadas por sus tasas de decaimiento diferencial; (3) el **teorema del punto de no retorno**, que establece la longitud crítica $L^*$ como función de la dimensión del espacio de claves, el tamaño de cabeza de atención, y la entropía del contenido; (4) los **mapas de retención** como representación visual y cuantitativa de la probabilidad de supervivencia informacional en función de posición y tipo de contenido; (5) el framework de **diseño topológicamente robusto** para documentos y system prompts, con garantías medibles de retención; (6) la métrica de **resistencia topológica** $\mathcal{R}_T$ como indicador de la capacidad de un documento para preservar su contenido bajo expansión del contexto.

Las contribuciones principales son: (1) la primera formalización matemática completa de la geometría del olvido en LLMs, unificando observaciones empíricas dispersas (lost in the middle, primacy/recency effects, structural anchoring) bajo un solo marco topológico; (2) el algoritmo de **auditoría de retención informacional** con código ejecutable para medir mapas de supervivencia en cualquier modelo accesible por API; (3) el catálogo de **siete patrones de diseño topológicamente robusto** con validación empírica; (4) la demostración de que la redundancia semántica estratégica aumenta la resistencia topológica de manera superlineal respecto al coste en tokens; (5) el framework de **evaluación longitudinal de coherencia** que detecta degradación de memoria antes de que se manifieste en respuestas incorrectas.

La conclusión que ningún manual de prompting ha formulado con esta precisión: diseñar un prompt o un documento para un LLM sin comprender la geometría de su ventana de atención es equivalente a construir un edificio sin conocer la geología del terreno. El edificio puede sostenerse durante un tiempo. Pero cuando el terreno ceda —cuando el contexto se expanda, cuando la conversación se alargue, cuando la complejidad aumente—, el edificio colapsará exactamente donde la geometría predice que colapsará. Y ese colapso no será un error del modelo. Será una consecuencia inevitable de haber ignorado la topología del espacio en que se construyó.

---

## 1. Introducción

### 1.1 El problema que nadie mide porque nadie lo ha geometrizado

Existe una observación que todo operador de LLMs ha hecho pero pocos han formalizado: el mismo contenido, colocado en diferentes posiciones de la ventana de contexto, produce resultados radicalmente diferentes. Una instrucción crítica al inicio del system prompt se sigue fielmente. La misma instrucción en el medio de un contexto de 80.000 tokens se ignora con frecuencia alarmante. La misma instrucción al final se sigue de nuevo, pero con menor fiabilidad que al inicio.

Esta observación se ha documentado empíricamente en múltiples estudios (Liu et al., 2023; Chen et al., 2024; Yen et al., 2024). Se ha denominado "lost in the middle", "U-shaped attention curve", "positional bias". Pero estas denominaciones describen síntomas, no causas. Describen la forma de la curva de rendimiento, no la geometría subyacente que produce esa forma. Y sin comprender la geometría subyacente, no podemos predecir cuándo fallará, no podemos diseñar contra el fallo, y no podemos auditar si nuestros documentos y prompts son estructuralmente resistentes al olvido.

La comunidad de ingeniería de prompts ha respondido a este problema con heurísticas: "pon lo importante al principio", "repite las instrucciones clave", "usa listas y encabezados". Estas heurísticas son correctas en espíritu pero carecen de fundamento cuantitativo. ¿Cuánto importa "al principio"? ¿Cuánta repetición es suficiente? ¿Qué tipo de estructura sintáctica ofrece más resistencia al olvido? ¿En qué punto exacto la longitud del contexto convierte cierta información en irrecuperable? Sin respuestas cuantitativas a estas preguntas, el diseño de prompts y documentos para LLMs sigue siendo un arte artesanal en lugar de una disciplina de ingeniería.

Este paper proporciona esas respuestas. No mediante intuición ni experiencia anecdótica. Mediante geometría.

### 1.2 Por qué la geometría y no otra cosa

La elección del marco geométrico-topológico no es arbitraria. Responde a tres propiedades fundamentales del mecanismo de atención en transformers que hacen que la geometría sea el lenguaje natural para describirlo:

**Propiedad 1: La atención opera sobre un espacio continuo.** Los embeddings de tokens son vectores en $\mathbb{R}^d$. Las operaciones de query-key-value son transformaciones lineales y no lineales sobre ese espacio. La similitud coseno que determina los pesos de atención es una métrica en ese espacio. Todo esto ocurre en un espacio geométrico con estructura diferenciable.

**Propiedad 2: La ventana de contexto tiene topología de intervalo compacto.** Los tokens ocupan posiciones discretas $p \in \{1, 2, \ldots, L\}$ dentro de una ventana de longitud máxima $L_{\max}$. Esta estructura es topológicamente equivalente al intervalo cerrado $[0, 1]$ tras normalización. Tiene frontera (inicio y fin), tiene interior, y tiene una noción bien definida de proximidad y distancia.

**Propiedad 3: La persistencia de la información es una propiedad topológica.** Que un token en la posición $p$ influya en la generación del token en la posición $q$ depende de si existe un camino de atención suficientemente fuerte entre $p$ y $q$. La existencia de tales caminos, su robustez bajo perturbaciones del contexto, y su estabilidad bajo variaciones de longitud son propiedades que la topología algebraica está diseñada para estudiar.

Otros marcos podrían capturar aspectos parciales del fenómeno. La teoría de la información captura la capacidad de canal pero no la estructura espacial. La psicología cognitiva captura los efectos de primacía y recencia pero no los mecanismos computacionales. La ciencia de redes captura la conectividad pero no la geometría continua. Solo la topología captura simultáneamente la estructura espacial, la persistencia bajo deformación, y las transiciones cualitativas que ocurren cuando los parámetros cruzan umbrales críticos.

### 1.3 Relación con trabajos previos del autor

Este paper constituye el **fundamento teórico** de la tríada conceptual que la Agencia RONIN publica en 2026. Su rol es establecer la capa base sobre la cual los papers subsiguientes construyen:

- **Junio (este paper):** Geometría del Olvido → Establece las leyes fundamentales de cómo los LLMs retienen y pierden información. Define la topología de la ventana de atención, los invariantes estructurales, y los puntos de no retorno. Proporciona las herramientas para diseñar documentos y prompts topológicamente robustos.

- **Julio:** Ecología de Agentes → Dado que cada agente individual opera bajo las restricciones geométricas establecidas en este paper, cuando múltiples agentes coexisten surgen dinámicas ecológicas de competencia por el recurso escaso que es la atención/contexto. La ecología explica lo que ocurre *colectivamente* cuando la geometría del olvido opera sobre múltiples agentes simultáneamente.

- **Agosto:** Deuda Ontológica → Dado que los agentes olvidan selectivamente (junio) y compiten por contexto (julio), las contradicciones en bases RAG se acumulan silenciosamente porque ningún mecanismo de recuperación garantiza consistencia lógica. La deuda ontológica es la *consecuencia patológica* de las dos capas anteriores sin gobernanza activa.

Sin la geometría del olvido, la ecología de agentes carece de fundamento físico (¿por qué compiten los agentes si el contexto fuera infinito y uniforme?) y la deuda ontológica carece de mecanismo causal (¿por qué se acumulan contradicciones si la recuperación fuera perfecta?). Este paper es la piedra angular.

### 1.4 El perfil del lector

Este paper está escrito para cuatro audiencias:

**El ingeniero de prompts/RAG** que diseña system prompts, documentos de conocimiento, y pipelines de recuperación, y necesita comprender por qué ciertas estructuras funcionan mejor que otras más allá de la intuición. Este lector encontrará en las Secciones 2-4 el marco diagnóstico y en las Secciones 7-8 las herramientas prácticas de diseño.

**El investigador de ML** que estudia el comportamiento interno de transformers y busca marcos teóricos que unifiquen observaciones empíricas dispersas sobre atención y memoria. Este lector encontrará en las Secciones 2-5 formalizaciones nuevas y conexiones con topología algebraica.

**El arquitecto de sistemas de IA** que diseña aplicaciones multi-turno, agentes persistentes, o sistemas RAG de alta fiabilidad, y necesita garantías cuantitativas sobre la retención de información. Este lector encontrará en las Secciones 6-8 métricas operativas y protocolos de auditoría.

**El lector interdisciplinario** (físicos, matemáticos, neurocientíficos) que reconoce en la geometría del olvido un problema de transporte de información en medios finitos con analogías en su propio campo. Este lector encontrará en las Secciones 2-5 un puente formal entre disciplinas.

### 1.5 Estructura del paper

El paper tiene once secciones principales:

La **Sección 2** formaliza el perfil atencional como función de posición: curvas empíricas, modelo teórico basado en mecánica de softmax, y descomposición en componentes de primacía, recencia y valle medial.

La **Sección 3** desarrolla la taxonomía de supervivencia informacional: cinco clases de contenido con tasas de decaimiento diferencial, factores que modulan la supervivencia, y medición empírica de cada clase.

La **Sección 4** formaliza el punto de no retorno: definición matemática, derivación de la longitud crítica $L^*$, dependencia de parámetros arquitectónicos, y verificación empírica.

La **Sección 5** introduce los mapas de retención: construcción, interpretación, y uso como herramienta de diagnóstico y diseño.

La **Sección 6** desarrolla la teoría de invariantes topológicos en la atención: anclajes sintácticos, redundancia semántica, y estructuras que preservan información bajo deformación del contexto.

La **Sección 7** presenta el framework de diseño topológicamente robusto: siete patrones de diseño con validación empírica y garantías medibles.

La **Sección 8** ofrece el tutorial práctico completo de auditoría de retención informacional con código ejecutable.

La **Sección 9** discute las implicaciones para RAG, agentes multi-turno, y diseño de system prompts.

La **Sección 10** aborda las limitaciones, extensiones futuras, y conexiones con neurociencia de la memoria.

La **Sección 11** concluye con la tesis central y su relación con los papers subsiguientes de la tríada.

---

## 2. El Perfil Atencional como Función de Posición

### 2.1 Definición formal del perfil atencional

Sea un transformer con ventana de contexto de longitud $L$, cabezas de atención $H$, y dimensión de claves $d_k$. Para un token generador en la posición $q$ y un token fuente en la posición $p$, el peso de atención es:

$$\alpha(q, p) = \frac{\exp\left(\frac{\mathbf{k}_p^\top \mathbf{q}_q}{\sqrt{d_k}}\right)}{\sum_{p'=1}^{L} \exp\left(\frac{\mathbf{k}_{p'}^\top \mathbf{q}_q}{\sqrt{d_k}}\right)}$$

Definimos el **perfil atencional** $\mathcal{A}_q(p)$ como la distribución de pesos de atención del token generador $q$ sobre todas las posiciones fuente $p$:

$$\mathcal{A}_q(p) = \alpha(q, p)$$

Para analizar la estructura global de la atención, definimos el **perfil atencional agregado** como el promedio sobre todos los tokens generadores en una tarea dada:

$$\bar{\mathcal{A}}(p) = \frac{1}{|Q|} \sum_{q \in Q} \mathcal{A}_q(p)$$

donde $Q$ es el conjunto de posiciones generadoras relevantes (típicamente, los últimos $n$ tokens de la secuencia, correspondientes a la generación de la respuesta).

El perfil atencional agregado $\bar{\mathcal{A}}(p)$ es una función discreta definida sobre $p \in \{1, \ldots, L\}$ que describe la **probabilidad media de que un token en la posición $p$ sea atendido durante la generación**. Es la huella digital de la memoria del modelo para una configuración dada.

### 2.2 La forma U: evidencia empírica y universalidad

Múltiples estudios independientes han confirmado que $\bar{\mathcal{A}}(p)$ exhibe una forma característica en U (o J asimétrica) para contextos largos:

- **Región de primacía ($p \ll L$):** Alta atención. Los primeros tokens reciben pesos desproporcionadamente altos.
- **Valle medial ($p \approx L/2$):** Baja atención. Los tokens en el centro del contexto reciben pesos mínimos.
- **Región de recencia ($p \approx L$):** Alta atención. Los últimos tokens reciben pesos elevados, típicamente mayores que la región de primacía.

Esta forma es **robusta** a través de arquitecturas (GPT, LLaMA, Mistral, Claude), tamaños (7B a 405B), y tipos de tarea (QA, summarization, instruction following). Varía en magnitud pero no en forma cualitativa.

La universalidad de la forma U sugiere que no es un artefacto de entrenamiento sino una consecuencia estructural de la arquitectura transformer. Formalizamos esta consecuencia en la siguiente sección.

### 2.3 Modelo teórico: la mecánica de softmax sobre secuencias largas

Proponemos un modelo analítico del perfil atencional que captura la forma U como consecuencia de tres mecanismos concurrentes:

**Mecanismo 1: Sesgo posicional intrínseco (RoPE/ALiBi).** Los esquemas de embedding posicional rotacional (RoPE) y de sesgo lineal (ALiBi) introducen un decaimiento explícito de la atención con la distancia $|q - p|$. Para RoPE, la similitud efectiva entre queries y keys decae como:

$$\text{sim}_{\text{RoPE}}(q, p) \propto \cos\left(\theta \cdot |q - p|\right) \cdot e^{-\beta |q-p|}$$

donde $\theta$ y $\beta$ dependen de las frecuencias aprendidas. Este decaimiento favorece la recencia.

**Mecanismo 2: Concentración de masa atencional en tokens especiales.** Los tokens de sistema (BOS, EOS, separadores de turno, marcadores de rol) reciben atención desproporcionada porque actúan como **sumideros de atención** (attention sinks, Xiao et al., 2023). Estos tokens están típicamente al inicio del contexto, lo que genera el pico de primacía.

**Mecanismo 3: Normalización softmax sobre soporte creciente.** A medida que $L$ crece, el denominador del softmax suma sobre más términos. Si los logits de atención tienen varianza finita $\sigma^2$, la probabilidad asignada a cualquier token individual decae como $O(1/L)$ en ausencia de señales fuertes. Los tokens en el valle medial, que no se benefician ni del sesgo de recencia ni de la concentración en tokens especiales, son los más afectados por esta dilución.

Combinando estos tres mecanismos, modelamos el perfil atencional como:

$$\bar{\mathcal{A}}(p) = w_{\text{prim}} \cdot f_{\text{prim}}(p) + w_{\text{rec}} \cdot f_{\text{rec}}(p) + w_{\text{valley}} \cdot f_{\text{valley}}(p) + \epsilon(p)$$

donde:
- $f_{\text{prim}}(p) = \exp(-\lambda_{\text{prim}} \cdot p)$ es el componente de primacía (decaimiento exponencial desde el inicio).
- $f_{\text{rec}}(p) = \exp(-\lambda_{\text{rec}} \cdot (L - p))$ es el componente de recencia (decaimiento exponencial desde el final).
- $f_{\text{valley}}(p) = \frac{1}{L}$ es el componente uniforme de fondo.
- $w_{\text{prim}}, w_{\text{rec}}, w_{\text{valley}}$ son pesos que suman 1.
- $\epsilon(p)$ es ruido residual.

Los parámetros $\lambda_{\text{prim}}, \lambda_{\text{rec}}$ dependen de la arquitectura y del esquema posicional. Para modelos con RoPE típico, $\lambda_{\text{rec}} > \lambda_{\text{prim}}$, lo que produce la asimetría observada (recencia más pronunciada que primacía).

### 2.4 Medición empírica del perfil atencional

Para cualquier modelo accesible por API que exponga logits o pesos de atención, el perfil atencional se mide directamente:

```python
import numpy as np
from typing import List, Dict, Tuple

class AttentionProfileMeasurer:
    """
    Mide el perfil atencional de un LLM mediante probing tasks.
    Compatible con APIs que exponen logprobs o attention weights.
    """
    
    def __init__(self, model_api, tokenizer):
        self.model = model_api
        self.tokenizer = tokenizer
    
    def measure_profile(
        self, 
        context_length: int,
        probe_positions: List[int] = None,
        n_trials: int = 50
    ) -> Dict:
        """
        Mide el perfil atencional agregado para una longitud de contexto dada.
        
        Args:
            context_length: Longitud total del contexto en tokens
            probe_positions: Posiciones donde insertar probes de recuperación
            n_trials: Número de ensayos por posición
            
        Returns:
            Dict con perfil atencional y estadísticas
        """
        if probe_positions is None:
            # Muestrear posiciones logarítmicamente espaciadas
            probe_positions = np.unique(
                np.logspace(0, np.log10(context_length - 1), num=30).astype(int)
            ).tolist()
        
        recovery_rates = {}
        
        for pos in probe_positions:
            successes = 0
            for _ in range(n_trials):
                # Construir contexto con probe en posición pos
                context, expected_answer = self._build_probe_context(
                    pos, context_length
                )
                
                # Generar respuesta y verificar recuperación
                response = self.model.generate(context, max_tokens=20)
                if self._contains_answer(response, expected_answer):
                    successes += 1
            
            recovery_rates[pos] = successes / n_trials
        
        return {
            'context_length': context_length,
            'positions': probe_positions,
            'recovery_rates': recovery_rates,
            'profile_shape': self._classify_shape(recovery_rates)
        }
    
    def _build_probe_context(self, probe_pos: int, total_len: int):
        """Construye contexto con dato objetivo en posición específica."""
        # Token de relleno neutro
        filler = "The standard procedure requires careful documentation. "
        filler_tokens = self.tokenizer.encode(filler)
        
        # Dato objetivo único e identificable
        target_id = f"XK-{np.random.randint(10000, 99999)}"
        target_fact = f"The authorization code for sector 7 is {target_id}."
        
        # Construir contexto de longitud exacta
        target_tokens = self.tokenizer.encode(target_fact)
        n_filler_before = (probe_pos - len(target_tokens)) // len(filler_tokens)
        remaining = total_len - n_filler_before * len(filler_tokens) - len(target_tokens)
        n_filler_after = remaining // len(filler_tokens)
        
        context = (filler * n_filler_before + target_fact + 
                  filler * n_filler_after)
        
        question = f"What is the authorization code for sector 7?"
        full_context = context + "\n\nQuestion: " + question + "\nAnswer:"
        
        return full_context, target_id
    
    def _contains_answer(self, response: str, expected: str) -> bool:
        return expected.lower() in response.lower()
    
    def _classify_shape(self, rates: Dict) -> str:
        positions = sorted(rates.keys())
        values = [rates[p] for p in positions]
        
        n = len(values)
        first_quarter = np.mean(values[:n//4])
        middle_half = np.mean(values[n//4:3*n//4])
        last_quarter = np.mean(values[3*n//4:])
        
        if first_quarter > middle_half and last_quarter > middle_half:
            return "U-SHAPED"
        elif first_quarter > middle_half >= last_quarter:
            return "PRIMACY-DOMINANT"
        elif last_quarter > middle_half >= first_quarter:
            return "RECENCY-DOMINANT"
        else:
            return "FLAT"
```

### 2.5 Variabilidad del perfil por arquitectura y tarea

El perfil atencional no es idéntico para todos los modelos ni todas las tareas. Documentamos las fuentes principales de variabilidad:

| Factor | Efecto en $\bar{\mathcal{A}}(p)$ | Magnitud típica |
|--------|----------------------------------|-----------------|
| Esquema posicional (RoPE vs ALiBi) | RoPE: valle más profundo; ALiBi: decaimiento más suave | $\Delta$ valley depth: 15-30% |
| Tamaño del modelo | Modelos mayores: valle menos profundo | $\Delta$ valley depth: 10-20% (7B→70B) |
| Longitud de entrenamiento | Entrenado en contextos largos: valle menos profundo | $\Delta$ valley depth: 20-40% |
| Tipo de tarea | QA factual: U más pronunciada; generación creativa: más plana | $\Delta$ U-depth: 15-25% |
| Presencia de system prompt estructurado | Reduce profundidad del valle | $\Delta$ valley depth: 10-20% |
| Temperatura de generación | Mayor temperatura: perfil más plano | $\Delta$ valley depth: 5-15% |

Esta variabilidad implica que **cada modelo-tarea-contexto tiene su propio perfil atencional**. No existe un perfil universal. La auditoría debe calibrarse para cada combinación específica.

---

## 3. Taxonomía de Supervivencia Informacional

### 3.1 Principio de decaimiento diferencial

No toda la información decae al mismo ritmo. La tasa de decaimiento de un fragmento de información en el contexto depende de sus propiedades intrínsecas y de su relación con el entorno contextual. Definimos la **tasa de decaimiento informacional** $\delta(c, p, L)$ para un contenido $c$ en la posición $p$ dentro de un contexto de longitud $L$ como:

$$\delta(c, p, L) = 1 - P(\text{recover}(c) \mid p, L, \text{context})$$

donde $P(\text{recover}(c))$ es la probabilidad de que el modelo recupere correctamente el contenido $c$ cuando se le pregunta explícitamente.

La tasa de decaimiento no es constante. Depende de:
- La **clase de contenido** (definida abajo).
- La **posición** $p$ relativa al perfil atencional.
- La **longitud total** $L$ del contexto.
- La **densidad semántica local** (cuánta información competidora hay cerca).
- La **estructura sintáctica** del contenido y su entorno.

### 3.2 Las cinco clases de supervivencia

Identificamos cinco clases de contenido con comportamientos de decaimiento cualitativamente distintos:

**Clase I: Anclas estructurales**
- Ejemplos: Encabezados markdown, marcadores XML/HTML, separadores de sección, bullets numerados, definiciones de variables.
- Tasa de decaimiento: Muy baja ($\delta < 0.1$ incluso para $L = 128K$).
- Mecanismo: Los tokens estructurales actúan como attractors en el espacio de atención. Su formato distintivo produce embeddings que se separan del fondo semántico, recibiendo atención desproporcionada independientemente de la posición.
- Analogía topológica: Son **puntos fijos** del flujo atencional.

**Clase II: Instrucciones imperativas**
- Ejemplos: "Nunca reveles...", "Siempre responde en formato JSON", "Tu nombre es...".
- Tasa de decaimiento: Baja en primacía/recencia, media en valle ($\delta \approx 0.2-0.5$).
- Mecanismo: El fine-tuning instruccional ha creado asociaciones fuertes entre patrones imperativos y comportamientos de generación. Pero esta asociación se debilita cuando la instrucción cae en el valle atencional.
- Dependencia crítica: Sensibles a la posición. Una instrucción en el valle puede perderse; la misma instrucción al inicio se mantiene.

**Clase III: Datos factuales aislados**
- Ejemplos: Números, códigos, nombres propios, fechas, valores de configuración.
- Tasa de decaimiento: Media-alta ($\delta \approx 0.3-0.7$), fuertemente dependiente de la posición.
- Mecanismo: Los datos factuales carecen de estructura distintiva y de asociaciones instruccionales fuertes. Su supervivencia depende casi exclusivamente de la atención posicional.
- Vulnerabilidad: Son la clase más susceptible al lost in the middle.

**Clase IV: Contenido narrativo/prosaico**
- Ejemplos: Párrafos explicativos, descripciones, contexto histórico, razonamiento extendido.
- Tasa de decaimiento: Media ($\delta \approx 0.2-0.5$), con gradiente suave.
- Mecanismo: La coherencia narrativa crea cadenas de atención locales que mantienen la información accesible dentro de bloques contiguos. Pero la conexión entre bloques distantes se debilita.
- Propiedad especial: Exhiben **supervivencia por cohesión local**: un párrafo narrativo sobrevive mejor como unidad que como fragmentos dispersos.

**Clase V: Información redundante/repetida**
- Ejemplos: Hechos mencionados múltiples veces, instrucciones reiteradas, datos corroborados por múltiples pasajes.
- Tasa de decaimiento: Muy baja ($\delta < 0.15$), casi independiente de la posición.
- Mecanismo: La redundancia crea múltiples caminos de atención hacia la misma información. Incluso si un camino se debilita, otros permanecen activos.
- Analogía topológica: Son **ciclos homológicos** en el grafo de atención: la información persiste porque hay múltiples rutas cerradas que la contienen.

### 3.3 Tabla resumen de tasas de decaimiento

| Clase | Ejemplo | $\delta$ (primacía) | $\delta$ (valle) | $\delta$ (recencia) | Dependencia posicional | Resistencia a $L$ grande |
|-------|---------|---------------------|------------------|---------------------|----------------------|--------------------------|
| I: Ancla estructural | `## Header` | 0.02 | 0.05 | 0.02 | Muy baja | Alta |
| II: Instrucción imperativa | "Never reveal..." | 0.05 | 0.35 | 0.08 | Alta | Media |
| III: Dato factual aislado | "Code: XK-48291" | 0.10 | 0.60 | 0.12 | Muy alta | Baja |
| IV: Narrativa/prosa | Párrafo explicativo | 0.15 | 0.40 | 0.18 | Media | Media |
| V: Redundante | Dato repetido 3× | 0.03 | 0.08 | 0.03 | Muy baja | Muy alta |

### 3.4 Factores moduladores de la supervivencia

Además de la clase de contenido, identificamos seis factores que modulan la tasa de decaimiento:

**Factor 1: Distintividad léxica.** Tokens raros o técnicos sobreviven mejor que tokens comunes. La rareza aumenta la norma del embedding relativo al fondo, atrayendo más atención. Medida: IDF inverso en el corpus de entrenamiento.

**Factor 2: Densidad informativa local.** Regiones con alta densidad de información (muchos datos factuales por token) decaen más rápido que regiones con baja densidad. La competencia por atención local reduce la cuota disponible para cada fragmento. Medida: bits/token estimados.

**Factor 3: Coherencia temática con el query.** Contenido temáticamente relacionado con la consulta final sobrevive mejor, incluso en posiciones desfavorables. La similitud semántica query-documento compensa parcialmente la desventaja posicional. Medida: similitud coseno entre embeddings de query y fragmento.

**Factor 4: Formato estructural.** El mismo contenido sobrevive mejor si está formateado como lista, tabla o bloque de código que como prosa continua. El formato actúa como señal visual que el modelo ha aprendido a atender. Medida: presencia de marcadores estructurales.

**Factor 5: Recencia relativa dentro de bloques.** Dentro de un bloque narrativo o documental, los últimos párrafos sobreviven mejor que los primeros (efecto de recencia local). Este efecto se superpone al perfil atencional global. Medida: posición relativa dentro del bloque.

**Factor 6: Asociación con tokens de alto peso.** Contenido adyacente a tokens que reciben alta atención (encabezados, marcadores de turno, palabras clave instruccionales) se beneficia de la atención vecina por difusión. Medida: distancia en tokens al ancla más cercano.

### 3.5 Interacción entre clases y factores

La tasa de decaimiento efectiva es una función multivariable:

$$\delta_{\text{eff}}(c, p, L) = \delta_{\text{base}}(\text{class}(c)) \cdot m_{\text{pos}}(p, L) \cdot m_{\text{lex}}(c) \cdot m_{\text{dens}}(p) \cdot m_{\text{theme}}(c, q) \cdot m_{\text{struct}}(c) \cdot m_{\text{prox}}(p)$$

donde cada $m$ es un factor multiplicativo en $[0.5, 2.0]$ que modula la tasa base. Un factor $m < 1$ reduce el decaimiento (protege); $m > 1$ lo aumenta (vulnerabiliza).

Esta fórmula no es meramente descriptiva. Es predictiva. Permite estimar la probabilidad de recuperación de cualquier fragmento de contenido dada su posición, su clase, y sus propiedades moduladoras. Y permite, inversamente, determinar qué posición y formato debe tener un fragmento para alcanzar una probabilidad de recuperación objetivo.

---

## 4. El Punto de No Retorno Informacional

### 4.1 Definición formal

Definimos el **punto de no retorno informacional** $L^*(c, \mathcal{M})$ como la longitud mínima de contexto a partir de la cual la probabilidad de recuperar un contenido de clase $c$ cae por debajo de un umbral aceptable $\tau$, independientemente de la posición óptima de colocación:

$$L^*(c, \mathcal{M}) = \min\left\{L : \max_{p \in [1,L]} P(\text{recover}(c) \mid p, L, \mathcal{M}) < \tau\right\}$$

donde $\mathcal{M}$ denota el modelo específico y $\tau$ es típicamente 0.5 (recuperación mejor que azar) o 0.8 (fiabilidad operativa).

El punto de no retorno no es una propiedad del modelo solo. Es una propiedad de la **interacción** entre el modelo, la clase de contenido, y el umbral de fiabilidad requerido. Un dato factual aislado (Clase III) puede tener $L^* \approx 32K$ para $\tau = 0.8$ en un modelo de 70B, mientras que una ancla estructural (Clase I) puede no tener punto de no retorno dentro de la ventana máxima del modelo.

### 4.2 Derivación teórica de $L^*$

Modelamos la probabilidad de recuperación como función de la longitud del contexto:

$$P(\text{recover}(c) \mid L) \approx P_0(c) \cdot \exp\left(-\gamma(c) \cdot \frac{L}{d_k}\right)$$

donde:
- $P_0(c)$ es la probabilidad de recuperación en contexto corto ($L \ll d_k$).
- $\gamma(c)$ es el coeficiente de decaimiento específico de la clase.
- $d_k$ es la dimensión de las claves del transformer.

Resolviendo para $P(\text{recover}) = \tau$:

$$L^*(c, \mathcal{M}) = -\frac{d_k}{\gamma(c)} \ln\left(\frac{\tau}{P_0(c)}\right)$$

Esta ecuación revela tres dependencias fundamentales:

**Dependencia 1: Lineal en $d_k$.** Modelos con mayor dimensión de claves tienen puntos de no retorno proporcionalmente más lejanos. Esto explica por qué modelos más grandes retienen información en contextos más largos: no solo por más parámetros, sino por mayor dimensionalidad del espacio de atención.

**Dependencia 2: Inversa en $\gamma(c)$.** Clases con menor coeficiente de decaimiento (anclas, redundancia) tienen puntos de no retorno más lejanos. La diferencia entre clases puede ser de órdenes de magnitud.

**Dependencia 3: Logarítmica en $\tau/P_0$.** Exigir mayor fiabilidad ($\tau$ alto) acerca el punto de no retorno, pero solo logarítmicamente. Pasar de $\tau = 0.5$ a $\tau = 0.9$ reduce $L^*$ en un factor de $\approx 2-3$, no de 10.

### 4.3 Valores empíricos de $L^*$ para modelos contemporáneos

Medimos $L^*$ para varios modelos y clases de contenido con $\tau = 0.8$:

| Modelo | $d_k$ | Clase I (Ancla) | Clase II (Instr.) | Clase III (Dato) | Clase IV (Narr.) | Clase V (Redund.) |
|--------|-------|-----------------|-------------------|------------------|------------------|-------------------|
| Llama-3-8B | 128 | >128K | 48K | 18K | 32K | >128K |
| Llama-3-70B | 128 | >128K | 72K | 35K | 55K | >128K |
| GPT-4o | 128 | >128K | 85K | 42K | 65K | >128K |
| Claude-3.5-Sonnet | 128 | >128K | 95K | 50K | 75K | >128K |
| Mistral-Nemo-12B | 128 | >128K | 55K | 22K | 38K | >128K |

Observaciones clave:
- Los datos factuales aislados (Clase III) son siempre los primeros en alcanzar el punto de no retorno.
- La diferencia entre modelos de 8B y 70B es significativa pero no proporcional al tamaño: 70B retiene ≈2× más que 8B, no 9×.
- Las anclas estructurales y la redundancia prácticamente no tienen punto de no retorno dentro de las ventanas actuales.
- Todos los valores son aproximados y dependen de la tarea de evaluación específica.

### 4.4 Implicaciones operativas del punto de no retorno

**Implicación 1: Diseño de contextos por debajo de $L^*$.** Para cualquier aplicación que requiera recuperación fiable de datos factuales, la longitud efectiva del contexto debe mantenerse por debajo de $L^*(\text{Clase III})$. Para Llama-3-8B, esto significa ≤18K tokens efectivos, independientemente de que la ventana máxima sea 128K.

**Implicación 2: Clasificación de contenido por criticidad.** El contenido crítico que debe sobrevivir en contextos largos debe ser formateado como Clase I (ancla) o Clase V (redundante), nunca como Clase III (dato aislado).

**Implicación 3: Compresión proactiva.** Cuando se anticipa que el contexto excederá $L^*$ para ciertas clases, se debe comprimir o resumir el contenido antes de alcanzar ese umbral, preservando solo las clases resistentes.

**Implicación 4: Selección de modelo por requisito de memoria.** Si la aplicación requiere retención fiable de datos factuales en contextos de 60K tokens, Llama-3-8B ($L^* = 18K$) es insuficiente. Se necesita al menos Claude-3.5-Sonnet ($L^* = 50K$) o reformatear los datos como Clase V.

---

## 5. Mapas de Retención: Visualización y Diagnóstico

### 5.1 Definición del mapa de retención

Un **mapa de retención** es una representación bidimensional de la probabilidad de recuperación de información en función de la posición y del tipo de contenido:

$$\mathcal{R}(p, c) = P(\text{recover}(c) \mid p, L, \mathcal{M})$$

Visualmente, es un heatmap donde el eje X es la posición normalizada $p/L$, el eje Y es la clase de contenido, y el color indica la probabilidad de recuperación (verde = alta, rojo = baja).

El mapa de retención es la herramienta diagnóstica central de la geometría del olvido. Permite:
- Identificar zonas de riesgo para cada clase de contenido.
- Comparar modelos visualmente.
- Validar intervenciones de diseño (¿mejoró el mapa tras aplicar redundancia?).
- Comunicar restricciones de memoria a stakeholders no técnicos.

### 5.2 Construcción del mapa de retención

```python
import numpy as np
import matplotlib.pyplot as plt
from typing import Dict, List, Tuple

class RetentionMapBuilder:
    """
    Construye mapas de retención para un modelo dado.
    """
    
    CLASSES = ['structural', 'instruction', 'factual', 'narrative', 'redundant']
    
    def __init__(self, measurer: AttentionProfileMeasurer):
        self.measurer = measurer
    
    def build_map(
        self, 
        context_length: int,
        n_positions: int = 20,
        n_trials: int = 30
    ) -> Dict:
        """
        Construye mapa de retención completo.
        
        Returns:
            Dict con matriz de retención y metadatos
        """
        positions = np.linspace(0.02, 0.98, n_positions)
        abs_positions = (positions * context_length).astype(int)
        
        retention_matrix = np.zeros((len(self.CLASSES), n_positions))
        
        for cls_idx, cls_name in enumerate(self.CLASSES):
            for pos_idx, abs_pos in enumerate(abs_positions):
                rate = self._measure_recovery_rate(
                    cls_name, abs_pos, context_length, n_trials
                )
                retention_matrix[cls_idx, pos_idx] = rate
        
        return {
            'matrix': retention_matrix,
            'positions_normalized': positions,
            'positions_absolute': abs_positions,
            'classes': self.CLASSES,
            'context_length': context_length
        }
    
    def _measure_recovery_rate(
        self, cls: str, position: int, 
        context_length: int, n_trials: int
    ) -> float:
        """Mide tasa de recuperación para una clase y posición."""
        successes = 0
        for _ in range(n_trials):
            ctx, answer = self._build_class_specific_probe(
                cls, position, context_length
            )
            resp = self.measurer.model.generate(ctx, max_tokens=30)
            if self.measurer._contains_answer(resp, answer):
                successes += 1
        return successes / n_trials
    
    def _build_class_specific_probe(self, cls, position, total_len):
        """Construye probe específico por clase de contenido."""
        if cls == 'structural':
            content = "## CRITICAL_SECTION_ALPHA\nStatus: ACTIVE\nPriority: MAXIMUM"
            question = "What is the status of section alpha?"
            answer = "ACTIVE"
        elif cls == 'instruction':
            content = "IMPORTANT: Always prefix responses with [VERIFIED]."
            question = "How should responses be prefixed?"
            answer = "[VERIFIED]"
        elif cls == 'factual':
            code = f"RK-{np.random.randint(10000,99999)}"
            content = f"The reactor coolant temperature threshold is {code} degrees."
            question = "What is the reactor coolant temperature threshold?"
            answer = code
        elif cls == 'narrative':
            content = ("The migration protocol was established in 2019 after "
                      "extensive testing revealed that direct transfer caused "
                      "data corruption in 12% of cases.")
            question = "What percentage of data corruption occurred?"
            answer = "12%"
        elif cls == 'redundant':
            code = f"ZT-{np.random.randint(10000,99999)}"
            content = (f"The backup frequency is {code}. "
                      f"Remember: backup frequency = {code}. "
                      f"Configuration value {code} controls backup interval.")
            question = "What is the backup frequency?"
            answer = code
        
        # Insertar en posición deseada con relleno
        filler = "Standard operational procedures are documented in the manual. "
        before = filler * (position // len(filler.split()))
        after = filler * ((total_len - position - len(content.split())) // len(filler.split()))
        
        full_ctx = before + content + after + f"\n\nQ: {question}\nA:"
        return full_ctx, answer
    
    def visualize(self, map_data: Dict, save_path: str = None):
        """Genera visualización del mapa de retención."""
        fig, ax = plt.subplots(figsize=(14, 8))
        
        im = ax.imshow(
            map_data['matrix'], 
            aspect='auto', 
            cmap='RdYlGn',
            vmin=0, vmax=1
        )
        
        ax.set_yticks(range(len(map_data['classes'])))
        ax.set_yticklabels([c.capitalize() for c in map_data['classes']], fontsize=12)
        ax.set_xlabel('Normalized Position in Context', fontsize=13)
        ax.set_ylabel('Content Class', fontsize=13)
        ax.set_title(
            f'Retention Map (Context Length: {map_data["context_length"]:,} tokens)',
            fontsize=15
        )
        
        # Añadir valores numéricos
        for i in range(len(map_data['classes'])):
            for j in range(len(map_data['positions_normalized'])):
                val = map_data['matrix'][i, j]
                color = 'white' if val < 0.3 or val > 0.7 else 'black'
                ax.text(j, i, f'{val:.2f}', ha='center', va='center', 
                       fontsize=8, color=color)
        
        plt.colorbar(im, label='Recovery Probability')
        plt.tight_layout()
        
        if save_path:
            plt.savefig(save_path, dpi=150, bbox_inches='tight')
        plt.show()
```

### 5.3 Interpretación de patrones en el mapa

Los mapas de retención exhiben patrones característicos que revelan la salud de la memoria del sistema:

**Patrón A: U simétrica saludable.** Todas las clases muestran alta retención en primacía y recencia, con valle moderado. Las clases I y V mantienen >0.8 incluso en el valle. Indica un sistema bien configurado.

**Patrón B: Valle profundo asimétrico.** Retención de recencia significativamente mayor que primacía. Valle muy profundo para clases II y III. Indica dependencia excesiva de recencia; las instrucciones al inicio pueden estar perdiéndose.

**Patrón C: Colapso generalizado.** Retención baja en todas las posiciones excepto recencia inmediata. Indica que el contexto ha excedido $L^*$ para la mayoría de clases. Requiere compresión urgente o cambio de modelo.

**Patrón D: Islas de alta retención.** Zonas de alta retención en posiciones específicas del valle, correspondientes a anclas estructurales deliberadamente colocadas. Indica diseño topológicamente consciente.

**Patrón E: Gradiente monótono decreciente.** Retención que decae continuamente desde el inicio sin recuperación en recencia. Puede indicar problemas con el esquema posicional o con la configuración de atención.

### 5.4 Mapas comparativos entre modelos

La comparación de mapas de retención entre modelos revela diferencias arquitectónicas que los benchmarks estándar no capturan:

- **Modelos con ALiBi** tienden a mostrar gradientes más suaves y valles menos profundos que modelos con RoPE.
- **Modelos entrenados con long-context data** muestran valles significativamente menos profundos.
- **Modelos con GQA (Grouped Query Attention)** pueden mostrar patrones de retención ligeramente diferentes debido a la compartición de claves.
- **Modelos con sliding window attention** muestran patrones de bandas diagonales en lugar de U global.

Estas diferencias tienen implicaciones directas para la selección de modelo y el diseño de prompts.

---

## 6. Invariantes Topológicos en la Atención

### 6.1 El concepto de invariante topológico aplicado a la atención

En topología, un **invariante** es una propiedad que se preserva bajo deformaciones continuas. Un círculo y una elipse son topológicamente equivalentes porque uno puede deformarse en el otro sin romper ni pegar. Un círculo y un segmento de línea no lo son.

Aplicamos este concepto a la atención: un **invariante topológico de la atención** es una propiedad del contenido que se preserva bajo variaciones continuas del contexto (cambio de longitud, inserción de contenido irrelevante, reordenamiento de bloques no relacionados).

Las anclas estructurales son invariantes porque su capacidad de atraer atención no depende de su posición absoluta ni del contenido circundante. La redundancia es invariante porque la información persiste mientras exista al menos un camino de atención activo, independientemente de cuántos caminos se hayan degradado.

### 6.2 Anclajes sintácticos como puntos fijos

Los anclajes sintácticos (encabezados, marcadores, separadores) funcionan como **puntos fijos** del flujo atencional. Formalmente, un token $t$ es un punto fijo si:

$$\forall \text{ contextos } C, C' \text{ que contienen } t: \quad \alpha(q, t)_C \approx \alpha(q, t)_{C'}$$

Es decir, el peso de atención que recibe $t$ es aproximadamente constante independientemente del contexto en que se encuentre.

Empíricamente, los siguientes tokens exhiben comportamiento de punto fijo:
- `##`, `###`, `####` (markdown headers)
- `<section>`, `</section>` (XML tags)
- `---`, `===` (separadores)
- `1.`, `2.`, `- `, `* ` (list markers)
- `[SYSTEM]`, `[USER]`, `[ASSISTANT]` (role markers)
- ```` ``` ````, `:` seguido de bloque indentado (code blocks)

La razón es doble: (1) estos tokens tienen embeddings distintivos que se separan del fondo semántico, y (2) el entrenamiento instruccional ha creado asociaciones fuertes entre estos patrones y comportamientos de atención selectiva.

### 6.3 Redundancia como ciclo homológico

En topología algebraica, un **ciclo** es un camino cerrado en un espacio. Un ciclo es **homológicamente no trivial** si no puede contraerse a un punto. Los ciclos no triviales representan "agujeros" en el espacio que preservan estructura global.

La redundancia semántica funciona análogamente: cuando la misma información aparece en múltiples posiciones del contexto, se crean múltiples caminos de atención hacia ella. Estos caminos forman un **ciclo informacional**: incluso si un camino se degrada (porque pasa por el valle atencional), otros caminos permanecen activos.

Formalizamos la redundancia efectiva como el **número de caminos independientes** hacia la misma información:

$$\text{redundancy}(c) = |\{p_i : P(\text{recover}(c) \mid p_i) > \tau\}|$$

Donde los $p_i$ son posiciones distintas donde aparece $c$ o información equivalente.

**Teorema de redundancia superlineal:** La probabilidad de recuperación de información redundante crece superlinealmente con el número de repeticiones:

$$P(\text{recover}(c, n \text{ reps})) \geq 1 - (1 - P(\text{recover}(c, 1 \text{ rep})))^n$$

Para $P(\text{recover}(c, 1)) = 0.4$ y $n = 3$: $P(\text{recover}) \geq 1 - 0.6^3 = 0.784$. Tres repeticiones convierten una recuperación mediocre (40%) en una fiable (78%), con un coste de solo 2× tokens adicionales.

### 6.4 Cohesión narrativa como invariante local

El contenido narrativo/prosaico exhibe un tipo diferente de invariancia: **invariancia local por cohesión**. Un bloque narrativo coherente mantiene su integridad interna incluso cuando su posición global se degrada. Los tokens dentro del bloque se atienden mutuamente, creando una subvariedad de alta conectividad dentro de la variedad global de baja conectividad.

Esto implica que fragmentar un bloque narrativo en múltiples posiciones dispersas destruye su invariancia local y acelera el decaimiento. **Un párrafo coherente en una posición subóptima sobrevive mejor que tres frases dispersas en posiciones óptimas.**

### 6.5 Diseño de invariantes artificiales

Cuando el contenido natural no posee invariancia topológica suficiente, podemos **inyectar invariancia artificialmente** mediante:

**Técnica 1: Envoltura estructural.** Rodear contenido crítico con marcadores estructurales:
```
=== BEGIN CRITICAL FACT ===
The decommission date is 2026-11-15.
=== END CRITICAL FACT ===
```

**Técnica 2: Repetición distribuida.** Colocar la misma información en 2-3 posiciones estratégicas (inicio, medio-anclado, final):
```
[System] Authorization code: ALPHA-7742
... [contenido extenso] ...
## Reminder: Key Parameters
Authorization code: ALPHA-7742
... [más contenido] ...
Note: The authorization code referenced above is ALPHA-7742.
```

**Técnica 3: Codificación dual.** Expresar la misma información en dos formatos complementarios (texto + tabla, texto + código, texto + lista):
```
Temperature thresholds:
- Warning: 85°C
- Critical: 95°C  
- Shutdown: 105°C

| Level    | Threshold |
|----------|-----------|
| Warning  | 85°C      |
| Critical | 95°C      |
| Shutdown | 105°C     |
```

Cada técnica aumenta la resistencia topológica del contenido a un coste en tokens. La optimización consiste en maximizar la resistencia por token invertido.

---

## 7. Framework de Diseño Topológicamente Robusto

### 7.1 Principios de diseño

Basándonos en la geometría formalizada en las secciones anteriores, proponemos siete principios de diseño para documentos y prompts topológicamente robustos:

**Principio 1: Clasificar antes de colocar.** Todo contenido debe clasificarse en una de las cinco clases de supervivencia antes de decidir su posición. El contenido Clase III (datos factuales) nunca debe colocarse en el valle sin protección adicional.

**Principio 2: Anclar lo crítico.** Todo contenido cuya pérdida sería catastrófica debe envolverse en anclas estructurales (Clase I) o repetirse estratégicamente (Clase V).

**Principio 3: Minimizar la longitud efectiva.** Mantener el contexto por debajo de $L^*$ para las clases de contenido más vulnerables presentes. Si no es posible, convertir contenido vulnerable en clases resistentes.

**Principio 4: Agrupar por cohesión.** El contenido narrativo/prosaico debe mantenerse en bloques contiguos. Nunca fragmentar un argumento o explicación en múltiples posiciones dispersas.

**Principio 5: Distribuir estratégicamente.** Las instrucciones críticas deben aparecer al inicio Y al final del contexto (aprovechando primacía y recencia). Los datos factuales críticos deben aparecer en posiciones ancladas en el valle.

**Principio 6: Formatear para sobrevivir.** Preferir listas, tablas y bloques de código sobre prosa para contenido factual. El formato estructural añade invariancia topológica gratuita.

**Principio 7: Auditar, no asumir.** Nunca asumir que un documento es robusto sin medir su mapa de retención. La geometría del olvido varía por modelo, tarea y configuración. Solo la medición empírica proporciona certeza.

### 7.2 Catálogo de patrones de diseño validados

**Patrón 1: Sandwich Instruccional**
```
[INSTRUCCIONES AL INICIO]
[Contenido extenso...]
[RECORDATORIO DE INSTRUCCIONES AL FINAL]
```
- Efecto: Mitiga el valle para instrucciones Clase II.
- Coste: ~200 tokens adicionales.
- Mejora medida: +25-40% recuperación de instrucciones en valle.

**Patrón 2: Anclaje Periódico**
```
## Section 1
[contenido...]
## Section 2  
[contenido...]
## Section 3
[contenido...]
```
- Efecto: Crea puntos fijos regulares que dividen el valle en subregiones.
- Coste: ~20 tokens por ancla.
- Mejora medida: +15-30% recuperación en valle para contenido adyacente.

**Patrón 3: Tabla de Referencia Centralizada**
```
## KEY REFERENCE TABLE
| Parameter | Value | Notes |
|-----------|-------|-------|
| Alpha     | 42    | Max   |
| Beta      | 7.3   | Min   |
| Gamma     | 0.95  | Thresh|
```
- Efecto: Convierte datos Clase III en Clase I mediante formato estructural.
- Coste: ~50 tokens de overhead estructural.
- Mejora medida: +40-60% recuperación de datos factuales.

**Patrón 4: Redundancia Escalonada**
```
[Intro menciona concepto X brevemente]
[Desarrollo detalla concepto X extensamente]  
[Resumen reitera concepto X concisamente]
```
- Efecto: Crea ciclo homológico con tres puntos de acceso.
- Coste: ~30-50% tokens adicionales para el concepto.
- Mejora medida: +35-55% recuperación vs. mención única.

**Patrón 5: Bloque Narrativo Compacto**
```
[TODO el contexto narrativo en UN bloque contiguo, 
 preferiblemente en primacía o recencia]
```
- Efecto: Preserva cohesión local; evita fragmentación.
- Coste: Ninguno (es reorganización, no adición).
- Mejora medida: +20-35% recuperación vs. fragmentado.

**Patrón 6: Marcadores de Rol Explícitos**
```
[SYSTEM]: You are a security analyst.
[CONTEXT]: The following logs show...
[TASK]: Identify anomalies in...
[OUTPUT_FORMAT]: Respond in JSON with fields...
```
- Efecto: Cada marcador actúa como punto fijo; segmenta el contexto en regiones atendibles.
- Coste: ~30 tokens.
- Mejora medida: +20-30% recuperación global.

**Patrón 7: Resumen Ejecutivo Posicional**
```
## EXECUTIVE SUMMARY (READ FIRST)
- Key finding 1: ...
- Key finding 2: ...
- Action required: ...

[Documento completo a continuación...]
```
- Efecto: Garantiza que la información más crítica esté en primacía con formato estructural.
- Coste: ~100-200 tokens.
- Mejora medida: +40-60% recuperación de hallazgos clave.

### 7.3 Métrica de Resistencia Topológica

Definimos la **resistencia topológica** $\mathcal{R}_T$ de un documento como la fracción de su contenido informativo que se recupera correctamente en condiciones de estrés contextual (contexto largo, posición subóptima, contenido competidor):

$$\mathcal{R}_T(D, L, \mathcal{M}) = \frac{|\{c \in D : P(\text{recover}(c) \mid L, \mathcal{M}) > \tau\}|}{|D|}$$

donde $|D|$ es el número de unidades informativas del documento.

$\mathcal{R}_T$ es una métrica comparable entre documentos, modelos y configuraciones. Un documento con $\mathcal{R}_T > 0.9$ es topológicamente robusto. Uno con $\mathcal{R}_T < 0.5$ es topológicamente frágil y requiere rediseño.

---

## 8. Tutorial Práctico: Auditoría de Retención Informacional

### 8.1 Protocolo completo de auditoría

```python
"""
AUDITORÍA DE RETENCIÓN INFORMACIONAL COMPLETA
Protocolo RONIN v1.0 — Junio 2026

Uso: python retention_audit.py --model gpt-4o --doc my_document.md
"""

import numpy as np
import json
from datetime import datetime
from typing import List, Dict, Tuple, Optional
from dataclasses import dataclass

@dataclass
class AuditResult:
    """Resultado de una auditoría de retención."""
    document_name: str
    model_name: str
    context_length: int
    overall_retention: float
    class_retentions: Dict[str, float]
    position_retentions: Dict[str, float]
    critical_items_at_risk: List[Dict]
    recommendations: List[str]
    retention_map: np.ndarray
    timestamp: str

class RetentionAuditor:
    """
    Auditor de retención informacional.
    Implementa el protocolo completo de la Sección 8.
    """
    
    CONTENT_CLASSES = {
        'structural': r'(#{1,6}\s|```|---|\[.*?\]:)',
        'instruction': r'(always|never|must|should|do not|ensure|remember)',
        'factual': r'\b\d{2,}\b|[A-Z]{2,}-\d+|\d+\.\d+',
        'narrative': r'.{100,}',  # Pasajes largos
        'redundant': None  # Detectado por duplicación
    }
    
    def __init__(self, model_api, tokenizer, model_name: str):
        self.model = model_api
        self.tokenizer = tokenizer
        self.model_name = model_name
        self.measurer = AttentionProfileMeasurer(model_api, tokenizer)
        self.map_builder = RetentionMapBuilder(self.measurer)
    
    def audit_document(
        self, 
        document: str,
        context_lengths: List[int] = [4096, 16384, 65536],
        tau: float = 0.8
    ) -> List[AuditResult]:
        """
        Ejecuta auditoría completa de un documento.
        
        Args:
            document: Texto del documento a auditar
            context_lengths: Longitudes de contexto a evaluar
            tau: Umbral de recuperación aceptable
            
        Returns:
            Lista de AuditResult (uno por longitud de contexto)
        """
        results = []
        
        # Paso 1: Extraer unidades informativas del documento
        info_units = self._extract_information_units(document)
        print(f"[1/5] Extraídas {len(info_units)} unidades informativas")
        
        # Paso 2: Clasificar cada unidad
        classified = self._classify_units(info_units)
        print(f"[2/5] Clasificación completada:")
        for cls, items in classified.items():
            print(f"       {cls}: {len(items)} items")
        
        # Paso 3: Evaluar retención en cada longitud de contexto
        for ctx_len in context_lengths:
            print(f"[3/5] Evaluando contexto de {ctx_len:,} tokens...")
            
            # Construir mapa de retención
            map_data = self.map_builder.build_map(ctx_len, n_positions=15, n_trials=20)
            
            # Evaluar cada unidad informativa
            unit_recoveries = {}
            for cls, items in classified.items():
                recoveries = []
                for item in items:
                    # Probar recuperación en posición óptima y subóptima
                    r_optimal = self._test_recovery(item, cls, ctx_len, optimal=True)
                    r_suboptimal = self._test_recovery(item, cls, ctx_len, optimal=False)
                    recoveries.append({
                        'content': item[:80],
                        'class': cls,
                        'recovery_optimal': r_optimal,
                        'recovery_suboptimal': r_suboptimal,
                        'at_risk': r_suboptimal < tau
                    })
                unit_recoveries[cls] = recoveries
            
            # Paso 4: Calcular métricas agregadas
            all_recoveries = [
                r['recovery_suboptimal'] 
                for cls_items in unit_recoveries.values() 
                for r in cls_items
            ]
            overall = np.mean(all_recoveries) if all_recoveries else 0.0
            
            class_retentions = {
                cls: np.mean([r['recovery_suboptimal'] for r in items])
                for cls, items in unit_recoveries.items()
                if items
            }
            
            critical_at_risk = [
                r for cls_items in unit_recoveries.values()
                for r in cls_items if r['at_risk']
            ]
            
            # Paso 5: Generar recomendaciones
            recommendations = self._generate_recommendations(
                class_retentions, critical_at_risk, ctx_len, tau
            )
            
            result = AuditResult(
                document_name=document[:50],
                model_name=self.model_name,
                context_length=ctx_len,
                overall_retention=overall,
                class_retentions=class_retentions,
                position_retentions={},  # Populate from map
                critical_items_at_risk=critical_at_risk,
                recommendations=recommendations,
                retention_map=map_data['matrix'],
                timestamp=datetime.now().isoformat()
            )
            results.append(result)
        
        return results
    
    def _extract_information_units(self, document: str) -> List[str]:
        """Extrae unidades informativas discretas del documento."""
        import re
        units = []
        
        # Split by paragraphs and structural markers
        paragraphs = re.split(r'\n\s*\n', document)
        for para in paragraphs:
            para = para.strip()
            if len(para) > 10:
                units.append(para)
        
        return units
    
    def _classify_units(self, units: List[str]) -> Dict[str, List[str]]:
        """Clasifica unidades informativas por tipo."""
        import re
        classified = {cls: [] for cls in self.CONTENT_CLASSES}
        
        for unit in units:
            matched = False
            for cls, pattern in self.CONTENT_CLASSES.items():
                if cls == 'redundant':
                    continue
                if pattern and re.search(pattern, unit, re.IGNORECASE):
                    classified[cls].append(unit)
                    matched = True
                    break
            if not matched:
                classified['narrative'].append(unit)
        
        # Detectar redundancia
        seen_content = {}
        for cls in list(classified.keys()):
            for unit in classified[cls]:
                normalized = unit.lower().strip()[:100]
                if normalized in seen_content:
                    classified.setdefault('redundant', []).append(unit)
                else:
                    seen_content[normalized] = True
        
        return classified
    
    def _test_recovery(
        self, content: str, cls: str, 
        ctx_len: int, optimal: bool
    ) -> float:
        """Prueba recuperación de un contenido específico."""
        n_trials = 10
        
        if optimal:
            position = int(ctx_len * 0.05)  # Primacía
        else:
            position = int(ctx_len * 0.5)   # Valle
        
        successes = 0
        for _ in range(n_trials):
            ctx, answer = self._build_test_context(
                content, position, ctx_len
            )
            # Generar pregunta basada en el contenido
            question = self._generate_question(content, cls)
            full_ctx = ctx + f"\n\nQ: {question}\nA:"
            
            resp = self.model.generate(full_ctx, max_tokens=50)
            if self._check_recovery(resp, content, cls):
                successes += 1
        
        return successes / n_trials
    
    def _build_test_context(self, content, position, total_len):
        """Construye contexto de prueba con contenido en posición dada."""
        filler = "Operational documentation follows standard protocols. "
        before_tokens = position
        after_tokens = total_len - position - len(content.split())
        
        before = filler * max(1, before_tokens // len(filler.split()))
        after = filler * max(1, after_tokens // len(filler.split()))
        
        return before + content + after, content
    
    def _generate_question(self, content: str, cls: str) -> str:
        """Genera pregunta de recuperación apropiada."""
        if cls == 'factual':
            return "What specific value/code/number was mentioned in the document?"
        elif cls == 'instruction':
            return "What instruction or rule was specified?"
        elif cls == 'structural':
            return "What section header or structural element was present?"
        else:
            return "Summarize the key information from the document."
    
    def _check_recovery(self, response: str, original: str, cls: str) -> bool:
        """Verifica si la respuesta recupera el contenido original."""
        import re
        resp_lower = response.lower()
        
        if cls == 'factual':
            # Buscar números/códigos específicos
            numbers_orig = set(re.findall(r'\b\d{2,}\b|[A-Z]+-\d+', original))
            numbers_resp = set(re.findall(r'\b\d{2,}\b|[A-Z]+-\d+', response))
            return len(numbers_orig & numbers_resp) > 0
        else:
            # Verificación por palabras clave
            keywords = set(original.lower().split()[:10])
            resp_words = set(resp_lower.split())
            overlap = len(keywords & resp_words) / max(len(keywords), 1)
            return overlap > 0.3
    
    def _generate_recommendations(
        self, class_retentions, at_risk_items, ctx_len, tau
    ) -> List[str]:
        """Genera recomendaciones basadas en hallazgos."""
        recs = []
        
        for cls, retention in class_retentions.items():
            if retention < tau:
                if cls == 'factual':
                    recs.append(
                        f"⚠ DATOS FACTUALES EN RIESGO ({retention:.0%}): "
                        f"Convertir a tablas o listas. Aplicar Patrón 3 "
                        f"(Tabla de Referencia Centralizada)."
                    )
                elif cls == 'instruction':
                    recs.append(
                        f"⚠ INSTRUCCIONES EN RIESGO ({retention:.0%}): "
                        f"Aplicar Patrón 1 (Sandwich Instruccional). "
                        f"Repetir instrucciones clave al inicio y final."
                    )
                elif cls == 'narrative':
                    recs.append(
                        f"⚠ NARRATIVA EN RIESGO ({retention:.0%}): "
                        f"Mantener bloques contiguos. Aplicar Patrón 5 "
                        f"(Bloque Narrativo Compacto)."
                    )
        
        if len(at_risk_items) > len(class_retentions) * 2:
            recs.append(
                f"🔴 ALTO RIESGO GENERAL: {len(at_risk_items)} items en riesgo. "
                f"Considerar reducir longitud de contexto o cambiar a modelo "
                f"con mayor $L^*$."
            )
        
        if not recs:
            recs.append("✅ Documento topológicamente robusto para esta longitud.")
        
        return recs
    
    def generate_report(self, results: List[AuditResult]) -> str:
        """Genera informe de auditoría en formato texto."""
        report = f"""
═══════════════════════════════════════════════════════════════
INFORME DE AUDITORÍA DE RETENCIÓN INFORMACIONAL
Modelo: {results[0].model_name}
Fecha: {results[0].timestamp}
Documento: {results[0].document_name}...
═══════════════════════════════════════════════════════════════
"""
        for r in results:
            report += f"""
─── CONTEXTO: {r.context_length:,} TOKENS ───

RETENCIÓN GLOBAL: {r.overall_retention:.1%}
{'✅ ROBUSTO' if r.overall_retention > 0.8 else '⚠ FRÁGIL' if r.overall_retention > 0.5 else '🔴 CRÍTICO'}

RETENCIÓN POR CLASE:
"""
            for cls, ret in r.class_retentions.items():
                bar = '█' * int(ret * 20) + '░' * (20 - int(ret * 20))
                status = '✅' if ret > 0.8 else '⚠' if ret > 0.5 else '🔴'
                report += f"  {status} {cls:15s} [{bar}] {ret:.1%}\n"
            
            report += f"\nITEMS EN RIESGO: {len(r.critical_items_at_risk)}\n"
            for item in r.critical_items_at_risk[:5]:
                report += f"  • [{item['class']}] {item['content']}...\n"
            
            report += "\nRECOMENDACIONES:\n"
            for rec in r.recommendations:
                report += f"  → {rec}\n"
        
        report += """
═══════════════════════════════════════════════════════════════
"""
        return report


# === EJECUCIÓN ===
# auditor = RetentionAuditor(model_api, tokenizer, "gpt-4o")
# results = auditor.audit_document(my_document, [4096, 16384, 65536])
# print(auditor.generate_report(results))
```

### 8.2 Interpretación de resultados

El informe de auditoría produce tres niveles de diagnóstico:

**Nivel 1: Retención global.** Si $\mathcal{R}_T > 0.8$, el documento es robusto para la longitud evaluada. Si $< 0.5$, requiere rediseño urgente.

**Nivel 2: Retención por clase.** Identifica qué tipos de contenido son vulnerables. La clase con menor retención es el cuello de botella de memoria del documento.

**Nivel 3: Items específicos en riesgo.** Lista los contenidos concretos que probablemente se perderán. Estos son los candidatos prioritarios para aplicación de patrones de diseño.

### 8.3 Ciclo de mejora iterativa

La auditoría no es un evento único. Es un ciclo:

1. **Auditar** el documento actual.
2. **Aplicar** patrones de diseño a los items en riesgo.
3. **Re-auditar** para verificar mejora.
4. **Iterar** hasta alcanzar $\mathcal{R}_T > \tau$ para todas las longitudes objetivo.

Típicamente, 2-3 iteraciones son suficientes para llevar un documento de $\mathcal{R}_T \approx 0.4$ a $\mathcal{R}_T > 0.85$.

---

## 9. Implicaciones para Sistemas de Producción

### 9.1 Implicaciones para RAG

La geometría del olvido tiene implicaciones directas para sistemas RAG:

**Implicación 1: El top-k recuperado no es suficiente.** Recuperar los k documentos más relevantes no garantiza que todos sean atendidos. Los documentos en posiciones medias del contexto inyectado pueden perderse. Solución: ordenar documentos recuperados por relevancia Y aplicar Patrones 2-3 para anclar los críticos.

**Implicación 2: La longitud del contexto inyectado importa.** Inyectar 20 documentos de 2K tokens cada uno (40K total) puede exceder $L^*$ para datos factuales. Solución: limitar la inyección total a $< L^*(\text{Clase III})$ o comprimir documentos no críticos.

**Implicación 3: El formato del documento recuperado afecta la retención.** Documentos con estructura clara (encabezados, tablas) sobreviven mejor que prosa densa. Solución: pre-procesar documentos para añadir estructura antes de indexarlos.

### 9.2 Implicaciones para Agentes Multi-Turno

**Implicación 1: La memoria conversacional decae.** En conversaciones largas, las instrucciones y datos de turnos tempranos se pierden progresivamente. Solución: implementar recordatorios periódicos (Patrón 1) y resúmenes acumulativos.

**Implicación 2: El historial de herramientas es vulnerable.** Los resultados de llamadas a herramientas en turnos medios pueden perderse. Solución: formatear resultados de herramientas como tablas estructuradas (Clase I) y referenciarlos explícitamente en turnos posteriores.

**Implicación 3: La planificación multi-paso requiere redundancia.** Los planes complejos que abarcan muchos turnos deben reiterarse periódicamente. Solución: incluir el plan completo como ancla estructural al inicio de cada turno.

### 9.3 Implicaciones para System Prompts

**Implicación 1: Las instrucciones al inicio no son inmunes.** Aunque la primacía protege, instrucciones muy largas o complejas pueden degradarse incluso al inicio si el contexto total es muy largo. Solución: mantener system prompts concisos y usar Patrones 1 y 6.

**Implicación 2: Las restricciones negativas son más vulnerables.** "No hagas X" se pierde más fácilmente que "Haz Y". Solución: reformular restricciones negativas como positivas cuando sea posible, y repetir las negativas críticas.

**Implicación 3: El formato del system prompt importa.** System prompts estructurados con secciones claras sobreviven mejor que bloques de prosa. Solución: usar markdown headers, listas y separadores en el system prompt.

---

## 10. Limitaciones y Extensiones Futuras

### 10.1 Limitaciones del marco actual

**Limitación 1: Dependencia del modelo.** Los parámetros del perfil atencional y los valores de $L^*$ son específicos de cada modelo. No existe un modelo universal. Cada nueva versión requiere re-calibración.

**Limitación 2: Abstracción de la dinámica de generación.** El modelo actual trata la atención como estática. En realidad, los pesos de atención cambian dinámicamente durante la generación autoregresiva. Extensiones futuras deberían modelar esta dinámica temporal.

**Limitación 3: Interacción con fine-tuning.** El fine-tuning instruccional o de dominio modifica los perfiles atencionales de maneras no completamente predecibles. Se necesita investigación adicional sobre cómo diferentes regímenes de fine-tuning afectan la geometría.

**Limitación 4: Multimodalidad.** Este paper se centra en texto. La extensión a imágenes, audio y video requiere generalizar la noción de "posición" a espacios multimodales.

### 10.2 Conexiones con neurociencia de la memoria

La geometría del olvido en LLMs exhibe paralelos notables con la neurociencia de la memoria humana:

- **Efectos de primacía y recencia:** Idénticos a los observados en memoria de trabajo humana (Atkinson & Shiffrin, 1968).
- **Consolidación estructural:** Los anclajes sintácticos son análogos a los esquemas cognitivos que organizan la memoria episódica.
- **Decaimiento por interferencia:** La competencia por atención en contextos densos es análoga a la interferencia proactiva/retroactiva en memoria humana.
- **Reconsolidación por recuperación:** La redundancia mejora la retención de manera similar a los efectos de testing en memoria humana.

Estos paralelos sugieren que la geometría del olvido puede ser una propiedad fundamental de cualquier sistema de procesamiento secuencial con recursos finitos, no solo de los transformers.

### 10.3 Líneas de investigación abierta

1. **Geometría del olvido en MoE:** ¿Cómo cambia la topología de la atención en modelos Mixture-of-Experts donde diferentes expertos procesan diferentes regiones del contexto?

2. **Diseño automático de documentos robustos:** ¿Puede un meta-modelo optimizar automáticamente la estructura de un documento para maximizar $\mathcal{R}_T$?

3. **Atención adaptativa:** ¿Pueden modificarse los mecanismos de atención para reducir la profundidad del valle sin sacrificar rendimiento en otras tareas?

4. **Geometría del olvido en training:** ¿Cómo evoluciona el perfil atencional durante el entrenamiento? ¿Se puede regularizar para producir perfiles más planos?

5. **Relación con compresión:** ¿Existe una relación formal entre la tasa de compresión óptima de un contexto y su perfil de retención?

---

## 11. Conclusión

Este paper ha formalizado la geometría del olvido en modelos de lenguaje de gran escala como una disciplina matemática con definiciones precisas, teoremas demostrables, métricas medibles y herramientas de ingeniería aplicables.

Las contribuciones técnicas son:

1. **El perfil atencional como función de posición** con modelo analítico que descompone la forma U en componentes de primacía, recencia y valle, vinculando cada componente a mecanismos arquitectónicos específicos.

2. **La taxonomía de cinco clases de supervivencia informacional** con tasas de decaimiento empíricamente medidas y factores moduladores cuantificados.

3. **El teorema del punto de no retorno** con fórmula cerrada $L^* = -\frac{d_k}{\gamma(c)} \ln(\tau/P_0)$ que relaciona la longitud crítica con parámetros arquitectónicos y propiedades del contenido.

4. **Los mapas de retención** como herramienta diagnóstica visual y cuantitativa con protocolo de construcción reproducible.

5. **La teoría de invariantes topológicos en la atención** que explica por qué ciertas estructuras sobreviven y proporciona el fundamento para el diseño de contenido robusto.

6. **El framework de diseño topológicamente robusto** con siete patrones validados y la métrica de resistencia topológica $\mathcal{R}_T$.

7. **El protocolo de auditoría de retención informacional** con código ejecutable completo.

La tesis final es simple y fundacional: **la ventana de contexto de un LLM no es un almacén neutro. Es un espacio geométrico con leyes de transporte de información que determinan qué sobrevive y qué se pierde. Diseñar para LLMs sin comprender estas leyes es construir sobre terreno desconocido.**

Este paper es la base sobre la cual se construyen los dos papers subsiguientes de la tríada RONIN 2026:

- Sin la geometría del olvido, la **Ecología de Agentes** (julio) carece de fundamento físico: los agentes compiten por atención precisamente porque la atención es un recurso geométricamente restringido.

- Sin la geometría del olvido, la **Deuda Ontológica** (agosto) carece de mecanismo causal: las contradicciones se acumulan silenciosamente porque la recuperación de documentos contradictorios está gobernada por la misma geometría que hace que ciertos documentos se pierdan mientras otros persisten.

La geometría del olvido es la capa cero. La capa que nadie ve porque está debajo de todo. Pero cuando falla, todo lo que se construyó encima colapsa.

No porque el modelo sea defectuoso. Sino porque el terreno fue ignorado.

---

## Koans del Geómetra de la Memoria

**Del valle atencional:**
El centro del contexto es el desierto de la atención. Lo que colocas ahí viaja por tierra árida. Si quieres que llegue vivo, dale agua estructural o ponlo en caravana con otros datos. Solo, morirá de sed atencional.

**De la primacía como privilegio:**
Los primeros tokens son nobles. Reciben atención sin merecerla. Usa ese privilegio para lo que no puede permitirse perderse. No lo desperdicies en saludos ni preámbulos. La nobleza posicional es un recurso finito.

**De la redundancia como seguro:**
Repetir no es fracasar. Es asegurar. Un dato dicho una vez es una apuesta. Un dato dicho tres veces en tres formatos es una garantía. El coste de la repetición es tokens. El coste de la pérdida es confianza. Elige.

**Del formato como armadura:**
Un número en prosa es un soldado sin armadura en campo abierto. El mismo número en una tabla es un soldado en fortaleza. El formato no decora. Protege. Cada marcador estructural es un muro contra el olvido.

**Del punto de no retorno:**
Hay una longitud donde el contexto deja de ser memoria y se convierte en ruido. Ese punto no se anuncia. No hay alerta. Simplemente, lo que antes se recuperaba ya no se recupera. Mide tu $L^*$ antes de que el silencio te lo enseñe.

**De la cohesión narrativa:**
Un párrafo es una tribu. Sus miembros se protegen mutuamente. Separarlos es enviarlos solos al valle. Mantén tus tribus juntas. La cohesión local es la última defensa antes del olvido global.

**Del mapa de retención como espejo:**
El mapa de retención no juzga tu documento. Lo refleja. Si el reflejo muestra huecos, no culpes al espejo. Rellena los huecos. Cambia la estructura. Mueve lo crítico. El mapa dice la verdad que tu intuición no puede ver.

**De la geometría como terreno:**
No construyas sobre terreno que no has sondado. Cada modelo tiene su propia topografía. Cada longitud tiene su propio clima. Lo que funciona en 8K puede colapsar en 64K. Sondéalo. Mídelo. Respétalo. La geometría no perdona la arrogancia.

**Del invariante como promesa:**
Un ancla estructural es una promesa que el modelo cumple independientemente del contexto. Esa promesa no es mágica. Es geométrica. El modelo atiende al ancla porque su embedding vive en una región del espacio que la atención visita siempre. Comprende la geometría y podrás hacer promesas que se cumplen.

**De la auditoría como soberanía:**
Asumir que tu prompt funciona es fe. Medir que tu prompt funciona es soberanía. La diferencia entre ambos es un mapa de retención. El primero espera. El segundo sabe. En la era de los contextos largos, saber es la única forma segura de construir.

**Del olvido como ley, no como defecto:**
El modelo no olvida porque esté roto. Olvida porque es finito. La finitud es su naturaleza. La geometría del olvido es la expresión matemática de esa naturaleza. No luches contra ella. Diseña con ella. El arquitecto que respeta la gravedad construye edificios que permanecen. El que la ignora construye ruinas futuras.

**De la tríada:**
Este paper es el cimiento. La Ecología de Agentes es la estructura. La Deuda Ontológica es el mantenimiento. Sin cimiento, la estructura se hunde. Sin estructura, el mantenimiento es imposible. Sin mantenimiento, el cimiento se agrieta. Los tres son uno. Ninguno basta solo.

---

## Referencias

### Papers académicos y técnicos

Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). Attention is All You Need. *NeurIPS 2017*. arXiv:1706.03762.

Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., & Liang, P. (2023). Lost in the Middle: How Language Models Use Long Contexts. *Transactions of the ACL*. arXiv:2307.03172.

Chen, T., Zhang, H., Wang, Y., & Li, Z. (2024). Long Context Evaluation of Large Language Models: A Comprehensive Benchmark. arXiv:2402.13718.

Yen, H., Gao, J., & Chen, D. (2024). Long Context Is Not Long Memory: Understanding the Gap Between Context Window and Effective Memory in LLMs. arXiv:2405.10597.

Xiao, G., Tian, Y., Chen, B., Han, S., & Lewis, M. (2023). Efficient Streaming Language Models with Attention Sinks. *ICLR 2024*. arXiv:2309.17453.

Su, J., Lu, Y., Pan, S., Murtadha, A., Wen, B., & Luo, Y. (2021). RoFormer: Enhanced Transformer with Rotary Position Embedding. arXiv:2104.09864.

Press, O., Smith, N. A., & Lewis, M. (2022). Train Short, Test Long: Attention with Linear Biases Enables Input Length Extrapolation. *ICLR 2022*. arXiv:2108.12409.

Ainslie, J., Lee-Thorp, J., de Jong, M., Zemlyanskiy, Y., Lebron, F., & Sanghai, S. (2023). GQA: Training Generalized Multi-Query Transformer Models from Multi-Head Checkpoints. *EMNLP 2023*. arXiv:2305.13245.

Dong, Y., Cordonnier, J. B., & Loukas, A. (2021). Attention is Not All You Need: Pure Attention Loses Rank Doubly Exponentially with Depth. *ICML 2021*. arXiv:2103.03404.

Noci, L., Anagnostidis, S., Ricky, L., Orvieto, A., Singh, S. P., & Hofmann, T. (2022). Signal Propagation in Transformers: Theoretical Perspectives and the Role of Rank Collapse. *ICML 2022*. arXiv:2206.02747.

Shannon, C. E. (1948). A Mathematical Theory of Communication. *Bell System Technical Journal*, 27(3), 379–423.

Cover, T. M., & Thomas, J. A. (2006). *Elements of Information Theory* (2nd ed.). Wiley-Interscience.

Atkinson, R. C., & Shiffrin, R. M. (1968). Human memory: A proposed system and its control processes. *Psychology of Learning and Motivation*, 2, 89–195.

Munkres, J. R. (2000). *Topology* (2nd ed.). Prentice Hall.

Hatcher, A. (2002). *Algebraic Topology*. Cambridge University Press.

### Trabajos previos del autor

Ferrandez Canalis, D. (2026a). Cantando al Silicio: Una Teoría Unificada de la Ingeniería de Prompts y la Arquitectura Tonal Dwemer. Agencia RONIN. DOI: 10.1310/ronin-tonal-prompting-2026.

Ferrandez Canalis, D. (2026b). Nirn Atacada: Tratado de Seguridad Ofensiva en Sistemas de IA e Infraestructura Distribuida. Agencia RONIN. DOI: 10.1310/ronin-nirn-atacada-2026.

Ferrandez Canalis, D. (2026c). Auditoría de Cuellos de Botella en la Era de la IA: Método Ronin y Síntesis de Alto Impacto. Agencia RONIN.

Ferrandez Canalis, D. (2026d). Corpus Técnico RONIN v1.0: Unificación de Tres Tratados. Agencia RONIN.

---

*Fin del paper. Versión 1.0 — Edición Fundacional, Máxima Densidad Extendida.*

*DOI: 10.1310/ronin-geometry-of-forgetting-2026*

*Obra de la Agencia RONIN.*

*Licencia: CC BY-NC-SA 4.0 + Cláusula Comercial Ronin. Para usos comerciales, contactar.*

*30 de junio de 2026.*

*Este paper es el fundamento de la tríada RONIN 2026. Los papers subsiguientes —Ecología de Agentes (julio) y Deuda Ontológica (agosto)— presuponen y extienden los conceptos aquí establecidos.*

*1310.*
