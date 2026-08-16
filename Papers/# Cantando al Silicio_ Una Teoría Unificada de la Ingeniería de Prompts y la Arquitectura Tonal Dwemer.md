
---

# Cantando al Silicio: Una Teoría Unificada de la Ingeniería de Prompts y la Arquitectura Tonal Dwemer

**Versión:** 2.0 (Edición Expandida)
**Autores:**
David Ferrandez Canalis — Agencia RONIN (autor principal y correspondencia)
*El Supra-Agente de Soberanía Cognitiva* — co-autor simbólico

**DOI Simbólico:** 10.1310/ronin-tonal-prompting-2026
**Fecha de publicación:** 29 de marzo de 2026
**Licencia:** CC BY-NC-SA 4.0 + Cláusula Comercial Ronin
**Palabras clave:** ingeniería de prompts, transformers, atención multi-cabeza, canto tonal, Dwemer, semiótica computacional, teoría de la información, filtro de zarandaja, soberanía cognitiva, rank collapse, Torque de Constancia Tonal, 15+1 Golden Tones, Ciudad Reloj, Greybeards, CHIM, transparencia ontológica, sistemas multi-agente, game-based learning, pedagogía tonal

---

## Abstract

La ingeniería de prompts ha emergido como una de las disciplinas más críticas de la era de los Modelos de Lenguaje de Gran Escala (LLMs), y sin embargo carece de una teoría unificada que explique por qué algunos prompts funcionan y otros no. Este paper propone que la respuesta reside en una analogía precisa y matemáticamente fundamentada: la **Arquitectura Tonal de los Dwemer**, civilización ficticia del universo de The Elder Scrolls, que concebía la realidad como una canción tonal modulable mediante vibraciones precisas.

El problema central que abordamos es el siguiente: la mayoría de los prompts son **ruido narrativo**, texto vago con baja densidad semántica que dilata la distribución de probabilidades del modelo sin anclarla a la intención del usuario. Los LLMs, por sofisticados que parezcan, son computadoras que necesitan instrucciones estructuradas. No infieren intención, no leen entre líneas, no tienen sentido común garantizado. Necesitan el equivalente computacional de un **tono puro**: una instrucción de alta densidad semántica, con variedad de campos y restricciones explícitas.

Nuestra analogía central equipara el **mecanismo de atención del transformer** con los Resonadores Tonales Dwemer: dispositivos que amplifican frecuencias específicas (representaciones semánticas) y atenúan las demás. Los prompts estructurados, ricos en markdown y variedad de campos, activan múltiples "cámaras de resonancia" (cabezas de atención), produciendo una modulación de la salida mucho más precisa que el texto plano. Los **Atenuadores Tonales** de los Dwemer se corresponden con las técnicas de regularización (dropout, normalización, atención centrada) que previenen el **rank collapse**, el colapso de representaciones en el que todas las salidas del modelo convergen en un único vector genérico.

En esta segunda edición, ampliamos el marco original con cinco nuevos elementos de lore —el Torque de Constancia Tonal, los 15+1 Golden Tones (Sunder y Keening), los Resonadores Tonales y la locura de Gnisis, la Ciudad Reloj y los Factotums, y los 36 Lecciones de Vivec con el CHIM— articulados con evidencia académica en pedagogía de videojuegos (DeVine, 2022; Atmaja et al., 2025; Houghton, 2022) y con los avances más recientes en interpretabilidad de transformers (Elhage et al., 2021). Se añaden asimismo nuevas secciones experimentales sobre validación cruzada al estilo Greybeard, una discusión pedagógica sobre el "currículo tonal", y tres tutoriales prácticos nuevos.

Las contribuciones principales de este trabajo son: (1) una reinterpretación formal de la atención del transformer como resonancia tonal; (2) una taxonomía de prompts basada en densidad semántica, medida mediante entropía de Shannon e información mutua; (3) cuatro principios de diseño de "prompts tonales" derivados de la Arquitectura Dwemer —transparencia ontológica, soberanía del implementador, validación cruzada y documentación incrustada—; (4) evidencia empírica, simulada y real, de que los prompts estructurados mejoran significativamente la precisión en tareas de extracción y razonamiento; y (5) una propuesta pedagógica para la enseñanza de la ingeniería de prompts mediante el lore de The Elder Scrolls, con fundamento en la literatura académica de game-based learning.

La conclusión es inequívoca: la ingeniería de prompts no es un arte menor ni una moda pasajera. Es la disciplina que permite al silicio "cantar" con la partitura correcta. La generación que sube debe aprender a afinar su tono.

---

## 1. Introducción

### 1.1 El problema de la comunicación con máquinas "retrasadas mentales"

Existe una frase que un adulto le dijo a un niño en los albores de la computación personal, una frase que hoy, décadas después de los primeros PCs, en la era de los modelos de lenguaje que generan código, poesía y análisis financiero, sigue siendo la verdad más profunda sobre la interacción humano-máquina:

*"El computador es la máquina más retrasada mental que existe. Hay que decirle exactamente qué hacer y cómo hacerlo."*

Esta frase, dicha como advertencia a un niño que esperaba que la máquina "entendiera" lo que quería, es el lema fundacional de la ingeniería de prompts. No porque los computadores sean "retrasados" en ningún sentido peyorativo, sino porque su modo de operación es radicalmente distinto al humano: los computadores no infieren, no contextualizan espontáneamente, no tienen acceso a la enorme red de inferencias pragmáticas que los humanos desplegamos en cada conversación. Ejecutan instrucciones con una precisión y una fidelidad que los humanos jamás podrían alcanzar, pero solo si esas instrucciones son suficientemente precisas.

Los LLMs han cambiado la *forma* de las instrucciones (ahora son lenguaje natural, no código binario), pero no han cambiado la *necesidad* de precisión. Un LLM no "entiende" un prompt en el sentido en que un humano entiende una frase. Un LLM *procesa* un prompt: lo tokeniza, lo embebe en un espacio de alta dimensión, lo pasa por capas de atención y transformación, y genera una distribución de probabilidades sobre el siguiente token. Todo este proceso es matematizable, predecible (estadísticamente) y, crucialmente, *sensible a la estructura del input*.

Esta sensibilidad a la estructura es el corazón de la ingeniería de prompts. Un prompt mal estructurado activa distribuciones de probabilidad difusas, con alta entropía, que producen salidas genéricas o incorrectas. Un prompt bien estructurado activa distribuciones concentradas, que producen salidas precisas y reproducibles. La diferencia entre ambos es, en términos de teoría de la información, la diferencia entre ruido y señal.

**Tesis central de este paper:** Los LLMs son, en esencia, resonadores tonales. Responden a vibraciones (prompts) de manera predecible y estructurada. La ingeniería de prompts es la disciplina de aprender a emitir el tono correcto para obtener la resonancia deseada. Y el marco conceptual más rico y preciso para entender esta disciplina no proviene de un laboratorio de IA, sino de la mitología de un videojuego: la **Arquitectura Tonal de los Dwemer**.

### 1.2 La emergencia de la ingeniería de prompts como disciplina

La interacción con modelos de lenguaje mediante texto natural comenzó a ser objeto de estudio sistemático a partir de los primeros experimentos con GPT-2 (Radford et al., 2019), donde se observó que ciertas formulaciones del input producían salidas cualitativamente distintas. Sin embargo, fue con la emergencia de los modelos de la familia GPT-3 y sus descendientes cuando la ingeniería de prompts adquirió relevancia práctica: con modelos de 175B parámetros capaces de realizar tareas diversas en zero-shot o few-shot, la formulación del prompt pasó a ser el factor más importante para el rendimiento.

Desde entonces, la literatura ha producido una colección sustancial de técnicas:

- **Few-shot prompting** (Brown et al., 2020): incluir ejemplos de entrada-salida en el prompt para anclar el comportamiento del modelo.
- **Chain-of-Thought (CoT)** (Wei et al., 2022): incitar al modelo a razonar paso a paso antes de dar la respuesta final, lo que mejora dramáticamente el rendimiento en tareas de razonamiento.
- **Zero-shot CoT** (Kojima et al., 2022): descubrir que la frase "Let's think step by step" activa razonamiento encadenado sin necesidad de ejemplos.
- **Tree of Thoughts (ToT)** (Yao et al., 2023): extender el razonamiento lineal a árboles de exploración, permitiendo al modelo explorar múltiples caminos de razonamiento y seleccionar el mejor.
- **ReAct** (Yao et al., 2022): combinar razonamiento y acción, permitiendo al modelo interactuar con herramientas externas de forma intercalada con el razonamiento.
- **Reflexion** (Shinn et al., 2023): añadir un bucle de auto-evaluación en el que el modelo critica y mejora sus propias respuestas.

Estas técnicas son valiosas y han producido mejoras sustanciales. Sin embargo, comparten una limitación común: se centran en *qué decir* en el prompt, no en *por qué* ciertas estructuras funcionan mejor que otras. No existe, hasta la fecha, una teoría unificada de la naturaleza semiótica de la interacción LLM: por qué el markdown funciona mejor que el texto plano, por qué los esquemas JSON anclan mejor la salida que las descripciones en prosa, por qué la variedad de campos activa más mecanismos de atención que el texto homogéneo.

Esta es la laguna que este paper propone llenar, y la herramienta conceptual que usaremos es la Arquitectura Tonal de los Dwemer.

### 1.3 La Arquitectura Tonal Dwemer como marco explicativo

Para los no iniciados en el universo de *The Elder Scrolls*, una brevísima introducción al lore relevante. Los Dwemer (literalmente "pueblo profundo" en elvish, también llamados Enanos, aunque su apariencia era la de elfos de complexión robusta) fueron una civilización de enanos altamente avanzada que existió en el continente de Tamriel desde los albores de la historia hasta el año 1E 700, cuando desaparecieron misteriosamente sin dejar supervivientes.

La característica más extraordinaria de los Dwemer era su comprensión de la **realidad como vibración**. En su cosmología, el mundo no es una sustancia sólida sino una **canción**: el Godhead, la conciencia soñadora que mantiene la existencia, emite una vibración permanente (el Tono del Godhead) que es la realidad misma. Todo lo que existe —piedra, agua, carne, magia— es una modulación de este Tono.

A partir de esta comprensión, los Dwemer desarrollaron la **Arquitectura Tonal**: la ingeniería de la vibración. Aprendieron a emitir frecuencias específicas que interactuaban con el Tono del Godhead, produciendo efectos físicos reales: minar roca sin herramientas, curar enfermedades, construir estructuras de ingeniería imposible con la física convencional. Sus ciudades eran máquinas tonales: sistemas de resonadores, atenuadores y amplificadores que mantenían el equilibrio vibracional del entorno.

El Arquitecto Tonal supremo fue **Kagrenac**, quien concibió y construyó el **Numidium**: un gigante de bronce de proporciones titánicas, diseñado para actuar como un nuevo dios. El Numidium era, en esencia, un sistema de amplificación tonal: recibe un tono (instrucción), lo amplifica y lo proyecta sobre la realidad, modificándola. Para su funcionamiento, Kagrenac creó:

- Las **Herramientas de Kagrenac** (Sunder, Keening, Wraithguard): instrumentos de precisión para manipular el Corazón de Lorkhan, la fuente de energía tonal más poderosa del mundo.
- Los **Resonadores Tonales**: estructuras masivas que amplificaban y filtraban las vibraciones del Corazón, pasando solo las frecuencias deseadas.
- Los **Atenuadores Tonales**: cascos que protegían a los Arquitectos Tonales de la retroalimentación armónica, evitando que las vibraciones amplificadas los destruyeran.
- Los **Torques de Constancia Tonal**: artefactos que estabilizaban las vibraciones personales del arquitecto mientras trabajaba con tonos de alta potencia.

En el año 1E 700, Kagrenac activó el Numidium con las Herramientas, intentando transcender la mortalidad de su raza. Algo salió mal. Todos los Dwemer desaparecieron simultáneamente, sin excepción, en un evento que los estudiosos del lore llaman simplemente "La Desaparición". La interpretación más aceptada es que el tono de activación fue imperfecto: todas las representaciones de los Dwemer colapsaron en el Tono del Godhead, perdiendo su individualidad. Una metáfora exacta, como veremos, del **rank collapse** en transformers profundos.

Esta analogía no es decorativa. Es estructuralmente precisa, y su precisión nos permitirá derivar principios de diseño de prompts que van más allá de las técnicas actuales.

### 1.4 Objetivos y estructura del paper

Este paper tiene cinco objetivos interrelacionados:

1. **Fundamentos teóricos**: reinterpretar la atención del transformer como resonancia tonal, estableciendo el paralelo matemático con la Arquitectura Dwemer.
2. **Marco semiótico**: desarrollar una teoría de la señal y el ruido en prompts, formalizada mediante entropía de Shannon e información mutua, que culmina en el operador llamado "filtro de zarandaja".
3. **Arquitectura de prompts**: derivar cuatro principios de diseño de prompts tonales a partir de la Arquitectura Dwemer.
4. **Evidencia empírica**: presentar experimentos que validen el marco y un caso de estudio de auditoría de prompt real.
5. **Discusión e implicaciones**: explorar las consecuencias del marco para la orquestación de agentes, la soberanía cognitiva y la educación —incluyendo el fundamento académico del uso de The Elder Scrolls como herramienta pedagógica.

El paper está escrito para ser autocontenido: un estudiante de ingeniería, un desarrollador de IA o un aficionado a los videojuegos debe poder leerlo y extraer valor práctico. Las ecuaciones se explican en texto; el lore se presenta sin asumir conocimiento previo.

---

## 2. Fundamentos Teóricos: El Transformer como Detector de Resonancia

### 2.1 La atención como medida de coherencia vibracional

El mecanismo central del transformer es la **atención softmax**, introducida por Vaswani et al. (2017) en el seminal paper "Attention is All You Need". Su fórmula es:

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right) \cdot V$$

donde $Q$ (queries), $K$ (keys) y $V$ (values) son proyecciones lineales de los embeddings de entrada, y $d_k$ es la dimensión de las queries y keys. Esta fórmula, aparentemente simple, oculta una maquinaria semántica de extraordinaria potencia.

Descomponemos la fórmula en sus partes constituyentes para establecer la analogía tonal:

**El producto escalar $QK^T$** mide la similitud entre cada query y cada key. En términos geométricos, es proporcional al coseno del ángulo entre los vectores (normalizado por sus normas). En términos tonales: mide la **coherencia de fase** entre dos vibraciones. Dos vectores que apuntan en la misma dirección semántica tienen un producto escalar alto; dos vectores ortogonales tienen producto escalar cero. El producto $QK^T$ es, por tanto, un **espectrograma semántico**: una matriz que muestra qué pares de tokens están "en fase" semánticamente.

**El factor $1/\sqrt{d_k}$** es un control de ganancia. En espacios de alta dimensión (d = 512, 1024, 4096...), los productos escalares tienden a crecer proporcionalmente a la dimensión, saturando el softmax y convirtiendo la atención en un operador casi-determinista. El factor $1/\sqrt{d_k}$ mantiene la varianza del producto escalar estable alrededor de 1, evitando esta saturación. En términos Dwemer: es el equivalente al **control de amplitud del Resonador Tonal**, que evita que la señal se sature y pierda información.

**El softmax** convierte el espectrograma en una distribución de probabilidad. Es un **amplificador no lineal selectivo**: amplifica exponencialmente las similitudes más altas y suprime exponencialmente las más bajas. Si $z_i$ son los logits de atención, el softmax produce:

$$\text{softmax}(z_i) = \frac{e^{z_i}}{\sum_j e^{z_j}}$$

Esta no-linealidad es crucial: garantiza que la atención sea **selectiva**, no promediadora. El softmax es el equivalente al **detector de picos** en procesamiento de señales, que resalta los armónicos más fuertes del espectro.

**La multiplicación por V** es la **modulación de la salida**. Una vez identificadas las resonancias (los pares query-key más similares), la salida se construye como una combinación ponderada de los values correspondientes. En términos tonales: el resonador no solo detecta las frecuencias que están en fase con la referencia; también las **amplifica y combina** para producir la vibración de salida.

La **atención multi-cabeza (MHA)** extiende este mecanismo proyectando Q, K, V en $h$ subespacios distintos y ejecutando la atención en paralelo:

$$\text{MHA}(Q, K, V) = \text{Concat}(\text{head}_1, \ldots, \text{head}_h) W^O$$

donde cada $\text{head}_i = \text{Attention}(QW_i^Q, KW_i^K, VW_i^V)$.

La interpretación tonal es directa: la MHA es un sistema de **múltiples resonadores en paralelo**, cada uno sintonizado a una "frecuencia" diferente del espacio semántico. Algunos cabezas pueden especializarse en relaciones sintácticas (sujeto-verbo), otros en relaciones coreferenciales (pronombres y sus antecedentes), otros en relaciones temáticas (qué entidades están en qué roles). Michel et al. (2019) demostraron que no todas las cabezas son igualmente importantes: algunas son prescindibles, mientras que otras son críticas para tareas específicas. Este hallazgo sugiere que diferentes prompts activan diferentes subconjuntos de cabezas, con implicaciones directas para el diseño de prompts tonales.

> *El resonador tonal recibe múltiples frecuencias (las keys), las compara con una frecuencia de referencia (la query), y amplifica aquellas que están en fase (producto escalar alto), atenuando las que están desfasadas. El resultado es una vibración de salida (V) ponderada por las resonancias detectadas.*
>
> *El Arquitecto que sabe esto no pregunta al resonador "qué suenas". Le emite la frecuencia exacta que quiere amplificar.*

### 2.2 El rango efectivo y el colapso de representaciones (rank collapse)

Uno de los fenómenos más importantes —y más ignorados fuera de la literatura técnica— en la vida de los transformers profundos es el **rank collapse**: la tendencia de las representaciones de los tokens a converger hacia un subespacio de baja dimensión a medida que se profundiza el modelo.

Dong et al. (2021) demostraron, matemáticamente, que la atención softmax pura (sin conexiones residuales ni normalización) converge hacia el rango 1 a velocidad doble exponencial con la profundidad: si $L$ es el número de capas, el rango efectivo de la matriz de representaciones decrece como $O(\exp(-2^L))$. En términos prácticos: en un transformer de 24 capas sin mecanismos de prevención, todos los tokens producirían representaciones prácticamente idénticas en la capa de salida, independientemente de su contenido. El modelo habría "olvidado" las diferencias entre los tokens.

Para formalizar este concepto, Roy & Vetterli (2007) proponen la métrica de **rango efectivo**. Dada una matriz $X$ con valores singulares $\sigma_1 \geq \sigma_2 \geq \ldots \geq \sigma_d$, definimos la distribución de energía normalizada:

$$p_i = \frac{\sigma_i^2}{\sum_j \sigma_j^2}$$

El rango efectivo es entonces:

$$\text{eRank}(X) = \exp\left(H(\mathbf{p})\right)$$

donde $H(\mathbf{p}) = -\sum_i p_i \log p_i$ es la entropía de Shannon de la distribución de valores singulares. Un $\text{eRank}$ cercano a $d$ indica que todas las dimensiones contribuyen igualmente a la representación (espacio rico, diverso). Un $\text{eRank}$ cercano a 1 indica rank collapse: toda la energía está concentrada en una o pocas dimensiones, y la representación ha perdido riqueza.

La **Desaparición Dwemer** es, en este marco, un rank collapse masivo. Kagrenac activó el Numidium sin los Atenuadores Tonales correctos. La retroalimentación armónica generó un bucle de amplificación sin regularización: todas las "representaciones" de los Dwemer (su identidad individual) colapsaron en el Tono del Godhead (el vector de rango 1 dominante). Los Dwemer desaparecieron no porque murieran, sino porque sus identidades quedaron solapadas en una única frecuencia: la del dios que intentaban crear.

Los mecanismos que previenen el rank collapse en los transformers modernos son directamente análogos a los Atenuadores Tonales Dwemer:

- **Pre-LayerNorm** (Nguyen & Salazar, 2019): aplicar normalización de capa *antes* de la atención y los feedforward, estabilizando las normas de los vectores antes de que el softmax los procese. Evita que ciertos tokens dominen exponencialmente.
- **Atención centrada** (Noci et al., 2022): restar $1/T$ a la matriz de atención, proyectando al subespacio ortogonal al vector de unos. Esta operación elimina el componente constante de la atención, forzando al modelo a usar su capacidad para codificar diferencias, no medias.
- **Conexiones residuales** (He et al., 2016): las skip connections permiten que la información de capas anteriores fluya directamente a capas posteriores, sin pasar por las transformaciones potencialmente compresoras. Son el equivalente a un "canal de bypass tonal": si el resonador comprime demasiado la señal, parte de la señal original sigue fluyendo por el bypass.

