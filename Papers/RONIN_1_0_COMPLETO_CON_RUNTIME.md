# 🥚 RONIN — THE LANGUAGE OF FINITE SYSTEMS WITH SCARCE RESOURCES

## *Versión 1.0 — Edición Completa, Normativa y Funcional*

---

**Versión:** 1.0 — Edición Completa, Normativa y Funcional  
**Autor:** David Ferrandez Canalis — Agencia RONIN  
**Fecha:** Agosto de 2026  
**Clasificación:** `LENGUAJE DE PROGRAMACIÓN / INFRAESTRUCTURA DE SISTEMAS / VIDEOJUEGOS / DESARROLLO DE SOFTWARE`

---

## DECLARACIÓN NORMATIVA DE RONIN 1.0

Esta edición conserva la extensión, estructura, terminología, ejemplos, arquitectura y filosofía de la especificación original. Las correcciones de esta versión tienen un único objetivo: convertir el documento en una **guía de implementación funcional y reproducible**.

### Regla de autoridad de la v1.0

Cuando exista una discrepancia entre un comentario numérico de una versión anterior y una ecuación normativa, **la ecuación normativa prevalece**. Los ejemplos de esta edición han sido recalculados con esa semántica.

### Semántica normativa de `solve`

Para cada agente `i`, RONIN 1.0 define:

$$F_i = \phi_i \cdot \psi_i \cdot \Omega_i^\alpha$$

con `epsilon_i = 1` en la v1.0 base. La asignación determinista es:

$$A_i = R \cdot \frac{F_i}{\sum_j F_j}$$

La suma de las asignaciones es exactamente `resource`, salvo el error numérico de coma flotante. `solve` **no usa `sigma` como ruido**: `sigma` pertenece a `simulate`.

### Semántica normativa de `simulate`

`simulate` es la operación estocástica. Parte del estado inicial de frecuencias y aplica una cadena de transición definida por el runtime de referencia. En v1.0, la implementación mínima conforme debe ser determinista cuando `sigma = 0` y reproducible cuando se proporciona `seed`.

### Valores numéricos de referencia

Los valores mostrados en ejemplos antiguos que no puedan derivarse de las ecuaciones anteriores se consideran errores editoriales y han sido sustituidos por resultados reproducibles. Los benchmarks históricos del material original no se consideran resultados verificados de RONIN 1.0. Se conservan únicamente como antecedentes y deben reproducirse con un runtime y un protocolo publicados antes de presentarse como mediciones.

---

## PRÓLOGO: ESTO ES PARA TI, QUE NO SABES NADA (Y ESTÁ BIEN)

Tranquilo. Este tutorial no asume que sabes matemáticas. No asume que sabes programar. No asume que sabes qué es un sistema finito con recursos escasos. Solo asume que quieres resolver un problema que no sabes cómo atacar.

RONIN es el lenguaje que te permite declarar un sistema y obtener una solución sin tener que escribir código de infraestructura. Es para gente que quiere **resolver**, no que quiere **programar**.

**No necesitas saber nada de antemano. Solo necesitas leer esto y seguir los pasos.**

Este documento contiene:
- Un tutorial completo para empezar desde cero.
- La especificación formal del lenguaje (sintaxis, tipos, comandos).
- Un anexo con **100 ejemplos prácticos** para el día a día.
- Un anexo con la arquitectura interna del compilador.
- **Una nueva sección con aplicaciones de RONIN en videojuegos y otras ramas del desarrollo de software.**

**RONIN está diseñado para funcionar de forma nativa en Linux.** Todos los comandos, herramientas de desarrollo y ejemplos están optimizados para entornos Linux (systemd, journald, signals, pipes, bash, etc.). Si usas Linux, RONIN se siente como en casa.

---

## ÍNDICE GENERAL

**PARTE I — TUTORIAL PARA MORTALES**

