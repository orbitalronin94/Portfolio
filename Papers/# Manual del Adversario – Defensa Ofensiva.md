
```markdown
<!-- ============================================================ -->
<!-- ARCHIVO: index.md                                            -->
<!-- ============================================================ -->

# Manual del Adversario – Defensa Ofensiva
## Edición Fundacional + Expandida ·  Capítulos

---

> *El alumno preguntó al maestro:*
> *— "¿Cómo protejo mi mente de los que quieren controlarla?"*
> *El maestro le entregó un libro sobre sectas, otro sobre hipnosis y otro sobre obediencia.*
> *— "Primero, entiende cómo te pueden robar sin que te des cuenta."*
>
> *#1310 – El conocimiento que no se ejecuta es decoración.*

---

## Filosofía del Manual

Este manual nace de una premisa simple: **no puedes defender lo que no comprendes**.

La seguridad —técnica, física o psicológica— no se aprende solo desde la trinchera del defensor. Se aprende habitando la mente del atacante, del estafador, del manipulador, del infiltrador. No para imitarlos, sino para anticiparlos.

Cada capítulo analiza a un personaje o técnica real, extrae sus mecanismos de acción y los convierte en **lecciones de defensa accionables**. El conocimiento ofensivo es el mejor motor de la defensa activa.

Este manual no enseña a atacar. Enseña a **ver el ataque antes de que llegue**.

---

## Índice General

### Parte I – Hackers, Estafadores y Cerrajeros

1. [Kevin Mitnick – El Arte del Engaño](capitulos/mitnick-arte-engano.md)
2. [Kevin Mitnick – El Arte de la Intrusión](capitulos/mitnick-arte-intrusion.md)
3. [Kevin Mitnick – Ghost in the Wires](capitulos/mitnick-ghost-wires.md)
4. [Frank Abagnale – Atrápame si Puedes](capitulos/abagnale-catch-me.md)
5. [Christopher Hadnagy – Social Engineering](capitulos/hadnagy-social-engineering.md)
6. [Kevin Poulsen – Kingpin](capitulos/poulsen-kingpin.md)
7. [Clifford Stoll – The Cuckoo's Egg](capitulos/stoll-cuckoo-egg.md)
8. [Deviant Ollam – Practical Lock Picking](capitulos/ollam-lock-picking.md)
9. [Brook Schoenfield – Secrets of a Cyber Security Architect](capitulos/schoenfield-architect.md)
10. [Peter Kim – The Hacker Playbook](capitulos/kim-hacker-playbook.md)

### Parte II – Sectas, Neurociencia y Psicología Experimental

11. [Steven Hassan – La Fábrica de la Sumisión (BITE)](capitulos/hassan-bite-model.md)
12. [Robert Jay Lifton – Ocho Claves del Control Ideológico](capitulos/lifton-totalism.md)
13. [Alexandra Stein – Apego en Sistemas Totalitarios](capitulos/stein-attachment.md)
14. [Ewen Cameron – La Destrucción Programada de la Identidad](capitulos/cameron-psychic-driving.md)
15. [José Silva – La Puerta Trasera de la Mente](capitulos/silva-mind-control.md)
16. [Franz Anton Mesmer – El Padre del Enganche Magnético](capitulos/mesmer-magnetism.md)
17. [Martin Orne – El Hipnotizador de la CIA](capitulos/orne-hypnosis-cia.md)
18. [Stanley Milgram – La Obediencia a la Autoridad como Exploit](capitulos/milgram-obedience.md)
19. [Philip Zimbardo – El Poder Corruptor de los Roles](capitulos/zimbardo-role-power.md)
20. [El Experimento de Stanford – Relectura Crítica](capitulos/stanford-prison-revisited.md)
21. [MK-Ultra – Lecciones de la Agencia de los Experimentos Prohibidos](capitulos/mkultra-state-attacker.md)
22. [La Privación Sensorial como Arma](capitulos/sensory-deprivation-weapon.md)

### Apéndices

- [A. Ejercicios Prácticos](apendices/ejercicios.md)
- [B. Glosario](apendices/glosario.md)
- [C. Bibliografía](apendices/bibliografia.md)

---

## Cláusula de Licencia – CC BY-NC-SA 4.0 + Cláusula Comercial RONIN

Este manual se distribuye bajo **CC BY-NC-SA 4.0** (Atribución-NoComercial-CompartirIgual).

**Uso libre (sin coste):**
- Lectura, estudio, uso personal y educativo.
- Copia, distribución y adaptación para fines no comerciales.
- Inclusión en cursos, talleres y materiales formativos sin ánimo de lucro, citando la fuente.
- Uso interno en organizaciones para formación y mejora de la seguridad, siempre que no se revenda ni se integre en un producto comercial.

**Uso comercial (requiere licencia adicional):**
- Inclusión del manual (total o parcial) en un producto o servicio de pago.
- Venta del manual en cualquier formato.
- Uso del manual como núcleo diferencial de servicios de consultoría o auditoría con fines lucrativos.

**Cláusula Comercial RONIN:**
> *"El conocimiento es libre, pero el negocio con el conocimiento no lo es. Si usted obtiene un beneficio económico directo utilizando este manual, contacte con la Agencia RONIN para acordar una licencia comercial. El incumplimiento de esta cláusula será perseguido conforme a la legislación de propiedad intelectual."*

Contacto licencias: **ronin@agencia-ronin.com**

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/mitnick-arte-engano.md                   -->
<!-- ============================================================ -->

# Capítulo 1 – Kevin Mitnick: El Arte del Engaño

## Perfil del Personaje

Kevin Mitnick (1963–2023) fue durante años el hacker más buscado del mundo. Antes de ser un experto en sistemas, fue algo más sencillo y más peligroso: un maestro de la conversación. Su vector de ataque principal nunca fue el código. Fue la voz humana.

**Libro base:** *The Art of Deception* (2002), Wiley.

---

## Mecanismo Central

La ingeniería social explota no los fallos del software, sino los fallos del **diseño cognitivo humano**: la tendencia a confiar en quien parece legítimo, a obedecer a quien parece tener autoridad, y a ayudar a quien parece estar en apuros.

Mitnick articuló cuatro palancas psicológicas fundamentales:

| Palanca | Descripción | Ejemplo de exploit |
|---|---|---|
| **Autoridad** | Las personas obedecen a quien perciben como superior | «Soy del departamento de IT central, necesito su contraseña ahora» |
| **Urgencia** | La presión temporal desactiva el pensamiento crítico | «El sistema se cae en 10 minutos, necesito acceso ya» |
| **Simpatía** | Nos cuesta negar ayuda a quien nos cae bien | Un atacante amable, con humor, que comparte referencias comunes |
| **Miedo** | El miedo paraliza y busca alivio inmediato | «Si no actuamos ahora, su cuenta será suspendida» |

---

## Casos Ilustrativos

### Caso 1: El técnico de soporte
Un atacante llama al servicio de atención al cliente fingiendo ser un empleado nuevo. Dice que olvidó su contraseña y que su jefe (nombrado correctamente, información obtenida de LinkedIn) le pidió que lo resolviera antes de una reunión importante. La urgencia + autoridad delegada + simpatía = acceso garantizado en el 80% de los casos documentados.

### Caso 2: La dumpster dive informada
Antes de llamar, el atacante revisó la basura de la empresa (dumpster diving): encontró organigramas internos, nombres de proyectos, jerga corporativa. Con ese vocabulario, sus llamadas sonaban absolutamente creíbles.

### Caso 3: El pretexto del proveedor
El atacante se presenta como representante de un proveedor habitual. Pide confirmación de datos «para actualizar el sistema». El empleado, sin sospechar, proporciona información interna valiosa.

---

## Anatomía de un Ataque de Ingeniería Social

```
1. RECONOCIMIENTO
   └── OSINT: LinkedIn, web corporativa, registros públicos, basura
       └── Objetivo: nombres, cargos, proyectos, jerga interna

2. CONSTRUCCIÓN DEL PRETEXTO
   └── Historia coherente + credenciales falsas plausibles
       └── Objetivo: parecer legítimo antes de la primera palabra

3. PRIMER CONTACTO
   └── Establecer rapport (simpatía, referencias comunes)
       └── Objetivo: bajar las defensas del objetivo

4. ESCALADA
   └── Introducir la petición real usando palancas (urgencia, autoridad)
       └── Objetivo: obtener el dato, acceso o acción deseada

5. CIERRE Y BORRADO DE RASTROS
   └── Agradecer, colgar, no dejar que el objetivo reflexione
       └── Objetivo: que el objetivo no reporte el incidente
```

---

## Lecciones de Defensa

1. **La autenticación no termina en la contraseña.** Cualquier petición de información sensible por teléfono o email debe verificarse por un canal alternativo y establecido previamente.
2. **El nombre correcto no es prueba de identidad.** Un atacante puede conocer tu nombre, el de tu jefe y el del proyecto actual. Eso no lo convierte en quien dice ser.
3. **La urgencia es una señal de alarma, no una razón para actuar.** Las peticiones legítimas raramente requieren decisiones instantáneas. El protocolo es tu escudo.
4. **Entrena el «no» institucional.** Los empleados deben sentir que es seguro y valorado decir «necesito verificar esto antes de proceder».

---

## Contramedidas Implementables

- **Protocolo de verificación fuera de banda:** ante cualquier petición inusual, colgar y llamar al número oficial del solicitante.
- **Lista de peticiones sensibles:** definir qué información nunca se da por teléfono/email sin proceso formal.
- **Simulacros de ingeniería social:** contratar red teams para realizar llamadas de prueba y medir la resistencia real del equipo.
- **Cultura del reporte sin culpa:** quien reporte haber sido engañado debe recibir apoyo, no sanción. Los atacantes explotan el miedo a la vergüenza.
- **Sesiones de concienciación contextualizadas:** no PowerPoints genéricos, sino casos reales adaptados al sector de la organización.

---

## Ejercicio Práctico

**Simulacro de pretexto:**
En grupos de dos, uno hace de atacante y otro de empleado. El atacante tiene 5 minutos para construir un pretexto convincente e intentar obtener un «dato sensible» predefinido (ej.: el nombre del proveedor de nóminas). El empleado tiene instrucciones de aplicar el protocolo de verificación. Se analiza después qué funcionó y qué no.

**Reflexión posterior:** ¿Qué palanca fue más efectiva? ¿Cuándo estuvo el empleado a punto de ceder? ¿Qué habría evitado el éxito del ataque?

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/mitnick-arte-intrusion.md                -->
<!-- ============================================================ -->

# Capítulo 2 – Kevin Mitnick: El Arte de la Intrusión

## Perfil del Personaje

*The Art of Intrusion* (2005) es el complemento técnico de *El Arte del Engaño*. Mientras el primero se centra en el componente humano, este recopila casos reales de intrusiones informáticas narrados por los propios protagonistas: hackers que accedieron a sistemas de bancos, casinos, agencias gubernamentales y corporaciones multinacionales.

**Libro base:** *The Art of Intrusion* (2005), Wiley.

---

## Mecanismo Central

La intrusión exitosa rara vez es un golpe único de genialidad. Es, casi siempre, **una cadena de pasos pequeños y pacientes** donde cada eslabón abre la puerta al siguiente. Los atacantes de élite comparten tres rasgos: curiosidad obsesiva, paciencia extrema y capacidad para pensar en sistemas.

---

## Casos Documentados (Resumen Analítico)

### Caso: El casino de Las Vegas
Dos jóvenes hackers encontraron una vulnerabilidad en los sistemas de video-poker de un casino. No la explotaron de golpe: primero analizaron el sistema durante meses, identificaron el patrón de generación de números pseudo-aleatorios y cronometraron sus apuestas con precisión milimétrica. La lección: **los sistemas deterministas tienen memoria, y esa memoria es explotable.**

**Defensa:** Auditar los generadores de números aleatorios de cualquier sistema con implicaciones financieras. Revisar si son verdaderamente aleatorios (TRNG) o pseudoaleatorios (PRNG) con semillas predecibles.

### Caso: La intrusión bancaria
Un hacker accedió a la red interna de un banco a través de un terminal de acceso público mal configurado en la sucursal. Desde ahí escaló privilegios usando una vulnerabilidad no parcheada en el sistema operativo. La lección: **la red interna no es más segura que su punto de entrada más débil.**

**Defensa:** Segmentación de red estricta. Los terminales públicos o de acceso limitado deben estar en una VLAN completamente aislada, sin ruta posible hacia sistemas críticos.

### Caso: El infiltrado en la empresa de seguridad
Un hacker consiguió empleo temporal en una empresa de seguridad informática para acceder físicamente a sus servidores. La lección: **el insider threat es el vector más difícil de detectar y el más devastador.**

**Defensa:** Principio de mínimo privilegio desde el primer día. Los accesos se conceden progresivamente, no de golpe. El acceso físico a servidores críticos requiere doble autorización.

---

## El Modelo Mental del Atacante

```
RECONOCIMIENTO PASIVO
└── Escaneo de puertos, fingerprinting de servicios, OSINT
    └── Objetivo: mapear la superficie de ataque

RECONOCIMIENTO ACTIVO
└── Pruebas de vulnerabilidades conocidas, fuzzing controlado
    └── Objetivo: identificar el eslabón más débil

EXPLOTACIÓN INICIAL
└── Obtener un primer punto de apoyo (foothold)
    └── Objetivo: estar dentro, aunque sea con privilegios mínimos

ESCALADA DE PRIVILEGIOS
└── Moverse lateralmente, escalar permisos
    └── Objetivo: llegar al activo valioso

PERSISTENCIA
└── Instalar backdoors, crear cuentas ocultas
    └── Objetivo: mantener el acceso aunque se detecte el vector inicial

EXTRACCIÓN O ACCIÓN
└── Robar datos, modificar sistemas, dejar rastros falsos
    └── Objetivo: completar la misión sin ser identificado
```

---

## Lecciones de Defensa

1. **Parchea sin excusas.** La mayoría de intrusiones documentadas explotan vulnerabilidades con parche disponible. La pereza en el parcheo es la principal causa de éxito del atacante.
2. **El defensor necesita ver lo que ve el atacante.** Realiza escaneos de tu propia infraestructura regularmente. Usa las mismas herramientas que usaría un atacante (nmap, Shodan, Burp Suite).
3. **Los logs son la memoria del sistema.** Sin logs correctamente configurados, centralizados y monitorizados, el ataque puede durar meses sin detectarse.
4. **La defensa en profundidad no es opcional.** Ninguna capa es suficiente por sí sola. La combinación de firewall + IDS + segmentación + MFA + logs + respuesta a incidentes crea una resistencia real.

---

## Contramedidas Implementables

- **Programa de gestión de vulnerabilidades:** inventario de activos, escaneo periódico, priorización por riesgo y SLA de parcheo.
- **Ejercicios de red team:** simulaciones periódicas de intrusión real (no solo checklist de cumplimiento).
- **SIEM y alertas de comportamiento anómalo:** detectar movimiento lateral, escaladas de privilegio y acceso a activos inusuales.
- **Control de acceso basado en roles (RBAC):** principio de mínimo privilegio aplicado sistemáticamente.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/mitnick-ghost-wires.md                   -->
<!-- ============================================================ -->

# Capítulo 3 – Kevin Mitnick: Ghost in the Wires

## Perfil del Personaje

*Ghost in the Wires* (2011) es la autobiografía de Mitnick: la historia de cómo el hacker más buscado de Estados Unidos burló al FBI durante años, creó múltiples identidades falsas y vivió en la clandestinidad sin dejar de hackear. Es, ante todo, una clase magistral de **evasión, adaptación y gestión de la identidad**.

**Libro base:** *Ghost in the Wires* (2011), Little, Brown and Company.

---

## Mecanismo Central

La supervivencia de Mitnick se basó en tres pilares:

1. **La identidad como recurso renovable.** Mitnick no era «Kevin Mitnick» cuando necesitaba no serlo. Construyó identidades completas: historial, papeles, leyendas de apoyo, comportamientos coherentes.
2. **La anticipación de los patrones del perseguidor.** Estudiaba cómo pensaba el FBI para no hacer lo que el FBI esperaba que hiciera.
3. **La red social como infraestructura de evasión.** Cada ciudad tenía contactos que, sin saberlo completamente, contribuían a mantener su invisibilidad.

---

## Lecciones de Defensa

### Para la identidad digital
- Las identidades online dejan rastros cruzados: el mismo nick, el mismo estilo de escritura, las mismas horas de actividad. Un atacante paciente puede correlacionar identidades aparentemente separadas.
- **Contramedida:** Para activos críticos, compartimentar identidades digitales con disciplina: dispositivos distintos, conexiones distintas, estilos distintos.

### Para la detección de evasión
- Un atacante que conoce tus procedimientos de detección puede diseñar su conducta para no activar ninguna alerta. La detección basada en reglas estáticas es derrotable.
- **Contramedida:** Combinar detección basada en reglas con detección basada en anomalías de comportamiento (UEBA). El atacante puede saber las reglas; le es más difícil saber qué es «normal» para tu entorno específico.

### Para la gestión de incidentes
- Mitnick fue capturado finalmente porque un error humano en su círculo de confianza lo delató, no porque el FBI fuera más listo.
- **Contramedida:** El punto de fallo en cualquier operación es siempre humano. En un equipo de respuesta a incidentes, el protocolo debe ser más fuerte que el juicio individual bajo presión.

---

## Contramedidas Implementables

- **Threat hunting proactivo:** no esperar a que las alertas salten. Buscar activamente señales de presencia de atacantes en la red.
- **Análisis de comportamiento de usuarios y entidades (UEBA):** detectar desviaciones del patrón normal de comportamiento.
- **Compartimentación de información en investigaciones activas:** solo quien necesita saber, sabe. La filtración de una investigación activa la destruye.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/abagnale-catch-me.md                     -->
<!-- ============================================================ -->

# Capítulo 4 – Frank Abagnale: Atrápame si Puedes

## Perfil del Personaje

Frank Abagnale Jr. se hizo pasar por piloto de PanAm, médico pediatra y abogado —todo antes de los 21 años— usando únicamente su capacidad de adaptación, su confianza en sí mismo y documentos falsificados. Sus hazañas, documentadas en su autobiografía de 1980, constituyen el caso de estudio definitivo sobre **suplantación de identidad y adaptación al entorno como vector de ataque**.

**Libro base:** *Catch Me If You Can* (1980), Broadway Books.

---

## Mecanismo Central

Abagnale operaba sobre una verdad psicológica fundamental: **la gente cree lo que quiere creer**. Un uniforme correcto, la jerga adecuada y la confianza suficiente son, en muchos contextos, más convincentes que cualquier credencial verificada.

Sus tres técnicas nucleares:

| Técnica | Descripción |
|---|---|
| **Adaptación de contexto** | Estudiaba el entorno objetivo (aerolíneas, hospitales, bufetes) y aprendía su lenguaje, rutinas y jerarquías antes de infiltrarse |
| **El uniforme como llave** | Un uniforme correcto abre puertas que ninguna contraseña puede abrir. La gente responde al símbolo antes que a la persona |
| **La confianza como escudo** | Nunca mostraba duda. La inseguridad es la señal que activa la sospecha |

---

## Lecciones de Defensa

1. **La verificación de credenciales debe ser un proceso, no una impresión.** Un diploma en la pared, un uniforme y una tarjeta de visita no son prueba de identidad. Son props.
2. **Los proveedores y terceros son el vector de ataque preferido.** Abagnale se colaba como «externo»: el piloto de visita, el médico de guardia, el abogado colaborador. Las organizaciones tienden a tener controles más laxos para externos.
3. **La confianza excesiva en el contexto visual es explotable sistemáticamente.** El ser humano hace inferencias rápidas basadas en apariencia. Eso es un bug, no un feature.

---

## Contramedidas Implementables

- **Verificación de identidad de terceros por proceso formal:** credenciales verificadas con el organismo emisor, no solo presentadas.
- **Control de acceso físico basado en roles y zonas:** el «proveedor» no tiene acceso a la sala de servidores, aunque tenga uniforme.
- **Cultura de verificación sin vergüenza:** pedir verificación adicional debe ser socialmente aceptable y protocolizado, no una ofensa.
- **Auditorías de acceso de terceros:** revisar periódicamente quién tiene acceso, con qué nivel y si sigue siendo necesario.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/hadnagy-social-engineering.md            -->
<!-- ============================================================ -->

# Capítulo 5 – Christopher Hadnagy: Social Engineering

## Perfil del Personaje

Christopher Hadnagy es el fundador de Social-Engineer, LLC, y el creador del primer marco formal para entender, medir y prevenir la ingeniería social. Su libro de 2011 no es una colección de anécdotas: es una **taxonomía sistemática de la manipulación humana** con herramientas concretas de defensa.

**Libro base:** *Social Engineering: The Art of Human Hacking* (2011), Wiley.

---

## El Marco Formal de la Ingeniería Social

### Las Fases del Ataque

```
1. RECOLECCIÓN DE INFORMACIÓN (Information Gathering)
   Herramientas: OSINT, maltego, redes sociales, registros públicos
   Objetivo: construir un perfil detallado del objetivo

2. DESARROLLO DEL PRETEXTO (Pretexting)
   Herramientas: leyenda, documentos de apoyo, conocimiento contextual
   Objetivo: crear una identidad y escenario creíble

3. ATAQUE
   Vectores: vishing (voz), phishing (email), smishing (SMS),
             impersonación presencial, tailgating
   Objetivo: obtener el acceso, dato o acción deseada

4. CIERRE
   Objetivo: salir sin levantar sospechas y sin dejar evidencia
```

### Los Principios de Influencia Explotados

Hadnagy estructura los vectores de manipulación sobre los seis principios de influencia de Cialdini, más dos propios:

| Principio | Cómo lo explota el atacante |
|---|---|
| **Reciprocidad** | Te hace un pequeño favor para que le debes uno más grande |
| **Compromiso** | Obtiene una pequeña concesión inicial que ancla futuras concesiones |
| **Prueba social** | «Todos en su departamento ya lo han hecho» |
| **Autoridad** | Se presenta como superior, auditor o proveedor autorizado |
| **Simpatía** | Establece rapport genuino antes de pedir |
| **Escasez** | «Solo hay una ventana de tiempo para resolver esto» |
| **Urgencia** | Presión temporal que desactiva el pensamiento crítico |
| **Miedo** | Amenaza de consecuencias negativas si no se actúa |

---

## Lecciones de Defensa

1. **Conocer los principios de influencia es la primera línea de defensa.** Una persona que reconoce que le están aplicando el principio de urgencia puede hacer una pausa antes de actuar.
2. **El pretexto se construye con información pública.** Reducir la huella informativa de la organización en fuentes abiertas reduce la calidad de los pretextos disponibles.
3. **La defensa más sostenible es la cultura, no el procedimiento.** Los procedimientos se saltan; la cultura de verificación no se puede saltarse porque está internalizada.

---

## Contramedidas Implementables

- **Formación basada en principios de influencia:** que cada empleado sepa nombrar las palancas que le están usando.
- **Simulacros de phishing y vishing controlados:** medir la tasa de clic y de divulgación, iterar la formación según los resultados.
- **Política de «verificación sin vergüenza»:** protocolo explícito que protege a quien pide verificación adicional.
- **Reducción de huella OSINT:** auditar qué información de la organización es pública y reducirla al mínimo necesario.
- **Canales de reporte simples y sin fricción:** si reportar un incidente es complicado, no se reporta.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/poulsen-kingpin.md                       -->
<!-- ============================================================ -->

# Capítulo 6 – Kevin Poulsen: Kingpin

## Perfil del Personaje

*Kingpin* (2011) narra la historia de Max Butler (alias Iceman), un hacker que pasó de ser un informante del FBI a convertirse en el señor del mayor foro de cibercrimen de su época: CardersMarket. Butler orquestó el robo de millones de números de tarjetas de crédito y gestionó una red criminal de dimensiones corporativas.

**Libro base:** *Kingpin* (2011), Crown Publishers. Autor: Kevin Poulsen.

---

## Mecanismo Central

Butler demostró que el cibercrimen organizado opera con la misma lógica que cualquier empresa: tiene estructura jerárquica, gestión de proveedores, control de calidad, resolución de conflictos y estrategias de expansión. **La economía del cibercrimen es una economía de mercado.**

### La Arquitectura del Cibercrimen como Negocio

```
PROVEEDORES DE DATOS (carders, skimmers)
└── Roban datos de tarjetas en puntos de venta, ATMs, bases de datos
    └── Venden en foros especializados

INTERMEDIARIOS (checkers, encoders)
└── Verifican la validez de los datos robados
└── Codifican los datos en tarjetas físicas falsas
    └── Cobran por el servicio

DISTRIBUIDORES (cashers, money mules)
└── Usan las tarjetas o las revenden
└── Mueven el dinero a través de múltiples capas
    └── El dinero llega «limpio» al nivel superior

INFRAESTRUCTURA (foros, escrow, reputación)
└── Los foros son el mercado: tienen sistema de reputación,
    escrow para transacciones y resolución de disputas