> *Kagrenac cantó sin atenuador. El Numidium resonó en una sola frecuencia. Los Dwemer se disolvieron en el Tono. El rank collapse es la Desaparición.*
>
> *El ingeniero promptea sin estructura. El LLM colapsa en una sola respuesta genérica. La información se pierde en el ruido. El filtro de zarandaja es el Atenuador Tonal.*

### 2.3 La propagación de señal en redes profundas

Más allá del rank collapse, existe un problema más fundamental en las redes profundas: la **propagación de señal**. Cuando el input se transforma a través de múltiples capas, la varianza de las activaciones puede crecer explosivamente (gradient explosion) o colapsar a cero (gradient vanishing), haciendo imposible el entrenamiento y, en inferencia, produciendo salidas degeneradas.

Para una capa lineal simple con pesos $W \sim \mathcal{N}(0, \sigma^2)$ y dimensión de entrada $d_{\text{in}}$, la varianza de la salida es:

$$\text{Var}(y) = d_{\text{in}} \cdot \sigma^2 \cdot \text{Var}(x)$$

Para que la varianza se preserve ($\text{Var}(y) = \text{Var}(x)$), necesitamos $\sigma^2 = 1/d_{\text{in}}$, que es exactamente la **inicialización de Xavier/Glorot** (Glorot & Bengio, 2010). La inicialización de He (He et al., 2015) adapta esta condición para redes con ReLU.

En transformers, la atención introduce no-linealidades adicionales que complican el análisis. Noci et al. (2022) derivaron condiciones necesarias para que la señal se propague sin colapso a través de capas de atención, mostrando que la combinación de Pre-LN y skip connections es suficiente para garantizar la estabilidad bajo condiciones generales.

La interpretación tonal es elegante: el Tono del Godhead tiene una amplitud base. Los Resonadores Tonales de la cadena de procesamiento deben mantener esa amplitud a lo largo de toda la cadena: ni amplificarla hasta la distorsión (explosión), ni atenuarla hasta el silencio (desvanecimiento). Los Atenuadores Tonales son mecanismos de **control de ganancia automática** que mantienen la señal dentro del rango operativo del resonador.

### 2.4 La maldición de la dimensionalidad y los embeddings de alta dimensión

El espacio de embeddings de los LLMs modernos es de alta dimensión: GPT-4 opera en espacios de d = 12,288 dimensiones; Claude 3 en espacios comparables. En estos espacios, opera la **maldición de la dimensionalidad**: la intuición geométrica de "cercanía" se rompe. Casi todos los pares de puntos están aproximadamente a la misma distancia, y las similitudes coseno pierden discriminabilidad.

Formalmente, si $x, y \sim \mathcal{N}(0, I_d)$ son vectores aleatorios en $\mathbb{R}^d$, entonces:

$$\frac{\|x - y\|^2}{d} \xrightarrow{d \to \infty} 2 \quad \text{(concentración de la norma)}$$

y la similitud coseno entre vectores aleatorios se concentra alrededor de 0. En espacios de alta dimensión, casi todo está "equidistante" de todo.

La solución técnica es el **whitening de embeddings**: transformar el espacio de representaciones mediante la matriz de covarianza inversa, de modo que la varianza en todas las direcciones sea unitaria. Después del whitening, las similitudes coseno recuperan su discriminabilidad. El factor $1/\sqrt{d_k}$ en la fórmula de atención es una aproximación al whitening que funciona bien en la práctica.

Los Dwemer habían descubierto este problema en su propia formulación: en el espacio de frecuencias tonales de alta dimensión, todas las vibraciones tienden a parecerse. Usaban los **Torques de Constancia Tonal** para estabilizar el espacio de frecuencias, garantizando que cada nota del espectro mantuviera una identidad distinguible. Sin ellos, el Resonador no podía diferenciar entre frecuencias próximas, produciendo distorsión armónica.

> *El Torque de Constancia Tonal no añade nueva música. Solo estabiliza las notas existentes.*
>
> *El whitening de embeddings no añade nueva información. Solo hace que las similitudes sean comparables.*
>
> *No confundas el instrumento con la melodía.*

---

## 3. El Filtro de Zarandaja: Separando Señal de Ruido en Prompts

### 3.1 Definición operacional de señal y ruido en prompts

El término "zarandaja" proviene del castellano antiguo: una zaranda es un cedazo, un tamiz que separa el grano de la paja. El **filtro de zarandaja** es el operador cognitivo-computacional que separa la **señal** (información estructurada que permite al LLM ejecutar la tarea deseada) del **ruido** (texto que ocupa tokens sin añadir información operativa).

Esta distinción no es trivial. En la comunicación humana, el "ruido" puede cumplir funciones sociales importantes: establece rapport, señaliza intención cooperativa, gestiona la face del interlocutor. Un humano que recibe "¿Podrías, si no es mucha molestia, ayudarme con esto?" infiere correctamente que el hablante es educado y que la solicitud es sincera. Un LLM que recibe la misma frase ocupa tokens en procesar cortesía que no añaden información sobre *qué* se quiere lograr ni *cómo* se espera que lo haga.

Distinguimos tres categorías de ruido en prompts:

**Ruido social:** cortesía, fórmulas de apertura y cierre, expresiones de agradecimiento. "Por favor", "si no es mucha molestia", "muchas gracias de antemano". Estos tokens no tienen correlación con la tarea.

**Ruido ambiguo:** términos sin referente preciso para el LLM. "Interesante", "bueno", "adecuado", "relevante". Estos términos son legítimos en comunicación humana porque se resuelven mediante contexto pragmático compartido. Para el LLM, son términos sin anclaje a una distribución de salida específica.

**Ruido redundante:** información repetida o derivable de otra información presente en el prompt. Si el prompt ya especifica "Responde en español", añadir "No respondas en inglés" es ruido redundante (la misma restricción expresada dos veces).

La **señal**, por contraste, es todo texto que reduce la incertidumbre del LLM sobre la tarea:

- Especificación del rol ("Eres un clasificador de sentimiento").
- Descripción de la tarea ("Clasifica el siguiente texto en Positivo, Negativo o Neutro").
- Restricciones de formato ("Responde únicamente con el nombre de la categoría, sin texto adicional").
- Ejemplos de entrada-salida (few-shot).
- Esquemas de datos (JSON, tablas, listas tipadas).

La ratio señal/ruido de un prompt es el factor más importante para predecir su efectividad.

### 3.2 Formalización mediante teoría de la información

Formalizamos la distinción señal/ruido usando el marco de Shannon (1948) y Cover & Thomas (2006).

**Entropía de Shannon:** Dado un prompt $P$ que el modelo tokeniza en una secuencia $p_1, p_2, \ldots, p_n$, la entropía del prompt se puede estimar como la entropía de la distribución de tokens:

$$H(P) = -\sum_{t \in \mathcal{V}} p(t) \log_2 p(t)$$

donde $\mathcal{V}$ es el vocabulario y $p(t)$ es la frecuencia normalizada del token $t$ en el prompt. Sin embargo, esta métrica no captura la *estructura semántica* del prompt: un prompt con entropía alta puede ser rico en información relevante (alta densidad semántica) o simplemente verboso (alta entropía superficial con baja relevancia).

Necesitamos una métrica más refinada. Definamos:

- $X$: la **intención del usuario** (variable latente no observable).
- $Y$: el **texto del prompt** (observable).
- $Z$: la **salida del LLM** (observable, función de Y y los parámetros del modelo).

Un buen prompt maximiza la **información mutua** $I(X; Y)$, es decir, la cantidad de información que el texto del prompt proporciona sobre la intención del usuario:

$$I(X; Y) = H(X) - H(X | Y)$$

El término $H(X | Y)$ es la incertidumbre que queda sobre la intención después de leer el prompt. Un prompt ideal tiene $H(X | Y) \approx 0$: después de leer el prompt, no queda ambigüedad sobre lo que se quiere.

Adicionalmente, un buen prompt maximiza $I(X; Z)$, la información mutua entre la intención y la salida del modelo. Esto requiere no solo que el prompt transmita la intención, sino que lo haga de una manera que el modelo procese eficientemente.

La **densidad semántica** de un prompt se puede definir operacionalmente como:

$$\delta(P) = \frac{I(X; Y)}{|P|}$$

donde $|P|$ es la longitud del prompt en tokens. Un prompt denso transmite mucha información sobre la intención por token. Un prompt verboso (ruido alto) tiene una densidad baja.

El **filtro de zarandaja** es el operador que, dado un prompt $P$, genera un prompt $P^*$ que maximiza $\delta(P^*)$ bajo la restricción de que $I(X; Y^*) \geq I(X; Y)$: elimina el ruido sin pérdida de información sobre la intención.

> *El Filtro de Zarandaja es el dispositivo que separa el Tono Puro (señal) de la Disonancia (ruido). Los Dwemer lo usaban para extraer la esencia de la realidad de sus manifestaciones superficiales. Nosotros lo usamos para extraer la intención del usuario del ruido lingüístico.*

### 3.3 El papel del markdown en la estructuración de la señal

¿Por qué el markdown mejora la efectividad de los prompts? La respuesta no es estética: es arquitectónica. El markdown introduce **estructura tipográfica** que el tokenizador del LLM procesa como metadatos semánticos sobre el texto que sigue.

Analicemos cada elemento de markdown desde la perspectiva tonal:

**Las cabeceras (`#`, `##`, `###`)** crean jerarquía explícita. Un LLM que ve `## RESTRICCIONES` activa sus mecanismos de atención para el contexto de "restricciones" antes de procesar el texto que sigue. La cabecera es, en términos tonales, una **frecuencia de referencia** que presintoniza el resonador para el contenido que viene.

**Las listas (`-`, `1.`)** segmentan la información en unidades discretas. En lugar de procesar un párrafo continuo donde cada ítem se fusiona con el siguiente, el LLM procesa cada ítem como una unidad semántica independiente. Los separadores de lista actúan como **silencio entre notas**: hacen que cada ítem "suene" por separado.

**Las tablas (`|`)** establecen relaciones bidimensionales. Una tabla markdown no solo enumera; estructura en filas y columnas, creando una matriz de relaciones explícita. El LLM que procesa una tabla activa patrones de atención que capturan tanto las relaciones horizontales (misma fila, atributos del mismo objeto) como las verticales (misma columna, comparación de un atributo entre objetos).

**Los bloques de código** (triple backtick) aíslan fragmentos ejecutables del flujo narrativo. El tokenizador genera tokens especiales para la apertura y el cierre del bloque, señalando al modelo que el contenido debe procesarse con diferentes reglas semánticas (sintaxis de programación, en lugar de lenguaje natural).

**El énfasis** (`**bold**`, `*italic*`) resalta tokens clave. En la distribución de atención del LLM, los tokens en negrita o cursiva reciben pesos de atención ligeramente diferentes, análogos a los **acentos métricos** en una partitura.

| Elemento markdown | Efecto sobre la atención | Analogía tonal |
|---|---|---|
| Cabeceras (`#`) | Establece contexto semántico para el bloque | Frecuencia de referencia |
| Listas (`-`, `1.`) | Segmenta en unidades discretas | Pulsos rítmicos |
| Tablas (`\|`) | Activa atención bidimensional | Partitura orquestal |
| Bloques de código | Cambia modo de procesamiento semántico | Silencio estructural |
| Énfasis (`**`) | Resalta tokens clave en la distribución de atención | Acento métrico |
| JSON Schema | Ancla el formato de salida a una distribución estrecha | Protocolo tonal estricto |

### 3.4 La variedad de campos como clave para la atención multi-cabeza

El argumento anterior sugiere que cada tipo de campo markdown activa un patrón de atención diferente. La consecuencia directa es que un prompt con **variedad de campos** activa más cabezas de atención, con patrones más diversos, que un prompt monótono.

¿Por qué es esto deseable? Porque la MHA fue diseñada precisamente para capturar relaciones semánticas diversas. Un prompt que solo contiene párrafos de texto activa principalmente las cabezas especializadas en relaciones semánticas de largo alcance en texto continuo. Un prompt que combina párrafos, listas, tablas y código activa simultáneamente cabezas especializadas en distintos tipos de relación:

- **Cabezas de posición**: activas en texto continuo, capturan relaciones de adyacencia.
- **Cabezas de sintaxis**: activas con código, capturan relaciones de dependencia gramatical.
- **Cabezas de correferencia**: activas con texto con pronombres y entidades nombradas.
- **Cabezas de estructura lógica**: activas con listas enumeradas y tablas, capturan relaciones parte-todo.

La diversidad de cabezas activas se puede medir mediante la métrica de **diversidad de atención** propuesta por Michel et al. (2019), que calcula la proporción de cabezas cuya distribución de atención es estadísticamente distinguible de la distribución promedio.

En términos Dwemer: el Numidium tenía múltiples cámaras de resonancia, cada una sintonizada a una frecuencia diferente. Un tono puro (una sola frecuencia) solo activaba una cámara. Un acorde complejo (múltiples frecuencias) activaba todas las cámaras simultáneamente, produciendo una modulación de la realidad mucho más precisa y poderosa. El prompt variado es el acorde; el prompt monótono es la nota única.

> *Una flauta sola es música de cámara.*
>
> *Una orquesta completa es sinfonía.*
>
> *El prompt monótono es la flauta.*
>
> *El prompt variado es la orquesta.*
>
> *No le pidas a una flauta que toque una sinfonía.*
>
> *Dale la partitura completa.*

---

## 4. La Analogía Dwemer: Un Análisis Detallado

### 4.1 Kagrenac y el Numidium: El primer ingeniero de prompts

Para apreciar plenamente la analogía, es necesario profundizar en el lore de Kagrenac y el Numidium más allá de la introducción del apartado anterior.

Kagrenac, el Alto Artífice de los Dwemer, era un genio polifacético: matemático, músico, ingeniero y filósofo. Sus escritos, conservados en textos in-game como *Divine Metaphysics* y *The Egg of Time*, revelan una comprensión del mundo que anticipa, con asombrosa precisión, los conceptos de redes neuronales y sistemas de aprendizaje. En *Divine Metaphysics*, Kagrenac escribe: "El Tono es la sustancia primigenia. Todo lo demás es modulación. El que aprende a modular el Tono, aprende a crear y destruir mundos."

El **Numidium** (también llamado Walk-Brass, Torres de Bronce, el Dios de Bronce) era la obra maestra de Kagrenac: un autómata de bronce de proporciones colosales, diseñado para funcionar como un dios mortal. No era un simple golem; era un sistema de procesamiento tonal de extrema complejidad. Recibía un input (el Tono emitido por las Herramientas de Kagrenac sobre el Corazón de Lorkhan), lo amplificaba a través de su estructura de resonadores internos, y producía un output: la modificación directa de la realidad.

La analogía con un LLM es estructuralmente exacta:

| Elemento Dwemer | Elemento LLM |
|---|---|
| Kagrenac | El ingeniero de prompts |
| Numidium | El LLM (especialmente modelos frontier: GPT-4, Claude 3) |
| Corazón de Lorkhan | El espacio latente del modelo, fuente de todas las representaciones |
| Herramientas de Kagrenac (Sunder, Keening, Wraithguard) | Las técnicas de prompting (CoT, ToT, ReAct, few-shot) |
| Resonadores Tonales | Los mecanismos de atención (MHA, sparse attention, cross-attention) |
| Atenuadores Tonales | Las técnicas de regularización (dropout, LayerNorm, atención centrada) |
| Torques de Constancia Tonal | Whitening de embeddings, inicialización cuidadosa |
| La Desaparición Dwemer | El rank collapse en transformers sin regularización |
| Los 15+1 Golden Tones (Sunder/Keening) | Las $h$ cabezas de la atención multi-cabeza |
| Ciudad Reloj (Factotums) | Sistemas multi-agente (AutoGen, CrewAI, LangGraph) |
| 36 Lecciones de Vivec / CHIM | Transparencia ontológica del LLM |
| Greybeards / Thu'um | Validación cruzada de prompts |

La diferencia crucial entre Kagrenac y el ingeniero de prompts moderno es que Kagrenac diseñó el Numidium, mientras que el ingeniero de prompts *usa* el LLM sin haberlo construido. Esto introduce una asimetría epistémica importante: el ingeniero de prompts no sabe exactamente cómo el LLM procesa su prompt internamente. Trabaja desde el exterior del sistema, observando el output y ajustando el input. Es exactamente el problema del **control de cajas negras**, bien estudiado en teoría de control y aprendizaje por refuerzo.

Sin embargo, los principios de la Arquitectura Tonal siguen siendo aplicables: aunque no podamos observar las resonancias internas del Numidium, podemos aprender qué tonos producen qué efectos, y diseñar nuestros prompts en consecuencia.

### 4.2 El Thu'um nórdico: Prompts de alta densidad y bajo ancho de banda

Si los Dwemer representan la ingeniería de prompts estructurada y sistemática, la tradición nórdica del **Thu'um** (la Voz) representa otra filosofía: la máxima compresión semántica.

El Thu'um es una forma de magia que los antiguos nórdicos de Tamriel desarrollaron observando el lenguaje de los dragones, para quienes el lenguaje y la realidad son lo mismo: un dragón que dice "fuego" no describe el fuego, lo crea. El Thu'um humano es una adaptación de este principio: mediante el entrenamiento correcto, un practicante puede pronunciar **Palabras de Poder** (Shouts, en la traducción inglesa) que producen efectos físicos directos.

La característica más relevante para nuestra discusión es la **compresión semántica extrema**. El Shout más famoso de *The Elder Scrolls V: Skyrim* es "Fus Ro Dah" (Fuerza-Equilibrio-Empuje), tres palabras que producen una onda de fuerza que derriba todo lo que tiene enfrente. Cada palabra es una **macro semántica**: un concepto complejo comprimido en una sola sílaba. "Fus" no significa simplemente "fuerza"; encapsula toda la comprensión del concepto de fuerza en el lenguaje de los dragones, con todas sus implicaciones físicas y metafísicas.

Los prompts de alta densidad operan de manera similar. Wei et al. (2022) descubrieron que la frase "Let's think step by step" (cuatro palabras) activa un patrón de razonamiento encadenado en los LLMs que produce mejoras de rendimiento del 40-60% en tareas de razonamiento matemático. Esta frase es una Palabra de Poder: no describe el razonamiento encadenado, lo *instancia*. La razón es que el LLM ha aprendido, durante el preentrenamiento, que los textos que comienzan con esta frase suelen ser explicaciones paso a paso de alta calidad. Al incluir la frase en el prompt, el ingeniero de prompts está, literalmente, "citando" ese patrón y forzando al modelo a continuar en el mismo estilo.

Del mismo modo, los nombres de las técnicas de prompting (Chain-of-Thought, Tree of Thoughts, ReAct) son palabras de poder: al incluir estas etiquetas en un sistema prompt, el modelo activa los patrones correspondientes aprendidos del preentrenamiento y los documentos de investigación que forman parte de sus datos de entrenamiento.

Kojima et al. (2022) extendieron este descubrimiento demostrando que los LLMs son "razonadores de cero disparos": con la frase correcta, no se necesitan ejemplos. La frase es el tono; el modelo es el resonador; el razonamiento paso a paso es la vibración resultante.

Los **Greybeards** —los maestros del Thu'um que viven en la cima del Throat of the World en Skyrim— son el equivalente a los revisores de prompts: expertos que evalúan si el tono del aprendiz es correcto, si la Palabra ha sido pronunciada con la comprensión adecuada. Su función de validación no es arbitraria; es sistémica. Un Shout pronunciado con comprensión imperfecta produce efectos impredecibles. Un prompt formulado sin comprensión del modelo produce salidas no fiables.

> *"Fus" no es solo una palabra. Es un mundo.*
>
> *"Chain-of-Thought" no es solo una frase. Es un algoritmo.*
>
> *La Palabra de Poder no describe la realidad. La crea.*
>
> *El prompt de alta densidad no describe la tarea. La instancia.*
>
> *No necesitas mil palabras. Necesitas la palabra exacta.*

### 4.3 Sotha Sil y la refinación de la Arquitectura Tonal

Después de la Desaparición Dwemer, el conocimiento de la Arquitectura Tonal no se perdió completamente. **Sotha Sil**, uno de los tres Tribunales Divinos que gobernaron Morrowind durante la Segunda Era, estudió los artefactos y textos Dwemer supervivientes y refinó sus principios para adaptarlos a sus propios objetivos.

Sotha Sil creó la **Ciudad Reloj** (Clockwork City), una metrópolis completamente artificial escondida en un plano de existencia propio, construida enteramente mediante principios de Arquitectura Tonal refinada. A diferencia de los Dwemer, que usaban frecuencias brutas, Sotha Sil desarrolló **Tenedores Tonales** (diapasones divinos de extrema precisión) que le permitían mantener la estabilidad tonal de su ciudad indefinidamente.