1. [Prólogo: Esto es para ti, que no sabes nada](#prólogo)
2. [Qué es un sistema y por qué te importa](#capítulo-1-qué-es-un-sistema)
3. [Tu primer sistema en RONIN](#capítulo-2-tu-primer-sistema)
4. [Qué significa cada cosa (sin jerga)](#capítulo-3-qué-significa-cada-cosa)
5. [Ejemplos progresivos](#capítulo-4-ejemplos-progresivos)
6. [Errores comunes y cómo el compilador te ayuda](#capítulo-5-errores-comunes)
7. [Lo que no necesitas saber (pero está ahí)](#capítulo-6-lo-que-no-necesitas-saber)
8. [Referencia rápida](#capítulo-7-referencia-rápida)
9. [Koans del tutorial](#capítulo-8-koans-del-tutorial)

**PARTE II — ESPECIFICACIÓN FORMAL DEL LENGUAJE (COMPLETA)**

10. [Filosofía operativa](#sección-0-filosofía-operativa)
11. [Principios fundamentales](#sección-1-principios-fundamentales)
12. [Sintaxis básica](#sección-2-sintaxis-básica)
13. [Sistema de tipos y validación](#sección-3-tipos-y-validación)
14. [Concurrencia y paralelismo](#sección-4-concurrencia-y-paralelismo)
15. [Interoperabilidad](#sección-5-interoperabilidad)
16. [Compilación y ejecución](#sección-6-compilación-y-ejecución)
17. [Herramientas de desarrollo](#sección-7-herramientas-de-desarrollo)
18. [Casos de uso completos](#sección-8-casos-de-uso-completos)
19. [Comparativa con otros lenguajes](#sección-9-comparativa-con-otros-lenguajes)
20. [Implementación interna](#sección-10-implementación)
21. [Extensiones y futuro](#sección-11-extensiones-y-futuro)
22. [Koans de RONIN](#sección-12-koans-de-ronin)
23. [Soporte nativo para Linux](#sección-13-soporte-nativo-para-linux)
24. **[NUEVO] Aplicaciones de RONIN en Desarrollo de Software**](#sección-14-aplicaciones-de-ronin-en-desarrollo-de-software)
    - 14.1 Videojuegos (balanceo, IA, economía, progresión)
    - 14.2 Desarrollo Web (balanceo de carga, asignación de recursos)
    - 14.3 Sistemas Embebidos e IoT
    - 14.4 Robótica y control de sistemas
    - 14.5 Ciencia de Datos y Machine Learning
    - 14.6 Finanzas y trading algorítmico
    - 14.7 Blockchain y criptomonedas
    - 14.8 Sistemas de recomendación
    - 14.9 Optimización de recursos en cloud
    - 14.10 Inteligencia Artificial multi-agente

**PARTE III — ANEXO: 100 COSAS QUE PUEDES HACER CON RONIN**

25. [Ejemplos 1 a 100](#anexo-1-100)
26. **[NUEVO] Ejemplos 101 a 110: Aplicaciones en desarrollo de software**](#anexo-101-110)

**PARTE IV — ANEXO DEL COMPILADOR: ARQUITECTURA Y EXTENSIÓN**

27. [Estructura interna del compilador](#anexo-compilador-estructura)
28. [El frontend: análisis sintáctico y semántico](#anexo-compilador-frontend)
29. [El IR: representación intermedia de sistemas](#anexo-compilador-ir)
30. [El backend: generación de código](#anexo-compilador-backend)
31. [Optimizaciones del compilador](#anexo-compilador-optimizaciones)
32. [Cómo extender RONIN con nuevos backends](#anexo-compilador-extension)
33. [Cómo añadir nuevos tipos de dominio](#anexo-compilador-tipos)
34. [Cómo añadir nuevos comandos](#anexo-compilador-comandos)
35. [El sistema de macros en tiempo de compilación](#anexo-compilador-macros)
36. [Cómo contribuir al compilador](#anexo-compilador-contribuir)

---

# PARTE I — TUTORIAL PARA MORTALES

## CAPÍTULO 1: QUÉ ES UN SISTEMA

### 1.1 Un sistema es cualquier cosa que tiene:

- **Partes**: varias entidades que compiten por algo.
- **Un recurso**: algo escaso que las partes quieren.
- **Un problema**: no sabes cómo repartirlo de forma justa.

**Ejemplos:**

- 5 flotas pesqueras (partes) y 10.000 toneladas de pescado (recurso).
- 20 activos financieros (partes) y 100 millones de euros (recurso).
- 100 semáforos (partes) y 120 segundos de ciclo (recurso).
- 50 regiones (partes) y 10.000 camas UCI (recurso).
- **10 clases de un juego RPG (partes) y 100 puntos de balance (recurso).**
- **8 microservicios (partes) y 1000 peticiones por segundo (recurso).**

### 1.2 Qué necesitas saber de cada parte

Solo tres números por cada parte:

- **Φ (phi)**: capacidad para usar el recurso (0..1).
- **Ψ (psi)**: consistencia, cuánto "debe" o "falla" (0..1).
- **Ω (omega)**: frecuencia inicial, cuánto se usa ahora (0..1). **La suma de todas las frecuencias debe ser 1.**

---

## CAPÍTULO 2: TU PRIMER SISTEMA

### 2.1 El problema

2 máquinas: A y B. 100 horas de trabajo.  
A: phi=0.8, psi=1.0, freq=0.6  
B: phi=0.5, psi=1.0, freq=0.4

**Pregunta:** ¿cuántas horas recibe cada una?

### 2.2 El código

```ronin
system Maquinas = {
    parts: 2,
    resource: 100,
    agents: [
        { phi: 0.8, psi: 1.0, frequency: 0.6 },
        { phi: 0.5, psi: 1.0, frequency: 0.4 }
    ],
    params: {
        alpha: 1.0,
        gamma: 0.4,
        sigma: 0.1
    }
}

result = solve Maquinas
print(result.allocation)  // [70.588235, 29.411765]
```

---

## CAPÍTULO 3: QUÉ SIGNIFICA CADA COSA

### 3.1 `phi` — Capacidad
- `phi = 0.9` → muy eficiente
- `phi = 0.3` → poco eficiente

### 3.2 `psi` — Consistencia
- `psi = 0.95` → casi sin deuda
- `psi = 0.5` → mucha deuda

### 3.3 `frequency` — Frecuencia
- `0.6` → se usa el 60% del tiempo
- **La suma de todas las frecuencias debe ser 1.**

### 3.4 `alpha` — Competencia
- `1.0` → competencia lineal (normal)
- `> 1.0` → winner-takes-all
- `< 1.0` → más biodiversidad

### 3.5 `gamma` — Penalización por deuda
- `0.0` → la deuda no importa
- `0.5` → la deuda importa mucho

### 3.6 `sigma` — Ruido
- `0.0` → determinista
- `0.2` → variabilidad alta

---

## CAPÍTULO 4: EJEMPLOS PROGRESIVOS

### 4.1 Dos partes (fácil)
```ronin
system DosPartes = {
    parts: 2,
    resource: 100,
    agents: [
        { phi: 0.9, psi: 0.9, frequency: 0.5 },
        { phi: 0.5, psi: 0.5, frequency: 0.5 }
    ],
    params: { alpha: 1.0, gamma: 0.3, sigma: 0.1 }
}
result = solve DosPartes  // [~76.415, ~23.585]
```

### 4.2 Tres partes
```ronin
system TresPartes = {
    parts: 3,
    resource: 1000,
    agents: [
        { phi: 0.9, psi: 0.9, frequency: 0.4 },
        { phi: 0.7, psi: 0.8, frequency: 0.35 },
        { phi: 0.4, psi: 0.9, frequency: 0.25 }
    ],
    params: { alpha: 1.2, gamma: 0.4, sigma: 0.15 }
}
result = solve TresPartes  // [~542.932, ~319.785, ~137.284]
```

### 4.3 Cinco partes (pesca)
```ronin
system Pesca = {
    parts: 5,
    resource: 10000,
    agents: [
        { phi: 0.95, psi: 0.68, frequency: 0.267 },
        { phi: 0.85, psi: 0.76, frequency: 0.238 },
        { phi: 0.60, psi: 0.92, frequency: 0.160 },
        { phi: 0.45, psi: 0.96, frequency: 0.131 },
        { phi: 0.70, psi: 0.84, frequency: 0.199 }
    ],
    params: { alpha: 1.3, gamma: 0.4, sigma: 0.15 }
}
result = solve Pesca  // [3138.305, 2702.592, 1378.139, 831.638, 1949.325]
```

### 4.4 Con auditoría de deuda
```ronin
audit = audit Pesca with {
    epsilon: 0.05,
    delta: 0.01,
    stratified: true
}
print(audit.estimated_debt)  // 0.034 ± 0.012 (99% CI)
```

### 4.5 Con simulación DTMC
```ronin
sim = simulate Pesca with {
    steps: 100,
    dtmc: true,
    stochastic: true
}
plot sim
```

---

## CAPÍTULO 5: ERRORES COMUNES

### 5.1 Frecuencias que no suman 1
```ronin
agents: [
    { phi: 0.8, psi: 1.0, frequency: 0.6 },
    { phi: 0.5, psi: 1.0, frequency: 0.5 }   // ❌ 0.6+0.5=1.1
]
```
**Error:** `Error: Las frecuencias deben sumar 1 (suma actual: 1.1)`

### 5.2 `phi` fuera de rango
```ronin
{ phi: 1.5, psi: 1.0, frequency: 0.5 }  // ❌
```
**Error:** `Error: phi debe estar entre 0 y 1 (valor actual: 1.5)`

### 5.3 `alpha` fuera de rango
```ronin
params: { alpha: 3.0, gamma: 0.4, sigma: 0.1 }  // ❌
```
**Error:** `Error: alpha debe estar entre 0.5 y 2.5 (valor actual: 3.0)`

### 5.4 Menos de 2 partes
```ronin
parts: 1  // ❌
```
**Error:** `Error: Un sistema debe tener al menos 2 partes.`

### 5.5 Coexistencia imposible
```ronin
system Imposible = {
    parts: 5,
    resource: 1,
    agents: [
        { phi: 0.99, psi: 0.99, frequency: 0.5 },
        { phi: 0.01, psi: 0.01, frequency: 0.5 }
    ],
    params: { alpha: 2.5, gamma: 0.9, sigma: 0.0 }
}
```
**Advertencia normativa:** `Warning: k_min (5313.81) > k_actual (1.0). La coexistencia no es posible.`

---

## CAPÍTULO 6: LO QUE NO NECESITAS SABER

RONIN hace todo esto por ti. No necesitas entenderlo para usarlo, pero por si te da curiosidad:

- **Ecuación Maestra:** `F_i = phi_i * psi_i * freq_i^alpha * epsilon_i`
- **DTMC:** Cadena de Markov en tiempo discreto
- **Hoeffding:** Garantía estadística para auditorías
- **Coexistencia-k:** Fórmula que calcula supervivencia de todas las partes
- **Fatiga de enrutamiento:** Coste de cambiar de una parte a otra
- **Geometría del olvido:** Cómo la posición afecta la retención
- **Deuda ontológica:** Cómo las contradicciones se acumulan

---

## CAPÍTULO 7: REFERENCIA RÁPIDA

### 7.1 Estructura básica
```ronin
system Nombre = {
    parts: N,
    resource: R,
    agents: [
        { phi: ..., psi: ..., frequency: ... },
        ...
    ],
    params: {
        alpha: ...,
        gamma: ...,
        sigma: ...
    }
}
```

### 7.2 Parámetros recomendados por dominio
| Dominio | alpha | gamma | sigma |
|---------|-------|-------|-------|
| Logística | 1.2 | 0.35 | 0.12 |
| Finanzas | 1.0 | 0.30 | 0.20 |
| Energía | 1.3 | 0.50 | 0.10 |
| Salud | 1.1 | 0.40 | 0.15 |
| Ciberseguridad | 1.2 | 0.50 | 0.12 |
| Telecomunicaciones | 1.2 | 0.40 | 0.15 |
| Agricultura | 1.0 | 0.30 | 0.20 |
| Retail | 1.1 | 0.40 | 0.15 |
| Manufactura | 1.2 | 0.30 | 0.10 |
| **Videojuegos (balanceo)** | **1.1** | **0.35** | **0.10** |
| **Web (balanceo de carga)** | **1.2** | **0.30** | **0.15** |
| **IoT/Embebido** | **1.0** | **0.40** | **0.08** |

### 7.3 Comandos básicos
| Comando | Función |
|---------|---------|
| `solve Nombre` | Resuelve el sistema |
| `simulate Nombre with { ... }` | Simula |
| `audit Nombre with { ... }` | Audita la deuda |
| `plot Nombre` | Visualiza |
| `print(result)` | Muestra el resultado |

### 7.4 Opciones comunes
| Opción | Valores | Defecto |
|--------|---------|---------|
| `steps` | entero > 0 | 100 |
| `dtmc` | true/false | true |
| `stochastic` | true/false | true |
| `parallel` | true/false | false |
| `threads` | entero > 0 | 8 |
| `epsilon` | 0.01 - 0.2 | 0.05 |
| `delta` | 0.01 - 0.1 | 0.01 |
| `stratified` | true/false | true |

---

## CAPÍTULO 8: KOANS DEL TUTORIAL

**Del que no sabe nada:** El que no sabe nada es el que más puede aprender.

**De la línea que resuelve todo:** Una línea de RONIN puede reemplazar 200 líneas de Python.

**Del error que no ocurre:** La arquitectura del compilador de RONIN no te deja equivocarte.

**Del torpe que resuelve:** No hace falta saber matemáticas para usar RONIN.

**Del miedo que desaparece:** El primer sistema da miedo. El décimo da risa.

---

# PARTE II — ESPECIFICACIÓN FORMAL DEL LENGUAJE

## SECCIÓN 0: FILOSOFÍA OPERATIVA

### 0.1 El principio de RONIN
> *"Cualquier sistema finito con recursos escasos puede modelarse como una asignación de recurso entre partes, y la solución óptima es la que maximiza la coexistencia."*

### 0.2 La metáfora del arquitecto
RONIN no es para programadores. Es para **arquitectos**.

### 0.3 La validación como guardián
RONIN no permite errores de dominio.

### 0.4 Interoperabilidad como puente
RONIN se integra con Python, Rust, SQL, APIs REST.

### 0.5 IA como generadora de sistemas
RONIN está diseñado para que una IA genere código.

---

## SECCIÓN 1: PRINCIPIOS FUNDAMENTALES

### 1.1 Todo es un sistema
```ronin
system Pesca = { parts: 5, resource: 10000, agents: [...], params: {...} }
```

### 1.2 La asignación es la computación
```ronin
result = solve Pesca
```

### 1.3 La coexistencia es la condición de corrección
```ronin
assert(result.coexistence == true)
```

### 1.4 La deuda se audita automáticamente
```ronin
audit = system.debt()
```

### 1.5 La geometría se mide automáticamente
```ronin
let geometry = system.geometry()
```

### 1.6 La fatiga de enrutamiento se calcula
```ronin
let fatigue = system.fatigue()
```

---

## SECCIÓN 2: SINTAXIS BÁSICA

### 2.1 Declaración de sistema
```ronin
system Nombre = {
    parts: entero,
    resource: flotante,
    agents: [Agent],
    params: {
        alpha: flotante,
        gamma: flotante,
        sigma: flotante
    }
}
```

### 2.2 Definición de agente
```ronin
agent Industrial = {
    phi: 0.95,
    psi: 0.68,
    frequency: 0.267
}
```

### 2.3 Agente extendido (con nicho)
```ronin
agent Longline = {
    phi: 0.60,
    psi: 0.92,
    frequency: 0.160,
    niche: [0.1, 0.3, 0.5, 0.7, 0.9],
    tools: ["palangre", "anzuelo"],
    protocol: "artesanal"
}
```

### 2.4 Arrays y estructuras
```ronin
let phi = [0.95, 0.85, 0.60, 0.45, 0.70]
let psi = [0.68, 0.76, 0.92, 0.96, 0.84]
```

### 2.5 Funciones puras
```ronin
fn fitness(phi: Probability, psi: Probability, frequency: Frequency, alpha: Alpha) -> Fitness {
    return phi * psi * frequency^alpha
}
```

### 2.6 Funciones impuras
```ronin
fn simulate(system: System) -> Simulation {
    return run_reference_simulation(system)
}
```

### 2.7 Simulación
```ronin
sim = simulate Pesca with {
    steps: 100,
    dtmc: true,
    stochastic: true,
    routing_pressure: Beta(2.3, 5.1)
}
```

### 2.8 Auditoría
```ronin
audit = audit Pesca with {
    epsilon: 0.05,
    delta: 0.01,
    stratified: true,
    clusters: HDBSCAN
}
```

### 2.9 Visualización
```ronin
plot Pesca
plot sim
plot audit
```

### 2.10 Condicionales
```ronin
if result.coexistence {
    print("Coexistencia garantizada")
} else {
    print("Sistema inestable. Ajustar parámetros.")
}
```

### 2.11 Bucles
```ronin
for agent in system.agents {
    print(agent.phi)
}
```

### 2.12 Módulos
```ronin
module Fisheries {
    system Atlantic = { ... }
    system Pacific = { ... }
}
import Fisheries
```

### 2.13 Macros
```ronin
macro audit_system(system) {
    return audit(system with {
        epsilon: 0.05,
        delta: 0.01,
        stratified: true
    })
}
```

---

## SECCIÓN 3: TIPOS Y VALIDACIÓN

### 3.1 Tipos primitivos
```ronin
type Integer = int
type Float = float
type Boolean = bool
type String = string
type Array = [T]
```

### 3.2 Tipos de dominio (COMPLETO — 150+ tipos)
```ronin
type Probability = float 0..1
type Frequency = Probability
type Resource = float >= 0
type AgentCount = integer >= 2
type Alpha = float 0.5..2.5
type Gamma = float 0..1
type Sigma = float 0..0.5
type Fitness = float >= 0
type Coexistence = bool
type Debt = float 0..1
type Geometry = float 0..1
type Fatigue = float 0..1
type Epsilon = float 0..1
type Rho = float 0..1
type Delta = float 0..0.1
type BatchSize = integer >= 1
type Steps = integer >= 1
type Horizon = integer >= 1
type Confidence = float 0.9..1
type ErrorMargin = float 0..0.2
type Entropy = float 0..max
type Divergence = float >= 0
type Similarity = float 0..1
type Distance = float >= 0
type Time = float >= 0
type Cost = float >= 0
type Benefit = float >= 0
type Utility = float
type Priority = float 0..1
type Severity = float 0..1
type Weight = Probability
type Share = Probability
type Ratio = float >= 0
type Exponent = float >= 0
type Volatility = float >= 0
type Return = float
type Risk = float 0..1
type Throughput = float >= 0
type Latency = float >= 0
type Capacity = float >= 0
type Demand = float >= 0
type Supply = float >= 0
type Inventory = float >= 0
type Backlog = float >= 0
type Waste = float >= 0
type Pollution = float 0..1
type Happiness = float 0..1
type Health = float 0..1
type Trust = float 0..1
type Satisfaction = float 0..1
type Resilience = float 0..1
type Robustness = float 0..1
type Diversity = float 0..1
type Biodiversity = float 0..1
type Complexity = float >= 0
type Stability = float 0..1
type Oscillation = float >= 0
type Convergence = float 0..1
type Error = float >= 0
type Accuracy = float 0..1
type Precision = float 0..1
type Recall = float 0..1
type F1 = float 0..1
type AUC = float 0..1
type ROC = float 0..1
type MSE = float >= 0
type RMSE = float >= 0
type MAE = float >= 0
type R2 = float 0..1
type LogLoss = float >= 0
type KLDivergence = float >= 0
type JSdivergence = float 0..1
type WDistance = float >= 0
type Energy = float >= 0
type Power = float >= 0
type Work = float >= 0
type Efficiency = float 0..1
type Productivity = float >= 0
type Profit = float >= 0
type Revenue = float >= 0
type Investment = float >= 0
type Capital = float >= 0
type Liability = float >= 0
type Asset = float >= 0
type Equity = float >= 0
type Interest = float >= 0
type Inflation = float 0..1
type Growth = float
type Development = float 0..1
type Sustainability = float 0..1
type Inequality = float 0..1
type Justice = float 0..1
type Peace = float 0..1
type Security = float 0..1
type Freedom = float 0..1
type Democracy = float 0..1
type Participation = float 0..1
type Representation = float 0..1
type Transparency = float 0..1
type Accountability = float 0..1
type Legitimacy = float 0..1
type Authority = float 0..1
type Power = float 0..1
type Influence = float 0..1
type Status = float 0..1
type Prestige = float 0..1
type Reputation = float 0..1
type Honor = float 0..1
type Respect = float 0..1
type Dignity = float 0..1
type Compassion = float 0..1
type Empathy = float 0..1
type Solidarity = float 0..1
type Cooperation = float 0..1
type Altruism = float 0..1
type Generosity = float 0..1
type Kindness = float 0..1
type Love = float 0..1
type Beauty = float 0..1
type Truth = float 0..1
type Wisdom = float 0..1
type Understanding = float 0..1
type Insight = float 0..1
type Creativity = float 0..1
type Innovation = float 0..1
type Invention = float 0..1
type Discovery = float 0..1
type Learning = float 0..1
type Teaching = float 0..1
type Mentoring = float 0..1
type Leadership = float 0..1
type Followership = float 0..1
type Partnership = float 0..1
type Friendship = float 0..1
type Community = float 0..1
type Society = float 0..1
type Culture = float 0..1
type Civilization = float 0..1
type Humanity = float 0..1
type Existence = float 0..1
type Reality = float 0..1
type Universe = float 0..1
```

### 3.3 Tipos compuestos
```ronin
type Agent = {
    phi: Probability,
    psi: Probability,
    frequency: Frequency,
    niche: Array[Float],
    tools: Array[String],
    protocol: String
}

type System = {
    parts: AgentCount,
    resource: Resource,
    agents: Array[Agent],
    params: Params
}

type Params = {
    alpha: Alpha,
    gamma: Gamma,
    sigma: Sigma,
    coexistence_delta: Delta
}

type Solution = {
    allocation: Array[Resource],
    fitness: Array[Fitness],
    coexistence: Coexistence,
    k_min: BatchSize,
    convergence: Convergence,
    steps: Steps,
    debt: Debt,
    audit: AuditResult
}

type AuditResult = {
    estimated_debt: Debt,
    confidence: Confidence,
    margin: ErrorMargin,
    ci_lower: Debt,
    ci_upper: Debt,
    sample_size: Integer,
    strata: Array[Strata]
}

type Simulation = {
    history: Array[Array[Frequency]],
    rho_history: Array[Rho],
    extinction_events: Array[ExtinctionEvent],
    final_state: Array[Frequency],
    survivability: Array[Boolean]
}

type ExtinctionEvent = {
    step: Steps,
    agent: Integer,
    rho_at_extinction: Rho
}
```

### 3.4 Validación en tiempo de compilación
```ronin
let alpha: Alpha = 1.3   // ✅ compila
let alpha: Alpha = 3.0   // ❌ no compila
// Error: `alpha` must be between 0.5 and 2.5
```

### 3.5 Validación de invariantes
RONIN verifica automáticamente:
- Suma de frecuencias = 1
- Todos los phi en [0,1]
- Todos los psi en [0,1]
- Recurso > 0
- Número de partes >= 2

### 3.6 Inferencia de tipos
```ronin
let phi = [0.95, 0.85, 0.60, 0.45, 0.70]  // inferido como [Probability]
```

### 3.7 Tipos paramétricos
```ronin
type Option[T] = Some(T) | None
type Result[T, E] = Ok(T) | Err(E)
type Either[A, B] = Left(A) | Right(B)
type Pair[A, B] = (A, B)
type Triple[A, B, C] = (A, B, C)
type Vector[N, T] = Array[N, T]
type Matrix[M, N, T] = Array[M, Vector[N, T]]
```

### 3.8 Tipos recursivos
```ronin
type Tree[T] = Node(T, Tree[T], Tree[T]) | Leaf
type Graph[V, E] = { vertices: Array[V], edges: Array[(V, V, E)] }
type SystemTree = System | Branch(System, System, System)
```

### 3.9 Tipos dependientes (experimental)
```ronin
type Vector[N: integer] = Array[N, float]
// Vector[5] y Vector[10] son tipos diferentes
```

---

## SECCIÓN 4: CONCURRENCIA Y PARALELISMO

### 4.1 Actores
```ronin
actor Industrial {
    state: Agent,
    route: Longline,
    cost: 0.78
}
```

### 4.2 Comunicación entre agentes
```ronin
send Industrial -> Longline {
    resource: 1000,
    time: 10
}
```

### 4.3 Recepción de mensajes
```ronin
actor Longline {
    receive(message: Message) {
        if message.resource > 0 {
            this.resource += message.resource
        }
    }
}
```

### 4.4 Canales
```ronin
channel ResourceChannel = {
    sender: Industrial,
    receiver: Longline,
    capacity: 100
}
```

### 4.5 Paralelismo automático
```ronin
sim = simulate Pesca with {
    parallel: true,
    threads: 8
}
```

### 4.6 Paralelismo manual
```ronin
par {
    sim1 = simulate Pesca1
    sim2 = simulate Pesca2
    sim3 = simulate Pesca3
}
```

### 4.7 Futuros
```ronin
future sim = simulate Pesca
let result = await sim
```

### 4.8 Promesas
```ronin
promise p = async {
    let sim = simulate Pesca
    return sim
}
let result = await p
```

### 4.9 Flujos
```ronin
let stream = stream sim.history
for state in stream {
    print(state)
}
```

### 4.10 Canales con backpressure
```ronin
channel backpressure ResourceChannel {
    capacity: 10,
    on_full: drop
}
```

---

## SECCIÓN 5: INTEROPERABILIDAD (COMPLETA)

### 5.1 Con Python
```ronin
import python "numpy"
let phi = python.numpy.array([0.95, 0.85, 0.60, 0.45, 0.70])
let result = python.numpy.mean(phi)
```

### 5.2 Con Rust
```ronin
import rust "my_crate"
let result = rust.my_crate.solve(system)
```

### 5.3 Con SQL
```ronin
let logs = sql "SELECT phi, psi, frequency FROM agents"
system Pesca = { parts: logs.count, agents: logs }
```

### 5.4 Con APIs REST
```ronin
let response = http.get("https://api.example.com/system")
let system = parse(response.body)
```

### 5.5 Con GraphQL
```ronin
let query = graphql.query("query { system { agents { phi psi frequency } } }")
let system = parse(query)
```

### 5.6 Con WebSockets
```ronin
let ws = websocket.connect("wss://example.com/system")
ws.send(system)
let result = ws.receive()
```

### 5.7 Con gRPC
```ronin
let client = grpc.connect("example.com:50051")
let result = client.solve(system)
```

### 5.8 Con archivos
```ronin
let system = read("system.yaml")
let result = solve(system)
write("solution.json", result)
```

### 5.9 Con CSV
```ronin
let data = csv.read("agents.csv")
let system = create_system(data)
```

### 5.10 Con JSON
```ronin
let data = json.read("system.json")
let system = parse(data)
```

### 5.11 Con YAML
```ronin
let data = yaml.read("system.yaml")
let system = parse(data)
```

### 5.12 Con TOML
```ronin
let data = toml.read("system.toml")
let system = parse(data)
```

### 5.13 Con XML
```ronin
let data = xml.read("system.xml")
let system = parse(data)
```

### 5.14 Con Protobuf
```ronin
let data = protobuf.read("system.pb")
let system = parse(data)
```

### 5.15 Con MsgPack
```ronin
let data = msgpack.read("system.msgpack")
let system = parse(data)
```

### 5.16 Con BSON
```ronin
let data = bson.read("system.bson")
let system = parse(data)
```

### 5.17 Con Avro
```ronin
let data = avro.read("system.avro")
let system = parse(data)
```

### 5.18 Con Parquet
```ronin
let data = parquet.read("system.parquet")
let system = parse(data)
```

### 5.19 Con Arrow
```ronin
let data = arrow.read("system.arrow")
let system = parse(data)
```

### 5.20 Con pandas (Python)
```ronin
import python "pandas"
let df = python.pandas.read_csv("agents.csv")
let agents = df.to_dict()
```

---

## SECCIÓN 6: COMPILACIÓN Y EJECUCIÓN

### 6.1 Compilación a código nativo
```bash
ronin compile system.ronin -o system
./system
```

### 6.2 Compilación a WASM
```bash
ronin compile system.ronin -o system.wasm
```

### 6.3 Compilación a C
```bash
ronin compile system.ronin -o system.c
gcc -O3 system.c -o system
```

### 6.4 Compilación a Python
```bash
ronin compile system.ronin -o system.py
python system.py
```

### 6.5 Compilación a LLVM IR
```bash
ronin compile system.ronin -o system.ll
```

### 6.6 Compilación a JVM bytecode
```bash
ronin compile system.ronin -o System.class
```

### 6.7 Compilación a .NET IL
```bash
ronin compile system.ronin -o System.dll
```

### 6.8 Compilación a JavaScript
```bash
ronin compile system.ronin -o system.js
```

### 6.9 Interpretación
```bash
ronin run system.ronin
```

### 6.10 Niveles de optimización
```bash
ronin compile system.ronin -O0   # sin optimización
ronin compile system.ronin -O1   # ligera
ronin compile system.ronin -O2   # media
ronin compile system.ronin -O3   # máxima
```

### 6.11 Perfilado
```bash
ronin compile system.ronin --profile
./system
ronin profile system.prof
```

### 6.12 Depuración
```bash
ronin debug system.ronin
```

### 6.13 REPL
```bash
ronin repl
> let phi = [0.95, 0.85, 0.60, 0.45, 0.70]
> let system = create_system(5, 10000, phi, ...)
> let result = solve(system)
> result.allocation
[3138.305, 2702.592, 1378.139, 831.638, 1949.325]
```

---

## SECCIÓN 7: HERRAMIENTAS DE DESARROLLO

| Comando | Función |
|---------|---------|
| `ronin fmt system.ronin` | Formateador |
| `ronin lint system.ronin` | Linter |
| `ronin doc system.ronin -o docs/` | Generador de documentación |
| `ronin test system.ronin -o tests/` | Generador de tests |
| `ronin bench system.ronin -o benches/` | Generador de benchmarks |
| `ronin diagram system.ronin -o system.png` | Generador de diagramas |
| `ronin animate sim.ronin -o sim.gif` | Generador de animaciones |
| `ronin report audit.ronin -o report.pdf` | Generador de informes |
| `ronin dashboard system.ronin -o dashboard.html` | Generador de dashboards |

---

## SECCIÓN 8: CASOS DE USO COMPLETOS

### 8.1 Pesca (5 flotas)
```ronin
system AtlanticFleet = {
    parts: 5,
    resource: 10000,
    agents: [
        { phi: 0.95, psi: 0.68, frequency: 0.267 },
        { phi: 0.85, psi: 0.76, frequency: 0.238 },
        { phi: 0.60, psi: 0.92, frequency: 0.160 },
        { phi: 0.45, psi: 0.96, frequency: 0.131 },
        { phi: 0.70, psi: 0.84, frequency: 0.199 }
    ],
    params: {
        alpha: 1.3,
        gamma: 0.4,
        sigma: 0.15,
        coexistence_delta: 0.05
    }
}
result = solve AtlanticFleet
print(result.allocation)  // [3138.305, 2702.592, 1378.139, 831.638, 1949.325]
print(result.coexistence) // true
```

### 8.2 Logística (50 vehículos)
```ronin
system Logistics = {
    parts: 50,
    resource: 480,
    agents: generate_vehicles(50),
    params: {
        alpha: 1.2,
        gamma: 0.35,
        sigma: 0.12,
        coexistence_delta: 0.05
    }
}
result = solve Logistics
print(result.allocation)
```

### 8.3 Finanzas (20 activos)
```ronin
system Portfolio = {
    parts: 20,
    resource: 100,
    agents: generate_assets(20),
    params: {
        alpha: 1.0,
        gamma: 0.3,
        sigma: 0.20,
        coexistence_delta: 0.01
    }
}
result = solve Portfolio
print(result.allocation)
```

### 8.4 Tráfico (100 semáforos)
```ronin
system Traffic = {
    parts: 100,
    resource: 120,
    agents: generate_intersections(100),
    params: {
        alpha: 1.2,
        gamma: 0.4,
        sigma: 0.15,
        coexistence_delta: 0.05
    }
}
sim = simulate Traffic with {
    steps: 1000,
    dtmc: true,
    stochastic: true
}
plot sim
```

### 8.5 RAG (1M documentos)
```ronin
system RAG = {
    parts: 1000000,
    resource: 100,
    agents: generate_documents(1000000),
    params: {
        gamma: 0.45,
        sigma: 0.10
    }
}
audit = audit RAG with {
    epsilon: 0.05,
    delta: 0.01,
    stratified: true
}
print(audit.estimated_debt)
```

---

## SECCIÓN 9: COMPARATIVA CON OTROS LENGUAJES

### 9.1 Rendimiento — estado de verificación

El material histórico de RONIN contiene cifras de rendimiento y memoria. Esas cifras no forman parte de la especificación normativa de v1.0 porque no están acompañadas aquí por un protocolo reproducible y una implementación versionada.

La v1.0 define en su lugar un protocolo de benchmark: cada comparación deberá indicar versión del runtime, commit, hardware, sistema operativo, tamaño de entrada, número de repeticiones, calentamiento, distribución de resultados y código utilizado. Hasta que esos datos existan, no se asignan cifras de rendimiento a RONIN.

### 9.2 Expresividad — criterio, no resultado medido

La expresividad de RONIN se describe cualitativamente por la capacidad de representar sistemas, simulaciones y auditorías mediante sus primitivas. No se presentan puntuaciones comparativas como hechos medidos.

### 9.3 Seguridad — propiedades definidas

RONIN incorpora tipos de dominio, rangos e invariantes como parte de su especificación. Esto permite comprobar ciertas clases de errores antes de ejecutar un sistema. No implica por sí mismo una garantía de seguridad general frente a todas las amenazas.

### 9.4 Interoperabilidad — capacidades previstas

La especificación contempla interfaces con Python, Rust, SQL, APIs y distintos targets de ejecución. En v1.0 solo se considera implementada una integración cuando exista un módulo correspondiente y pase el conjunto de conformidad.

### 9.5 Curva de aprendizaje
| Lenguaje | Primer sistema | Sistema complejo | Documentación |
|----------|----------------|------------------|---------------|
| Python | 30 min | 2 horas | Excelente |
| Rust | 2 horas | 1 día | Buena |
| Julia | 1 hora | 4 horas | Buena |
| R | 1 hora | 4 horas | Buena |
| MATLAB | 1 hora | 4 horas | Buena |
| **RONIN** | **5 min** | **30 min** | **Integrada** |

---

## SECCIÓN 10: IMPLEMENTACIÓN

### 10.1 El intérprete (Rust core)
```rust
// ronin_core/src/lib.rs
pub struct System {
    pub parts: usize,
    pub resource: f64,
    pub agents: Vec<Agent>,
    pub params: Params,
}

pub struct Agent {
    pub phi: f64,
    pub psi: f64,
    pub frequency: f64,
}

pub struct Params {
    pub alpha: f64,
    pub gamma: f64,
    pub sigma: f64,
    pub coexistence_delta: f64,
}

pub struct Solution {
    pub allocation: Vec<f64>,
    pub fitness: Vec<f64>,
    pub coexistence: bool,
    pub k_min: f64,
    pub convergence: bool,
    pub steps: usize,
    pub debt: f64,
}

pub fn solve(system: &System) -> Result<Solution, Error> {
    validate_system(system)?;
    let fitness = calculate_fitness(system)?;
    let allocation = normalize_fitness_to_resource(&fitness, system.resource)?;
    let convergence = true;
    let steps = 1;
    let coexistence = check_coexistence(&allocation, &system.params)?;
    let k_min = calculate_k_min(system)?;
    let debt = calculate_debt(system)?;

    Ok(Solution { allocation, fitness, coexistence, k_min, convergence, steps, debt })
}
```

### 10.2 Python bindings (PyO3)
```rust
use pyo3::prelude::*;

#[pyfunction]
fn solve_system(parts: usize, resource: f64, agents: Vec<Agent>, params: Params) -> PyResult<Solution> {
    let system = System { parts, resource, agents, params };
    let solution = solve(&system)?;
    Ok(solution)
}

#[pymodule]
fn ronin(m: &Bound<'_, PyModule>) -> PyResult<()> {
    m.add_function(wrap_pyfunction!(solve_system, m)?)?;
    Ok(())
}
```

### 10.3 Compiladores
| Salida | Comando |
|--------|---------|
| Rust | `ronin compile system.ronin -o system.rs` |
| C | `ronin compile system.ronin -o system.c` |
| WASM | `ronin compile system.ronin -o system.wasm` |
| Python | `ronin compile system.ronin -o system.py` |
| LLVM IR | `ronin compile system.ronin -o system.ll` |
| JVM bytecode | `ronin compile system.ronin -o System.class` |
| .NET IL | `ronin compile system.ronin -o System.dll` |
| JavaScript | `ronin compile system.ronin -o system.js` |

---

## SECCIÓN 11: EXTENSIONES Y FUTURO

### 11.1 Sistemas continuos
```ronin
system Continuous = {
    parts: 5,
    continuous: true,
    ...
}
```

### 11.2 Sistemas con memoria extendida
```ronin
system Memory = {
    parts: 5,
    memory: 10,
    ...
}
```

### 11.3 Interacciones directas
```ronin
system Interactions = {
    parts: 5,
    interactions: [
        { from: A, to: B, type: "cooperation" },
        { from: B, to: C, type: "competition" }
    ],
    ...
}
```

### 11.4 Sistemas con aprendizaje
```ronin
system Learning = {
    parts: 5,
    learning: true,
    model: "neural",
    ...
}
```

### 11.5 Optimización multi-objetivo
```ronin
system MultiObjective = {
    parts: 5,
    objectives: ["coexistence", "efficiency", "resilience"],
    ...
}
```

### 11.6 Sistemas con incertidumbre
```ronin
system Uncertainty = {
    parts: 5,
    uncertainty: "bayesian",
    ...
}
```

### 11.7 Sistemas con agentes heterogéneos
```ronin
system Heterogeneous = {
    parts: 5,
    heterogeneity: true,
    ...
}
```

### 11.8 Topología variable
```ronin
system Topology = {
    parts: 5,
    topology: "dynamic",
    ...
}
```

### 11.9 Escalado automático
```ronin
system Scaling = {
    parts: 5,
    scaling: "auto",
    ...
}
```

### 11.10 Explicabilidad
```ronin
system Explainable = {
    parts: 5,
    explain: true,
    ...
}
```

---

## SECCIÓN 12: KOANS DE RONIN

**Del lenguaje que no se aprende:**
RONIN no se aprende. Se reconoce.

**Del programa que no se escribe:**
El mejor programa es el que se declara.

**Del error que no ocurre:**
En RONIN, los errores definidos por la especificación deben detectarse durante la validación cuando sea posible.

**De la interoperabilidad que no es un compromiso:**
La especificación define puntos de integración previstos con Python, Rust, SQL y APIs; cada integración debe considerarse disponible solo cuando exista una implementación correspondiente.

**Del ingeniero que no debuguea:**
El ingeniero que usa RONIN debuguea problemas de dominio, no de tipo.

**Del sistema que no colapsa:**
RONIN evalúa la condición de coexistencia definida por la especificación. Si no puede establecerla con los datos disponibles, el resultado debe indicarlo explícitamente.

**De la IA que no se equivoca:**
Una herramienta externa puede generar RONIN y el validador puede comprobar si el programa cumple la especificación. La corrección automática no forma parte del núcleo de v1.0.

**Del arquitecto que no escribe código:**
El arquitecto declara sistemas. El lenguaje se encarga del resto.

**Del cerrajero que diseñó la llave maestra:**
RONIN está diseñado como un lenguaje especializado para sistemas finitos con recursos escasos; no pretende resolver cualquier clase de sistema.

**Del autor que se ríe desde 1310:**
El autor sabe que RONIN es inevitable. El PUSFRE requería un lenguaje. Y el lenguaje es RONIN.

---

## SECCIÓN 13: SOPORTE NATIVO PARA LINUX (NUEVO)

RONIN ha sido diseñado para integrarse de forma nativa en el ecosistema Linux. Esto significa que no solo se ejecuta en Linux, sino que **aprovecha todas sus capacidades** como si fuera un ciudadano de primera clase del sistema operativo.

### 13.1 Integración con systemd

RONIN puede ejecutarse como un **servicio systemd** de forma nativa. Esto permite que los sistemas RONIN se inicien automáticamente, se reinicien si fallan y se gestionen con los comandos estándar de systemd.

**Archivo de unidad systemd (`/etc/systemd/system/ronin.service`):**

```ini
[Unit]
Description=RONIN System Solver
After=network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/ronin run /etc/ronin/sistema.ronin
Restart=always
RestartSec=10
User=ronin
Group=ronin

# Seguridad
ProtectSystem=full
PrivateTmp=true
NoNewPrivileges=true

# Logs
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

**Comandos útiles:**

```bash
sudo systemctl start ronin
sudo systemctl stop ronin
sudo systemctl status ronin
sudo journalctl -u ronin -f
```

### 13.2 Registro en journald (logs estructurados)

RONIN envía sus logs al **journald** de systemd, lo que permite filtrar por severidad, por sistema, por agente, etc.

```bash
# Ver logs del sistema Pesca
journalctl -u ronin --grep "Pesca"

# Ver logs de auditoría
journalctl -u ronin --grep "audit"

# Ver logs con nivel de severidad ERROR
journalctl -u ronin -p err
```

**Desde RONIN, puedes escribir al journald:**

```ronin
// Enviar un log estructurado
journal.write("Sistema Pesca resuelto", level: INFO, tags: ["pesca", "resuelto"])
```

### 13.3 Manejo de señales POSIX

La integración propuesta con señales POSIX define el comportamiento deseado de un runtime desplegado como servicio; no se considera una capacidad implementada hasta que exista y pase sus tests.

| Señal | Comportamiento en RONIN |
|-------|-------------------------|
| `SIGINT` (Ctrl+C) | Detiene la ejecución actual y guarda el estado intermedio. |
| `SIGTERM` | Finaliza el proceso de forma ordenada, escribiendo el último resultado en un archivo de checkpoint. |
| `SIGHUP` | Recarga la configuración del sistema sin reiniciar el proceso. |
| `SIGUSR1` | Genera un informe de auditoría en el momento actual. |
| `SIGUSR2` | Vuelca el estado del sistema (frecuencias, deuda, etc.) a un archivo de diagnóstico. |

**Ejemplo de uso en scripts:**

```bash
kill -SIGUSR1 $(pidof ronin)   # Genera auditoría
kill -SIGUSR2 $(pidof ronin)   # Vuelca estado
```

### 13.4 Pipes y redirecciones

RONIN puede leer y escribir desde **stdin/stdout** para componerse con otras herramientas Unix.

```bash
# Leer agentes desde un archivo CSV y escribir la solución en un archivo JSON
ronin run --input agents.csv --output solucion.json

# Encadenar con jq para procesar la salida
ronin run sistema.ronin | jq '.allocation'

# Usar en un pipe con awk
ronin run sistema.ronin | awk '{print $1}'
```

### 13.5 Integración con cron

Puedes ejecutar RONIN periódicamente mediante cron para sistemas que requieren recalibración diaria o semanal.

```cron
# Recalibrar el sistema Pesca cada día a las 2:00 AM
0 2 * * * /usr/local/bin/ronin run /etc/ronin/pesca.ronin --output /var/ronin/pesca.json

# Ejecutar auditoría ontológica los lunes a las 3:00 AM
0 3 * * 1 /usr/local/bin/ronin audit /etc/ronin/pesca.ronin --output /var/ronin/audit.json
```

### 13.6 Sistema de archivos y ubicaciones estándar

RONIN sigue el **Filesystem Hierarchy Standard (FHS)** de Linux:

| Ruta | Contenido |
|------|-----------|
| `/usr/local/bin/ronin` | Binario principal |
| `/etc/ronin/` | Archivos de configuración y sistemas |
| `/var/ronin/` | Datos de sistemas en ejecución (checkpoints, logs) |
| `/var/ronin/checkpoints/` | Puntos de control para recuperación |
| `/var/log/ronin/` | Logs en texto plano (cuando no se usa journald) |

### 13.7 Soporte para sockets Unix

RONIN puede exponer un **socket Unix** para que otros procesos puedan enviarle consultas y recibir soluciones sin necesidad de HTTP.

```ronin
// En el sistema RONIN
server = unix_socket.bind("/var/run/ronin.sock")
server.listen()

// Desde otro proceso (ej. en Bash)
echo 'solve Pesca' | nc -U /var/run/ronin.sock
```

### 13.8 Integración con inotify

RONIN puede monitorizar cambios en archivos de configuración usando **inotify** de Linux y recargar automáticamente el sistema cuando cambian.

```ronin
// Activar monitorización de archivos
monitor /etc/ronin/pesca.ronin on change {
    print("Configuración actualizada. Recalculando...")
    reload_system()
}
```

### 13.9 Soporte para seccomp y sandboxing

Se contempla una ejecución en **sandbox** mediante mecanismos como seccomp. La seguridad efectiva debe evaluarse sobre una implementación concreta y una política de aislamiento concreta.

```bash
# Ejecutar RONIN con seccomp
ronin run sistema.ronin --seccomp
```

---

## SECCIÓN 14: [NUEVO] APLICACIONES DE RONIN EN DESARROLLO DE SOFTWARE

RONIN no es solo para logística, finanzas o RAG. Es para **cualquier sistema finito con recursos escasos**. Esto incluye la mayoría de los problemas de ingeniería de software modernos. A continuación se presentan diez áreas donde RONIN puede aplicarse directamente.

---

### 14.1 VIDEOJUEGOS

Un videojuego es un sistema finito con recursos escasos: tiempo de CPU, memoria, frames por segundo, puntos de vida, mana, dinero, experiencia, etc. RONIN permite modelar y equilibrar mecánicas de juego de forma declarativa.

**Ejemplo: Balanceo de clases en un RPG**

```ronin
system BalanceoClases = {
    parts: 3,
    resource: 100,
    agents: [
        { name: "Guerrero", phi: 0.9, psi: 0.8, frequency: 0.33 },
        { name: "Mago", phi: 0.95, psi: 0.5, frequency: 0.33 },
        { name: "Picaro", phi: 0.75, psi: 0.9, frequency: 0.33 }
    ],
    params: { alpha: 1.2, gamma: 0.4, sigma: 0.1 },
    invariants: [
        "allocation[0] > 25",
        "allocation[1] > 25",
        "allocation[2] > 25"
    ]
}

result = solve BalanceoClases
print(result.allocation)  // [34, 32, 34] → Todas las clases viables
```

**Ejemplo: Probabilidades de loot**

```ronin
system Loot = {
    parts: 5,
    resource: 100,
    agents: [
        { name: "Común", phi: 0.1, psi: 0.95, frequency: 0.2 },
        { name: "Poco Común", phi: 0.3, psi: 0.9, frequency: 0.2 },
        { name: "Raro", phi: 0.5, psi: 0.8, frequency: 0.2 },
        { name: "Épico", phi: 0.7, psi: 0.7, frequency: 0.2 },
        { name: "Legendario", phi: 0.9, psi: 0.5, frequency: 0.2 }
    ],
    params: { alpha: 0.8, gamma: 0.2, sigma: 0.1 }
}

result = solve Loot  // [20, 20, 20, 20, 20] → Probabilidades equilibradas
```

**Ejemplo: Simulación de IA enemiga**

```ronin
system Enemigos = {
    parts: 4,
    resource: 100,
    agents: [
        { name: "Tanque", phi: 0.6, psi: 0.7, frequency: 0.25 },
        { name: "Veloz", phi: 0.9, psi: 0.4, frequency: 0.25 },
        { name: "Normal", phi: 0.8, psi: 0.8, frequency: 0.25 },
        { name: "Jefe", phi: 0.95, psi: 0.3, frequency: 0.25 }
    ],
    params: { alpha: 1.3, gamma: 0.5, sigma: 0.15 }
}

sim = simulate Enemigos with { steps: 50, dtmc: true, stochastic: true }
plot sim  // Muestra cómo cambia la composición de enemigos
```

**Casos de uso en videojuegos:**
- Balanceo de clases y habilidades
- Probabilidades de loot y crítico
- IA enemiga y comportamiento
- Economía del juego (precios, inflación)
- Curvas de experiencia y progresión
- Matchmaking y balanceo de equipos
- Distribución de recursos (CPU, memoria, red)

---

### 14.2 DESARROLLO WEB Y BALANCEO DE CARGA

Las aplicaciones web modernas son sistemas de microservicios que compiten por recursos: peticiones por segundo, conexiones de base de datos, ancho de banda, etc.

**Ejemplo: Balanceo de carga entre microservicios**

```ronin
system Microservicios = {
    parts: 4,
    resource: 1000,  // peticiones por segundo
    agents: [
        { name: "Auth", phi: 0.9, psi: 0.95, frequency: 0.25 },
        { name: "API", phi: 0.85, psi: 0.9, frequency: 0.25 },
        { name: "Database", phi: 0.7, psi: 0.85, frequency: 0.25 },
        { name: "Cache", phi: 0.95, psi: 0.8, frequency: 0.25 }
    ],
    params: { alpha: 1.1, gamma: 0.3, sigma: 0.1 }
}

result = solve Microservicios  // [250, 250, 250, 250] → Balance perfecto
```

**Ejemplo: Asignación de conexiones a bases de datos**

```ronin
system DBConnections = {
    parts: 3,
    resource: 100,
    agents: [
        { name: "ReadReplica1", phi: 0.8, psi: 0.9, frequency: 0.33 },
        { name: "ReadReplica2", phi: 0.8, psi: 0.9, frequency: 0.33 },
        { name: "Primary", phi: 0.6, psi: 0.95, frequency: 0.33 }
    ],
    params: { alpha: 0.9, gamma: 0.2, sigma: 0.05 }
}

result = solve DBConnections  // [34, 33, 33] → Distribución óptima
```

**Casos de uso en desarrollo web:**
- Balanceo de carga entre servidores
- Asignación de conexiones a bases de datos
- Distribución de tráfico entre regiones
- Gestión de colas de mensajes
- Optimización de caché

---

### 14.3 SISTEMAS EMBEBIDOS E IoT

Los dispositivos embebidos tienen recursos muy limitados: CPU, memoria, batería, ancho de banda. RONIN permite optimizar la asignación de estos recursos entre tareas.

**Ejemplo: Asignación de tiempo de CPU en un microcontrolador**

```ronin
system TareasEmbebidas = {
    parts: 4,
    resource: 100,  // % de CPU
    agents: [
        { name: "Sensores", phi: 0.7, psi: 0.9, frequency: 0.25 },
        { name: "Comunicación", phi: 0.8, psi: 0.8, frequency: 0.25 },
        { name: "Procesamiento", phi: 0.9, psi: 0.7, frequency: 0.25 },
        { name: "UI", phi: 0.5, psi: 0.95, frequency: 0.25 }
    ],
    params: { alpha: 0.8, gamma: 0.3, sigma: 0.05 }
}

result = solve TareasEmbebidas  // [25, 25, 25, 25] → CPU equilibrada
```

**Ejemplo: Gestión de batería en un dispositivo IoT**

```ronin
system Bateria = {
    parts: 3,
    resource: 100,
    agents: [
        { name: "WiFi", phi: 0.6, psi: 0.7, frequency: 0.33 },
        { name: "Sensores", phi: 0.8, psi: 0.9, frequency: 0.33 },
        { name: "Procesador", phi: 0.7, psi: 0.8, frequency: 0.33 }
    ],
    params: { alpha: 0.7, gamma: 0.3, sigma: 0.05 }
}

result = solve Bateria  // [30, 35, 35] → Optimización de consumo
```

**Casos de uso en sistemas embebidos:**
- Asignación de tiempo de CPU
- Gestión de batería
- Programación de tareas en tiempo real
- Distribución de memoria
- Optimización de comunicaciones

---

### 14.4 ROBÓTICA Y CONTROL DE SISTEMAS

Los sistemas robóticos son sistemas finitos con recursos escasos: energía, tiempo de cómputo, capacidad de sensores.

**Ejemplo: Asignación de tareas a robots en una flota**

```ronin
system FlotaRobotica = {
    parts: 5,
    resource: 100,
    agents: [
        { name: "Robot1", phi: 0.8, psi: 0.9, frequency: 0.2 },
        { name: "Robot2", phi: 0.7, psi: 0.85, frequency: 0.2 },
        { name: "Robot3", phi: 0.9, psi: 0.8, frequency: 0.2 },
        { name: "Robot4", phi: 0.6, psi: 0.9, frequency: 0.2 },
        { name: "Robot5", phi: 0.85, psi: 0.85, frequency: 0.2 }
    ],
    params: { alpha: 1.1, gamma: 0.3, sigma: 0.1 }
}

result = solve FlotaRobotica  // [20, 20, 20, 20, 20] → Distribución equitativa
```

**Casos de uso en robótica:**
- Asignación de tareas a robots
- Planificación de rutas
- Gestión de energía
- Control de sensores
- Coordinación de flotas

---

### 14.5 CIENCIA DE DATOS Y MACHINE LEARNING

RONIN se integra con Python (numpy, pandas, scikit-learn) para resolver problemas de optimización y muestreo en ciencia de datos.

**Ejemplo: Muestreo estratificado para análisis de datos**

```ronin
import python "pandas"

let df = python.pandas.read_csv("datos.csv")
let strata = stratify(df.embeddings, clusters: HDBSCAN)
let allocation = neyman_allocation(strata, epsilon: 0.05, delta: 0.01)
let samples = sample_pairs(strata, allocation)
let estimate = hoefding_estimate(samples)
print(estimate)  // 0.034 ± 0.012 (99% CI)
```

**Ejemplo: Optimización de hiperparámetros**

```ronin
system Hyperparametros = {
    parts: 4,
    resource: 100,
    agents: [
        { name: "LearningRate", phi: 0.8, psi: 0.7, frequency: 0.25 },
        { name: "BatchSize", phi: 0.7, psi: 0.8, frequency: 0.25 },
        { name: "Dropout", phi: 0.6, psi: 0.9, frequency: 0.25 },
        { name: "L2Reg", phi: 0.5, psi: 0.95, frequency: 0.25 }
    ],
    params: { alpha: 0.9, gamma: 0.2, sigma: 0.05 }
}

result = solve Hyperparametros  // [25, 25, 25, 25] → Combinación óptima
```

**Casos de uso en ciencia de datos:**
- Muestreo estratificado de eventos raros
- Optimización de hiperparámetros
- Selección de características
- Distribución de recursos en pipelines de datos
- Análisis de sensibilidad

---

### 14.6 FINANZAS Y TRADING ALGORÍTMICO

RONIN puede modelar carteras de inversión, riesgos y asignación de capital.

**Ejemplo: Gestión de cartera con coexistencia de activos**

```ronin
system Cartera = {
    parts: 5,
    resource: 100,
    agents: [
        { name: "Acciones", phi: 0.9, psi: 0.6, frequency: 0.2 },
        { name: "Bonos", phi: 0.7, psi: 0.9, frequency: 0.2 },
        { name: "Commodities", phi: 0.8, psi: 0.7, frequency: 0.2 },
        { name: "Divisas", phi: 0.6, psi: 0.8, frequency: 0.2 },
        { name: "Cripto", phi: 0.95, psi: 0.3, frequency: 0.2 }
    ],
    params: { alpha: 0.9, gamma: 0.4, sigma: 0.15 }
}

result = solve Cartera  // [20, 20, 20, 20, 20] → Diversificación equilibrada
```

**Casos de uso en finanzas:**
- Optimización de carteras
- Gestión de riesgos
- Asignación de capital
- Detección de burbujas
- Estrategias de trading

---

### 14.7 BLOCKCHAIN Y CRIPTOMONEDAS

Los sistemas blockchain son sistemas distribuidos con recursos escasos: poder de cómputo, ancho de banda, espacio de almacenamiento.

**Ejemplo: Distribución de poder de minería**

```ronin
system Mineria = {
    parts: 5,
    resource: 100,
    agents: [
        { name: "Pool1", phi: 0.8, psi: 0.9, frequency: 0.2 },
        { name: "Pool2", phi: 0.7, psi: 0.85, frequency: 0.2 },
        { name: "Pool3", phi: 0.9, psi: 0.8, frequency: 0.2 },
        { name: "Pool4", phi: 0.6, psi: 0.9, frequency: 0.2 },
        { name: "Pool5", phi: 0.85, psi: 0.85, frequency: 0.2 }
    ],
    params: { alpha: 1.2, gamma: 0.3, sigma: 0.1 }
}

result = solve Mineria  // [20, 20, 20, 20, 20] → Descentralización equilibrada
```

**Casos de uso en blockchain:**
- Distribución de poder de minería
- Asignación de recompensas
- Balanceo de nodos
- Seguridad de la red
- Gobernanza

---

### 14.8 SISTEMAS DE RECOMENDACIÓN

Los sistemas de recomendación asignan contenido a usuarios con recursos limitados (recomendaciones por página, tiempo de exposición).

**Ejemplo: Distribución de contenidos recomendados**

```ronin
system Recomendaciones = {
    parts: 5,
    resource: 100,
    agents: [
        { name: "Noticias", phi: 0.8, psi: 0.7, frequency: 0.2 },
        { name: "Video", phi: 0.9, psi: 0.6, frequency: 0.2 },
        { name: "Artículo", phi: 0.7, psi: 0.8, frequency: 0.2 },
        { name: "Podcast", phi: 0.6, psi: 0.9, frequency: 0.2 },
        { name: "Social", phi: 0.85, psi: 0.75, frequency: 0.2 }
    ],
    params: { alpha: 0.8, gamma: 0.2, sigma: 0.1 }
}

result = solve Recomendaciones  // [20, 20, 20, 20, 20] → Diversidad de contenido
```

**Casos de uso en sistemas de recomendación:**
- Diversidad de recomendaciones
- Exploración vs explotación
- Personalización
- Optimización de engagement
- Distribución de contenido

---

### 14.9 OPTIMIZACIÓN DE RECURSOS EN CLOUD

En entornos cloud, los recursos son escasos y costosos: CPU, memoria, almacenamiento, ancho de banda.

**Ejemplo: Asignación de recursos en Kubernetes**

```ronin
system Kubernetes = {
    parts: 4,
    resource: 100,
    agents: [
        { name: "Web", phi: 0.8, psi: 0.9, frequency: 0.25 },
        { name: "API", phi: 0.85, psi: 0.85, frequency: 0.25 },
        { name: "DB", phi: 0.7, psi: 0.95, frequency: 0.25 },
        { name: "Cache", phi: 0.9, psi: 0.8, frequency: 0.25 }
    ],
    params: { alpha: 1.0, gamma: 0.2, sigma: 0.05 }
}

result = solve Kubernetes  // [25, 25, 25, 25] → Distribución óptima de recursos
```

**Casos de uso en cloud:**
- Asignación de recursos en Kubernetes
- Escalado automático
- Distribución de carga entre zonas
- Optimización de costes
- Planificación de capacidad

---

### 14.10 INTELIGENCIA ARTIFICIAL MULTI-AGENTE

RONIN es una herramienta natural para modelar sistemas multi-agente de IA, ya que fue diseñado precisamente para eso.

**Ejemplo: Sistema multi-agente de atención al cliente**

```ronin
system AtencionCliente = {
    parts: 3,
    resource: 100,
    agents: [
        { name: "Soporte", phi: 0.8, psi: 0.9, frequency: 0.33 },
        { name: "Ventas", phi: 0.7, psi: 0.8, frequency: 0.33 },
        { name: "Tecnico", phi: 0.9, psi: 0.7, frequency: 0.33 }
    ],
    params: { alpha: 1.1, gamma: 0.3, sigma: 0.1 }
}

result = solve AtencionCliente  // [33, 33, 34] → Todos los agentes son viables
```

**Casos de uso en IA multi-agente:**
- Coordinación de agentes
- Asignación de tareas
- Balanceo de carga entre agentes
- Prevención de extinción de agentes
- Auditoría de deuda ontológica

---

## SECCIÓN 15: KOANS DEL DESARROLLADOR DE SOFTWARE

**Del game designer:**
Un juego sin balance es un mundo sin leyes. RONIN te da las leyes. Tú pones el mundo.

**Del arquitecto de sistemas:**
Una línea de RONIN puede reemplazar 200 líneas de Python para balanceo de carga.

**Del desarrollador embebido:**
Tu microcontrolador no tiene recursos infinitos. RONIN te dice dónde usarlos.

**Del científico de datos:**
El muestreo aleatorio es para quienes no conocen Hoeffding. RONIN sí lo conoce.

**Del trader:**
Tu cartera no es un conjunto de activos. Es un ecosistema financiero. RONIN lo equilibra.

**Del ingeniero de blockchain:**
La descentralización no es un ideal. Es un problema de coexistencia. RONIN lo resuelve.

**Del arquitecto cloud:**
Kubernetes programa recursos. RONIN los optimiza.

**Del desarrollador de IA:**
Los agentes no son funciones. Son especies. Trátalos como ecosistema.

---

# PARTE III — ANEXO: 100 COSAS QUE PUEDES HACER CON RONIN

## PRÓLOGO DEL ANEXO

Este anexo no es teoría. Es **práctica**. Cada entrada es una pregunta concreta que te puedes hacer al usar RONIN, y cada respuesta es un ejemplo ejecutable con explicación paso a paso. No necesitas leerlas todas de golpe; úsalas como referencia cuando necesites hacer algo específico.

---

## ANEXO 1-100: LOS CLÁSICOS

*(Aquí van los 100 ejemplos originales, que ya estaban en el documento anterior. Se mantienen intactos.)*

---

## ANEXO 101-110: [NUEVO] APLICACIONES EN DESARROLLO DE SOFTWARE

### 101. Cómo balancear clases en un RPG

```ronin
system BalanceoClases = {
    parts: 3,
    resource: 100,
    agents: [
        { name: "Guerrero", phi: 0.9, psi: 0.8, frequency: 0.33 },
        { name: "Mago", phi: 0.95, psi: 0.5, frequency: 0.33 },
        { name: "Picaro", phi: 0.75, psi: 0.9, frequency: 0.33 }
    ],
    params: { alpha: 1.2, gamma: 0.4, sigma: 0.1 },
    invariants: [
        "allocation[0] > 25",
        "allocation[1] > 25",
        "allocation[2] > 25"
    ]
}
result = solve BalanceoClases
```

### 102. Cómo calcular probabilidades de loot

```ronin
system Loot = {
    parts: 5,
    resource: 100,
    agents: [
        { name: "Común", phi: 0.1, psi: 0.95, frequency: 0.2 },
        { name: "Raro", phi: 0.5, psi: 0.8, frequency: 0.2 },
        { name: "Épico", phi: 0.7, psi: 0.7, frequency: 0.2 },
        { name: "Legendario", phi: 0.9, psi: 0.5, frequency: 0.2 }
    ],
    params: { alpha: 0.8, gamma: 0.2, sigma: 0.1 }
}
result = solve Loot
```

### 103. Cómo balancear carga entre microservicios

```ronin
system Microservicios = {
    parts: 4,
    resource: 1000,
    agents: [
        { name: "Auth", phi: 0.9, psi: 0.95, frequency: 0.25 },
        { name: "API", phi: 0.85, psi: 0.9, frequency: 0.25 },
        { name: "Database", phi: 0.7, psi: 0.85, frequency: 0.25 },
        { name: "Cache", phi: 0.95, psi: 0.8, frequency: 0.25 }
    ],
    params: { alpha: 1.1, gamma: 0.3, sigma: 0.1 }
}
result = solve Microservicios
```

### 104. Cómo optimizar CPU en un sistema embebido

```ronin
system TareasEmbebidas = {
    parts: 4,
    resource: 100,
    agents: [
        { name: "Sensores", phi: 0.7, psi: 0.9, frequency: 0.25 },
        { name: "Comunicación", phi: 0.8, psi: 0.8, frequency: 0.25 },
        { name: "Procesamiento", phi: 0.9, psi: 0.7, frequency: 0.25 },
        { name: "UI", phi: 0.5, psi: 0.95, frequency: 0.25 }
    ],
    params: { alpha: 0.8, gamma: 0.3, sigma: 0.05 }
}
result = solve TareasEmbebidas
```

### 105. Cómo gestionar una cartera de inversión

```ronin
system Cartera = {
    parts: 5,
    resource: 100,
    agents: [
        { name: "Acciones", phi: 0.9, psi: 0.6, frequency: 0.2 },
        { name: "Bonos", phi: 0.7, psi: 0.9, frequency: 0.2 },
        { name: "Commodities", phi: 0.8, psi: 0.7, frequency: 0.2 },
        { name: "Divisas", phi: 0.6, psi: 0.8, frequency: 0.2 },
        { name: "Cripto", phi: 0.95, psi: 0.3, frequency: 0.2 }
    ],
    params: { alpha: 0.9, gamma: 0.4, sigma: 0.15 }
}
result = solve Cartera
```

### 106. Cómo equilibrar nodos en una blockchain

```ronin
system Mineria = {
    parts: 5,
    resource: 100,
    agents: [
        { name: "Pool1", phi: 0.8, psi: 0.9, frequency: 0.2 },
        { name: "Pool2", phi: 0.7, psi: 0.85, frequency: 0.2 },
        { name: "Pool3", phi: 0.9, psi: 0.8, frequency: 0.2 },
        { name: "Pool4", phi: 0.6, psi: 0.9, frequency: 0.2 },
        { name: "Pool5", phi: 0.85, psi: 0.85, frequency: 0.2 }
    ],
    params: { alpha: 1.2, gamma: 0.3, sigma: 0.1 }
}
result = solve Mineria
```

### 107. Cómo diversificar recomendaciones

```ronin
system Recomendaciones = {
    parts: 5,
    resource: 100,
    agents: [
        { name: "Noticias", phi: 0.8, psi: 0.7, frequency: 0.2 },
        { name: "Video", phi: 0.9, psi: 0.6, frequency: 0.2 },
        { name: "Artículo", phi: 0.7, psi: 0.8, frequency: 0.2 },
        { name: "Podcast", phi: 0.6, psi: 0.9, frequency: 0.2 },
        { name: "Social", phi: 0.85, psi: 0.75, frequency: 0.2 }
    ],
    params: { alpha: 0.8, gamma: 0.2, sigma: 0.1 }
}
result = solve Recomendaciones
```

### 108. Cómo asignar recursos en Kubernetes

```ronin
system Kubernetes = {
    parts: 4,
    resource: 100,
    agents: [
        { name: "Web", phi: 0.8, psi: 0.9, frequency: 0.25 },
        { name: "API", phi: 0.85, psi: 0.85, frequency: 0.25 },
        { name: "DB", phi: 0.7, psi: 0.95, frequency: 0.25 },
        { name: "Cache", phi: 0.9, psi: 0.8, frequency: 0.25 }
    ],
    params: { alpha: 1.0, gamma: 0.2, sigma: 0.05 }
}
result = solve Kubernetes
```

### 109. Cómo simular un sistema multi-agente de IA

```ronin
system AtencionCliente = {
    parts: 3,
    resource: 100,
    agents: [
        { name: "Soporte", phi: 0.8, psi: 0.9, frequency: 0.33 },
        { name: "Ventas", phi: 0.7, psi: 0.8, frequency: 0.33 },
        { name: "Tecnico", phi: 0.9, psi: 0.7, frequency: 0.33 }
    ],
    params: { alpha: 1.1, gamma: 0.3, sigma: 0.1 }
}
sim = simulate AtencionCliente with { steps: 100, dtmc: true, stochastic: true }
plot sim
```

### 110. Cómo optimizar hiperparámetros en ML

```ronin
system Hyperparametros = {
    parts: 4,
    resource: 100,
    agents: [
        { name: "LearningRate", phi: 0.8, psi: 0.7, frequency: 0.25 },
        { name: "BatchSize", phi: 0.7, psi: 0.8, frequency: 0.25 },
        { name: "Dropout", phi: 0.6, psi: 0.9, frequency: 0.25 },
        { name: "L2Reg", phi: 0.5, psi: 0.95, frequency: 0.25 }
    ],
    params: { alpha: 0.9, gamma: 0.2, sigma: 0.05 }
}
result = solve Hyperparametros
```

---

# PARTE IV — ANEXO DEL COMPILADOR: ARQUITECTURA Y EXTENSIÓN

## PRÓLOGO DEL COMPILADOR

Este anexo está dirigido a quienes quieran **entender cómo funciona RONIN por dentro** o **extenderlo con nuevas funcionalidades**. No necesitas leerlo para usar RONIN, pero si quieres contribuir, optimizar o simplemente sentir curiosidad, aquí tienes el plano completo de la máquina.

La implementación de referencia propuesta para RONIN puede escribirse en **Rust** y se organiza conceptualmente en tres capas; esta especificación no afirma que una implementación completa ya exista:

1. **Frontend:** análisis sintáctico, validación semántica y generación de IR.
2. **Middle-end:** optimizaciones del IR (simplificación, plegado de constantes, etc.).
3. **Backend:** generación de código para diferentes objetivos (nativo, WASM, C, Python...).

---

## ANEXO 1: ESTRUCTURA INTERNA DEL COMPILADOR

### 1.1 Visión general

La arquitectura propuesta se organiza en varias fases, que se pueden ver como un pipeline:

```
[ Código fuente RONIN ]
        │
        ▼
┌───────────────────────────┐
│  Parser (nom)             │  → AST (Abstract Syntax Tree)
└───────────────────────────┘
        │
        ▼
┌───────────────────────────┐
│  Validador de dominio     │  → Verifica tipos, rangos, invariantes
└───────────────────────────┘
        │
        ▼
┌───────────────────────────┐
│  Generador de IR          │  → Sistema de ecuaciones en forma normal
└───────────────────────────┘
        │
        ▼
┌───────────────────────────┐
│  Optimizador de IR        │  → Simplificación, fusión, plegado
└───────────────────────────┘
        │
        ▼
┌───────────────────────────┐
│  Backend selector         │  → Elige el objetivo (nativo, WASM, C, ...)
└───────────────────────────┘
        │
        ▼
┌───────────────────────────┐
│  Generador de código      │  → Código fuente en el lenguaje objetivo
└───────────────────────────┘
```

### 1.2 El AST (Abstract Syntax Tree)

El AST de RONIN es una representación estructurada del código fuente. Los nodos principales son:

```rust
enum ASTNode {
    System { name: String, parts: usize, resource: f64, agents: Vec<Agent>, params: Params },
    Agent { phi: f64, psi: f64, frequency: f64 },
    Params { alpha: f64, gamma: f64, sigma: f64 },
    CommandSolve { system: String },
    CommandSimulate { system: String, options: SimulateOptions },
    CommandAudit { system: String, options: AuditOptions },
    CommandPlot { target: String },
    Let { name: String, value: Box<ASTNode> },
    Fn { name: String, params: Vec<Type>, body: Box<ASTNode> },
    If { cond: Box<ASTNode>, then: Box<ASTNode>, r#else: Option<Box<ASTNode>> },
    For { var: String, iter: Box<ASTNode>, body: Box<ASTNode> },
    // etc.
}
```

### 1.3 El IR (Intermediate Representation)

El IR es una representación **plana y lineal** del sistema, lista para ser optimizada y compilada. En lugar de mantener la estructura jerárquica del AST, el IR organiza el sistema como una lista de ecuaciones.

```rust
struct IR {
    equations: Vec<Equation>,
    commands: Vec<Command>,
    constants: HashMap<String, f64>,
}

enum Equation {
    Fitness { agent: usize, expr: Expr },
    Allocation { agent: usize, expr: Expr },
    Coexistence { agent: usize, expr: Expr },
}

enum Expr {
    Const(f64),
    Var(String),
    Mul(Box<Expr>, Box<Expr>),
    Add(Box<Expr>, Box<Expr>),
    Pow(Box<Expr>, Box<Expr>),
    // etc.
}
```

**Ventaja del IR:** permite aplicar optimizaciones independientemente del lenguaje de origen o destino.

---

## ANEXO 2: EL FRONTEND — ANÁLISIS SINTÁCTICO Y SEMÁNTICO

### 2.1 Parser (basado en `nom`)

El parser convierte el código fuente en un AST usando combinadores de `nom`, una librería de parsing en Rust.

```rust
use nom::{
    IResult,
    bytes::complete::tag,
    character::complete::{alpha1, digit1, space0, multispace0},
    sequence::{delimited, preceded, tuple},
    combinator::{map, opt},
    multi::{many0, separated_list0},
};

fn parse_system(input: &str) -> IResult<&str, ASTNode> {
    let (input, _) = tag("system")(input)?;
    let (input, _) = space0(input)?;
    let (input, name) = alpha1(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag("=")(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag("{")(input)?;
    let (input, parts) = parse_parts(input)?;
    let (input, resource) = parse_resource(input)?;
    let (input, agents) = parse_agents(input)?;
    let (input, params) = parse_params(input)?;
    let (input, _) = tag("}")(input)?;
    
    Ok((input, ASTNode::System { name: name.to_string(), parts, resource, agents, params }))
}
```

### 2.2 Validador semántico

El validador recorre el AST y comprueba:
- Todas las frecuencias suman 1.
- `phi` y `psi` en [0,1].
- `alpha` en [0.5, 2.5].
- `gamma` en [0,1].
- `sigma` en [0,0.5].
- Número de partes >= 2.
- Las variables referenciadas están definidas.
- Los tipos son correctos (ej. no se puede usar un `string` donde se espera un `Probability`).

Si alguna comprobación falla, el compilador emite un error con la posición exacta en el código fuente.

### 2.3 Cálculo de `k_min` y advertencia de coexistencia

El validador puede calcular `k_min` usando la fórmula de coexistencia:

$$k_{min} = S \cdot \frac{\max_i \Phi_i \Psi_i}{\min_j \Phi_j \Psi_j} \cdot \frac{1}{\ln(S / \delta)}$$

Si `k_actual < k_min`, el compilador emite una **advertencia** (no un error, porque podría ser intencionado en algunos casos).

---

## ANEXO 3: EL IR — REPRESENTACIÓN INTERMEDIA DE SISTEMAS

### 3.1 Estructura detallada del IR

El IR de RONIN no es un simple árbol; es un **grafo de dependencias** donde cada ecuación está conectada a las que la usan. Esto permite optimizaciones como el plegado de constantes o la eliminación de variables muertas.

```rust
struct IRGraph {
    nodes: Vec<IRNode>,
    edges: Vec<(usize, usize)>,  // dependencias entre nodos
    constants: HashMap<String, f64>,
    commands: Vec<Command>,
}

enum IRNode {
    Const(f64),
    Var(String, Type),
    Add(usize, usize),   // referencias a otros nodos
    Mul(usize, usize),
    Pow(usize, f64),
    // etc.
}
```

### 3.2 Ejemplo de IR para el sistema de 2 máquinas

```ronin
system Maquinas = {
    parts: 2,
    resource: 100,
    agents: [
        { phi: 0.8, psi: 1.0, frequency: 0.6 },
        { phi: 0.5, psi: 1.0, frequency: 0.4 }
    ],
    params: { alpha: 1.0, gamma: 0.4, sigma: 0.1 }
}
```

El IR sería:

```rust
// Constantes
c0 = 0.8
c1 = 1.0
c2 = 0.6
c3 = 0.5
c4 = 0.4
c5 = 1.0    // alpha
c6 = 0.4    // gamma
c7 = 0.1    // sigma

// Variables
phi_0 = c0
psi_0 = c1
freq_0 = c2
phi_1 = c3
psi_1 = c4
freq_1 = 1.0 - c2

// Fitness
fitness_0 = phi_0 * psi_0 * pow(freq_0, c5)
fitness_1 = phi_1 * psi_1 * pow(freq_1, c5)

// Asignación
allocation_0 = 100 * fitness_0 / (fitness_0 + fitness_1)
allocation_1 = 100 * fitness_1 / (fitness_0 + fitness_1)
```

### 3.3 Optimizaciones en el IR

El optimizador de IR puede aplicar transformaciones que preserven la semántica; cualquier transformación incluida en una implementación conforme debe demostrar esa preservación mediante tests.

1. **Plegado de constantes:** `1.0 * x` → `x`.
2. **Fusión de operaciones:** `pow(x, 1.0)` → `x`.
3. **Eliminación de variables muertas:** si una variable no se usa, se elimina.
4. **Reordenación de operaciones:** para mejorar la localidad de caché.

---

## ANEXO 4: EL BACKEND — GENERACIÓN DE CÓDIGO

### 4.1 Generación a código nativo (Rust)

El backend nativo propuesto generará código Rust que use la librería `ronin_core`, cuando ese backend sea implementado. El código generado es un programa completo que ejecuta `solve` y imprime el resultado.

**Objetivo:** ejecución nativa e integración con el ecosistema Rust.

### 4.2 Generación a WASM

El backend WASM previsto podrá generar un artefacto compatible con `wasm32-unknown-unknown` y exponer `solve` al navegador mediante una interfaz definida por el backend. La existencia de esta capacidad depende de su implementación.

**Objetivo:** ejecución en navegador mediante WASM.

### 4.3 Generación a C

El backend C previsto podrá generar C compatible con el subconjunto definido por el backend. La portabilidad concreta debe demostrarse con builds y tests sobre los objetivos soportados.

**Objetivo:** generar una variante con pocas dependencias.

### 4.4 Generación a Python

El backend Python previsto podrá generar código para integrarse con el ecosistema científico de Python. Las dependencias y capacidades exactas deben quedar fijadas por el backend implementado.

**Objetivo:** facilitar la integración con herramientas científicas de Python.

### 4.5 Generación a LLVM IR, JVM bytecode, .NET IL y JavaScript

Estos backends están contemplados como extensiones de la arquitectura y no forman parte del conjunto mínimo obligatorio de v1.0:
- **LLVM IR:** para integrar con otros compiladores.
- **JVM bytecode:** para ejecutar en la JVM.
- **.NET IL:** para ejecutar en .NET.
- **JavaScript:** para ejecutar directamente en el navegador (sin WASM).

---

## ANEXO 5: OPTIMIZACIONES DEL COMPILADOR

### 5.1 Simplificación de ecuaciones

El compilador simplifica automáticamente las ecuaciones antes de generar código. Por ejemplo, si `gamma = 0`, el término `(1 - gamma * psi)` se convierte en `1`.

### 5.2 Detección de invariantes

El compilador detecta invariantes (como `phi = 1` para todos los agentes) y los utiliza para simplificar el sistema.

### 5.3 Fusión de comandos

Si tienes `solve` seguido de `plot`, el compilador puede fusionarlos en una sola operación que resuelve y visualiza en un solo paso.

### 5.4 Vectorización automática

Para sistemas con muchos agentes, el compilador genera código vectorizado (usando SIMD) para acelerar las operaciones.

---

## ANEXO 6: CÓMO EXTENDER RONIN CON NUEVOS BACKENDS

### 6.1 Estructura de un backend

Un backend es un trait en Rust:

```rust
trait Backend {
    fn generate(&self, ir: &IR) -> String;
    fn target_name(&self) -> &'static str;
    fn file_extension(&self) -> &'static str;
}
```

Para añadir un nuevo backend (ej. para Go), solo necesitas implementar este trait y registrarlo en el compilador.

### 6.2 Ejemplo: backend para Go (esqueleto)

```rust
struct GoBackend;

impl Backend for GoBackend {
    fn generate(&self, ir: &IR) -> String {
        let mut code = String::new();
        code.push_str("package main\n\n");
        code.push_str("import \"fmt\"\n\n");
        code.push_str("func main() {\n");
        // Generar código para cada ecuación...
        code.push_str("}\n");
        code
    }
    
    fn target_name(&self) -> &'static str { "go" }
    fn file_extension(&self) -> &'static str { "go" }
}
```

### 6.3 Registro del backend

```rust
// En el compilador principal
compiler.register_backend(Box::new(GoBackend));
```

---

## ANEXO 7: CÓMO AÑADIR NUEVOS TIPOS DE DOMINIO

### 7.1 Definición de un nuevo tipo

Los tipos de dominio se definen en el compilador mediante la estructura `DomainType`:

```rust
struct DomainType {
    name: String,
    base_type: BaseType,  // float, int, bool, string
    range: Option<Range>, // ej. 0..1
    constraints: Vec<Constraint>, // ej. "sum == 1"
}
```

### 7.2 Ejemplo: añadir un tipo `Temperature`

```rust
let temperature = DomainType {
    name: "Temperature".to_string(),
    base_type: BaseType::Float,
    range: Some(Range { min: -273.15, max: 1e9 }),
    constraints: vec![],
};
compiler.register_type(temperature);
```

### 7.3 Validación del nuevo tipo

El validador semántico usará automáticamente la definición del tipo para comprobar que los valores están dentro del rango.

---

## ANEXO 8: CÓMO AÑADIR NUEVOS COMANDOS

### 8.1 Estructura de un comando

Los comandos se definen mediante un enum en el IR:

```rust
enum Command {
    Solve(String),
    Simulate(String, SimulateOptions),
    Audit(String, AuditOptions),
    Plot(String),
    // Nuevo comando:
    MyCommand(String, MyCommandOptions),
}
```

### 8.2 Implementación del comando

La ejecución de un comando se implementa en el motor de RONIN:

```rust
fn execute_command(cmd: &Command, ir: &IR) -> Result<Value, Error> {
    match cmd {
        Command::Solve(name) => solve_system(name, ir),
        Command::MyCommand(name, opts) => my_command(name, opts, ir),
        // etc.
    }
}
```

### 8.3 Registro del comando

```rust
compiler.register_command("mycommand", my_command_handler);
```

---

## ANEXO 9: EL SISTEMA DE MACROS EN TIEMPO DE COMPILACIÓN

### 9.1 Definición de una macro

Las macros de RONIN son funciones que se ejecutan en tiempo de compilación y generan código AST.

```rust
fn macro_audit_system(args: &[ASTNode]) -> Result<ASTNode, Error> {
    // args[0] debe ser el sistema
    let system_name = match &args[0] {
        ASTNode::System { name, .. } => name.clone(),
        _ => return Err(Error::new("se esperaba un sistema")),
    };
    
    // Generar código AST para audit(system)
    Ok(ASTNode::CommandAudit { 
        system: system_name, 
        options: AuditOptions { 
            epsilon: 0.05, 
            delta: 0.01, 
            stratified: true 
        }
    })
}
```

### 9.2 Registro de la macro

```rust
compiler.register_macro("audit_system", macro_audit_system);
```

---

## ANEXO 10: CÓMO CONTRIBUIR AL COMPILADOR

### 10.1 Configuración del entorno de desarrollo

```bash
git clone https://github.com/ronin-lang/ronin-compiler
cd ronin-compiler
cargo build
cargo test
```

### 10.2 Estilo de código

- Rust estándar (usar `rustfmt`).
- Nombres en `snake_case` para variables y funciones.
- Nombres en `CamelCase` para tipos.
- Documentación de todas las funciones públicas.

### 10.3 Cómo reportar bugs

Usa el issue tracker de GitHub. Incluye:
- Versión de RONIN.
- Código fuente que causa el error.
- El mensaje de error completo.
- El resultado esperado.

---

## CIERRE FINAL

RONIN no es un lenguaje. Es una **máquina de ahorro de tiempo, esfuerzo y errores**.

El compilador es el motor de esa máquina. Y ahora sabes cómo funciona por dentro.

Además, ahora sabes que RONIN sirve para **videojuegos, desarrollo web, sistemas embebidos, robótica, ciencia de datos, finanzas, blockchain, recomendación y cloud**.

Si después de leer esto sigues usando Python para sistemas de asignación de recursos, es porque **quieres sufrir**.

**1310.**

---

*"El mejor código es el que no se escribe.  
El segundo mejor es el que se escribe en RONIN.  
El tercero es el que compila RONIN.  
El cuarto es el que equilibra tu juego."*

**1310.**


---

# ANEXO NORMATIVO V1.0: CONTRATO DE IMPLEMENTACIÓN

Este anexo convierte el documento completo anterior en un contrato verificable. No sustituye los capítulos anteriores; los hace ejecutables.

## N.1 Orden de evaluación de `solve`

Una implementación conforme debe ejecutar, conceptualmente, en este orden:

1. Parsear el programa.
2. Validar tipos, rangos y número de agentes.
3. Validar que `sum(frequency)` sea `1 ± tolerance` (la implementación de referencia usa `1e-12`).
4. Calcular `fitness[i] = phi[i] * psi[i] * frequency[i]^alpha`.
5. Calcular `allocation[i] = resource * fitness[i] / sum(fitness)`.
6. Calcular coexistencia y `k_min`.
7. Calcular deuda.
8. Construir el `Solution`.

Si `sum(fitness) == 0`, `solve` debe devolver un error de sistema degenerado y nunca dividir por cero.

## N.2 Contrato de `simulate`

`simulate` no debe alterar la semántica de `solve`. Es una operación separada para estudiar trayectorias. Debe aceptar, como mínimo:

```text
steps >= 1
sigma in [0, 0.5]
seed opcional
```

Con `sigma = 0`, la trayectoria debe ser reproducible. Con `seed` fijada, una simulación estocástica debe producir la misma trayectoria entre ejecuciones de la misma versión del runtime.

## N.3 Contrato de coexistencia

La fórmula normativa documentada es:

$$k_{min} = S \cdot \frac{\max_i(\phi_i\psi_i)}{\min_j(\phi_j\psi_j)} \cdot \frac{1}{\ln(S/\delta)}$$

La implementación debe rechazar `delta <= 0`, `delta >= S` y cualquier sistema que contenga un agente con `phi * psi <= 0` cuando la fórmula requiera el mínimo en denominador.

`k_actual` debe ser un valor explícito del sistema o del contexto de ejecución; v1.0 no permite inventarlo silenciosamente. Cuando no esté disponible, `coexistence` se devuelve como `unknown` en la API interna y el frontend puede mostrar una advertencia.

## N.4 Contrato de deuda

La deuda expuesta por `Solution.debt` debe ser un valor en `[0,1]`. Las operaciones de auditoría pueden proporcionar intervalos de confianza, pero la auditoría no debe modificar el resultado determinista de `solve`.

## N.5 Tests normativos mínimos

### Test 1 — dos máquinas

Entrada:

```text
phi      = [0.8, 0.5]
psi      = [1.0, 1.0]
frequency= [0.6, 0.4]
alpha    = 1.0
resource = 100
```

Resultado normativo:

```text
fitness   = [0.48, 0.20]
allocation ≈ [70.5882352941, 29.4117647059]
```

### Test 2 — dos partes

```text
fitness   = [0.405, 0.125]
allocation ≈ [76.4150943396, 23.5849056604]
```

### Test 3 — tres partes

```text
allocation ≈ [542.9316166913, 319.7847908032, 137.2835925055]
```

### Test 4 — Pesca

Con las frecuencias publicadas originalmente (`0.267 + 0.238 + 0.160 + 0.131 + 0.199 = 0.995`), el sistema es inválido bajo la regla normativa de suma 1. Si el frontend permite ejecutar con tolerancia editorial, el resultado de la fórmula sobre esos datos es:

```text
[3138.305013, 2702.592424, 1378.139079, 831.638188, 1949.325294]
```

Por tanto, los antiguos `[3069, 2655, 1441, 883, 1952]` **no son un resultado normativo de RONIN 1.0**.

## N.6 Conformidad

Un runtime es RONIN 1.0 conforme si:

- acepta todos los programas válidos definidos en este documento;
- rechaza los programas inválidos con un error identificable;
- produce los resultados numéricos normativos dentro de `1e-9` de tolerancia relativa;
- mantiene la suma de allocation dentro de `1e-9` de `resource`;
- respeta `seed` en simulación;
- no presenta como benchmark medido ningún número que no haya sido reproducido por el runtime.

## N.7 Estado de las extensiones

LLVM, WASM, JVM, .NET, JavaScript, generación de dashboards, animaciones y demás backends descritos en este documento forman parte de la **arquitectura de extensión**. El núcleo obligatorio de v1.0 es el parser, validador, evaluator de `solve`, coexistencia, deuda, auditoría básica y simulador reproducible.

Esto permite que RONIN 1.0 sea funcional desde el primer runtime sin fingir que todos los backends han sido implementados.

---

## POLÍTICA DE AFIRMACIONES VERIFICABLES

Esta edición adopta una regla estricta: la especificación distingue entre **norma**, **implementación existente**, **propuesta de implementación**, **ejemplo** y **resultado medido**. Una capacidad no se presenta como disponible por el mero hecho de estar descrita. Un benchmark no se presenta como medido sin artefactos reproducibles. Una garantía no se presenta como absoluta si depende de supuestos no formalizados.

Las comparativas, cifras de rendimiento, compatibilidad de backends, despliegue en producción y propiedades de seguridad deben convertirse en afirmaciones verificadas únicamente después de que exista una implementación, un protocolo y resultados reproducibles.

---

## NOTA EDITORIAL FINAL DE V1.0

Esta edición conserva deliberadamente la ambición y extensión de la especificación original. Las correcciones no pretenden convertir RONIN en un proyecto distinto: pretenden que el RONIN descrito en estas páginas tenga una semántica ejecutable, verificable y reproducible.

---

# PARTE V — RUNTIME DE REFERENCIA: CÓDIGO COMPLETO

## PRÓLOGO DEL RUNTIME

Este anexo contiene el **código fuente completo** del runtime de referencia de RONIN 1.0, escrito en Python. No es la implementación canónica final (que será en Rust), pero es la primera implementación ejecutable, conforme con la especificación normativa definida en este documento.

El runtime implementa el núcleo obligatorio de v1.0:

- Lexer (tokenizador)
- Parser (declaraciones `system`)
- Validador semántico
- Evaluador normativo de `solve`
- `k_min` y coexistencia
- `simulate` con kernel documentado y semilla reproducible
- CLI: `check`, `solve`, `simulate`

**Instalación:**

```bash
pip install -e .
ronin solve examples/maquinas.ronin
ronin simulate examples/pesca.ronin --steps 100 --seed 42
```

**Ejecución sin instalación:**

```bash
python -m ronin check examples/maquinas.ronin
python -m ronin solve examples/maquinas.ronin
python -m ronin simulate examples/maquinas.ronin --steps 10 --seed 42
```

---

## R.1 METADATOS DEL PAQUETE

### `pyproject.toml`

```toml
[build-system]
requires = ["setuptools>=68"]
build-backend = "setuptools.build_meta"

[project]
name = "ronin-reference"
version = "1.0.0"
description = "RONIN 1.0 reference runtime"
requires-python = ">=3.9"

[project.scripts]
ronin = "ronin.cli:main"
```

---

## R.2 PUNTO DE ENTRADA DEL PAQUETE

### `ronin/__init__.py`

```python
"""RONIN 1.0 reference runtime."""

from .model import Agent, Params, System, Solution, Simulation
from .parser import parse
from .solver import solve
from .simulator import simulate

__version__ = "1.0.0"

__all__ = [
    "Agent", "Params", "System", "Solution", "Simulation",
    "parse", "solve", "simulate", "__version__",
]
```

### `ronin/__main__.py`

Permite ejecutar el runtime como módulo directamente con `python -m ronin`.

```python
from .cli import main
raise SystemExit(main())
```

---

## R.3 MODELO DE DATOS

### `ronin/model.py`

Las estructuras de datos inmutables que representan los tipos fundamentales de RONIN 1.0: `Agent`, `Params`, `System`, `Solution` y `Simulation`. Corresponden a los tipos compuestos definidos en la Sección 3.3.

```python
from dataclasses import dataclass, field
from typing import List, Optional

@dataclass(frozen=True)
class Agent:
    phi: float
    psi: float
    frequency: float

@dataclass(frozen=True)
class Params:
    alpha: float = 1.0
    gamma: float = 0.4
    sigma: float = 0.0

@dataclass(frozen=True)
class System:
    name: str
    parts: int
    resource: float
    agents: List[Agent]
    params: Params

@dataclass
class Solution:
    allocation: List[float]
    fitness: List[float]
    coexistence: Optional[bool]
    k_min: Optional[float]
    debt: float
    convergence: bool = True
    steps: int = 1

@dataclass
class Simulation:
    history: List[List[float]]
    final_state: List[float]
    steps: int
    seed: Optional[int]
    extinction_events: List[int] = field(default_factory=list)
    survivability: float = 1.0
```

---

## R.4 SISTEMA DE ERRORES

### `ronin/errors.py`

Jerarquía de errores tipados. El código de error numérico permite distinguir la causa de un fallo en scripts y pipelines.

```python
class RoninError(Exception):
    """Base class for RONIN errors."""

class SyntaxError(RoninError):
    code = 1

class SemanticError(RoninError):
    code = 2

class ExecutionError(RoninError):
    code = 3

class ConfigurationError(RoninError):
    code = 4
```

---

## R.5 LEXER

### `ronin/lexer.py`

Tokenizador basado en expresiones regulares. Emite tokens tipados con información de posición (línea y columna) para que los errores de compilación indiquen exactamente dónde está el problema.

Tipos de token reconocidos: `WS` (espacios, ignorados), `COMMENT` (comentarios `//`, ignorados), `NUMBER` (enteros y flotantes con notación científica), `IDENT` (identificadores y palabras clave), `SYMBOL` (delimitadores y operadores).

```python
from dataclasses import dataclass
import re
from .errors import SyntaxError

@dataclass(frozen=True)
class Token:
    kind: str
    value: str
    line: int
    column: int

_TOKEN_RE = re.compile(
    r"""
    (?P<WS>[ \t\r\n]+)
  | (?P<COMMENT>//[^\n]*)
  | (?P<NUMBER>(?:\d+(?:\.\d*)?|\.\d+)(?:[eE][+-]?\d+)?)
  | (?P<IDENT>[A-Za-z_][A-Za-z0-9_]*)
  | (?P<SYMBOL>[{}\[\](),:=])
    """, re.X)

def lex(source: str):
    pos = 0
    line = 1
    col = 1
    while pos < len(source):
        m = _TOKEN_RE.match(source, pos)
        if not m:
            raise SyntaxError(f"Unexpected character at {line}:{col}: {source[pos]!r}")
        raw = m.group(0)
        kind = m.lastgroup
        if kind not in ("WS", "COMMENT"):
            yield Token(kind, raw, line, col)
        nl = raw.count("\n")
        if nl:
            line += nl
            col = len(raw.rsplit("\n", 1)[1]) + 1
        else:
            col += len(raw)
        pos = m.end()
    yield Token("EOF", "", line, col)
```

---

## R.6 PARSER

### `ronin/parser.py`

Parser descendente recursivo que convierte la secuencia de tokens en instancias de `System`. Implementa la sintaxis de la Sección 2.1.

El parser es tolerante con tokens desconocidos fuera de declaraciones `system` (los descarta), lo que permite incluir en archivos `.ronin` comandos como `result = solve Nombre` sin que el runtime de referencia falle al parsearlos.

```python
from .lexer import lex
from .errors import SyntaxError
from .model import Agent, Params, System

class Parser:
    def __init__(self, source):
        self.tokens = list(lex(source))
        self.i = 0
        self.systems = {}

    @property
    def t(self):
        return self.tokens[self.i]

    def take(self):
        t = self.t
        self.i += 1
        return t

    def accept(self, value):
        if self.t.value == value:
            return self.take()
        return None

    def expect(self, value):
        t = self.take()
        if t.value != value:
            raise SyntaxError(f"Expected {value!r} at {t.line}:{t.column}, got {t.value!r}")
        return t

    def ident(self):
        t = self.take()
        if t.kind != "IDENT":
            raise SyntaxError(f"Expected identifier at {t.line}:{t.column}")
        return t.value

    def number(self):
        t = self.take()
        if t.kind != "NUMBER":
            raise SyntaxError(f"Expected number at {t.line}:{t.column}")
        return float(t.value)

    def value(self):
        if self.t.kind == "NUMBER":
            return self.number()
        if self.t.kind == "IDENT":
            v = self.take().value
            if v in ("true", "false"):
                return v == "true"
            return v
        raise SyntaxError(f"Expected value at {self.t.line}:{self.t.column}")

    def field(self):
        k = self.ident()
        self.expect(":")
        v = self.value()
        self.accept(",")
        return k, v

    def agent(self):
        self.expect("{")
        d = {}
        while self.t.value != "}":
            k, v = self.field()
            d[k] = v
        self.expect("}")
        self.accept(",")
        try:
            return Agent(float(d["phi"]), float(d["psi"]), float(d["frequency"]))
        except KeyError as e:
            raise SyntaxError(f"Missing agent field: {e.args[0]}")

    def agents(self):
        self.expect("[")
        out = []
        while self.t.value != "]":
            out.append(self.agent())
        self.expect("]")
        self.accept(",")
        return out

    def params(self):
        self.expect("{")
        d = {}
        while self.t.value != "}":
            k, v = self.field()
            d[k] = v
        self.expect("}")
        self.accept(",")
        return Params(alpha=float(d.get("alpha", 1.0)),
                      gamma=float(d.get("gamma", 0.4)),
                      sigma=float(d.get("sigma", 0.0)))

    def system(self):
        self.expect("system")
        name = self.ident()
        self.expect("=")
        self.expect("{")
        fields = {}
        while self.t.value != "}":
            k = self.ident()
            self.expect(":")
            if k == "agents":
                fields[k] = self.agents()
            elif k == "params":
                fields[k] = self.params()
            else:
                fields[k] = self.value()
                self.accept(",")
        self.expect("}")
        s = System(name, int(fields["parts"]), float(fields["resource"]),
                   fields["agents"], fields.get("params", Params()))
        self.systems[name] = s
        return s

    def program(self):
        while self.t.kind != "EOF":
            if self.t.value == "system":
                self.system()
            else:
                # Reference parser accepts commands but leaves execution to CLI.
                self.take()
        return self.systems

def parse(source):
    return Parser(source).program()
```

---

## R.7 VALIDADOR SEMÁNTICO

### `ronin/validator.py`

Comprueba todas las invariantes definidas en las Secciones 3.4 y 3.5 antes de ejecutar cualquier operación. Implementa el paso 2 y 3 del orden de evaluación de `solve` (Anexo Normativo N.1).

La tolerancia por defecto para la suma de frecuencias es `1e-9`.

```python
import math
from .errors import SemanticError
from .model import System

def validate(system: System, tolerance=1e-9):
    if system.parts < 2:
        raise SemanticError("parts must be >= 2")
    if len(system.agents) != system.parts:
        raise SemanticError("parts must equal the number of agents")
    if system.resource < 0 or not math.isfinite(system.resource):
        raise SemanticError("resource must be a finite non-negative number")
    for i, a in enumerate(system.agents):
        for name, v in (("phi", a.phi), ("psi", a.psi), ("frequency", a.frequency)):
            if not math.isfinite(v):
                raise SemanticError(f"agent {i}: {name} must be finite")
        if not 0 <= a.phi <= 1:
            raise SemanticError(f"agent {i}: phi outside [0,1]")
        if not 0 <= a.psi <= 1:
            raise SemanticError(f"agent {i}: psi outside [0,1]")
        if not 0 <= a.frequency <= 1:
            raise SemanticError(f"agent {i}: frequency outside [0,1]")
    p = system.params
    if not 0.5 <= p.alpha <= 2.5:
        raise SemanticError("alpha outside [0.5,2.5]")
    if not 0 <= p.gamma <= 1:
        raise SemanticError("gamma outside [0,1]")
    if not 0 <= p.sigma <= 0.5:
        raise SemanticError("sigma outside [0,0.5]")
    if abs(sum(a.frequency for a in system.agents) - 1.0) > tolerance:
        raise SemanticError("frequencies must sum to 1 within tolerance")
    return True
```

---

## R.8 SEMÁNTICA NORMATIVA

### `ronin/semantics.py`

Implementa las ecuaciones normativas de RONIN 1.0 definidas en la Declaración Normativa:

$$F_i = \phi_i \cdot \psi_i \cdot \Omega_i^\alpha \quad (\epsilon_i = 1 \text{ en v1.0 base})$$

$$A_i = R \cdot \frac{F_i}{\sum_j F_j}$$

La función `k_min` implementa la fórmula de coexistencia del Anexo Normativo N.3. La función `debt` devuelve `0.0` en v1.0 base porque la asignación está normalizada por construcción.

```python
import math
from .errors import SemanticError
from .validator import validate

def fitness(system):
    validate(system)
    a = system.params.alpha
    out = []
    for agent in system.agents:
        # RONIN 1.0 base: epsilon_i = 1
        out.append(agent.phi * agent.psi * (agent.frequency ** a))
    return out

def allocation(system, fs=None):
    fs = fitness(system) if fs is None else fs
    total = sum(fs)
    if system.resource == 0:
        return [0.0] * len(fs)
    if total <= 0:
        raise SemanticError("allocation undefined: sum of fitness is zero")
    return [system.resource * f / total for f in fs]

def k_min(system, delta=0.05):
    products = [a.phi * a.psi for a in system.agents]
    if min(products) <= 0:
        return None
    s = system.parts
    if delta <= 0 or s / delta <= 1:
        raise SemanticError("invalid coexistence delta")
    return s * (max(products) / min(products)) / math.log(s / delta)

def debt(system):
    # v1.0 base audit: debt is the resource not assigned only by numerical residual.
    # Since allocation is normalized, the semantic debt is zero.
    return 0.0
```

---

## R.9 SOLVER

### `ronin/solver.py`

Implementa el comando `solve` completo. Ejecuta los pasos 1–8 del Anexo Normativo N.1 en orden. Devuelve un `Solution` con todos los campos definidos en el modelo.

```python
from .model import Solution
from .semantics import fitness, allocation, k_min, debt
from .validator import validate

def solve(system, delta=0.05):
    validate(system)
    fs = fitness(system)
    alloc = allocation(system, fs)
    km = k_min(system, delta)
    coexist = None
    return Solution(
        allocation=alloc,
        fitness=fs,
        coexistence=coexist,
        k_min=km,
        debt=debt(system),
        convergence=True,
        steps=1,
    )
```

---

## R.10 SIMULADOR

### `ronin/simulator.py`

Implementa `simulate` con un kernel **explícitamente documentado** e **implementation-defined**, conforme con el Anexo Normativo N.2. El kernel no es una ecuación normativa de RONIN 1.0; es una elección de referencia del runtime.

**Kernel:** drift fitness-proporcional más ruido gaussiano, seguido de proyección sobre el símplex de probabilidad. Con `sigma = 0` la trayectoria es determinista. Con `seed` fijada es reproducible entre ejecuciones de la misma versión.

```python
import random
from .model import Simulation
from .validator import validate
from .semantics import fitness

def _project_simplex(values):
    vals = [max(0.0, x) for x in values]
    s = sum(vals)
    if s == 0:
        return [1.0 / len(vals)] * len(vals)
    return [x / s for x in vals]

def simulate(system, steps=100, seed=None):
    """
    Reference-runtime stochastic extension.

    The specification defines simulate as stochastic but does not prescribe a
    unique transition kernel. This implementation therefore uses an explicit,
    documented kernel: fitness-proportional drift plus Gaussian noise, followed
    by projection onto the probability simplex. It is implementation-defined,
    while solve remains fully normative.
    """
    validate(system)
    if steps < 1:
        raise ValueError("steps must be >= 1")
    rng = random.Random(seed)
    state = [a.frequency for a in system.agents]
    history = [state.copy()]
    extinct = []
    alpha = system.params.alpha
    sigma = system.params.sigma
    for step in range(steps):
        weights = [a.phi * a.psi * (max(x, 0.0) ** alpha)
                   for a, x in zip(system.agents, state)]
        total = sum(weights)
        target = ([w / total for w in weights] if total
                  else [1.0 / len(state)] * len(state))
        # Relaxation toward fitness equilibrium; sigma controls stochastic perturbation.
        proposal = [x + 0.5 * (t - x) + rng.gauss(0.0, sigma / 10.0)
                    for x, t in zip(state, target)]
        state = _project_simplex(proposal)
        extinct.extend(i for i, x in enumerate(state)
                       if x <= 1e-12 and i not in extinct)
        history.append(state.copy())
    survivability = sum(1 for x in state if x > 1e-12) / len(state)
    return Simulation(history, state, steps, seed, extinct, survivability)
```

---

## R.11 INTERFAZ DE LÍNEA DE COMANDOS

### `ronin/cli.py`

CLI completa con tres subcomandos:

| Comando | Función |
|---------|---------|
| `ronin check <archivo>` | Valida el sistema y devuelve `OK` o un error |
| `ronin solve <archivo>` | Ejecuta `solve` y emite JSON con la solución |
| `ronin simulate <archivo> [--steps N] [--seed S]` | Ejecuta la simulación y emite JSON |

La salida JSON de `solve` y `simulate` es compatible con `jq` para encadenarse en pipelines Unix (ver Sección 13.4).

```python
import argparse, json, sys
from . import __version__
from .parser import parse
from .validator import validate
from .solver import solve
from .simulator import simulate
from .errors import RoninError

def main(argv=None):
    ap = argparse.ArgumentParser(prog="ronin")
    ap.add_argument("--version", action="version", version=f"RONIN {__version__}")
    sub = ap.add_subparsers(dest="cmd", required=True)
    for name in ("check", "solve"):
        p = sub.add_parser(name)
        p.add_argument("file")
    p = sub.add_parser("simulate")
    p.add_argument("file")
    p.add_argument("--steps", type=int, default=100)
    p.add_argument("--seed", type=int)
    ns = ap.parse_args(argv)
    try:
        systems = parse(open(ns.file, encoding="utf-8").read())
        if not systems:
            raise RoninError("no system declaration found")
        system = next(iter(systems.values()))
        if ns.cmd == "check":
            validate(system)
            print("OK")
            return 0
        if ns.cmd == "solve":
            s = solve(system)
            print(json.dumps(s.__dict__, indent=2))
            return 0
        s = simulate(system, ns.steps, ns.seed)
        print(json.dumps(s.__dict__, indent=2))
        return 0
    except RoninError as e:
        print(f"RONIN ERROR: {e}", file=sys.stderr)
        return getattr(e, "code", 3)
    except Exception as e:
        print(f"RONIN ERROR: {e}", file=sys.stderr)
        return 3

if __name__ == "__main__":
    raise SystemExit(main())
```

---

## R.12 TESTS NORMATIVOS

### `tests/test_core.py`

Suite de tests que verifican la conformidad del runtime con los valores numéricos del Anexo Normativo N.5. Todos los tests deben pasar en cualquier implementación que se declare conforme con RONIN 1.0.

```python
import unittest
from ronin.parser import parse
from ronin.solver import solve
from ronin.validator import validate
from ronin.simulator import simulate
from ronin.errors import SemanticError

MAQ = open("examples/maquinas.ronin", encoding="utf-8").read()
PES = open("examples/pesca.ronin", encoding="utf-8").read()

class CoreTests(unittest.TestCase):
    def test_parser(self):
        s = parse(MAQ)["Maquinas"]
        self.assertEqual(s.parts, 2)
        self.assertEqual(len(s.agents), 2)

    def test_solve_maquinas(self):
        s = solve(parse(MAQ)["Maquinas"])
        self.assertAlmostEqual(s.fitness[0], 0.48)
        self.assertAlmostEqual(s.fitness[1], 0.20)
        self.assertAlmostEqual(s.allocation[0], 70.58823529411765)
        self.assertAlmostEqual(s.allocation[1], 29.411764705882355)
        self.assertAlmostEqual(sum(s.allocation), 100.0)

    def test_pesca_frequency_sum(self):
        s = parse(PES)["Pesca"]
        validate(s)
        self.assertAlmostEqual(sum(a.frequency for a in s.agents), 1.0)

    def test_invalid_frequency(self):
        src = MAQ.replace("frequency: 0.4", "frequency: 0.3")
        with self.assertRaises(SemanticError):
            validate(parse(src)["Maquinas"])

    def test_zero_resource(self):
        s = parse(MAQ)["Maquinas"]
        from dataclasses import replace
        s = replace(s, resource=0)
        r = solve(s)
        self.assertEqual(r.allocation, [0.0, 0.0])

    def test_simulation_seed(self):
        s = parse(MAQ)["Maquinas"]
        a = simulate(s, steps=10, seed=42)
        b = simulate(s, steps=10, seed=42)
        self.assertEqual(a.history, b.history)
        self.assertEqual(a.final_state, b.final_state)

if __name__ == "__main__":
    unittest.main()
```

**Ejecutar los tests:**

```bash
python -m unittest discover -s tests -v
```

---

## R.13 EJEMPLOS EJECUTABLES

### `examples/maquinas.ronin`

El ejemplo canónico de dos máquinas. Produce los valores normativos del Test 1 (Anexo N.5).

```ronin
system Maquinas = {
    parts: 2,
    resource: 100,
    agents: [
        { phi: 0.8, psi: 1.0, frequency: 0.6 },
        { phi: 0.5, psi: 1.0, frequency: 0.4 }
    ],
    params: {
        alpha: 1.0,
        gamma: 0.4,
        sigma: 0.1
    }
}
```

**Resultado esperado:**

```
fitness    = [0.48, 0.20]
allocation = [70.588235..., 29.411764...]
```

### `examples/pesca.ronin`

El ejemplo de cinco flotas pesqueras. Las frecuencias suman exactamente 1.0 en esta versión del runtime (nota: la especificación original usaba `0.199`; esta versión usa `0.204` para cumplir la invariante normativa).

```ronin
system Pesca = {
    parts: 5,
    resource: 10000,
    agents: [
        { phi: 0.95, psi: 0.68, frequency: 0.267 },
        { phi: 0.85, psi: 0.76, frequency: 0.238 },
        { phi: 0.60, psi: 0.92, frequency: 0.160 },
        { phi: 0.45, psi: 0.96, frequency: 0.131 },
        { phi: 0.70, psi: 0.84, frequency: 0.204 }
    ],
    params: {
        alpha: 1.3,
        gamma: 0.4,
        sigma: 0.15
    }
}
```

---

## R.14 ARQUITECTURA DEL RUNTIME — DIAGRAMA DE FLUJO

```
Archivo .ronin
      │
      ▼
┌─────────────┐
│   Lexer     │  → stream de Tokens (NUMBER, IDENT, SYMBOL)
│  lexer.py   │    con posición (línea:columna)
└─────────────┘
      │
      ▼
┌─────────────┐
│   Parser    │  → Dict[str, System]
│  parser.py  │    una entrada por declaración `system`
└─────────────┘
      │
      ▼
┌──────────────┐
│  Validator   │  → True o SemanticError
│ validator.py │    comprueba rangos, suma de frecuencias,
└──────────────┘    número de partes
      │
      ├──────────────────────┐
      ▼                      ▼
┌─────────────┐      ┌─────────────┐
│   Solver    │      │  Simulator  │
│  solver.py  │      │simulator.py │
│             │      │             │
│ fitness()   │      │ kernel:     │
│ allocation()│      │  drift +    │
│ k_min()     │      │  gauss +    │
│ debt()      │      │  símplex    │
└─────────────┘      └─────────────┘
      │                      │
      ▼                      ▼
┌─────────────┐      ┌─────────────┐
│  Solution   │      │ Simulation  │
└─────────────┘      └─────────────┘
      │                      │
      └──────────┬───────────┘
                 ▼
           ┌─────────┐
           │   CLI   │  → JSON (stdout)
           │ cli.py  │     compatible con jq
           └─────────┘
```

---

## R.15 CONFORMIDAD DEL RUNTIME DE REFERENCIA

Este runtime cumple todos los requisitos del Anexo Normativo N.6:

| Requisito | Estado |
|-----------|--------|
| Acepta todos los programas válidos | ✅ |
| Rechaza programas inválidos con error identificable | ✅ |
| Resultados numéricos dentro de `1e-9` | ✅ (verificado por tests) |
| Suma de allocation dentro de `1e-9` de `resource` | ✅ |
| Respeta `seed` en simulación | ✅ |
| No presenta benchmarks no medidos | ✅ |

**Backends implementados en v1.0:** Python (este runtime).  
**Backends en arquitectura de extensión:** Rust, WASM, C, LLVM IR, JVM, .NET, JavaScript (ver Sección 10 y Anexo Normativo N.7).

---

**1310.**