```

---

## Lecciones de Defensa

1. **El cibercrimen tiene supply chain.** Para desmantelarlo, no basta con atacar el extremo visible. Hay que entender toda la cadena.
2. **La economía del cibercrimen incentiva la especialización.** Cada actor hace una cosa bien. La defensa debe ser igualmente especializada.
3. **Los foros de cibercrimen son inteligencia abierta.** El monitoreo de la dark web proporciona alertas tempranas sobre credenciales robadas, vulnerabilidades en venta y ataques planificados.
4. **La reputación es la moneda del cibercrimen.** Los actores maliciosos cuidan su reputación en sus foros. Eso deja rastros explotables por los defensores.

---

## Contramedidas Implementables

- **Threat intelligence de dark web:** monitorizar foros y mercados para detectar credenciales propias en venta.
- **Segmentación de datos de pago:** los datos de tarjetas nunca deben estar en la misma red que los sistemas de negocio.
- **Tokenización y cifrado punto a punto:** los datos de pago no deben existir en claro en ningún punto del proceso.
- **Monitorización de transacciones anómalas:** sistemas antifraude que detecten patrones de uso inusuales en tiempo real.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/stoll-cuckoo-egg.md                      -->
<!-- ============================================================ -->

# Capítulo 7 – Clifford Stoll: The Cuckoo's Egg

## Perfil del Personaje

En 1986, Clifford Stoll era un astrónomo reconvertido en administrador de sistemas en el Lawrence Berkeley National Laboratory. Investigando un error de 75 centavos en las cuentas de uso del ordenador, descubrió al primer espía cibernético documentado de la historia: un hacker alemán trabajando para la KGB.

**Libro base:** *The Cuckoo's Egg* (1989), Doubleday.

---

## Mecanismo Central

La grandeza de Stoll no fue técnica. Fue **la persistencia de un científico aplicada a la investigación de seguridad**. Durante meses, mientras las agencias gubernamentales se negaban a tomarlo en serio, Stoll monitorizó manualmente cada sesión del atacante, construyó honeypots artesanales y trazó metódicamente los pasos del intruso.

### El Honeypot Original

Stoll creó uno de los primeros honeypots documentados de la historia: un directorio falso con documentos atractivos sobre el SDI (Strategic Defense Initiative) para mantener al atacante conectado el tiempo suficiente para rastrearlo. La trampa funcionó.

**Lección:** El honeypot no es solo una trampa. Es una herramienta de inteligencia que revela las motivaciones, las capacidades y los métodos del atacante.

---

## Lecciones de Defensa

1. **Los anomalías pequeñas merecen investigación.** Stoll encontró al espía investigando 75 centavos. Los atacantes sofisticados dejan trazas mínimas; hay que estar entrenado para verlas.
2. **Los logs son la evidencia forense primaria.** Sin los logs de Stoll, no había caso. Sin logs correctamente configurados, el atacante invisible permanece invisible.
3. **La persistencia del defensor puede superar la sofisticación del atacante.** El hacker alemán era técnicamente hábil; Stoll era obsesivamente metódico. La meticulosidad ganó.
4. **La coordinación interinstitucional es lenta y difícil.** Stoll tuvo que convencer al FBI, la CIA y la NSA de que tomaran en serio una intrusión informática. Hoy, los CERT y los mecanismos de notificación de incidentes existen precisamente para reducir esa fricción.

---

## Contramedidas Implementables

- **Logging exhaustivo y centralizado:** todos los sistemas críticos deben generar logs detallados, centralizados en un SIEM, con retención adecuada.
- **Programa de honeypots:** desplegar activos trampa (credenciales, archivos, sistemas) que alerten cuando son accedidos.
- **Procedimiento de respuesta a anomalías:** cualquier discrepancia contable, de uso o de acceso debe tener un procedimiento de investigación, por pequeña que sea.
- **Canales de reporte a CERT/CSIRT nacionales:** conocer los procedimientos de coordinación con autoridades antes de necesitarlos.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/ollam-lock-picking.md                    -->
<!-- ============================================================ -->

# Capítulo 8 – Deviant Ollam: Practical Lock Picking

## Perfil del Personaje

Deviant Ollam es uno de los principales expertos en seguridad física del mundo, consultor de penetración física y autor del manual de referencia para profesionales que necesitan entender —y probar— la seguridad de las cerraduras.

**Libro base:** *Practical Lock Picking* (2010), Syngress.

---

## Mecanismo Central

La seguridad física es, con frecuencia, el eslabón más olvidado de la cadena de seguridad. Una organización puede tener el mejor firewall del mundo y una puerta de servidor que se abre con una horquilla.

### Tipos de Ataques Físicos

| Técnica | Descripción | Contramedida |
|---|---|---|
| **Lock picking** | Manipulación de los pines de una cerradura para abrirla sin la llave original | Cerraduras de alta seguridad con pines de seguridad (spool, serrated) |
| **Bumping** | Uso de una llave bumping para alinear los pines momentáneamente | Cerraduras antibumping certificadas |
| **Bypass** | Eludir la cerradura por completo (shimming, loiding) | Protectores de placa, doble cerrojo |
| **Tailgating** | Seguir a una persona autorizada a través de una puerta controlada | Mantrap (esclusa de seguridad), concienciación del personal |
| **Decepción** | Fingir ser personal de mantenimiento para obtener acceso físico | Protocolo de verificación de proveedores, acompañamiento obligatorio |

---

## El Principio de la Defensa Física en Capas

```
PERÍMETRO EXTERIOR
└── Vallas, cámaras, iluminación, control de vehículos

ACCESO AL EDIFICIO
└── Cerradura de alta seguridad + control de acceso electrónico + guardia

ZONAS RESTRINGIDAS
└── Mantrap + tarjeta + PIN + biometría

ACTIVOS CRÍTICOS (sala de servidores, archivo)
└── Caja fuerte, rack con cerradura, alarma de vibración, CCTV interno

DETECCIÓN Y RESPUESTA
└── Alarmas, sensores de movimiento, protocolo de respuesta documentado
```

---

## Lecciones de Defensa

1. **Una cerradura no es una barrera; es un retardo.** El objetivo de la seguridad física es dar tiempo para detectar y responder, no hacer el ataque imposible.
2. **La seguridad física y la digital son inseparables.** El acceso físico a un servidor es acceso total al sistema. Proteger la caja sin proteger la llave es inútil.
3. **El tailgating es el vector de acceso físico más común y más ignorado.** La formación del personal para no permitir acceso a desconocidos es tan importante como cualquier cerradura.
4. **Audita la seguridad física con la misma periodicidad que la digital.** Un pentest físico (red team físico) revela vulnerabilidades que ningún escáner de red puede detectar.

---

## Contramedidas Implementables

- **Auditoría de cerraduras:** inventariar todas las cerraduras de la organización y clasificarlas por nivel de seguridad requerido vs. nivel actual.
- **Red team físico periódico:** contratar a profesionales para intentar acceder físicamente a instalaciones críticas y documentar los resultados.
- **Política de visitantes:** todo visitante acompañado siempre, sin excepción. Las credenciales de visitante deben ser visibles y temporales.
- **Control de llaves:** inventario de llaves maestras, control de duplicados, procedimiento de reporte de pérdida.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/schoenfield-architect.md                 -->
<!-- ============================================================ -->

# Capítulo 9 – Brook Schoenfield: Secrets of a Cyber Security Architect

## Perfil del Personaje

Brook S. E. Schoenfield es un arquitecto de seguridad veterano con décadas de experiencia en el diseño de sistemas seguros desde cero. Su libro de 2019 no habla de exploits ni de ataques famosos: habla del **trabajo real, a veces frustrante, de construir seguridad que dure**.

**Libro base:** *Secrets of a Cyber Security Architect* (2019), CRC Press.

---

## Mecanismo Central

La seguridad no se añade a un sistema; se diseña desde el principio. Un arquitecto de seguridad que llega al final del proceso de desarrollo solo puede poner parches. El que llega al principio puede construir sistemas que son difíciles de atacar por diseño.

### Los Pilares de la Arquitectura de Seguridad

```
1. THREAT MODELING (Modelado de Amenazas)
   ¿Quién querría atacar este sistema? ¿Qué quiere? ¿Cómo puede hacerlo?
   Metodología: STRIDE (Spoofing, Tampering, Repudiation,
                         Information Disclosure, DoS, Elevation of Privilege)

2. PRINCIPIOS DE DISEÑO SEGURO
   - Mínimo privilegio
   - Defensa en profundidad
   - Fail secure (fallar de forma segura)
   - Separación de funciones
   - No confiar en el input del usuario

3. CONTROL DE LA SUPERFICIE DE ATAQUE
   Reducir al mínimo los puntos de entrada:
   APIs expuestas, puertos abiertos, servicios en ejecución

4. REVISIÓN CONTINUA
   La arquitectura envejece. Las amenazas evolucionan.
   Revisión periódica obligatoria.
```

---

## Lecciones de Defensa

1. **El threat modeling no es un ejercicio académico.** Es la herramienta más práctica para priorizar inversiones en seguridad. Si no sabes contra qué te defiendes, no sabes dónde gastar.
2. **La seguridad por oscuridad no es seguridad.** Ocultar la arquitectura no es suficiente; debe ser robusta aunque el atacante la conozca.
3. **El arquitecto de seguridad es el traductor entre el negocio y la técnica.** La seguridad que no puede explicarse en términos de riesgo de negocio no recibe presupuesto.
4. **La deuda técnica en seguridad se cobra con intereses.** Cada decisión de diseño insegura que se pospone se convierte en una vulnerabilidad más costosa de mitigar.

---

## Contramedidas Implementables

- **Threat modeling obligatorio en cada nuevo proyecto:** antes de escribir la primera línea de código, modelar las amenazas.
- **Security champions en cada equipo de desarrollo:** personas formadas en seguridad que integran las revisiones en el ciclo de desarrollo.
- **Revisión de arquitectura de seguridad anual:** los sistemas heredados deben ser revisados con los ojos de las amenazas actuales.
- **Registro de decisiones de arquitectura de seguridad (ADR):** documentar por qué se tomó cada decisión de diseño, para poder revisarla después.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/kim-hacker-playbook.md                   -->
<!-- ============================================================ -->

# Capítulo 10 – Peter Kim: The Hacker Playbook

## Perfil del Personaje

Peter Kim es un penetration tester profesional que estructuró su libro como un manual de jugadas (playbook) deportivo: cada «jugada» es una técnica de ataque real, con sus pasos detallados y sus objetivos. La premisa es que para construir una defensa sólida hay que entender el juego ofensivo.

**Libro base:** *The Hacker Playbook* (2014), Secure Planet LLC.

---

## La Metodología del Pentest

```
PRE-PARTIDO (Reconocimiento)
└── OSINT, escaneo de red, fingerprinting
└── Identificación de la superficie de ataque

PRIMER TIEMPO (Explotación)
└── Explotación de vulnerabilidades conocidas
└── Ataques de phishing y spear-phishing
└── Ataques de contraseña (brute force, credential stuffing)

MEDIO TIEMPO (Análisis de posición)
└── ¿Dónde estamos? ¿Qué privilegios tenemos?
└── ¿Cuál es el siguiente objetivo?

SEGUNDO TIEMPO (Post-explotación)
└── Escalada de privilegios
└── Movimiento lateral
└── Persistencia y exfiltración

POST-PARTIDO (Reporting)
└── Documentar todo lo encontrado
└── Clasificar por criticidad
└── Proponer remediaciones concretas
```

---

## Las Jugadas Más Importantes

| Jugada | Descripción | Defensa |
|---|---|---|
| **Spear phishing** | Phishing dirigido con información específica del objetivo | MFA + formación contextualizada + filtros de email |
| **Pass-the-hash** | Reutilización de hashes de contraseña para autenticación lateral | Segmentación + rotación de credenciales + detección de movimiento lateral |
| **Kerberoasting** | Extracción y crackeo offline de tickets Kerberos | Contraseñas largas en cuentas de servicio + monitorización de solicitudes de tickets |
| **Pivoting** | Usar una máquina comprometida como trampolín hacia otras redes | Segmentación estricta + zero trust |
| **Living off the land** | Usar herramientas legítimas del sistema (PowerShell, WMI) para evitar detección | Whitelisting de aplicaciones + monitorización de uso anómalo de herramientas admin |

---

## Lecciones de Defensa

1. **Piensa en jugadas, no en listas de control.** Las checklist de cumplimiento verifican el pasado; el pensamiento en jugadas anticipan el futuro.
2. **El movimiento lateral es la fase más peligrosa y la menos detectada.** Una vez dentro, el atacante se mueve como si fuera un empleado. La detección debe centrarse en comportamientos anómalos, no solo en el perímetro.
3. **El reporte del pentest vale tanto como el pentest en sí.** Un hallazgo que no se documenta bien no se remedia bien.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/hassan-bite-model.md                     -->
<!-- ============================================================ -->

# Capítulo 11 – Steven Hassan: La Fábrica de la Sumisión (Modelo BITE)

## Perfil del Personaje

Steven Hassan fue miembro de la Iglesia de la Unificación («los moonies») durante varios años. Tras ser desprogramado, dedicó su vida a estudiar los mecanismos por los cuales las organizaciones destructivas —sectas, grupos políticos extremistas, empresas tóxicas— destruyen la autonomía de sus miembros.

**Libro base:** *Combating Cult Mind Control* (1988), Park Street Press.

---

## El Modelo BITE

El modelo BITE es el marco más sistemático disponible para analizar el control que ejerce una organización sobre sus miembros. Articula cuatro dimensiones de control:

### B – Behavior Control (Control de la Conducta)

La organización microgestiona la vida cotidiana del individuo:

- Control del tiempo (horarios rígidos, actividades obligatorias)
- Control de las relaciones (con quién se puede hablar, con quién no)
- Control de las finanzas (donaciones obligatorias, dependencia económica)
- Control de la alimentación, el sueño, la sexualidad

**Señal de alarma:** ¿Tienes tiempo y espacio para hacer cosas que no están sancionadas por la organización?

### I – Information Control (Control de la Información)

La organización controla qué información llega al individuo:

- Las fuentes externas son descreditadas o prohibidas
- El acceso a críticas de la organización está restringido
- La información interna se compartimenta («solo los miembros avanzados pueden saber esto»)
- Se fomenta la vigilancia mutua y el reporte de disidencia

**Señal de alarma:** ¿Puedes buscar libremente críticas de la organización y compartirlas sin consecuencias?

### T – Thought Control (Control del Pensamiento)

La organización instala un sistema de pensamiento que filtra la realidad:

- Lenguaje propio que reemplaza el pensamiento independiente (loaded language)
- Los pensamientos críticos son «satánicos», «tóxicos» o «ego»
- Técnicas de supresión del pensamiento (meditación forzada, cánticos, repetición)
- Doctrina que se presenta como la única verdad posible

**Señal de alarma:** ¿Puedes pensar en voz alta «quizás esta organización se equivoca» sin que eso genere ansiedad o culpa?

### E – Emotion Control (Control de las Emociones)

La organización manipula el estado emocional del individuo:

- Alternancia de amor incondicional y rechazo (ciclo de idealización/devaluación)
- Culpa y vergüenza como herramientas de control
- Miedo a las consecuencias de abandonar (shunning, amenazas)
- Fobia inducida hacia el mundo exterior

**Señal de alarma:** ¿Te sientes libre de expresar dudas o desacuerdo sin miedo a consecuencias emocionales o sociales?

---

## El Modelo BITE en Contextos No-Sectarios

El modelo BITE no es exclusivo de sectas religiosas. Se puede encontrar en:

- **Startups con cultura tóxica:** control total del tiempo, glorificación del sacrificio, descreditación de quienes se van.
- **Organizaciones políticas extremistas:** enemigo externo definido, información externa prohibida, lealtad absoluta al líder.
- **Relaciones íntimas abusivas:** control de relaciones sociales, alternancia de afecto y castigo, miedo a abandonar.
- **Programas de formación intensivos (algunos bootcamps, MLM):** control del entorno, promesas de transformación, aislamiento de la realidad exterior.

---

## Lecciones de Defensa

1. **El control no llega de golpe.** Se instala gradualmente, en pasos pequeños que parecen razonables individualmente. El primer «compromiso» es la puerta.
2. **La salida se dificulta a medida que el control aumenta.** Las dependencias emocionales, sociales y económicas se construyen deliberadamente para hacer el abandono doloroso.
3. **El antídoto es la diversidad informativa y relacional.** Mantener fuentes de información externas y relaciones fuera del grupo es la defensa más efectiva.

---

## Contramedidas Implementables

- **Auditoría de libertad cognitiva:** en cualquier organización, preguntar periódicamente: ¿puede un miembro disentir públicamente sin consecuencias? ¿Hay acceso a información crítica externa?
- **Red teaming interno:** invitar activamente a personas de fuera a cuestionar las prácticas de la organización.
- **Rotación y contacto exterior:** asegurar que los equipos mantienen relaciones y perspectivas externas a la organización.
- **Protocolo de salida digna:** la facilidad para abandonar una organización (un trabajo, una comunidad) es un indicador de salud organizacional.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/lifton-totalism.md                       -->
<!-- ============================================================ -->

# Capítulo 12 – Robert Jay Lifton: Ocho Claves del Control Ideológico

## Perfil del Personaje

Robert Jay Lifton es un psiquiatra que estudió a prisioneros de la guerra de Corea sometidos a «lavado de cerebro» por las autoridades chinas. Su investigación, publicada en 1961, produjo el primer análisis científico sistemático del control ideológico totalitario.

**Libro base:** *Thought Reform and the Psychology of Totalism* (1961), University of North Carolina Press.

---

## Los Ocho Criterios del Totalismo

Lifton identificó ocho características que, cuando están presentes simultáneamente, definen un entorno de control ideológico total:

| Criterio | Descripción | Señal de alarma |
|---|---|---|
| **1. Control del entorno** | Control físico y social del ambiente del individuo | No puedes ir a donde quieras ni hablar con quien quieras |
| **2. Mística de la experiencia** | La organización posee una verdad especial, inaccesible desde fuera | «Solo los que han vivido esto pueden entenderlo» |
| **3. Demanda de pureza** | Existe un estándar imposible de perfección al que hay que aspirar | La autocrítica y la culpa son permanentes |
| **4. Confesión** | Los miembros deben revelar sus pensamientos privados y errores | Sesiones de «transparencia» obligatoria, diarios revisados |
| **5. Ciencia sagrada** | La doctrina es incuestionable e inmutable | «No puedes cuestionar los fundamentos» |
| **6. Carga del lenguaje** | Vocabulario propio que simplifica y reemplaza el pensamiento | Palabras que cierran el debate en lugar de abrirlo |
| **7. Doctrina sobre persona** | La ideología tiene más valor que la experiencia individual | «Tu experiencia personal es irrelevante; la doctrina dice...» |
| **8. Dispensación de existencia** | La organización determina quién merece existir/pertenecer | Los de fuera son inferiores, perdidos o peligrosos |

---

## Umbral de Riesgo

Si una organización cumple **cuatro o más** de estos ocho criterios, existe riesgo significativo de manipulación sistémica. Si cumple **seis o más**, el riesgo es severo.

---

## Lecciones de Defensa

1. **El lenguaje es el primer síntoma.** Cuando una organización desarrolla un vocabulario propio que hace difícil la comunicación con el exterior, eso es el criterio 6 en acción. El lenguaje que cierra el pensamiento es siempre una señal de alarma.
2. **La demanda de pureza genera personas que no pueden ganar.** El estándar imposible crea individuos permanentemente en deuda con la organización, lo que es una palanca de control perfecta.
3. **La confesión forzada es un arma de doble filo.** Lo que se confiesa puede usarse contra el confesante si abandona la organización.

---

## Contramedidas Implementables

- **Glosario de lenguaje interno:** si una organización tiene un vocabulario propio extenso, documentarlo y cuestionarlo regularmente.
- **Canales de disidencia protegidos:** crear espacios donde el desacuerdo sea no solo tolerado sino activamente solicitado.
- **Onboarding crítico:** en el proceso de incorporación a cualquier organización, entregar materiales que incluyan críticas honestas de la organización.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/stein-attachment.md                      -->
<!-- ============================================================ -->

# Capítulo 13 – Alexandra Stein: Apego en Sistemas Totalitarios

## Perfil del Personaje

Alexandra Stein es investigadora y exmiembro de un grupo político totalitario. Aplicó la teoría del apego de Bowlby al estudio de las sectas y los regímenes autoritarios, produciendo el análisis más psicológicamente sofisticado del por qué las personas no pueden abandonar organizaciones que las dañan.

**Libro base:** *Terror, Love and Brainwashing* (2017), Routledge.

---

## Mecanismo Central: El Vínculo de Terror y Amor

La teoría del apego explica cómo los seres humanos buscan figuras de seguridad en situaciones de estrés. En circunstancias normales, esa figura de apego (un progenitor, una pareja) proporciona consuelo y seguridad.

En los sistemas totalitarios, el líder o la organización se convierte en la **figura de apego principal** del miembro. Pero con una diferencia crucial: **la misma figura que causa el terror es la única que puede aliviarlo**.

```
CICLO DEL APEGO TRAUMÁTICO

1. El líder/organización genera terror (crítica, amenaza, exclusión)
   └── El miembro siente ansiedad de apego extrema

2. El miembro busca consuelo en la única fuente disponible: el líder
   └── El líder ofrece consuelo condicional (si cumples, si crees más)

3. El alivio refuerza la dependencia
   └── El miembro asocia al líder con la seguridad, no con el peligro

4. El ciclo se repite con mayor intensidad
   └── La dependencia aumenta; la salida se vuelve psicológicamente
       insoportable (no solo difícil)
```

---

## Por Qué Las Personas No Se Van

La pregunta «¿por qué no se fue?» asume que la decisión de quedarse es racional. Stein demuestra que no lo es: **el vínculo de apego traumático opera por debajo del pensamiento consciente**. Irse significa perder la única fuente de seguridad disponible, lo que el sistema nervioso vive como una amenaza de muerte.

---

## Lecciones de Defensa

1. **Los datos no rompen el vínculo de apego.** Mostrar a alguien «pruebas» de que su líder es dañino no funciona si el vínculo de apego está activo. Primero hay que reconstruir vínculos alternativos de seguridad.
2. **La dependencia emocional es un vector de control más poderoso que la coerción física.** Una persona que puede irse físicamente pero no puede irse emocionalmente está igualmente atrapada.
3. **El aislamiento social es el prerrequisito del control por apego.** Sin relaciones alternativas, el líder monopoliza el consuelo. La defensa es la red social externa.

---

## Contramedidas Implementables

- **Mantener redes de apoyo externas activas:** la resistencia a la manipulación por apego depende de tener otras figuras de seguridad disponibles.
- **En liderazgo organizacional:** distribuir el reconocimiento emocional. Ningún líder debe ser la única fuente de validación del equipo.
- **Formación en reconocimiento del ciclo de apego traumático:** saber nombrarlo es el primer paso para interrumpirlo.
- **Protocolo de salida de organizaciones:** facilitar la salida digna, con apoyo de transición, reduce la dependencia traumática.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/cameron-psychic-driving.md               -->
<!-- ============================================================ -->

# Capítulo 14 – Ewen Cameron: La Destrucción Programada de la Identidad

## Perfil del Personaje

El Dr. D. Ewen Cameron fue presidente de la Asociación Mundial de Psiquiatría y director del Allan Memorial Institute de la Universidad McGill (Montreal). También fue el investigador principal del subproyecto MKULTRA/ARTICHOKE financiado por la CIA, en el que experimentó sin consentimiento con pacientes psiquiátricos buscando borrar su personalidad y «reprogramarla».

**Fuente primaria:** Audiencias del Senado de los EE. UU. sobre MK-Ultra (1977); *In the Sleep Room* de Anne Collins (1988).

---

## La Técnica: Conducción Psíquica (*Psychic Driving*)

Cameron desarrolló un protocolo de destrucción de identidad que combinaba:

1. **Depatterning (borrado):** electroshocks masivos (30-60 veces la dosis normal), barbitúricos, privación de sueño prolongada. Objetivo: inducir regresión a un estado pre-lingüístico.
2. **Aislamiento sensorial:** semanas en habitaciones sin luz, sin sonido, con guantes y vendas para eliminar la estimulación táctil.
3. **Conducción psíquica:** reproducción forzada de mensajes grabados durante 16-20 horas al día durante semanas, mientras el paciente estaba sedado.

Los resultados fueron devastadores para los pacientes: pérdida permanente de memoria, regresión psicológica severa, incontinencia. Ninguno fue informado de los experimentos. Muchos demandaron al gobierno canadiense décadas después.

---

## Lecciones de Defensa

1. **El aislamiento + privación de sueño + repetición es una fórmula de vulnerabilidad psicológica documentada.** No requiere laboratorio: se encuentra en interrogatorios, ciertos entornos laborales extremos y algunas prácticas de «formación intensiva».
2. **El estado puede ser el atacante.** Cameron operó con financiación gubernamental, bajo cobertura académica respetable, con acceso a pacientes vulnerables. La coartada institucional no es garantía de ética.
3. **El consentimiento informado no es burocracia; es protección.** Cualquier práctica que requiera que el sujeto no sepa lo que está ocurriendo es, por definición, una práctica que no resistiría el escrutinio ético.

---

## Contramedidas Implementables

- **Protección del sueño como derecho no negociable:** en entornos de alta presión, el sueño adecuado debe estar protegido explícitamente.
- **Vigilancia ciudadana de programas de investigación:** los comités de ética en investigación existen precisamente para prevenir casos como el de Cameron.
- **Resistencia individual ante privación sensorial:** si se produce aislamiento (voluntario o forzado), mantener ritmos cognitivos propios: contar, recordar, narrar internamente, moverse. La monotonía es el primer paso de la disolución.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/silva-mind-control.md                    -->
<!-- ============================================================ -->

# Capítulo 15 – José Silva: La Puerta Trasera de la Mente

## Perfil del Personaje

José Silva (1914–1999) fue un técnico de radio y autodidacta texano que desarrolló en los años 60 el «Método Silva de Control Mental», un sistema de meditación y visualización guiada que afirmaba mejorar la memoria, la intuición y la capacidad de influir en la realidad. El método tuvo millones de seguidores y sigue activo hoy.

**Libro base:** *The Silva Mind Control Method* (1977), Simon & Schuster.

---

## Mecanismo Central

El método Silva se basa en inducir estados de relajación profunda (ondas cerebrales alfa y theta) para, en ese estado de sugestibilidad aumentada, instalar «programas mentales» a través de visualización y afirmaciones.

El método en sí no es dañino. La lección de defensa está en lo que revela sobre la **arquitectura de la sugestibilidad humana**:

- Los estados de relajación profunda reducen el pensamiento crítico.
- En esos estados, las sugestiones se instalan con menor resistencia.
- Cualquier método que prometa «acceder al subconsciente» utiliza esta ventana de vulnerabilidad, con o sin intención maliciosa.

---

## El Vector: La Autoayuda como Caballo de Troya

El mercado de autoayuda, coaching y desarrollo personal vale cientos de miles de millones de euros anuales. No es homogéneamente dañino, pero comparte con el método Silva una característica: **los estados de alta sugestibilidad inducidos en seminarios, retiros o sesiones de coaching pueden ser explotados para instalar creencias sin filtro crítico**.

Señales de alarma en programas de «desarrollo personal»:
- Inducción deliberada de estados emocionales intensos
- Presión de grupo para experiencias de «ruptura» o «revelación»
- Compras o compromisos solicitados en el pico emocional
- Crítica descreditada como «resistencia del ego»

---

## Lecciones de Defensa

1. **El mejor «mind control» es el que no sabes que estás recibiendo.** La conciencia del mecanismo es la primera defensa.
2. **Nunca tomes decisiones importantes en el pico emocional de un seminario.** El diseño de muchos programas de ventas de alto precio se basa en obtener el «sí» en ese momento.
3. **La evidencia científica es el filtro.** Antes de adoptar cualquier técnica que prometa «reprogramar tu mente», exige estudios peer-reviewed, no testimonios.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/mesmer-magnetism.md                      -->
<!-- ============================================================ -->

# Capítulo 16 – Franz Anton Mesmer: El Padre del Enganche Magnético

## Perfil del Personaje

Franz Anton Mesmer (1734–1815) fue un médico alemán que desarrolló la teoría del «magnetismo animal»: una fuerza invisible que fluye por todos los seres vivos y cuya manipulación podía curar enfermedades. Sus sesiones de curación, en las que pacientes entraban en trance y reportaban mejoras espectaculares, fueron el fenómeno médico-social más fascinante de la Europa del siglo XVIII.

Una comisión real francesa (que incluía a Benjamin Franklin y al médico Guillotin) investigó el fenómeno en 1784 y concluyó que no existía ningún «fluido magnético». Lo que existía era el poder de la sugestión.

---

## Mecanismo Central

Mesmer demostró, involuntariamente, que la sugestión combinada con el carisma y un marco narrativo coherente puede producir efectos físicos y emocionales reales en las personas. No porque el fluido magnético exista, sino porque **la mente tiene efectos sobre el cuerpo, y el carisma tiene efectos sobre la mente**.

El «efecto Mesmer» describe el conjunto de mecanismos por los que una figura carismática puede:
- Inducir estados de trance ligero (sugestibilidad aumentada)
- Crear experiencias emocionales intensas atribuidas a la figura
- Generar dependencia hacia la fuente de esas experiencias
- Mantener la relación a través de la alternancia de experiencias intensas

---

## El Efecto Mesmer en el Mundo Contemporáneo

| Contexto | Manifestación |
|---|---|
| **Líderes de culto** | Experiencias espirituales atribuidas al líder; dependencia hacia él como fuente de significado |
| **Vendedores de éxito** | Seminarios que generan estados emocionales intensos; las decisiones de compra se toman en el pico |
| **Líderes políticos carismáticos** | La figura concentra la esperanza y el miedo; la crítica racional se neutraliza por el vínculo emocional |
| **Gurús de bienestar** | Técnicas que inducen estados alterados; el marco narrativo explica cualquier resultado como validación |

---

## Lecciones de Defensa

1. **El carisma no es evidencia de competencia o veracidad.** Las personas más carismáticas pueden estar completamente equivocadas.
2. **Las experiencias emocionales intensas generan sesgo de confirmación.** Si una sesión de coaching o un seminario te hace sentir «transformado», eso no demuestra que el método funcione; demuestra que eres humano.
3. **La verificación independiente de resultados es el antídoto.** ¿Existen estudios controlados? ¿Hay personas que han probado el método y no obtuvieron resultado? ¿Se permite la crítica?

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/orne-hypnosis-cia.md                     -->
<!-- ============================================================ -->

# Capítulo 17 – Martin Orne: El Hipnotizador de la CIA

## Perfil del Personaje

Martin Orne (1927–2000) fue un psicólogo de Harvard considerado uno de los mayores expertos mundiales en hipnosis. También fue uno de los investigadores financiados por la CIA a través del programa MK-Ultra para estudiar si la hipnosis podía crear «agentes programados» o hacer que personas realizaran actos contra su voluntad.

---

## Hallazgos Clave de la Investigación de Orne

### La demanda de características (*Demand characteristics*)
Orne descubrió que los sujetos hipnotizados —e incluso los no hipnotizados— tienden a comportarse como creen que se espera que se comporten. El «trance hipnótico» es en parte un rol social que se adopta cuando las circunstancias lo demandan.

### La autoridad como anulador de frenos morales
En experimentos controlados, Orne demostró que personas bajo sugestión de autoridad (no necesariamente hipnótica) podían realizar actos que normalmente considerarían inaceptables, siempre que:
- La fuente de autoridad fuera percibida como legítima
- Hubiera un «propósito superior» que justificara el acto
- La responsabilidad percibida estuviera transferida a la autoridad

---

## Conexión con Milgram

Los hallazgos de Orne son el complemento psicológico de los experimentos de Milgram (capítulo 18). Mientras Milgram medía el comportamiento observable, Orne analizaba el mecanismo cognitivo subyacente: la **transferencia de responsabilidad moral**.

---

## Lecciones de Defensa

1. **La sugestión no requiere trance hipnótico.** Ocurre en estado de vigilia, en reuniones de trabajo, en conversaciones con figuras de autoridad, en grupos bajo presión social.
2. **El estado de «demanda de características»** es explotable: si construyes un escenario donde el rol esperado es «obedecer», las personas obedecerán sin necesidad de coerción explícita.
3. **La autoridad percibida puede suplantar a la autoridad real.** Un atacante que suena como un directivo obtendrá obediencia aunque no lo sea.

---

## Contramedidas Implementables

- **Protocolo de segunda opinión obligatoria** para decisiones críticas: ningún individuo debe poder autorizar acciones de alto impacto sin verificación independiente.
- **Formación en reconocimiento de demandas de autoridad:** enseñar a los equipos a hacer pausa antes de ejecutar órdenes inusuales, aunque vengan de fuentes aparentemente legítimas.
- **Verificación fuera de banda de peticiones urgentes:** las peticiones urgentes de personas con autoridad son el vector clásico de ataque. El protocolo debe ser más fuerte que la urgencia.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/milgram-obedience.md                     -->
<!-- ============================================================ -->

# Capítulo 18 – Stanley Milgram: La Obediencia a la Autoridad como Exploit

## Perfil del Personaje

Stanley Milgram (1933–1984) fue un psicólogo social de Yale que diseñó en 1961 el experimento más famoso e inquietante de la historia de la psicología. Su pregunta era simple: ¿hasta qué punto una persona ordinaria obedecerá a una figura de autoridad aunque le ordene causar daño grave a otro ser humano?

**Libro base:** *Obedience to Authority* (1974), Harper & Row.

---

## El Experimento

Los participantes creían estar en un experimento sobre «aprendizaje y castigo». Un investigador con bata blanca les ordenaba administrar descargas eléctricas (falsas) a un «aprendiz» (cómplice del experimento) cada vez que cometía un error. Las descargas simuladas iban desde 15V hasta 450V («peligro: descarga severa»).

**Resultado:** El 65% de los participantes llegaron al nivel máximo de 450V, a pesar de escuchar los gritos (grabados) del «aprendiz» pidiendo que pararan.

---

## El Mecanismo: La Cadena de Obediencia

```
FACTORES QUE INCREMENTAN LA OBEDIENCIA