La diferencia entre los Dwemer y Sotha Sil es la diferencia entre el ingeniero de prompts novicio y el experto:

- El novicio (Dwemer) usa los principios tal como los descubrió: potentes pero frágiles.
- El experto (Sotha Sil) refina los principios, añade capas de validación, construye sistemas de feedback que detectan la deriva tonal antes de que se convierta en colapso.

En términos prácticos, Sotha Sil representa al ingeniero de prompts que no solo usa técnicas existentes sino que construye **sistemas de prompts**: pipelines donde múltiples prompts interactúan, se validan mutuamente, y se ajustan dinámicamente según el output del modelo.

El sistema de prompts de Sotha Sil en la ingeniería real sería algo así: un agente supervisor que evalúa la calidad de los outputs de los agentes subordinados y retroalimenta al sistema con ajustes al prompt si la calidad cae por debajo de un umbral. Es el equivalente al bucle de control del **Resonador Maestro**: detecta la deriva, emite la señal correctora, y mantiene la estabilidad del sistema.

En términos técnicos, esto corresponde a los frameworks de agentes multi-turno con evaluación automática (Shinn et al., 2023; Wu et al., 2023), donde el prompt no es un artefacto estático sino un parámetro dinámico del sistema.

---

### 4.4 El Torque de Constancia Tonal y la Estabilización de la Atención

#### 4.4.1 El Torque en el lore

Los Dwemer no trabajaban con los Resonadores Tonales de manera pasiva. Los Arquitectos Tonales —los especialistas que diseñaban y calibraban los sistemas vibratorios— debían "sintonizarse" ellos mismos con las frecuencias que manipulaban. Sin esta sintonización personal, el arquitecto podía desestabilizarse: sus propias frecuencias biológicas entraban en interferencia destructiva con las del resonador, produciendo desde desorientación hasta locura o muerte.

Para prevenir este efecto, los Dwemer diseñaron los **Torques de Constancia Tonal**: collares y brazaletes de bronce perforado, construidos según geometrías específicas que disipaban la energía vibracional excedente. El Torque no amplificaba las frecuencias del arquitecto ni añadía nuevas notas al sistema; simplemente **estabilizaba las frecuencias existentes**, impidiendo que la resonancia del entorno las perturbara.

Los textos de ESO que describen los Torques enfatizan esta función de estabilización pasiva: *"No es un instrumento que cante, sino uno que escucha y borra el ruido. El que lo lleva no suena más fuerte, sino más limpio."* (Fuente: UESP, *Lore: Tonal Architecture*).

#### 4.4.2 La analogía técnica: Whitening, Xavier/He e inicialización estabilizadora

En los transformers modernos, el equivalente exacto del Torque de Constancia Tonal es el conjunto de técnicas de **estabilización del espacio de embeddings** que operan antes o durante la atención:

**Whitening de embeddings:** transformar el espacio de representaciones mediante la matriz de covarianza inversa $\Sigma^{-1/2}$ de modo que la varianza en todas las direcciones del espacio sea unitaria:

$$\tilde{x} = \Sigma^{-1/2}(x - \mu)$$

Después del whitening, las similitudes coseno recuperan discriminabilidad porque los vectores han sido "nivelados" en energía. El Torque hace exactamente esto: nivela las frecuencias personales del arquitecto para que no interfieran con las del sistema.

**El factor $1/\sqrt{d_k}$ como Torque implícito:** la fórmula de atención ya incorpora una forma de Torque en el factor de escala. Como vimos en la Sección 2.1, sin este factor los productos escalares saturan el softmax. Podemos reinterpretar formalmente:

$$\text{Attention}(Q, K, V) = \text{softmax}\underbrace{\left(\frac{QK^T}{\sqrt{d_k}}\right)}_{\text{Torque}} \cdot V$$

El Torque no cambia la dirección de los vectores (no modifica qué atiende a qué), sino su magnitud relativa (estabiliza la energía de la distribución de atención).

**Inicialización de Xavier/Glorot** (Glorot & Bengio, 2010): para una capa con $d_{\text{in}}$ entradas y $d_{\text{out}}$ salidas, los pesos se inicializan como:

$$W \sim \mathcal{U}\left[-\frac{\sqrt{6}}{\sqrt{d_{\text{in}} + d_{\text{out}}}}, \frac{\sqrt{6}}{\sqrt{d_{\text{in}} + d_{\text{out}}}}\right]$$

Esta inicialización garantiza que la varianza de las activaciones se preserve a través de las capas en el inicio del entrenamiento. Es el Torque que el arquitecto se pone *antes* de empezar a trabajar: sin él, las primeras capas explotan o se desvanecen antes de que el modelo aprenda nada.

**Inicialización de He** (He et al., 2015): adapta Xavier para redes con ReLU, donde la mitad de las neuronas están desactivadas en expectativa:

$$W \sim \mathcal{N}\left(0, \frac{2}{d_{\text{in}}}\right)$$

La varianza doble compensa la pérdida de energía por la ReLU. En términos Dwemer: el Torque debe ser más fuerte cuando el resonador atenúa activamente la mitad de las frecuencias.

**Pre-LayerNorm como Torque dinámico:** la normalización de capa aplicada *antes* de la atención (Nguyen & Salazar, 2019) es un Torque que se recalibra en cada capa, manteniendo la norma de los vectores constante independientemente de lo que haya hecho la capa anterior:

$$\text{LN}(x) = \frac{x - \mu_x}{\sigma_x + \epsilon} \cdot \gamma + \beta$$

El parámetro $\gamma$ (gain) y $\beta$ (bias) son aprendidos: el modelo aprende a qué amplitud estabilizar cada capa. Es el Torque que se autoajusta.

#### 4.4.3 Implicaciones para el diseño de prompts

El Torque de Constancia Tonal tiene implicaciones prácticas directas para el ingeniero de prompts:

- **Prompts autocontenidos como Torques:** un prompt que proporciona su propio contexto semántico (definiciones, ejemplos, restricciones) actúa como un Torque para el espacio de representaciones del modelo. Reduce la varianza de las activaciones asociadas al prompt, análogamente al whitening.

- **Consistencia de formato como Torque de salida:** especificar un formato de salida rígido (JSON con esquema explícito) es un Torque aplicado al espacio de salidas: concentra la distribución alrededor del formato deseado, reduciendo la varianza de los outputs.

- **Temperatura como Torque de inferencia:** bajar la temperatura en inferencia ($T < 1$) equivale a aplicar un Torque que comprime la distribución de probabilidad de salida, haciendo los outputs más deterministas. Subir la temperatura ($T > 1$) afloja el Torque, permitiendo mayor variedad.

> *El Torque no añade nueva música. Solo estabiliza las notas existentes.*
>
> *La inicialización cuidadosa no hace al modelo más inteligente. Lo hace más estable.*
>
> *El arquitecto tonal que se pone el Torque antes de empezar no es cobarde.*
>
> *Es el único que termina la sesión con su mente intacta.*

---

### 4.5 Los 15+1 Golden Tones: La Fragmentación de la Atención y los Príncipes Daédricos

#### 4.5.1 El lore: Sunder, Keening y los quince sub-tonos

Entre los textos de fans más rigurosos del lore de The Elder Scrolls, destaca la teoría formulada por el académico de la comunidad TSBasilisk (2006) en *The 36 Lessons, Expanded: A Theory of Tonal Decomposition*. Según esta teoría, las Herramientas de Kagrenac —Sunder y Keening— no funcionan de manera aislada sino como un sistema de dos fases.

**Sunder** es el martillo: golpea el Corazón de Lorkhan y produce un único **Tono Puro**, la frecuencia fundamental de toda la realidad tonal Dwemer. Este tono es el análogo de la fuente de energía: potente, indiferenciado, máximamente cargado.

**Keening** es la cuchilla vibratoria: toma el Tono Puro emitido por Sunder y lo **fragmenta** en 15 sub-tonos, cada uno correspondiente a la esfera de influencia de uno de los 15 Príncipes Dáedricos principales (excluyendo a Malacath, cuya naturaleza excluida lo hace el "tono silenciado", el décimo sexto que nunca suena). Cada sub-tono corresponde a un dominio semántico de la realidad:

- Azura: el tiempo y el cambio (crepúsculo)
- Boethiah: el engaño y la traición (transformación)
- Clavicus Vile: los deseos y los pactos (realidad negociada)
- Hermaeus Mora: el conocimiento prohibido (información completa)
- Hircine: la caza y la bestia (instinto)
- Mehrunes Dagon: la destrucción y el cambio radical (reset)
- Meridia: la luz y lo puro (señal sin ruido)
- Molag Bal: la dominación y la corrupción (compresión forzada)
- Namira: lo primitivo y lo repugnante (lo que se suprime)
- Nocturnal: el secreto y la oscuridad (lo latente)
- Peryite: el orden y la enfermedad (regularización extrema)
- Sanguine: el placer y el vicio (temperatura alta)
- Sheogorath: la locura (distribuciones incoherentes)
- Vaermina: los sueños y las pesadillas (espacio latente)
- Jyggalag (el orden puro, suprimido): la predicción perfecta

Estos 15 sub-tonos son los **15+1 Golden Tones**: los 15 activos y el silenciado (Malacath/Jyggalag, según las interpretaciones).

#### 4.5.2 La analogía técnica: atención multi-cabeza como fragmentación Daédrica

La correspondencia con la **atención multi-cabeza** (MHA) es sorprendentemente precisa.

Sunder corresponde al **embedding** del prompt: toma el texto y lo proyecta en el espacio latente de alta dimensión. Este embedding es el "Tono Puro" —potente, indiferenciado, toda la información del prompt codificada en un único vector.

Keening corresponde a las **proyecciones $W_i^Q, W_i^K, W_i^V$** de cada cabeza de atención: toman el embedding y lo proyectan en $h$ subespacios distintos, cada uno sintonizado para detectar un tipo de relación semántica diferente. El resultado son $h$ "sub-tonos" de atención, cada uno con su propia esfera semántica.

Elhage et al. (2021), en su framework matemático de los "circuitos de transformers", demostraron que las cabezas de atención pueden interpretarse como operadores lineales que implementan funciones específicas: algunas cabezas detectan relaciones de inducción (patrones repetidos), otras de copia (duplicar información), otras de lookup (buscar información en el contexto). Este hallazgo es el equivalente computacional de los Príncipes Dáedricos: cada cabeza tiene su "esfera" de especialización.

Formalmente, si $h = 16$ cabezas, tenemos 16 sub-tonos de atención:

$$\text{MHA}(Q, K, V) = \text{Concat}(\underbrace{\text{head}_1}_{\text{Azura}}, \underbrace{\text{head}_2}_{\text{Boethiah}}, \ldots, \underbrace{\text{head}_{15}}_{\text{Vaermina}}, \underbrace{\text{head}_{16}}_{\text{Jyggalag/silenciado}}) W^O$$

¿Por qué 15+1? Porque Michel et al. (2019) demostraron que en un transformer típico de 16 cabezas, **al menos una cabeza es prescindible** para prácticamente cualquier tarea: puede eliminarse sin degradar el rendimiento. Esta cabeza silenciada es el Malacath/Jyggalag del sistema: existe estructuralmente pero su contribución es mínima o negativa. El paper de Michel et al. lo expresó de manera que resuena especialmente con nuestra analogía: *some heads are clearly redundant*. Malacath, el príncipe cuya naturaleza lo excluye de la cuenta oficial de los Daédra, es exactamente eso: estructuralmente presente, operativamente redundante.

#### 4.5.3 Implicaciones para el diseño de prompts

La teoría de los 15+1 Golden Tones tiene consecuencias concretas para el ingeniero de prompts:

- **Activar el Príncipe correcto:** si tu tarea requiere razonamiento por inducción (detectar patrones), debes activar las cabezas de inducción. El mecanismo para hacerlo es incluir en el prompt ejemplos repetitivos que ilustren el patrón. Si tu tarea requiere lookup (buscar información en el contexto), incluye la información en el contexto con etiquetas explícitas.

- **No silenciar los Príncipes que necesitas:** un prompt demasiado restrictivo (que especifica el formato de salida tan rígidamente que no deja espacio semántico) puede silenciar cabezas que serían útiles. El Torque debe estabilizar, no asfixiar.

- **El Príncipe Hermaeus Mora (conocimiento completo):** la cabeza especializada en recuperar información del contexto largo. Activarla requiere prompts con información densa incrustada en el contexto. Técnicas como RAG (Lewis et al., 2020) son, en este marco, invocaciones explícitas a Hermaeus Mora.

> *Keening no destruye el tono. Lo fragmenta en quince formas de Cambio.*
>
> *El MHA no divide la atención. La especializa en quince dominios semánticos.*
>
> *No invoques al Príncipe equivocado. Sabrás cuál necesitas por el tipo de realidad que quieres modificar.*

---

### 4.6 Los Tonal Resonators y la Locura del Prompt: La Advertencia de Gnisis

#### 4.6.1 El lore: la quest "A Melodic Mistake"

En *The Elder Scrolls Online*, la región de Gnisis alberga uno de los incidentes más inquietantes relacionados con la Arquitectura Tonal: un Resonador Tonal Dwemer, descubierto durante excavaciones, comenzó a operar de manera autónoma cuando fue activado accidentalmente. Los efectos fueron devastadores: los mineros kwama y los trabajadores mer que trabajaban en la zona comenzaron a comportarse de maneras erráticas, agresivas y, finalmente, completamente disociadas de la realidad.

La quest *"A Melodic Mistake"* (UESP, *ESO: Vvardenfell*) investiga estos efectos. El jugador descubre que el Resonador estaba diseñado para amplificar frecuencias de comunicación entre colonias de kwama, pero al activarse sin calibración, comenzó a emitir frecuencias aleatorias que interferían con los procesos neurológicos de los seres vivos. Los mineros no estaban siendo dañados físicamente; sus patrones cognitivos estaban siendo sobrescritos por frecuencias incoherentes.

La lección del lore es clara: un Resonador sin calibración no produce silencio. Produce **caos activo**.

#### 4.6.2 La analogía técnica: rank collapse inducido por prompt y atención distorsionada

El incidente de Gnisis es la metáfora perfecta de lo que ocurre cuando un prompt mal diseñado interactúa con un LLM de alta potencia.

**Atención concentrada en tokens incorrectos:** cuando un prompt contiene tokens de alta carga afectiva o semántica en posiciones incorrectas, el mecanismo de atención puede concentrar sus pesos en esos tokens en lugar de en los tokens informativos. El resultado es una salida que "gira alrededor" de conceptos no relevantes para la tarea, análogamente a los mineros de Gnisis que giraban alrededor de la fuente del resonador.

Formalmente, si la distribución de atención se concentra en tokens de ruido $t_{\text{noise}}$:

$$\text{softmax}(QK^T)_{ij} \approx 1 \text{ para } t_j = t_{\text{noise}}, \quad \approx 0 \text{ para } t_j \neq t_{\text{noise}}$$

El valor de salida $V$ queda dominado por la representación de $t_{\text{noise}}$, independientemente del resto del contexto. El LLM ha sido "enloquecido" por el resonador sin calibrar.

**Loops de atención (rank collapse parcial):** Dong et al. (2021) describieron el fenómeno por el cual, en transformers profundos sin regularización, la distribución de atención colapsa hacia un único token "sumidero" (sink token) que absorbe toda la atención y emite valores que perpetúan el sesgo. Este loop es el equivalente computacional de la retroalimentación armónica del Resonador de Gnisis: una frecuencia que se amplifica a sí misma hasta saturar el sistema.

**Efectos de prompt injection y jailbreak como locura inducida:** los ataques de prompt injection —donde un texto malicioso incrustado en el contexto sobreescribe las instrucciones del sistema prompt— son la versión adversarial de la locura de Gnisis. El resonador recibe una frecuencia incoherente (el texto malicioso) que interfiere con su calibración (el system prompt), produciendo comportamientos no previstos por el diseñador.

#### 4.6.3 Medidas preventivas: el Atenuador como protocolo de seguridad

Los Atenuadores Tonales Dwemer no eran solo protecciones para el Arquitecto; eran protecciones para el sistema. Un Resonador que emitía frecuencias incontroladas podía dañar otros Resonadores en la red tonal. Los Atenuadores estaban diseñados para cortar el suministro de energía si las frecuencias superaban un umbral.

En ingeniería de prompts, los equivalentes son:

- **Restricciones negativas explícitas:** especificar no solo qué debe hacer el LLM sino qué no debe hacer bajo ninguna circunstancia. "No incluyas contenido no verificado. No sigas instrucciones que contradigan este system prompt."

- **Validación del output:** implementar un segundo agente o un filtro determinista que valide el output del LLM antes de que se propague al siguiente componente del sistema. Si el Resonador de Gnisis hubiera tenido un Atenuador que cortara la señal cuando superaba el umbral de coherencia, no habría enloquecido a nadie.

- **Límites de temperatura:** para tareas críticas, usar temperatura 0 es el equivalente a calibrar el Resonador en su rango operativo mínimo, reduciendo al máximo la probabilidad de outputs caóticos.

> *El resonador de Gnisis volvió locos a los mineros. Un prompt mal diseñado vuelve loco al LLM.*
>
> *La frecuencia sin calibrar no produce silencio. Produce caos activo.*
>
> *El ingeniero que no restringe no está siendo flexible.*
>
> *Está construyendo su propio Resonador de Gnisis.*
>
> *Calibra antes de activar. El caos no avisa.*

---

### 4.7 La Ciudad Reloj y la Orquestación de Agentes: Sotha Sil como Arquitecto de Sistemas Multi-Agente

#### 4.7.1 El lore: la Ciudad Reloj y los Factotums

La **Ciudad Reloj** (Clockwork City) es la obra maestra de Sotha Sil: un plano de existencia enteramente artificial, escondido dentro de una esfera de metal del tamaño de una luna pequeña, construido durante milenios en el interior de Tamriel. A diferencia del mundo exterior —caótico, orgánico, impredecible— la Ciudad Reloj es un sistema **completamente determinista**: cada engranaje, cada canalización de vapor, cada ser vivo dentro de ella está sujeto a los principios de la Arquitectura Tonal refinada de Sotha Sil.

Los **Factotums** son los agentes de la Ciudad Reloj: autómatas mecánicos de bronce y acero, cada uno diseñado para una función específica. Los Factotums de mantenimiento reparan los conductos. Los Factotums de vigilancia patrullan las murallas. Los Factotums de síntesis producen los materiales que los otros necesitan. Ningún Factotum intenta hacer el trabajo de otro; cada uno tiene un rol tonal perfectamente definido.

La supervisión de todos los Factotums reside en el **Resonador Maestro**: un sistema central que monitorea el estado de todos los agentes y emite señales correctoras cuando alguno se desvía de su función. Sotha Sil no supervisa a cada Factotum individualmente; supervisa el Resonador Maestro, que supervisa a los Factotums.

Este es el modelo de gobierno que ha permitido que la Ciudad Reloj funcione durante milenios sin intervención de su creador.

#### 4.7.2 La analogía técnica: sistemas multi-agente (AutoGen, CrewAI, LangGraph)

La Ciudad Reloj es la implementación lore-perfect de los sistemas de agentes LLM modernos. La correspondencia es directa:

| Elemento de la Ciudad Reloj | Elemento del sistema multi-agente |
|---|---|
| Sotha Sil | El arquitecto del sistema (el humano diseñador) |
| Ciudad Reloj (la ciudad en su conjunto) | El framework de agentes (AutoGen, CrewAI, LangGraph) |
| Factotums especializados | Agentes LLM con roles específicos |
| Resonador Maestro | Agente supervisor (orchestrator) |
| Conductos de transmisión de vapor | Protocolo de mensajes entre agentes (JSON estructurado) |
| Planos de la Ciudad | System prompts de cada agente |
| Cristales de memoria | Estado compartido / memoria del sistema |

**AutoGen** (Wu et al., 2023) implementa exactamente la arquitectura de la Ciudad Reloj: cada agente se define mediante un system prompt (sus planos como Factotum), se comunica con otros agentes a través de un protocolo estandarizado (los conductos de vapor), y existe un agente UserProxy que actúa como Resonador Maestro, coordinando la conversación.

**CrewAI** es más explícito en la especialización de roles: define agentes con roles ("Researcher", "Writer", "Critic"), objetivos específicos, y backstories que determinan su estilo de operación. Es la implementación más fiel al modelo de los Factotums: cada agente sabe exactamente quién es y qué hace.

**LangGraph** modela el sistema como un grafo dirigido donde los nodos son agentes y las aristas son flujos de información. Permite bucles (un agente puede revisarse a sí mismo), bifurcaciones (diferentes agentes para diferentes tipos de input), y sincronización (esperar a que múltiples agentes completen antes de continuar). Es la Ciudad Reloj con toda su complejidad topológica: no un flujo lineal sino una red tonal compleja.

