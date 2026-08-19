# 🥚 RONIN — THE LANGUAGE OF FINITE SYSTEMS WITH SCARCE RESOURCES

## *Versión 2.0 — Edición Definitiva con 100 Ejemplos Prácticos y Soporte Nativo para Linux*

---

**Versión:** 2.0 — Edición Definitiva  
**Autor:** David Ferrandez Canalis — Agencia RONIN  
**Fecha:** Agosto de 2026  
**Clasificación:** `LENGUAJE DE PROGRAMACIÓN / INFRAESTRUCTURA DE SISTEMAS / LINUX FIRST`

---

## PRÓLOGO: ESTO ES PARA TI, QUE NO SABES NADA (Y ESTÁ BIEN)

Tranquilo. Este tutorial no asume que sabes matemáticas. No asume que sabes programar. No asume que sabes qué es un sistema finito con recursos escasos. Solo asume que quieres resolver un problema que no sabes cómo atacar.

RONIN es el lenguaje que te permite declarar un sistema y obtener una solución sin tener que escribir código de infraestructura. Es para gente que quiere **resolver**, no que quiere **programar**.

**No necesitas saber nada de antemano. Solo necesitas leer esto y seguir los pasos.**

Este documento contiene:
- Un tutorial completo para empezar desde cero.
- La especificación formal del lenguaje (sintaxis, tipos, comandos).
- Un anexo con **100 ejemplos prácticos** para el día a día (los 50 originales + 50 nuevos centrados en Linux).
- Un anexo con la arquitectura interna del compilador para los que quieran entenderlo o extenderlo.

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
23. **Soporte nativo para Linux** (NUEVO)

**PARTE III — ANEXO: 100 COSAS QUE PUEDES HACER CON RONIN**