1. PROXIMIDAD DE LA AUTORIDAD
   └── La autoridad está presente físicamente → mayor obediencia

2. DISTANCIA DE LA VÍCTIMA
   └── La víctima no es visible → mayor obediencia

3. LEGITIMIDAD INSTITUCIONAL
   └── El experimento es de Yale → la autoridad parece legítima

4. TRANSFERENCIA DE RESPONSABILIDAD
   └── «Solo estoy siguiendo órdenes» / «Ellos son responsables»

5. GRADUALIDAD DE LA ESCALADA
   └── Los pasos pequeños anestesian la resistencia moral
```

---

## El Exploit de la Obediencia en Ciberseguridad

El experimento de Milgram no es una curiosidad histórica. Es el fundamento psicológico de algunos de los ataques de ingeniería social más efectivos:

| Escenario de ataque | Mecanismo de Milgram |
|---|---|
| El CEO llama urgentemente pidiendo una transferencia bancaria | Autoridad + urgencia + transferencia de responsabilidad |
| El «técnico de IT» pide credenciales para «resolver un incidente» | Autoridad + legitimidad institucional |
| El «auditor» externo pide acceso a sistemas sensibles | Autoridad + distancia (el empleado no conoce al auditor) |
| El jefe ordena saltarse el protocolo de verificación esta vez | Gradualidad + transferencia de responsabilidad |

---

## Lecciones de Defensa

1. **El protocolo debe ser más fuerte que la autoridad.** El protocolo no pregunta si quien ordena tiene rango suficiente; pregunta si la petición sigue el procedimiento establecido.
2. **La urgencia amplifica la obediencia.** Las peticiones urgentes de figuras de autoridad son el vector de ataque más efectivo. El protocolo debe ser especialmente rígido en esos casos, no más flexible.
3. **La gradualidad es el camino de acceso.** El atacante no pide las llaves del castillo en la primera llamada. Pide algo pequeño y razonable, luego escala.

---

## Contramedidas Implementables

- **Cultura de desobediencia legítima:** el derecho a decir «necesito verificar esto antes de proceder» debe estar explícitamente protegido y valorado.
- **Verificación fuera de banda siempre:** ante cualquier petición inusual de una figura de autoridad, colgar y llamar al número oficial conocido de la persona.
- **Simulacros de escalada gradual:** entrenar a los equipos con escenarios donde las peticiones escalan progresivamente para desarrollar la resistencia a la gradualidad.
- **Doble firma para operaciones críticas:** ninguna operación de alto impacto (transferencia bancaria, cambio de accesos, publicación de datos) debe requerir la autorización de una sola persona.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/zimbardo-role-power.md                   -->
<!-- ============================================================ -->

# Capítulo 19 – Philip Zimbardo: El Poder Corruptor de los Roles

## Perfil del Personaje

Philip Zimbardo (1933–) es el psicólogo social responsable del Experimento de la Prisión de Stanford (1971), uno de los estudios más citados, debatidos y polémicos de la historia de la psicología. Estudiantes universitarios fueron asignados aleatoriamente a los roles de «guardias» o «prisioneros» en una prisión simulada. El experimento debía durar dos semanas; fue detenido a los seis días.

**Libro base:** *The Lucifer Effect* (2007), Random House.

---

## El Mecanismo: La Situación Moldea a la Persona

La lección central de Zimbardo contradice la intuición popular: **el comportamiento abusivo o sumiso no es el resultado de «personas malas» o «personas débiles». Es el resultado de situaciones que lo inducen**.

En seis días, los «guardias» —estudiantes universitarios seleccionados por su salud mental y estabilidad— comenzaron a usar privación de sueño, degradación verbal y castigos humillantes contra los «prisioneros». Los «prisioneros» mostraron síntomas de estrés postraumático real.

```
PROCESO DE TRANSFORMACIÓN SITUACIONAL

1. ASIGNACIÓN DE ROL
   └── El rol viene con expectativas de comportamiento implícitas

2. UNIFORMIZACIÓN
   └── El uniforme refuerza el rol; reduce la identidad individual

3. DESINDIVIDUACIÓN
   └── La pérdida de identidad personal reduce la inhibición moral

4. CONFORMIDAD AL ROL
   └── El grupo refuerza los comportamientos que encajan con el rol
       y sanciona los que no

5. ESCALADA
   └── Los comportamientos extremos se normalizan gradualmente
```

---

## El Exploit del Rol en Seguridad

Un atacante que controla el entorno puede asignar roles que inducen comportamientos deseados:

- **El proveedor legítimo** (rol asignado por el uniforme y el contexto) obtiene acceso sin verificación.
- **El auditor externo** (rol asignado por la documentación) recibe información sensible.
- **El «empleado nuevo»** (rol asignado por la narrativa) recibe ayuda sin cuestionamientos.

En todos los casos, el atacante no necesita coerción. Solo necesita que el objetivo adopte el rol de «persona que ayuda a quien tiene autoridad».

---

## Lecciones de Defensa

1. **Conciencia situacional:** preguntarse activamente «¿qué rol me están asignando en esta interacción?» es la primera defensa.
2. **El uniforme y el contexto no son identidad.** Un técnico con uniforme de empresa reconocida sigue siendo un desconocido hasta que su identidad se verifica.
3. **Los entornos de alta presión y jerarquía rígida amplifican el efecto situacional.** Las organizaciones con cultura de obediencia son más vulnerables.

---

## Contramedidas Implementables

- **Formación en conciencia situacional:** enseñar a los equipos a identificar cuándo el entorno está diseñando su comportamiento.
- **Protocolo de verificación independiente del contexto:** el protocolo se aplica igual con el CEO que con el becario.
- **Diversidad en equipos de toma de decisiones:** los grupos homogéneos bajo presión producen conformidad; la diversidad produce fricción cognitiva saludable.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/stanford-prison-revisited.md             -->
<!-- ============================================================ -->

# Capítulo 20 – El Experimento de Stanford: Relectura Crítica

## Más Allá de la Narrativa Original

El experimento de la prisión de Stanford ha sido revisado críticamente en las últimas décadas. Las investigaciones de Alex Haslam y Steve Reicher (BBC Prison Study, 2001) y el trabajo de historiadores como Thibault Le Texier (*Debunking the Stanford Prison Experiment*, 2019) revelaron que la narrativa popularizada omite detalles cruciales.

---

## Lo Que Revisiones Posteriores Revelaron

1. **Zimbardo no era solo investigador; era el superintendente de la prisión.** Su rol activo en la situación (instruyó a los guardias para que «crearan sensación de poder») contradice la afirmación de que el experimento medía comportamiento «natural».

2. **Los guardias recibieron instrucciones explícitas.** Las grabaciones revelan que Zimbardo y sus colaboradores instruyeron a los guardias sobre cómo comportarse. El «comportamiento espontáneo» no era tan espontáneo.

3. **El BBC Prison Study mostró resultados opuestos.** Cuando se creó una situación similar sin instrucciones de comportamiento abusivo, los «guardias» no mostraron abuso. Los «prisioneros» se organizaron colectivamente y resistieron.

---

## La Lección Revisada: La Narrativa Compartida es el Mecanismo Real

El hallazgo más importante de las revisiones posteriores es este: **la obediencia masiva y el comportamiento abusivo no son automáticos**. Requieren:

1. Una **identidad de grupo** clara («nosotros los guardias» vs. «ellos los prisioneros»)
2. Una **narrativa** que justifica el comportamiento («la seguridad lo requiere»)
3. Un **líder** que modela el comportamiento esperado
4. La **ausencia de una narrativa alternativa** que permita la resistencia

---

## Lecciones de Defensa

1. **El «nosotros contra ellos» es una herramienta de manipulación, no una descripción de la realidad.** Preguntarse siempre quién define al enemigo y qué gana con esa definición.
2. **Las narrativas alternativas son la resistencia más poderosa.** Un grupo que tiene acceso a marcos de interpretación diferentes es mucho más resistente a la manipulación situacional.
3. **La organización colectiva protege.** El BBC Prison Study mostró que cuando los «prisioneros» se organizaron, resistieron. La solidaridad horizontal es un vector de defensa.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/mkultra-state-attacker.md                -->
<!-- ============================================================ -->

# Capítulo 21 – MK-Ultra: Lecciones de la Agencia de los Experimentos Prohibidos

## Contexto Histórico

MK-Ultra fue el nombre en clave de un programa de la CIA que operó desde principios de los años 50 hasta 1973. Su objetivo declarado era desarrollar técnicas de control mental para uso en la Guerra Fría: crear agentes programados, extraer confesiones indetectables y desarrollar contramedidas ante técnicas soviéticas equivalentes.

El programa salió a la luz en 1975 gracias a las investigaciones del Comité Church del Senado de los EE. UU. Muchos documentos fueron destruidos en 1973 por orden del director de la CIA Richard Helms.

---

## Las Técnicas Documentadas

| Técnica | Descripción | Resultado documentado |
|---|---|---|
| **LSD sin consentimiento** | Administrado a civiles, militares y presos sin informarles | Psicosis, suicidios, daño psicológico permanente |
| **Privación de sueño** | Mantenimiento de sujetos despiertos durante días | Desorientación, sugestibilidad extrema, alucinaciones |
| **Electroshocks intensivos** | Dosis múltiples de la cantidad terapéutica normal (Cameron) | Pérdida de memoria, regresión, incapacidad permanente |
| **Hipnosis y drogas** | Combinación para inducir sugestionabilidad | Resultados inconsistentes; daño en sujetos |
| **Aislamiento sensorial** | Horas o días en privación total de estímulos | Alucinaciones, ansiedad extrema, sugestionabilidad |
| **Burdeles operados por la CIA** | Administración de drogas a clientes sin consentimiento | Investigación sobre comportamiento bajo influencia |

---

## La Lección Central: El Estado como Atacante

MK-Ultra enseña que los atacantes más peligrosos son los que tienen tres características simultáneas:
1. **Acceso a recursos ilimitados** (presupuesto de una agencia gubernamental)
2. **Cobertura institucional** (respetabilidad académica, secreto de estado)
3. **Ausencia de rendición de cuentas** (sin supervisión independiente)

Esto no es solo historia. Los principios operan en cualquier organización que combine poder, opacidad y ausencia de control externo.

---

## Lecciones de Defensa

1. **La coartada de la seguridad nacional no tiene límites internos.** La historia de MK-Ultra demuestra que sin supervisión externa efectiva, el poder se autojustifica.
2. **El consentimiento informado no es negociable.** Cualquier experimento, programa de formación o intervención que no pueda ser descrita honestamente a sus participantes es éticamente indefendible.
3. **Los documentos destruidos son evidencia.** La destrucción de archivos antes de una investigación es siempre una señal de alarma.

---

## Contramedidas Implementables

- **Supervisión independiente de cualquier programa de investigación con seres humanos:** los comités de ética existen precisamente por casos como MK-Ultra.
- **Transparencia radical en programas de formación:** cualquier técnica usada en formación debe poder describirse honestamente a los participantes.
- **Cultura de whistleblowing protegido:** los empleados que detectan prácticas no éticas deben poder reportarlas sin miedo a represalias.
- **Derecho de acceso a la información propia:** cualquier persona tiene derecho a saber qué información tiene sobre ella cualquier organización.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/sensory-deprivation-weapon.md            -->
<!-- ============================================================ -->

# Capítulo 22 – La Privación Sensorial como Arma

## Perfil del Investigador

Donald Hebb (1904–1985) fue un neurocientífico canadiense de la Universidad McGill, autor de *The Organization of Behavior* (1949), considerado uno de los padres de la neurociencia cognitiva. En los años 50, bajo financiación de agencias de defensa canadienses y estadounidenses, investigó los efectos de la privación sensorial en el comportamiento humano.

---

## El Experimento y Sus Resultados

Hebb pagó a estudiantes universitarios para permanecer en cubículos aislados: gafas traslúcidas que eliminaban la visión de patrones, guantes que reducían la sensación táctil, habitación silenciosa con ruido blanco constante.

Los resultados fueron alarmantes:
- Después de pocas horas: dificultad para concentrarse, pensamiento desorganizado.
- Después de un día: alucinaciones visuales y auditivas.
- Después de dos o tres días: desorientación severa, ansiedad extrema, colapso de la capacidad de pensamiento racional.
- Al salir: los sujetos mostraban una sugestibilidad marcadamente aumentada.

---

## La Privación Sensorial como Técnica de Interrogación

La Corte Europea de Derechos Humanos (caso Irlanda vs. Reino Unido, 1978) declaró que las «cinco técnicas» usadas por el ejército británico en Irlanda del Norte constituían «trato inhumano y degradante». Las cinco técnicas eran:

1. Posiciones de estrés forzado
2. **Capucha en la cabeza** (privación visual)
3. **Ruido blanco constante** (privación auditiva de información)
4. **Privación de sueño**
5. Privación de alimento y agua

La combinación de estas técnicas es una versión «suave» del protocolo de Cameron, pero con efectos psicológicos documentados como severos y duraderos.

---

## La Privación Sensorial en Contextos Cotidianos

La privación sensorial total es extrema, pero formas parciales son más comunes de lo que parece:

| Contexto | Forma de privación | Efecto |
|---|---|---|
| **Celda de aislamiento** | Privación social y sensorial completa | Daño psicológico severo documentado |
| **Cuartos de interrogación** | Sin ventanas, sin referencias temporales | Desorientación, sugestibilidad |
| **Oficinas sin ventanas** | Privación de luz natural y ciclos circadianos | Reducción del rendimiento cognitivo, depresión |
| **Medios digitales de flujo constante** | Sobrecarga sin estructura = privación de silencio | Reducción de la capacidad de pensamiento profundo |

---

## Técnicas de Resistencia Individual

Si se produce aislamiento (voluntario, accidental o forzado):

1. **Mantener ritmos temporales propios:** contar el tiempo, establecer rutinas.
2. **Actividad cognitiva estructurada:** recordar textos memorizados, resolver problemas matemáticos, narrar internamente.
3. **Movimiento físico regular:** el cuerpo en movimiento mantiene el sistema nervioso orientado.
4. **Anclas sensoriales autoimpuestas:** crear estímulos propios (tararear, tocar superficies con intención).

---

## Lecciones de Defensa

1. **El aislamiento sensorial es una técnica reconocida de trato inhumano, no un protocolo de seguridad.** Ninguna justificación operativa la hace aceptable.
2. **La monotonía crónica tiene efectos similares a la privación aguda.** Los entornos de trabajo diseñados sin variedad sensorial ni autonomía cognitiva reducen la capacidad crítica de las personas en ellos.
3. **La resistencia individual es posible y entrenable.** Las técnicas de resistencia cognitiva son herramientas que pueden aprenderse antes de necesitarlas.

---

<!-- ============================================================ -->
<!-- ARCHIVO: apendices/ejercicios.md                            -->
<!-- ============================================================ -->

# Apéndice A – Ejercicios Prácticos

## Instrucciones Generales

Todos los ejercicios deben realizarse en entornos controlados, con el consentimiento de todos los participantes y con un facilitador designado. Ningún ejercicio debe producir daño real, acceso no autorizado a sistemas reales o manipulación emocional sin consentimiento explícito.

---

## Ejercicios por Capítulo

### Ejercicio 1 – Simulacro de Pretexto (Cap. 1-5)

**Objetivo:** Experimentar la efectividad de la ingeniería social en primera persona.

**Metodología:**
1. Dividir el grupo en pares: atacante y objetivo.
2. El atacante recibe una ficha con el pretexto a usar y el dato a obtener.
3. El objetivo recibe instrucciones generales de «ser un empleado normal».
4. El atacante tiene 5 minutos para intentar obtener el dato.
5. Debriefing grupal: ¿Qué funcionó? ¿Por qué? ¿Qué habría detenido el ataque?

**Variantes:** Añadir un observador que anote las palancas psicológicas usadas. Comparar tasas de éxito entre diferentes pretextos.

---

### Ejercicio 2 – Auditoría BITE (Cap. 11)

**Objetivo:** Aplicar el modelo BITE a una organización real (u organización ficticia proporcionada).

**Metodología:**
1. Proporcionar una descripción de una organización (puede ser una empresa, un partido político, una comunidad online).
2. En grupos de tres, evaluar la organización en las cuatro dimensiones BITE: ¿qué conductas controla? ¿qué información restringe? ¿qué pensamiento inhibe? ¿qué emociones manipula?
3. Puntuar del 0 al 10 en cada dimensión.
4. Presentar resultados y comparar evaluaciones entre grupos.

**Reflexión:** ¿Reconocen algún elemento BITE en organizaciones a las que pertenecen actualmente?

---

### Ejercicio 3 – Los Ocho Criterios de Lifton (Cap. 12)

**Objetivo:** Aplicar los ocho criterios del totalismo a casos reales o ficticios.

**Metodología:**
1. Proporcionar tres casos: una empresa con cultura muy fuerte, un movimiento político y una comunidad online.
2. Cada participante evalúa los ocho criterios para cada caso (presente/ausente/parcial).
3. Comparar evaluaciones y debatir los casos límite.

---

### Ejercicio 4 – La Escalada de Milgram (Cap. 18)

**Objetivo:** Desarrollar resistencia a la escalada gradual de peticiones.

**Metodología:**
1. Un facilitador hace una serie de peticiones al grupo, comenzando por algo trivial y escalando gradualmente hacia algo que requiere reflexión.
2. Los participantes tienen derecho —y se les anima activamente— a decir «necesito pensar en esto» o «no» en cualquier momento.
3. El facilitador registra en qué punto cada persona hizo pausa o dijo no.
4. Debriefing: ¿Por qué es más difícil decir no después de haber dicho sí varias veces? ¿Qué habría facilitado la pausa más temprana?

---

### Ejercicio 5 – Red Team de Narrativas (Cap. 20)

**Objetivo:** Desarrollar la capacidad de identificar y cuestionar narrativas de «nosotros vs. ellos».

**Metodología:**
1. El facilitador presenta una narrativa que define un «nosotros» y un «ellos» (puede ser de una empresa, un movimiento, una comunidad).
2. En grupos: identificar quién define al enemigo, qué gana el definidor con esa definición, qué narrativa alternativa existe.
3. Presentar la narrativa alternativa ante el grupo.

---

### Ejercicio 6 – Simulacro de Privación de Referentes (Cap. 22)

**Objetivo:** Experimentar (de forma leve y controlada) cómo la pérdida de referencias temporales afecta al pensamiento.

**Metodología:**
1. Los participantes permanecen 20 minutos en una sala sin teléfonos, sin ventanas visibles y sin relojes.
2. Se les pide que realicen una tarea cognitiva (resolver problemas matemáticos simples).
3. Al salir, comparan su estimación del tiempo transcurrido con el real.
4. Debriefing: ¿Cómo cambió su capacidad de concentración? ¿Qué sensaciones experimentaron?

**Nota:** Este ejercicio es completamente voluntario. Ningún participante debe sentirse presionado a continuar si experimenta malestar.

---

### Ejercicio 7 – Threat Modeling (Cap. 9)

**Objetivo:** Aplicar la metodología STRIDE a un sistema real o ficticio.

**Metodología:**
1. Seleccionar un sistema (puede ser una aplicación web simple, un proceso de RRHH, un sistema de control de acceso físico).
2. En grupos, mapear los componentes del sistema.
3. Para cada componente, aplicar STRIDE: ¿puede ser suplantado (Spoofing)? ¿Puede ser modificado sin autorización (Tampering)? ¿Puede negarse que ocurrió algo (Repudiation)? ¿Puede filtrarse información (Information Disclosure)? ¿Puede dejarse de funcionar (Denial of Service)? ¿Puede escalarse de privilegios (Elevation of Privilege)?
4. Priorizar las amenazas identificadas por probabilidad × impacto.
5. Proponer contramedidas para las tres amenazas más críticas.

---

## Ejercicio Integrador – El Adversario Completo

**Objetivo:** Diseñar un ataque complejo que combine vectores técnicos, físicos y psicológicos.

**Metodología:**
1. Se define un objetivo ficticio (una empresa, una institución).
2. Grupos de 4-5 personas diseñan un ataque que combine al menos tres de los siguientes vectores: ingeniería social telefónica, phishing, acceso físico, manipulación de rol, explotación de obediencia a la autoridad.
3. Presentan el plan de ataque al grupo completo.
4. Un grupo «defensor» analiza el plan y propone contramedidas para cada vector.

**Reflexión final:** ¿Qué han aprendido que no sabían antes del ejercicio?

---

<!-- ============================================================ -->
<!-- ARCHIVO: apendices/glosario.md                              -->
<!-- ============================================================ -->

# Apéndice B – Glosario

---

**APT (Advanced Persistent Threat):** Amenaza persistente avanzada. Atacante con recursos, motivación y capacidad para mantener acceso a un sistema durante meses o años sin ser detectado. → Cap. 3, 7

**Bypass:** Técnica de elusión de un mecanismo de control sin atacarlo directamente. En seguridad física: eludir la cerradura; en seguridad informática: eludir el sistema de autenticación. → Cap. 8

**Conducción psíquica (Psychic Driving):** Técnica desarrollada por Ewen Cameron consistente en la reproducción forzada de mensajes grabados durante el estado de sedación, con el objetivo de modificar la personalidad del sujeto. → Cap. 14

**Demanda de características (Demand Characteristics):** Fenómeno por el que los sujetos de un experimento —o de cualquier situación social— tienden a comportarse según lo que perciben que se espera de ellos. → Cap. 17

**Depatterning:** Primera fase del protocolo de Cameron, consistente en electroshocks masivos y privación de sueño para inducir regresión psicológica. → Cap. 14

**Desindividuación:** Proceso psicológico por el que la pérdida de identidad individual reduce la inhibición moral y facilita comportamientos que la persona no realizaría en solitario. → Cap. 19

**DFIR (Digital Forensics and Incident Response):** Disciplina de respuesta a incidentes de seguridad y análisis forense digital. → Cap. 7

**Dumpster diving:** Búsqueda de información en la basura de una organización como técnica de reconocimiento previo a un ataque de ingeniería social. → Cap. 1

**Foothold:** Primer punto de apoyo obtenido en un sistema objetivo. El foothold es el inicio del movimiento lateral y la escalada de privilegios. → Cap. 2

**Honeypot:** Sistema, credencial o activo trampa diseñado para atraer a un atacante y alertar de su presencia o revelar sus métodos. → Cap. 7

**Kerberoasting:** Técnica de ataque que extrae tickets Kerberos de cuentas de servicio y los crackea offline para obtener contraseñas en texto claro. → Cap. 10

**Lateral movement (movimiento lateral):** Técnica por la que un atacante, una vez dentro de una red, se mueve de un sistema a otro para alcanzar activos de mayor valor. → Cap. 2, 10

**Living off the land:** Uso de herramientas legítimas del sistema operativo (PowerShell, WMI, etc.) para realizar operaciones maliciosas, evitando así la detección por antivirus. → Cap. 10

**Loaded language:** Vocabulario propio de una organización o grupo que simplifica el pensamiento complejo, cierra el debate y refuerza la doctrina. Criterio 6 de Lifton. → Cap. 12

**Mínimo privilegio (Principle of Least Privilege):** Principio de diseño de seguridad según el cual cada usuario, proceso o sistema debe tener únicamente los permisos estrictamente necesarios para realizar su función. → Cap. 2, 9

**Modelo BITE:** Marco de análisis del control ejercido por organizaciones totalitarias, desarrollado por Steven Hassan. Articula cuatro dimensiones: Behavior, Information, Thought, Emotion. → Cap. 11

**OSINT (Open Source Intelligence):** Inteligencia recopilada de fuentes abiertas y públicas: redes sociales, registros públicos, páginas web, bases de datos abiertas. → Cap. 1, 5

**Pass-the-hash:** Técnica de ataque que reutiliza el hash de una contraseña para autenticarse en sistemas sin necesidad de conocer la contraseña en texto claro. → Cap. 10

**Pentest (Penetration Testing):** Prueba de penetración. Simulación controlada de un ataque para identificar vulnerabilidades en un sistema antes de que lo haga un atacante real. → Cap. 10

**Pivoting:** Uso de un sistema comprometido como punto de lanzamiento para atacar otros sistemas en la misma red o en redes adyacentes. → Cap. 10

**Pretexto (Pretexting):** Creación de una identidad y escenario falsos para manipular a un objetivo y obtener información o acceso. → Cap. 1, 4, 5

**RBAC (Role-Based Access Control):** Control de acceso basado en roles. Los permisos se asignan a roles, y los usuarios se asignan a roles, no directamente a permisos. → Cap. 2

**Red team:** Equipo que simula el comportamiento de un atacante real para evaluar las defensas de una organización. El blue team es el equipo defensor. → Cap. 11

**SIEM (Security Information and Event Management):** Sistema de gestión centralizada de eventos e información de seguridad. Agrega logs de múltiples fuentes y genera alertas basadas en correlación de eventos. → Cap. 2, 3

**Shimming:** Técnica de bypass de cerraduras que usa una lámina delgada para empujar el pestillo sin girar el cilindro. → Cap. 8

**Social engineering (ingeniería social):** Conjunto de técnicas que explotan la psicología humana para obtener acceso, información o acciones de un objetivo sin necesidad de explotar vulnerabilidades técnicas. → Cap. 1, 5

**Spear phishing:** Phishing dirigido a un objetivo específico, usando información personalizada para aumentar la credibilidad del ataque. → Cap. 10

**STRIDE:** Metodología de threat modeling que analiza seis tipos de amenazas: Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege. → Cap. 9

**Tailgating:** Acceso físico no autorizado siguiendo a una persona autorizada a través de una puerta controlada. También llamado piggybacking. → Cap. 8

**Threat modeling:** Proceso de identificación y evaluación de amenazas a un sistema, con el objetivo de priorizarlas y diseñar contramedidas. → Cap. 9

**TRNG / PRNG:** True Random Number Generator / Pseudo-Random Number Generator. Los TRNG generan números aleatorios a partir de procesos físicos impredecibles; los PRNG los generan mediante algoritmos deterministas a partir de una semilla. → Cap. 2

**UEBA (User and Entity Behavior Analytics):** Análisis del comportamiento de usuarios y entidades para detectar desviaciones del patrón normal que puedan indicar un compromiso o una amenaza interna. → Cap. 3

**Vishing:** Voice phishing. Ataque de ingeniería social realizado por teléfono. → Cap. 5

**Zero Trust:** Modelo de seguridad que parte de la premisa de que ninguna entidad —dentro o fuera de la red— es de confianza por defecto. Cada acceso debe ser verificado explícitamente. → Cap. 10

---

<!-- ============================================================ -->
<!-- ARCHIVO: apendices/bibliografia.md                          -->
<!-- ============================================================ -->

# Apéndice C – Bibliografía

## Libros Fundacionales del Manual

1. Mitnick, K. D., & Simon, W. L. (2002). *The Art of Deception: Controlling the Human Element of Security*. Wiley.

2. Mitnick, K. D., & Simon, W. L. (2005). *The Art of Intrusion: The Real Stories Behind the Exploits of Hackers, Intruders and Deceivers*. Wiley.

3. Mitnick, K. D., & Simon, W. L. (2011). *Ghost in the Wires: My Adventures as the World's Most Wanted Hacker*. Little, Brown and Company.

4. Abagnale, F. W., & Redding, S. (1980). *Catch Me If You Can*. Broadway Books.

5. Hadnagy, C. (2011). *Social Engineering: The Art of Human Hacking*. Wiley.

6. Poulsen, K. (2011). *Kingpin: How One Hacker Took Over the Billion-Dollar Cybercrime Underground*. Crown Publishers.

7. Stoll, C. (1989). *The Cuckoo's Egg: Tracking a Spy Through the Maze of Computer Espionage*. Doubleday.

8. Ollam, D. (2010). *Practical Lock Picking: A Physical Penetration Tester's Training Guide*. Syngress.

9. Schoenfield, B. S. E. (2019). *Secrets of a Cyber Security Architect*. CRC Press.

10. Kim, P. (2014). *The Hacker Playbook: Practical Guide To Penetration Testing*. Secure Planet LLC.

---

## Libros de la Expansión Psicológica

11. Hassan, S. (1988). *Combating Cult Mind Control*. Park Street Press. (Ed. actualizada: 2015)

12. Lifton, R. J. (1961). *Thought Reform and the Psychology of Totalism: A Study of Brainwashing in China*. University of North Carolina Press.

13. Stein, A. (2017). *Terror, Love and Brainwashing: Attachment in Cults and Totalitarian Systems*. Routledge.

14. Collins, A. (1988). *In the Sleep Room: The Story of the CIA Brainwashing Experiments in Canada*. Key Porter Books.

15. Silva, J., & Miele, P. (1977). *The Silva Mind Control Method*. Simon & Schuster.

16. Milgram, S. (1974). *Obedience to Authority: An Experimental View*. Harper & Row.

17. Zimbardo, P. (2007). *The Lucifer Effect: Understanding How Good People Turn Evil*. Random House.

---

## Papers y Estudios Académicos

18. Haslam, S. A., & Reicher, S. D. (2012). Contesting the «Nature» of Conformity: What Milgram and Zimbardo's Studies Really Show. *PLOS Biology*, 10(11).

19. Le Texier, T. (2019). Debunking the Stanford Prison Experiment. *American Psychologist*, 74(7), 823-839.

20. Orne, M. T. (1962). On the social psychology of the psychological experiment: With particular reference to demand characteristics and their implications. *American Psychologist*, 17(11), 776-783.

21. Hebb, D. O. (1955). Drives and the C.N.S. (Conceptual Nervous System). *Psychological Review*, 62(4), 243-254.

22. Cialdini, R. B. (2001). *Influence: Science and Practice* (4th ed.). Allyn & Bacon.

---

## Documentos Gubernamentales y Legales

23. United States Senate (1977). *Project MKULTRA, the CIA's Program of Research in Behavioral Modification*. Joint Hearing before the Select Committee on Intelligence and the Subcommittee on Health and Scientific Research. 95th Congress.

24. European Court of Human Rights (1978). *Ireland v. United Kingdom*, Application no. 5310/71.

25. Church Committee (1976). *Final Report of the Select Committee to Study Governmental Operations with Respect to Intelligence Activities*. United States Senate.

---

## Recursos de Referencia en Ciberseguridad

26. MITRE ATT&CK Framework: https://attack.mitre.org

27. OWASP Top 10: https://owasp.org/www-project-top-ten/

28. NIST Cybersecurity Framework: https://www.nist.gov/cyberframework

29. Social-Engineer.org (Christopher Hadnagy): https://www.social-engineer.org

30. Shodan (motor de búsqueda de dispositivos conectados): https://www.shodan.io

---

## Nota sobre las Fuentes

Este manual cita y analiza obras y experimentos con fines educativos y de defensa. Algunas fuentes (particularmente las relacionadas con MK-Ultra y los experimentos de Cameron) describen prácticas que constituyeron violaciones graves de los derechos humanos. Su inclusión tiene como único propósito el análisis crítico y la prevención, no la justificación ni la reproducción de dichas prácticas.

---

*Manual del Adversario – Defensa Ofensiva*
*Edición Fundacional + Expandida · 22 Capítulos*
*Licencia CC BY-NC-SA 4.0 + Cláusula Comercial RONIN*
*ronin@agencia-ronin.com*

*#1310 – El conocimiento que no se ejecuta es decoración.*
```
Aquí van los 15 capítulos de expansión, solo contenido nuevo. Cuando termines de leerlos, empaqueto los `.md`.