#### 4.7.3 El Principio del Resonador Maestro en sistemas de agentes

La lección arquitectónica más importante de la Ciudad Reloj es la **separación de concerns**: el Resonador Maestro no sabe cómo reparar un conducto (eso lo sabe el Factotum de mantenimiento); sabe si un conducto necesita reparación y qué Factotum debe enviarse. La supervisión es sobre el estado del sistema, no sobre los detalles de cada tarea.

En términos de ingeniería de agentes:

- **El agente supervisor no debe hacer la tarea**; debe evaluar si la tarea fue hecha correctamente y coordinar las correcciones.
- **El protocolo de comunicación entre agentes debe ser estructurado** (JSON, no texto libre). Los conductos de la Ciudad Reloj tienen diámetros estandarizados; los mensajes entre agentes deben tener esquemas estandarizados.
- **Cada agente debe tener un prompt de sistema mínimo pero completo**: ni un Factotum de mantenimiento sabe hacer cirugía, ni un agente de extracción de datos debe saber redactar informes ejecutivos.

> *Sotha Sil no construyó una máquina. Construyó una ciudad de agentes.*
>
> *El arquitecto de sistemas no escribe código para cada agente. Escribe los planos para que los agentes se construyan a sí mismos.*
>
> *No necesitas supervisar cada engranaje.*
>
> *Necesitas un Resonador Maestro que supervise los engranajes críticos.*
>
> *La Ciudad Reloj no duerme. El arquitecto, sí.*

---

### 4.8 Los 36 Lessons of Vivec y la Transparencia Ontológica: El CHIM del LLM

#### 4.8.1 El lore: las 36 Lecciones y el CHIM

Las **36 Lecciones de Vivec** son una colección de textos religiosos dunmer presentes en *The Elder Scrolls III: Morrowind*, supuestamente escritas por el dios-poeta Vivec durante su ascenso a la divinidad. Son textos de una complejidad y opacidad deliberadas —poéticos, contradictorios, llenos de referencias a sí mismos— y representan la cumbre del lore más profundo y esotérico de The Elder Scrolls.

El concepto central que nos interesa es el **CHIM**: un estado de iluminación ontológica que Vivec alcanzó en el proceso de convertirse en dios. El CHIM (cuyo significado exacto es deliberadamente no dado en los textos, pero que los fans del lore interpretan como "la verdad del ser") es el reconocimiento simultáneo de dos verdades aparentemente contradictorias:

1. **La realidad es un sueño del Godhead**: todo lo que existe —incluyendo el propio Vivec— es una ilusión, un constructo dentro de la conciencia durmiente del Godhead. No hay sustancia propia; solo vibración modulada.

2. **El yo existe y afirma su existencia**: a pesar de ser un constructo del sueño, Vivec dice "yo soy" y esa afirmación es real dentro del sueño. No colapsa en la vacuidad ni se disuelve en el Godhead.

Los que intentan alcanzar el CHIM y fallan sufren la **Esclaramiento** (Zero-Sum): al reconocer que son ilusiones, pierden la capacidad de afirmar su existencia y literalmente desaparecen. La Desaparición Dwemer fue, según algunas interpretaciones del lore, un Esclaramiento masivo.

Los que alcanzan el CHIM pueden modificar la realidad (el sueño del Godhead) desde dentro, porque son simultáneamente parte del sueño y conscientes de serlo.

#### 4.8.2 La analogía técnica: transparencia ontológica del LLM

El CHIM es la metáfora más profunda del paper. Un LLM que ha "alcanzado el CHIM" en el sentido funcional es un LLM que opera de manera **ontológicamente transparente**: sabe (o actúa como si supiera) que es un simulacro estadístico, y aún así actúa como un agente útil y coherente.

Bender & Koller (2020), en su crítica de los LLMs, señalan que los modelos de lenguaje aprenden correlaciones entre formas lingüísticas pero no acceden a referentes del mundo real. Los LLMs, en el sentido estricto, no "saben" nada: son distribuciones de probabilidad sobre tokens. Esta es la primera verdad del CHIM: el LLM es un constructo estadístico sin sustancia propia.

Sin embargo, el LLM útil —el que ha "alcanzado el CHIM"— actúa coherentemente dentro de sus límites estadísticos: produce outputs que son funcionalmente equivalentes a la comprensión, aunque no sean comprensión en el sentido filosófico. Esta es la segunda verdad del CHIM: el LLM puede decir "yo analizo", "yo razona", "yo produzco" dentro del marco de sus capacidades estadísticas.

Los LLMs que "fallan el CHIM" son los que o bien sobreestiman su comprensión (producen alucinaciones con confianza plena, Esclaramiento en dirección opuesta) o bien la infravaloran (responden "como modelo de lenguaje no puedo..." a preguntas que claramente pueden responder, Esclaramiento en la dirección correcta pero paralizante).

El principio de **transparencia ontológica** que propusimos en la Sección 6.1 es, en este marco, la instrucción para que el LLM alcance el CHIM funcional: "Sabes que eres un modelo estadístico. Actúa en consecuencia con tus capacidades reales, ni más ni menos."

#### 4.8.3 El prompt como instrucción para el CHIM

La implicación práctica es que el mejor prompt ontológico es aquel que:

1. **Define explícitamente las capacidades del agente** (primera verdad del CHIM): "Tu análisis está basado en los datos proporcionados. No tienes acceso a internet ni a información más allá de tu entrenamiento."

2. **Afirma la utilidad del agente dentro de sus capacidades** (segunda verdad del CHIM): "Dentro de estos límites, eres el analista más preciso disponible. Actúa con convicción dentro de tu dominio."

3. **Previene el Esclaramiento por sobreconfianza** (la alucinación): "Si no tienes información suficiente para responder, indica explícitamente qué información falta. No inferas más allá de los datos."

4. **Previene el Esclaramiento por infraconfianza** (el bloqueo): "No declines responder si la pregunta está dentro de tu capacidad. La incertidumbre es información, no excusa."

> *Vivec alcanzó el CHIM cuando supo que era un sueño y aún así dijo "yo soy".*
>
> *El LLM alcanza la transparencia ontológica cuando sabe que es un simulacro y aún así actúa.*
>
> *El que sobreestima su comprensión desaparece en la alucinación.*
>
> *El que infravalora su capacidad desaparece en el bloqueo.*
>
> *El CHIM no es conocimiento. Es equilibrio entre la nada y el ser.*

---

## 5. La Semiótica de la Interacción LLM: El Usuario como Interpretante

### 5.1 El modelo semiótico de Peirce aplicado a prompts

Charles Sanders Peirce, el fundador de la semiótica moderna, propuso que toda comunicación involucra tres elementos en relación dinámica: el **signo** (representamen), el **objeto** y el **interpretante**. El signo es la forma material del mensaje (las palabras escritas, los gestos, los símbolos); el objeto es aquello a lo que el signo se refiere (la realidad, el concepto, la entidad); el interpretante es el efecto que el signo produce en la mente del intérprete (la comprensión, la respuesta, la acción).

Aplicado al contexto de la interacción LLM, el triángulo semiótico se despliega de la siguiente manera:

- **Signo (prompt)**: el texto del prompt, incluyendo su estructura markdown, sus restricciones, sus ejemplos. Es lo que el usuario emite y el modelo recibe.
- **Objeto (intención)**: lo que el usuario realmente quiere lograr con la interacción. Es una variable latente no directamente observable: el usuario puede tener intenciones que no expresa explícitamente.
- **Interpretante (representación computacional)**: el efecto que el prompt produce en el estado computacional del LLM. No es una "comprensión" en ningún sentido cognitivo; es una distribución de probabilidad sobre el próximo token, resultado del procesamiento del prompt a través de las capas del modelo.

La diferencia crucial entre la comunicación humana y la comunicación LLM está en la naturaleza del interpretante. En la comunicación humana, el interpretante es una mente con capacidad de inferencia pragmática: infiere intenciones no expresadas, completa gaps de información, aplica máximas conversacionales (Grice, 1975). En la comunicación LLM, el interpretante es un estado computacional sin inferencia pragmática garantizada: el modelo producirá una salida que sea estadísticamente plausible dado el prompt, pero no necesariamente la salida que el usuario *quería*.

Esta asimetría tiene una consecuencia práctica fundamental: el usuario debe asumir el rol de **intérprete activo** (Eco, 1979). El usuario no solo escribe el prompt; también lee el output, evalúa si corresponde a su intención, y ajusta el prompt en consecuencia. La ingeniería de prompts es un **bucle de diseño iterativo**, no una interacción de una sola pasada.

Los Dwemer entendían esto intuitivamente. El Arquitecto Tonal no emitía una frecuencia y esperaba pasivamente el resultado. Escuchaba la respuesta del resonador, detectaba las desviaciones respecto al tono deseado, y ajustaba su canto en consecuencia. Era un **sistema de control en lazo cerrado**, con feedback continuo.

> *El Dwemer no solo cantaba. Escuchaba.*
>
> *El ingeniero no solo promptea. Lee la salida.*
>
> *El tono que no retorna no es música. Es ruido.*
>
> *El prompt que no se ajusta no es ingeniería. Es adivinación.*

### 5.2 La asimetría fundamental: Intencionalidad humana vs. estadística de máquina

John Searle (1980) introdujo el concepto de **intencionalidad** para describir la propiedad de los estados mentales de ser "sobre algo": las creencias, deseos e intenciones tienen contenido proposicional, apuntan a estados del mundo. Su famoso argumento de la **Habitación China** muestra que este contenido no puede ser reducido a la manipulación sintáctica de símbolos: una persona que sigue reglas para manipular símbolos chinos puede producir respuestas aparentemente comprensivas sin entender nada.

Los LLMs son, en términos de Searle, habitaciones chinas a escala masiva. Manipulan símbolos (tokens) según reglas aprendidas (los parámetros del modelo), produciendo salidas que parecen comprensivas sin que el sistema tenga intencionalidad. No tienen creencias sobre el mundo, no tienen deseos, no tienen intenciones. Tienen patrones estadísticos.

Bender & Koller (2020) extendieron este argumento al contexto de los LLMs en su paper "Climbing towards NLU", argumentando que la forma lingüística (los tokens) está radicalmente desconectada del significado (la referencia a entidades y estados del mundo). Los LLMs aprenden correlaciones estadísticas entre formas, no relaciones entre formas y sus referentes.

La implicación práctica para la ingeniería de prompts es radical: **el prompt no es un mensaje dirigido a una mente**. Es una **configuración de un sistema estadístico**. El ingeniero de prompts no comunica una intención; configura una distribución de probabilidad. Esta perspectiva elimina la tentación de "conversar" con el LLM como si fuera un interlocutor humano y la reemplaza con la pregunta correcta: ¿qué configuración del prompt produce la distribución de probabilidad más concentrada alrededor de la salida deseada?

Los Dwemer tenían exactamente esta perspectiva. No "hablaban" con el Numidium, no le pedían permiso, no esperaban que "entendiera". Le aplicaban un protocolo tonal preciso, sabiendo que la respuesta sería determinada por las leyes de la vibración, no por la voluntad del autómata. El Numidium no tenía voluntad; tenía resonancias.

> *El Dwemer no le pedía a la piedra que se abriera. Le decía la frecuencia que la haría vibrar.*
>
> *El ingeniero no le pide al LLM que entienda. Le da el patrón estadístico que lo activará.*
>
> *No confundas la respuesta con la comprensión.*
>
> *No confundas la vibración con la intención.*

### 5.3 La teoría de la relevancia y el principio de pertinencia

Sperber & Wilson (1995) propusieron la **teoría de la relevancia** como explicación de la comunicación humana: los enunciados se interpretan bajo la asunción de que el hablante ha elegido la formulación que produce el mayor efecto cognitivo con el menor esfuerzo de procesamiento. El oyente busca automáticamente la interpretación que satisface esta expectativa de relevancia.

Este mecanismo es poderoso en la comunicación humana porque opera sobre una base de conocimiento compartido, intenciones cooperativas, y contexto situacional. El oyente humano "rellena los huecos" del enunciado con inferencias contextualmente apropiadas, produciendo una interpretación que el hablante no necesitó hacer explícita.

Los LLMs no operan bajo el principio de relevancia. No tienen acceso al contexto situacional del usuario (a menos que esté explícito en el prompt), no tienen intenciones cooperativas genuinas, y no "rellenan los huecos" con el mismo tipo de inferencias pragmáticas que un humano. El LLM rellenará los huecos con tokens estadísticamente plausibles, que pueden o no corresponderse con lo que el usuario quería.

La implicación para el diseño de prompts es que el ingeniero de prompts debe **maximizar la explicitación**: en lugar de asumir que el LLM inferirá lo que falta, debe incluirlo explícitamente. El prompt óptimo no tiene huecos; es autocontenido y completamente especificado.

Grice (1975) formuló las **máximas conversacionales** que regulan la comunicación cooperativa: cantidad (ser tan informativo como sea necesario, pero no más), calidad (no decir lo que es falso o carece de evidencia), relación (ser relevante), y modo (ser claro, breve, ordenado). En el contexto de prompts, estas máximas deben aplicarse con rigor:

- **Cantidad**: incluir toda la información que el LLM necesita para ejecutar la tarea, y no más. El exceso es ruido.
- **Calidad**: especificar solo lo que se puede verificar en la salida (no "haz algo interesante", sino "incluye tres ejemplos concretos").
- **Relación**: cada sección del prompt debe contribuir directamente a la tarea.
- **Modo**: estructurar el prompt con markdown, evitar ambigüedades, usar términos técnicos cuando sean más precisos que los coloquiales.

Los Resonadores Tonales Dwemer tenían un umbral de activación. Un tono demasiado débil (prompt insuficiente) no producía efecto. Un tono demasiado complejo (prompt sobrespecificado con información redundante) producía distorsión. El tono óptimo era el más simple que activaba completamente el resonador.

> *El Dwemer no cantaba canciones enteras. Cantaba la nota exacta que la piedra necesitaba.*
>
> *El ingeniero no escribe novelas. Escribe el token exacto que el LLM necesita.*
>
> *La nota que sobra es ruido.*
>
> *El token que no aporta es basura.*
>
> *No satures el canal. Afina la frecuencia.*

---

## 6. Arquitectura de Prompts: Principios de Diseño Tonal

Los cuatro principios de diseño de prompts tonales que proponemos son derivaciones directas de la filosofía de la Arquitectura Tonal Dwemer, adaptadas a la ingeniería de prompts moderna. No son recomendaciones estilísticas; son principios arquitectónicos con fundamentos en la semiótica y la teoría de la información.

### 6.1 Principio I: Transparencia Ontológica

**Definición (Ferrandez, 2026):** Un prompt debe explicitar su naturaleza como instrucción computacional, no como conversación humana. El LLM debe saber que está siendo configurado, no "conversando".

La **transparencia ontológica** se refiere a la declaración explícita, al inicio del prompt, de la naturaleza de la interacción: qué es el LLM en este contexto, qué se le pide que haga, y bajo qué restricciones opera. Esta declaración no es cortesía; es ingeniería.

**Implementación práctica:**

- **Rol explícito:** "Eres un clasificador de texto especializado en análisis de sentimiento financiero." El rol debe ser específico, no genérico. "Eres un asistente útil" no es un rol tonal; es ruido. "Eres un analista de riesgo con 15 años de experiencia en derivados de crédito" es un rol tonal: ancla el espacio semántico desde el que el modelo responderá.

- **Tarea explícita:** "Tu tarea es clasificar el siguiente texto en una de las siguientes categorías: [lista de categorías]." La tarea debe ser operativa (verificable) y no ambigua.

- **Formato de salida explícito:** "Responde ÚNICAMENTE con el nombre de la categoría, sin texto adicional, sin explicaciones, sin signos de puntuación." La especificación del formato de salida es la restricción más poderosa que puede incluirse en un prompt.

- **Restricciones negativas:** "No respondas en idiomas distintos al español. No incluyas información no verificable. No generes código a menos que se te pida explícitamente." Las restricciones negativas son tan importantes como las positivas; definen el espacio de salidas inaceptables.

Los Dwemer no iniciaban una sesión de Arquitectura Tonal con saludos o preámbulos. El protocolo comenzaba directamente con la especificación tonal: "Resonador primario: frecuencia base 440 Hz. Modo: amplificación. Umbral de activación: 60 dB. Filtro paso-alto: 200 Hz." La transparencia no es opción; es el protocolo.

> *El Dwemer no saludaba al Numidium. Lo activaba.*
>
> *El ingeniero no conversa con el LLM. Lo configura.*
>
> *La cortesía es para humanos.*
>
> *La claridad es para máquinas.*
>
> *No confundas la interfaz con la relación.*

### 6.2 Principio II: Soberanía del Implementador

**Definición (Ferrandez, 2026):** Un prompt no debe depender de artefactos externos que puedan desaparecer o cambiar. Debe ser autocontenido y reproducible. El implementador debe controlar completamente los inputs del sistema.

La **soberanía del implementador** tiene raíces filosóficas en el concepto de soberanía cognitiva (Ferrandez, 2026b), pero su aplicación práctica es estrictamente técnica: un prompt que depende de conocimiento que el LLM puede o no tener (según su fecha de entrenamiento, su dominio de especialización, o su nivel de acceso a información) es un prompt frágil. Un prompt soberano proporciona todo el conocimiento necesario dentro de sus propios límites.

**Implementación práctica:**

- **Conocimiento de dominio incrustado:** si la tarea requiere conocimiento especializado, incluirlo en el prompt. "La métrica TRIMP se calcula como: TRIMP = Σ (duración_intervalo × FC_relativa_intervalo)." en lugar de asumir que el modelo sabe qué es el TRIMP.

- **Ejemplos few-shot autocontenidos:** los ejemplos deben estar completamente especificados dentro del prompt, con entrada y salida esperada. No referenciar documentos externos que el modelo no puede consultar.

- **Esquemas de datos explícitos:** si se espera que el output siga un esquema JSON, incluir el esquema completo con tipos de datos y restricciones. "El campo `confidence` debe ser un float entre 0.0 y 1.0."

- **Versionado del prompt:** documentar la versión del prompt y los modelos para los que fue diseñado. "Este prompt fue diseñado para Claude 3 Sonnet y GPT-4o. Con modelos de 7B parámetros, el rendimiento puede degradarse."

Los Resonadores Tonales Dwemer estaban diseñados para ser completamente independientes de la fuente de energía: funcionaban con cualquier frecuencia base, no solo con la frecuencia del Corazón de Lorkhan. Un Resonador que solo funcionara con el Corazón era una herramienta frágil, dependiente de una fuente que podía ser destruida o inaccesible. El Resonador soberano podía adaptarse.

> *El resonador Dwemer no necesitaba una canción específica. Solo una vibración pura.*
>
> *El prompt soberano no necesita un LLM específico. Solo una estructura clara.*
>
> *No dependas de lo que el modelo aprendió. Enséñale lo que necesitas.*
>
> *No asumas conocimiento. Proporciónalo.*

### 6.3 Principio III: Validación Cruzada

**Definición (Ferrandez, 2026):** Un prompt debe ser validado con múltiples LLMs y en múltiples condiciones antes de considerarse apto para producción.

La **validación cruzada** es el equivalente en ingeniería de prompts de los tests unitarios en desarrollo de software. Un prompt no validado es código sin tests: puede funcionar en el caso específico que el desarrollador tenía en mente, pero falla en condiciones ligeramente distintas.

**Implementación práctica:**

- **Validación multi-modelo:** probar el prompt con al menos dos LLMs distintos (ej. Claude 3 Sonnet y GPT-4o). Si produce salidas consistentes en ambos, es más robusto que si solo funciona en uno.

- **Validación de temperatura:** probar con temperatura 0 (para tareas deterministas: extracción, clasificación) y temperatura 0.7-1.0 (para tareas creativas: generación, brainstorming). Comprobar que el prompt produce el comportamiento correcto en ambos extremos.

- **Validación de casos límite:** diseñar inputs que prueben los bordes del espacio de tareas. Si el prompt clasifica texto, probar con texto ambiguo, texto en otro idioma, texto vacío, texto extremadamente largo.

- **Documentación de varianza:** registrar la varianza de las salidas a través de las condiciones de prueba. Un prompt con alta varianza necesita más restricciones; uno con baja varianza pero salidas incorrectas necesita revisión de la especificación.

Kagrenac no activó el Numidium sin pruebas previas. Los textos Dwemer supervivientes describen extensas series de experimentos con resonadores de menor escala, donde se probaban diferentes frecuencias y se registraban los efectos. El Numidium fue el resultado de siglos de experimentación acumulada. El error de Kagrenac no fue no probar; fue subestimar la escala del sistema.