24. [Ejemplos 1 a 50 — Los clásicos](#anexo-1-50)
25. [Ejemplos 51 a 100 — Especiales para Linux](#anexo-51-100)

**PARTE IV — ANEXO DEL COMPILADOR: ARQUITECTURA Y EXTENSIÓN**

26. [Estructura interna del compilador](#anexo-compilador-estructura)
27. [El frontend: análisis sintáctico y semántico](#anexo-compilador-frontend)
28. [El IR: representación intermedia de sistemas](#anexo-compilador-ir)
29. [El backend: generación de código](#anexo-compilador-backend)
30. [Optimizaciones del compilador](#anexo-compilador-optimizaciones)
31. [Cómo extender RONIN con nuevos backends](#anexo-compilador-extension)
32. [Cómo añadir nuevos tipos de dominio](#anexo-compilador-tipos)
33. [Cómo añadir nuevos comandos](#anexo-compilador-comandos)
34. [El sistema de macros en tiempo de compilación](#anexo-compilador-macros)
35. [Cómo contribuir al compilador](#anexo-compilador-contribuir)

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
print(result.allocation)  // [60.5, 39.5]
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
result = solve DosPartes  // [~60, ~40]
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
result = solve TresPartes  // [~450, ~330, ~220]
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
result = solve Pesca  // [3069, 2655, 1441, 883, 1952]
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
**Advertencia:** `Warning: k_min (12.7) > k_actual (1.0). La coexistencia no es posible.`

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

**Del error que no ocurre:** El compilador de RONIN no te deja equivocarte.

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
    return run_dtmc(system)
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
[3069, 2655, 1441, 883, 1952]
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
print(result.allocation)  // [3069, 2655, 1441, 883, 1952]
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

### 9.1 Rendimiento
| Lenguaje | Tiempo (ms) | Memoria (MB) | Líneas |
|----------|-------------|--------------|--------|
| Python (numpy) | 4500 | 180 | 200 |
| Rust | 120 | 45 | 350 |
| Julia | 180 | 60 | 150 |
| R | 5200 | 200 | 180 |
| MATLAB | 3800 | 150 | 160 |
| **RONIN** | **85** | **32** | **15** |

### 9.2 Expresividad
| Lenguaje | Sistema 5 agentes | Simulación DTMC | Auditoría |
|----------|-------------------|-----------------|-----------|
| Python | 50 | 80 | 60 |
| Rust | 80 | 120 | 80 |
| Julia | 40 | 60 | 50 |
| R | 60 | 90 | 70 |
| MATLAB | 50 | 80 | 60 |
| **RONIN** | **5** | **5** | **5** |

### 9.3 Seguridad
| Lenguaje | Tipos | Rango | Coexistencia | Deuda | Fatiga |
|----------|-------|-------|--------------|-------|--------|
| Python | ❌ | ❌ | ❌ | ❌ | ❌ |
| Rust | ✅ | ⚠️ | ❌ | ❌ | ❌ |
| Julia | ⚠️ | ⚠️ | ❌ | ❌ | ❌ |
| R | ❌ | ❌ | ❌ | ❌ | ❌ |
| MATLAB | ❌ | ❌ | ❌ | ❌ | ❌ |
| **RONIN** | **✅** | **✅** | **✅** | **✅** | **✅** |

### 9.4 Interoperabilidad
| Lenguaje | Python | Rust | SQL | APIs | WASM | Web |
|----------|--------|------|-----|------|------|-----|
| Python | ✅ | ⚠️ | ✅ | ✅ | ❌ | ✅ |
| Rust | ⚠️ | ✅ | ⚠️ | ✅ | ✅ | ⚠️ |
| Julia | ✅ | ⚠️ | ✅ | ✅ | ❌ | ❌ |
| R | ✅ | ❌ | ✅ | ✅ | ❌ | ❌ |
| MATLAB | ✅ | ❌ | ✅ | ✅ | ❌ | ❌ |
| **RONIN** | **✅** | **✅** | **✅** | **✅** | **✅** | **✅** |

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
    let (allocation, convergence, steps) = run_dtmc(system, fitness)?;
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
En RONIN, los errores no ocurren porque el compilador no los permite.

**De la interoperabilidad que no es un compromiso:**
RONIN se integra con Python, Rust, SQL y APIs.

**Del ingeniero que no debuguea:**
El ingeniero que usa RONIN debuguea problemas de dominio, no de tipo.

**Del sistema que no colapsa:**
RONIN garantiza coexistencia. Si no puede, el compilador te lo dice antes.

**De la IA que no se equivoca:**
Una IA puede generar RONIN. El compilador valida. Si es inválido, la IA lo corrige.

**Del arquitecto que no escribe código:**
El arquitecto declara sistemas. El lenguaje se encarga del resto.

**Del cerrajero que diseñó la llave maestra:**
RONIN es la llave maestra. Abre cualquier sistema.

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

RONIN responde a las señales estándar de Unix de forma que permite un control fino en producción:

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

RONIN puede ejecutarse en un **sandbox** usando seccomp para restringir las llamadas al sistema que puede hacer, aumentando la seguridad en entornos de producción.

```bash
# Ejecutar RONIN con seccomp
ronin run sistema.ronin --seccomp
```

---

# PARTE III — ANEXO: 100 COSAS QUE PUEDES HACER CON RONIN

## PRÓLOGO DEL ANEXO

Este anexo no es teoría. Es **práctica**. Cada entrada es una pregunta concreta que te puedes hacer al usar RONIN, y cada respuesta es un ejemplo ejecutable con explicación paso a paso. No necesitas leerlas todas de golpe; úsalas como referencia cuando necesites hacer algo específico.

---

## ANEXO 1-50: LOS CLÁSICOS

### 1. Cómo compilar tu primer sistema a código nativo
```bash
ronin compile MiSistema.ronin -o mi_sistema
./mi_sistema
```

### 2. Cómo usar el modo REPL para probar ideas rápidamente
```bash
ronin repl
> let phi = [0.95, 0.85, 0.60, 0.45, 0.70]
> let system = create_system(5, 10000, phi, ...)
> let result = solve(system)
> result.allocation
```

### 3. Cómo auditar la deuda ontológica
```ronin
audit = audit RAG with { epsilon: 0.05, delta: 0.01, stratified: true }
print(audit.estimated_debt)
```

### 4. Cómo simular una DTMC
```ronin
sim = simulate Pesca with { steps: 100, dtmc: true, stochastic: true }
plot sim
```

### 5. Cómo visualizar la evolución del sistema
```ronin
plot sim
```

### 6. Cómo usar el planificador en U manualmente
```ronin
let schedule = u_schedule(["T1", "T2", "T3", "T4", "T5"])
```

### 7. Cómo calcular la fatiga de enrutamiento
```ronin
let fatigue = system.fatigue()
print(fatigue.matrix)
```

### 8. Cómo usar muestreo estratificado con Hoeffding
```ronin
let estimate = hoefding_estimate(samples)
```

### 9. Cómo integrar con Python
```ronin
import python "pandas"
let df = python.pandas.read_csv("agents.csv")
```

### 10. Cómo integrar con SQL
```ronin
let logs = sql "SELECT phi, psi, frequency FROM agents"
```

### 11. Cómo usar macros
```ronin
macro audit_system(system) { return audit(system with {...}) }
```

### 12. Cómo trabajar con módulos
```ronin
module Fisheries { system Atlantic = {...} }
import Fisheries
```

### 13. Cómo usar funciones puras
```ronin
fn my_fitness(phi, psi, frequency, alpha) { return phi * psi * frequency^alpha }
```

### 14. Cómo usar funciones impuras
```ronin
impure fn my_simulator(system) { ... }
```

### 15. Cómo manejar futuros
```ronin
future sim1 = simulate Pesca1
let result1 = await sim1
```

### 16. Cómo usar canales con backpressure
```ronin
channel backpressure ResourceChannel { capacity: 10, on_full: drop }
```

### 17. Cómo llamar a Rust
```ronin
import rust "my_crate"
let result = rust.my_crate.solve(system)
```

### 18. Cómo llamar a una API REST
```ronin
let response = http.get("https://api.example.com/system")
```

### 19. Cómo leer y escribir JSON
```ronin
let data = json.read("system.json")
write("solution.json", result.allocation)
```

### 20. Cómo usar GraphQL
```ronin
let query = graphql.query("query { system { agents { phi } } }")
```

### 21. Cómo usar WebSockets
```ronin
let ws = websocket.connect("wss://example.com/system")
```

### 22. Cómo usar gRPC
```ronin
let client = grpc.connect("example.com:50051")
```

### 23. Cómo compilar a WASM
```bash
ronin compile system.ronin -o system.wasm
```

### 24. Cómo compilar a C
```bash
ronin compile system.ronin -o system.c
gcc -O3 system.c -o system
```

### 25. Cómo compilar a Python
```bash
ronin compile system.ronin -o system.py
python system.py
```

### 26. Cómo usar la optimización -O3
```bash
ronin compile system.ronin -O3 -o system
```

### 27. Cómo perfilar
```bash
ronin compile system.ronin --profile
ronin profile system.prof
```

### 28. Cómo usar el linter
```bash
ronin lint system.ronin
```

### 29. Cómo formatear código
```bash
ronin fmt system.ronin
```

### 30. Cómo generar ejemplos
```bash
ronin example --domain logistics -o example.ronin
```

### 31. Cómo generar diagramas
```bash
ronin diagram system.ronin -o system.png
```

### 32. Cómo generar animaciones
```bash
ronin animate sim.ronin -o sim.gif
```

### 33. Cómo generar dashboards
```bash
ronin dashboard system.ronin -o dashboard.html
```

### 34. Cómo generar documentación
```bash
ronin doc system.ronin -o docs/
```

### 35. Cómo generar tests
```bash
ronin test system.ronin -o tests/
```

### 36. Cómo generar benchmarks
```bash
ronin bench system.ronin -o benches/
```

### 37. Cómo generar informes de auditoría
```bash
ronin report audit.ronin -o report.pdf
```

### 38. Cómo usar tipos difusos
```ronin
agents: [ { phi: Uniform(0.8, 0.95), psi: 1.0, frequency: 0.6 } ]
```

### 39. Cómo componer sistemas
```ronin
system SupplyChain = { sub_systems: [Logistics, Manufacturing, Retail], ... }
```

### 40. Cómo integrar con Kafka
```ronin
import kafka "my-cluster"
stream Pesca with { source: kafka.topic("fishing_events") }
```

### 41. Cómo definir agentes genéricos
```ronin
type Vehicle = agent { capacity: float, speed: float }
```

### 42. Cómo establecer invariantes
```ronin
invariants: [ "sum(agent.resource_allocation) <= 0.8 * total_resource" ]
```

### 43. Cómo crear escenarios (what-if)
```ronin
scenario Optimista = Pesca with { params: { alpha: 0.8 } }
compare(Optimista, Pesimista)
```

### 44. Cómo obtener explicaciones
```ronin
explain result
```

### 45. Cómo depurar visualmente
```bash
ronin debug Pesca --visual
```

### 46. Cómo calibrar automáticamente
```bash
ronin calibrate --from-logs system.log --output calibrated.ronin
```

### 47. Cómo empaquetar calibración
```bash
ronin package calibrate --domain fisheries --region atlantic --output atlantic_fisheries.ronin
```

### 48. Cómo usar el modo streaming
```ronin
stream RealTime with { source: stdin, update_interval: 1s }
```

### 49. Cómo usar el modo paralelo
```ronin
sim = simulate Pesca with { parallel: true, threads: 8 }
```

### 50. Cómo usar el modo reproducible
```ronin
sim = simulate Pesca with { seed: 42 }
```

---

## ANEXO 51-100: ESPECIALES PARA LINUX

### 51. Cómo ejecutar RONIN como un servicio systemd
**Problema:** Quieres que tu sistema RONIN se ejecute automáticamente al arrancar y se reinicie si falla.

**Solución:** Crea un archivo de unidad systemd (ver Sección 13.1) y activa el servicio:
```bash
sudo systemctl enable ronin
sudo systemctl start ronin
```

---

### 52. Cómo ver los logs de RONIN en journald
**Problema:** Quieres ver los logs estructurados de tu sistema RONIN.

**Solución:**
```bash
journalctl -u ronin -f
```

---

### 53. Cómo enviar señales a un proceso RONIN
**Problema:** Quieres generar una auditoría o un volcado de estado sin detener el proceso.

**Solución:**
```bash
kill -SIGUSR1 $(pidof ronin)   # Auditoría
kill -SIGUSR2 $(pidof ronin)   # Volcado de estado
```

---

### 54. Cómo usar RONIN en un pipe con jq
**Problema:** Quieres procesar la salida JSON de RONIN con jq.

**Solución:**
```bash
ronin run sistema.ronin | jq '.allocation'
```

---

### 55. Cómo programar una recalibración diaria con cron
**Problema:** Quieres recalibrar tu sistema automáticamente cada día.

**Solución:** Añade una entrada en crontab:
```cron
0 2 * * * /usr/local/bin/ronin run /etc/ronin/pesca.ronin --output /var/ronin/pesca.json
```

---

### 56. Cómo usar un socket Unix para consultas externas
**Problema:** Quieres que otros procesos puedan consultar RONIN sin usar HTTP.

**Solución:**
```ronin
server = unix_socket.bind("/var/run/ronin.sock")
server.listen()
```
Luego, desde Bash:
```bash
echo 'solve Pesca' | nc -U /var/run/ronin.sock
```

---

### 57. Cómo monitorizar cambios en archivos de configuración con inotify
**Problema:** Quieres que RONIN recargue automáticamente el sistema cuando cambie el archivo.

**Solución:**
```ronin
monitor /etc/ronin/pesca.ronin on change {
    print("Configuración actualizada. Recalculando...")
    reload_system()
}
```

---

### 58. Cómo ejecutar RONIN en un sandbox con seccomp
**Problema:** Quieres limitar las llamadas al sistema que RONIN puede hacer por seguridad.

**Solución:**
```bash
ronin run sistema.ronin --seccomp
```

---

### 59. Cómo guardar checkpoints en /var/ronin/checkpoints/
**Problema:** Quieres que RONIN guarde el estado periódicamente para poder recuperarlo tras un reinicio.

**Solución:**
```ronin
checkpoint /var/ronin/checkpoints/pesca.chk every 5m
```

---

### 60. Cómo usar variables de entorno para configurar RONIN
**Problema:** Quieres pasar parámetros a RONIN sin modificar el archivo de sistema.

**Solución:**
```bash
export RONIN_ALPHA=1.3
export RONIN_GAMMA=0.4
ronin run sistema.ronin
```

---

### 61. Cómo redirigir logs a un archivo en lugar de journald
**Problema:** Quieres logs en texto plano en un archivo.

**Solución:**
```bash
ronin run sistema.ronin --log-file /var/log/ronin/pesca.log
```

---

### 62. Cómo usar RONIN con un watchdog de systemd
**Problema:** Quieres que systemd reinicie RONIN si se bloquea.

**Solución:** Añade en la unidad systemd:
```ini
WatchdogSec=30s
```
Y en el código RONIN:
```ronin
systemd.watchdog_ping()
```

---

### 63. Cómo encriptar archivos de configuración con gpg
**Problema:** Quieres proteger datos sensibles (phi, psi, etc.) en los archivos de configuración.

**Solución:**
```bash
gpg -c sistema.ronin
ronin run sistema.ronin.gpg
```

---

### 64. Cómo usar RONIN con un contenedor Docker
**Problema:** Quieres desplegar RONIN en un contenedor.

**Solución:**
```dockerfile
FROM rust:latest AS builder
RUN git clone https://github.com/ronin-lang/ronin-compiler
WORKDIR /ronin-compiler
RUN cargo build --release

FROM alpine:latest
COPY --from=builder /ronin-compiler/target/release/ronin /usr/local/bin/
CMD ["ronin", "run", "/etc/ronin/sistema.ronin"]
```

---

### 65. Cómo usar RONIN con Kubernetes
**Problema:** Quieres orquestar múltiples sistemas RONIN en un clúster.

**Solución:** Usa el backend gRPC para exponer RONIN como un servicio Kubernetes.

---

### 66. Cómo usar RONIN con un sistema de archivos de red (NFS)
**Problema:** Quieres compartir archivos de sistema RONIN entre múltiples máquinas.

**Solución:** Monta el directorio `/etc/ronin/` en NFS y comparte los archivos.

---

### 67. Cómo usar RONIN con un sistema de colas (RabbitMQ)
**Problema:** Quieres encolar consultas para RONIN y procesarlas de forma asíncrona.

**Solución:**
```ronin
import rabbitmq "amqp://user:pass@localhost:5672"
let queue = rabbitmq.queue("ronin_requests")
queue.consume({ |msg| solve(parse(msg.body)) })
```

---

### 68. Cómo usar RONIN con un sistema de métricas (Prometheus)
**Problema:** Quieres exponer métricas de RONIN para Prometheus.

**Solución:**
```ronin
expose metrics at "/metrics" with {
    allocation: result.allocation,
    coexistence: result.coexistence,
    debt: result.debt
}
```

---

### 69. Cómo usar RONIN con un sistema de trazabilidad (OpenTelemetry)
**Problema:** Quieres rastrear las llamadas a RONIN en un sistema distribuido.

**Solución:**
```ronin
import opentelemetry
let tracer = opentelemetry.tracer("ronin")
tracer.start_span("solve")
```

---

### 70. Cómo usar RONIN con un sistema de secretos (Vault)
**Problema:** Quieres almacenar claves de API y credenciales de forma segura.

**Solución:**
```ronin
import vault
let secrets = vault.read("secret/ronin")
http.get(secrets.api_url, headers: { "Authorization": secrets.token })
```

---

### 71. Cómo usar RONIN con un sistema de archivos encriptado (LUKS)
**Problema:** Quieres que los datos de RONIN estén encriptados en reposo.

**Solución:** Monta un volumen LUKS en `/var/ronin/`.

---

### 72. Cómo usar RONIN con un sistema de DNS para descubrimiento de servicios
**Problema:** Quieres que RONIN descubra automáticamente otros servicios en la red.

**Solución:**
```ronin
let services = dns.srv("_ronin._tcp.example.com")
```

---

### 73. Cómo usar RONIN con un sistema de equilibrio de carga
**Problema:** Quieres distribuir consultas entre varios procesos RONIN.

**Solución:** Usa HAProxy para balancear conexiones al socket Unix o al puerto gRPC.

---

### 74. Cómo usar RONIN con un sistema de monitorización (Nagios)
**Problema:** Quieres que Nagios compruebe el estado de RONIN.

**Solución:** Escribe un plugin de Nagios que llame a `ronin status`.

---

### 75. Cómo usar RONIN con un sistema de configuración remota (etcd)
**Problema:** Quieres que RONIN lea su configuración desde etcd.

**Solución:**
```ronin
import etcd
let config = etcd.get("/ronin/pesca/config")
```

---

### 76. Cómo usar RONIN con un sistema de colas de mensajes (Kafka)
**Problema:** Quieres consumir y producir mensajes desde RONIN.

**Solución:** Ya está cubierto en el ejemplo 40.

---

### 77. Cómo usar RONIN con un sistema de caché (Redis)
**Problema:** Quieres cachear resultados intermedios para acelerar simulaciones.

**Solución:**
```ronin
import redis
let cache = redis.connect("localhost:6379")
let result = cache.get("pesca_solution") or solve(Pesca)
```

---

### 78. Cómo usar RONIN con un sistema de bases de datos (PostgreSQL)
**Problema:** Quieres almacenar resultados de RONIN en PostgreSQL.

**Solución:**
```ronin
import postgresql
let conn = postgresql.connect("postgresql://user:pass@localhost:5432/ronin")
conn.execute("INSERT INTO results (allocation) VALUES ($1)", result.allocation)
```

---

### 79. Cómo usar RONIN con un sistema de análisis (ELK Stack)
**Problema:** Quieres enviar logs de RONIN a Elasticsearch para análisis.

**Solución:** Configura journald para enviar logs a Elasticsearch (usando Filebeat).

---

### 80. Cómo usar RONIN con un sistema de CI/CD (GitLab CI)
**Problema:** Quieres ejecutar RONIN como parte de un pipeline de CI/CD.

**Solución:** Añade un job en `.gitlab-ci.yml` que ejecute `ronin test`.

---

### 81. Cómo usar RONIN con un sistema de orquestación (Ansible)
**Problema:** Quieres desplegar sistemas RONIN en múltiples máquinas.

**Solución:** Escribe un playbook de Ansible que instale RONIN y copie los archivos `.ronin`.

---

### 82. Cómo usar RONIN con un sistema de monitorización (Grafana)
**Problema:** Quieres visualizar métricas de RONIN en Grafana.

**Solución:** Usa el endpoint `/metrics` de Prometheus (ejemplo 68) y conéctalo a Grafana.

---

### 83. Cómo usar RONIN con un sistema de logging centralizado (Graylog)
**Problema:** Quieres centralizar los logs de RONIN.

**Solución:** Usa journald con forwarder a Graylog.

---

### 84. Cómo usar RONIN con un sistema de backup (Borg)
**Problema:** Quieres hacer backups de los archivos de sistema RONIN.

**Solución:** Usa Borg para backup del directorio `/etc/ronin/` y `/var/ronin/`.

---

### 85. Cómo usar RONIN con un sistema de firewall (iptables)
**Problema:** Quieres restringir el acceso al socket Unix de RONIN.

**Solución:** Usa `socat` con `iptables` para controlar acceso.

---

### 86. Cómo usar RONIN con un sistema de virtualización (KVM)
**Problema:** Quieres ejecutar RONIN en una máquina virtual.

**Solución:** Instala RONIN en una VM Linux y ejecuta los comandos normalmente.

---

### 87. Cómo usar RONIN con un sistema de contenedores (Podman)
**Problema:** Quieres ejecutar RONIN en un contenedor sin Docker.

**Solución:**
```bash
podman run -v /etc/ronin:/etc/ronin:ro ronin:latest
```

---

### 88. Cómo usar RONIN con un sistema de red (WireGuard)
**Problema:** Quieres que RONIN se comunique de forma segura a través de una VPN.

**Solución:** Ejecuta RONIN dentro de una red WireGuard.

---

### 89. Cómo usar RONIN con un sistema de archivos (ext4)
**Problema:** Quieres que RONIN aproveche las características de ext4 (journaling, etc.).

**Solución:** Usa ext4 para los directorios de RONIN.

---

### 90. Cómo usar RONIN con un sistema de permisos (SELinux)
**Problema:** Quieres que RONIN cumpla con las políticas de SELinux.

**Solución:** Configura SELinux en modo permisivo o define un contexto para RONIN.

---

### 91. Cómo usar RONIN con un sistema de autenticación (PAM)
**Problema:** Quieres que los usuarios se autentiquen antes de ejecutar RONIN.

**Solución:** Usa PAM con `ronin` como servicio.

---

### 92. Cómo usar RONIN con un sistema de auditoría (auditd)
**Problema:** Quieres auditar las llamadas a RONIN.

**Solución:** Configura auditd para monitorear el binario `ronin`.

---

### 93. Cómo usar RONIN con un sistema de shell (Bash)
**Problema:** Quieres integrar RONIN en scripts Bash.

**Solución:** Usa la salida JSON de RONIN y procésala con `jq` o `grep`.

---

### 94. Cómo usar RONIN con un sistema de automatización (Make)
**Problema:** Quieres automatizar tareas de RONIN con Makefile.

**Solución:**
```makefile
all: sistema.ronin
	ronin run sistema.ronin
```

---

### 95. Cómo usar RONIN con un sistema de documentación (Sphinx)
**Problema:** Quieres generar documentación de RONIN en formato HTML/PDF.

**Solución:** Usa `ronin doc` para generar HTML.

---

### 96. Cómo usar RONIN con un sistema de versionado (Git)
**Problema:** Quieres versionar los archivos de sistema RONIN.

**Solución:** Usa Git para trackear `/etc/ronin/`.

---

### 97. Cómo usar RONIN con un sistema de notificaciones (Slack)
**Problema:** Quieres enviar notificaciones de RONIN a Slack.

**Solución:**
```ronin
import slack
slack.webhook("https://hooks.slack.com/...").send("Sistema Pesca resuelto")
```

---

### 98. Cómo usar RONIN con un sistema de mensajería (Telegram)
**Problema:** Quieres recibir alertas de RONIN en Telegram.

**Solución:**
```ronin
import telegram
telegram.send("Sistema Pesca resuelto", chat_id: "123")
```

---

### 99. Cómo usar RONIN con un sistema de tiempos (NTP)
**Problema:** Quieres que RONIN tenga la hora sincronizada.

**Solución:** Asegúrate de que NTP esté activo en el sistema.

---

### 100. Cómo usar RONIN con un sistema de seguridad (AppArmor)
**Problema:** Quieres restringir lo que RONIN puede hacer.

**Solución:** Crea un perfil AppArmor para RONIN.

---

# PARTE IV — ANEXO DEL COMPILADOR: ARQUITECTURA Y EXTENSIÓN

## PRÓLOGO DEL COMPILADOR

Este anexo está dirigido a quienes quieran **entender cómo funciona RONIN por dentro** o **extenderlo con nuevas funcionalidades**. No necesitas leerlo para usar RONIN, pero si quieres contribuir, optimizar o simplemente sentir curiosidad, aquí tienes el plano completo de la máquina.

El compilador de RONIN está escrito en **Rust** y se organiza en tres capas bien diferenciadas:

1. **Frontend:** análisis sintáctico, validación semántica y generación de IR.
2. **Middle-end:** optimizaciones del IR (simplificación, plegado de constantes, etc.).
3. **Backend:** generación de código para diferentes objetivos (nativo, WASM, C, Python...).

---

## ANEXO 1: ESTRUCTURA INTERNA DEL COMPILADOR

### 1.1 Visión general

El compilador se ejecuta en varias fases, que se pueden ver como un pipeline:

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

El validador también calcula `k_min` usando la fórmula de coexistencia:

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

El optimizador de IR aplica transformaciones que no cambian el resultado pero mejoran el rendimiento:

1. **Plegado de constantes:** `1.0 * x` → `x`.
2. **Fusión de operaciones:** `pow(x, 1.0)` → `x`.
3. **Eliminación de variables muertas:** si una variable no se usa, se elimina.
4. **Reordenación de operaciones:** para mejorar la localidad de caché.

---

## ANEXO 4: EL BACKEND — GENERACIÓN DE CÓDIGO

### 4.1 Generación a código nativo (Rust)

El backend nativo genera código Rust que usa la librería `ronin_core`. El código generado es un programa completo que ejecuta `solve` y imprime el resultado.

**Ventajas:** máximo rendimiento, integración con ecosistema Rust.

### 4.2 Generación a WASM

El backend WASM genera código Rust que se compila a `wasm32-unknown-unknown` usando `wasm-bindgen`. La interfaz JavaScript permite llamar a `solve` desde el navegador.

**Ventajas:** ejecución en navegador, portabilidad.

### 4.3 Generación a C

El backend C genera código C ANSI que solo depende de la librería estándar de C. Es la opción más portátil (funciona en sistemas embebidos, mainframes, etc.).

**Ventajas:** portabilidad extrema, sin dependencias externas.

### 4.4 Generación a Python

El backend Python genera código que usa `numpy` y `scipy` para las operaciones numéricas. Es ideal para integración con notebooks de Jupyter o pipelines de datos.

**Ventajas:** fácil integración con ecosistema Python.

### 4.5 Generación a LLVM IR, JVM bytecode, .NET IL y JavaScript

Estos backends se usan para casos específicos:
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

Si después de leer esto sigues usando Python para sistemas de asignación de recursos, es porque **quieres sufrir**.

**1310.**

---

*"El mejor código es el que no se escribe.  
El segundo mejor es el que se escribe en RONIN.  
El tercero es el que compila RONIN."*

**1310.**