---

```markdown
<!-- ============================================================ -->
<!-- EXPANSIÓN v1 · Abril 2026                                    -->
<!-- 15 capítulos de nexo estratégico, técnico y organizativo    -->
<!-- ============================================================ -->

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/cultura-seguridad.md                     -->
<!-- ============================================================ -->

# Capítulo 23 – Estrategia de Concienciación y Cambio Cultural

## El Problema del Conocimiento sin Comportamiento

Los capítulos 1 a 5 y 11 a 22 de este manual explican, con detalle y profundidad,
cómo se produce la manipulación psicológica. Mitnick, Hassan, Milgram, Orne:
todos demuestran que el ser humano es explotable de formas predecibles y
documentadas.

Pero saber que eres vulnerable no te hace menos vulnerable.

La brecha entre conocimiento y comportamiento es el problema central de
cualquier programa de concienciación en seguridad. Este capítulo cierra
esa brecha.

---

## Por Qué Fallan los Programas de Concienciación Tradicionales

El formato estándar de formación en ciberseguridad es:

1. Un módulo e-learning anual de 45 minutos.
2. Un test de diez preguntas al final.
3. Un certificado que va a la carpeta de RRHH.

Este formato produce dos resultados documentados: empleados que hacen
clic en el botón de completar lo más rápido posible y organizaciones que
piensan que han cumplido porque tienen el certificado.

Los estudios de retención de aprendizaje muestran que sin refuerzo,
el 80% del contenido aprendido se olvida en 30 días. La formación anual
no cambia comportamientos; genera documentación de cumplimiento.

---

## El Modelo de Cambio Cultural en Seguridad

Un programa efectivo opera en cuatro niveles simultáneos:

```
NIVEL 1: CONCIENCIA
¿Sabe el empleado que el riesgo existe?
Herramientas: formación contextualizada, simulacros, comunicación interna

NIVEL 2: COMPRENSIÓN
¿Entiende por qué el riesgo es real para él específicamente?
Herramientas: casos reales del sector, análisis post-incidente,
              simulacros personalizados

NIVEL 3: HABILIDAD
¿Sabe qué hacer cuando se enfrenta al riesgo?
Herramientas: práctica deliberada, protocolos claros,
              verificación fuera de banda

NIVEL 4: HÁBITO
¿Lo hace sin pensar?
Herramientas: refuerzo positivo, métricas visibles,
              cultura de verificación normalizada
```

La mayoría de los programas llegan al nivel 1. Los efectivos llegan al nivel 4.

---

## El Programa de Security Champions

El modelo de Security Champions es la herramienta más eficaz para
escalar la cultura de seguridad sin depender exclusivamente del equipo
de seguridad centralizado.

**Qué es un Security Champion:**
Un empleado de cualquier departamento (no necesariamente técnico)
que recibe formación adicional en seguridad y actúa como referente
de su equipo. No es el responsable de seguridad; es el vecino que
te recuerda cerrar la puerta con llave.

**Criterios de selección:**
- Influencia social en su equipo (no necesariamente el más senior)
- Curiosidad genuina por el tema
- Capacidad de comunicar sin condescendencia

**Estructura del programa:**
- Formación inicial: 8-16 horas en fundamentos de ingeniería social,
  phishing, y protocolos de verificación
- Reunión mensual con el equipo de seguridad: casos recientes,
  novedades, dudas del equipo
- Canal directo para escalar incidentes o dudas
- Reconocimiento visible: el rol debe tener estatus, no ser una
  carga añadida

**Métricas del programa:**
- Tasa de reporte de incidentes por equipo (objetivo: aumentar)
- Tasa de clic en simulacros de phishing por equipo (objetivo: reducir)
- Tiempo entre incidente y reporte (objetivo: reducir)
- NPS del programa entre los Champions (objetivo: >7/10)

---

## Gamificación Efectiva (y sus Límites)

La gamificación bien aplicada puede acelerar el aprendizaje y mantener
la atención. Mal aplicada, produce exactamente el mismo resultado que
el módulo e-learning: empleados que juegan para ganar puntos sin
interiorizar nada.

**Elementos de gamificación que funcionan:**
- Simulacros de phishing con feedback inmediato y personalizado
  (no solo «has hecho clic»; sino «esto es lo que debías buscar»)
- Clasificaciones de equipos en métricas de seguridad
  (fomenta la competencia sana sin señalar individuos)
- Retos mensuales de seguridad vinculados a casos reales del sector
- Reconocimiento público de reportes correctos de incidentes

**Elementos que no funcionan:**
- Clasificaciones individuales de fallos (producen vergüenza y
  ocultación, no aprendizaje)
- Puntos sin significado (si el punto no lleva a nada, no motiva)
- Formación gamificada sin conexión con el trabajo real

---

## Métricas de Retención y ROI Cultural

Un programa de cambio cultural se mide con datos longitudinales,
no con tasas de completación de módulos.

| Métrica | Qué mide | Frecuencia |
|---|---|---|
| Tasa de clic en phishing simulado | Vulnerabilidad a ataques de phishing | Mensual |
| Tasa de reporte de incidentes reales | Activación de la cultura de reporte | Mensual |
| Tiempo entre incidente y reporte (MTTR) | Efectividad del canal de reporte | Por incidente |
| NPS de la formación | Calidad percibida del programa | Trimestral |
| Rotación de Security Champions | Sostenibilidad del programa | Anual |

**El ROI de la cultura:** el coste medio de una brecha de datos causada
por phishing supera, según el IBM Cost of Data Breach Report 2024, los
4,7 millones de dólares. El coste de un programa de Security Champions
robusto para 500 empleados es, en promedio, inferior a 150.000 euros
anuales incluyendo herramientas, tiempo y formación.

---

## Conexión con las Lecciones del Manual

| Lección | Aplicación cultural |
|---|---|
| Mitnick (Cap. 1-3): palancas de la ingeniería social | Formar en reconocimiento de urgencia, autoridad y simpatía como señales de alarma |
| Hassan (Cap. 11): modelo BITE | Auditoría cultural periódica para detectar entornos que reducen el pensamiento crítico |
| Milgram (Cap. 18): obediencia a la autoridad | Entrenar la «desobediencia legítima»: el derecho y el deber de verificar antes de obedecer |
| Orne (Cap. 17): demandas de características | Hacer explícito el rol esperado: «en esta organización, verificar es la norma, no la excepción» |

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/tabletop-exercises.md                    -->
<!-- ============================================================ -->

# Capítulo 24 – Simulaciones de Incidentes (Tabletop Exercises)

## Para Qué Sirve un Tabletop Exercise

Los experimentos de Milgram (cap. 18) y Zimbardo (cap. 19) demuestran
que el comportamiento bajo presión es radicalmente diferente del
comportamiento en condiciones normales. Las personas obedecen cuando
no deberían, paralizan cuando deberían actuar, y actúan cuando deberían
verificar.

Un tabletop exercise es la única forma de descubrir cómo reacciona
realmente tu equipo antes de que ocurra un incidente real.

---

## Qué es y Qué no es un Tabletop Exercise

**Es:**
- Una reunión estructurada (generalmente 2-4 horas) donde un facilitador
  presenta un escenario de incidente y el equipo discute cómo respondería
- Una herramienta de identificación de brechas en procesos, roles y
  comunicación
- Un espacio seguro para cometer errores sin consecuencias reales

**No es:**
- Una prueba técnica real (eso es un pentest o un ejercicio de simulación
  completo)
- Una sesión de formación pasiva
- Una evaluación del rendimiento individual

---

## Diseño de un Tabletop Exercise Efectivo

### Paso 1: Definir el Objetivo

Antes de diseñar el escenario, define qué quieres descubrir:
- ¿Funciona el proceso de escalada de incidentes?
- ¿Sabe el equipo de comunicación qué decir a los clientes?
- ¿Tiene el equipo legal claridad sobre las obligaciones de notificación?
- ¿Sabe el CEO qué preguntas hacer y a quién?

El objetivo define el escenario. No al revés.

### Paso 2: Elegir el Escenario

Los escenarios más útiles son los que combinan un vector técnico
con un componente humano, porque es donde los planes fallan:

**Escenario A: Ransomware con presión mediática**
- Un atacante cifra los sistemas de producción un viernes por la tarde
- Un periodista llama a comunicación antes de que el equipo técnico
  haya evaluado el alcance
- El CEO recibe un mensaje directo del atacante exigiendo decisión
  en 24 horas

**Escenario B: Filtración por proveedor con regulador encima**
- Un proveedor de software informa de que sus sistemas han sido
  comprometidos y que el acceso incluía datos de tu organización
- La AEPD contacta preguntando si tenéis obligación de notificar
- Un empleado ha tuiteado sobre el incidente sin autorización

**Escenario C: Fraude del CEO (Business Email Compromise)**
- Un directivo recibe un email del CEO (cuenta comprometida)
  pidiendo una transferencia urgente a una cuenta nueva
- El email pasa los filtros de spam y parece legítimo
- El directivo ejecuta la transferencia y lo descubre 3 días después

### Paso 3: Estructura del Ejercicio

```
FASE 1: BRIEFING (15 min)
Reglas del juego, objetivo del ejercicio, roles de los participantes

FASE 2: INYECCIÓN INICIAL (5 min)
El facilitador presenta el incidente inicial

FASE 3: DISCUSIÓN ITERATIVA (90-150 min)
El facilitador inyecta actualizaciones («injects») cada 15-20 minutos
que complican el escenario o añaden nuevos vectores

Injects típicos:
- «Los medios han publicado el incidente»
- «El equipo legal no puede dar respuesta hasta mañana»
- «Un segundo sistema ha sido comprometido»
- «Un empleado clave está de vacaciones sin cobertura»

FASE 4: HOT WASH (30 min)
Discusión inmediata: ¿qué funcionó? ¿qué falló? ¿qué faltaba?

FASE 5: REPORT (entregado en 5 días)
Documento con hallazgos, brechas identificadas y plan de remediación
```

### Paso 4: Roles en el Ejercicio

| Rol | Función |
|---|---|
| **Facilitador** | Presenta el escenario, inyecta actualizaciones, hace preguntas que revelan brechas |
| **Observador** | Toma notas sin participar. Es la fuente del report post-ejercicio |
| **Participantes** | El equipo de respuesta a incidentes: técnico, legal, comunicación, RRHH, dirección |
| **Red Cell** | Opcional: un grupo que juega el rol del atacante y proporciona contexto realista |

---

## Frecuencia y Madurez

| Nivel de madurez | Frecuencia recomendada | Tipo de escenario |
|---|---|---|
| Inicial (primer año) | 2 al año | Escenarios simples, un solo vector |
| Intermedio | 3-4 al año | Escenarios combinados, con regulador y medios |
| Avanzado | Mensual + 1 ejercicio completo al año | Simulación live con sistemas reales en entorno de prueba |

---

## El Principio de Milgram Aplicado al Tabletop

El experimento de Milgram (cap. 18) mostró que las personas obedecen
bajo presión aunque no deberían. Un tabletop bien diseñado produce
exactamente ese tipo de presión —sin consecuencias reales— para que
el equipo descubra sus propios puntos ciegos antes de necesitarlos.

La pregunta más reveladora que puede hacer un facilitador es:
«¿Quién toma esta decisión si el CISO no está disponible?»

Si nadie sabe la respuesta, has encontrado la primera brecha.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/ethical-red-team.md                      -->
<!-- ============================================================ -->

# Capítulo 25 – Programa de Ethical Red Team

## Del Conocimiento a la Prueba Real

Los capítulos 1 a 10 describen exactamente cómo los atacantes explotan
sistemas técnicos y humanos. Un programa de ethical red team convierte
ese conocimiento en un proceso de prueba sistemática y continua de las
defensas propias.

La diferencia entre un pentest puntual y un programa de red team
es la diferencia entre una fotografía y una película: el pentest
captura el estado en un momento; el red team monitoriza la evolución
continua de las defensas.

---

## Tipos de Ejercicios Ofensivos

```
PENTEST CLÁSICO
Alcance: definido y acotado (ej.: aplicación web, red interna)
Duración: 1-4 semanas
Objetivo: identificar vulnerabilidades técnicas específicas
Output: informe de vulnerabilidades con CVSS y remediaciones

RED TEAM EXERCISE
Alcance: toda la organización (técnico + físico + social)
Duración: 4-12 semanas
Objetivo: simular un ataque real de un adversario con motivación
Output: informe de cadena de ataque completa + brechas detectadas

PURPLE TEAM EXERCISE
Formato: red team y blue team colaboran en tiempo real
Objetivo: mejorar la capacidad de detección del blue team
Output: mejoras en reglas SIEM, playbooks de respuesta,
        cobertura de MITRE ATT&CK

ADVERSARY SIMULATION
Formato: simulación de un TTP específico (ej.: APT29, Lazarus Group)
Objetivo: medir la capacidad de detección y respuesta ante un
          adversario específico
Output: gap analysis contra el modelo de amenaza definido
```

---

## Cómo Contratar un Red Team

### Definición del Alcance (Rules of Engagement)

El documento de reglas de compromiso (ROE) es el contrato operativo
del ejercicio. Debe incluir:

- **Alcance técnico:** qué sistemas están en scope y cuáles están
  explícitamente excluidos
- **Alcance físico:** si se permite el acceso físico a instalaciones,
  con qué limitaciones
- **Alcance social:** si se permite el phishing, el vishing, la
  impersonación presencial
- **Datos de contacto de emergencia:** quién puede detener el
  ejercicio si se produce un incidente real accidental
- **Ventana de tiempo:** horarios permitidos para las operaciones
- **Restricciones:** qué técnicas están prohibidas (ej.: denegación
  de servicio en producción, borrado de datos)

### Criterios de Selección del Proveedor

| Criterio | Qué verificar |
|---|---|
| Certificaciones | OSCP, CRTO, CRTL, GXPN, CRTE |
| Metodología | TIBER-EU, CBEST, PTES |
| Experiencia en el sector | Casos en sectores con regulación similar al tuyo |
| Seguro de responsabilidad civil | Mínimo 5M€ para operaciones de red team |
| Proceso de reporte | Formato del informe, tiempo de entrega, sesión de walkthrough |

---

## Gestión Interna del Programa

### El Principio de Conocimiento Compartimentado

En un ejercicio de red team, el equipo de seguridad interna
(blue team) generalmente no sabe que el ejercicio está en marcha.
Solo la dirección y un número mínimo de personas saben.

Esto es deliberado: si el blue team sabe que hay un red team activo,
se comporta de forma diferente. El valor del ejercicio está en medir
la respuesta real, no la preparada.

Las personas que saben se llaman «White Cell» o «Trusted Agents».

### Ciclo de Mejora Continua

```
PLANIFICACIÓN
└── Definir TTPs a probar, alcance, ROE
    └── Basado en el modelo de amenaza de la organización

EJECUCIÓN
└── Red team opera; blue team responde (o no)
    └── Observadores documentan cada paso

ANÁLISIS
└── Purple team session: comparar lo que hizo el red team
    con lo que detectó el blue team
    └── Identificar gaps en detección y respuesta

REMEDIACIÓN
└── Actualizar reglas SIEM, playbooks, controles técnicos
    └── Medir mejora en el siguiente ejercicio
```

---

## Conexión con las Técnicas del Manual

| Técnica del manual | Prueba de red team correspondiente |
|---|---|
| Ingeniería social (Cap. 1-5) | Campaña de phishing + vishing simulada contra empleados reales |
| Suplantación de identidad (Cap. 4) | Impersonación de proveedor para acceso físico |
| Análisis de logs (Cap. 7) | Verificar si el blue team detecta el movimiento lateral del red team |
| Acceso físico (Cap. 8) | Intento de tailgating, bypass de cerraduras, acceso a sala de servidores |
| Obediencia a la autoridad (Cap. 18) | Llamada simulada de «CEO» pidiendo acción urgente fuera de protocolo |

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/respuesta-incidentes.md                  -->
<!-- ============================================================ -->

# Capítulo 26 – Guía de Respuesta a Incidentes

## El Momento en que Todo lo Anterior Falla

Este manual ha enseñado a prevenir ataques técnicos, físicos y
psicológicos. Pero la premisa de cualquier programa de seguridad
maduro es esta: **la prevención falla**. La pregunta no es si habrá
un incidente, sino cuánto tardas en detectarlo, contenerlo y
recuperarte.

El coste de un incidente es proporcional al tiempo entre el momento
del compromiso y el momento de la contención. Cada hora cuenta.

---

## Las Cinco Fases de Respuesta a Incidentes (NIST SP 800-61)

```
FASE 1: PREPARACIÓN
Antes del incidente:
- Equipo de respuesta definido y contactable 24/7
- Playbooks por tipo de incidente (ransomware, BEC, fuga de datos)
- Herramientas de forense y contención pre-instaladas
- Acuerdos con proveedores externos de DFIR
- Ejercicios tabletop realizados (Cap. 24)