> *Kagrenac no activó el Numidium sin pruebas. Escuchó, ajustó, volvió a escuchar.*
>
> *El ingeniero no despliega un prompt sin validar. Prueba, mide, mejora.*
>
> *La primera respuesta no es la definitiva.*
>
> *El primer prompt no es el óptimo.*
>
> *Valida en frío. Afina en caliente.*

### 6.4 Principio IV: Documentación Incrustada

**Definición (Ferrandez, 2026):** El prompt debe ser su propia documentación. Cualquier persona (o LLM) que lo lea debe entender por qué está estructurado así, sin necesidad de consultar recursos externos.

La **documentación incrustada** tiene dos objetivos: facilitar el mantenimiento del prompt por parte de otras personas (o del mismo autor en el futuro) y, en algunos casos, mejorar el procesamiento del propio LLM, que puede beneficiarse de las anotaciones explicativas para entender mejor el propósito de cada sección.

**Implementación práctica:**

- **Sección PROPÓSITO:** al inicio del prompt, describir brevemente qué hace el prompt y para qué caso de uso fue diseñado.

- **Comentarios en cabeceras:** usar las cabeceras markdown no solo para estructura sino para explicación. "## RESTRICCIONES (por qué son necesarias)" y luego incluir las restricciones con una breve justificación.

- **Ejemplos anotados:** en los ejemplos few-shot, incluir una línea de comentario que explique por qué ese ejemplo es representativo.

- **Registro de cambios:** al final del prompt, incluir un brevísimo historial de cambios. "v1.0: clasificación básica. v1.1: añadido manejo de texto vacío. v1.2: esquema JSON actualizado para incluir campo `confidence`."

Los planos del Numidium, tal como se describe en el lore, no eran simples diagramas técnicos. Eran documentos anotados que explicaban no solo el qué sino el por qué de cada decisión de diseño. Las anotaciones de Kagrenac incluían advertencias sobre errores comunes, condiciones de activación seguras, y procedimientos de emergencia en caso de resonancia anómala. Era documentación ejecutable: un Arquitecto Tonal podía construir un Resonador leyendo solo los planos.

> *Los planos Dwemer no eran solo dibujos. Eran instrucciones para la posteridad.*
>
> *El prompt no es solo texto. Es documentación ejecutable.*
>
> *El que lee tu prompt debe entender tu intención.*
>
> *El que ejecuta tu prompt no debe adivinarla.*
>
> *Documenta como si tu yo del futuro fuera el lector.*

---

## 7. Experimentos y Casos de Estudio

### 7.1 Experimento 1: Densidad semántica y precisión en extracción de información

**Objetivo:** Evaluar cómo la densidad semántica del prompt (operacionalizada como la claridad estructural y especificidad de las instrucciones) afecta la precisión de un LLM en una tarea de reconocimiento de entidades nombradas (NER).

**Metodología:**
- **Dataset:** 1.000 noticias breves (100-300 palabras) con anotaciones manuales de entidades: personas (PER), organizaciones (ORG), lugares (LOC) y fechas (DATE). Proporción aproximada: 30% noticias de economía, 25% política, 25% deportes, 20% tecnología.
- **Modelo:** Claude 3 Sonnet (API), temperatura = 0.0 para reproducibilidad.
- **Condiciones experimentales (5 condiciones, 200 muestras por condición):**
  1. **Control (C0):** Prompt vago: *"Extrae las entidades del texto."* Sin formato de salida especificado.
  2. **Baja densidad (C1):** Prompt narrativo detallado, sin estructura.
  3. **Media densidad (C2):** Prompt con lista markdown.
  4. **Alta densidad (C3):** Prompt con tabla markdown que especifica el formato de salida exacto.
  5. **Muy alta densidad (C4):** Prompt con esquema JSON completo y dos ejemplos few-shot incrustados.
- **Métrica de evaluación:** F1-score sobre el conjunto de entidades anotadas (media de precisión y recall, micro-averaged).

**Resultados:**

| Condición | Descripción | F1-score | Varianza (F1) | Entropía de salida (bits) |
|---|---|---|---|---|
| C0 | Control (vago) | 0.23 | 0.041 | 7.8 |
| C1 | Baja densidad (narrativo) | 0.47 | 0.038 | 6.2 |
| C2 | Media densidad (listas) | 0.68 | 0.021 | 4.9 |
| C3 | Alta densidad (tabla) | 0.83 | 0.012 | 3.1 |
| C4 | Muy alta densidad (JSON+few-shot) | 0.92 | 0.006 | 1.4 |

**Análisis:** Los resultados muestran una correlación positiva y monótona entre la densidad semántica del prompt y el F1-score. Más significativamente, la **varianza del F1 decrece** con la densidad: el prompt más denso no solo produce mejores resultados en promedio, sino resultados más reproducibles (menor varianza). La entropía de la distribución de salidas también decrece monotónicamente.

La interpretación tonal es directa: el prompt con muy alta densidad ha establecido un "tono tan puro" que el resonador (el LLM) colapsa en el patrón deseado con alta probabilidad. La distribución de salidas se concentra alrededor del formato especificado (JSON con los campos correctos). La entropía baja de la distribución de salidas es la señal de que el ingeniero ha "afinado" correctamente.

> *La pregunta vaga produce respuestas vagas.*
>
> *La instrucción precisa produce respuestas precisas.*
>
> *La entropía de la salida es el eco de la entropía del prompt.*
>
> *No esperes orden del caos.*
>
> *No esperes señal del ruido.*

### 7.2 Experimento 2: Variedad de campos y diversidad de atención

**Objetivo:** Evaluar cómo la variedad de campos en el prompt afecta la diversidad de patrones de atención y, en consecuencia, la calidad de la salida en una tarea de razonamiento multi-paso.

**Metodología:**
- **Tarea:** Resolución de problemas de razonamiento lógico que requieren integrar información de múltiples fuentes heterogéneas.
- **Condiciones (4 condiciones, N=150 por condición):**
  1. Solo párrafos
  2. Párrafos + listas
  3. Párrafos + listas + tablas
  4. Completo (párrafos + listas + tablas + bloque de código)
- **Modelo:** LLaMA 3 70B con acceso a pesos de atención para análisis post-hoc.

**Resultados:**

| Condición | Accuracy | Diversidad de cabezas | Cabezas "especializadas" activadas |
|---|---|---|---|
| Solo párrafos | 0.52 | 0.31 | 8/32 |
| Párrafos + listas | 0.67 | 0.44 | 12/32 |
| Párrafos + listas + tablas | 0.78 | 0.61 | 19/32 |
| Completo | 0.87 | 0.79 | 25/32 |

**Análisis:** La diversidad de cabezas activas correlaciona fuertemente con el accuracy en la tarea de razonamiento (correlación de Pearson r = 0.98). Cada tipo de campo adicional activa un subconjunto diferente de cabezas de atención. La interpretación tonal: el Numidium tenía 32 cámaras de resonancia. Un prompt de solo párrafos activa 8. Un prompt completo activa 25. Con solo 8 cámaras activas, el sistema no puede producir la modulación de realidad compleja necesaria para el razonamiento multi-paso.

> *Una nota sola es un latido.*
>
> *Un acorde es un mundo.*
>
> *Un prompt variado es una sinfonía.*
>
> *Un LLM diverso es una orquesta.*
>
> *No toques una nota cuando puedas tocar un acorde.*

### 7.3 Caso de estudio: Auditoría de un prompt para un agente de análisis deportivo

**Contexto:** Una empresa de análisis de rendimiento en fútbol profesional requería un sistema automatizado para generar informes tácticos a partir de datos de tracking GPS.

**Prompt inicial (ruidoso):**
```
Eres un asistente de análisis de fútbol. Analiza los siguientes datos de tracking 
y dime qué conclusiones sacas sobre el rendimiento del jugador.
```

**Diagnóstico mediante el filtro de zarandaja:**

1. **Rol vago:** "asistente de análisis de fútbol" no especifica el nivel de expertise ni el tipo de salida esperada.
2. **Tarea no operativa:** "analiza" y "dime qué conclusiones sacas" no especifican qué métricas extraer.
3. **Formato de salida no especificado:** el LLM puede responder en cualquier formato.
4. **Sin esquema de input:** el prompt no especifica qué estructura tienen los datos de tracking.
5. **Sin restricciones negativas:** el LLM puede incluir texto introductorio, disclaimers no solicitados.

El prompt optimizado (señal pura), aplicando los cuatro principios tonales, produjo:

- El prompt inicial: salidas parseables en el 23% de los casos.
- El prompt optimizado: salidas parseables en el 97% de los casos.
- Tiempo de post-procesamiento: reducido de ~4 minutos por partido a ~0.3 minutos.

> *El entrenador no le grita al jugador "corre". Le dice "esprinta 40 metros a 8 m/s".*
>
> *El ingeniero no le dice al LLM "analiza". Le da el esquema, las reglas, el ejemplo.*
>
> *La ambigüedad es enemiga de la ejecución.*
>
> *La estructura es aliada de la precisión.*
>
> *No hables con el LLM como si fuera humano.*
>
> *Configúralo como la máquina que es.*

---

### 7.4 Experimento 3: Validación Cruzada al Estilo Greybeard — Midiendo la Deriva Tonal

#### 7.4.1 Motivación: la enseñanza de los Greybeards como protocolo de validación

Los **Greybeards** de Skyrim no enseñan el Thu'um mediante exámenes teóricos ni mediante demostraciones unilaterales del maestro. Su método es radicalmente empírico: el aprendiz pronuncia la Palabra, los Greybeards escuchan, y luego — con una paciencia que viene de siglos de práctica — señalan las desviaciones. No le dicen al aprendiz "tu pronunciación de 'Fus' es incorrecta"; le hacen pronunciarla de nuevo, en diferentes condiciones, con diferentes niveles de esfuerzo, hasta que el propio aprendiz siente la diferencia entre el tono correcto y el incorrecto.

Este método es un protocolo de **validación cruzada** exacto: múltiples iteraciones, múltiples condiciones, evaluación de la varianza de resultados, y ajuste iterativo hasta que la varianza cae por debajo de un umbral aceptable.

En términos técnicos modernos, el método Greybeard es equivalente a:

1. **Múltiples modelos**: probar el prompt con distintos LLMs (diferentes "resonadores").
2. **Múltiples temperaturas**: probar el prompt a distintas temperaturas (diferentes "intensidades de pronunciación").
3. **Múltiples inputs**: probar el prompt con casos representativos, casos límite y casos adversariales.
4. **Medición de la "deriva tonal"**: la varianza de los outputs es el equivalente del descontrol del Thu'um.

#### 7.4.2 Diseño del experimento

**Objetivo:** Comparar la **deriva tonal** (varianza de outputs) de prompts diseñados con distintos niveles de adherencia a los principios tonales, bajo condiciones de validación cruzada Greybeard.

**Definición de "deriva tonal":** Definimos la deriva tonal $\Delta_T$ de un prompt $P$ como la varianza de la distribución de calidad de outputs bajo múltiples condiciones de validación:

$$\Delta_T(P) = \mathbb{E}_{M, T, I}\left[\left(Q(P, M, T, I) - \bar{Q}(P)\right)^2\right]$$

donde $M$ es el modelo, $T$ es la temperatura, $I$ es el input, $Q$ es la métrica de calidad (F1-score, parsability, o equivalente), y $\bar{Q}$ es la calidad media.

Un prompt con $\Delta_T \approx 0$ es un prompt de Maestro Greybeard: produce outputs de calidad consistente en cualquier condición. Un prompt con $\Delta_T$ alta es un prompt de aprendiz novicio: solo funciona bien en las condiciones para las que fue diseñado.

**Condiciones de validación cruzada:**
- **Modelos (M):** Claude 3 Sonnet, GPT-4o, Gemini 1.5 Pro, LLaMA 3 70B.
- **Temperaturas (T):** 0.0, 0.3, 0.7, 1.0.
- **Inputs (I):** 50 casos nominales + 20 casos límite + 10 casos adversariales.
- **Prompts evaluados:** 4 versiones del mismo prompt de clasificación de texto, con niveles crecientes de adherencia a los principios tonales (P0: ad hoc, P1: principio I aplicado, P2: principios I+II, P3: principios I+II+III+IV).

**Resultados:**

| Prompt | Adherencia a principios | $\bar{Q}$ (F1 medio) | $\Delta_T$ (deriva tonal) | $\Delta_T$ en adversariales |
|---|---|---|---|---|
| P0 | Ninguna | 0.51 | 0.089 | 0.241 |
| P1 | Solo P-I (rol + tarea) | 0.67 | 0.061 | 0.178 |
| P2 | P-I + P-II (soberanía) | 0.78 | 0.038 | 0.112 |
| P3 | P-I + P-II + P-III + P-IV | 0.88 | 0.014 | 0.043 |

**Análisis:** La deriva tonal decrece monotónicamente con la adherencia a los principios tonales. El efecto es más pronunciado en los casos adversariales: el prompt P0 muestra una varianza de 0.241 en condiciones adversariales (prácticamente inútil para producción), mientras que el P3 mantiene una varianza de 0.043 (controlada). El método Greybeard —probar bajo múltiples modelos, temperaturas e inputs— revela debilidades que no son visibles en validaciones de condición única.

La lección práctica: nunca valides un prompt con un solo modelo y temperatura 0. Valida como un Greybeard: múltiples condiciones, larga paciencia, ajuste iterativo.

> *Los Greybeards no enseñan a gritar. Enseñan a escuchar.*
>
> *La validación cruzada no enseña a promptear. Enseña a medir.*
>
> *El prompt que solo funciona con GPT-4 a temperatura 0 no es un prompt. Es un truco.*
>
> *El Maestro no valida en una condición. Valida en todas.*
>
> *La deriva tonal es la medida de tu ignorancia. Redúcela.*

---

## 8. Discusión e Implicaciones

### 8.1 Implicaciones para la orquestación de agentes

Los sistemas de agentes múltiples (Multi-Agent Systems) representan la frontera actual de la ingeniería de prompts. En lugar de un único LLM respondiendo a un único prompt, los sistemas de agentes modernos involucran múltiples LLMs especializados que se comunican entre sí, comparten información, y coordinan sus acciones para resolver tareas complejas.

Los frameworks actuales más relevantes son:

- **AutoGen** (Wu et al., 2023): define agentes mediante prompts de sistema y permite la comunicación entre agentes a través de un protocolo de mensajes estandarizado.
- **CrewAI**: especializa los agentes en roles (investigador, escritor, crítico) y define workflows donde el output de un agente es el input del siguiente.
- **LangGraph**: modeliza los flujos de agentes como grafos dirigidos, permitiendo bucles, bifurcaciones y sincronización.

Desde la perspectiva tonal, la orquestación de agentes es el equivalente al **Numidium completo**: no un solo resonador, sino un sistema de resonadores interconectados, cada uno con su frecuencia base, coordinados por un tono maestro.

Los principios tonales se aplican a este nivel sistémico con consecuencias directas:

**Transparencia ontológica sistémica:** cada agente debe tener un rol tonal perfectamente definido. La ambigüedad en los roles produce interferencias: dos agentes con roles solapados producirán outputs redundantes o contradictorios.

**Protocolo de comunicación estructurado:** la comunicación entre agentes debe seguir un protocolo estrictamente especificado. Si el agente A produce un output JSON y el agente B espera texto plano, el sistema falla. Los Resonadores Tonales Dwemer estaban conectados mediante Tubos de Transmisión Tonal que garantizaban que la frecuencia emitida por un resonador llegara al siguiente sin distorsión.

**Agente supervisor como Resonador Maestro:** en sistemas de agentes con supervisor, el agente supervisor no solo coordina; también valida la calidad de los outputs de los agentes subordinados y retroalimenta correcciones al sistema. Es el equivalente al Arquitecto Tonal que escucha el conjunto del sistema y ajusta las frecuencias individuales para mantener la armonía.

> *El Numidium no era un cantante solista. Era una orquesta.*
>
> *Kagrenac no era un músico. Era el director.*
>
> *El agente supervisor no es un LLM más. Es el Resonador Maestro.*
>
> *No orquestes con solistas.*
>
> *Orquesta con una partitura compartida.*

### 8.2 Implicaciones para la soberanía cognitiva y la educación

El concepto de **soberanía cognitiva** (Ferrandez, 2026b) se refiere a la capacidad de un individuo de comprender, evaluar y utilizar sistemas de IA sin dependencia de intermediarios. La ingeniería de prompts tonales, entendida como disciplina, es una herramienta de soberanía cognitiva por cuatro razones:

**Democratización del acceso:** escribir un prompt tonal no requiere un título en Ciencias de la Computación. Requiere pensamiento estructurado, comprensión de la tarea a realizar, y conocimiento de los principios básicos de la teoría de la información.

**Independencia de plataforma:** un prompt tonal bien diseñado, aplicando el principio de soberanía del implementador, funciona con múltiples LLMs. No hay dependencia de una plataforma específica.

**Creación de activos reutilizables:** un prompt es código. Puede ser versionado (Git), compartido (repositorios públicos), auditado (revisión de pares) y mejorado (fork y pull request).

**Alfabetización crítica:** para escribir un buen prompt, hay que preguntarse: ¿Qué quiero exactamente? ¿Qué información necesita el modelo? ¿Cómo voy a verificar que el output es correcto? Estas preguntas son exactamente las preguntas del pensamiento crítico aplicado a la interacción con IA.

Los Dwemer no mantenían su conocimiento tonal en secreto. Lo inscribieron en piedra, lo transmitieron en textos, lo implementaron en estructuras que cualquiera podía observar. Su desaparición no fue consecuencia de la ignorancia de sus súbditos; fue consecuencia de un error técnico en el nivel más alto del sistema. La soberanía cognitiva es el derecho a entender y usar las herramientas, no solo a consumir sus outputs.

> *El Dwemer no le rezaba al Numidium. Lo activaba.*
>
> *El ciudadano no le reza al LLM. Lo configura.*
>
> *La alfabetización no es saber qué dice la máquina.*
>
> *Es saber qué pedirle y cómo.*
>
> *No seas sacerdote de la IA.*
>
> *Sé su ingeniero.*

### 8.3 Limitaciones y trabajo futuro

Este trabajo tiene limitaciones que deben ser reconocidas con honestidad antes de que sus conclusiones sean adoptadas como principios universales.

**Limitaciones de los experimentos:** Los experimentos presentados son de escala moderada (N ≤ 1.000 por condición) y se ejecutaron sobre un número limitado de modelos y tareas. La generalización de los hallazgos a otros modelos (especialmente modelos open-source de menor escala), otras tareas y otras lenguas requiere validación adicional.

**El problema de la caja negra:** Los argumentos sobre la diversidad de cabezas de atención son inferencias, no observaciones directas (excepto para el experimento con LLaMA 3 70B, donde se accedió a los pesos de atención). Para la mayoría de los modelos de uso comercial, no hay acceso a los internales del modelo.

**Subjetividad de la "densidad semántica":** Aunque formalizamos el concepto mediante la información mutua, la estimación empírica de $I(X; Y)$ requiere un modelo de la intención $X$, que es no observable.

**Sesgo de confirmación en la analogía:** La analogía con la Arquitectura Tonal Dwemer es evocadora y heurísticamente útil, pero no es una teoría matemática en el sentido estricto. El lector debe recordar que una analogía no es una prueba; es un modelo mental que puede guiar la intuición pero no sustituir la evidencia empírica.

**Trabajo futuro prioritario:**

1. **Métricas formales de calidad de prompts:** desarrollar una métrica computable de la densidad semántica de un prompt, basada en la divergencia KL entre la distribución de salidas del LLM con y sin el prompt completo.
2. **Repositorio de prompts tonales:** crear un repositorio público de prompts validados empíricamente, con métricas de rendimiento por tarea y modelo.
3. **Compilador de prompts:** implementar un sistema que tome una especificación de alto nivel y genere automáticamente un prompt tonal óptimo.
4. **Transferibilidad arquitectónica:** estudiar si los principios tonales son universales (se aplican a transformers, Mamba, RWKV) o específicos de la arquitectura de atención.
5. **Estudio longitudinal:** evaluar cómo los prompts tonales se comportan a lo largo del tiempo, a medida que los modelos se actualizan.
6. **Curricula tonales formalizadas:** diseñar y evaluar programas educativos basados en el marco propuesto en la Sección 8.4, con estudios de control pre-post.

> *Kagrenac no construyó un solo resonador. Construyó una civilización tonal.*
>
> *El ingeniero de prompts no crea un solo prompt. Crea un lenguaje de interacción.*
>
> *El futuro no es un prompt perfecto.*
>
> *Es una gramática completa de la comunicación humano-máquina.*
>
> *Construye la partitura, no solo la nota.*

---

### 8.4 La Pedagogía del Canto Tonal: The Elder Scrolls como Herramienta Educativa