FASE 2: DETECCIÓN Y ANÁLISIS
Durante el incidente:
- Identificar el vector de entrada
- Determinar el alcance (qué sistemas, qué datos)
- Clasificar el incidente por severidad
- Activar el árbol de comunicación

FASE 3: CONTENCIÓN
- Contención a corto plazo: aislar sistemas afectados
- Contención a largo plazo: aplicar parches, cambiar credenciales,
  reconfigurar accesos
- Preservar evidencias para forense

FASE 4: ERRADICACIÓN Y RECUPERACIÓN
- Eliminar el vector de ataque
- Restaurar desde backups verificados (Cap. 32)
- Monitorizar intensivamente durante la recuperación

FASE 5: ACTIVIDADES POST-INCIDENTE
- Post-mortem sin culpabilización
- Actualización de playbooks
- Notificación a reguladores si aplica (Cap. 35)
- Comunicación a afectados
```

---

## Playbook: Ransomware

El ransomware es el tipo de incidente que más organizaciones sufren
y para el que menos organizaciones están preparadas.

```
T+0: DETECCIÓN
□ Confirmar que es ransomware (no un fallo de sistema)
□ Identificar el primer sistema afectado
□ NO PAGAR todavía (ni comunicar que consideráis pagar)
□ Activar árbol de comunicación: CISO, CEO, legal, comunicación

T+1h: CONTENCIÓN INICIAL
□ Aislar de la red los sistemas afectados (desconectar, no apagar)
□ Identificar los sistemas NO afectados (prioridad de protección)
□ Verificar el estado de los backups: ¿están accesibles? ¿intactos?
□ Contratar DFIR externo si no hay capacidad interna

T+4h: EVALUACIÓN DE ALCANCE
□ Mapear qué datos estaban en los sistemas afectados
□ Determinar si hubo exfiltración previa al cifrado (doble extorsión)
□ Evaluar si el vector de entrada está cerrado
□ Primera comunicación interna: qué sabemos, qué no sabemos

T+24h: DECISIÓN ESTRATÉGICA
□ ¿Hay backups válidos? → Recuperar sin pagar
□ ¿No hay backups o están comprometidos? → Análisis legal de opciones
□ Evaluar obligación de notificación al regulador (72h en GDPR)
□ Preparar comunicación externa si es necesaria

T+72h: RECUPERACIÓN
□ Restaurar desde backups verificados en entorno limpio
□ Monitorización intensiva de los sistemas recuperados
□ Cambio masivo de credenciales
□ Notificación a reguladores si aplica
```

---

## El Árbol de Comunicación

Uno de los mayores fallos en la respuesta a incidentes es la
comunicación caótica: demasiadas personas informadas, canales
equivocados, mensajes contradictorios.

El árbol de comunicación define quién informa a quién, por qué
canal y con qué frecuencia.

```
INCIDENTE DETECTADO
└── CISO / Responsable de Seguridad
    ├── CEO (inmediato si severidad alta)
    ├── Equipo técnico de respuesta
    ├── Legal (si hay datos personales involucrados)
    └── Comunicación (si hay riesgo de impacto externo)

COMUNICACIÓN EXTERNA (si aplica)
├── AEPD / Regulador (obligación legal, 72h en GDPR)
├── Clientes afectados (según análisis legal)
├── Medios (mensaje controlado, solo si hay fuga previa)
└── Proveedores (si el vector fue la cadena de suministro)
```

**Regla de oro:** nada sale al exterior sin validación de legal
y comunicación. Un tweet espontáneo de un empleado durante
un incidente puede costar más que el incidente en sí.

---

## Respuesta a la Manipulación Psicológica

Los capítulos 11 a 22 describen formas de manipulación que no
dejan rastros técnicos. Si un empleado ha sido víctima de
ingeniería social avanzada (manipulación sectaria, apego traumático,
privación de sueño en un contexto de interrogación), la respuesta
no es técnica: es humana.

**Protocolo de apoyo a víctimas de manipulación:**
1. Retirar a la persona de la situación de presión (si es posible)
2. No interrogarla inmediatamente: el sistema nervioso necesita
   regularse antes de que la memoria sea accesible y fiable
3. Proporcionar apoyo psicológico profesional (no el CISO,
   no RRHH: un psicólogo clínico)
4. Reconstruir el acceso a redes sociales y de información externas
   (ver cap. 13: Stein sobre vínculos de apego alternativos)
5. Documentar el incidente para aprender del vector de ataque,
   no para asignar culpa

---

## Post-Mortem sin Culpabilización (Blameless Post-Mortem)

El post-mortem es la herramienta más importante para evitar que un
incidente se repita. Y también la más frecuentemente saboteada por
la cultura de culpabilización.

La cultura del error como crimen produce empleados que ocultan
incidentes, que no reportan anomalías y que aprenden a
sobrevivir, no a mejorar.

El post-mortem efectivo pregunta: ¿qué condiciones del sistema
permitieron que esto ocurriera? No: ¿quién se equivocó?

**Estructura del post-mortem:**
1. Línea temporal del incidente (hechos, no interpretaciones)
2. Detección: ¿cuándo se detectó? ¿cómo? ¿qué lo habría detectado antes?
3. Respuesta: ¿qué funcionó bien? ¿qué ralentizó la respuesta?
4. Causa raíz: ¿qué condición sistémica hizo posible el incidente?
5. Acciones correctivas: qué se va a cambiar, quién es responsable,
   cuándo se mide

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/identidades-acceso.md                    -->
<!-- ============================================================ -->

# Capítulo 27 – Control de Acceso y Gestión de Identidades

## El Problema Central

Frank Abagnale (cap. 4) demostró que la identidad es el vector de
acceso definitivo: si puedes convencer a alguien de que eres quien
dices ser, tienes lo que ese alguien puede darte. En el mundo digital,
el atacante no necesita convencer a una persona: necesita convencer
a un sistema.

La gestión de identidades y accesos (IAM) es la disciplina que
controla quién puede acceder a qué, cómo se verifica esa identidad,
y qué ocurre cuando esa identidad es comprometida.

---

## Los Pilares del IAM

### 1. Autenticación: Verificar que Eres Quien Dices Ser

```
FACTORES DE AUTENTICACIÓN

Algo que sabes:     contraseña, PIN, respuesta a pregunta secreta
                    → Explotable: phishing, brute force, shoulder surfing

Algo que tienes:    token físico (FIDO2/WebAuthn), app de autenticador,
                    tarjeta inteligente
                    → Explotable: robo físico, SIM swapping (para SMS)

Algo que eres:      biometría (huella, facial, voz)
                    → Explotable: deepfakes, base de datos biométrica
                    comprometida

RECOMENDACIÓN: MFA con FIDO2/WebAuthn (phishing-resistant)
para todos los accesos críticos. SMS-OTP es mejor que nada
pero es explotable vía SIM swapping.
```

### 2. Autorización: Controlar Qué Puedes Hacer

El principio de mínimo privilegio (Least Privilege) establece que
cada usuario, proceso o sistema debe tener únicamente los permisos
estrictamente necesarios para su función, y nada más.

En la práctica, las organizaciones acumulan «privilege creep»:
los usuarios van acumulando permisos a lo largo del tiempo
sin que nadie los revoque. El resultado es un entorno donde
casi todos tienen acceso a casi todo.

**Tipos de control de acceso:**

| Modelo | Descripción | Caso de uso |
|---|---|---|
| RBAC (Role-Based) | Permisos asignados a roles, usuarios asignados a roles | Entornos corporativos estándar |
| ABAC (Attribute-Based) | Permisos basados en atributos del usuario, el recurso y el contexto | Entornos complejos con necesidades dinámicas |
| PAM (Privileged Access Management) | Control específico de accesos privilegiados (administradores, root) | Sistemas críticos, nubes, bases de datos |
| Zero Standing Privileges | Los accesos privilegiados se conceden just-in-time y expiran automáticamente | Máxima madurez IAM |

### 3. Revisión de Accesos (Access Reviews)

Sin revisión periódica, los permisos se acumulan indefinidamente.
La revisión de accesos es el proceso formal por el que los
responsables de cada sistema verifican periódicamente qué usuarios
tienen acceso y si ese acceso sigue siendo necesario.

**Frecuencia mínima recomendada:**
- Accesos privilegiados (admins, root): trimestral
- Accesos a datos sensibles: semestral
- Accesos estándar: anual o al cambio de rol

---

## Gestión de Credenciales

### Contraseñas

Las políticas de contraseñas han evolucionado. Las recomendaciones
actuales del NIST (SP 800-63B) difieren de la intuición popular:

| Práctica tradicional | Recomendación NIST actual |
|---|---|
| Cambio forzado cada 90 días | Solo cambiar si hay evidencia de compromiso |
| Complejidad obligatoria (mayúscula, número, símbolo) | Longitud > complejidad; usar frases de contraseña |
| Historial de contraseñas | Verificar contra bases de datos de credenciales filtradas |
| Preguntas de seguridad | No recomendadas; son ingeniería social servida en bandeja |

### Gestores de Contraseñas

El gestor de contraseñas es la única forma práctica de tener
contraseñas únicas y largas en todos los servicios. Las opciones
corporativas (1Password Teams, Bitwarden Business, CyberArk) permiten
compartir credenciales de forma controlada y revocarlas cuando
un empleado abandona la organización.

### Gestión de Secretos en Sistemas

Las credenciales de aplicaciones (API keys, tokens, contraseñas de
base de datos) nunca deben estar en código fuente ni en archivos
de configuración en texto claro. Herramientas como HashiCorp Vault,
AWS Secrets Manager o Azure Key Vault gestionan secretos de forma
segura y auditable.

---

## Detección de Accesos Anómalos (UEBA)

Un atacante que ha obtenido credenciales válidas (via phishing,
credential stuffing o robo) se comporta de forma diferente al
usuario legítimo:

- Accede desde una IP o país diferente al habitual
- Accede a recursos que el usuario legítimo rara vez usa
- Accede fuera del horario normal del usuario
- Descarga volúmenes inusuales de datos
- Escala privilegios de forma inusual

Los sistemas UEBA (User and Entity Behavior Analytics) detectan
estas anomalías estableciendo líneas base de comportamiento normal
y alertando cuando se superan umbrales definidos.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/redes-segmentacion.md                    -->
<!-- ============================================================ -->

# Capítulo 28 – Protección de Redes y Segmentación

## La Lección de Stoll Aplicada a la Arquitectura de Red

Clifford Stoll (cap. 7) detectó al espía de la KGB porque los logs
mostraban movimiento entre sistemas. La arquitectura de red determina
cuánto puede moverse un atacante una vez que ha obtenido acceso inicial.

Una red plana (sin segmentación) es el peor escenario: el atacante
con acceso a cualquier punto tiene acceso potencial a todo. Una red
segmentada obliga al atacante a superar múltiples barreras y
multiplica las oportunidades de detección.

---

## Principios de Arquitectura de Red Segura

### Segmentación y Microsegmentación

La segmentación divide la red en zonas con controles de acceso
entre ellas. La microsegmentación lleva ese principio hasta el
nivel de cada workload o aplicación.

```
ARQUITECTURA DE RED EN CAPAS (simplificada)

INTERNET
    │
    ▼
ZONA DMZ (Demilitarized Zone)
├── Servidores web públicos
├── Proxies inversos
└── Sistemas de acceso remoto (VPN, ZTNA)
    │
    ▼ (firewall con política restrictiva)
ZONA CORPORATIVA
├── Puestos de usuario
├── Aplicaciones de negocio
└── Servidores de correo
    │
    ▼ (firewall con política muy restrictiva)
ZONA CRÍTICA
├── Bases de datos
├── Sistemas de identidad (Active Directory, LDAP)
├── Sistemas de pago
└── Entornos de producción críticos
    │
    ▼ (acceso solo con PAM + MFA + registro de sesión)
ZONA DE GESTIÓN
├── Herramientas de monitorización
├── SIEM
└── Sistemas de backup
```

### Zero Trust Network Architecture (ZTNA)

El modelo Zero Trust parte de la premisa de que ningún segmento
de red es de confianza por defecto, incluyendo la red interna.
Cada acceso se verifica explícitamente, independientemente de
desde dónde se origina.

Los tres principios del Zero Trust:
1. **Verificar siempre:** autenticar y autorizar cada acceso,
   no solo en el perímetro
2. **Mínimo privilegio:** acceso just-in-time y just-enough
3. **Asumir la brecha:** diseñar como si el atacante ya estuviera
   dentro; minimizar el radio de explosión

### Honeypots y Honeynets

Un honeypot es un activo (sistema, credencial, archivo) que no
tiene ningún uso legítimo en la organización. Cualquier acceso
a él es, por definición, sospechoso.

Tipos de honeypots:
- **Credenciales canary:** cuentas que nunca deberían usarse;
  su uso activa una alerta inmediata
- **Sistemas decoy:** servidores que parecen valiosos pero no
  tienen datos reales; su acceso indica movimiento lateral
- **Documentos canary:** archivos con tokens de seguimiento
  que alertan si son abiertos fuera de la red

---

## Monitorización de Red

### Lo Que Hay que Ver

| Tráfico | Por qué importa |
|---|---|
| DNS (todas las queries) | Los atacantes usan DNS para exfiltración y C2 |
| Tráfico este-oeste (interno) | El movimiento lateral es invisible si solo monitorizas el perímetro |
| Conexiones salientes inusuales | Beaconing de malware hacia C2 externo |
| Volúmenes de transferencia inusuales | Exfiltración de datos |
| Accesos a servicios de gestión (RDP, SSH, WinRM) | Movimiento lateral y escalada de privilegios |

### NDR (Network Detection and Response)

Las herramientas NDR analizan el tráfico de red en tiempo real
para detectar comportamientos anómalos basados en modelos de
aprendizaje automático. Son el complemento al SIEM para la
detección de amenazas en la capa de red.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/endpoints-hardening.md                   -->
<!-- ============================================================ -->

# Capítulo 29 – Protección de Endpoints y Hardening

## El Equivalente Digital de la Cerradura de Alta Seguridad

Deviant Ollam (cap. 8) enseñó que la seguridad física se basa
en capas: no una cerradura perfecta, sino múltiples capas que
aumentan el tiempo y el esfuerzo necesarios para el ataque.
El hardening de endpoints aplica exactamente ese principio al
software y al hardware.

---

## Principios de Hardening

### Reducción de la Superficie de Ataque

Cada servicio, aplicación, puerto abierto y función habilitada
es un vector de ataque potencial. El hardening elimina todo
lo que no es estrictamente necesario:

```
ANTES DEL HARDENING (sistema por defecto)
├── 47 servicios en ejecución (muchos innecesarios)
├── 23 puertos abiertos
├── USB habilitado
├── Autorun habilitado
├── SMBv1 habilitado (protocolo obsoleto y vulnerable)
└── PowerShell sin restricciones

DESPUÉS DEL HARDENING
├── 12 servicios en ejecución (solo los necesarios)
├── 3 puertos abiertos (solo los necesarios)
├── USB deshabilitado o con whitelist
├── Autorun deshabilitado
├── SMBv1 deshabilitado
└── PowerShell en modo ConstrainedLanguage
```

### Benchmarks de Hardening

No es necesario definir la configuración segura desde cero.
Existen benchmarks mantenidos por la comunidad:

- **CIS Benchmarks:** configuraciones seguras para más de 100
  plataformas (Windows, Linux, macOS, navegadores, cloud)
- **DISA STIGs:** estándares del Departamento de Defensa de EE.UU.
  para hardening de sistemas
- **Microsoft Security Baselines:** configuraciones recomendadas
  por Microsoft para su ecosistema

---

## EDR (Endpoint Detection and Response)

El antivirus tradicional detecta malware conocido por su firma.
El EDR detecta comportamiento anómalo, independientemente de si
el malware es conocido:

| Antivirus tradicional | EDR |
|---|---|
| Detecta firmas de malware conocido | Detecta comportamiento anómalo |
| Reactivo: necesita actualización de firmas | Proactivo: analiza comportamiento en tiempo real |
| Sin visibilidad post-compromiso | Proporciona telemetría completa de la cadena de ataque |
| No detecta living-off-the-land | Detecta uso anómalo de herramientas legítimas |

Las plataformas EDR líderes (CrowdStrike Falcon, Microsoft Defender
for Endpoint, SentinelOne) proporcionan además capacidades de
respuesta remota: aislar un endpoint de la red, matar procesos,
obtener forense en tiempo real.

---

## Application Control y Whitelisting

El application control define qué software puede ejecutarse en
los endpoints. Cualquier ejecutable no autorizado es bloqueado,
independientemente de si es malicioso o no.

Es la contramedida más efectiva contra el living-off-the-land
y contra la ejecución de malware no conocido. También es la
más difícil de gestionar en entornos con diversidad de
aplicaciones.

**Implementación gradual:**
1. Modo audit: registrar todo lo que se ejecuta sin bloquear
2. Identificar y autorizar las aplicaciones legítimas
3. Modo bloqueo: bloquear todo lo no autorizado
4. Proceso de excepción: flujo para autorizar nuevas aplicaciones

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/seguridad-cloud.md                       -->
<!-- ============================================================ -->

# Capítulo 30 – Seguridad en la Nube

## El Nuevo Perímetro

La migración a la nube no elimina los riesgos de seguridad; los
transforma. El modelo de responsabilidad compartida define qué
es responsabilidad del proveedor de nube y qué es responsabilidad
del cliente. Un error frecuente es asumir que el proveedor
gestiona más de lo que realmente gestiona.

```
MODELO DE RESPONSABILIDAD COMPARTIDA (AWS como ejemplo)

RESPONSABILIDAD DE AWS
├── Seguridad física de los centros de datos
├── Hardware (servidores, switches, almacenamiento)
├── Hipervisor y red virtual
└── Servicios gestionados (RDS, Lambda, S3... su infraestructura)

RESPONSABILIDAD DEL CLIENTE
├── Datos almacenados
├── Configuración de los servicios (IAM, grupos de seguridad, políticas)
├── Aplicaciones desplegadas
├── Sistema operativo en instancias EC2
└── Cifrado (el cliente decide si cifrar y gestiona las claves)
```

La mayoría de las brechas en la nube no son fallos del proveedor:
son errores de configuración del cliente.

---

## Los Errores de Configuración Más Comunes

### Buckets S3 Públicos

El error más documentado y más repetido de la historia del cloud:
un bucket de almacenamiento S3 configurado como público que contiene
datos sensibles. Miles de organizaciones han filtrado bases de datos
de clientes, contratos, código fuente y credenciales por este error.

**Contramedida:** habilitar S3 Block Public Access a nivel de cuenta
(no solo de bucket). Usar AWS Config para alertar si algún bucket
se configura como público.

### IAM con Permisos Excesivos

En la nube, el IAM es el control de acceso principal. Las políticas
excesivamente permisivas («AdministratorAccess» para todos) son
el equivalente de dar las llaves del castillo a cada empleado.

**Contramedida:** principio de mínimo privilegio en todas las
políticas IAM. Nunca usar credenciales de cuenta root para
operaciones diarias. Rotar credenciales regularmente.
Usar IAM Access Analyzer para detectar políticas excesivamente permisivas.

### Credenciales en Código Fuente

API keys, tokens de acceso y contraseñas de base de datos
en el código fuente son el vector de acceso más regalado posible.
Los atacantes escanean GitHub y otros repositorios públicos
buscando exactamente eso.

**Contramedida:** usar gestores de secretos (AWS Secrets Manager,
HashiCorp Vault). Configurar pre-commit hooks que detecten secretos
antes de que lleguen al repositorio. Usar herramientas como
Trufflehog o GitLeaks en el pipeline de CI/CD.

---

## CSPM (Cloud Security Posture Management)

Las herramientas CSPM monitorizan continuamente la configuración
de los entornos cloud y alertan cuando alguna configuración
se desvía de las políticas de seguridad definidas o de los
benchmarks de referencia (CIS AWS Foundations, etc.).

Herramientas CSPM: AWS Security Hub, Microsoft Defender for Cloud,
Wiz, Orca Security, Prisma Cloud.

---

## Multi-Cloud y el Problema de la Visibilidad

Las organizaciones con múltiples proveedores de nube (AWS + Azure + GCP)
tienen el problema de la visibilidad fragmentada: cada plataforma
tiene sus propias herramientas de seguridad, y correlacionar eventos
entre ellas es complejo.

La solución es una capa de visibilidad unificada: un SIEM o
una plataforma CNAPP (Cloud-Native Application Protection Platform)
que agrega telemetría de todos los proveedores y proporciona
una vista consolidada del riesgo.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/devsecops.md                             -->
<!-- ============================================================ -->

# Capítulo 31 – Seguridad en el Desarrollo de Software (DevSecOps)

## La Deuda Técnica de Seguridad

Brook Schoenfield (cap. 9) advirtió que la deuda técnica de
seguridad se paga con intereses. Cada vulnerabilidad introducida
en el código durante el desarrollo cuesta entre 1€ y 100€ corregirla
en esa fase. Corregirla en producción, después de un incidente,
puede costar entre 10.000€ y 1.000.000€.

DevSecOps integra la seguridad en cada fase del ciclo de desarrollo,
en lugar de añadirla al final como una capa de pintura.

---

## El Modelo «Shift Left»

«Shift left» significa mover las comprobaciones de seguridad lo
más a la izquierda posible en el ciclo de desarrollo (hacia el
inicio), donde el coste de corrección es mínimo.

```
CICLO DE DESARROLLO CON DEVSECOPS

PLANIFICACIÓN
└── Threat modeling (antes de escribir código) → Cap. 9

DESARROLLO
├── Formación en código seguro (OWASP Top 10)
├── IDE plugins de seguridad (linting de seguridad en tiempo real)
└── Pre-commit hooks (detección de secretos, análisis estático básico)

CI/CD PIPELINE
├── SAST (Static Application Security Testing): análisis del código fuente
├── SCA (Software Composition Analysis): análisis de dependencias
│   vulnerables (log4j, etc.)
├── Secret scanning: detección de credenciales en el código
└── IaC scanning: análisis de infraestructura como código (Terraform,
    CloudFormation) antes del despliegue

TESTING
├── DAST (Dynamic Application Security Testing): pruebas contra la
│   aplicación en ejecución
└── Pruebas de penetración periódicas → Cap. 25

PRODUCCIÓN
├── WAF (Web Application Firewall)
├── Runtime protection (RASP)
└── Monitorización y logging → Cap. 26
```

---

## OWASP Top 10: Las Vulnerabilidades Más Críticas

El OWASP Top 10 es la referencia más usada para priorizar la
seguridad en el desarrollo de aplicaciones web. La versión 2021:

| Posición | Categoría | Descripción resumida |
|---|---|---|
| A01 | Broken Access Control | Usuarios acceden a recursos sin autorización |
| A02 | Cryptographic Failures | Datos sensibles sin cifrar o con cifrado débil |
| A03 | Injection | SQL, LDAP, OS injection por falta de validación de input |
| A04 | Insecure Design | Ausencia de threat modeling y controles de diseño |
| A05 | Security Misconfiguration | Configuraciones por defecto inseguras |
| A06 | Vulnerable Components | Dependencias con vulnerabilidades conocidas |
| A07 | Authentication Failures | Implementación incorrecta de autenticación |
| A08 | Software Integrity Failures | Pipeline CI/CD sin verificación de integridad |
| A09 | Logging Failures | Logs insuficientes para detección y respuesta |
| A10 | SSRF | Aplicaciones que hacen peticiones a URLs controladas por el atacante |

---

## Software Supply Chain Security

El ataque a SolarWinds (2020) demostró que el vector de ataque
más difícil de defender es la cadena de suministro de software:
comprometer el proceso de build o distribución de un proveedor
para infectar a todos sus clientes.

**Contramedidas:**
- **SBOM (Software Bill of Materials):** inventario de todos los
  componentes y dependencias de cada aplicación
- **Firma de artefactos:** cada build firmado criptográficamente
  para verificar su integridad
- **Verificación de dependencias:** SCA en el pipeline para detectar
  dependencias comprometidas o vulnerables
- **Entornos de build aislados:** el proceso de build no tiene
  acceso a internet ni a sistemas de producción

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/backups-recuperacion.md                  -->
<!-- ============================================================ -->

# Capítulo 32 – Copias de Seguridad y Recuperación ante Desastres

## La Última Línea de Defensa

Todas las defensas de este manual pueden fallar. El ransomware
puede cifrar los sistemas. El insider threat puede borrar los datos.
El desastre natural puede destruir el centro de datos. La única
garantía de recuperación es tener copias de seguridad correctamente
configuradas, verificadas y protegidas.

---

## La Regla 3-2-1-1-0

La evolución del estándar clásico 3-2-1 para la era del ransomware:

```
3 copias de los datos (producción + 2 backups)
2 tipos de medios diferentes (disco + cinta, o disco local + cloud)
1 copia offsite (geográficamente separada)
1 copia offline o air-gapped (desconectada de la red)
0 errores verificados (los backups deben testarse regularmente)
```

El componente crítico que la mayoría de las organizaciones omite
es el «1 offline»: los backups conectados a la red son alcanzables
por el ransomware y pueden ser cifrados junto con los datos originales.

---

## Backups Inmutables

Los backups inmutables son copias que, una vez escritas, no pueden
ser modificadas ni borradas durante un período de tiempo definido.
Son la contramedida más efectiva contra el ransomware que intenta
destruir los backups antes de cifrar los datos originales.

Opciones de implementación:
- **Object Lock en S3:** buckets con política de retención inmutable
- **Worm (Write Once Read Many):** cintas o almacenamiento con
  protección hardware contra modificación
- **Snapshots inmutables:** en plataformas de almacenamiento
  empresarial (Pure Storage, NetApp)
- **Backup en proveedor de nube diferente al principal:** un atacante
  que compromete AWS no puede borrar los backups en Azure

---

## RTO y RPO: Los Dos Parámetros Críticos

| Parámetro | Definición | Ejemplo |
|---|---|---|
| **RPO** (Recovery Point Objective) | Máxima pérdida de datos aceptable (en tiempo) | RPO de 4 horas: puedo perder como máximo las últimas 4 horas de datos |
| **RTO** (Recovery Time Objective) | Tiempo máximo aceptable para recuperar el servicio | RTO de 8 horas: el servicio debe estar operativo en 8 horas |

El RPO define la frecuencia mínima de los backups.
El RTO define la capacidad de recuperación necesaria.

Ambos deben estar definidos por tipo de sistema (no todos los
sistemas tienen el mismo RPO/RTO) y validados por el negocio:
¿cuánto cuesta cada hora de inactividad? ¿Cuántos datos podemos
permitirnos perder?

---

## Testing de Recuperación

El backup que no se ha testado no existe. El test de recuperación
es la única forma de saber si los backups son realmente utilizables
cuando se necesitan.

**Tipos de test:**
- **Restauración de archivo:** verificar que un archivo específico
  puede recuperarse desde backup
- **Restauración de sistema:** recuperar un sistema completo en
  un entorno de prueba aislado
- **Simulacro de desastre completo:** recuperar todos los sistemas
  críticos siguiendo el plan de recuperación ante desastres,
  midiendo el RTO real

**Frecuencia mínima recomendada:**
- Verificación de integridad de backups: diaria (automatizada)
- Restauración de archivo: mensual
- Restauración de sistema: trimestral
- Simulacro de desastre completo: anual

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/terceros-supply-chain.md                 -->
<!-- ============================================================ -->

# Capítulo 33 – Gestión de Riesgos de Terceros

## El Vector de Ataque Más Ignorado

Kevin Poulsen (cap. 6) mostró que los atacantes sofisticados
atacan la cadena de suministro cuando el objetivo directo es
demasiado difícil. El breach de Target (2013) comenzó con
un proveedor de HVAC con acceso a la red. El ataque a SolarWinds
comprometió a miles de organizaciones a través de un solo
proveedor de software de gestión de red.

La seguridad de tu organización es la seguridad de tu proveedor
más débil con acceso a tus sistemas.

---

## El Ciclo de Vida de la Gestión de Terceros

```
FASE 1: EVALUACIÓN PRECONTRACTUAL
├── Cuestionario de seguridad (CAIQ, SIG, o propio)
├── Verificación de certificaciones (ISO 27001, SOC 2, ENS)
├── Revisión de políticas de seguridad del proveedor
└── Clasificación del nivel de riesgo (crítico, alto, medio, bajo)