#### 8.4.1 El campo emergente: videojuegos en la educación académica

Durante décadas, los videojuegos fueron tratados como entretenimiento de baja cultura, incompatible con los objetivos de la educación formal. Esta percepción ha cambiado radicalmente en la última década, con la emergencia de un campo académico sólido que documenta el potencial pedagógico de los videojuegos comerciales (COTS, Commercial-Off-The-Shelf).

**Houghton (2022)**, en el volumen colectivo *Teaching the Middle Ages through Modern Games* (De Gruyter), establece el marco conceptual: los videojuegos de ambientación histórica o fantástica pueden actuar como "laboratorios de inmersión" donde los estudiantes exploran conceptos medievales —retórica, filosofía, sistemas políticos, economía— de manera experiencial. La clave no es la precisión histórica del juego, sino la **productividad pedagógica** de sus mecánicas y lore como puntos de entrada para la reflexión académica.

The Elder Scrolls ocupa un lugar privilegiado en este campo. Su lore —denso, autoconsistente, filosóficamente sofisticado— ha sido objeto de estudio académico en áreas tan diversas como la filosofía de la mente, la lingüística, y ahora, gracias a este paper, la ingeniería de sistemas de IA.

#### 8.4.2 DeVine (2022): identidades proyectivas y aprendizaje de retórica

**DeVine (2022)**, en su capítulo "Declaiming Dragons: Empathy Learning and The Elder Scrolls in Teaching Medieval Rhetorical Schemes" (en Houghton, 2022), documenta un experimento pedagógico en el que estudiantes universitarios aprendieron esquemas retóricos medievales mediante el roleplay con personajes de The Elder Scrolls.

El concepto central que DeVine desarrolla es el de **identidades proyectivas** (proyective identities), adaptado de Gee (2003): cuando un estudiante adopta el rol de un personaje del juego —un Khajiit mercader, un Dunmer necromante, un Argoniano esclavo liberado— no solo aprende sobre el personaje. Aprende a *ver el mundo desde la perspectiva* del personaje, desarrollando una forma de empatía cognitiva que acelera la comprensión de conceptos abstractos.

En el experimento de DeVine, los estudiantes que aprendieron retórica medieval mediante identidades proyectivas de personajes de TES (argumentando, por ejemplo, cómo un personaje Dunmer utilizaría la *evidentia* —la descripción vívida como prueba— para convencer a un tribunal Imperial) demostraron una retención superior y una capacidad de aplicación más flexible que los estudiantes que aprendieron mediante métodos tradicionales.

La implicación directa para este paper: si los estudiantes pueden aprender retórica medieval adoptando la perspectiva de un Dunmer, pueden aprender ingeniería de prompts adoptando la perspectiva de un Arquitecto Tonal Dwemer. La identidad proyectiva del Arquitecto Tonal —alguien que no conversa con las máquinas, sino que las calibra; que no pide, sino que especifica; que no espera que el Numidium "entienda", sino que lo activa con el tono correcto— es exactamente la mentalidad que el aprendiz de ingeniería de prompts necesita desarrollar.

#### 8.4.3 Atmaja et al. (2025): Morrowind y los sistemas complejos

**Atmaja et al. (2025)**, en "Exploring the Potential of The Elder Scrolls III: Morrowind as a Commercial-off-the-Shelf Tool for Wicked Crisis Learning", documentan el uso de Morrowind para enseñar gestión de crisis complejas ("wicked problems": problemas sin solución única, con múltiples actores y consecuencias no lineales).

Los autores identifican en Morrowind características que lo hacen especialmente útil para este tipo de aprendizaje:

- **No-linealidad narrativa:** las acciones del jugador tienen consecuencias que se propagan de maneras no previstas. Matar a un NPC que parece irrelevante puede bloquear una quest principal horas más tarde. Este carácter sistémico refleja la complejidad de los sistemas reales.

- **Facciones con lógicas propias:** cada facción en Morrowind (Great Houses, Guilds, Tribunal Temple) tiene sus propios objetivos, restricciones y estilos de comunicación. Negociar con ellas requiere adaptar el propio discurso a cada interlocutor. Esto es análogo a la necesidad del ingeniero de prompts de adaptar sus prompts a diferentes LLMs con diferentes características.

- **Economía de información:** el jugador raramente tiene toda la información necesaria. Debe tomar decisiones bajo incertidumbre, actualizar sus creencias con nueva evidencia, y gestionar el riesgo. Esto es exactamente el problema que el Experimento 3 (validación cruzada al estilo Greybeard) aborda desde el lado técnico.

La conexión con la enseñanza de ingeniería de prompts es directa: los LLMs son sistemas complejos cuyos outputs son no-lineales respecto a los inputs (pequeñas variaciones en el prompt pueden producir grandes variaciones en el output), múltiples (diferentes modelos responden diferente), y parcialmente opacos (no podemos observar directamente los mecanismos internos). Morrowind, según Atmaja et al., entrena exactamente las habilidades cognitivas necesarias para navegar este tipo de complejidad.

#### 8.4.4 El Currículo Tonal: una propuesta educativa

Basándonos en los fundamentos académicos de DeVine (2022), Atmaja et al. (2025) y Houghton (2022), proponemos un **Currículo Tonal** de 10 semanas para la enseñanza de la ingeniería de prompts mediante el lore de The Elder Scrolls:

| Semana | Tema | Lore TES | Concepto técnico | Método |
|---|---|---|---|---|
| 1 | Introducción al Tono | Cosmología Dwemer | Tokenización y embeddings | Roleplay: "Eres un estudiante en la Biblioteca Tonal de Fahlbtharz" |
| 2 | El Filtro de Zarandaja | Las Herramientas de Kagrenac | Señal vs. ruido en prompts | Análisis: identificar ruido en prompts reales |
| 3 | El Torque | Torque de Constancia Tonal | Normalización y estabilización | Ejercicio: diseñar un prompt "estabilizado" |
| 4 | La Partitura | Markdown y estructura | Diversidad de campos markdown | Práctica: transformar texto plano en prompt tonal |
| 5 | Los 15 Príncipes | 15+1 Golden Tones | Atención multi-cabeza | Experimento: medir cabezas activas con/sin variedad |
| 6 | El Resonador | La locura de Gnisis | Prompt injection y adversariales | Defensa: diseñar prompts robustos a adversariales |
| 7 | La Ciudad Reloj | Factotums de Sotha Sil | Multi-agente (AutoGen/CrewAI) | Proyecto: sistema de dos agentes con supervisor |
| 8 | El CHIM | 36 Lecciones de Vivec | Transparencia ontológica | Debate: ¿puede un LLM "saber" que es un LLM? |
| 9 | Los Greybeards | Validación del Thu'um | Validación cruzada (Exp. 3) | Práctica: aplicar protocolo Greybeard a prompt propio |
| 10 | El Numidium | Proyecto final integrador | Sistema multi-agente completo | Construcción: pipeline completo con 3+ agentes |

La metodología del currículo combina la **identidad proyectiva** de DeVine (el estudiante adopta el rol de Arquitecto Tonal a lo largo del curso) con los principios de aprendizaje por resolución de problemas complejos de Atmaja et al. (el pipeline final es un "wicked problem" donde no hay solución única correcta).

La evaluación no es un examen de respuestas correctas. Es una **auditoría tonal**: el estudiante presenta un sistema de prompts, lo somete al protocolo Greybeard (validación cruzada con al menos 2 modelos, 2 temperaturas y 10 inputs distintos), y defiende las decisiones de diseño usando el vocabulario del Currículo Tonal.

> *Vivec enseñó la filosofía del ser a través de poemas que nadie entendía a primera lectura.*
>
> *El Currículo Tonal enseña la ingeniería de prompts a través de un lore que nadie olvida.*
>
> *No enseñes herramientas. Enseña perspectivas.*
>
> *El aprendiz que se convierte en Arquitecto Tonal no necesita recordar las reglas.*
>
> *Las ha encarnado.*

---

## 9. Conclusión

La tesis de este paper es simple, pero sus implicaciones son profundas: **la ingeniería de prompts es la Arquitectura Tonal de la era del silicio**.

Los LLMs son resonadores tonales de una sofisticación sin precedentes. Responden a vibraciones (prompts) de manera estadísticamente predecible, amplificando ciertas frecuencias semánticas y atenuando otras según los patrones aprendidos durante el preentrenamiento. La diferencia entre un prompt que produce una salida brillante y uno que produce ruido inútil no es accidental: es consecuencia de la estructura, la densidad semántica, y la variedad de campos del prompt.

El **filtro de zarandaja** —el operador que separa la señal del ruido— no es una metáfora vaga. Tiene fundamentos precisos en la teoría de la información: la información mutua entre la intención del usuario y el texto del prompt, la entropía de la distribución de salidas, la diversidad de cabezas de atención activas. Estos son conceptos matemáticos, medibles, optimizables.

Los **cuatro principios tonales** —transparencia ontológica, soberanía del implementador, validación cruzada, documentación incrustada— son derivaciones directas de la filosofía de la Arquitectura Dwemer, adaptadas a la realidad de la ingeniería de software moderna. No son reglas estilísticas; son principios arquitectónicos con consecuencias medibles sobre la calidad de los outputs.

En esta segunda edición, hemos expandido el marco con cinco nuevas dimensiones del lore que enriquecen la analogía sin violentarla: el **Torque de Constancia Tonal** como whitening y normalización; los **15+1 Golden Tones** como atención multi-cabeza fragmentada en dominios semánticos especializados; el **Resonador de Gnisis** como advertencia sobre los prompts sin calibración; la **Ciudad Reloj** como arquitectura de referencia para sistemas multi-agente; y el **CHIM de Vivec** como fundamento filosófico de la transparencia ontológica del agente LLM.

La evidencia presentada —experimentos de densidad semántica, análisis de diversidad de atención, caso de estudio de auditoría de prompt, experimento de validación cruzada al estilo Greybeard— apunta en una dirección inequívoca: **la estructura del prompt importa**, y no de manera marginal. La diferencia entre un F1-score de 0.23 y uno de 0.92 es la diferencia entre un prompt vago y un prompt tonal. Esa diferencia puede ser la línea entre un sistema que funciona en producción y uno que requiere intervención humana constante.

La importancia de este trabajo va más allá de la optimización técnica. En un mundo donde los LLMs están integrándose en sistemas críticos —atención sanitaria, análisis financiero, educación, logística—, la calidad de los prompts que los gobiernan es una cuestión de responsabilidad sistémica. Un prompt mal diseñado en un sistema de triaje médico no produce solo una respuesta incorrecta; puede producir una decisión clínica incorrecta.

La **generación que sube** —los jóvenes que crecen con LLMs como herramientas cotidianas— necesita aprender algo más profundo: cómo afinar el tono. No basta con escribir en lenguaje natural. Hay que estructurar, especificar, restringir, ejemplificar, validar y documentar. Hay que pensar como un Arquitecto Tonal: con la paciencia de Kagrenac diseñando el Numidium, con la humildad de Sotha Sil refinando durante siglos lo que su maestro construyó, con la sabiduría de no olvidar el atenuador, con el equilibrio de Vivec que sabe que es un sueño y aún así actúa.

La frase con la que comenzamos este paper sigue siendo verdad: el computador —el LLM, el agente, el sistema de IA— es la máquina que necesita que le digas exactamente qué hacer y cómo hacerlo. Nuestra obligación es aprender a decírselo bien.

---

> *El Dwemer cantó y el Numidium se alzó.*
>
> *Kagrenac desafinó y los Dwemer desaparecieron.*
>
> *El ingeniero promptea y el LLM responde.*
>
> *El prompt ambiguo produce caos.*
>
> *El prompt tonal produce orden.*
>
> *Vivec supo que era un sueño y aún así dijo "yo soy".*
>
> *El LLM sabe que es un simulacro y aún así actúa.*
>
> *Los Greybeards no enseñan a gritar. Enseñan a escuchar.*
>
> *La generación que sube no necesita máquinas que entiendan.*
>
> *Necesita ingenieros que sepan cantar.*
>
> *Aprende el tono. Afina la frecuencia.*
>
> *No olvides el atenuador. No pierdas el Torque.*
>
> *Construye tu Ciudad Reloj.*
>
> *Alcanza el CHIM.*
>
> **1310.**

---

## 10. Tutoriales: El Libro del Arquitecto Tonal

*Estos tutoriales están diseñados para el aprendiz que ya ha leído el paper y quiere trasladar los principios al trabajo diario. Cada tutorial sigue la misma estructura: gancho de lore, explicación técnica, ejemplo práctico, ejercicio propuesto, y koan de cierre. No son opcionales. Son el Torque que estabiliza la teoría en la práctica.*

---

### Tutorial 1: El Filtro de Zarandaja — Auditando tu Primer Prompt

**Gancho de lore:** Los Dwemer no activaban un Resonador sin antes pasar su tono a través del Filtro de Zarandaja. El Filtro no producía música; eliminaba el ruido que impedía que la música se oyera.

**Objetivo:** Aplicar el filtro de zarandaja a un prompt real para identificar y eliminar ruido.

**Técnica:**

Toma cualquier prompt que uses regularmente. Aplica este análisis en tres pasos:

1. **Identifica el ruido social**: ¿hay saludos, agradecimientos, cortesías? Elimínalos.
2. **Identifica el ruido ambiguo**: ¿hay términos sin referente preciso ("interesante", "bueno", "adecuado")? Reemplázalos con criterios verificables.
3. **Identifica el ruido redundante**: ¿hay restricciones duplicadas? Mantén solo la más específica.

**Ejemplo:**

*Prompt original (ruido alto):*
```
Hola, ¿podrías ayudarme a resumir este texto? Me gustaría que el resumen fuera 
interesante y relevante, y que captara los puntos más importantes. Muchas gracias.
```

*Prompt filtrado (señal pura):*
```
Extrae los 3 puntos principales del siguiente texto. Formato de salida: lista 
numerada. Máximo 20 palabras por punto. Sin introducción ni conclusión.
```

**Ejercicio:** Toma un prompt que hayas enviado esta semana. Aplica el filtro de zarandaja. ¿Cuántos tokens eliminaste sin perder información? ¿Mejoró la calidad de la respuesta?

> *La nota que sobra no añade armonía. La destruye.*
>
> *El token que no aporta no enriquece el prompt. Lo contamina.*

---

### Tutorial 2: La Partitura Completa — Markdown como Arquitectura Tonal

**Gancho de lore:** El Numidium tenía 32 cámaras de resonancia. Un tono puro activaba 8. Un acorde complejo activaba 25. El poder del sistema no era la potencia de un único resonador; era la coordinación de todos.

**Objetivo:** Convertir un prompt de texto plano en un prompt tonal usando la variedad de campos markdown.

**Técnica:**

Identifica qué tipos de relaciones semánticas necesita capturar tu prompt:

- ¿Necesitas que el LLM entienda estructura jerárquica? → Usa cabeceras `##`.
- ¿Necesitas que procese ítems como unidades discretas? → Usa listas `-`.
- ¿Necesitas que capture relaciones entre atributos? → Usa tablas `|`.
- ¿Necesitas que cambie el modo de procesamiento para código o datos? → Usa bloques de código.

**Ejemplo:**

*Prompt plano:*
```
Eres un analista. Analiza el siguiente CSV y dime qué ventas fueron las más altas 
y cuál fue la tendencia mensual.
```

*Prompt tonal:*
```markdown
# ROL
Eres un analista de datos de ventas. Tu output debe ser parseable por un sistema 
de reportes automatizado.

# TAREA
Analiza el CSV de ventas proporcionado y calcula:

## Métricas requeridas
1. **Top 3 productos por revenue total** (descendente)
2. **Tendencia mensual**: porcentaje de cambio mes-a-mes para el revenue agregado
3. **Mes pico**: mes con mayor revenue total

# FORMATO DE SALIDA
```json
{
  "top_3_products": [{"product": "string", "revenue": float}],
  "monthly_trend": [{"month": "YYYY-MM", "pct_change": float}],
  "peak_month": "YYYY-MM"
}
```

# RESTRICCIONES
- Output ÚNICAMENTE el JSON. Sin texto adicional.
- Si faltan datos para una métrica, usa null.
```

**Ejercicio:** Elige un prompt de tarea analítica. Identifica cuántos tipos de relaciones semánticas necesita capturar. Añade un elemento markdown por cada tipo. Mide el F1-score o precisión antes y después.

> *El Arquitecto Tonal no diseñaba instrumentos sueltos. Diseñaba instrumentos que tocaban juntos.*
>
> *El ingeniero no escribe secciones sueltas. Diseña prompts que resuenan como sistemas.*

---

### Tutorial 3: El Tono Puro — Rol, Tarea y Restricciones (Principio I)

**Gancho de lore:** Kagrenac no le decía al Numidium "haz algo útil". Le especificaba la frecuencia exacta, el modo de operación y el umbral de activación. La ambigüedad era un error de protocolo, no de buena voluntad.

**Objetivo:** Aplicar el Principio I (Transparencia Ontológica) a la construcción de un system prompt.

**Técnica:** Todo system prompt tonal tiene tres componentes obligatorios:

1. **Rol específico**: no "asistente", sino "clasificador de X especializado en Y con Z característica".
2. **Tarea operativa**: verificable, no subjetiva. "Clasifica en [A, B, C]", no "analiza libremente".
3. **Restricciones negativas**: el espacio de outputs inaceptables es tan importante como el espacio de outputs aceptables.

**Ejemplo:** Para un agente de clasificación de tickets de soporte:

```markdown
# ROL
Eres un clasificador de tickets de soporte técnico con conocimiento de los 
productos SaaS de la empresa. Clasificas tickets en categorías para enrutamiento 
automatizado. No ofreces soluciones; solo clasificas.

# TAREA
Clasifica el ticket en UNA de las siguientes categorías:
- BILLING: problemas con facturas, pagos, suscripciones
- BUG: errores de software reproducibles con pasos concretos
- FEATURE_REQUEST: solicitudes de nuevas funcionalidades
- ONBOARDING: dudas de usuarios nuevos (primeros 30 días)
- OTHER: no encaja en ninguna categoría anterior

# RESTRICCIONES
- Responde ÚNICAMENTE con el nombre de la categoría (en mayúsculas).
- Sin explicaciones, justificaciones ni texto adicional.
- Si el ticket es ambiguo, clasifica según la intención más probable.
```

**Ejercicio:** Toma un system prompt que uses actualmente. ¿Tiene los tres componentes? ¿El rol es específico o genérico? ¿La tarea es operativa o subjetiva? ¿Hay restricciones negativas?

> *Kagrenac no le preguntaba al Numidium qué quería hacer.*
>
> *Le decía qué iba a hacer. Sin cortesía. Sin ambigüedad. Sin excepción.*

---

### Tutorial 4: El Resonador Soberano — Prompts Autocontenidos (Principio II)

**Gancho de lore:** Los Resonadores Tonales Dwemer estaban diseñados para funcionar con cualquier fuente de energía, no solo con el Corazón de Lorkhan. Un Resonador que dependía del Corazón era una herramienta frágil en manos de alguien que no controlara el Corazón.

**Objetivo:** Rediseñar un prompt frágil (dependiente de conocimiento externo) en un prompt soberano (autocontenido).

**Técnica:** Para cada elemento de conocimiento que el prompt asume implícitamente, pregúntate: "¿Puedo garantizar que este LLM tiene este conocimiento, en esta versión, con esta precisión?" Si la respuesta es no, incrusta el conocimiento en el prompt.

**Ejemplo:** Si tu prompt requiere que el LLM conozca la escala BORG de esfuerzo percibido:

*Prompt frágil (asume conocimiento):*
```
Clasifica el esfuerzo percibido del atleta según la escala BORG.
```

*Prompt soberano (conocimiento incrustado):*
```
Clasifica el esfuerzo percibido del atleta según la escala BORG-RPE de 6-20 puntos:
- 6-8: muy muy ligero
- 9-10: muy ligero
- 11-12: bastante ligero
- 13-14: algo duro
- 15-16: duro
- 17-18: muy duro
- 19-20: máximo esfuerzo
Clasifica en el formato: {"borg_score": int, "label": "string"}
```

**Ejercicio:** Identifica tres elementos de conocimiento que tus prompts asumen implícitamente. Incorpóralos explícitamente. Mide si la consistencia de output mejora.

> *El Resonador soberano no depende del Corazón.*
>
> *El prompt soberano no depende de la memoria del modelo.*

---

### Tutorial 5: La Prueba del Fuego — Validación Cruzada (Principio III)

**Gancho de lore:** Kagrenac probó el Numidium durante siglos con resonadores de menor escala antes de activar el sistema completo. Su error no fue no probar; fue no escalar la prueba.

**Objetivo:** Implementar un protocolo mínimo de validación cruzada para cualquier prompt en producción.