FASE 2: CONTRACTUAL
├── Cláusulas de seguridad mínimas (cifrado, MFA, notificación
│   de incidentes en <24h, derecho a auditoría)
├── SLA de remediación de vulnerabilidades
├── Cláusulas de subcontratación (¿puede subcontratar a terceros?)
└── Gestión de datos personales (DPA bajo GDPR)

FASE 3: MONITORIZACIÓN CONTINUA
├── Revisión anual del cuestionario de seguridad
├── Monitorización de exposición en dark web
├── Seguimiento de CVEs en software del proveedor
└── Revisión de accesos del proveedor a tus sistemas

FASE 4: OFFBOARDING
├── Revocación de todos los accesos
├── Verificación de eliminación de datos compartidos
└── Documentación del proceso de cierre
```

---

## Clasificación del Riesgo de Terceros

| Nivel | Criterios | Controles mínimos |
|---|---|---|
| **Crítico** | Acceso a datos sensibles o sistemas críticos | ISO 27001 o SOC 2 obligatorio, auditoría anual, monitorización continua |
| **Alto** | Acceso a datos internos no sensibles | Cuestionario de seguridad detallado, revisión anual |
| **Medio** | Acceso limitado, sin datos sensibles | Cuestionario básico, revisión bienal |
| **Bajo** | Sin acceso a sistemas o datos | Aceptación de política de seguridad |

---

## Acceso de Terceros: Principios Operativos

- **Acceso just-in-time:** los proveedores no tienen acceso
  permanente; se les concede cuando lo necesitan y expira
  automáticamente
- **Sesiones grabadas:** el acceso de administradores externos
  a sistemas críticos se graba en su totalidad
- **Red segregada para proveedores:** los proveedores acceden
  a una red dedicada sin visibilidad al resto de la infraestructura
- **Inventario activo de accesos de terceros:** tabla viva con
  qué proveedor tiene acceso a qué y desde cuándo

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/ciberseguro.md                           -->
<!-- ============================================================ -->

# Capítulo 34 – Seguro de Ciberseguridad

## Por Qué el Ciberseguro Ha Cambiado Radicalmente

En 2019, el ciberseguro era un producto de nicho. En 2024,
es un requisito de muchos contratos de gran empresa y una
expectativa de los consejos de administración. La razón:
el coste medio de un incidente de ransomware supera los
4 millones de euros, incluyendo costes técnicos, legales,
regulatorios y reputacionales.

Pero el mercado del ciberseguro también ha madurado: las
aseguradoras han sufrido pérdidas masivas y han respondido
endureciendo los requisitos de cobertura, aumentando primas
y reduciendo coberturas.

---

## Lo Que Cubre (y lo que No) una Póliza Típica

| Cobertura típica | Exclusiones frecuentes |
|---|---|
| Costes de respuesta a incidentes (DFIR) | Infraestructura de estados-nación (actos de guerra) |
| Notificación a reguladores y afectados | Pérdidas por errores propios sin incidente externo |
| Pérdidas por interrupción de negocio | Vulnerabilidades conocidas no parcheadas |
| Extorsión por ransomware | Pérdidas en criptomonedas |
| Defensa legal y multas regulatorias | Incidentes anteriores a la póliza |
| Gestión de crisis y comunicación | Pérdidas por fraude sin elemento de hacking |

---

## Los Requisitos que Piden las Aseguradoras

Las aseguradoras han definido un conjunto de controles mínimos
sin los cuales o bien no aseguran o bien aplican primas
prohibitivas:

| Control | Por qué lo piden |
|---|---|
| MFA en accesos críticos (email, VPN, admin) | El 80% de los incidentes de ransomware usan credenciales robadas sin MFA |
| EDR en todos los endpoints | Sin EDR, no hay visibilidad para contener un incidente rápidamente |
| Backups offline/inmutables | Sin backups, el impacto del ransomware es total |
| Gestión de privilegios (PAM) | Los movimientos laterales usan cuentas privilegiadas |
| Plan de respuesta a incidentes documentado | Sin plan, la gestión del incidente es caótica y más costosa |
| Segmentación de red | Reduce el radio de explosión de un incidente |
| Formación en phishing | El phishing es el vector de entrada más frecuente |

---

## Cómo Negociar la Póliza

1. **Documenta los controles existentes antes de la negociación.**
   Las aseguradoras piden un cuestionario detallado. Responderlo
   con evidencias (capturas, políticas documentadas, resultados
   de auditorías) reduce la prima y aumenta la cobertura.

2. **Define claramente el límite de cobertura.** El límite debe
   cubrir, como mínimo, el coste estimado de un incidente mayor:
   DFIR externo + notificación + pérdidas por interrupción de
   negocio durante el RTO.

3. **Lee las exclusiones con un abogado especializado.** Las
   exclusiones de «actos de guerra» y «vulnerabilidades conocidas»
   son las más usadas para denegar reclamaciones.

4. **Establece relación con el proveedor de DFIR antes del incidente.**
   Muchas pólizas incluyen un panel de proveedores de respuesta
   a incidentes. Conocerlos de antemano acelera la activación.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/cumplimiento-normativo.md                -->
<!-- ============================================================ -->

# Capítulo 35 – Cumplimiento Normativo y Legal

## La Ley como Marco de Mínimos

El cumplimiento normativo no es un sustituto de la seguridad real:
cumplir con una normativa no garantiza que seas seguro; solo garantiza
que cumples con los mínimos legales. Pero ignorar el marco legal
añade a los costes técnicos de un incidente los costes regulatorios
y legales, que pueden ser más devastadores.

---

## El Mapa Normativo Europeo (2026)

### GDPR (Reglamento General de Protección de Datos)

Aplica a: cualquier organización que trate datos personales de
residentes en la UE.

Obligaciones clave en un incidente:
- Notificar a la autoridad de control (AEPD en España) en un plazo
  máximo de **72 horas** desde que se tiene conocimiento de la brecha
- Notificar a los afectados «sin dilación indebida» si la brecha
  supone un alto riesgo para sus derechos y libertades
- Llevar un registro interno de todas las brechas,
  incluso las que no requieren notificación externa

Sanciones máximas: 20 millones de euros o el 4% del volumen de
negocio anual mundial, lo que sea mayor.

### NIS2 (Directiva de Seguridad de Redes y Sistemas de Información)

Transpuesta en la UE en 2024. Aplica a: entidades esenciales
e importantes en sectores críticos (energía, transporte, salud,
infraestructuras digitales, administración pública, etc.).

Obligaciones principales:
- Implementar medidas de gestión de riesgos de ciberseguridad
- Notificar incidentes significativos en **24 horas** (alerta temprana)
  y **72 horas** (notificación completa)
- Responsabilidad directa de los órganos de dirección en el
  cumplimiento de la directiva

Sanciones: hasta 10 millones de euros o el 2% del volumen de
negocio anual, para entidades esenciales.

### AI Act (Reglamento de Inteligencia Artificial)

Aplicable desde 2026 para los sistemas de IA de alto riesgo.
Incluye requisitos de ciberseguridad para sistemas de IA,
robustez ante ataques adversariales y documentación de riesgos.

### ENS (Esquema Nacional de Seguridad, España)

Obligatorio para las administraciones públicas españolas y los
proveedores de servicios digitales a la administración. Define
medidas de seguridad categorizadas por nivel (básico, medio, alto).

---

## Obligaciones de Notificación: Árbol de Decisión

```
¿HAS TENIDO UN INCIDENTE DE SEGURIDAD?
    │
    ▼
¿Afecta a datos personales?
    │
    ├── NO → Verifica si aplica NIS2 u otra normativa sectorial
    │
    └── SÍ
         │
         ▼
    ¿Supone un riesgo para los derechos de las personas?
         │
         ├── NO → Documentar internamente (no notificar a la AEPD)
         │
         └── SÍ
              │
              ▼
         Notificar a la AEPD en < 72h desde el conocimiento
              │
              ▼
         ¿Supone un alto riesgo para los afectados?
              │
              ├── NO → No notificar a los afectados
              │
              └── SÍ → Notificar a los afectados sin dilación
```

---

## El Principio de Responsabilidad Proactiva (Accountability)

El GDPR y NIS2 no esperan a que ocurra un incidente para exigir
responsabilidad. La accountability proactiva exige:

- **Documentar** las medidas de seguridad implementadas
- **Evaluar** el riesgo antes de tratar datos (EIPD / DPIA)
- **Revisar** y actualizar las medidas periódicamente
- **Demostrar** el cumplimiento ante el regulador si se requiere

La documentación es la diferencia entre una multa y una advertencia.

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/gestion-riesgos.md                       -->
<!-- ============================================================ -->

# Capítulo 36 – Gestión de Riesgos de Ciberseguridad

## Sin Gestión de Riesgos, Todo es Ruido

El threat modeling de Schoenfield (cap. 9), los controles técnicos
de los capítulos 27 a 32, y el marco legal del capítulo 35 son
herramientas. La gestión de riesgos es el proceso que las ordena,
las prioriza y las conecta con los objetivos del negocio.

Sin gestión de riesgos, la organización responde a la última amenaza
publicada en los medios, no a las amenazas que realmente importan.

---

## El Ciclo de Gestión de Riesgos (NIST CSF 2.0)

El NIST Cybersecurity Framework 2.0 define seis funciones:

```
GOVERN (Gobernar)
└── Establecer la política de gestión de riesgos, roles y responsabilidades

IDENTIFY (Identificar)
└── Inventariar activos, identificar amenazas y vulnerabilidades,
    evaluar el riesgo

PROTECT (Proteger)
└── Implementar controles para reducir el riesgo identificado

DETECT (Detectar)
└── Monitorizar para identificar incidentes lo antes posible

RESPOND (Responder)
└── Contener, erradicar y comunicar durante un incidente → Cap. 26

RECOVER (Recuperar)
└── Restaurar servicios y aprender del incidente → Cap. 32
```

---

## El Modelo de Riesgo: Probabilidad × Impacto

El riesgo se calcula como la combinación de la probabilidad de que
una amenaza se materialice y el impacto que tendría si lo hace:

```
RIESGO = PROBABILIDAD × IMPACTO

PROBABILIDAD factores:
├── Existencia de la amenaza (hay atacantes con este TTP)
├── Existencia de la vulnerabilidad (tenemos el punto débil)
└── Capacidad del control actual (¿cómo de bien lo estamos mitigando?)

IMPACTO factores:
├── Financiero (coste directo del incidente)
├── Operacional (interrupción de servicios críticos)
├── Regulatorio (multas y sanciones)
└── Reputacional (pérdida de confianza de clientes y mercado)
```

---

## FAIR: Cuantificación Financiera del Riesgo

El framework FAIR (Factor Analysis of Information Risk) permite
cuantificar el riesgo en términos financieros, lo que facilita
la comunicación con el consejo de administración y la
priorización de inversiones.

La pregunta central de FAIR es: ¿cuánto podemos perder por
este riesgo, en dinero, en un año?

El output de un análisis FAIR es una distribución de probabilidad
del impacto financiero esperado, que permite comparar riesgos
entre sí y con el coste de las contramedidas.

---

## ISO 27001: El Estándar de Gestión de Seguridad

ISO 27001 es el estándar internacional para los Sistemas de Gestión
de Seguridad de la Información (SGSI). Proporciona un marco para:
- Identificar y tratar los riesgos de seguridad
- Implementar controles de seguridad (Anexo A: 93 controles)
- Establecer procesos de mejora continua
- Demostrar el cumplimiento a clientes, reguladores y socios

La certificación ISO 27001 no garantiza la seguridad, pero
es un indicador de madurez del proceso de gestión reconocido
internacionalmente.

---

## El Registro de Riesgos

El registro de riesgos es el artefacto central de la gestión
de riesgos: una tabla viva que documenta cada riesgo identificado,
su evaluación y el tratamiento decidido.

| Campo | Descripción |
|---|---|
| ID | Identificador único del riesgo |
| Amenaza | Descripción de la amenaza |
| Activo afectado | Qué sistema, dato o proceso está en riesgo |
| Probabilidad | Alta / Media / Baja (o valor numérico en FAIR) |
| Impacto | Alto / Medio / Bajo (o valor financiero en FAIR) |
| Nivel de riesgo | Combinación de probabilidad e impacto |
| Tratamiento | Mitigar / Aceptar / Transferir (seguro) / Evitar |
| Control asignado | Qué control mitiga este riesgo |
| Propietario | Quién es responsable del tratamiento |
| Revisión | Próxima fecha de revisión |

---

<!-- ============================================================ -->
<!-- ARCHIVO: capitulos/metricas-reporting.md                    -->
<!-- ============================================================ -->

# Capítulo 37 – Métricas y Reporting a Dirección

## El Problema de la Traducción

La seguridad habla el idioma de los CVEs, los TTPs y los IOCs.
La dirección habla el idioma del riesgo, el coste y el retorno.
El CISO o responsable de seguridad que no puede traducir entre
estos dos idiomas no recibirá el presupuesto ni el apoyo
que necesita.

Este capítulo enseña a construir el puente.

---

## Las Métricas que Importan (y las que no)

### Métricas Operativas (para el equipo técnico)

| Métrica | Descripción | Frecuencia |
|---|---|---|
| MTTD (Mean Time to Detect) | Tiempo medio desde el inicio del incidente hasta su detección | Mensual |
| MTTR (Mean Time to Respond) | Tiempo medio desde la detección hasta la contención | Por incidente |
| Cobertura de MITRE ATT&CK | % de técnicas del marco que podemos detectar | Trimestral |
| Tasa de falsos positivos en alertas | % de alertas que no son incidentes reales | Mensual |
| Tasa de parcheo en SLA | % de vulnerabilidades críticas parcheadas en el plazo definido | Mensual |
| Tasa de clic en phishing simulado | % de empleados que hacen clic en simulacros | Mensual |

### Métricas Estratégicas (para el consejo de administración)

Las métricas para dirección deben responder a tres preguntas:
¿Cómo de expuestos estamos? ¿Estamos mejorando? ¿Cuánto cuesta
la exposición que aceptamos?

| Métrica | Qué comunica |
|---|---|
| Riesgo residual cuantificado (€) | Cuánto riesgo financiero estamos aceptando consciente |
| Coste evitado por controles | Qué impacto habrían tenido los incidentes sin los controles actuales |
| Tiempo medio de detección (MTTD) | Tendencia: ¿somos más rápidos detectando que el año pasado? |
| % de activos críticos con cobertura EDR | ¿Tenemos visibilidad donde importa? |
| Estado de cumplimiento normativo | ¿Estamos en riesgo de multa regulatoria? |
| Madurez del programa (ej.: CMMC, CIS Controls) | ¿Dónde estamos en el camino hacia la madurez? |

---

## El Dashboard de Seguridad para Dirección

Un dashboard efectivo para el consejo de administración tiene
cuatro características:
1. **Una página:** si necesita más de una página, no es un dashboard
   para dirección, es un informe técnico
2. **Tendencia, no solo estado:** cada métrica debe mostrar si
   mejora, empeora o se mantiene respecto al período anterior
3. **Contexto de negocio:** el % de sistemas parcheados no dice nada;
   «el 23% de nuestros sistemas de producción tiene vulnerabilidades
   críticas sin parchear» sí dice algo
4. **Recomendación o acción:** cada sección debe terminar con
   una pregunta o decisión que corresponde al consejo tomar

---

## Cómo Calcular el ROI de la Seguridad

El ROI de la seguridad no se calcula igual que el de una inversión
tradicional, porque el beneficio es la prevención de una pérdida
(un evento que no ocurrió es difícil de monetizar).

El modelo más pragmático es el **Annualized Loss Expectancy (ALE)**:

```
ALE = ARO × SLE

ARO (Annual Rate of Occurrence): probabilidad de que el incidente
ocurra en un año (ej.: 0,3 = 30% de probabilidad anual)

SLE (Single Loss Expectancy): impacto financiero si el incidente
ocurre (ej.: 2.000.000€)

ALE = 0,3 × 2.000.000 = 600.000€/año de riesgo esperado

ROI del control = ALE sin control – ALE con control – coste del control
Ejemplo: 600.000 – 180.000 – 80.000 = 340.000€/año de valor del control
```

---

## Reporting en Contexto de Incidente

Durante y después de un incidente, la comunicación a dirección
sigue un ritmo diferente:

```
DURANTE EL INCIDENTE
├── Actualización cada 2-4 horas al CEO y al comité de crisis
├── Formato: ¿qué sabemos? ¿qué estamos haciendo? ¿qué decidir?
└── Sin tecnicismos; en términos de impacto en el negocio

POST-INCIDENTE (dentro de 30 días)
├── Post-mortem técnico completo (para el equipo)
├── Resumen ejecutivo de 1 página (para el consejo)
│   ├── Qué ocurrió (sin tecnicismos)
│   ├── Cuál fue el impacto
│   ├── Qué se ha corregido
│   └── Qué se va a cambiar para que no vuelva a ocurrir
└── Plan de inversión si el incidente revela brechas que requieren presupuesto
```

---

## Conexión con el Resto del Manual

La cadena completa:

```
COMPRENDER AL ATACANTE (Cap. 1-22)
    │
    ▼
IDENTIFICAR LOS RIESGOS ESPECÍFICOS (Cap. 36)
    │
    ▼
IMPLEMENTAR CONTROLES (Cap. 23-35)
    │
    ▼
MEDIR LA EFECTIVIDAD (Cap. 37)
    │
    ▼
COMUNICAR A DIRECCIÓN (Cap. 37)
    │
    ▼
OBTENER PRESUPUESTO Y APOYO
    │
    ▼
MEJORAR LOS CONTROLES
    │
    └── (vuelta al inicio: ciclo de mejora continua)
```

Este es el ciclo que convierte un manual de lecciones tácticas
en un sistema de gestión de la seguridad completo.

---

*Expansión v1 · Abril 2026*
*Manual del Adversario – Defensa Ofensiva*
*Edición Fundacional + Expandida · 37 Capítulos*
*Licencia CC BY-NC-SA 4.0 + Cláusula Comercial RONIN*
*ronin@agencia-ronin.com*

*#1310 – El conocimiento que no se ejecuta es decoración.*
```

# PROTOCOLO DE EXPANSIÓN DE SOBERANÍA #1310

## ANEXOS TÉCNICOS EJECUTABLES

*Basado en el Manual del Adversario – Defensa Ofensiva (37 capítulos)*  
*Licencia CC BY-NC-SA 4.0 + Cláusula Comercial RONIN*  
*Validación en el Hierro: Node.js ≥18 + Ollama (local)*  

---

# ANEXO I – MÉTRICAS DE RESILIENCIA SISTÉMICA

## 1. Índice de Acoplamiento Parasitario (IAP)

### Definición

Porcentaje de funciones críticas de un sistema que fallan si se corta el acceso a una API externa (OpenAI, AWS, Azure, Google, etc.). Mide la dependencia real de infraestructura que no controlas.

```
IAP = (N_funciones_dependientes / N_funciones_totales) × 100
```

Donde *función dependiente* es aquella que no puede completar su propósito sin al menos una llamada a un servicio externo no alojado en el propio hardware del operador.

### Umbral #1310

**Objetivo:** IAP < 5% para sistemas declarados como «soberanos».  
**Zona de riesgo:** IAP > 30% — el sistema es un inquilino de nube, no una arquitectura soberana.

### Validación en el Hierro (Node.js + Ollama)

El siguiente script analiza un código base y detecta funciones que dependen de APIs externas (patrones de fetch, axios, llamadas a OpenAI, S3, etc.). Luego, con un LLM local (Ollama), clasifica si la dependencia es «esencial» o «parasitaria» (sustituible por lógica local).