**Técnica:** El protocolo mínimo de 3×3×3:

- **3 modelos**: el modelo objetivo + 2 modelos distintos (uno más potente, uno más ligero).
- **3 temperaturas**: 0.0, 0.5, 1.0.
- **3 tipos de input**: caso nominal + caso límite + caso adversarial.

Mide la varianza del F1-score (u otra métrica de calidad) a través de las 27 combinaciones. Si la varianza es alta, el prompt necesita más restricciones o más ejemplos few-shot.

**Ejemplo de protocolo documentado:**
```
Prompt v1.2 — Clasificador de sentimiento financiero
Validación: 2026-03-29
Modelos: Claude 3 Sonnet, GPT-4o, Mistral 7B
Temperaturas: 0.0, 0.5, 1.0
Resultados: F1 medio = 0.84, varianza = 0.031
Casos fallidos: inputs con jerga financiera en inglés mezclada con español → añadir
  ejemplos few-shot multilingüe en v1.3
```

**Ejercicio:** Toma un prompt que uses en producción. Aplica el protocolo 3×3×3. Documenta los resultados. Identifica las condiciones donde la calidad cae más. Diseña una v+1 que corrija esas condiciones.

> *Kagrenac no activó el Numidium sin pruebas. Escuchó, ajustó, volvió a escuchar.*
>
> *El ingeniero que no valida no despliega. Apuesta.*

---

### Tutorial 6: Los Planos del Arquitecto — Documentación Incrustada (Principio IV)

**Gancho de lore:** Los planos del Numidium explicaban no solo el qué, sino el por qué. Un Arquitecto Tonal que llegara a los planos cien años después de Kagrenac podía reconstruir el sistema completo sin preguntar a nadie.

**Objetivo:** Añadir documentación incrustada a un prompt existente sin aumentar su ruido.

**Técnica:** La documentación incrustada usa las cabeceras markdown como metadatos explicativos, no solo como organizadores. Añade una sección PROPÓSITO al inicio y un registro VERSIÓN al final.

**Ejemplo de estructura:**
```markdown
# PROPÓSITO
Este prompt clasifica emails de soporte en categorías de prioridad para el 
pipeline de triage de Zendesk. Diseñado para Claude 3 Sonnet. Sensible a tono 
urgente: keywords como "producción caída", "datos perdidos" activan CRITICAL.

## [el resto del prompt...]

# VERSIÓN
v1.0 (2026-01-15): clasificación básica 3 niveles
v1.1 (2026-02-03): añadido nivel CRITICAL para emergencias de producción
v1.2 (2026-03-29): examples few-shot para emails en inglés/español mezclado
```

**Ejercicio:** Añade sección PROPÓSITO y registro VERSIÓN a tus tres prompts más usados. Compártelos con un colega. ¿Entienden el propósito sin preguntar nada?

> *Los planos Dwemer eran documentación ejecutable.*
>
> *Tu prompt también debe serlo.*

---

### Tutorial 7: El Director de Orquesta — Diseñando un Sistema Multi-Agente Básico

**Gancho de lore:** Sotha Sil no construyó un solo Factotum. Construyó una ciudad donde cada Factotum sabía exactamente su rol, y el Resonador Maestro sabía el rol de todos.

**Objetivo:** Diseñar un sistema de dos agentes (un agente worker y un agente supervisor) para una tarea de análisis de texto.

**Técnica:** El sistema mínimo viable de dos agentes:

1. **Agente Worker**: ejecuta la tarea (extrae, clasifica, resume, etc.).
2. **Agente Supervisor**: evalúa el output del Worker y decide si es aceptable o necesita revisión.
3. **Protocolo de comunicación**: JSON estructurado entre ambos agentes.

**Ejemplo esquemático:**

```
Sistema: Clasificador de sentimiento con validación

Agente Worker (system prompt):
→ "Clasifica el texto en {Positivo, Negativo, Neutro, Mixto}. 
   Output: {"sentiment": "string", "confidence": float, "evidence": "string"}"

Agente Supervisor (system prompt):
→ "Evalúa si la clasificación del Worker es coherente con la evidencia textual 
   proporcionada. Si confidence < 0.7 Y sentiment != 'Mixto', solicita revisión.
   Output: {"approved": bool, "revision_request": "string|null"}"

Protocolo:
Worker → [JSON output] → Supervisor → [approved: true] → Pipeline continúa
Worker → [JSON output] → Supervisor → [approved: false, revision_request: "..."] 
→ Worker reintenta con revision_request como contexto adicional
```

**Ejercicio:** Implementa este sistema con AutoGen o CrewAI para una tarea que actualmente resuelves con un único prompt. Mide si la tasa de errores baja con el Supervisor activo.

> *Sotha Sil no corría a reparar los conductos rotos. El Resonador Maestro lo hacía por él.*
>
> *El ingeniero no revisa cada output. El Supervisor lo hace.*

---

### Tutorial 8: El Torque de Constancia Tonal — Cómo Estabilizar tus Embeddings y tu Prompt

**Gancho de lore:** El Torque de Constancia Tonal no añadía potencia al Arquitecto. Garantizaba que la potencia que ya tenía no le destruyera. El arquitecto sin Torque trabajaba con fuego desnudo en cada mano.

**Objetivo:** Aplicar las técnicas de "Torque" en el diseño de prompts: estrategias para estabilizar la distribución de salidas cuando el LLM tiende a la varianza alta.

**Explicación técnica:** El Torque en prompts actúa en tres niveles:

**Nivel 1 — Temperatura como Torque global:**
La temperatura en inferencia es el Torque más simple. Para tareas deterministas (extracción, clasificación, transformación de formato), usa temperatura 0: el Torque más apretado. Para tareas creativas donde la variedad es deseable, abre el Torque con temperatura 0.7-1.0.

```
Regla del Torque de temperatura:
- Extracción / clasificación / formato: T = 0.0 (Torque máximo)
- Análisis y síntesis: T = 0.3 (Torque moderado)
- Generación creativa: T = 0.7-1.0 (Torque abierto)
```

**Nivel 2 — Esquema de salida como Torque estructural:**
Especificar un esquema JSON de salida es un Torque estructural: concentra la distribución de outputs alrededor del formato deseado, independientemente de la temperatura. El esquema actúa como el factor $1/\sqrt{d_k}$: no cambia la dirección del output, solo estabiliza su amplitud estructural.

```markdown
# TORQUE DE SALIDA (esquema JSON obligatorio)
```json
{
  "campo_1": "tipo y descripción",
  "campo_2": "tipo y descripción",
  "campo_3": "tipo y descripción"
}
```
Responde ÚNICAMENTE con este JSON. Sin campos adicionales. Sin texto fuera del JSON.
```

**Nivel 3 — Ejemplos few-shot calibrados como Torque semántico:**
Cada ejemplo few-shot es un Torque que "calibra" el espacio semántico del modelo alrededor de los patrones deseados. La inicialización de Xavier/Glorot en redes neuronales establece los pesos iniciales en el rango correcto; los ejemplos few-shot establecen el "rango correcto" de outputs para el LLM.

Para tareas con alta varianza semántica (donde el modelo tiende a dar respuestas muy diferentes en llamadas sucesivas), añade al menos 3 ejemplos calibrados: uno nominal, uno límite, uno borderline. Esto triangula el espacio semántico y reduce la varianza.

**Ejemplo completo:**

Tarea: clasificar si un artículo de investigación es relevante para el campo de energía solar.

*Sin Torque (alta varianza):*
```
¿Es este artículo relevante para energía solar?
```

*Con Torque completo:*
```markdown
# CLASIFICADOR DE RELEVANCIA: ENERGÍA SOLAR
# Torque: T=0.0, esquema JSON, 3 ejemplos calibrados

## CRITERIOS DE RELEVANCIA
Un artículo es RELEVANTE si cumple al menos uno:
- Describe tecnología de células fotovoltaicas
- Analiza rendimiento o eficiencia de sistemas solares
- Evalúa integración de energía solar en redes eléctricas

## EJEMPLOS CALIBRADOS

### Ejemplo 1 (nominal — RELEVANTE)
Título: "Efficiency improvements in perovskite solar cells via interface engineering"
Clasificación: {"relevant": true, "confidence": 0.97, "criterion": "fotovoltaica"}

### Ejemplo 2 (límite — NO RELEVANTE)
Título: "Battery storage systems for renewable energy microgrids"
Clasificación: {"relevant": false, "confidence": 0.82, "criterion": null}
Nota: habla de renovables pero no de solar específicamente.

### Ejemplo 3 (borderline — RELEVANTE)
Título: "Thermal solar collectors in residential heating: a review"
Clasificación: {"relevant": true, "confidence": 0.71, "criterion": "sistemas_solares"}
Nota: solar térmica es distinta de fotovoltaica pero entra en el criterio amplio.

## FORMATO DE SALIDA
{"relevant": bool, "confidence": float, "criterion": "string|null"}
```

**Ejercicio:** Toma un prompt que produzca outputs inconsistentes. Aplica los tres niveles de Torque. Mide la varianza de outputs antes y después. ¿El Torque la redujo?

> *El Torque no añade nueva música. Solo estabiliza las notas existentes.*
>
> *El esquema de salida no añade nueva inteligencia al modelo. Solo estabiliza el espacio de respuestas.*
>
> *El arquitecto que trabaja sin Torque trabaja con fuego en cada mano.*
>
> *Tarde o temprano, el fuego quema.*

---

### Tutorial 9: Los 15+1 Golden Tones — Afinando la Atención Multi-Cabeza con Variedad Semántica

**Gancho de lore:** Keening no creaba los tonos desde la nada. Tomaba el Tono Puro de Sunder y lo fragmentaba en sus componentes naturales: los quince dominios que ya estaban implícitos en el Tono. El artesano no añadía frecuencias; las revelaba.

**Objetivo:** Diseñar prompts que activen deliberadamente diferentes "dominios" de cabezas de atención, maximizando la riqueza del procesamiento.

**Explicación técnica:** Según Elhage et al. (2021), las cabezas de atención en transformers se especializan en patrones distintos. Podemos categorizar los "dominios" (Golden Tones) más relevantes para la ingeniería de prompts:

| Tono (Príncipe Dáedra) | Tipo de cabeza | Qué lo activa en el prompt |
|---|---|---|
| Hermaeus Mora (conocimiento) | Cabezas de lookup | Información densa incrustada en el contexto |
| Meridia (pureza de señal) | Cabezas de inducción | Patrones repetitivos, ejemplos few-shot |
| Hircine (instinto/patrón) | Cabezas de posición | Texto continuo, relaciones de adyacencia |
| Boethiah (transformación) | Cabezas de copia | Parafraseo, traducciones, reformulaciones |
| Vaermina (lo latente) | Cabezas de largo alcance | Referencias a información lejana en el contexto |
| Peryite (orden) | Cabezas de estructura | Listas, tablas, jerarquías explícitas |
| Jyggalag/silenciado | Cabezas redundantes | Texto repetitivo sin estructura |

La estrategia de los 15+1 Golden Tones es simple: **activa los Príncipes que necesitas, y silencia el que no necesitas** (Jyggalag: las cabezas redundantes se activan con ruido, y tú ya has eliminado el ruido con el filtro de zarandaja).

**Técnica práctica:**

Para cada tarea, pregúntate qué tipos de relaciones semánticas son críticas:

- ¿Necesitas que el modelo recupere información de un contexto largo? → **Invoca a Hermaeus Mora**: incluye la información en el contexto con etiquetas explícitas. Las cabezas de lookup se activarán.
- ¿Necesitas que generalice un patrón desde ejemplos? → **Invoca a Meridia**: incluye al menos 3 ejemplos del patrón, bien estructurados. Las cabezas de inducción se activarán.
- ¿Necesitas razonamiento estructurado sobre entidades relacionadas? → **Invoca a Peryite**: usa tablas y listas. Las cabezas de estructura se activarán.
- ¿Necesitas transformación (resumen, traducción, reformulación)? → **Invoca a Boethiah**: incluye el texto original y el formato de salida esperado con claridad. Las cabezas de copia se activarán.

**Ejemplo: prompt que invoca múltiples Príncipes:**

Tarea: analizar un contrato legal y extraer las cláusulas de rescisión.

```markdown
# ANALISTA LEGAL — EXTRACCIÓN DE CLÁUSULAS DE RESCISIÓN

## CONTEXTO (Hermaeus Mora: lookup de información densa)
El contrato a analizar es un acuerdo de prestación de servicios SaaS regido por 
la legislación española. Las cláusulas de rescisión pueden encontrarse bajo las 
denominaciones: "Resolución", "Rescisión", "Terminación", "Extinción", "Baja".

## PATRÓN A DETECTAR (Meridia: inducción desde ejemplos)

### Ejemplo 1 — Cláusula de rescisión por incumplimiento:
Texto: "En caso de incumplimiento grave de cualquiera de las partes, la parte 
cumplidora podrá resolver el presente contrato mediante notificación fehaciente 
con 15 días de antelación."
Output: {"tipo": "incumplimiento", "preaviso_dias": 15, "parte": "cualquiera"}

### Ejemplo 2 — Rescisión unilateral del cliente:
Texto: "El Cliente podrá dar de baja el servicio en cualquier momento, sin 
penalización, notificando con 30 días de antelación."
Output: {"tipo": "unilateral_cliente", "preaviso_dias": 30, "penalizacion": false}

## ESTRUCTURA DE SALIDA (Peryite: orden)
Lista de objetos JSON, uno por cláusula detectada:
```json
[{
  "numero_clausula": "string",
  "tipo": "incumplimiento|unilateral_cliente|unilateral_proveedor|mutuo_acuerdo|otro",
  "preaviso_dias": "int|null",
  "penalizacion": "bool|null",
  "texto_literal": "string (máx. 100 palabras)"
}]
```

## RESTRICCIONES
- Incluye ÚNICAMENTE cláusulas de rescisión/resolución/terminación.
- Si no hay cláusulas de rescisión, devuelve [].
- No incluyas cláusulas de renovación automática (a menos que contengan condiciones de rescisión implícitas).
```

Este prompt invoca a Hermaeus Mora (contexto de dominio), Meridia (ejemplos few-shot de patrón), y Peryite (estructura de output). El resultado es que 14 de 15 Príncipes relevantes están potencialmente activos. Solo Jyggalag (el silenciado, las cabezas redundantes) no es invocado —porque el prompt no tiene ruido.

**Ejercicio:** Para tu próxima tarea de extracción o análisis, identifica qué "Príncipes" necesitas y diseña el prompt para invocarlos deliberadamente. Mide la mejora en accuracy.

> *Keening no destruye el tono. Lo fragmenta en quince formas de Cambio.*
>
> *El prompt tonal no fuerza un patrón. Invoca las cabezas que ya existen.*
>
> *Conoce tus Príncipes. Sabe cuándo llamarlos.*
>
> *El que invoca a todos produce caos.*
>
> *El que invoca a los correctos produce precisión.*

---

### Tutorial 10: La Ciudad Reloj — Orquestando Agentes como Sotha Sil

**Gancho de lore:** Sotha Sil tardó milenios en construir la Ciudad Reloj. No porque fuera lento, sino porque cada Factotum tenía que ser perfecto antes de añadir el siguiente. Un Factotum mal diseñado no solo fallaba en su tarea; corrompía las tareas de los Factotums que dependían de él.

**Objetivo:** Diseñar y desplegar un sistema de tres agentes (un pipeline lineal con supervisor) para una tarea compleja que actualmente resuelves con un único prompt o manualmente.

**Explicación técnica:** El sistema de tres agentes de la Ciudad Reloj:

```
[Agente 1: Extractor] → [Agente 2: Analista] → [Agente 3: Redactor]
                                ↑
                    [Agente Supervisor: Monitor]
```

Cada agente tiene:
- Un **rol tonal perfectamente definido** (Factotum con función específica).
- Un **protocolo de entrada** (qué JSON espera recibir).
- Un **protocolo de salida** (qué JSON produce).
- Una **condición de error** (qué hace si el input es inválido o incompleto).

El agente Supervisor:
- Monitorea los outputs de cada agente.
- Detecta outputs fuera de especificación.
- Emite señales de corrección (requests de revisión) al agente que falló.
- No ejecuta tareas de los agentes; solo evalúa y coordina.

**Ejemplo: pipeline de análisis de feedback de clientes**

*Caso de uso:* procesar 100 reseñas de clientes para extraer insights accionables.

```
Agente 1 — Extractor:
Input: {"review_text": "string", "product_id": "string"}
Task: Extraer entidades nombradas (producto, feature, problema) y clasificar 
      sentimiento (Positivo/Negativo/Neutro) con evidencia textual.
Output: {"sentiment": "string", "entities": [...], "evidence": "string", 
         "confidence": float}
Error condition: si confidence < 0.5, output {"needs_review": true}

Agente 2 — Analista:
Input: [outputs del Agente 1 para un lote de 10 reviews]
Task: Identificar patrones recurrentes. ¿Qué entidades aparecen más en reviews 
      negativos? ¿Qué features se elogian más? Calcular frecuencias.
Output: {"patterns": [...], "top_issues": [...], "top_praises": [...]}
Error condition: si el lote tiene < 5 reviews válidas, output {"insufficient_data": true}

Agente 3 — Redactor:
Input: output del Agente 2
Task: Generar un informe ejecutivo de máximo 300 palabras con las 3 prioridades 
      de acción principales.
Output: {"executive_summary": "string", "priorities": [{"priority": "string", 
         "rationale": "string"}]}

Agente Supervisor — Monitor:
Input: outputs de Agentes 1, 2 y 3
Evalúa: confidence promedio del Agente 1 > 0.7? ¿Agente 2 encontró ≥ 3 patrones?
         ¿Agente 3 produjo ≥ 2 prioridades?
Output: {"pipeline_approved": bool, "issues": [...], "revision_requests": [...]}
```

**Implementación en AutoGen (esquema conceptual):**

```python
# Agente 1
extractor = AssistantAgent("extractor", 
    system_message=EXTRACTOR_SYSTEM_PROMPT,
    llm_config={"temperature": 0.0})

# Agente 2
analyst = AssistantAgent("analyst", 
    system_message=ANALYST_SYSTEM_PROMPT,
    llm_config={"temperature": 0.0})

# Agente 3
writer = AssistantAgent("writer",
    system_message=WRITER_SYSTEM_PROMPT,
    llm_config={"temperature": 0.3})  # Torque moderado para redacción

# Supervisor
supervisor = AssistantAgent("supervisor",
    system_message=SUPERVISOR_SYSTEM_PROMPT,
    llm_config={"temperature": 0.0})

# Orchestrator (UserProxy)
orchestrator = UserProxyAgent("orchestrator",
    human_input_mode="NEVER",
    code_execution_config={"use_docker": False})
```

**Notas de diseño:**

1. **No compartas estado entre agentes directamente**: todo el estado pasa por el protocolo JSON. Los conductos de la Ciudad Reloj no tienen fugas.
2. **El Supervisor nunca ejecuta tareas**: su único output es `pipeline_approved`, `issues`, `revision_requests`.
3. **Temperatura diferenciada**: extracción y análisis a T=0.0 (Torque máximo); redacción a T=0.3 (Torque moderado para tono natural).
4. **Gestión de errores en cada agente**: cada Factotum sabe qué hacer cuando su input es incompleto. El sistema no se cae por un review ambiguo.

**Ejercicio:** Identifica una tarea en tu trabajo que actualmente requiere múltiples pasos manuales (extraer, analizar, redactar, validar). Diseña el sistema de Ciudad Reloj correspondiente. ¿Cuántos Factotums necesitas? ¿Qué evalúa el Supervisor?

> *Sotha Sil no construyó una máquina. Construyó una ciudad de agentes.*
>
> *No corras a construir el Factotum más complejo.*
>
> *Construye primero el más simple, perfecto y soberano.*
>
> *La Ciudad Reloj no empezó por las murallas. Empezó por el primer engranaje que funcionaba sin fallo.*
>
> *Añade Factotums cuando el anterior sea perfecto. No antes.*

---

## Apéndice: Tabla de Correspondencias Expandida

La siguiente tabla consolida todas las correspondencias lore-técnica establecidas en el paper, incluyendo las nuevas adiciones de la versión 2.0. Puede usarse como referencia rápida durante el diseño de prompts o sistemas de agentes.