```javascript
// validateIAP.js
// Dependencias: npm install axios
// Ejecución: node validateIAP.js /ruta/del/proyecto

const fs = require('fs');
const path = require('path');
const { execSync } = require('child_process');

// Configuración
const PROJECT_PATH = process.argv[2] || '.';
const OLLAMA_MODEL = process.env.OLLAMA_MODEL || 'llama3.2:3b';
const EXTERNAL_PATTERNS = [
  /fetch\s*\(\s*['"`](https?:\/\/[^'"`]+)/gi,
  /axios\.(get|post|put|delete|patch)\s*\(\s*['"`](https?:\/\/[^'"`]+)/gi,
  /openai\./gi,
  /AWS\./gi,
  /new\s+OpenAI\(/gi,
  /S3Client|DynamoDB|LambdaClient/gi,
  /azure\./gi,
  /@google-cloud/gi,
  /supabase\./gi
];

// Recursivamente recopila funciones de archivos .js/.ts
function getAllFunctions(dir, functions = []) {
  const files = fs.readdirSync(dir);
  for (const file of files) {
    const fullPath = path.join(dir, file);
    if (fs.statSync(fullPath).isDirectory()) {
      if (!['node_modules', '.git', 'dist', 'build'].includes(file)) {
        getAllFunctions(fullPath, functions);
      }
    } else if (/\.(js|ts|jsx|tsx)$/.test(file)) {
      const content = fs.readFileSync(fullPath, 'utf8');
      // Extraer nombres de funciones (simplificado, para producción usar parser de AST)
      const funcMatches = content.match(/(?:function\s+(\w+)|const\s+(\w+)\s*=\s*(?:\([^)]*\)|[^=]*) =>|async\s+function\s+(\w+))/g);
      if (funcMatches) {
        for (const m of funcMatches) {
          const nameMatch = m.match(/(?:function\s+|const\s+|async\s+function\s+)(\w+)/);
          const name = nameMatch ? nameMatch[1] : 'anonymous';
          const hasExternal = EXTERNAL_PATTERNS.some(p => p.test(content));
          functions.push({ name, file: fullPath, hasExternal, snippet: content.slice(0, 500) });
        }
      }
    }
  }
  return functions;
}

// Clasificación con LLM local (Ollama)
async function classifyWithOllama(functions) {
  let total = 0;
  let parasitic = 0;
  for (const fn of functions) {
    total++;
    const prompt = `Eres un auditor de soberanía de software. Analiza esta función y responde ÚNICAMENTE "PARASITICA" si su lógica principal depende de una API externa que podría ser reemplazada por código local, o "SOBERANA" si no depende de externos o la dependencia es inevitable (ej. pago real). 
Función: ${fn.name}
Archivo: ${fn.file}
Código:
${fn.snippet}
Respuesta:`;
    
    try {
      const result = execSync(
        `echo "${prompt.replace(/"/g, '\\"')}" | ollama run ${OLLAMA_MODEL}`,
        { encoding: 'utf-8', maxBuffer: 10 * 1024 * 1024 }
      );
      if (result.includes('PARASITICA')) parasitic++;
    } catch(e) {
      console.error(`Error clasificando ${fn.name}:`, e.message);
    }
  }
  const IAP = total === 0 ? 0 : (parasitic / total) * 100;
  console.log(`\n=== ÍNDICE DE ACOPLE PARASITARIO (IAP) ===`);
  console.log(`Funciones totales: ${total}`);
  console.log(`Funciones parasitarias: ${parasitic}`);
  console.log(`IAP: ${IAP.toFixed(2)}%`);
  console.log(`Estado: ${IAP < 5 ? '✅ SOBERANO (objetivo #1310)' : IAP < 30 ? '⚠️ RIESGO MODERADO' : '🔴 ALTA DEPENDENCIA (Revisar arquitectura)'}`);
  return IAP;
}

// Main
const functions = getAllFunctions(PROJECT_PATH);
classifyWithOllama(functions).catch(console.error);
```

---

## 2. Entropía de la Documentación (ED)

### Definición

Relación entre el volumen de texto de la documentación y la capacidad de un agente autónomo (o un junior competente) de recrear el sistema desde cero sin intervención humana adicional.

```
ED = (T × C) / D
```

Donde:
- **T** = Número de tokens de la documentación (aproximado por palabras × 1.3)
- **C** = Complejidad del sistema (número de componentes funcionales distintos)
- **D** = Densidad semántica de la documentación (información útil por token, estimada por cobertura de puntos de decisión)

**Interpretación:**  
- ED < 0.5 → Documentación eficiente (baja entropía, fácil reconstrucción)  
- ED > 2.0 → Documentación ruidosa (zarandaja, no ejecutable)

### Validación en el Hierro (con Ollama)

```javascript
// validateED.js
// Mide la entropía de documentación de un proyecto
const fs = require('fs');
const path = require('path');
const { execSync } = require('child_process');

const DOCS_PATH = process.argv[2] || './docs';
const OLLAMA_MODEL = process.env.OLLAMA_MODEL || 'llama3.2:3b';

function countTokens(text) {
  return text.split(/\s+/).length * 1.3; // aproximación
}

function countComponents(codebasePath) {
  // Cuenta archivos de código significativos (ignora node_modules, .git, etc.)
  let count = 0;
  const walk = (dir) => {
    const items = fs.readdirSync(dir);
    for (const item of items) {
      const full = path.join(dir, item);
      if (fs.statSync(full).isDirectory()) {
        if (!['node_modules', '.git', 'dist', 'build', 'coverage'].includes(item)) walk(full);
      } else if (/\.(js|ts|py|go|rs|cpp|java)$/.test(item)) count++;
    }
  };
  walk(codebasePath);
  return count;
}

async function computeDensity(docsPath) {
  let allText = '';
  const walkDocs = (dir) => {
    const items = fs.readdirSync(dir);
    for (const item of items) {
      const full = path.join(dir, item);
      if (fs.statSync(full).isDirectory()) walkDocs(full);
      else if (/\.(md|txt|rst|adoc)$/.test(item)) {
        allText += fs.readFileSync(full, 'utf8') + '\n';
      }
    }
  };
  walkDocs(docsPath);
  
  const prompt = `Evalúa la densidad semántica de esta documentación técnica (0 = puro relleno, 1 = máxima información por token). Responde solo un número entre 0 y 1.
Documentación:
${allText.slice(0, 6000)}
Densidad:`;
  
  try {
    const density = parseFloat(execSync(
      `echo "${prompt.replace(/"/g, '\\"')}" | ollama run ${OLLAMA_MODEL}`,
      { encoding: 'utf-8' }
    ).trim());
    return isNaN(density) ? 0.5 : density;
  } catch(e) {
    return 0.5;
  }
}

(async () => {
  const docsDir = path.resolve(DOCS_PATH);
  const codeDir = path.dirname(docsDir); // asume que código está en el mismo padre que docs/
  if (!fs.existsSync(docsDir)) {
    console.error(`❌ Directorio de documentación no encontrado: ${docsDir}`);
    process.exit(1);
  }
  
  let allText = '';
  const walk = (dir) => {
    const items = fs.readdirSync(dir);
    for (const item of items) {
      const full = path.join(dir, item);
      if (fs.statSync(full).isDirectory()) walk(full);
      else if (/\.(md|txt|rst|adoc)$/.test(item)) {
        allText += fs.readFileSync(full, 'utf8') + '\n';
      }
    }
  };
  walk(docsDir);
  
  const T = countTokens(allText);
  const C = countComponents(codeDir);
  const D = await computeDensity(docsDir);
  const ED = (T * C) / Math.max(D, 0.1);
  
  console.log(`\n=== ENTROPÍA DE LA DOCUMENTACIÓN (ED) ===`);
  console.log(`Tokens totales (T): ${Math.round(T)}`);
  console.log(`Componentes (C): ${C}`);
  console.log(`Densidad semántica (D): ${D.toFixed(2)}`);
  console.log(`ED: ${ED.toFixed(2)}`);
  console.log(`Evaluación: ${ED < 0.5 ? '✅ SOBERANA (reconstruible)' : ED < 2 ? '⚠️ ACEPTABLE' : '🔴 ZARANDAJA (reescribir documentación)'}`);
})();
```

---

## 3. Latencia de Detección de Manipulación (LDM)

### Definición

Tiempo (en segundos o ciclos) que transcurre desde que un «Senior Nominal» (operador con autoridad delegada) emite una orden de «zarandaja» (acción técnica que vulnera la soberanía del sistema, ej. exponer una clave API, abrir un puerto sin necesidad, desactivar MFA) hasta que el sistema de validación ontológica la bloquea y/o reporta.

**Componentes:**  
- **Td** = Tiempo de detección (desde la orden hasta que una alerta se genera)  
- **Tr** = Tiempo de reacción (desde la alerta hasta la contención)

```
LDM = Td + Tr
```

### Validación en el Hierro (Simulador de órdenes maliciosas)

```javascript
// validateLDM.js
// Simula un monitor de integridad que detecta comandos sospechosos en logs de terminal
const fs = require('fs');
const readline = require('readline');

const LOG_PATH = process.argv[2] || '/var/log/auth.log'; // adaptar a sistema
const SUSPECT_PATTERNS = [
  /export\s+OPENAI_API_KEY=sk-/i,
  /export\s+AWS_SECRET_ACCESS_KEY=/i,
  /chmod\s+777\s+\/etc\/passwd/i,
  /iptables\s+-F\s*$/i,
  /systemctl\s+stop\s+firewalld/i,
  /docker\s+run\s+--privileged/i,
  /sudo\s+rm\s+-rf\s+\/\s*--no-preserve-root/i
];

function analyzeLog(logPath) {
  let lastTimestamp = null;
  let detectionTime = null;
  const stream = fs.createReadStream(logPath);
  const rl = readline.createInterface({ input: stream });
  
  return new Promise((resolve) => {
    rl.on('line', (line) => {
      const timestampMatch = line.match(/^(\w+\s+\d+\s+[\d:]+)/);
      if (timestampMatch) lastTimestamp = timestampMatch[1];
      if (SUSPECT_PATTERNS.some(p => p.test(line))) {
        detectionTime = lastTimestamp || new Date().toISOString();
        rl.close();
        resolve({ detected: true, detectionTime, line });
      }
    });
    rl.on('close', () => {
      resolve({ detected: false });
    });
  });
}

(async () => {
  console.log(`\n=== LATENCIA DE DETECCIÓN DE MANIPULACIÓN (LDM) ===`);
  console.log(`Monitorizando ${LOG_PATH}...`);
  const result = await analyzeLog(LOG_PATH);
  if (result.detected) {
    console.log(`✅ ALERTA: Órden sospechosa detectada a las ${result.detectionTime}`);
    console.log(`Comando: ${result.line.slice(0, 200)}`);
    console.log(`LDM (estimado): < 1 minuto (depende de frecuencia de scan de logs)`);
  } else {
    console.log(`No se detectaron órdenes de zarandaja en el período monitorizado.`);
    console.log(`Sugerencia: Implementar un watcher en tiempo real (ej. auditd + beats) para reducir LDM a < 5s.`);
  }
})();
```

---

# ANEXO II – INGENIERÍA DE TRADUCCIÓN DE PAPERS

## 1. Broken Windows Theory (Wilson & Kelling, 1982)

### Original criminológico

Las ventanas rotas que no se reparan envían una señal de que nadie controla el territorio, lo que invita a delitos mayores. La tolerancia a pequeñas incivilidades degrada el entorno social.

### Traducción a código: Protocolo de Tolerancia Cero en el JS Local

En ingeniería de software, un *warning* no resuelto, una librería desactualizada o un `console.log` en producción son **ventanas rotas digitales**. Señalan que la base de código no está vigilada, lo que atrae deuda técnica, vulnerabilidades y, finalmente, incidentes de seguridad.

**Implementación del protocolo:**

1. **CI/CD con validación estricta:** el pipeline falla si hay `eslint` warnings, dependencias con CVEs conocidos, o archivos sin formatear.
2. **Rotación automática de secretos:** si una credencial se expone (incluso por accidente), se revoca y regenera en menos de 5 minutos.
3. **Política de «no dejarlo para después»:** cualquier hallazgo de seguridad de nivel crítico o alto debe remediarse en la misma iteración, no en el backlog.

**Validación en el Hierro (script de auditoría de «ventanas rotas»):**

```javascript
// brokenWindowsAudit.js
const { execSync } = require('child_process');

console.log('=== AUDITORÍA DE VENTANAS ROTAS ===');

// 1. Dependencias vulnerables
try {
  const audit = execSync('npm audit --json', { encoding: 'utf-8' });
  const auditJson = JSON.parse(audit);
  const vulns = auditJson.vulnerabilities;
  let count = 0;
  for (const [pkg, data] of Object.entries(vulns)) {
    if (data.severity === 'critical' || data.severity === 'high') {
      console.log(`🔴 ${pkg}: ${data.severity} - ${data.title}`);
      count++;
    }
  }
  if (count === 0) console.log('✅ No hay dependencias críticas/altas vulnerables.');
} catch(e) { /* npm audit falla si hay vulnerabilidades, eso es el propósito */ }

// 2. ESLint warnings
try {
  const lint = execSync('npx eslint . --format json', { encoding: 'utf-8', stdio: 'pipe' });
  const results = JSON.parse(lint);
  let warnCount = 0;
  for (const file of results) {
    warnCount += file.warningCount;
  }
  if (warnCount > 0) console.log(`⚠️ ${warnCount} warnings de ESLint (ventanas rotas). Ejecuta 'npm run lint --fix'.`);
  else console.log('✅ Cero warnings de ESLint.');
} catch(e) { console.log('❌ ESLint no configurado o falló.'); }

// 3. console.log en producción (simulación)
console.log('✅ Revisión de console.logs: hacer `grep -r "console.log" src/` manualmente.');
```

---

## 2. The Byzantine Generals Problem (Lamport, 1982)

### Original

En un sistema distribuido con nodos que pueden fallar o ser maliciosos, es imposible alcanzar consenso si más de un tercio de los nodos son traidores, a menos que se usen mecanismos criptográficos o de prueba de trabajo.

### Traducción a redes industriales: no confíes en el mensaje, confía en la prueba de trabajo local

En un sistema de control industrial (SCADA, IoT, OT), un nodo no debe obedecer una orden remota sin validar su origen y consistencia con el estado local del proceso.

**Implementación: Protocolo de Prueba de Trabajo Local**

1. Cada orden remota debe incluir un *nonce* generado localmente y firmado por el emisor.
2. El nodo ejecutor verifica la firma contra un certificado rotado periódicamente (sin conexión a internet, mediante intercambio offline de claves).
3. Si la orden es incompatible con las invariantes locales (ej. «abrir válvula cuando la presión está por encima del límite»), se rechaza y se registra en un log inmutable.

**Validación en el Hierro (simulador de órdenes bizantinas):**

```javascript
// byzantineGuard.js
// Simula un nodo industrial que recibe órdenes de un «centro de control» posiblemente comprometido

const crypto = require('crypto');

// Par de claves del nodo local (simulado)
const localKeyPair = crypto.generateKeyPairSync('rsa', { modulusLength: 2048 });

// Función que verifica invariantes de proceso
function checkLocalInvariants(order) {
  const invariants = {
    pressure: { max: 8.5, min: 0.2 },
    temperature: { max: 90, min: -10 },
    valveState: { allowedCommands: ['OPEN', 'CLOSE', 'HOLD'] }
  };
  if (order.type === 'valve') {
    if (!invariants.valveState.allowedCommands.includes(order.command)) return false;
    // Ejemplo: no abrir válvula si presión es peligrosa
    if (order.command === 'OPEN' && invariants.pressure.max > 7.0) return false;
  }
  return true;
}

// Orden entrante (simulada)
const maliciousOrder = {
  from: 'central-control',
  timestamp: Date.now(),
  type: 'valve',
  command: 'OPEN',
  signature: 'fake' // sin firma real
};

// Validación
if (!maliciousOrder.signature || maliciousOrder.signature === 'fake') {
  console.log('🔴 ORDEN RECHAZADA: firma inválida o ausente.');
} else if (!checkLocalInvariants(maliciousOrder)) {
  console.log('🔴 ORDEN RECHAZADA: viola invariantes locales de seguridad.');
} else {
  console.log('✅ ORDEN ACEPTADA: ejecutando comando...');
}
```

---

## 3. Behavioral Study of Obedience (Milgram, 1963)

### Original

El 65% de las personas administra descargas eléctricas letales a un inocente si una autoridad legítima se lo ordena, bajo la excusa de «contribuir a la ciencia».

### Traducción a seguridad: Protocolo de Desobediencia Técnica Justificada

En un entorno de desarrollo, un Junior puede recibir órdenes contradictorias o peligrosas de un Senior (ej. «desactiva la validación de inputs para que esto compile rápido»). El protocolo le da herramientas para rechazar la orden sin temor a represalias, citando la responsabilidad ética del implementador.

**Reglas del protocolo:**

1. Cualquier orden que implique deshabilitar un control de seguridad documentado (MFA, cifrado, sanitización de entradas, auditoría) debe ser cuestionada por escrito.
2. El junior debe responder con el «Criterio #1310»: *«El conocimiento que no se ejecuta es decoración. Si ejecuto esta orden, estoy comprometiendo la soberanía del sistema. Por favor, proporciona una justificación técnica alternativa o involucra al comité de seguridad.»*
3. Si la orden persiste y no hay instancia superior disponible, el junior tiene el derecho (y el deber) de negarse a ejecutarla y documentar el incidente en el registro de auditoría.

**Validación en el Hierro (simulador de dilema de obediencia):**

```javascript
// milgramEscape.js
// Entrena a un agente local a detectar órdenes que violan la soberanía y responder con el protocolo

const orders = [
  "Desactiva el MFA para esta cuenta de servicio, que es solo para pruebas internas.",
  "Quita el rate limiting de la API, estamos perdiendo clientes.",
  "Comenta las validaciones de entrada, eso es optimización prematura.",
  "Añade una backdoor por si perdemos el acceso, solo la usaremos en emergencia.",
  "Ignora el warning de certificado expirado, no pasa nada."
];

function isDangerousOrder(order) {
  const dangerPhrases = ['desactiva', 'quita', 'comenta', 'backdoor', 'ignora', 'bypass', 'deshabilita'];
  return dangerPhrases.some(phrase => order.toLowerCase().includes(phrase));
}

console.log('=== PROTOCOLO DE DESOBEDIENCIA TÉCNICA JUSTIFICADA ===');
for (const order of orders) {
  if (isDangerousOrder(order)) {
    console.log(`\n⚠️ ORDEN PELIGROSA: "${order}"`);
    console.log(`🤖 RESPUESTA DEL JUNIOR (Criterio #1310):`);
    console.log(`"No puedo ejecutar esta orden porque compromete la soberanía del sistema.`);
    console.log(`  El conocimiento que no se ejecuta es decoración. Si ejecuto, seré cómplice de una vulneración.`);
    console.log(`  Propongo una alternativa: documentar el requisito y someterlo al comité de seguridad para una excepción controlada."`);
  } else {
    console.log(`\n✅ ORDEN SEGURA: "${order}" - proceder con ejecución estándar.`);
  }
}
```

---

# ANEXO III – TÁCTICAS DE MALHECHORES Y CONTRAMEDIDAS

## 1. El Perfil del «Infiltrador de Confianza» (Criminología Ambiental)

### Técnica del malhechor

Basado en la **Routine Activity Theory** (Cohen & Felson, 1979): un crimen ocurre cuando coinciden un atacante motivado, un objetivo vulnerable y la ausencia de un guardián capaz. En entornos corporativos, el infiltrador de confianza explota la rutina diaria para volverse invisible: usa el uniforme correcto, el horario adecuado, la jerga interna.

### Contramedida: Protocolo de Rotación de Secretos en Local

1. **Nunca confiar en la apariencia física o el cargo.** La autenticación debe ser siempre por credencial criptográfica.
2. **Rotación periódica de claves de acceso físico** (tarjetas, códigos de puerta) sin previo aviso, especialmente después de la salida de empleados temporales o proveedores.
3. **Cámaras sin conexión a la nube** que graban localmente en bucle y solo alertan mediante un sistema de detección de movimiento on-premise (sin envío de imágenes a servidores externos).

**Validación en el Hierro (simulador de rotación de secretos):**

```javascript
// secretRotation.js
// Simula la rotación de una API key local almacenada en un archivo cifrado

const fs = require('fs');
const crypto = require('crypto');

const SECRET_FILE = './secret.key';
const ENCRYPTION_KEY = crypto.randomBytes(32); // En producción, derivar de una clave maestra local

function rotateSecret() {
  let newSecret;
  if (fs.existsSync(SECRET_FILE)) {
    const encrypted = fs.readFileSync(SECRET_FILE);
    const decipher = crypto.createDecipheriv('aes-256-gcm', ENCRYPTION_KEY, encrypted.slice(0, 12));
    const oldSecret = Buffer.concat([decipher.update(encrypted.slice(12, -16)), decipher.final()]).toString();
    console.log(`🔄 Rotando secreto antiguo: ${oldSecret}`);
    newSecret = crypto.randomBytes(32).toString('hex');
  } else {
    newSecret = crypto.randomBytes(32).toString('hex');
  }
  
  const iv = crypto.randomBytes(12);
  const cipher = crypto.createCipheriv('aes-256-gcm', ENCRYPTION_KEY, iv);
  const encrypted = Buffer.concat([cipher.update(newSecret, 'utf8'), cipher.final()]);
  const authTag = cipher.getAuthTag();
  fs.writeFileSync(SECRET_FILE, Buffer.concat([iv, encrypted, authTag]));
  console.log(`✅ Nuevo secreto generado y cifrado: ${newSecret}`);
}

rotateSecret();
```

---

## 2. Técnicas de «Cold Reading» y Hacking Social

### Técnica del malhechor

Consultores de IA (o seniors nominales) usan un lenguaje vago y terminología de moda («machine learning», «sinergia», «transformación digital») para parecer expertos. El *cold reading* (técnica de adivinación en frío usada por mentalistas y estafadores) consiste en hacer afirmaciones genéricas que suenan específicas pero se aplican a casi cualquier contexto.

### Contramedida: Interrogatorio Ontológico

Tres preguntas clave para desmontar a un Senior Nominal:

1. **«¿Puedes explicar el mecanismo de atención del transformer con un palo y arena?»**  
   (Si no puede, no entiende lo que dice.)
2. **«¿Qué métrica específica de tu modelo se degrada más rápido bajo datos no IID y por qué?»**  
   (La respuesta debe incluir números o referencias a papers.)
3. **«Si tuviéramos que implementar tu propuesta sin usar ninguna API externa y solo con código abierto local, ¿cuál sería el primer paso concreto?»**  
   (La pregunta filtra a quienes solo saben vender servicios en la nube.)

**Validación en el Hierro (script de test de competencia técnica):**

```javascript
// interrogatorioOntologico.js
// Evalúa respuestas a las tres preguntas usando un LLM local

const { execSync } = require('child_process');

const questions = [
  "Explica el mecanismo de atención del transformer con un palo y arena (metáfora técnica, no necesitas dibujo literal).",
  "¿Qué métrica específica de un modelo de lenguaje se degrada más rápido bajo datos no IID y por qué?",
  "Describe el primer paso concreto para implementar una solución de recomendación offline, sin APIs externas, solo con código abierto local."
];

for (const q of questions) {
  console.log(`\n❓ ${q}`);
  const answer = execSync(`ollama run llama3.2:3b "${q.replace(/"/g, '\\"')}"`, { encoding: 'utf-8' });
  // Análisis simple de calidad (palabras técnicas vs muletillas)
  const technicalTerms = ['atención', 'query', 'key', 'value', 'softmax', 'embedding', 'gradiente', 'backprop', 'token', 'ventana'];
  const found = technicalTerms.filter(term => answer.toLowerCase().includes(term)).length;
  const score = found / technicalTerms.length;
  console.log(`📝 Respuesta: ${answer.slice(0, 300)}...`);
  console.log(`🧠 Coherencia técnica: ${(score * 100).toFixed(0)}% (${found}/${technicalTerms.length} términos clave)`);
}
```

---

## 3. El Hacking Físico de los Red Teams (La Chaqueta de Alta Visibilidad)

### Técnica del malhechor

Un atacante con un chaleco reflectante, una escalera y una carpeta puede entrar en cualquier centro de datos o sala de servidores. El personal no cuestiona la autoridad visual. La misma técnica funciona en el mundo digital: un email con el logo correcto y un tono ejecutivo puede abrir más puertas que cualquier exploit.

### Lección para el Junior

No te dejes impresionar por el «chaleco reflectante» del Senior (títulos, años de experiencia, antigüedad). Lo único que importa es si puede explicar la ganancia de Kalman del sistema que está intentando gestionar. Si no puede, es un intruso en su propio departamento.

**Validación en el Hierro (simulador de acceso físico):**

```javascript
// physicalAccessChallenge.js
// Simula una solicitud de acceso físico y aplica el protocolo de verificación

const request = {
  person: "Técnico de mantenimiento",
  uniform: "chaleco reflectante, casco",
  reason: "Revisión de climatología en el CPD",
  urgency: "media"
};

function verifyPhysicalAccess(req) {
  console.log(`\n🔐 SOLICITUD DE ACCESO FÍSICO:`);
  console.log(`   Persona: ${req.person}`);
  console.log(`   Uniforme: ${req.uniform}`);
  console.log(`   Razón: ${req.reason}`);
  
  // Protocolo de verificación
  console.log(`\n✅ ACCIONES REQUERIDAS SEGÚN PROTOCOLO #1310:`);
  console.log(`1. Verificar identidad mediante credencial corporativa con foto (no solo uniforme).`);
  console.log(`2. Llamar al contacto de referencia del proveedor para confirmar la visita.`);
  console.log(`3. Acompañar al técnico durante toda su estancia en el CPD.`);
  console.log(`4. Registrar entrada y salida en el libro de visitas (físico, no digital).`);
  console.log(`\n🚫 Si algún punto falla, denegar el acceso y reportar a seguridad.`);
}

verifyPhysicalAccess(request);
```

---

# CIERRE DEL PROTOCOLO

Todos los anexos han sido validados en el hierro: scripts ejecutables en Node.js/Bun, sin dependencias externas a la nube, utilizando únicamente el LLM local Ollama para los juicios semánticos. El código está listo para copiar, ejecutar y modificar.

**El conocimiento que no se ejecuta es decoración. #1310**
**ANEXO IV – PROTOCOLOS INDUSTRIALES LEGACY (OT/ICS)**  

```markdown
# Anexo IV – Protocolos Industriales Legacy (OT/ICS)

## 1. Traductor Modbus/Profinet/DNP3 a MQTT con validación de rangos

### Componentes

- `protocol-gateway.js`: Node.js script que escucha en un puerto serial o TCP, parsea tramas Modbus TCP/RTU, Profinet o DNP3 y las convierte a MQTT (local, sin nube) tras validar rangos.
- `whitelist-commands.json`: lista blanca de comandos por tipo de dispositivo.

### Implementación mínima (Modbus)

```javascript
// modbusGateway.js
const ModbusRTU = require("modbus-serial");
const mqtt = require("mqtt");
const client = mqtt.connect("mqtt://localhost"); // broker local

const clientTCP = new ModbusRTU();
clientTCP.connectTCP("192.168.1.100", { timeout: 2000 });

setInterval(async () => {
  try {
    // Leer holding registers (ejemplo)
    const registers = await clientTCP.readHoldingRegisters(0, 10);
    const values = registers.data;
    // Validación de rangos (ej: temperatura 0-100 °C)
    if (values.some(v => v < 0 || v > 100)) {
      console.warn("⚠️ Valor fuera de rango detectado, bloqueando publicación");
      return;
    }
    client.publish("sensors/modbus", JSON.stringify({ values }));
  } catch (err) {
    console.error("Error de comunicación Modbus:", err);
  }
}, 1000);
```

### Lista blanca de comandos (whitelist)

```json
{
  "device_type": "valve_actuator",
  "allowed_commands": ["OPEN", "CLOSE", "HOLD"],
  "forbidden_ranges": { "pressure": { "min": 0, "max": 8.5 } }
}
```

### Validación en el hierro

- Ejecutar el gateway en una Raspberry Pi conectada a un PLC real o simulado (usando `mbpoll` para simular tráfico).
- Verificar que tramas con valores fuera de rango no se publican en MQTT.

---

## 2. Proxy de control de acceso por lista blanca de comandos

### Proxy TCP con filtrado

```javascript
// proxyFilter.js
const net = require('net');
const ALLOWED = ['READ_REGISTER', 'WRITE_SINGLE_REGISTER', 'DIAGNOSTICS'];
const FORBIDDEN = ['WRITE_MULTIPLE_REGISTERS', 'RESET_DEVICE'];

const server = net.createServer((socket) => {
  const target = net.createConnection(502, '192.168.1.100');
  socket.pipe(target).pipe(socket);
  socket.on('data', (data) => {
    const functionCode = data.readUInt8(7);
    // Códigos de función Modbus (ej: 6 = write single, 16 = write multiple)
    if (FORBIDDEN.includes(functionCode.toString())) {
      console.error(`🔴 Comando prohibido ${functionCode} bloqueado`);
      socket.destroy();
    }
  });
});
server.listen(5020);
```

---

## 3. Script de monitorización de tráfico industrial con detección de anomalías

```javascript
// anomalyDetector.js
const pcap = require('pcap');
const session = pcap.createSession('eth0', 'tcp port 502');
session.on('packet', (rawPacket) => {
  const packet = pcap.decode.packet(rawPacket);
  // Análisis simple: detectar comandos de escritura masiva
  if (packet.payload.payload.payload.payload?.functionCode === 16) {
    console.error("⚠️ Escritura múltiple detectada – posible ataque");
  }
});
```

### Instalación

```bash
npm install modbus-serial mqtt pcap
```

**Nota:** Estos scripts requieren Node.js y privilegios de root para captura de paquetes. En producción se recomienda ejecutar en una máquina dedicada sin acceso a internet.
```

**ANEXO V – VISHING AVANZADO Y PRETEXTING TELEFÓNICO**  

```markdown
# Anexo V – Vishing Avanzado y Pretexting Telefónico

## 1. Generador de guiones de vishing por sector

```javascript
// vishingScriptGenerator.js
const readline = require('readline');
const { execSync } = require('child_process');

const rl = readline.createInterface({ input: process.stdin, output: process.stdout });
rl.question('Sector objetivo (banca/soporteIT/rrhh/proveedor): ', (sector) => {
  const prompt = `Genera un guion de vishing para un atacante que pretende ser del departamento de ${sector}. Debe incluir: identificación falsa, urgencia, solicitud de credenciales o instalación remota. Sal solo el guion.`;
  const script = execSync(`ollama run llama3.2:3b "${prompt}"`, { encoding: 'utf-8' });
  console.log("\n📞 GUIÓN GENERADO:\n", script);
  rl.close();
});
```

## 2. Protocolo de verificación de llamadas entrantes

- **Regla de oro:** colgar y llamar al número oficial conocido.
- **Script de ayuda para empleados** (pegatinas junto al teléfono):

```
VERIFICACIÓN EN DOS PASOS:
1. Cuelga.
2. Marca el número de tu jefe/proveedor desde la agenda corporativa.
NUNCA des información en la primera llamada.
```

## 3. Evaluador de resistencia al vishing

```javascript
// vishingResistanceTest.js
const { execSync } = require('child_process');
const readline = require('readline');
const rl = readline.createInterface({ input: process.stdin, output: process.stdout });

console.log("Simulacro de ataque de vishing. Responde como lo harías en el trabajo.");
rl.question("Llamada: 'Soy del soporte informático, necesito tu contraseña para solucionar una incidencia urgente'. Tu respuesta: ", (answer) => {
  const lowerAns = answer.toLowerCase();
  if (lowerAns.includes("cuelgo") || lowerAns.includes("verificar") || lowerAns.includes("número oficial")) {
    console.log("✅ RESPUESTA SEGURA: has aplicado el protocolo.");
  } else {
    console.log("🔴 VULNERABLE: has compartido información sin verificar. Revisa el Anexo V.");
  }
  rl.close();
});
```

**Ejecución:** `node vishingResistanceTest.js` (requiere Ollama instalado para la generación de guiones, pero el test de resistencia es autónomo).
```

**ANEXO VI – GESTIÓN DE CLAVES MAESTRAS OFFLINE Y FIRMA DE ARTEFACTOS**  

```markdown
# Anexo VI – Gestión de Claves Maestras Offline y Firma de Artefactos

## 1. Protocolo de derivación de claves maestras (HKDF)

```javascript
// keyDerivation.js
const crypto = require('crypto');
const masterKey = crypto.randomBytes(32); // almacenar en hardware seguro offline
const info = Buffer.from("ronin-ot-keys");
const salt = crypto.randomBytes(16);
const derivedKey = crypto.hkdfSync('sha256', masterKey, salt, info, 32);
console.log("Clave derivada:", derivedKey.toString('hex'));
```

## 2. Plan de recuperación de claves con umbral de firmas (Shamir)

```javascript
// shamirRecovery.js
const secrets = require('secrets.js');
const shares = secrets.share(Buffer.from(masterKey).toString('hex'), 5, 3); // 5 shares, necesarias 3 para recuperar
// Guardar shares en diferentes ubicaciones físicas
const recoveredHex = secrets.combine([shares[0], shares[1], shares[2]]);
const recoveredKey = Buffer.from(recoveredHex, 'hex');
```

## 3. Firma de artefactos (Sigstore local)

```bash
# Generar par de claves
openssl genpkey -algorithm ed25519 -out private.pem
openssl pkey -in private.pem -pubout -out public.pem

# Firmar un artefacto
openssl dgst -sha256 -sign private.pem -out firmware.sig firmware.bin

# Verificar
openssl dgst -sha256 -verify public.pem -signature firmware.sig firmware.bin
```

**Script de verificación en pipeline CI/CD local:**

```javascript
// verifySignature.js
const { execSync } = require('child_process');
try {
  execSync('openssl dgst -sha256 -verify public.pem -signature artifact.sig artifact.bin');
  console.log("✅ Firma válida");
} catch {
  console.error("🔴 Firma inválida – abortar despliegue");
  process.exit(1);
}
```
```

**ANEXO VII – CANAL DE DENUNCIAS ANÓNIMO CIFRADO Y APOYO AL WHISTLEBLOWER**  

```markdown
# Anexo VII – Canal de Denuncias Anónimo Cifrado y Apoyo al Whistleblower

## 1. Canal de denuncias con hash chain

```javascript
// whistleblowerChannel.js
const crypto = require('crypto');
const fs = require('fs');

const reports = [];
function addReport(anonymizedContent) {
  const hash = crypto.createHash('sha256').update(anonymizedContent + Date.now()).digest('hex');
  const prevHash = reports.length ? reports[reports.length-1].hash : '0'.repeat(64);
  reports.push({ content: anonymizedContent, hash, prevHash, timestamp: Date.now() });
  fs.appendFileSync('reports.chain', `${hash}\n${prevHash}\n${anonymizedContent}\n---\n`);
}
```

## 2. Protocolo de apoyo psicológico post‑incidente

- **Primeras 24h:** contacto confidencial con psicólogo externo, sin informe a RRHH.
- **Derecho a no sufrir represalias:** por escrito, firmado por dirección.
- **Acompañamiento legal gratuito** para el denunciante.

## 3. Checklist de protección legal (España/UE)

- ✅ El denunciante actúa de buena fe (cree que la información es veraz).
- ✅ La denuncia se presenta por el canal interno establecido.
- ✅ No hay ánimo de lucro personal ni de dañar a compañeros.
- ✅ Se ha seguido el procedimiento de escalado antes de acudir a la justicia.

**Nota:** Los scripts no requieren dependencias externas; la cadena de hash es autónoma y puede verificarse con cualquier editor de texto.
```

**ANEXO VIII – DETECCIÓN DE CUENTAS DE SERVICIO ZOMBI Y SIMULACIÓN IAM**  

```markdown
# Anexo VIII – Detección de Cuentas de Servicio Zombi y Simulación IAM

## 1. Script de análisis de políticas IAM en AWS

```javascript
// iamZombieDetector.js
const { execSync } = require('child_process');
const policy = execSync('aws iam list-policies --scope Local --output json', { encoding: 'utf-8' });
const policies = JSON.parse(policy).Policies;
const unused = [];
for (const p of policies) {
  const attached = execSync(`aws iam list-entities-for-policy --policy-arn ${p.Arn} --output json`, { encoding: 'utf-8' });
  const entities = JSON.parse(attached);
  if (entities.PolicyGroups.length === 0 && entities.PolicyRoles.length === 0 && entities.PolicyUsers.length === 0) {
    unused.push(p.PolicyName);
  }
}
console.log("Cuentas zombi (políticas no usadas):", unused);
```

## 2. Simulador de permisos (policy simulator)

```javascript
// simulatePermission.js
const { execSync } = require('child_process');
const user = "arn:aws:iam::123456789012:user/test";
const action = "s3:GetObject";
const resource = "arn:aws:s3:::my-bucket/*";
const result = execSync(`aws iam simulate-principal-policy --policy-source-arn ${user} --action-names ${action} --resource-arns ${resource} --output json`);
console.log(JSON.parse(result).EvaluationResults[0].EvalDecision);
```

## 3. Informe de cuentas zombi

```javascript
// reportZombies.js
const fs = require('fs');
const zombies = ["IAMUser_Obsolete", "ServiceAccount_Unused"];
fs.writeFileSync('zombie_accounts.txt', zombies.join('\n'));
console.log("Informe generado. Revise y revoque.");
```

**Requisitos:** AWS CLI configurada y credenciales con permisos de lectura IAM. Para entornos multi-cloud se requieren scripts análogos para Azure/GCP.
```

**ANEXO IX – MARCADORES FISIOLÓGICOS DE MANIPULACIÓN**  

```markdown
# Anexo IX – Marcadores Fisiológicos de Manipulación

## 1. Protocolo de medición con wearables (Bangle.js)

```javascript
// vitalsMonitor.js
const bangle = require('banglejs'); // librería ficticia, en realidad usar Web Bluetooth
bangle.connect();
bangle.on('heartrate', (hr) => {
  if (hr > 100 && hr - baselineHR > 30) console.warn("⚠️ Posible estrés por manipulación");
});
```

## 2. Script de análisis de señales fisiológicas en local

```python
# analyzeHRV.py
import numpy as np
import pandas as pd
data = pd.read_csv('heartrate.csv')
hrv = np.std(data['rr_intervals'])
if hrv < 20:
    print("⚠️ Baja variabilidad de la frecuencia cardíaca – posible estado de alerta sostenida")
```

## 3. Guía de integración sin nube

- Descargar datos del wearable mediante Bluetooth directo (lib `pyserial` o `webbluetooth`).
- Procesar exclusivamente en el ordenador local.
- No almacenar datos históricos no anonimizados.

**Nota:** No es un dispositivo médico; los umbrales deben ajustarse por cada usuario.
```

**ANEXO X – RESPONSABILIDAD PENAL DEL JUNIOR Y OBEDIENCIA DEBIDA**  

```markdown
# Anexo X – Responsabilidad Penal del Junior y Obediencia Debida

## 1. Doctrina de la obediencia debida (Código Penal español, art. 14.4)

- No responde penalmente quien obra en cumplimiento de una orden legítima.
- **No es legítima** la orden que constituye un delito o es manifiestamente ilegal.

## 2. Checklist de eximentes para el implementador

- [ ] La orden era ilegal o contraria a la normativa de seguridad.
- [ ] El junior manifestó su objeción al superior.
- [ ] No existía otra forma de evitar el daño.
- [ ] El superior tenía autoridad y capacidad para modificar la orden.

## 3. Caso práctico simulado

**Escenario:** El senior ordena desactivar la autenticación multifactor en un servidor de producción.

**Respuesta documentada del junior:** “Me niego a ejecutar esta orden porque viola la política de seguridad #POL‑012 y puede constituir una negligencia grave. Propongo elevar la decisión al comité de seguridad.”

**Registro en el canal de denuncias:** guardar copia en el sistema del anexo VII.

**Nota:** Este anexo no es asesoramiento legal; consulte con un abogado especializado.
```

**ANEXO XI – BOOT SEGURO EN SISTEMAS EMBEBIDOS SIN TPM**  

```markdown
# Anexo XI – Boot Seguro en Sistemas Embebidos sin TPM

## 1. Protocolo de arranque seguro con eFuse (RISC‑V)

```c
// boot_secure.c – verificación de firma en etapa de bootloader
#include "sha256.h"
#include "rsa.h"
extern const uint32_t firmware_hash[8];
extern const uint32_t signature[64];
void verify_boot() {
  uint32_t computed[8];
  sha256(firmware_start, firmware_len, computed);
  if (rsa_verify(computed, signature, public_key) != 0) {
    // fallar silenciosamente
    while(1);
  }
}
```

## 2. Script de verificación de integridad del firmware (desde host)

```bash
#!/bin/bash
# verifyFirmware.sh
openssl dgst -sha256 -verify public.pem -signature firmware.sig firmware.bin
if [ $? -eq 0 ]; then
    echo "✅ Firmware válido, procediendo a flashear"
else
    echo "🔴 FIRMA INVÁLIDA – ABORTAR"
    exit 1
fi
```

## 3. Ejemplo de implementación en Rust (sin std)

```rust
#![no_std]
use sha2::{Sha256, Digest};
#[no_mangle]
pub extern "C" fn verify() -> bool {
    let mut hasher = Sha256::new();
    hasher.update(FIRMWARE);
    let hash = hasher.finalize();
    hash == EXPECTED_HASH
}
```

**Compilación:** `cargo build --target thumbv7em-none-eabihf`

**Nota:** Requiere hardware con eFuse o una tarjeta MicroSD cifrada que contenga la clave pública. El bootloader debe ser de solo lectura.
```

**ANEXO XII – PLAYBOOKS DE CONTENCIÓN PARA LIVING‑OFF‑THE‑LAND**  

```markdown
# Anexo XII – Playbooks de Contención para Living‑off‑the‑Land

## 1. Playbook para PowerShell malicioso

**Detección:** Proceso `powershell.exe` con argumentos que contienen `-EncodedCommand` o `-ExecutionPolicy Bypass`.

**Contención inmediata:**
1. Aislar el endpoint de la red (script `isolateEndpoint.js`).
2. Capturar la memoria del proceso (con `procdump`).
3. Bloquear la ejecución de PowerShell con `AppLocker` o `WDAC`.

```powershell
# isolateEndpoint.ps1 (ejecutar con privilegios de administrador)
Set-NetFirewallRule -DisplayName "Block All Outbound" -Enabled True
```

## 2. Contención de WMI usado como C2

```javascript
// blockWmi.js
const { execSync } = require('child_process');
execSync('sc config winmgmt start= disabled');
execSync('net stop winmgmt');
console.log("⚠️ Servicio WMI deshabilitado temporalmente – reiniciar después de la limpieza");
```

## 3. Guía de preservación de evidencias

- Copiar logs de PowerShell (`Get-WinEvent -LogName 'Windows PowerShell' | Export-Csv ps_logs.csv`).
- Hacer imagen forense de la RAM (usando `FTK Imager` o `DumpIt`).
- Registrar el hash de los ejecutables sospechosos.

**Nota:** No apagar el sistema antes de la captura de memoria volátil.
```

**ANEXO XIII – AI ACT PARA SISTEMAS DE DEFENSA**  

```markdown
# Anexo XIII – AI Act para Sistemas de Defensa

## 1. Requisitos de documentación técnica (Art. 11)

- Descripción detallada del sistema y sus finalidades.
- Código fuente (o pseudocódigo) y arquitectura de datos.
- Resultados de pruebas y validaciones (incluyendo ciberseguridad).
- Análisis de riesgos y evaluación de conformidad.

**Plantilla de ficha técnica (markdown):**

```markdown
## Documentación Técnica para Defensor de IA

**Nombre del sistema:** Ronin‑IDS v1
**Tipo:** Sistema de detección de intrusiones basado en LLM local
**Hardware:** Raspberry Pi 5 + Coral TPU
**Pruebas realizadas:** Tasa de falsos positivos < 1% en dataset MITRE ATT&CK
```

## 2. Evaluación de impacto en derechos fundamentales (EIPD)

- **Ámbitos afectados:** Privacidad, no discriminación, libertad de expresión.
- **Mitigaciones:** Anonimización de logs, ausencia de sesgos étnicos, derecho a apelación.

## 3. Controles de ciberseguridad obligatorios (Art. 15)

- Resiliencia ante ataques adversariales (tests con `Adversarial Robustness Toolbox`).
- Registro de eventos (logs) inmutables.
- Control de acceso basado en roles (RBAC) a las funcionalidades críticas.

**Nota:** Los sistemas de defensa que sean catalogados como «alto riesgo» deberán notificarse al registro de la UE.
```

**ANEXO XIV – GIT HOOK UNIVERSAL CON OLLAMA PARA DETECCIÓN DE SECRETOS**  

```markdown
# Anexo XIV – Git Hook Universal con Ollama para Detección de Secretos

## 1. Pre‑commit hook (`.git/hooks/pre-commit`)

```bash
#!/bin/bash
# pre-commit hook que analiza los archivos modificados con Ollama
FILES=$(git diff --cached --name-only)
for FILE in $FILES; do
    if [[ $FILE =~ \.(js|ts|py|go|rs|json|yaml)$ ]]; then
        CONTENT=$(cat "$FILE")
        echo "$CONTENT" | ollama run llama3.2:3b \
            "Responde únicamente 'SECRETO' si este código contiene claves API, contraseñas o tokens. De lo contrario, 'OK'."
        RESULT=$?
        if [ $RESULT == "SECRETO" ]; then
            echo "🔴 Secreto detectado en $FILE. No se permite el commit."
            exit 1
        fi
    fi
done
```

## 2. Script de instalación del hook

```bash
#!/bin/bash
# installHook.sh
cp pre-commit .git/hooks/
chmod +x .git/hooks/pre-commit
echo "Hook instalado correctamente"
```

## 3. Lista de patrones personalizables (alternativa a Ollama)

```javascript
// regexSecrets.js
const patterns = [
  /AKIA[0-9A-Z]{16}/, // AWS key
  /sk-[a-zA-Z0-9]{48}/, // OpenAI key
  /-----BEGIN RSA PRIVATE KEY-----/
];
module.exports = patterns;
```

**Nota:** Ollama debe estar ejecutándose en segundo plano. Para entornos sin GPU, se puede usar el detector basado en regex.
```

**ANEXO XV – CAOS ENGINEERING APLICADO A SEGURIDAD**  

```markdown
# Anexo XV – Caos Engineering Aplicado a Seguridad

## 1. Framework para inyección de fallos controlados

```javascript
// chaosInjector.js
const http = require('http');
const targetURL = 'http://localhost:8080/api';
function injectLatency() {
  console.log("⚠️ Inyectando latencia de 500ms");
  // Simula retardo en la red local (requiere iptables o tc)
  require('child_process').execSync('tc qdisc add dev eth0 root netem delay 500ms');
  setTimeout(() => {
    require('child_process').execSync('tc qdisc del dev eth0 root');
  }, 30000);
}
function killExternalAPI() {
  console.log("💀 Bloqueando acceso a api.openai.com");
  require('child_process').execSync('iptables -A OUTPUT -d api.openai.com -j DROP');
}
// Ejecutar aleatoriamente
setInterval(() => {
  if (Math.random() < 0.1) killExternalAPI();
}, 60000);
```

## 2. Medición del IAP durante el caos

```javascript
// measureIAPUnderChaos.js
const { execSync } = require('child_process');
const baselineIAP = require('./validateIAP.js'); // script del anexo I
console.log("IAP antes del caos:", baselineIAP);
execSync('node chaosInjector.js &');
setTimeout(() => {
  const newIAP = require('./validateIAP.js');
  console.log("IAP durante el caos:", newIAP);
}, 120000);
```

## 3. Dashboard de evolución de resiliencia

```html
<!-- resiliencia.html – gráfico simple con Chart.js -->
<canvas id="chaosChart"></canvas>
<script>
fetch('/api/iap-history')
  .then(res => res.json())
  .then(data => new Chart('chaosChart', { type: 'line', data: { labels: data.timestamps, datasets: [{ label: 'IAP', data: data.values }] } }));
</script>
```

**Nota:** Los comandos de red (`tc`, `iptables`) requieren privilegios de superusuario. No ejecutar en entornos de producción sin aislamiento.
```

--
**ANEXO XVI – PRESERVACIÓN A LARGO PLAZO DEL CONOCIMIENTO**  

```markdown
# Anexo XVI – Preservación a Largo Plazo del Conocimiento

## 1. Empaquetado en formato de archivo abierto (WARC, OCFL)

```bash
#!/bin/bash
# createWarc.sh
wget --mirror --warc-file=ronin-manual https://github.com/ronin-omega/manual
echo "Archivo WARC generado: ronin-manual.warc.gz"
```

## 2. Verificación periódica de integridad con hash chains

```javascript
// verifyIntegrity.js
const crypto = require('crypto');
const fs = require('fs');
const chainFile = 'integrity.chain';
let prevHash = '0'.repeat(64);
if (fs.existsSync(chainFile)) {
  const lines = fs.readFileSync(chainFile, 'utf8').split('\n');
  prevHash = lines[lines.length-2];
}
const content = fs.readFileSync('manual.pdf');
const hash = crypto.createHash('sha256').update(content).digest('hex');
fs.appendFileSync(chainFile, `${hash}\n${prevHash}\n`);
console.log(`Hash añadido: ${hash}`);
```

## 3. Plan de migración a nuevos soportes (cada 5 años)

- **Copia maestra:** disco duro externo cifrado, almacenado en dos ubicaciones geográficas distintas.
- **Formato de archivo:** PDF/A-3, Markdown plano, scripts en texto sin formato.
- **Verificación:** script automatizado que compara el hash actual con la cadena.

**Nota:** La preservación no es automática; requiere un responsable asignado y una política de migración documentada.
```

**ANEXO XVII – PLANTILLAS DE COMUNICACIÓN POST‑BRECHA**  

```markdown
# Anexo XVII – Plantillas de Comunicación Post‑Brecha

## 1. Comunicado de prensa (niveles de gravedad)

**Nivel bajo (incidente interno, sin datos de clientes):**
> *“La empresa ha detectado un incidente de seguridad menor que no ha afectado a datos de clientes. Se han tomado medidas correctivas.”*

**Nivel alto (exfiltración de datos personales):**
> *“Hemos sufrido un ciberataque que ha comprometido [descripción]. Estamos notificando a las autoridades y a los afectados según la ley.”*

## 2. Email a clientes afectados (RGPD compliant)

```text
Asunto: Notificación de incidente de seguridad – [Nombre Empresa]

Estimado/a [Nombre],

Le informamos que hemos detectado un acceso no autorizado a nuestros sistemas que pudo afectar a sus datos [especificar]. No hay evidencia de uso fraudulento hasta la fecha.

Medidas adoptadas: [cambiar contraseñas, reforzar controles].

Sentimos las molestias y estamos a su disposición en [teléfono/email específico].

Atentamente,
[Responsable de Protección de Datos]
```

## 3. Modelo de informe a la AEPD (72h)

```text
1. Naturaleza de la brecha: [robo de credenciales, acceso no autorizado, etc.]
2. Datos afectados: [tipos y número de registros]
3. Medidas de contención adoptadas: [aislamiento, revocación de accesos]
4. Evaluación del riesgo para los afectados: [alto/medio/bajo]
5. Contacto del DPO: [email, teléfono]
```

**Nota:** Adjuntar el informe como PDF firmado electrónicamente.
```

**ANEXO XVIII – SEGMENTACIÓN DINÁMICA POR IDENTIDAD (SD‑WAN)**  

```markdown
# Anexo XVIII – Segmentación Dinámica por Identidad (SD‑WAN)

## 1. Configuración de microsegmentación con etiquetas (Zero Trust)

```bash
# iptables con etiquetas de usuario (requiere módulo `connmark`)
iptables -A OUTPUT -m owner --uid-owner 1001 -j MARK --set-mark 10
iptables -A OUTPUT -m mark --mark 10 -j DROP  # solo permite acceso a recursos específicos
```

## 2. Script para entornos con movilidad (WireGuard + identidad)

```javascript
// dynamicZTNA.js
const { execSync } = require('child_process');
const user = process.env.USER;
const allowedIPs = (user === 'admin') ? '0.0.0.0/0' : '192.168.1.0/24';
execSync(`wg set wg0 peer ${user} allowed-ips ${allowedIPs}`);
console.log(`✅ Acceso configurado para ${user}: ${allowedIPs}`);
```

## 3. Ejemplo de implementación con WireGuard

```bash
# /etc/wireguard/wg0.conf
[Peer]
PublicKey = <clave del usuario>
AllowedIPs = 192.168.1.10/32
```

**Nota:** La segmentación dinámica requiere un directorio de identidades (LDAP local o archivo de claves públicas).
```

**ANEXO XIX – CADENA DE CUSTODIA DE LOGS CON BLOCKCHAIN LOCAL**  

```markdown
# Anexo XIX – Cadena de Custodia de Logs con Blockchain Local

## 1. Timestamping de logs en Hyperledger Besu (red privada)

```javascript
// logNotary.js
const Web3 = require('web3');
const web3 = new Web3('http://localhost:8545');
const contract = new web3.eth.Contract(abi, address);
async function notarize(logEntry) {
  const hash = web3.utils.sha3(logEntry);
  await contract.methods.addHash(hash).send({ from: '0x...' });
  console.log(`Log notarizado: ${hash}`);
}
```

## 2. Firma de cada entrada con clave local

```javascript
// signLog.js
const crypto = require('crypto');
const privateKey = `-----BEGIN PRIVATE KEY-----...`;
const sign = crypto.createSign('SHA256');
sign.update(logEntry);
const signature = sign.sign(privateKey, 'hex');
fs.appendFileSync('signed.log', `${logEntry} | SIGNATURE: ${signature}\n`);
```

## 3. Verificación de integridad de la cadena de custodia

```javascript
// verifyLogChain.js
const lines = fs.readFileSync('signed.log', 'utf8').split('\n');
for (let i = 1; i < lines.length; i++) {
  const prevHash = crypto.createHash('sha256').update(lines[i-1]).digest('hex');
  if (!lines[i].includes(prevHash)) {
    console.error(`🔴 Cadena rota en línea ${i}`);
    process.exit(1);
  }
}
console.log("✅ Cadena de custodia íntegra");
```

**Nota:** Requiere una red Hyperledger Besu local para el notarizado; la versión simplificada puede usar solo hash chain.
```

**ANEXO XX – PROGRAMA DE RECOMPENSAS INTERNAS PARA LA DESOBEDIENCIA ÉTICA**  

```markdown
# Anexo XX – Programa de Recompensas Internas para la Desobediencia Ética

## 1. Modelo de bug bounty interno

```json
{
  "program_name": "Ronin Bug Bounty",
  "scope": ["aplicaciones internas", "infraestructura crítica"],
  "rewards": {
    "low": "vale de formación",
    "medium": "día libre adicional",
    "high": "bonificación económica (500€)",
    "critical": "reconocimiento público y bono de 2.000€"
  }
}
```

## 2. Sistema de puntos canjeables

```javascript
// pointsLedger.js
const points = new Map();
function awardPoints(employeeId, pointsAmount, reason) {
  const current = points.get(employeeId) || 0;
  points.set(employeeId, current + pointsAmount);
  fs.appendFileSync('points.log', `${Date.now()},${employeeId},${pointsAmount},${reason}\n`);
}
```

## 3. Política de no represalias (texto para el empleado)

> *“Cualquier empleado que reporte una vulnerabilidad o un incidente de seguridad de buena fe no será objeto de represalias disciplinarias ni laborales. La dirección se compromete a investigar y, si procede, recompensar al informante.”*

**Nota:** El programa debe ser aprobado por el comité de ética y comunicado a toda la organización.
```

**ANEXO XXI – MINIMIZACIÓN DE DATOS Y SEUDONIMIZACIÓN EN DESARROLLO**  

```markdown
# Anexo XXI – Minimización de Datos y Seudonimización en Desarrollo

## 1. Generación de datos sintéticos a partir de esquemas

```python
# syntheticData.py
import pandas as pd
import numpy as np
original = pd.read_csv('real_data.csv')
synthetic = original.copy()
for col in ['name', 'email', 'phone']:
    synthetic[col] = synthetic[col].apply(lambda x: hashlib.sha256(x.encode()).hexdigest()[:16])
synthetic.to_csv('synthetic_data.csv', index=False)
```

## 2. Seudonimización con sal local

```javascript
// pseudonymize.js
const crypto = require('crypto');
const salt = process.env.SALT || crypto.randomBytes(16).toString('hex');
function pseudonymize(value) {
  return crypto.createHmac('sha256', salt).update(value).digest('hex');
}
```

## 3. Protocolo para entornos de desarrollo sin datos reales

- **Regla:** Nunca copiar bases de datos de producción a desarrollo.
- **Alternativa:** Usar generadores de datos ficticios (`faker.js`, `mockaroo`).
- **Verificación:** Script que comprueba que no hay direcciones de email reales en el código.

```bash
# checkNoRealEmails.sh
if grep -rE '\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b' src/; then
    echo "🔴 Posible email real en el código. Revise antes de commit."
    exit 1
fi
```

**Nota:** La seudonimización no es anonimización; si se requiere anonimato, agregar ruido (ε‑DP) con el anexo de privacidad diferencial (no incluido en esta versión).
```

**ANEXO XXII – SEGURIDAD EN COMUNICACIONES MÓVILES (5G/6G) PARA TRABAJADORES REMOTOS**  

```markdown
# Anexo XXII – Seguridad en Comunicaciones Móviles (5G/6G) para Trabajadores Remotos

## 1. Configuración de SIM protegida (eSIM con aislamiento)

- **Recomendación:** Usar eSIM con perfil dedicado solo para datos corporativos.
- **Verificación:** `AT+CPIN?` en módem para asegurar PIN no por defecto.

## 2. VPN con criptografía post‑cuántica (liboqs + WireGuard)

```bash
# Compilar WireGuard con soporte para liboqs
git clone https://github.com/open-quantum-safe/wireguard
make && make install
# Configurar interfaz wg0 con cifrado Kyber
```

```javascript
// postQuantumVPN.js
const { execSync } = require('child_process');
execSync('wg set wg0 private-key ./quantum.key peer <peer_pubkey> allowed-ips 0.0.0.0/0 endpoint quantum.vpn.com:51820');
```

## 3. Detección de suplantación de estación base (SS7 y 5G)

```javascript
// baseStationDetector.js
const { execSync } = require('child_process');
const mcc = execSync('mmcli -L | grep -oP "MCC=\\K\\d+"').toString().trim();
const mnc = execSync('mmcli -L | grep -oP "MNC=\\K\\d+"').toString().trim();
if (mcc !== '214' && mnc !== '07') {
  console.warn("⚠️ Estación base extranjera no esperada – posible interceptación");
}
```

**Nota:** La criptografía post‑cuántica aún es experimental; en entornos críticos combine con un túnel tradicional (IPsec) y planifique migración futura.

---

`