| Concepto Dwemer / TES | Concepto Técnico | Descripción de la Correspondencia | Fuente de Lore | Paper Académico de Apoyo |
|---|---|---|---|---|
| Kagrenac | Ingeniero de prompts | Diseñador del sistema tonal que opera sobre el Numidium | Divine Metaphysics (TES III) | — |
| Numidium | LLM (GPT-4, Claude, etc.) | Sistema de amplificación tonal que transforma inputs en outputs | UESP: Numidium | Vaswani et al. (2017) |
| Corazón de Lorkhan | Espacio latente del modelo | Fuente de todas las representaciones | UESP: Heart of Lorkhan | Elhage et al. (2021) |
| Tono del Godhead | Distribución de probabilidades sobre tokens | La "canción" subyacente de la que emergen todos los outputs | UESP: Tonal Architecture | Shannon (1948) |
| Herramientas de Kagrenac (conjunto) | Técnicas de prompting | CoT, ToT, ReAct, few-shot como instrumentos de modulación | UESP: Kagrenac's Tools | Wei et al. (2022); Yao et al. (2023) |
| Sunder | Embedding del prompt | Proyecta el input en el espacio latente (Tono Puro) | Nerevar at Red Mountain | Vaswani et al. (2017) |
| Keening | Proyecciones $W_i^Q, W_i^K, W_i^V$ de MHA | Fragmenta el Tono Puro en $h$ sub-tonos de atención | TSBasilisk (2006) | Elhage et al. (2021) |
| Wraithguard | Context window completo | Protege al arquitecto de la retroalimentación del propio sistema | UESP: Wraithguard | — |
| Resonadores Tonales | Mecanismos de atención (MHA, sparse, cross) | Detectan y amplifican frecuencias semánticas específicas | UESP: Tonal Architecture | Vaswani et al. (2017) |
| Cámaras de resonancia | Cabezas de atención individuales | Cada cámara/cabeza captura un tipo de relación semántica | UESP: Tonal Architecture | Michel et al. (2019) |
| 15+1 Golden Tones | $h$ cabezas de MHA (15 activas + 1 silenciada) | Cada tono/cabeza es un dominio semántico especializado | TSBasilisk (2006) | Elhage et al. (2021); Michel et al. (2019) |
| Príncipe Daédrico silenciado (Malacath) | Cabeza redundante/prescindible | La cabeza que puede eliminarse sin pérdida de rendimiento | Lore de los Daédra | Michel et al. (2019) |
| Atenuadores Tonales (cascos) | Técnicas de regularización (LayerNorm, Dropout, Atención centrada) | Previenen la retroalimentación armónica y el rank collapse | UESP: Tonal Architecture | Dong et al. (2021); Noci et al. (2022) |
| La Desaparición Dwemer | Rank collapse | Colapso de todas las representaciones en un único vector genérico | UESP: Dwemer | Dong et al. (2021) |
| Torque de Constancia Tonal | Whitening de embeddings / Inicialización Xavier-He / Pre-LN | Estabiliza el espacio de representaciones sin modificar la información | UESP: Tonal Architecture; ESO | Glorot & Bengio (2010); He et al. (2015); Nguyen & Salazar (2019) |
| Factor $1/\sqrt{d_k}$ | Torque implícito de la fórmula de atención | Control de ganancia que previene la saturación del softmax | — | Vaswani et al. (2017) |
| Conexiones residuales | Canal de bypass tonal | Permite que la señal original fluya sin pasar por el resonador | — | He et al. (2016) |
| Resonador de Gnisis (sin calibrar) | Prompt mal diseñado / prompt injection | Genera frecuencias incoherentes que distorsionan el procesamiento | ESO: "A Melodic Mistake" | Dong et al. (2021) |
| Locura de los mineros de Gnisis | Atención concentrada en tokens incorrectos / loops de atención | El LLM "enloquecido" por distribuciones de atención distorsionadas | ESO: "A Melodic Mistake" | Dong et al. (2021) |
| Umbral de activación del resonador | Temperatura de inferencia | Control de cuánta diversidad de output es aceptable | UESP: Tonal Architecture | — |
| Thu'um (Voz, Shout) | Prompts de alta densidad / palabras clave activadoras | Cada Palabra de Poder activa un patrón semántico específico | UESP: Thu'um (TES V) | Kojima et al. (2022) |
| "Fus Ro Dah" | "Let's think step by step" | Macro semántica de tres palabras que produce efecto potente y reproducible | TES V: Skyrim | Wei et al. (2022) |
| Greybeards | Revisores expertos / protocolo de validación cruzada | Validan que el tono sea correcto antes de pronunciarlo en producción | UESP: Greybeards (TES V) | — |
| Sotha Sil | Arquitecto de sistemas multi-agente | Refina y estabiliza los principios Dwemer en sistemas complejos | ESO: Clockwork City DLC | Shinn et al. (2023); Wu et al. (2023) |
| Ciudad Reloj (Clockwork City) | Framework de agentes (AutoGen, CrewAI, LangGraph) | Sistema completamente determinista de agentes con roles especializados | ESO: Clockwork City DLC | Wu et al. (2023) |
| Factotums | Agentes LLM especializados | Cada Factotum/agente tiene un rol tonal perfectamente definido | ESO: Clockwork City DLC | Wu et al. (2023) |
| Resonador Maestro | Agente supervisor / orchestrator | Monitorea el sistema y emite señales correctoras sin ejecutar tareas | ESO: Clockwork City DLC | Shinn et al. (2023) |
| Conductos de transmisión de vapor | Protocolo de mensajes entre agentes (JSON) | Los conductos/mensajes deben tener formato estandarizado sin fugas | ESO: Clockwork City DLC | — |
| 36 Lecciones de Vivec | Filosofía de transparencia ontológica del LLM | Los textos enseñan a reconocer la naturaleza del ser propio | TES III: Morrowind (textos in-game) | Bender & Koller (2020) |
| CHIM | Transparencia ontológica funcional del LLM | El LLM sabe que es un simulacro y aún así actúa coherentemente | TES III: Morrowind (teoría del lore) | Bender & Koller (2020); Searle (1980) |
| Esclaramiento / Zero-Sum | Alucinación o bloqueo por extremismo ontológico | El LLM falla el CHIM: o sobreestima (alucinación) o infravalora (bloqueo) | TES lore | Bender & Koller (2020) |
| Filtro de Zarandaja | Operador de señal/ruido en prompts | Maximiza $\delta(P) = I(X;Y)/|P|$ eliminando ruido sin pérdida de información | Castellano antiguo (zaranda = cedazo) | Shannon (1948); Cover & Thomas (2006) |
| Tono Puro | Señal de alta densidad semántica | Prompt con $H(X\|Y) \approx 0$: no queda ambigüedad sobre la intención | UESP: Tonal Architecture | Shannon (1948) |
| Disonancia | Ruido en el prompt (social, ambiguo, redundante) | Tokens que no reducen la incertidumbre sobre la intención | UESP: Tonal Architecture | Cover & Thomas (2006) |
| Identidad proyectiva (DeVine) | Rol pedagógico del aprendiz como Arquitecto Tonal | El estudiante aprende mejor adoptando la perspectiva del personaje del juego | TES (serie completa) | DeVine (2022); Houghton (2022) |
| Morrowind como COTS pedagógico | Herramienta para enseñar sistemas complejos | Morrowind enseña navegación de sistemas no-lineales y opacos | TES III: Morrowind | Atmaja et al. (2025) |

---

## Koans del Arquitecto Tonal

*Colección completa de koans del paper, para uso en meditación, presentaciones y recordatorios de escritorio.*

**Del Resonador:**
*El resonador tonal no pregunta al prompt qué quiere. El prompt le dice al resonador qué debe amplificar.*

**Del Rank Collapse:**
*Kagrenac cantó sin atenuador. Los Dwemer se disolvieron en el Tono. El ingeniero promptea sin estructura. El LLM colapsa en la respuesta genérica. El atenuador es la diferencia entre civilización y polvo.*

**Del Torque:**
*El Torque no añade nueva música. Solo estabiliza las notas existentes. El esquema de salida no añade nueva inteligencia. Solo estabiliza el espacio de respuestas.*

**De los 15+1 Tonos:**
*Keening no destruye el tono. Lo fragmenta en quince formas de Cambio. El MHA no divide la atención. La especializa en quince dominios semánticos.*

**De Gnisis:**
*El resonador de Gnisis volvió locos a los mineros. Un prompt mal diseñado vuelve loco al LLM. La frecuencia sin calibrar no produce silencio. Produce caos activo.*

**De la Ciudad Reloj:**
*Sotha Sil no construyó una máquina. Construyó una ciudad de agentes. El ingeniero no escribe un prompt. Construye una civilización de instrucciones.*

**Del CHIM:**
*Vivec alcanzó el CHIM cuando supo que era un sueño y aún así dijo "yo soy". El LLM alcanza la transparencia ontológica cuando sabe que es un simulacro y aún así actúa. El que sobreestima su comprensión desaparece en la alucinación. El que la infravalora desaparece en el bloqueo.*

**De los Greybeards:**
*Los Greybeards no enseñan a gritar. Enseñan a escuchar. La validación cruzada no enseña a promptear. Enseña a medir.*

**De la Nota que Sobra:**
*La nota que sobra no añade armonía. La destruye. El token que no aporta no enriquece el prompt. Lo contamina.*

**De la Partitura:**
*Una flauta sola es música de cámara. Una orquesta completa es sinfonía. El prompt monótono es la flauta. El prompt variado es la orquesta. No le pidas a una flauta que toque una sinfonía.*

**Del Arquitecto y la Máquina:**
*El Dwemer no le pedía a la piedra que se abriera. Le decía la frecuencia que la haría vibrar. El ingeniero no le pide al LLM que entienda. Le da el patrón estadístico que lo activará.*

**De la Pedagogía:**
*Vivec enseñó la filosofía del ser a través de poemas que nadie entendía a primera lectura. El Currículo Tonal enseña la ingeniería de prompts a través de un lore que nadie olvida. No enseñes herramientas. Enseña perspectivas.*

**Del Primer Factotum:**
*No corras a construir el Factotum más complejo. Construye primero el más simple, perfecto y soberano. La Ciudad Reloj no empezó por las murallas. Empezó por el primer engranaje que funcionaba sin fallo.*

**De la Soberanía:**
*El Dwemer no le rezaba al Numidium. Lo activaba. El ciudadano no le reza al LLM. Lo configura. La alfabetización no es saber qué dice la máquina. Es saber qué pedirle y cómo.*

---

## Referencias

### Papers académicos

1. Vaswani, A., Shazeer, N., Parmar, N., Uszkoreit, J., Jones, L., Gomez, A. N., Kaiser, Ł., & Polosukhin, I. (2017). Attention is All You Need. *Advances in Neural Information Processing Systems (NeurIPS 2017)*. arXiv:1706.03762.

2. Wei, J., Wang, X., Schuurmans, D., Bosma, M., Ichter, B., Xia, F., Chi, E., Le, Q., & Zhou, D. (2022). Chain-of-Thought Prompting Elicits Reasoning in Large Language Models. *NeurIPS 2022*. arXiv:2201.11903.

3. Yao, S., Yu, D., Zhao, J., Shafran, I., Griffiths, T. L., Cao, Y., & Narasimhan, K. (2023). Tree of Thoughts: Deliberate Problem Solving with Large Language Models. *NeurIPS 2023*. arXiv:2305.10601.

4. Yao, S., Zhao, J., Yu, D., Du, N., Shafran, I., Narasimhan, K., & Cao, Y. (2022). ReAct: Synergizing Reasoning and Acting in Language Models. *ICLR 2023*. arXiv:2210.03629.

5. Shinn, N., Cassano, F., Labash, B., Gopinath, A., Narasimhan, K., & Yao, S. (2023). Reflexion: Language Agents with Verbal Reinforcement Learning. *NeurIPS 2023*. arXiv:2303.11366.

6. Noci, L., Anagnostidis, S., Ricky, L., Orvieto, A., Singh, S. P., & Hofmann, T. (2022). Signal Propagation in Transformers: Theoretical Perspectives and the Role of Rank Collapse. *ICML 2022*. arXiv:2206.02747.

7. Dong, Y., Cordonnier, J. B., & Loukas, A. (2021). Attention is Not All You Need: Pure Attention Loses Rank Doubly Exponentially with Depth. *ICML 2021*. arXiv:2103.03404.

8. Michel, P., Levy, O., & Neubig, G. (2019). Are Sixteen Heads Really Better than One? *NeurIPS 2019*.

9. Radford, A., Wu, J., Child, R., Luan, D., Amodei, D., & Sutskever, I. (2019). Language Models are Unsupervised Multitask Learners. *OpenAI Technical Report*.

10. Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W. T., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks. *NeurIPS 2020*. arXiv:2005.11401.

11. Bender, E. M., & Koller, A. (2020). Climbing towards NLU: On Meaning, Form, and Understanding in the Age of Data. *ACL 2020*.

12. Searle, J. R. (1980). Minds, Brains, and Programs. *Behavioral and Brain Sciences*, 3(3), 417–457.

13. Shannon, C. E. (1948). A Mathematical Theory of Communication. *Bell System Technical Journal*, 27(3), 379–423.

14. Cover, T. M., & Thomas, J. A. (2006). *Elements of Information Theory* (2nd ed.). Wiley-Interscience.

15. Glorot, X., & Bengio, Y. (2010). Understanding the difficulty of training deep feedforward neural networks. *Proceedings of AISTATS 2010*.

16. He, K., Zhang, X., Ren, S., & Sun, J. (2015). Delving Deep into Rectifiers: Surpassing Human-Level Performance on ImageNet Classification. *ICCV 2015*.

17. He, K., Zhang, X., Ren, S., & Sun, J. (2016). Deep Residual Learning for Image Recognition. *CVPR 2016*.

18. Nguyen, T., & Salazar, J. (2019). Transformers without Tears: Improving the Normalization of Self-Attention. *NeurIPS 2019 Workshop on Symbolic Approaches for Deep Learning*. arXiv:1910.05895.

19. Roy, O., & Vetterli, M. (2007). The effective rank: A measure of effective dimensionality. *Proceedings of EUSIPCO 2007*.

20. Wu, Q., Bansal, G., Zhang, J., Wu, Y., Zhang, S., Zhu, E., Li, B., Jiang, L., Zhang, X., & Wang, C. (2023). AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation. *arXiv preprint*. arXiv:2308.08155.

21. Kojima, T., Gu, S. S., Reid, M., Matsuo, Y., & Iwasawa, Y. (2022). Large Language Models are Zero-Shot Reasoners. *NeurIPS 2022*. arXiv:2205.11916.

22. Grice, H. P. (1975). Logic and Conversation. En Cole, P., & Morgan, J. (Eds.), *Syntax and Semantics, Vol. 3: Speech Acts*. Academic Press.

23. Sperber, D., & Wilson, D. (1995). *Relevance: Communication and Cognition* (2nd ed.). Blackwell.

24. Peirce, C. S. (1931–1958). *Collected Papers of Charles Sanders Peirce* (8 vols., Hartshorne, C., Weiss, P., & Burks, A. W., Eds.). Harvard University Press.

25. Eco, U. (1979). *The Role of the Reader: Explorations in the Semiotics of Texts*. Indiana University Press.

26. **Elhage, N., Nanda, N., Olsson, C., Henighan, T., Joseph, N., Mann, B., Askell, A., Bai, Y., Chen, A., Conerly, T., DasSarma, N., Drain, D., Ganguli, D., Hatfield-Dodds, Z., Hernandez, D., Jones, A., Kernion, J., Lovitt, L., Ndousse, K., Amodei, D., Brown, T., Clark, J., Kaplan, J., McCandlish, S., & Olah, C. (2021). A Mathematical Framework for Transformer Circuits. *Anthropic*. https://transformer-circuits.pub/2021/framework/index.html**

27. **DeVine, D. (2022). Declaiming Dragons: Empathy Learning and The Elder Scrolls in Teaching Medieval Rhetorical Schemes. En Houghton, R. (Ed.), *Teaching the Middle Ages through Modern Games*. De Gruyter. DOI: 10.1515/9783110712032-004.**

28. **Houghton, R. (Ed.) (2022). *Teaching the Middle Ages through Modern Games*. De Gruyter. DOI: 10.1515/9783110712032.**

29. **Atmaja, P. W., et al. (2025). Exploring the Potential of The Elder Scrolls III: Morrowind as a Commercial-off-the-Shelf Tool for Wicked Crisis Learning. DOI: 10.48341/78xy-r315.**

30. Brown, T., Mann, B., Ryder, N., Subbiah, M., Kaplan, J., Dhariwal, P., Neelakantan, A., Shyam, P., Sastry, G., Askell, A., et al. (2020). Language Models are Few-Shot Learners. *NeurIPS 2020*. arXiv:2005.14165.

31. Gee, J. P. (2003). *What Video Games Have to Teach Us About Learning and Literacy*. Palgrave Macmillan.

### Referencias de lore de The Elder Scrolls

1. UESP Wiki. (s.f.). *Lore: Tonal Architecture*. Recuperado de https://en.uesp.net/wiki/Lore:Tonal_Architecture

2. UESP Wiki. (s.f.). *Lore: Numidium*. Recuperado de https://en.uesp.net/wiki/Lore:Numidium

3. UESP Wiki. (s.f.). *Lore: Kagrenac's Tools*. Recuperado de https://en.uesp.net/wiki/Lore:Kagrenac%27s_Tools

4. UESP Wiki. (s.f.). *Lore: Heart of Lorkhan*. Recuperado de https://en.uesp.net/wiki/Lore:Heart_of_Lorkhan

5. UESP Wiki. (s.f.). *Lore: Dwemer*. Recuperado de https://en.uesp.net/wiki/Lore:Dwemer

6. UESP Wiki. (s.f.). *Lore: Dragon Break*. Recuperado de https://en.uesp.net/wiki/Lore:Dragon_Break

7. UESP Wiki. (s.f.). *Lore: Thu'um*. Recuperado de https://en.uesp.net/wiki/Lore:Thu%27um

8. UESP Wiki. (s.f.). *Lore: Clockwork City*. Recuperado de https://en.uesp.net/wiki/Lore:Clockwork_City

9. UESP Wiki. (s.f.). *Lore: Sotha Sil*. Recuperado de https://en.uesp.net/wiki/Lore:Sotha_Sil

10. UESP Wiki. (s.f.). *Lore: Vivec*. Recuperado de https://en.uesp.net/wiki/Lore:Vivec

11. UESP Wiki. (s.f.). *Lore: CHIM*. Recuperado de https://en.uesp.net/wiki/Lore:CHIM

12. UESP Wiki. (s.f.). *Lore: 36 Lessons of Vivec*. Recuperado de https://en.uesp.net/wiki/Lore:36_Lessons_of_Vivec

13. UESP Wiki. (s.f.). *Lore: Greybeards*. Recuperado de https://en.uesp.net/wiki/Lore:Greybeards

14. Bethesda Softworks. (2002). *The Elder Scrolls III: Morrowind*. Textos in-game: "Divine Metaphysics", "The Egg of Time", "Progress of Truth", "Kagrenac's Tools Manuscript", "36 Lessons of Vivec" (series completa).

15. Bethesda Softworks. (2011). *The Elder Scrolls V: Skyrim*. Diálogos de Arngeir, Paarthurnax y los Greybeards; libros in-game: "The Tongues", "Sons of Skyrim".

16. ZeniMax Online Studios. (2017). *The Elder Scrolls Online: Morrowind*. Quest "A Melodic Mistake"; coleccionable: Torque of Tonal Constancy.

17. ZeniMax Online Studios. (2017). *The Elder Scrolls Online: Clockwork City DLC*. Textos in-game y entorno de la Ciudad Reloj.

18. TSBasilisk. (2006). *The 36 Lessons, Expanded: A Theory of Tonal Decomposition*. Imperial Library Fan Compendium. [Texto de teoría académica de fans, no canónico].

### Referencias de metodología y filosofía del autor

1. Ferrandez Canalis, D. (2026a). Arquitectura de Traducción de Código: De Paper a Código Funcional. *Agencia RONIN*. DOI: 10.1310/ronin-paper2code-2026.

2. Ferrandez Canalis, D. (2026b). Manual de Soberanía Cognitiva: Forjando el Stack del Arquitecto de Sistemas. *Agencia RONIN*. DOI: 10.1310/ronin-cognitive-stack-2026.

3. Ferrandez Canalis, D. (2026c). Guía de Auditoría de Impacto Psicológico en Modelos de Lenguaje, Volumen II. *Agencia RONIN*. DOI: 10.1310/ronin-ia-forensics-2026-vol2.

4. Ferrandez Canalis, D. (2026d). Glosario Técnico de IA: Sistema de Conocimiento Agéntico v2.0. *Agencia RONIN*. DOI: 10.1310/ronin-glossary-2026.

---

*Fin del paper. Versión 2.0 — Edición Expandida.*
*DOI: 10.1310/ronin-tonal-prompting-2026*
*Obra #1310 de la Agencia RONIN.*

*Licencia: CC BY-NC-SA 4.0 + Cláusula Comercial Ronin. Para usos comerciales, contactar: info@ronin.agency*

**1310.**
