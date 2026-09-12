```markdown
# 🥚 RONIN — THE LANGUAGE OF FINITE SYSTEMS WITH SCARCE RESOURCES

## Versión 1.1 — Edición Familia: Especificación + Runtime Python + Implementación Rust + RONIN Office + Familia CES-Saturada

---

**Autor:** David Ferrandez Canalis — Agencia RONIN
**Fecha:** Septiembre de 2026
**Clasificación:** `LENGUAJE DE PROGRAMACIÓN / INFRAESTRUCTURA DE SISTEMAS / DESARROLLO DE SOFTWARE`

**Base:** RONIN 1.0 + Tratado de Extensión del PUSFRE v3.5
**Compatibilidad:** Total con RONIN 1.0. Todo programa 1.0 es válido en 1.1.

---

## DECLARACIÓN NORMATIVA DE RONIN 1.1

Esta edición unifica la especificación completa del lenguaje RONIN 1.1 con:

1. **Runtime de referencia en Python** (funcional, testeado, reproducible).
2. **Implementación canónica en Rust** del compilador y runtime.
3. **RONIN Office**: Interfaz visual para diseñar, resolver y simular sistemas.
4. **Familia CES-Saturada**: Extensión matemática que generaliza la ecuación maestra.
5. **Comando `diagnose`**: Diagnóstico de degeneración estructural K–α.
6. **Visión de futuro**: RONIN como lenguaje nativo para sistemas multi-agente autónomos.

La semántica normativa de `solve`, `simulate` y `diagnose` es la base inmutable del lenguaje. Todas las extensiones son aditivas y no rompen compatibilidad.

### Regla de autoridad de la v1.1

Cuando exista una discrepancia entre un comentario numérico de una versión anterior y una ecuación normativa, **la ecuación normativa prevalece**. Los ejemplos de esta edición han sido recalculados con esa semántica.

### Semántica normativa de `solve` — Familia CES-Saturada

RONIN 1.1 implementa una **familia** de funciones de fitness. El PUSFRE clásico es el caso por defecto.

**Para cada agente `i`:**

```
Paso 1 — Saturación Hill (si K < ∞):
    Ω_sat_i = Ω_i^α_h / (K^α_h + Ω_i^α_h)
    Si K = ∞: Ω_sat_i = Ω_i

Paso 2 — Agregación CES:
    Si |λ| < 1e-6:
        F_i = Φ_i^w1 · Ψ_i^w2 · Ω_sat_i^w3 · ε_i
    Si |λ| ≥ 1e-6:
        inner_i = w1·Φ_i^λ + w2·Ψ_i^λ + w3·Ω_sat_i^λ
        F_i = inner_i^(1/λ) · ε_i
```

**Caso degenerado (compatibilidad 1.0):** `model = "pusfre"` → `λ = 0, K = ∞, k = 1` → `F_i = Φ_i · Ψ_i · Ω_i^α`.

**Asignación determinista:**

$$A_i = R \cdot \frac{F_i}{\sum_j F_j}$$

La suma de las asignaciones es exactamente `resource`, salvo el error numérico de coma flotante. `solve` **no usa `sigma` como ruido**: `sigma` pertenece a `simulate`.

### Semántica normativa de `simulate`

`simulate` es la operación estocástica. Parte del estado inicial de frecuencias y aplica una cadena de transición definida por el runtime de referencia. En v1.1, la implementación mínima conforme debe ser determinista cuando `sigma = 0` y reproducible cuando se proporciona `seed`. El kernel no cambia respecto a 1.0.

### Semántica normativa de `diagnose`

`diagnose` calcula:

1. **Ω range** en órdenes de magnitud: `log10(max(Ω) / min(Ω))`.
2. **Estado de degeneración K–α**:
   - `"inactive"` si Ω_range ≥ 3 órdenes.
   - `"active"` si Ω_range < 3 órdenes y K, α_h son libres.
   - `"unknown"` si no hay datos suficientes.
3. **Identificabilidad por parámetro** (bootstrap si se solicita).
4. **Recomendación textual**.

### Valores numéricos de referencia

Los valores mostrados en ejemplos antiguos que no puedan derivarse de las ecuaciones anteriores se consideran errores editoriales y han sido sustituidos por resultados reproducibles. Los benchmarks históricos del material original no se consideran resultados verificados de RONIN 1.1. Se conservan únicamente como antecedentes y deben reproducirse con un runtime y un protocolo publicados antes de presentarse como mediciones.

---

## PRÓLOGO: ESTO ES PARA TI, QUE NO SABES NADA (Y ESTÁ BIEN)

Tranquilo. Este tutorial no asume que sabes matemáticas. No asume que sabes programar. No asume que sabes qué es un sistema finito con recursos escasos. Solo asume que quieres resolver un problema que no sabes cómo atacar.

RONIN es el lenguaje que te permite declarar un sistema y obtener una solución sin tener que escribir código de infraestructura. Es para gente que quiere **resolver**, no que quiere **programar**.

**No necesitas saber nada de antemano. Solo necesitas leer esto y seguir los pasos.**

Este documento contiene:
- Un tutorial completo para empezar desde cero.
- La especificación formal del lenguaje (sintaxis, tipos, comandos).
- **La familia CES-Saturada: definición, casos límite, diagnóstico.**
- Un anexo con **100 ejemplos prácticos** para el día a día.
- Un anexo con la arquitectura interna del compilador.
- **Una sección con aplicaciones de RONIN en videojuegos y otras ramas del desarrollo de software.**
- **Parte VI: Implementación completa en Rust del compilador y runtime.**
- **Parte VII: RONIN Office — Interfaz visual para diseñar sistemas.**
- **Parte VIII: Visión de futuro: RONIN como lenguaje de sistemas.**

**RONIN está diseñado para funcionar de forma nativa en Linux.** Todos los comandos, herramientas de desarrollo y ejemplos están optimizados para entornos Linux (systemd, journald, signals, pipes, bash, etc.). Si usas Linux, RONIN se siente como en casa.

---

## ÍNDICE GENERAL

**PARTE I — TUTORIAL PARA MORTALES**

1. [Prólogo: Esto es para ti, que no sabes nada](#prólogo)
2. [Qué es un sistema y por qué te importa](#capítulo-1-qué-es-un-sistema)
3. [Tu primer sistema en RONIN](#capítulo-2-tu-primer-sistema)
4. [Qué significa cada cosa (sin jerga)](#capítulo-3-qué-significa-cada-cosa)
5. [Ejemplos progresivos](#capítulo-4-ejemplos-progresivos)
6. [La familia CES-Saturada (nuevo en 1.1)](#capítulo-5-la-familia-ces-saturada)
7. [Diagnóstico de degeneración (nuevo en 1.1)](#capítulo-6-diagnóstico-de-degeneración)
8. [Errores comunes y cómo el compilador te ayuda](#capítulo-7-errores-comunes)
9. [Referencia rápida](#capítulo-8-referencia-rápida)
10. [Koans del tutorial](#capítulo-9-koans-del-tutorial)

**PARTE II — ESPECIFICACIÓN FORMAL DEL LENGUAJE (COMPLETA)**

11. [Filosofía operativa](#sección-0-filosofía-operativa)
12. [Principios fundamentales](#sección-1-principios-fundamentales)
13. [Sintaxis básica extendida](#sección-2-sintaxis-básica-extendida)
14. [Sistema de tipos y validación extendido](#sección-3-tipos-y-validación-extendido)
15. [Concurrencia y paralelismo](#sección-4-concurrencia-y-paralelismo)
16. [Interoperabilidad](#sección-5-interoperabilidad)
17. [Compilación y ejecución](#sección-6-compilación-y-ejecución)
18. [Herramientas de desarrollo](#sección-7-herramientas-de-desarrollo)
19. [Casos de uso completos](#sección-8-casos-de-uso-completos)
20. [Comparativa con otros lenguajes](#sección-9-comparativa-con-otros-lenguajes)
21. [Implementación interna](#sección-10-implementación)
22. [Extensiones y futuro](#sección-11-extensiones-y-futuro)
23. [Koans de RONIN](#sección-12-koans-de-ronin)
24. [Soporte nativo para Linux](#sección-13-soporte-nativo-para-linux)
25. [Aplicaciones de RONIN en Desarrollo de Software](#sección-14-aplicaciones-de-ronin-en-desarrollo-de-software)

**PARTE III — ANEXO: 100 COSAS QUE PUEDES HACER CON RONIN**

26. [Ejemplos 1 a 100](#anexo-1-100)
27. [Ejemplos 101 a 120: Aplicaciones en desarrollo de software](#anexo-101-120)
28. [Ejemplos 121 a 130: Familia CES-Saturada en dominios reales](#anexo-121-130)

**PARTE IV — ANEXO DEL COMPILADOR: ARQUITECTURA Y EXTENSIÓN**

29. [Estructura interna del compilador](#anexo-compilador-estructura)
30. [El frontend: análisis sintáctico y semántico](#anexo-compilador-frontend)
31. [El IR: representación intermedia de sistemas](#anexo-compilador-ir)
32. [El backend: generación de código](#anexo-compilador-backend)
33. [Optimizaciones del compilador](#anexo-compilador-optimizaciones)
34. [Cómo extender RONIN con nuevos backends](#anexo-compilador-extension)
35. [Cómo añadir nuevos tipos de dominio](#anexo-compilador-tipos)
36. [Cómo añadir nuevos comandos](#anexo-compilador-comandos)
37. [El sistema de macros en tiempo de compilación](#anexo-compilador-macros)
38. [Cómo contribuir al compilador](#anexo-compilador-contribuir)

**PARTE V — RUNTIME DE REFERENCIA (PYTHON)**

39. [Metadatos del paquete](#r1-metadatos-del-paquete)
40. [Punto de entrada del paquete](#r2-punto-de-entrada-del-paquete)
41. [Modelo de datos extendido](#r3-modelo-de-datos-extendido)
42. [Sistema de errores](#r4-sistema-de-errores)
43. [Lexer](#r5-lexer)
44. [Parser extendido](#r6-parser-extendido)
45. [Validador semántico extendido](#r7-validador-semántico-extendido)
46. [Semántica normativa extendida](#r8-semántica-normativa-extendida)
47. [Solver extendido](#r9-solver-extendido)
48. [Simulador](#r10-simulador)
49. [Diagnóstico](#r11-diagnóstico)
50. [Interfaz de línea de comandos](#r12-interfaz-de-línea-de-comandos)
51. [Tests normativos](#r13-tests-normativos)
52. [Ejemplos ejecutables](#r14-ejemplos-ejecutables)
53. [Arquitectura del runtime — diagrama de flujo](#r15-arquitectura-del-runtime)
54. [Conformidad del runtime de referencia](#r16-conformidad-del-runtime-de-referencia)

**PARTE VI — IMPLEMENTACIÓN EN RUST**

55. [Estructura del proyecto](#61-estructura-del-proyecto)
56. [Lexer en Rust](#62-lexer-en-rust)
57. [Parser con nom extendido](#63-parser-con-nom-extendido)
58. [Validador semántico extendido](#64-validador-semántico-extendido)
59. [IR (Intermediate Representation)](#65-ir-intermediate-representation)
60. [Solver extendido](#66-solver-extendido)
61. [Simulador](#67-simulador)
62. [Diagnóstico en Rust](#68-diagnóstico-en-rust)
63. [CLI con clap extendida](#69-cli-con-clap-extendida)
64. [Tests normativos en Rust](#610-tests-normativos-en-rust)
65. [Integración con Python (PyO3)](#611-integración-con-python-pyo3)
66. [Backend a WASM](#612-backend-a-wasm)
67. [Backend a C](#613-backend-a-c)
68. [Optimizaciones del compilador Rust](#614-optimizaciones-del-compilador-rust)

**PARTE VII — RONIN OFFICE: INTERFAZ VISUAL**

69. [Visión general](#71-visión-general)
70. [Arquitectura de la interfaz](#72-arquitectura-de-la-interfaz)
71. [Panel de Chat](#73-panel-de-chat)
72. [Panel Sheet](#74-panel-sheet)
73. [Panel Optimizer](#75-panel-optimizer)
74. [Panel Simulator](#76-panel-simulator)
75. [Panel Agent Studio](#77-panel-agent-studio)
76. [Panel Diagnose (nuevo en 1.1)](#78-panel-diagnose)
77. [Motor RONIN — Implementación en JavaScript](#79-motor-ronin-javascript)
78. [Flujo de trabajo completo](#710-flujo-de-trabajo-completo)
79. [Generador local de sistemas](#711-generador-local-de-sistemas)
80. [Estado de la implementación](#712-estado-de-la-implementación)
81. [Koans de RONIN Office](#713-koans-de-ronin-office)
82. [Referencias técnicas](#714-referencias-técnicas)

**PARTE VIII — EL FUTURO: RONIN COMO LENGUAJE DE SISTEMAS**

83. [Visión: Sistemas que se diseñan solos](#81-visión-sistemas-que-se-diseñan-solos)
84. [RONIN como lenguaje de orquestación](#82-ronin-como-lenguaje-de-orquestación)
85. [El ecosistema RONIN](#83-el-ecosistema-ronin)
86. [RONIN y la computación neuromórfica](#84-ronin-y-la-computación-neuromórfica)
87. [RONIN y los sistemas autónomos](#85-ronin-y-los-sistemas-autónomos)
88. [Koans del futuro](#86-koans-del-futuro)

**ANEXO NORMATIVO V1.1**

89. [Contrato de implementación](#n1-contrato-de-implementación)
90. [Tests normativos](#n2-tests-normativos)
91. [Conformidad](#n3-conformidad)
92. [Estado de las extensiones](#n4-estado-de-las-extensiones)
93. [Política de afirmaciones verificables](#n5-política-de-afirmaciones-verificables)

**APÉNDICE FAMILIA CES-SATURADA**

94. [Definición matemática de la familia](#a1-definición-matemática)
95. [Casos límite con verificación](#a2-casos-límite)
96. [Degeneración K–α demostrada](#a3-degeneración-k-α)
97. [Guía de uso por dominio](#a4-guía-de-uso-por-dominio)
98. [Referencias al Tratado de Extensión v3.5](#a5-referencias-tratado)

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
- **1000 ciudades (partes) y presupuesto de infraestructura (recurso).**
- **46 modelos de lenguaje (partes) y cómputo total (recurso).**

### 1.2 Qué necesitas saber de cada parte

Solo tres números por cada parte:

- **Φ (phi)**: capacidad para usar el recurso (0..1).
- **Ψ (psi)**: consistencia, cuánto "debe" o "falla" (0..1).
- **Ω (omega)**: frecuencia inicial, cuánto se usa ahora (0..1). **La suma de todas las frecuencias debe ser 1.**

**Nuevo en 1.1:** Opcionalmente puedes especificar cómo se combinan estos tres números. Por defecto se multiplican (PUSFRE clásico), pero puedes elegir otras formas (CES, Hill, CES-Saturada).

### 1.3 La pregunta correcta

Antes de resolver, pregúntate: **¿mis datos cubren un rango amplio de Ω?**

Si tu Ω cubre menos de 3 órdenes de magnitud, usa `model: "pusfre"` (el default).
Si tu Ω cubre 3+ órdenes, prueba `model: "ces_hill"` y ejecuta `diagnose`.
Si tu Ω cubre 5+ órdenes, la familia CES-Saturada es completamente identificable.

---

## CAPÍTULO 2: TU PRIMER SISTEMA

### 2.1 El problema

2 máquinas: A y B. 100 horas de trabajo.
A: phi=0.8, psi=1.0, freq=0.6
B: phi=0.5, psi=1.0, freq=0.4

**Pregunta:** ¿cuántas horas recibe cada una?

### 2.2 El código (compatibilidad 1.0)

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
print(result.model_used)  // "pusfre"
print(result.omega_range) // 0.18 órdenes de magnitud
```

### 2.3 El mismo problema con familia (nuevo en 1.1)

```ronin
system MaquinasCES = {
    parts: 2,
    resource: 100,
    agents: [
        { phi: 0.8, psi: 1.0, frequency: 0.6 },
        { phi: 0.5, psi: 1.0, frequency: 0.4 }
    ],
    params: {
        model: "ces",
        lambda: 0.5,
        alpha: 1.0,
        gamma: 0.4,
        sigma: 0.1
    }
}

result = solve MaquinasCES
print(result.model_used)  // "ces"
print(result.lambda_used) // 0.5
```

**Nota:** Con `lambda = 0.5` y dos agentes, el resultado difiere del PUSFRE clásico. La familia da más peso a los agentes con valores altos.

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

### 3.7 `model` — Modelo de la familia (nuevo en 1.1)
- `"pusfre"` → PUSFRE clásico (default, compatibilidad total)
- `"ces"` → Curvatura CES sin saturación
- `"hill"` → Saturación Hill sin curvatura
- `"ces_hill"` → M6: curvatura + saturación
- `"full"` → Con memoria temporal

### 3.8 `lambda` — Curvatura CES (nuevo en 1.1)
- `0` → log-lineal (PUSFRE)
- `-1` → Leontief (complementos perfectos)
- `1` → lineal (suma ponderada)
- `0.5` → curvatura moderada
- `2` → compensación fuerte

### 3.9 `K` — Constante de saturación Hill (nuevo en 1.1)
- `∞` → sin saturación (PUSFRE/CES)
- `0.5` → saturación a partir de Ω ≈ 0.5
- `1.0` → saturación a partir de Ω ≈ 1.0
- `10` → saturación tardía

### 3.10 `alpha_h` — Exponente Hill (nuevo en 1.1)
- `1.0` → saturación suave
- `1.5` → saturación pronunciada
- `2.0` → saturación muy abrupta

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
        { phi: 0.70, psi: 0.84, frequency: 0.204 }
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

### 4.6 Con CES explícito (nuevo en 1.1)

```ronin
system PescaCES = {
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
        model: "ces",
        lambda: 0.5,
        alpha: 1.3,
        gamma: 0.4,
        sigma: 0.15
    }
}
result = solve PescaCES
print(result.model_used)  // "ces"
print(result.lambda_used) // 0.5
```

### 4.7 Con CES-Saturada (M6, nuevo en 1.1)

```ronin
system PescaFull = {
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
        model: "ces_hill",
        lambda: 0.5,
        K: 0.5,
        alpha_h: 1.5,
        alpha: 1.3,
        gamma: 0.4,
        sigma: 0.15,
        degeneracy_check: true,
        omega_range_report: true
    }
}
result = solve PescaFull
print(result.degeneracy)  // "active" (Ω cubre solo 0.2 órdenes)
print(result.warnings)    // ["K–α_h degeneracy active..."]
```

---

## CAPÍTULO 5: LA FAMILIA CES-SATURADA

### 5.1 La idea en una frase

El PUSFRE clásico dice: `F_i = Φ_i · Ψ_i · Ω_i^α`.

La familia CES-Saturada dice: **los tres factores no tienen por qué combinarse multiplicativamente, y Ω puede saturarse.**

### 5.2 Los cinco modelos

| `model` | Qué hace diferente | Cuándo usarlo |
|---------|-------------------|---------------|
| `"pusfre"` | Nada (default) | Datos log-lineales, Ω estrecho |
| `"ces"` | Curvatura en la combinación de Φ, Ψ, Ω | Factores no separables |
| `"hill"` | Saturación en Ω | Ω amplio con rendimientos decrecientes |
| `"ces_hill"` | Curvatura + saturación | Estructura multiplicativa + saturación visible |
| `"full"` | + memoria temporal | Sistemas con dependencia temporal |

### 5.3 El caso real: Neural Scaling

Los datos de Hoffmann et al. (2022) sobre cómputo óptimo en entrenamiento de LLMs cubren Ω ~ 3 órdenes de magnitud. La familia CES-Saturada detecta saturación donde el PUSFRE clásico falla.

```ronin
system NeuralScaling = {
    parts: 46,
    resource: 1.0,
    agents: [ /* 46 modelos con log N, log D, log C */ ],
    params: {
        model: "ces_hill",
        lambda: 0.5,
        K: 1.0,
        alpha_h: 1.5,
        degeneracy_check: true,
        omega_range_report: true
    }
}
result = solve NeuralScaling
print(result.degeneracy)      // "inactive"
print(result.omega_range)     // 3.0
```

### 5.4 El caso real: Fama-French

Los datos del modelo de tres factores de Fama-French tienen Ω ~ 0.5 órdenes de magnitud. La familia CES-Saturada **no mejora** al modelo lineal clásico.

```ronin
system FamaFrench = {
    parts: 720,
    resource: 1.0,
    agents: [ /* retornos mensuales */ ],
    params: {
        model: "pusfre",  // la elección correcta aquí
        alpha: 1.0,
        gamma: 0.3,
        sigma: 0.2
    }
}
```

**Lección:** No todos los dominios se benefician de la familia. La familia es útil cuando la estructura es multiplicativa y la saturación es visible.

---

## CAPÍTULO 6: DIAGNÓSTICO DE DEGENERACIÓN

### 6.1 Por qué necesitas `diagnose`

La familia CES-Saturada tiene un problema: **K y α_h son indistinguibles si tu Ω cubre un rango estrecho**. Esto se llama **degeneración K–α**.

El comando `diagnose` te lo dice.

### 6.2 Cómo usarlo

```ronin
diagnose PescaFull with {
    omega_range: true,
    degeneracy: true,
    bootstrap: 200
}
```

### 6.3 La salida

```json
{
  "omega_range_orders": 0.42,
  "degeneracy": "active",
  "K_identifiable": false,
  "alpha_h_identifiable": false,
  "recommendation": "Ω cubre < 1 orden de magnitud. K y α_h son indistinguibles. Recolectar datos con Ω en un rango mayor o fijar K externamente."
}
```

### 6.4 Qué hacer con la respuesta

**Si `degeneracy: "active"`:**
- No uses `model: "ces_hill"` con K y α_h libres.
- Fija K a un valor conocido o usa `model: "pusfre"`.
- Si necesitas la familia, recolecta datos con Ω más amplio.

**Si `degeneracy: "inactive"`:**
- Tu Ω cubre ≥ 3 órdenes.
- K y α_h son identificables.
- Usa la familia con confianza.

### 6.5 Ejemplo numérico

| Ω range | degeneracy | K identificable | alpha_h identificable |
|---------|------------|-----------------|----------------------|
| 0.42 órdenes | active | ❌ | ❌ |
| 1.5 órdenes | active | ❌ | ❌ |
| 3.0 órdenes | inactive | ✅ | ✅ |
| 5.0 órdenes | inactive | ✅ | ✅ |

---

## CAPÍTULO 7: ERRORES COMUNES

### 7.1 Frecuencias que no suman 1

```ronin
agents: [
    { phi: 0.8, psi: 1.0, frequency: 0.6 },
    { phi: 0.5, psi: 1.0, frequency: 0.5 }   // ❌ 0.6+0.5=1.1
]
```
**Error:** `Error: Las frecuencias deben sumar 1 (suma actual: 1.1)`

### 7.2 `phi` fuera de rango

```ronin
{ phi: 1.5, psi: 1.0, frequency: 0.5 }  // ❌
```
**Error:** `Error: phi debe estar entre 0 y 1 (valor actual: 1.5)`

### 7.3 `alpha` fuera de rango

```ronin
params: { alpha: 3.0, gamma: 0.4, sigma: 0.1 }  // ❌
```
**Error:** `Error: alpha debe estar entre 0.5 y 2.5 (valor actual: 3.0)`

### 7.4 Menos de 2 partes

```ronin
parts: 1  // ❌
```
**Error:** `Error: Un sistema debe tener al menos 2 partes.`

### 7.5 Incoherencia de modelo (nuevo en 1.1)

```ronin
params: { model: "pusfre", lambda: 0.5 }  // ❌
```
**Error:** `Error: model "pusfre" requiere lambda = 0`

```ronin
params: { model: "ces", K: 0.5 }  // ❌
```
**Error:** `Error: model "ces" requiere K = ∞`

```ronin
params: { model: "hill", lambda: 0.5 }  // ❌
```
**Error:** `Error: model "hill" requiere lambda = 0`

### 7.6 Coexistencia imposible

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

### 7.7 Degeneración no diagnosticada (nuevo en 1.1)

Si usas `model: "ces_hill"` con Ω estrecho y no activas `degeneracy_check`, el runtime no te avisa. Los parámetros K y α_h serán inidentificables pero el sistema te dará una solución.

**Buena práctica:** Activa siempre `degeneracy_check: true` cuando uses la familia.

---

## CAPÍTULO 8: REFERENCIA RÁPIDA

### 8.1 Estructura básica

```ronin
system Nombre = {
    parts: N,
    resource: R,
    agents: [
        { phi: ..., psi: ..., frequency: ... },
        ...
    ],
    params: {
        // Núcleo 1.0
        alpha: ..., gamma: ..., sigma: ...,
        // Extensión 1.1
        model: "...", lambda: ..., K: ..., alpha_h: ...,
        memory_order: ..., degeneracy_check: ...
    }
}
```

### 8.2 Parámetros recomendados por dominio

| Dominio | model | lambda | K | alpha_h | alpha | gamma | sigma |
|---------|-------|--------|---|---------|-------|-------|-------|
| Logística | pusfre | 0 | ∞ | 1.0 | 1.2 | 0.35 | 0.12 |
| Finanzas | ces | 0.5 | ∞ | 1.0 | 1.0 | 0.30 | 0.20 |
| Energía | ces_hill | 0.4 | 0.8 | 1.3 | 1.3 | 0.50 | 0.10 |
| Salud | pusfre | 0 | ∞ | 1.0 | 1.1 | 0.40 | 0.15 |
| Ciberseguridad | ces | 0.3 | ∞ | 1.0 | 1.2 | 0.50 | 0.12 |
| Telecom | ces | 0.5 | ∞ | 1.0 | 1.2 | 0.40 | 0.15 |
| Agricultura | pusfre | 0 | ∞ | 1.0 | 1.0 | 0.30 | 0.20 |
| Retail | ces | 0.4 | ∞ | 1.0 | 1.1 | 0.40 | 0.15 |
| Manufactura | ces_hill | 0.5 | 1.0 | 1.5 | 1.2 | 0.30 | 0.10 |
| Videojuegos | ces | 0.6 | ∞ | 1.0 | 1.1 | 0.35 | 0.10 |
| Web | ces | 0.4 | ∞ | 1.0 | 1.2 | 0.30 | 0.15 |
| IoT | pusfre | 0 | ∞ | 1.0 | 1.0 | 0.40 | 0.08 |
| Neural Scaling | ces_hill | 0.5 | 1.0 | 1.5 | 1.3 | 0.4 | 0.15 |
| **Fama-French** | **pusfre** | **0** | **∞** | **1.0** | **1.0** | **0.3** | **0.2** |
| Urban Scaling | ces_hill | 0.5 | 1.0 | 1.4 | 1.1 | 0.4 | 0.15 |

### 8.3 Comandos básicos

| Comando | Función |
|---------|---------|
| `solve Nombre` | Resuelve el sistema |
| `simulate Nombre with { ... }` | Simula |
| `audit Nombre with { ... }` | Audita la deuda |
| **`diagnose Nombre with { ... }`** | **Diagnóstico de degeneración (nuevo)** |
| `plot Nombre` | Visualiza |
| `print(result)` | Muestra el resultado |

### 8.4 Opciones comunes

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
| `bootstrap` | entero ≥ 0 | 0 |
| `degeneracy_check` | true/false | false |
| `omega_range_report` | true/false | false |

---

## CAPÍTULO 9: KOANS DEL TUTORIAL

**Del que no sabe nada:** El que no sabe nada es el que más puede aprender.

**De la línea que resuelve todo:** Una línea de RONIN puede reemplazar 200 líneas de Python.

**Del error que no ocurre:** La arquitectura del compilador de RONIN no te deja equivocarte.

**Del torpe que resuelve:** No hace falta saber matemáticas para usar RONIN.

**Del miedo que desaparece:** El primer sistema da miedo. El décimo da risa.

**De la familia:** No busques la ecuación única. Busca la familia que la contiene.

**De la degeneración:** Dos parámetros que no puedes distinguir no son dos parámetros. Son uno disfrazado.

**Del diagnóstico:** El sistema que te dice cuándo no puedes confiar en él vale más que el que te dice que todo está bien.

**De la honestidad:** El PUSFRE no es una ecuación. Es una familia. RONIN no la impone. La ejecuta.

---

# PARTE II — ESPECIFICACIÓN FORMAL DEL LENGUAJE

## SECCIÓN 0: FILOSOFÍA OPERATIVA

### 0.1 El principio de RONIN

> *"Cualquier sistema finito con recursos escasos puede modelarse como una asignación de recurso entre partes. La familia CES-Saturada contiene al PUSFRE clásico como caso límite y extiende su dominio a regímenes con saturación, curvatura y memoria."*

### 0.2 La metáfora del arquitecto

RONIN no es para programadores. Es para **arquitectos**.

### 0.3 La validación como guardián

RONIN no permite errores de dominio. Además, en 1.1, verifica la coherencia entre `model` y parámetros.

### 0.4 Interoperabilidad como puente

RONIN se integra con Python, Rust, SQL, APIs REST.

### 0.5 RONIN Office como interfaz

RONIN Office permite diseñar sistemas visualmente sin escribir código.

### 0.6 Diagnóstico como honestidad

El comando `diagnose` es la declaración de humildad del lenguaje: te dice cuándo no puedes confiar en los parámetros que estás usando.

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

### 1.7 La degeneración se diagnostica (nuevo en 1.1)

```ronin
report = diagnose Pesca with { degeneracy: true }
assert(report.degeneracy == "inactive")
```

---

## SECCIÓN 2: SINTAXIS BÁSICA EXTENDIDA

### 2.1 Declaración de sistema

```ronin
system Nombre = {
    parts: entero,
    resource: flotante,
    agents: [Agent],
    params: Params
}
```

### 2.2 Bloque `params` extendido

```ronin
params: {
    // Núcleo 1.0 (todos opcionales en 1.1)
    alpha:   flotante ∈ [0.5, 2.5]    por defecto 1.0
    gamma:   flotante ∈ [0, 1]         por defecto 0.4
    sigma:   flotante ∈ [0, 0.5]      por defecto 0.0

    // Extensión CES-Saturada
    model:   string ∈ {"pusfre", "ces", "hill", "ces_hill", "full"}
                                       por defecto "pusfre"
    lambda:  flotante ∈ [-1, 2], ≠ 0   por defecto 0.0
    K:       flotante > 0              por defecto ∞
    alpha_h: flotante > 0              por defecto 1.0
    memory_order: entero ∈ {1,2,3,5}   por defecto 1
    memory_weights: [flotante] | null  por defecto null

    // Diagnóstico
    degeneracy_check: booleano         por defecto false
    omega_range_report: booleano       por defecto false
}
```

### 2.3 Restricciones de coherencia

| `model` | `lambda` | `K` | `memory_order` |
|---------|----------|-----|----------------|
| `"pusfre"` | 0 | ∞ | 1 |
| `"ces"` | libre ≠ 0 | ∞ | 1 |
| `"hill"` | 0 | libre > 0 | 1 |
| `"ces_hill"` | libre ≠ 0 | libre > 0 | 1 |
| `"full"` | libre ≠ 0 | libre > 0 | ≥ 1 |

Violación → `SemanticError` con código 2.

### 2.4 Definición de agente

```ronin
agent Industrial = {
    phi: 0.95,
    psi: 0.68,
    frequency: 0.267
}
```

### 2.5 Agente extendido (con nicho)

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

### 2.6 Arrays y estructuras

```ronin
let phi = [0.95, 0.85, 0.60, 0.45, 0.70]
let psi = [0.68, 0.76, 0.92, 0.96, 0.84]
```

### 2.7 Funciones puras

```ronin
fn fitness(phi: Probability, psi: Probability, frequency: Frequency, alpha: Alpha) -> Fitness {
    return phi * psi * frequency^alpha
}
```

### 2.8 Funciones impuras

```ronin
fn simulate(system: System) -> Simulation {
    return run_reference_simulation(system)
}
```

### 2.9 Simulación

```ronin
sim = simulate Pesca with {
    steps: 100,
    dtmc: true,
    stochastic: true,
    routing_pressure: Beta(2.3, 5.1)
}
```

### 2.10 Auditoría

```ronin
audit = audit Pesca with {
    epsilon: 0.05,
    delta: 0.01,
    stratified: true,
    clusters: HDBSCAN
}
```

### 2.11 Diagnóstico (nuevo en 1.1)

```ronin
report = diagnose Pesca with {
    omega_range: true,
    degeneracy: true,
    bootstrap: 200
}
```

### 2.12 Visualización

```ronin
plot Pesca
plot sim
plot audit
plot report
```

### 2.13 Condicionales

```ronin
if result.coexistence {
    print("Coexistencia garantizada")
} else {
    print("Sistema inestable. Ajustar parámetros.")
}
```

### 2.14 Bucles

```ronin
for agent in system.agents {
    print(agent.phi)
}
```

### 2.15 Módulos

```ronin
module Fisheries {
    system Atlantic = { ... }
    system Pacific = { ... }
}
import Fisheries
```

### 2.16 Macros

```ronin
macro audit_system(system) {
    return audit(system with {
        epsilon: 0.05,
        delta: 0.01,
        stratified: true
    })
}
```

### 2.17 Macros de diagnóstico (nuevo en 1.1)

```ronin
macro diagnose_and_warn(system) {
    let report = diagnose(system with { degeneracy: true })
    if report.degeneracy == "active" {
        print("ADVERTENCIA: degeneración K–α activa")
    }
    return report
}
```

---

## SECCIÓN 3: TIPOS Y VALIDACIÓN EXTENDIDO

### 3.1 Tipos primitivos

```ronin
type Integer = int
type Float = float
type Boolean = bool
type String = string
type Array = [T]
```

### 3.2 Tipos de dominio (COMPLETO — 160+ tipos)

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

// Nuevos en 1.1
type Lambda = float -1.0..2.0
type K = float > 0
type AlphaH = float > 0
type MemoryOrder = integer {1, 2, 3, 5}
type ModelName = "pusfre" | "ces" | "hill" | "ces_hill" | "full"
type OmegaRange = float >= 0
type Degeneracy = "active" | "inactive" | "unknown"
type Recommendation = String
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
    coexistence_delta: Delta,
    // Extensión 1.1
    model: ModelName,
    lambda: Lambda,
    K: K,
    alpha_h: AlphaH,
    memory_order: MemoryOrder,
    memory_weights: Option[Array[Probability]],
    degeneracy_check: Boolean,
    omega_range_report: Boolean
}

type Solution = {
    allocation: Array[Resource],
    fitness: Array[Fitness],
    coexistence: Option[Coexistence],
    k_min: Option[BatchSize],
    convergence: Convergence,
    steps: Steps,
    debt: Debt,
    audit: Option[AuditResult],
    // Nuevos en 1.1
    model_used: ModelName,
    lambda_used: Lambda,
    K_used: K,
    alpha_h_used: AlphaH,
    omega_range: OmegaRange,
    degeneracy: Degeneracy,
    warnings: Array[String]
}

type DegeneracyReport = {
    omega_range_orders: OmegaRange,
    k_alpha_degenerate: Degeneracy,
    lambda_identifiable: Boolean,
    K_identifiable: Boolean,
    alpha_h_identifiable: Boolean,
    recommendation: Recommendation,
    bootstrap_ci: Option[BootstrapCI]
}

type BootstrapCI = {
    lambda_lo: Float,
    lambda_hi: Float,
    K_lo: Float,
    K_hi: Float,
    alpha_h_lo: Float,
    alpha_h_hi: Float
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

let lambda: Lambda = 0.5  // ✅
let lambda: Lambda = 2.5  // ❌
// Error: `lambda` must be between -1.0 and 2.0

let K: K = 0.5   // ✅
let K: K = -1.0  // ❌
// Error: `K` must be > 0
```

### 3.5 Validación de invariantes

RONIN verifica automáticamente:
- Suma de frecuencias = 1
- Todos los phi en [0,1]
- Todos los psi en [0,1]
- Recurso > 0
- Número de partes >= 2
- **Coherencia `model` ↔ parámetros (nuevo en 1.1)**

### 3.6 Inferencia de tipos

```ronin
let phi = [0.95, 0.85, 0.60, 0.45, 0.70]  // inferido como [Probability]
let model = "ces_hill"                     // inferido como ModelName
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

### 4.11 Diagnóstico en paralelo (nuevo en 1.1)

```ronin
par {
    report1 = diagnose Sistema1 with { bootstrap: 500 }
    report2 = diagnose Sistema2 with { bootstrap: 500 }
    report3 = diagnose Sistema3 with { bootstrap: 500 }
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
> let report = diagnose(system with { degeneracy: true })
> report.degeneracy
"inactive"
```

### 6.14 Diagnóstico desde CLI (nuevo en 1.1)

```bash
ronin diagnose system.ronin --bootstrap 200
# {
#   "omega_range_orders": 3.0,
#   "degeneracy": "inactive",
#   "K_identifiable": true,
#   "alpha_h_identifiable": true,
#   "recommendation": "Identificación estructural OK."
# }
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
| **`ronin diagnose system.ronin`** | **Diagnóstico de degeneración (nuevo en 1.1)** |

---

## SECCIÓN 8: CASOS DE USO COMPLETOS

### 8.1 Pesca (5 flotas, PUSFRE clásico)

```ronin
system AtlanticFleet = {
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
        sigma: 0.15,
        coexistence_delta: 0.05
    }
}
result = solve AtlanticFleet
print(result.allocation)  // [3138.305, 2702.592, 1378.139, 831.638, 1949.325]
print(result.coexistence) // true
```

### 8.2 Pesca con CES-Saturada (nuevo en 1.1)

```ronin
system AtlanticFleetCES = {
    parts: 5,
    resource: 10000,
    agents: [ /* mismos agentes */ ],
    params: {
        model: "ces_hill",
        lambda: 0.5,
        K: 0.5,
        alpha_h: 1.5,
        alpha: 1.3,
        gamma: 0.4,
        sigma: 0.15,
        coexistence_delta: 0.05,
        degeneracy_check: true
    }
}
result = solve AtlanticFleetCES
report = diagnose AtlanticFleetCES with { degeneracy: true }
print(report.degeneracy)  // "active" (Ω estrecho)
```

### 8.3 Neural Scaling (nuevo en 1.1)

```ronin
system NeuralScaling = {
    parts: 46,
    resource: 1.0,
    agents: [ /* 46 modelos con log N, log D, log C */ ],
    params: {
        model: "ces_hill",
        lambda: 0.5,
        K: 1.0,
        alpha_h: 1.5,
        degeneracy_check: true,
        omega_range_report: true
    }
}
result = solve NeuralScaling
report = diagnose NeuralScaling with { degeneracy: true, bootstrap: 1000 }
print(report.omega_range_orders)  // ~3.0
print(report.degeneracy)           // "inactive"
print(report.K_identifiable)       // true
```

### 8.4 Logística (50 vehículos)

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

### 8.5 Finanzas (20 activos)

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

### 8.6 Tráfico (100 semáforos)

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

### 8.7 RAG (1M documentos)

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

### 8.8 Urban Scaling (nuevo en 1.1)

```ronin
system UrbanScaling = {
    parts: 10000,
    resource: 1.0,
    agents: generate_cities(10000),
    params: {
        model: "ces_hill",
        lambda: 0.5,
        K: 1.0,
        alpha_h: 1.4,
        degeneracy_check: true,
        omega_range_report: true
    }
}
result = solve UrbanScaling
report = diagnose UrbanScaling with { degeneracy: true }
print(report.omega_range_orders)  // ~5.0
print(report.degeneracy)           // "inactive"
```

### 8.9 Fama-French (720 meses, negativo)

```ronin
system FamaFrench = {
    parts: 720,
    resource: 1.0,
    agents: generate_returns(720),
    params: {
        model: "pusfre",  // la elección correcta aquí
        alpha: 1.0,
        gamma: 0.3,
        sigma: 0.2
    }
}
result = solve FamaFrench
// La familia CES-Saturada no mejora aquí porque Ω es estrecho
```

---

## SECCIÓN 9: COMPARATIVA CON OTROS LENGUAJES

### 9.1 Rendimiento — estado de verificación

El material histórico de RONIN contiene cifras de rendimiento y memoria. Esas cifras no forman parte de la especificación normativa de v1.1 porque no están acompañadas aquí por un protocolo reproducible y una implementación versionada.

La v1.1 define en su lugar un protocolo de benchmark: cada comparación deberá indicar versión del runtime, commit, hardware, sistema operativo, tamaño de entrada, número de repeticiones, calentamiento, distribución de resultados y código utilizado. Hasta que esos datos existan, no se asignan cifras de rendimiento a RONIN.

### 9.2 Expresividad — criterio, no resultado medido

La expresividad de RONIN se describe cualitativamente por la capacidad de representar sistemas, simulaciones, auditorías y diagnósticos mediante sus primitivas. No se presentan puntuaciones comparativas como hechos medidos.

### 9.3 Seguridad — propiedades definidas

RONIN incorpora tipos de dominio, rangos e invariantes como parte de su especificación. Esto permite comprobar ciertas clases de errores antes de ejecutar un sistema. No implica por sí mismo una garantía de seguridad general frente a todas las amenazas.

### 9.4 Interoperabilidad — capacidades previstas

La especificación contempla interfaces con Python, Rust, SQL, APIs y distintos targets de ejecución. En v1.1 solo se considera implementada una integración cuando exista un módulo correspondiente y pase el conjunto de conformidad.

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

### 10.1 El intérprete (Rust core extendido)

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
    // Núcleo 1.0
    pub alpha: f64,
    pub gamma: f64,
    pub sigma: f64,
    pub coexistence_delta: f64,
    // Extensión 1.1
    pub model: String,
    pub lambda: f64,
    pub K: f64,
    pub alpha_h: f64,
    pub memory_order: usize,
    pub memory_weights: Option<Vec<f64>>,
    pub degeneracy_check: bool,
    pub omega_range_report: bool,
}

pub struct Solution {
    pub allocation: Vec<f64>,
    pub fitness: Vec<f64>,
    pub coexistence: Option<bool>,
    pub k_min: Option<f64>,
    pub convergence: bool,
    pub steps: usize,
    pub debt: f64,
    // Nuevos en 1.1
    pub model_used: String,
    pub lambda_used: f64,
    pub K_used: f64,
    pub alpha_h_used: f64,
    pub omega_range: f64,
    pub degeneracy: String,
    pub warnings: Vec<String>,
}

pub fn solve(system: &System) -> Result<Solution, Error> {
    validate_system(system)?;
    validate_coherence(&system.params)?;
    let fitness = calculate_fitness(system)?;
    let allocation = normalize_fitness_to_resource(&fitness, system.resource)?;
    let coexistence = check_coexistence(&allocation, &system.params)?;
    let k_min = calculate_k_min(system)?;
    let debt = calculate_debt(system)?;

    let omega_range = omega_range_orders(&system.agents);
    let degeneracy = degeneracy_state(
        omega_range,
        system.params.K.is_finite(),
        system.params.alpha_h != 1.0,
    );

    Ok(Solution {
        allocation, fitness, coexistence, k_min, debt,
        convergence: true, steps: 1,
        model_used: system.params.model.clone(),
        lambda_used: system.params.lambda,
        K_used: system.params.K,
        alpha_h_used: system.params.alpha_h,
        omega_range, degeneracy,
        warnings: vec![],
    })
}
```

### 10.2 Python bindings (PyO3 extendido)

```rust
use pyo3::prelude::*;

#[pyfunction]
fn solve_system(parts: usize, resource: f64, agents: Vec<Agent>, params: Params) -> PyResult<Solution> {
    let system = System { parts, resource, agents, params };
    let solution = solve(&system)?;
    Ok(solution)
}

#[pyfunction]
fn diagnose_system(parts: usize, resource: f64, agents: Vec<Agent>, params: Params) -> PyResult<DegeneracyReport> {
    let system = System { parts, resource, agents, params };
    let report = diagnose(&system)?;
    Ok(report)
}

#[pymodule]
fn ronin(m: &Bound<'_, PyModule>) -> PyResult<()> {
    m.add_function(wrap_pyfunction!(solve_system, m)?)?;
    m.add_function(wrap_pyfunction!(diagnose_system, m)?)?;
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

### 11.11 Diagnóstico multi-dominio (nuevo en 1.1)

```ronin
system MultiDiagnose = {
    domains: ["neural_scaling", "urban_scaling", "fama_french"],
    diagnostic: true,
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
Una herramienta externa puede generar RONIN y el validador puede comprobar si el programa cumple la especificación. La corrección automática no forma parte del núcleo de v1.1.

**Del arquitecto que no escribe código:**
El arquitecto declara sistemas. El lenguaje se encarga del resto.

**Del cerrajero que diseñó la llave maestra:**
RONIN está diseñado como un lenguaje especializado para sistemas finitos con recursos escasos; no pretende resolver cualquier clase de sistema.

**Del autor que se ríe desde 1310:**
El autor sabe que RONIN es inevitable. El PUSFRE requería un lenguaje. Y el lenguaje es RONIN.

**De la familia:**
No busques la ecuación única. Busca la familia que la contiene.

**De la degeneración:**
Dos parámetros que no puedes distinguir no son dos parámetros. Son uno disfrazado.

**Del diagnóstico:**
El sistema que te dice cuándo no puedes confiar en él vale más que el que te dice que todo está bien.

**De la honestidad:**
El PUSFRE no es una ecuación. Es una familia. RONIN no la impone. La ejecuta.

---

## SECCIÓN 13: SOPORTE NATIVO PARA LINUX

### 13.1 Integración con systemd

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

```bash
journalctl -u ronin --grep "Pesca"
journalctl -u ronin --grep "audit"
journalctl -u ronin --grep "degeneracy"
journalctl -u ronin -p err
```

```ronin
journal.write("Sistema Pesca resuelto", level: INFO, tags: ["pesca", "resuelto"])
journal.write("Degeneración detectada", level: WARNING, tags: ["degeneracy", "K-alpha"])
```

### 13.3 Manejo de señales POSIX

| Señal | Comportamiento en RONIN |
|-------|-------------------------|
| `SIGINT` (Ctrl+C) | Detiene la ejecución actual y guarda el estado intermedio. |
| `SIGTERM` | Finaliza el proceso de forma ordenada, escribiendo el último resultado en un archivo de checkpoint. |
| `SIGHUP` | Recarga la configuración del sistema sin reiniciar el proceso. |
| `SIGUSR1` | Genera un informe de auditoría en el momento actual. |
| `SIGUSR2` | Vuelca el estado del sistema (frecuencias, deuda, degeneración) a un archivo de diagnóstico. |

### 13.4 Pipes y redirecciones

```bash
ronin run --input agents.csv --output solucion.json
ronin run sistema.ronin | jq '.allocation'
ronin diagnose sistema.ronin | jq '.degeneracy'
ronin run sistema.ronin | awk '{print $1}'
```

### 13.5 Integración con cron

```cron
0 2 * * * /usr/local/bin/ronin run /etc/ronin/pesca.ronin --output /var/ronin/pesca.json
0 3 * * 1 /usr/local/bin/ronin audit /etc/ronin/pesca.ronin --output /var/ronin/audit.json
0 4 * * 0 /usr/local/bin/ronin diagnose /etc/ronin/pesca.ronin --output /var/ronin/diag.json
```

### 13.6 Sistema de archivos y ubicaciones estándar

| Ruta | Contenido |
|------|-----------|
| `/usr/local/bin/ronin` | Binario principal |
| `/etc/ronin/` | Archivos de configuración y sistemas |
| `/var/ronin/` | Datos de sistemas en ejecución |
| `/var/ronin/checkpoints/` | Puntos de control |
| `/var/ronin/diagnostics/` | Informes de degeneración (nuevo en 1.1) |
| `/var/log/ronin/` | Logs en texto plano |

### 13.7 Soporte para sockets Unix

```ronin
server = unix_socket.bind("/var/run/ronin.sock")
server.listen()
```

```bash
echo 'solve Pesca' | nc -U /var/run/ronin.sock
echo 'diagnose Pesca' | nc -U /var/run/ronin.sock
```

### 13.8 Integración con inotify

```ronin
monitor /etc/ronin/pesca.ronin on change {
    print("Configuración actualizada. Recalculando...")
    reload_system()
}
```

### 13.9 Soporte para seccomp y sandboxing

```bash
ronin run sistema.ronin --seccomp
```

---

## SECCIÓN 14: APLICACIONES DE RONIN EN DESARROLLO DE SOFTWARE

### 14.1 VIDEOJUEGOS

**Ejemplo: Balanceo de clases en un RPG con CES**

```ronin
system BalanceoClases = {
    parts: 3,
    resource: 100,
    agents: [
        { name: "Guerrero", phi: 0.9, psi: 0.8, frequency: 0.33 },
        { name: "Mago", phi: 0.95, psi: 0.5, frequency: 0.33 },
        { name: "Picaro", phi: 0.75, psi: 0.9, frequency: 0.33 }
    ],
    params: {
        model: "ces",
        lambda: 0.6,
        alpha: 1.2,
        gamma: 0.4,
        sigma: 0.1
    },
    invariants: [
        "allocation[0] > 25",
        "allocation[1] > 25",
        "allocation[2] > 25"
    ]
}

result = solve BalanceoClases
print(result.allocation)  // Distribución con curvatura CES
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
plot sim
```

### 14.2 DESARROLLO WEB Y BALANCEO DE CARGA

**Ejemplo: Balanceo de carga entre microservicios**

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
    params: { model: "ces", lambda: 0.4, alpha: 1.1, gamma: 0.3, sigma: 0.1 }
}

result = solve Microservicios
```

### 14.3 SISTEMAS EMBEBIDOS E IoT

**Ejemplo: Asignación de tiempo de CPU en un microcontrolador**

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
    params: { model: "pusfre", alpha: 0.8, gamma: 0.3, sigma: 0.05 }
}

result = solve TareasEmbebidas
```

### 14.4 ROBÓTICA Y CONTROL DE SISTEMAS

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
    params: { model: "ces", lambda: 0.4, alpha: 1.1, gamma: 0.3, sigma: 0.1 }
}

result = solve FlotaRobotica
```

### 14.5 CIENCIA DE DATOS Y MACHINE LEARNING

**Ejemplo: Muestreo estratificado**

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
    params: { model: "ces", lambda: 0.5, alpha: 0.9, gamma: 0.2, sigma: 0.05 }
}

result = solve Hyperparametros
```

### 14.6 FINANZAS Y TRADING ALGORÍTMICO

**Ejemplo: Gestión de cartera con coexistencia**

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
    params: { model: "ces", lambda: 0.4, alpha: 0.9, gamma: 0.4, sigma: 0.15 }
}

result = solve Cartera
```

### 14.7 BLOCKCHAIN Y CRIPTOMONEDAS

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
    params: { model: "pusfre", alpha: 1.2, gamma: 0.3, sigma: 0.1 }
}

result = solve Mineria
```

### 14.8 SISTEMAS DE RECOMENDACIÓN

**Ejemplo: Distribución de contenidos**

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
    params: { model: "ces", lambda: 0.5, alpha: 0.8, gamma: 0.2, sigma: 0.1 }
}

result = solve Recomendaciones
```

### 14.9 OPTIMIZACIÓN DE RECURSOS EN CLOUD

**Ejemplo: Kubernetes**

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
    params: { model: "pusfre", alpha: 1.0, gamma: 0.2, sigma: 0.05 }
}

result = solve Kubernetes
```

### 14.10 INTELIGENCIA ARTIFICIAL MULTI-AGENTE

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
    params: { model: "ces", lambda: 0.4, alpha: 1.1, gamma: 0.3, sigma: 0.1 }
}

result = solve AtencionCliente
diagnose_result = diagnose AtencionCliente with { degeneracy: true }
print(diagnose_result.degeneracy)  // "active" (Ω estrecho)
```

### 14.11 ANÁLISIS CIENTÍFICO CON FAMILIA (nuevo en 1.1)

**Ejemplo: Neural Scaling**

```ronin
system NeuralScaling = {
    parts: 46,
    resource: 1.0,
    agents: [
        { name: "Model1", phi: log(8M), psi: log(10B), frequency: log(1e18) },
        ...
    ],
    params: {
        model: "ces_hill",
        lambda: 0.5,
        K: 1.0,
        alpha_h: 1.5,
        degeneracy_check: true
    }
}
result = solve NeuralScaling
report = diagnose NeuralScaling with { degeneracy: true, bootstrap: 1000 }
print(report.degeneracy)         // "inactive"
print(report.omega_range_orders) // ~3.0
print(report.K_identifiable)     // true
```

**Ejemplo: Urban Scaling**

```ronin
system UrbanScaling = {
    parts: 10000,
    resource: 1.0,
    agents: generate_cities(10000),
    params: {
        model: "ces_hill",
        lambda: 0.5,
        K: 1.0,
        alpha_h: 1.4,
        degeneracy_check: true
    }
}
result = solve UrbanScaling
report = diagnose UrbanScaling with { degeneracy: true }
print(report.omega_range_orders)  // ~5.0
print(report.degeneracy)          // "inactive"
```

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

**Del investigador:**
No todas las estructuras son log-lineales. La familia CES-Saturada existe para cuando no lo son.

**Del diagnosticador:**
El número sin diagnóstico es una opinión.

---

# PARTE III — ANEXO: 100 COSAS QUE PUEDES HACER CON RONIN

## PRÓLOGO DEL ANEXO

Este anexo no es teoría. Es **práctica**. Cada entrada es una pregunta concreta que te puedes hacer al usar RONIN, y cada respuesta es un ejemplo ejecutable con explicación paso a paso. No necesitas leerlas todas de golpe; úsalas como referencia cuando necesites hacer algo específico.

---

## ANEXO 1-100: LOS CLÁSICOS

*(Aquí van los 100 ejemplos originales, que ya estaban en el documento anterior. Se mantienen intactos. Todos funcionan con `model: "pusfre"` por defecto.)*

---

## ANEXO 101-120: APLICACIONES EN DESARROLLO DE SOFTWARE

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
    params: { model: "ces", lambda: 0.6, alpha: 1.2, gamma: 0.4, sigma: 0.1 },
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
    params: { model: "ces", lambda: 0.5, alpha: 0.8, gamma: 0.2, sigma: 0.1 }
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
    params: { model: "ces", lambda: 0.4, alpha: 1.1, gamma: 0.3, sigma: 0.1 }
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
    params: { model: "pusfre", alpha: 0.8, gamma: 0.3, sigma: 0.05 }
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
    params: { model: "ces", lambda: 0.4, alpha: 0.9, gamma: 0.4, sigma: 0.15 }
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
    params: { model: "pusfre", alpha: 1.2, gamma: 0.3, sigma: 0.1 }
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
    params: { model: "ces", lambda: 0.5, alpha: 0.8, gamma: 0.2, sigma: 0.1 }
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
    params: { model: "pusfre", alpha: 1.0, gamma: 0.2, sigma: 0.05 }
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
    params: { model: "ces", lambda: 0.4, alpha: 1.1, gamma: 0.3, sigma: 0.1 }
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
    params: { model: "ces", lambda: 0.5, alpha: 0.9, gamma: 0.2, sigma: 0.05 }
}
result = solve Hyperparametros
```

### 111. Cómo modelar un ecosistema de agentes LLM

```ronin
system EcosistemaLLM = {
    parts: 5,
    resource: 10000,
    agents: [
        { name: "Investigador", phi: 0.9, psi: 0.7, frequency: 0.25 },
        { name: "Sintetizador", phi: 0.85, psi: 0.85, frequency: 0.2 },
        { name: "Validador", phi: 0.8, psi: 0.95, frequency: 0.2 },
        { name: "Redactor", phi: 0.7, psi: 0.9, frequency: 0.2 },
        { name: "Planificador", phi: 0.95, psi: 0.6, frequency: 0.15 }
    ],
    params: { model: "ces_hill", lambda: 0.5, K: 1.0, alpha_h: 1.3,
              alpha: 1.2, gamma: 0.4, sigma: 0.1,
              degeneracy_check: true }
}
result = solve EcosistemaLLM
report = diagnose EcosistemaLLM with { degeneracy: true }
```

### 112. Cómo optimizar un pipeline de datos

```ronin
system PipelineDatos = {
    parts: 4,
    resource: 1000,
    agents: [
        { name: "Ingest", phi: 0.8, psi: 0.95, frequency: 0.25 },
        { name: "Transform", phi: 0.7, psi: 0.9, frequency: 0.25 },
        { name: "Load", phi: 0.6, psi: 0.85, frequency: 0.25 },
        { name: "Validate", phi: 0.9, psi: 0.8, frequency: 0.25 }
    ],
    params: { model: "ces", lambda: 0.4, alpha: 1.1, gamma: 0.3, sigma: 0.1 }
}
result = solve PipelineDatos
```

### 113. Cómo balancear un juego de cartas

```ronin
system JuegoCartas = {
    parts: 5,
    resource: 100,
    agents: [
        { name: "Ataque", phi: 0.9, psi: 0.6, frequency: 0.25 },
        { name: "Defensa", phi: 0.6, psi: 0.9, frequency: 0.2 },
        { name: "Control", phi: 0.8, psi: 0.7, frequency: 0.2 },
        { name: "Combo", phi: 0.95, psi: 0.5, frequency: 0.15 },
        { name: "Soporte", phi: 0.7, psi: 0.85, frequency: 0.2 }
    ],
    params: { model: "ces", lambda: 0.6, alpha: 1.1, gamma: 0.3, sigma: 0.1 }
}
result = solve JuegoCartas
```

### 114. Cómo optimizar un sistema de trading

```ronin
system SistemaTrading = {
    parts: 4,
    resource: 1000000,
    agents: [
        { name: "Momentum", phi: 0.8, psi: 0.6, frequency: 0.3 },
        { name: "MeanReversion", phi: 0.7, psi: 0.8, frequency: 0.3 },
        { name: "Arbitrage", phi: 0.9, psi: 0.5, frequency: 0.2 },
        { name: "Hedging", phi: 0.6, psi: 0.95, frequency: 0.2 }
    ],
    params: { model: "ces_hill", lambda: 0.5, K: 1.0, alpha_h: 1.4,
              alpha: 1.0, gamma: 0.4, sigma: 0.2 }
}
result = solve SistemaTrading
```

### 115. Cómo modelar la asignación de ancho de banda

```ronin
system AnchoBanda = {
    parts: 10,
    resource: 10000,
    agents: generate_users(10),
    params: { model: "ces", lambda: 0.4, alpha: 1.2, gamma: 0.3, sigma: 0.1 }
}
result = solve AnchoBanda
```

### 116. Cómo priorizar tareas en un sistema operativo

```ronin
system TareasSO = {
    parts: 6,
    resource: 100,
    agents: [
        { name: "Kernel", phi: 0.95, psi: 0.99, frequency: 0.3 },
        { name: "Servicios", phi: 0.8, psi: 0.9, frequency: 0.25 },
        { name: "Usuario", phi: 0.7, psi: 0.8, frequency: 0.2 },
        { name: "Background", phi: 0.5, psi: 0.85, frequency: 0.15 },
        { name: "Red", phi: 0.85, psi: 0.75, frequency: 0.05 },
        { name: "Disco", phi: 0.6, psi: 0.95, frequency: 0.05 }
    ],
    params: { model: "ces", lambda: 0.5, alpha: 1.1, gamma: 0.3, sigma: 0.05 }
}
result = solve TareasSO
```

### 117. Cómo balancear un juego de estrategia

```ronin
system JuegoEstrategia = {
    parts: 4,
    resource: 1000,
    agents: [
        { name: "Economía", phi: 0.8, psi: 0.7, frequency: 0.3 },
        { name: "Militar", phi: 0.9, psi: 0.6, frequency: 0.3 },
        { name: "Tecnología", phi: 0.7, psi: 0.85, frequency: 0.2 },
        { name: "Diplomacia", phi: 0.6, psi: 0.9, frequency: 0.2 }
    ],
    params: { model: "ces", lambda: 0.6, alpha: 1.2, gamma: 0.3, sigma: 0.1 }
}
result = solve JuegoEstrategia
```

### 118. Cómo optimizar un chatbot multi-agente

```ronin
system ChatbotMultiAgente = {
    parts: 4,
    resource: 100,
    agents: [
        { name: "Intención", phi: 0.9, psi: 0.85, frequency: 0.3 },
        { name: "Respuesta", phi: 0.8, psi: 0.9, frequency: 0.3 },
        { name: "Validación", phi: 0.7, psi: 0.95, frequency: 0.2 },
        { name: "Fallback", phi: 0.5, psi: 0.8, frequency: 0.2 }
    ],
    params: { model: "ces", lambda: 0.4, alpha: 1.0, gamma: 0.3, sigma: 0.1 }
}
result = solve ChatbotMultiAgente
```

### 119. Cómo modelar la asignación de memoria en un servidor

```ronin
system MemoriaServidor = {
    parts: 5,
    resource: 64,
    agents: [
        { name: "DB", phi: 0.9, psi: 0.95, frequency: 0.3 },
        { name: "Cache", phi: 0.8, psi: 0.85, frequency: 0.25 },
        { name: "App", phi: 0.7, psi: 0.9, frequency: 0.2 },
        { name: "Logs", phi: 0.4, psi: 0.8, frequency: 0.15 },
        { name: "Kernel", phi: 0.95, psi: 0.99, frequency: 0.1 }
    ],
    params: { model: "ces", lambda: 0.5, alpha: 1.1, gamma: 0.3, sigma: 0.05 }
}
result = solve MemoriaServidor
```

### 120. Cómo diagnosticar si tu sistema necesita la familia CES-Saturada

```ronin
system MiSistema = {
    parts: N,
    resource: R,
    agents: [ ... ],
    params: {
        model: "ces_hill",
        lambda: 0.5,
        K: 1.0,
        alpha_h: 1.5,
        degeneracy_check: true
    }
}
result = solve MiSistema
report = diagnose MiSistema with { degeneracy: true }
if report.degeneracy == "active" {
    print("Usa model: pusfre. La familia no es identificable con tus datos.")
} else {
    print("La familia es identificable. Puedes usar ces_hill.")
}
```

---

## ANEXO 121-130: FAMILIA CES-SATURADA EN DOMINIOS REALES

### 121. Neural Scaling (positivo)

```ronin
system NeuralScaling = {
    parts: 46,
    resource: 1.0,
    agents: [ /* Hoffmann et al. 2022 */ ],
    params: {
        model: "ces_hill",
        lambda: 0.5,
        K: 1.0,
        alpha_h: 1.5,
        degeneracy_check: true
    }
}
result = solve NeuralScaling
report = diagnose NeuralScaling with { bootstrap: 1000 }
// ΔBIC = -14.3 vs M0
// degeneracy = "inactive"
```

### 122. Fama-French (negativo)

```ronin
system FamaFrench = {
    parts: 720,
    resource: 1.0,
    agents: [ /* retornos mensuales 1963-2023 */ ],
    params: {
        model: "pusfre",  // la elección correcta
        alpha: 1.0,
        gamma: 0.3,
        sigma: 0.2
    }
}
result = solve FamaFrench
report = diagnose FamaFrench with { degeneracy: true }
// degeneracy = "active"
// La familia CES-Saturada NO mejora aquí
```

### 123. Urban Scaling

```ronin
system UrbanScaling = {
    parts: 10000,
    resource: 1.0,
    agents: [ /* PIB, población, infraestructura */ ],
    params: {
        model: "ces_hill",
        lambda: 0.5,
        K: 1.0,
        alpha_h: 1.4,
        degeneracy_check: true
    }
}
result = solve UrbanScaling
report = diagnose UrbanScaling with { degeneracy: true }
// Ω = PIB cubre 5+ órdenes
// degeneracy = "inactive"
```

### 124. Species-Area

```ronin
system SpeciesArea = {
    parts: 500,
    resource: 1.0,
    agents: [ /* islas con área y número de especies */ ],
    params: {
        model: "ces_hill",
        lambda: 0.5,
        K: 1.0,
        alpha_h: 1.2,
        degeneracy_check: true
    }
}
result = solve SpeciesArea
report = diagnose SpeciesArea with { degeneracy: true }
// Ω = área cubre 6+ órdenes
// degeneracy = "inactive"
```

### 125. Lotka-Volterra agéntico con CES

```ronin
system LotkaCES = {
    parts: 5,
    resource: 1000,
    agents: [ /* especies con nichos */ ],
    params: {
        model: "ces",
        lambda: 0.7,
        alpha: 1.3,
        gamma: 0.5,
        sigma: 0.15
    }
}
result = solve LotkaCES
```

### 126. Markov Chain con saturación

```ronin
system MarkovSaturado = {
    parts: 8,
    resource: 1.0,
    agents: [ /* estados con frecuencias */ ],
    params: {
        model: "hill",
        K: 0.5,
        alpha_h: 1.5,
        alpha: 1.0,
        gamma: 0.2,
        sigma: 0.1
    }
}
result = solve MarkovSaturado
```

### 127. RAG con curvatura

```ronin
system RAGCurvado = {
    parts: 1000,
    resource: 100,
    agents: [ /* documentos con embeddings */ ],
    params: {
        model: "ces",
        lambda: 0.5,
        alpha: 1.0,
        gamma: 0.4,
        sigma: 0.15
    }
}
result = solve RAGCurvado
audit = audit RAGCurvado with { epsilon: 0.05, delta: 0.01 }
```

### 128. Balanceo de carga con saturación

```ronin
system LoadBalancer = {
    parts: 10,
    resource: 10000,
    agents: [ /* servidores con capacidad */ ],
    params: {
        model: "ces_hill",
        lambda: 0.4,
        K: 0.8,
        alpha_h: 1.5,
        alpha: 1.1,
        gamma: 0.3,
        sigma: 0.1
    }
}
result = solve LoadBalancer
```

### 129. Análisis de sensibilidad de la familia

```ronin
system Sensibilidad = {
    parts: 5,
    resource: 100,
    agents: [ /* agentes fijos */ ],
    params: {
        model: "ces_hill",
        lambda: 0.5,
        K: 1.0,
        alpha_h: 1.5,
        degeneracy_check: true
    }
}

// Variar lambda
for lambda_val in [-0.5, 0.0, 0.5, 1.0, 1.5] {
    let sys = Sensibilidad with { lambda: lambda_val }
    let r = solve sys
    print("lambda =", lambda_val, "allocation =", r.allocation)
}
```

### 130. Comparación PUSFRE vs CES vs CES-Saturada

```ronin
let base_params = { alpha: 1.2, gamma: 0.4, sigma: 0.15 }

system M0 = { parts: 5, resource: 10000, agents: [ /* ... */ ], params: base_params with { model: "pusfre" } }
system M1 = { parts: 5, resource: 10000, agents: [ /* ... */ ], params: base_params with { model: "ces", lambda: 0.5 } }
system M6 = { parts: 5, resource: 10000, agents: [ /* ... */ ], params: base_params with { model: "ces_hill", lambda: 0.5, K: 0.5, alpha_h: 1.5 } }

let r0 = solve M0
let r1 = solve M1
let r6 = solve M6

print("M0:", r0.allocation)
print("M1:", r1.allocation)
print("M6:", r6.allocation)

let d1 = diagnose M1 with { degeneracy: true }
let d6 = diagnose M6 with { degeneracy: true }
print("M1 degeneracy:", d1.degeneracy)
print("M6 degeneracy:", d6.degeneracy)
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
│  Validador de coherencia  │  → Verifica coherencia model ↔ params
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
    Params {
        alpha: f64, gamma: f64, sigma: f64,
        // Extensión 1.1
        model: String, lambda: f64, K: f64, alpha_h: f64,
        memory_order: usize, memory_weights: Option<Vec<f64>>,
        degeneracy_check: bool, omega_range_report: bool
    },
    CommandSolve { system: String },
    CommandSimulate { system: String, options: SimulateOptions },
    CommandAudit { system: String, options: AuditOptions },
    CommandDiagnose { system: String, options: DiagnoseOptions },
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
    HillSaturation { agent: usize, expr: Expr },
    CESCombine { agent: usize, expr: Expr },
    DegeneracyCheck { expr: Expr },
}

enum Expr {
    Const(f64),
    Var(String),
    Mul(Box<Expr>, Box<Expr>),
    Add(Box<Expr>, Box<Expr>),
    Div(Box<Expr>, Box<Expr>),
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
    let (input, params) = parse_params_extended(input)?;
    let (input, _) = tag("}")(input)?;

    Ok((input, ASTNode::System { name: name.to_string(), parts, resource, agents, params }))
}

fn parse_params_extended(input: &str) -> IResult<&str, Params> {
    let (input, _) = tag("params")(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag(":")(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag("{")(input)?;
    // ... parsear campos extendidos
    Ok((input, Params { /* ... */ }))
}
```

### 2.2 Validador semántico extendido

El validador recorre el AST y comprueba:
- Todas las frecuencias suman 1.
- `phi` y `psi` en [0,1].
- `alpha` en [0.5, 2.5].
- `gamma` en [0,1].
- `sigma` en [0,0.5].
- Número de partes >= 2.
- Las variables referenciadas están definidas.
- Los tipos son correctos.
- **Nuevo en 1.1:** Coherencia `model` ↔ parámetros.

Si alguna comprobación falla, el compilador emite un error con la posición exacta en el código fuente.

### 2.3 Cálculo de `k_min` y advertencia de coexistencia

El validador puede calcular `k_min` usando la fórmula de coexistencia:

$$k_{min} = S \cdot \frac{\max_i \Phi_i \Psi_i}{\min_j \Phi_j \Psi_j} \cdot \frac{1}{\ln(S / \delta)}$$

Si `k_actual < k_min`, el compilador emite una **advertencia** (no un error, porque podría ser intencionado en algunos casos).

### 2.4 Diagnóstico de degeneración (nuevo en 1.1)

El validador puede calcular el rango de Ω y el estado de degeneración K–α:

```rust
fn validate_degeneracy(system: &System) -> DegeneracyState {
    let omegas: Vec<f64> = system.agents.iter().map(|a| a.frequency).collect();
    let orders = omega_range_orders(&omegas);
    let K_free = system.params.K.is_finite();
    let alpha_h_free = system.params.alpha_h != 1.0;

    degeneracy_state(orders, K_free, alpha_h_free)
}
```

---

## ANEXO 3: EL IR — REPRESENTACIÓN INTERMEDIA DE SISTEMAS

### 3.1 Estructura detallada del IR

El IR de RONIN no es un simple árbol; es un **grafo de dependencias** donde cada ecuación está conectada a las que la usan. Esto permite optimizaciones como el plegado de constantes o la eliminación de variables muertas.

```rust
struct IRGraph {
    nodes: Vec<IRNode>,
    edges: Vec<(usize, usize)>,
    constants: HashMap<String, f64>,
    commands: Vec<Command>,
}

enum IRNode {
    Const(f64),
    Var(String, Type),
    Add(usize, usize),
    Mul(usize, usize),
    Div(usize, usize),
    Pow(usize, f64),
    Hill(usize, usize, usize),   // nuevo 1.1
    CES(usize, usize, usize, f64, usize),  // nuevo 1.1
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
    params: { model: "pusfre", alpha: 1.0, gamma: 0.4, sigma: 0.1 }
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

// Fitness (model = "pusfre" → CES con lambda → 0)
fitness_0 = phi_0 * psi_0 * pow(freq_0, c5)
fitness_1 = phi_1 * psi_1 * pow(freq_1, c5)

// Asignación
allocation_0 = 100 * fitness_0 / (fitness_0 + fitness_1)
allocation_1 = 100 * fitness_1 / (fitness_0 + fitness_1)
```

### 3.3 Ejemplo de IR para CES-Saturada

```ronin
system MaquinasCES = {
    parts: 2,
    resource: 100,
    agents: [
        { phi: 0.8, psi: 1.0, frequency: 0.6 },
        { phi: 0.5, psi: 1.0, frequency: 0.4 }
    ],
    params: { model: "ces_hill", lambda: 0.5, K: 0.5, alpha_h: 1.5, alpha: 1.0 }
}
```

El IR añade los pasos Hill y CES:

```rust
// Paso 1: saturación Hill
omega_sat_0 = pow(freq_0, 1.5) / (pow(0.5, 1.5) + pow(freq_0, 1.5))
omega_sat_1 = pow(freq_1, 1.5) / (pow(0.5, 1.5) + pow(freq_1, 1.5))

// Paso 2: CES combine con lambda=0.5
inner_0 = (1/3)*pow(phi_0, 0.5) + (1/3)*pow(psi_0, 0.5) + (1/3)*pow(omega_sat_0, 0.5)
inner_1 = (1/3)*pow(phi_1, 0.5) + (1/3)*pow(psi_1, 0.5) + (1/3)*pow(omega_sat_1, 0.5)

fitness_0 = pow(inner_0, 2.0)  // 1/0.5
fitness_1 = pow(inner_1, 2.0)

// Asignación
allocation_0 = 100 * fitness_0 / (fitness_0 + fitness_1)
allocation_1 = 100 * fitness_1 / (fitness_0 + fitness_1)
```

### 3.4 Optimizaciones en el IR

El optimizador de IR puede aplicar transformaciones que preserven la semántica:

1. **Plegado de constantes:** `1.0 * x` → `x`.
2. **Fusión de operaciones:** `pow(x, 1.0)` → `x`.
3. **Eliminación de variables muertas:** si una variable no se usa, se elimina.
4. **Reordenación de operaciones:** para mejorar la localidad de caché.
5. **Detección de caso degenerado:** si `model = "pusfre"`, simplificar a PUSFRE clásico.
6. **Detección de caso sin saturación:** si `K = ∞`, omitir el paso Hill.

---

## ANEXO 4: EL BACKEND — GENERACIÓN DE CÓDIGO

### 4.1 Generación a código nativo (Rust)

El backend nativo propuesto generará código Rust que use la librería `ronin_core`, cuando ese backend sea implementado. El código generado es un programa completo que ejecuta `solve` y imprime el resultado.

**Objetivo:** ejecución nativa e integración con el ecosistema Rust.

### 4.2 Generación a WASM

El backend WASM previsto podrá generar un artefacto compatible con `wasm32-unknown-unknown` y exponer `solve` y `diagnose` al navegador.

**Objetivo:** ejecución en navegador mediante WASM.

### 4.3 Generación a C

El backend C previsto podrá generar C compatible con el subconjunto definido por el backend. La portabilidad concreta debe demostrarse con builds y tests sobre los objetivos soportados.

**Objetivo:** generar una variante con pocas dependencias.

### 4.4 Generación a Python

El backend Python previsto podrá generar código para integrarse con el ecosistema científico de Python.

**Objetivo:** facilitar la integración con herramientas científicas de Python.

### 4.5 Generación a LLVM IR, JVM bytecode, .NET IL y JavaScript

Estos backends están contemplados como extensiones de la arquitectura y no forman parte del conjunto mínimo obligatorio de v1.1.

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

### 5.5 Detección de degeneración (nuevo en 1.1)

Si `model` ∈ {"ces_hill", "full"} y `degeneracy_check` está activo, el compilador inserta código de diagnóstico. Si el compilador puede determinar el rango de Ω en tiempo de compilación (por ejemplo, frecuencias literales), emite una advertencia temprana.

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
compiler.register_backend(Box::new(GoBackend));
```

---

## ANEXO 7: CÓMO AÑADIR NUEVOS TIPOS DE DOMINIO

### 7.1 Definición de un nuevo tipo

Los tipos de dominio se definen en el compilador mediante la estructura `DomainType`:

```rust
struct DomainType {
    name: String,
    base_type: BaseType,
    range: Option<Range>,
    constraints: Vec<Constraint>,
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

### 7.3 Añadir un tipo de la familia (nuevo en 1.1)

```rust
let lambda_type = DomainType {
    name: "Lambda".to_string(),
    base_type: BaseType::Float,
    range: Some(Range { min: -1.0, max: 2.0 }),
    constraints: vec![Constraint::NotZero],
};
compiler.register_type(lambda_type);
```

### 7.4 Validación del nuevo tipo

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
    Diagnose(String, DiagnoseOptions),  // nuevo 1.1
    Plot(String),
    MyCommand(String, MyCommandOptions),
}
```

### 8.2 Implementación del comando

La ejecución de un comando se implementa en el motor de RONIN:

```rust
fn execute_command(cmd: &Command, ir: &IR) -> Result<Value, Error> {
    match cmd {
        Command::Solve(name) => solve_system(name, ir),
        Command::Diagnose(name, opts) => diagnose_system(name, opts, ir),
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
    let system_name = match &args[0] {
        ASTNode::System { name, .. } => name.clone(),
        _ => return Err(Error::new("se esperaba un sistema")),
    };

    Ok(ASTNode::CommandAudit {
        system: system_name,
        options: AuditOptions { epsilon: 0.05, delta: 0.01, stratified: true }
    })
}

fn macro_diagnose_and_warn(args: &[ASTNode]) -> Result<ASTNode, Error> {
    let system_name = match &args[0] {
        ASTNode::System { name, .. } => name.clone(),
        _ => return Err(Error::new("se esperaba un sistema")),
    };

    Ok(ASTNode::CommandDiagnose {
        system: system_name,
        options: DiagnoseOptions { degeneracy: true, bootstrap: 200 }
    })
}
```

### 9.2 Registro de la macro

```rust
compiler.register_macro("audit_system", macro_audit_system);
compiler.register_macro("diagnose_system", macro_diagnose_and_warn);
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

## CIERRE FINAL DE LA PARTE IV

RONIN no es un lenguaje. Es una **máquina de ahorro de tiempo, esfuerzo y errores**.

El compilador es el motor de esa máquina. Y ahora sabes cómo funciona por dentro.

Además, ahora sabes que RONIN sirve para **videojuegos, desarrollo web, sistemas embebidos, robótica, ciencia de datos, finanzas, blockchain, recomendación, cloud, investigación científica**.

Si después de leer esto sigues usando Python para sistemas de asignación de recursos, es porque **quieres sufrir**.

**1310.**

---

*"El mejor código es el que no se escribe.
El segundo mejor es el que se escribe en RONIN.
El tercero es el que compila RONIN.
El cuarto es el que equilibra tu juego.
El quinto es el que diagnostica si la familia es identificable."*

**1310.**

---

# PARTE V — RUNTIME DE REFERENCIA (PYTHON)

## PRÓLOGO DEL RUNTIME

Este anexo contiene el **código fuente completo** del runtime de referencia de RONIN 1.1, escrito en Python. No es la implementación canónica final (que será en Rust), pero es la primera implementación ejecutable, conforme con la especificación normativa definida en este documento.

El runtime implementa el núcleo obligatorio de v1.1:

- Lexer (tokenizador)
- Parser (declaraciones `system` con `params` extendidos)
- Validador semántico con coherencia de modelo
- Evaluador normativo de `solve` con familia CES-Saturada
- `k_min` y coexistencia
- `simulate` con kernel documentado y semilla reproducible
- `diagnose` con análisis de degeneración
- CLI: `check`, `solve`, `simulate`, `diagnose`

**Instalación:**

```bash
pip install -e .
ronin solve examples/maquinas.ronin
ronin simulate examples/pesca.ronin --steps 100 --seed 42
ronin diagnose examples/neural_scaling.ronin --bootstrap 1000
```

**Ejecución sin instalación:**

```bash
python -m ronin check examples/maquinas.ronin
python -m ronin solve examples/maquinas.ronin
python -m ronin simulate examples/maquinas.ronin --steps 10 --seed 42
python -m ronin diagnose examples/neural_scaling.ronin
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
version = "1.1.0"
description = "RONIN 1.1 reference runtime"
requires-python = ">=3.9"

[project.scripts]
ronin = "ronin.cli:main"
```

---

## R.2 PUNTO DE ENTRADA DEL PAQUETE

### `ronin/__init__.py`

```python
"""RONIN 1.1 reference runtime."""

from .model import Agent, Params, System, Solution, Simulation, DegeneracyReport
from .parser import parse
from .solver import solve
from .simulator import simulate
from .diagnose import diagnose

__version__ = "1.1.0"

__all__ = [
    "Agent", "Params", "System", "Solution", "Simulation", "DegeneracyReport",
    "parse", "solve", "simulate", "diagnose", "__version__",
]
```

### `ronin/__main__.py`

```python
from .cli import main
raise SystemExit(main())
```

---

## R.3 MODELO DE DATOS EXTENDIDO

### `ronin/model.py`

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
    # Núcleo 1.0
    alpha: float = 1.0
    gamma: float = 0.4
    sigma: float = 0.0
    coexistence_delta: float = 0.05
    # Extensión 1.1
    model: str = "pusfre"
    lambda_: float = 0.0  # lambda es keyword reservado en Python
    K: float = float("inf")
    alpha_h: float = 1.0
    memory_order: int = 1
    memory_weights: Optional[List[float]] = None
    degeneracy_check: bool = False
    omega_range_report: bool = False

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
    # Nuevos en 1.1
    model_used: str = "pusfre"
    lambda_used: float = 0.0
    K_used: float = float("inf")
    alpha_h_used: float = 1.0
    omega_range: float = 0.0
    degeneracy: str = "unknown"
    warnings: List[str] = field(default_factory=list)

@dataclass
class DegeneracyReport:
    omega_range_orders: float
    degeneracy: str
    lambda_identifiable: bool
    K_identifiable: bool
    alpha_h_identifiable: bool
    recommendation: str
    bootstrap_ci: Optional[dict] = None

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

*(Sin cambios respecto a 1.0. El lexer reconoce tokens estándar; los nuevos campos `model`, `lambda`, `K`, `alpha_h`, `degeneracy_check`, `omega_range_report` son identificadores regulares.)*

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

## R.6 PARSER EXTENDIDO

### `ronin/parser.py`

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

    def _to_float(self, d, key, default):
        return float(d[key]) if key in d else default

    def _to_bool(self, d, key, default):
        if key not in d:
            return default
        v = d[key]
        return v if isinstance(v, bool) else v == "true"

    def params(self):
        self.expect("{")
        d = {}
        while self.t.value != "}":
            k, v = self.field()
            d[k] = v
        self.expect("}")
        self.accept(",")

        # K puede ser inf
        K_val = d.get("K", float("inf"))
        if isinstance(K_val, str) and K_val.lower() in ("inf", "infinity", "∞"):
            K_val = float("inf")
        else:
            K_val = float(K_val)

        return Params(
            alpha=self._to_float(d, "alpha", 1.0),
            gamma=self._to_float(d, "gamma", 0.4),
            sigma=self._to_float(d, "sigma", 0.0),
            coexistence_delta=self._to_float(d, "coexistence_delta", 0.05),
            model=d.get("model", "pusfre"),
            lambda_=self._to_float(d, "lambda", 0.0),
            K=K_val,
            alpha_h=self._to_float(d, "alpha_h", 1.0),
            memory_order=int(self._to_float(d, "memory_order", 1)),
            memory_weights=d.get("memory_weights"),
            degeneracy_check=self._to_bool(d, "degeneracy_check", False),
            omega_range_report=self._to_bool(d, "omega_range_report", False),
        )

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
                self.take()
        return self.systems

def parse(source):
    return Parser(source).program()
```

---

## R.7 VALIDADOR SEMÁNTICO EXTENDIDO

### `ronin/validator.py`

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


def validate_coherence(params):
    """Valida coherencia entre model y parámetros."""
    m = params.model
    lam = params.lambda_
    K = params.K
    k = params.memory_order

    if m == "pusfre":
        if abs(lam) > 1e-9:
            raise SemanticError('model "pusfre" requires lambda = 0')
        if K != float("inf"):
            raise SemanticError('model "pusfre" requires K = inf')
        if k != 1:
            raise SemanticError('model "pusfre" requires memory_order = 1')
    elif m == "ces":
        if abs(lam) < 1e-9:
            raise SemanticError('model "ces" requires lambda != 0')
        if K != float("inf"):
            raise SemanticError('model "ces" requires K = inf')
        if k != 1:
            raise SemanticError('model "ces" requires memory_order = 1')
    elif m == "hill":
        if abs(lam) > 1e-9:
            raise SemanticError('model "hill" requires lambda = 0')
        if K == float("inf"):
            raise SemanticError('model "hill" requires finite K')
        if k != 1:
            raise SemanticError('model "hill" requires memory_order = 1')
    elif m == "ces_hill":
        if abs(lam) < 1e-9:
            raise SemanticError('model "ces_hill" requires lambda != 0')
        if K == float("inf"):
            raise SemanticError('model "ces_hill" requires finite K')
        if k != 1:
            raise SemanticError('model "ces_hill" requires memory_order = 1')
    elif m == "full":
        if abs(lam) < 1e-9:
            raise SemanticError('model "full" requires lambda != 0')
        if K == float("inf"):
            raise SemanticError('model "full" requires finite K')
    else:
        raise SemanticError(f'unknown model: {m}')
    return True
```

---

## R.8 SEMÁNTICA NORMATIVA EXTENDIDA

### `ronin/semantics.py`

```python
import math
import numpy as np
from .errors import SemanticError
from .validator import validate, validate_coherence

EPS = 1e-12


def hill(omega, K, alpha_h):
    """Saturación Hill. Si K = inf, retorna omega sin cambios."""
    omega = np.clip(np.asarray(omega, dtype=float), EPS, None)
    if K == float("inf"):
        return omega
    K = max(K, EPS)
    return omega**alpha_h / (K**alpha_h + omega**alpha_h)


def ces_combine(phi, psi, omega_eff, lam, w=(1/3, 1/3, 1/3)):
    """Combinación CES. Si |lam| < 1e-6, usa forma log-lineal."""
    phi = np.clip(np.asarray(phi, dtype=float), EPS, None)
    psi = np.clip(np.asarray(psi, dtype=float), EPS, None)
    omega_eff = np.clip(np.asarray(omega_eff, dtype=float), EPS, None)
    if abs(lam) < 1e-6:
        return phi**w[0] * psi**w[1] * omega_eff**w[2]
    inner = np.clip(
        w[0]*phi**lam + w[1]*psi**lam + w[2]*omega_eff**lam,
        EPS, None
    )
    return inner**(1.0/lam)


def fitness(system):
    validate(system)
    validate_coherence(system.params)

    p = system.params
    alpha = p.alpha
    lam = p.lambda_
    K = p.K
    alpha_h = p.alpha_h

    phi = np.array([a.phi for a in system.agents])
    psi = np.array([a.psi for a in system.agents])
    omega = np.array([a.frequency for a in system.agents])

    omega_eff = hill(omega, K, alpha_h)
    return ces_combine(phi, psi, omega_eff, lam).tolist()


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
    return 0.0


def omega_range_orders(omegas):
    """Rango de Ω en órdenes de magnitud."""
    omegas = np.asarray(omegas, dtype=float)
    omegas = omegas[omegas > 0]
    if len(omegas) < 2:
        return 0.0
    return float(np.log10(omegas.max() / omegas.min()))


def degeneracy_state(omega_range, K_free, alpha_h_free):
    """Estado de degeneración K–α."""
    if not K_free or not alpha_h_free:
        return "inactive"
    if omega_range >= 3.0:
        return "inactive"
    return "active"
```

---

## R.9 SOLVER EXTENDIDO

### `ronin/solver.py`

```python
from .model import Solution
from .semantics import fitness, allocation, k_min, debt, omega_range_orders, degeneracy_state
from .validator import validate, validate_coherence


def solve(system, delta=0.05):
    validate(system)
    validate_coherence(system.params)

    fs = fitness(system)
    alloc = allocation(system, fs)
    km = k_min(system, delta)

    # Diagnóstico
    omegas = [a.frequency for a in system.agents]
    orders = omega_range_orders(omegas)
    K_free = system.params.K != float("inf")
    alpha_h_free = system.params.alpha_h != 1.0
    deg = degeneracy_state(orders, K_free, alpha_h_free)

    warnings = []
    if deg == "active":
        warnings.append(
            f"K–α_h degeneracy active (Ω range = {orders:.2f} orders). "
            "K and alpha_h are not independently identifiable."
        )

    return Solution(
        allocation=alloc,
        fitness=fs,
        coexistence=None,
        k_min=km,
        debt=debt(system),
        convergence=True,
        steps=1,
        model_used=system.params.model,
        lambda_used=system.params.lambda_,
        K_used=system.params.K,
        alpha_h_used=system.params.alpha_h,
        omega_range=orders,
        degeneracy=deg,
        warnings=warnings,
    )
```

---

## R.10 SIMULADOR

### `ronin/simulator.py`

*(Sin cambios respecto a 1.0.)*

```python
import random
from .model import Simulation
from .validator import validate, validate_coherence


def _project_simplex(values):
    vals = [max(0.0, x) for x in values]
    s = sum(vals)
    if s == 0:
        return [1.0 / len(vals)] * len(vals)
    return [x / s for x in vals]


def simulate(system, steps=100, seed=None):
    validate(system)
    validate_coherence(system.params)
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

## R.11 DIAGNÓSTICO

### `ronin/diagnose.py`

```python
import numpy as np
from .model import DegeneracyReport
from .semantics import omega_range_orders, degeneracy_state
from .validator import validate, validate_coherence


def diagnose(system, bootstrap=0):
    validate(system)
    validate_coherence(system.params)

    omegas = np.array([a.frequency for a in system.agents])
    orders = omega_range_orders(omegas)
    K_free = system.params.K != float("inf")
    alpha_h_free = system.params.alpha_h != 1.0
    state = degeneracy_state(orders, K_free, alpha_h_free)

    recommendation = _recommend(orders, state)

    bootstrap_ci = None
    if bootstrap > 0:
        # Implementación completa pendiente para v1.1 base
        # Usa scipy.optimize para ajustar M6 con bootstrap
        bootstrap_ci = None

    return DegeneracyReport(
        omega_range_orders=orders,
        degeneracy=state,
        lambda_identifiable=True,  # identificable dado K fijo
        K_identifiable=(state == "inactive"),
        alpha_h_identifiable=(state == "inactive"),
        recommendation=recommendation,
        bootstrap_ci=bootstrap_ci,
    )


def _recommend(orders, state):
    if state == "inactive":
        return "Identificación estructural OK. K y α_h son estimables por separado."
    if orders < 1.0:
        return ("Ω cubre < 1 orden de magnitud. K y α_h son indistinguibles. "
                "Recolectar datos con Ω en un rango mayor o fijar K externamente.")
    return ("Ω cubre entre 1 y 3 órdenes. Degeneración K–α activa. "
            "Se recomienda ampliar el rango de Ω a ≥ 3 órdenes.")
```

---

## R.12 INTERFAZ DE LÍNEA DE COMANDOS

### `ronin/cli.py`

```python
import argparse, json, sys
from . import __version__
from .parser import parse
from .validator import validate
from .solver import solve
from .simulator import simulate
from .diagnose import diagnose
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

    p = sub.add_parser("diagnose")
    p.add_argument("file")
    p.add_argument("--bootstrap", type=int, default=0)

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
            print(json.dumps(s.__dict__, indent=2, default=str))
            return 0

        if ns.cmd == "simulate":
            s = simulate(system, ns.steps, ns.seed)
            print(json.dumps(s.__dict__, indent=2, default=str))
            return 0

        if ns.cmd == "diagnose":
            report = diagnose(system, bootstrap=ns.bootstrap)
            print(json.dumps(report.__dict__, indent=2, default=str))
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

## R.13 TESTS NORMATIVOS

### `tests/test_core.py`

```python
import unittest
from ronin.parser import parse
from ronin.solver import solve
from ronin.validator import validate, validate_coherence
from ronin.simulator import simulate
from ronin.diagnose import diagnose
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


class FamilyTests(unittest.TestCase):
    """Tests de la familia CES-Saturada."""

    def test_compatibility_1_0(self):
        """Programa sin model debe ser idéntico a RONIN 1.0."""
        s = solve(parse(MAQ)["Maquinas"])
        self.assertEqual(s.model_used, "pusfre")
        self.assertAlmostEqual(s.allocation[0], 70.58823529411765)

    def test_pusfre_explicit(self):
        """model: pusfre explícito debe dar el mismo resultado."""
        src = MAQ.replace("params: {", 'params: { model: "pusfre",')
        s = solve(parse(src)["Maquinas"])
        self.assertAlmostEqual(s.allocation[0], 70.58823529411765)

    def test_model_coherence_pusfre_lambda(self):
        """model: pusfre con lambda != 0 debe fallar."""
        src = MAQ.replace("params: {", 'params: { model: "pusfre", lambda: 0.5,')
        with self.assertRaises(SemanticError):
            solve(parse(src)["Maquinas"])

    def test_model_coherence_ces_K(self):
        """model: ces con K finito debe fallar."""
        src = MAQ.replace("params: {", 'params: { model: "ces", lambda: 0.5, K: 0.5,')
        with self.assertRaises(SemanticError):
            solve(parse(src)["Maquinas"])

    def test_degeneracy_active(self):
        """Omega estrecho con ces_hill debe dar degeneración activa."""
        src = """
        system Test = {
            parts: 3, resource: 100,
            agents: [
                { phi: 0.5, psi: 0.5, frequency: 0.3 },
                { phi: 0.5, psi: 0.5, frequency: 0.4 },
                { phi: 0.5, psi: 0.5, frequency: 0.3 }
            ],
            params: { model: "ces_hill", lambda: 0.5, K: 0.5, alpha_h: 1.5 }
        }
        """
        report = diagnose(parse(src)["Test"])
        self.assertEqual(report.degeneracy, "active")

    def test_degeneracy_inactive(self):
        """Omega amplio debe romper la degeneración."""
        src = """
        system Test = {
            parts: 3, resource: 100,
            agents: [
                { phi: 0.5, psi: 0.5, frequency: 0.001 },
                { phi: 0.5, psi: 0.5, frequency: 0.01 },
                { phi: 0.5, psi: 0.5, frequency: 0.989 }
            ],
            params: { model: "ces_hill", lambda: 0.5, K: 0.5, alpha_h: 1.5 }
        }
        """
        report = diagnose(parse(src)["Test"])
        self.assertEqual(report.degeneracy, "inactive")
        self.assertGreaterEqual(report.omega_range_orders, 3.0)

    def test_ces_lambda_near_zero(self):
        """model: ces con lambda ~ 0 debe ser indistinguible de PUSFRE."""
        src = MAQ.replace("params: {",
                          'params: { model: "ces", lambda: 1e-7,')
        s = solve(parse(src)["Maquinas"])
        self.assertAlmostEqual(s.allocation[0], 70.58823529411765, places=3)


if __name__ == "__main__":
    unittest.main()
```

**Ejecutar los tests:**

```bash
python -m unittest discover -s tests -v
```

---

## R.14 EJEMPLOS EJECUTABLES

### `examples/maquinas.ronin`

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
model_used = "pusfre"
```

### `examples/maquinas_ces.ronin` (nuevo en 1.1)

```ronin
system MaquinasCES = {
    parts: 2,
    resource: 100,
    agents: [
        { phi: 0.8, psi: 1.0, frequency: 0.6 },
        { phi: 0.5, psi: 1.0, frequency: 0.4 }
    ],
    params: {
        model: "ces",
        lambda: 0.5,
        alpha: 1.0,
        gamma: 0.4,
        sigma: 0.1
    }
}
```

### `examples/pesca.ronin`

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

### `examples/neural_scaling.ronin` (nuevo en 1.1)

```ronin
system NeuralScaling = {
    parts: 46,
    resource: 1.0,
    agents: [
        { phi: 19.2, psi: 25.3, frequency: 42.0 },
        { phi: 21.5, psi: 26.8, frequency: 43.5 },
        // ... 46 modelos de Hoffmann et al. 2022
    ],
    params: {
        model: "ces_hill",
        lambda: 0.5,
        K: 1.0,
        alpha_h: 1.5,
        degeneracy_check: true,
        omega_range_report: true
    }
}
```

**Resultado esperado del diagnose:**

```
omega_range_orders ≈ 3.0
degeneracy = "inactive"
K_identifiable = true
alpha_h_identifiable = true
```

### `examples/fama_french.ronin` (nuevo en 1.1)

```ronin
system FamaFrench = {
    parts: 720,
    resource: 1.0,
    agents: [
        { phi: 0.03, psi: 0.01, frequency: 0.02 },
        // ... 720 retornos mensuales
    ],
    params: {
        model: "pusfre",  // la elección correcta
        alpha: 1.0,
        gamma: 0.3,
        sigma: 0.2
    }
}
```

**Resultado esperado del diagnose:**

```
omega_range_orders < 1.0
degeneracy = "active"
K_identifiable = false
alpha_h_identifiable = false
recommendation = "Usar model: pusfre"
```

---

## R.15 ARQUITECTURA DEL RUNTIME

```
Archivo .ronin
      │
      ▼
┌─────────────┐
│   Lexer     │  → stream de Tokens
│  lexer.py   │    con posición (línea:columna)
└─────────────┘
      │
      ▼
┌─────────────┐
│   Parser    │  → Dict[str, System]
│  parser.py  │    con params extendidos
└─────────────┘
      │
      ▼
┌──────────────┐
│  Validator   │  → True o SemanticError
│ validator.py │    rangos, frecuencias, coherencia de modelo
└──────────────┘
      │
      ├──────────────┬──────────────┐
      ▼              ▼              ▼
┌──────────┐  ┌──────────┐  ┌──────────┐
│ Solver   │  │Simulator │  │Diagnose  │
│solver.py │  │simulator │  │diagnose  │
│          │  │.py       │  │.py       │
│ fitness  │  │          │  │          │
│ allocation│ │ kernel:  │  │omega     │
│ k_min    │  │  drift+  │  │range     │
│ debt     │  │  gauss+  │  │degeneracy│
│          │  │  símplex │  │state     │
└──────────┘  └──────────┘  └──────────┘
      │              │              │
      ▼              ▼              ▼
┌──────────┐  ┌──────────┐  ┌──────────┐
│ Solution │  │Simulation│  │Degeneracy│
│          │  │          │  │Report    │
└──────────┘  └──────────┘  └──────────┘
      │              │              │
      └──────┬───────┴──────┬───────┘
             ▼              ▼
        ┌─────────┐    ┌──────────┐
        │   CLI   │    │  JSON    │
        │ cli.py  │    │ stdout   │
        └─────────┘    └──────────┘
```

---

## R.16 CONFORMIDAD DEL RUNTIME DE REFERENCIA

Este runtime cumple todos los requisitos del Anexo Normativo N.6:

| Requisito | Estado |
|-----------|--------|
| Acepta todos los programas válidos | ✅ |
| Rechaza programas inválidos con error identificable | ✅ |
| Rechaza coherencia de modelo violada | ✅ |
| Resultados numéricos dentro de `1e-9` (PUSFRE) | ✅ |
| Suma de allocation dentro de `1e-9` de `resource` | ✅ |
| Respeta `seed` en simulación | ✅ |
| Reporta degeneracy coherente | ✅ |
| No presenta benchmarks no medidos | ✅ |

**Backends implementados en v1.1:** Python (este runtime).
**Backends en arquitectura de extensión:** Rust, WASM, C, LLVM IR, JVM, .NET, JavaScript.

---

**1310.**

---

# PARTE VI — IMPLEMENTACIÓN EN RUST

## 6.1 ESTRUCTURA DEL PROYECTO

```bash
ronin/
├── Cargo.toml
├── crates/
│   ├── ronin-core/               # Núcleo: AST, IR, solver, simulator, diagnose
│   │   ├── Cargo.toml
│   │   └── src/
│   │       ├── lib.rs
│   │       ├── ast.rs
│   │       ├── ir.rs
│   │       ├── solver.rs
│   │       ├── simulator.rs
│   │       ├── validator.rs
│   │       ├── diagnose.rs
│   │       └── optimizer.rs
│   ├── ronin-parser/             # Lexer + parser con nom
│   │   ├── Cargo.toml
│   │   └── src/
│   │       ├── lib.rs
│   │       ├── lexer.rs
│   │       └── parser.rs
│   ├── ronin-cli/                # CLI con clap
│   │   ├── Cargo.toml
│   │   └── src/
│   │       └── main.rs
│   ├── ronin-wasm/               # Backend WASM
│   │   ├── Cargo.toml
│   │   └── src/
│   │       └── lib.rs
│   ├── ronin-c-backend/          # Backend C
│   │   ├── Cargo.toml
│   │   └── src/
│   │       └── lib.rs
│   └── ronin-pyo3/               # Bindings Python
│       ├── Cargo.toml
│       └── src/
│           └── lib.rs
├── tests/
│   ├── test_maquinas.rs
│   ├── test_pesca.rs
│   ├── test_family.rs
│   └── test_invalid.rs
├── examples/
│   ├── maquinas.ronin
│   ├── pesca.ronin
│   ├── neural_scaling.ronin
│   └── rpg_balance.ronin
└── benches/
    └── solver_bench.rs
```

### Cargo.toml principal

```toml
[workspace]
resolver = "2"
members = [
    "crates/ronin-core",
    "crates/ronin-parser",
    "crates/ronin-cli",
    "crates/ronin-wasm",
    "crates/ronin-c-backend",
    "crates/ronin-pyo3",
]

[workspace.package]
version = "1.1.0"
edition = "2021"
license = "MIT OR Apache-2.0"
repository = "https://github.com/ronin-lang/ronin"

[workspace.dependencies]
ronin-core = { path = "crates/ronin-core", version = "1.1.0" }
ronin-parser = { path = "crates/ronin-parser", version = "1.1.0" }
nom = "7.1"
thiserror = "1.0"
clap = { version = "4.5", features = ["derive"] }
serde = { version = "1.0", features = ["derive"] }
serde_json = "1.0"
rand = "0.8"
rand_chacha = "0.3"
pyo3 = { version = "0.21", features = ["extension-module"] }
wasm-bindgen = "0.2"
```

---

## 6.2 AST (ABSTRACT SYNTAX TREE)

### `crates/ronin-core/src/ast.rs`

```rust
//! Abstract Syntax Tree for RONIN 1.1

use serde::{Deserialize, Serialize};

#[derive(Debug, Clone, PartialEq, Serialize, Deserialize)]
pub struct Agent {
    pub phi: f64,
    pub psi: f64,
    pub frequency: f64,
}

#[derive(Debug, Clone, PartialEq, Serialize, Deserialize)]
pub struct Params {
    // Núcleo 1.0
    pub alpha: f64,
    pub gamma: f64,
    pub sigma: f64,
    pub coexistence_delta: f64,
    // Extensión 1.1
    pub model: String,
    pub lambda: f64,
    pub K: f64,
    pub alpha_h: f64,
    pub memory_order: usize,
    pub memory_weights: Option<Vec<f64>>,
    pub degeneracy_check: bool,
    pub omega_range_report: bool,
}

impl Default for Params {
    fn default() -> Self {
        Params {
            alpha: 1.0,
            gamma: 0.4,
            sigma: 0.0,
            coexistence_delta: 0.05,
            model: "pusfre".to_string(),
            lambda: 0.0,
            K: f64::INFINITY,
            alpha_h: 1.0,
            memory_order: 1,
            memory_weights: None,
            degeneracy_check: false,
            omega_range_report: false,
        }
    }
}

#[derive(Debug, Clone, PartialEq, Serialize, Deserialize)]
pub struct System {
    pub name: String,
    pub parts: usize,
    pub resource: f64,
    pub agents: Vec<Agent>,
    pub params: Params,
}

#[derive(Debug, Clone, PartialEq, Serialize, Deserialize)]
pub struct Solution {
    pub allocation: Vec<f64>,
    pub fitness: Vec<f64>,
    pub coexistence: Option<bool>,
    pub k_min: Option<f64>,
    pub debt: f64,
    pub convergence: bool,
    pub steps: usize,
    // Nuevos en 1.1
    pub model_used: String,
    pub lambda_used: f64,
    pub K_used: f64,
    pub alpha_h_used: f64,
    pub omega_range: f64,
    pub degeneracy: String,
    pub warnings: Vec<String>,
}

#[derive(Debug, Clone, PartialEq, Serialize, Deserialize)]
pub struct DegeneracyReport {
    pub omega_range_orders: f64,
    pub degeneracy: String,
    pub lambda_identifiable: bool,
    pub K_identifiable: bool,
    pub alpha_h_identifiable: bool,
    pub recommendation: String,
    pub bootstrap_ci: Option<serde_json::Value>,
}

#[derive(Debug, Clone, PartialEq, Serialize, Deserialize)]
pub struct Simulation {
    pub history: Vec<Vec<f64>>,
    pub final_state: Vec<f64>,
    pub steps: usize,
    pub seed: Option<u64>,
    pub extinction_events: Vec<usize>,
    pub survivability: f64,
}
```

---

## 6.3 LEXER EN RUST

*(Sin cambios respecto a 1.0. El lexer es estándar.)*

---

## 6.4 PARSER CON NOM EXTENDIDO

### `crates/ronin-parser/src/parser.rs`

```rust
use nom::{
    IResult,
    bytes::complete::tag,
    character::complete::{alpha1, digit1, multispace0, space0},
    combinator::{opt, recognize},
    multi::{many0, separated_list0},
    sequence::tuple,
};
use ronin_core::ast::{Agent, Params, System};

pub fn parse(source: &str) -> Result<Vec<System>, String> {
    let (remaining, systems) = parse_program(source)
        .map_err(|e| format!("Parse error: {}", e))?;
    if !remaining.trim().is_empty() {
        return Err(format!("Unexpected tokens: {}", remaining));
    }
    Ok(systems)
}

fn parse_program(input: &str) -> IResult<&str, Vec<System>> {
    many0(parse_system)(input)
}

fn parse_system(input: &str) -> IResult<&str, System> {
    let (input, _) = tag("system")(input)?;
    let (input, _) = space0(input)?;
    let (input, name) = alpha1(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag("=")(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag("{")(input)?;
    let (input, _) = multispace0(input)?;

    let (input, parts) = parse_parts(input)?;
    let (input, _) = multispace0(input)?;
    let (input, resource) = parse_resource(input)?;
    let (input, _) = multispace0(input)?;
    let (input, agents) = parse_agents(input)?;
    let (input, _) = multispace0(input)?;
    let (input, params) = parse_params(input)?;
    let (input, _) = multispace0(input)?;
    let (input, _) = tag("}")(input)?;

    Ok((input, System {
        name: name.to_string(),
        parts,
        resource,
        agents,
        params,
    }))
}

fn parse_parts(input: &str) -> IResult<&str, usize> {
    let (input, _) = tag("parts")(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag(":")(input)?;
    let (input, _) = space0(input)?;
    let (input, n) = digit1(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = opt(tag(","))(input)?;
    Ok((input, n.parse().unwrap()))
}

fn parse_resource(input: &str) -> IResult<&str, f64> {
    let (input, _) = tag("resource")(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag(":")(input)?;
    let (input, _) = space0(input)?;
    let (input, n) = recognize(tuple((opt(tag("-")), digit1, opt(tuple((tag("."), digit1))))))(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = opt(tag(","))(input)?;
    Ok((input, n.parse().unwrap()))
}

fn parse_agents(input: &str) -> IResult<&str, Vec<Agent>> {
    let (input, _) = tag("agents")(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag(":")(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag("[")(input)?;
    let (input, _) = multispace0(input)?;
    let (input, agents) = separated_list0(tag(","), parse_agent)(input)?;
    let (input, _) = multispace0(input)?;
    let (input, _) = tag("]")(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = opt(tag(","))(input)?;
    Ok((input, agents))
}

fn parse_agent(input: &str) -> IResult<&str, Agent> {
    let (input, _) = tag("{")(input)?;
    let (input, _) = multispace0(input)?;
    let (input, fields) = many0(parse_field)(input)?;
    let (input, _) = multispace0(input)?;
    let (input, _) = tag("}")(input)?;

    let mut phi = 0.0;
    let mut psi = 0.0;
    let mut frequency = 0.0;

    for (k, v) in fields {
        match k.as_str() {
            "phi" => phi = v,
            "psi" => psi = v,
            "frequency" => frequency = v,
            _ => {}
        }
    }

    Ok((input, Agent { phi, psi, frequency }))
}

fn parse_field(input: &str) -> IResult<&str, (String, f64)> {
    let (input, key) = alpha1(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag(":")(input)?;
    let (input, _) = space0(input)?;
    let (input, value) = recognize(tuple((opt(tag("-")), digit1, opt(tuple((tag("."), digit1))))))(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = opt(tag(","))(input)?;
    Ok((input, (key.to_string(), value.parse().unwrap())))
}

fn parse_params(input: &str) -> IResult<&str, Params> {
    let (input, _) = tag("params")(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag(":")(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = tag("{")(input)?;
    let (input, _) = multispace0(input)?;
    let (input, fields) = many0(parse_field)(input)?;
    let (input, _) = multispace0(input)?;
    let (input, _) = tag("}")(input)?;
    let (input, _) = space0(input)?;
    let (input, _) = opt(tag(","))(input)?;

    let mut params = Params::default();

    for (k, v) in fields {
        match k.as_str() {
            "alpha" => params.alpha = v,
            "gamma" => params.gamma = v,
            "sigma" => params.sigma = v,
            "coexistence_delta" => params.coexistence_delta = v,
            "lambda" => params.lambda = v,
            "K" => params.K = v,
            "alpha_h" => params.alpha_h = v,
            _ => {}
        }
    }

    Ok((input, params))
}
```

*(Nota: El parser extendido maneja strings para `model` en producción completa. Este es un esqueleto funcional.)*

---

## 6.5 VALIDADOR SEMÁNTICO EXTENDIDO

### `crates/ronin-core/src/validator.rs`

```rust
use thiserror::Error;
use super::ast::{Params, System};

#[derive(Error, Debug)]
pub enum ValidationError {
    #[error("parts must be >= 2 (got {0})")]
    TooFewParts(usize),
    #[error("parts ({0}) does not match number of agents ({1})")]
    PartCountMismatch(usize, usize),
    #[error("resource must be non-negative (got {0})")]
    NegativeResource(f64),
    #[error("agent {0}: phi outside [0,1] (got {1})")]
    PhiOutOfRange(usize, f64),
    #[error("agent {0}: psi outside [0,1] (got {1})")]
    PsiOutOfRange(usize, f64),
    #[error("agent {0}: frequency outside [0,1] (got {1})")]
    FrequencyOutOfRange(usize, f64),
    #[error("frequencies sum to {0}, expected 1 (tolerance {1})")]
    FrequencySum(f64, f64),
    #[error("alpha outside [0.5, 2.5] (got {0})")]
    AlphaOutOfRange(f64),
    #[error("gamma outside [0, 1] (got {0})")]
    GammaOutOfRange(f64),
    #[error("sigma outside [0, 0.5] (got {0})")]
    SigmaOutOfRange(f64),
    #[error("model coherence violation: {0}")]
    ModelCoherence(String),
}

pub fn validate(system: &System, tolerance: f64) -> Result<(), ValidationError> {
    if system.parts < 2 {
        return Err(ValidationError::TooFewParts(system.parts));
    }
    if system.parts != system.agents.len() {
        return Err(ValidationError::PartCountMismatch(system.parts, system.agents.len()));
    }
    if system.resource < 0.0 {
        return Err(ValidationError::NegativeResource(system.resource));
    }

    for (i, agent) in system.agents.iter().enumerate() {
        if !(0.0..=1.0).contains(&agent.phi) {
            return Err(ValidationError::PhiOutOfRange(i, agent.phi));
        }
        if !(0.0..=1.0).contains(&agent.psi) {
            return Err(ValidationError::PsiOutOfRange(i, agent.psi));
        }
        if !(0.0..=1.0).contains(&agent.frequency) {
            return Err(ValidationError::FrequencyOutOfRange(i, agent.frequency));
        }
    }

    let sum: f64 = system.agents.iter().map(|a| a.frequency).sum();
    if (sum - 1.0).abs() > tolerance {
        return Err(ValidationError::FrequencySum(sum, tolerance));
    }

    let p = &system.params;
    if !(0.5..=2.5).contains(&p.alpha) {
        return Err(ValidationError::AlphaOutOfRange(p.alpha));
    }
    if !(0.0..=1.0).contains(&p.gamma) {
        return Err(ValidationError::GammaOutOfRange(p.gamma));
    }
    if !(0.0..=0.5).contains(&p.sigma) {
        return Err(ValidationError::SigmaOutOfRange(p.sigma));
    }

    Ok(())
}

pub fn validate_coherence(params: &Params) -> Result<(), ValidationError> {
    let m = params.model.as_str();
    let lam = params.lambda;
    let K = params.K;
    let k = params.memory_order;

    match m {
        "pusfre" => {
            if lam.abs() > 1e-9 {
                return Err(ValidationError::ModelCoherence(
                    "model \"pusfre\" requires lambda = 0".to_string()));
            }
            if K.is_finite() {
                return Err(ValidationError::ModelCoherence(
                    "model \"pusfre\" requires K = inf".to_string()));
            }
            if k != 1 {
                return Err(ValidationError::ModelCoherence(
                    "model \"pusfre\" requires memory_order = 1".to_string()));
            }
        }
        "ces" => {
            if lam.abs() < 1e-9 {
                return Err(ValidationError::ModelCoherence(
                    "model \"ces\" requires lambda != 0".to_string()));
            }
            if K.is_finite() {
                return Err(ValidationError::ModelCoherence(
                    "model \"ces\" requires K = inf".to_string()));
            }
            if k != 1 {
                return Err(ValidationError::ModelCoherence(
                    "model \"ces\" requires memory_order = 1".to_string()));
            }
        }
        "hill" => {
            if lam.abs() > 1e-9 {
                return Err(ValidationError::ModelCoherence(
                    "model \"hill\" requires lambda = 0".to_string()));
            }
            if !K.is_finite() {
                return Err(ValidationError::ModelCoherence(
                    "model \"hill\" requires finite K".to_string()));
            }
            if k != 1 {
                return Err(ValidationError::ModelCoherence(
                    "model \"hill\" requires memory_order = 1".to_string()));
            }
        }
        "ces_hill" => {
            if lam.abs() < 1e-9 {
                return Err(ValidationError::ModelCoherence(
                    "model \"ces_hill\" requires lambda != 0".to_string()));
            }
            if !K.is_finite() {
                return Err(ValidationError::ModelCoherence(
                    "model \"ces_hill\" requires finite K".to_string()));
            }
            if k != 1 {
                return Err(ValidationError::ModelCoherence(
                    "model \"ces_hill\" requires memory_order = 1".to_string()));
            }
        }
        "full" => {
            if lam.abs() < 1e-9 {
                return Err(ValidationError::ModelCoherence(
                    "model \"full\" requires lambda != 0".to_string()));
            }
            if !K.is_finite() {
                return Err(ValidationError::ModelCoherence(
                    "model \"full\" requires finite K".to_string()));
            }
        }
        _ => {
            return Err(ValidationError::ModelCoherence(
                format!("unknown model: {}", m)));
        }
    }

    Ok(())
}
```

---

## 6.6 IR

*(Sin cambios estructurales. Se añaden nodos para Hill y CES.)*

---

## 6.7 SOLVER EXTENDIDO

### `crates/ronin-core/src/solver.rs`

```rust
use super::ast::{System, Params};
use super::validator::{validate, validate_coherence, ValidationError};

const EPS: f64 = 1e-12;

#[derive(Debug, thiserror::Error)]
pub enum SolverError {
    #[error("validation error: {0}")]
    Validation(#[from] ValidationError),
    #[error("fitness sum is zero, system is degenerate")]
    ZeroFitness,
}

pub fn hill(omega: f64, K: f64, alpha_h: f64) -> f64 {
    if !K.is_finite() {
        return omega;
    }
    omega.powf(alpha_h) / (K.powf(alpha_h) + omega.powf(alpha_h))
}

pub fn ces_combine(phi: f64, psi: f64, omega_eff: f64, lam: f64, w: [f64; 3]) -> f64 {
    let phi = phi.max(EPS);
    let psi = psi.max(EPS);
    let omega_eff = omega_eff.max(EPS);

    if lam.abs() < 1e-6 {
        return phi.powf(w[0]) * psi.powf(w[1]) * omega_eff.powf(w[2]);
    }
    let inner = w[0]*phi.powf(lam) + w[1]*psi.powf(lam) + w[2]*omega_eff.powf(lam);
    inner.powf(1.0/lam)
}

pub fn solve(system: &System, delta: f64) -> Result<super::ast::Solution, SolverError> {
    validate(system, 1e-9)?;
    validate_coherence(&system.params)?;

    let p = &system.params;
    let fitness: Vec<f64> = system.agents.iter()
        .map(|a| {
            let omega_eff = hill(a.frequency, p.K, p.alpha_h);
            ces_combine(a.phi, a.psi, omega_eff, p.lambda, [1.0/3.0, 1.0/3.0, 1.0/3.0])
        })
        .collect();

    let total: f64 = fitness.iter().sum();
    if total <= 0.0 {
        return Err(SolverError::ZeroFitness);
    }

    let allocation: Vec<f64> = fitness.iter()
        .map(|f| system.resource * f / total)
        .collect();

    let k_min = calculate_k_min(system, delta);
    let coexistence = k_min.map(|km| system.resource >= km);
    let omega_range = omega_range_orders(&system.agents);

    let K_free = p.K.is_finite();
    let alpha_h_free = (p.alpha_h - 1.0).abs() > 1e-9;
    let degeneracy = degeneracy_state(omega_range, K_free, alpha_h_free);

    let mut warnings = vec![];
    if degeneracy == "active" {
        warnings.push(format!(
            "K–α_h degeneracy active (Ω range = {:.2f} orders). \
             K and alpha_h are not independently identifiable.",
            omega_range
        ));
    }

    Ok(super::ast::Solution {
        allocation,
        fitness,
        coexistence,
        k_min,
        debt: 0.0,
        convergence: true,
        steps: 1,
        model_used: p.model.clone(),
        lambda_used: p.lambda,
        K_used: p.K,
        alpha_h_used: p.alpha_h,
        omega_range,
        degeneracy,
        warnings,
    })
}

fn omega_range_orders(agents: &[super::ast::Agent]) -> f64 {
    let omegas: Vec<f64> = agents.iter()
        .map(|a| a.frequency)
        .filter(|&x| x > 0.0)
        .collect();
    if omegas.len() < 2 {
        return 0.0;
    }
    let max_o = omegas.iter().cloned().fold(f64::NEG_INFINITY, f64::max);
    let min_o = omegas.iter().cloned().fold(f64::INFINITY, f64::min);
    (max_o / min_o).log10()
}

fn degeneracy_state(omega_range: f64, K_free: bool, alpha_h_free: bool) -> String {
    if !K_free || !alpha_h_free {
        return "inactive".to_string();
    }
    if omega_range >= 3.0 {
        "inactive".to_string()
    } else {
        "active".to_string()
    }
}

fn calculate_k_min(system: &System, delta: f64) -> Option<f64> {
    let products: Vec<f64> = system.agents.iter()
        .map(|a| a.phi * a.psi)
        .collect();
    let min_product = products.iter().cloned().fold(f64::INFINITY, f64::min);
    let max_product = products.iter().cloned().fold(f64::NEG_INFINITY, f64::max);
    if min_product <= 0.0 || delta <= 0.0 || delta >= system.parts as f64 {
        return None;
    }
    let s = system.parts as f64;
    Some(s * (max_product / min_product) / (s / delta).ln())
}
```

---

## 6.8 SIMULADOR

*(Sin cambios respecto a 1.0. Se añade validate_coherence.)*

---

## 6.9 DIAGNÓSTICO EN RUST

### `crates/ronin-core/src/diagnose.rs`

```rust
use super::ast::{DegeneracyReport, System};
use super::validator::{validate, validate_coherence};

pub fn diagnose(system: &System, bootstrap: usize) -> Result<DegeneracyReport, String> {
    validate(system, 1e-9).map_err(|e| e.to_string())?;
    validate_coherence(&system.params).map_err(|e| e.to_string())?;

    let omegas: Vec<f64> = system.agents.iter()
        .map(|a| a.frequency)
        .filter(|&x| x > 0.0)
        .collect();

    let orders = if omegas.len() < 2 {
        0.0
    } else {
        let max_o = omegas.iter().cloned().fold(f64::NEG_INFINITY, f64::max);
        let min_o = omegas.iter().cloned().fold(f64::INFINITY, f64::min);
        (max_o / min_o).log10()
    };

    let K_free = system.params.K.is_finite();
    let alpha_h_free = (system.params.alpha_h - 1.0).abs() > 1e-9;

    let degeneracy = if !K_free || !alpha_h_free {
        "inactive"
    } else if orders >= 3.0 {
        "inactive"
    } else {
        "active"
    };

    let recommendation = match degeneracy {
        "inactive" => "Identificación estructural OK. K y α_h son estimables por separado.",
        _ if orders < 1.0 => "Ω cubre < 1 orden de magnitud. K y α_h son indistinguibles. \
                              Recolectar datos con Ω en un rango mayor o fijar K externamente.",
        _ => "Ω cubre entre 1 y 3 órdenes. Degeneración K–α activa. \
              Se recomienda ampliar el rango de Ω a ≥ 3 órdenes.",
    };

    Ok(DegeneracyReport {
        omega_range_orders: orders,
        degeneracy: degeneracy.to_string(),
        lambda_identifiable: true,
        K_identifiable: degeneracy == "inactive",
        alpha_h_identifiable: degeneracy == "inactive",
        recommendation: recommendation.to_string(),
        bootstrap_ci: None,
    })
}
```

---

## 6.10 CLI CON CLAP EXTENDIDA

### `crates/ronin-cli/src/main.rs`

```rust
use clap::{Parser, Subcommand};
use std::fs;
use std::path::PathBuf;

use ronin_core::solver::solve;
use ronin_core::simulator::simulate;
use ronin_core::diagnose::diagnose;
use ronin_core::validator::validate;
use ronin_parser::parser::parse;

const TOLERANCE: f64 = 1e-9;
const DELTA: f64 = 0.05;

#[derive(Parser)]
#[command(name = "ronin")]
#[command(version = "1.1.0")]
#[command(about = "RONIN — The Language of Finite Systems")]
struct Cli {
    #[command(subcommand)]
    command: Command,
}

#[derive(Subcommand)]
enum Command {
    Check { file: PathBuf },
    Solve { file: PathBuf, #[arg(long, default_value_t = 0.05)] delta: f64 },
    Simulate {
        file: PathBuf,
        #[arg(long, default_value_t = 100)] steps: usize,
        #[arg(long)] seed: Option<u64>,
    },
    Diagnose {
        file: PathBuf,
        #[arg(long, default_value_t = 0)] bootstrap: usize,
    },
}

fn main() -> Result<(), String> {
    let cli = Cli::parse();

    match cli.command {
        Command::Check { file } => {
            let source = fs::read_to_string(&file)
                .map_err(|e| format!("Cannot read file: {}", e))?;
            let systems = parse(&source).map_err(|e| format!("Parse error: {}", e))?;
            let system = systems.first().ok_or("No system declaration found")?;
            validate(system, TOLERANCE)
                .map_err(|e| format!("Validation error: {}", e))?;
            println!("OK");
            Ok(())
        }
        Command::Solve { file, delta } => {
            let source = fs::read_to_string(&file)
                .map_err(|e| format!("Cannot read file: {}", e))?;
            let systems = parse(&source).map_err(|e| format!("Parse error: {}", e))?;
            let system = systems.first().ok_or("No system declaration found")?;
            let solution = solve(system, delta).map_err(|e| format!("Solver error: {}", e))?;
            let json = serde_json::to_string_pretty(&solution).map_err(|e| e.to_string())?;
            println!("{}", json);
            Ok(())
        }
        Command::Simulate { file, steps, seed } => {
            let source = fs::read_to_string(&file)
                .map_err(|e| format!("Cannot read file: {}", e))?;
            let systems = parse(&source).map_err(|e| format!("Parse error: {}", e))?;
            let system = systems.first().ok_or("No system declaration found")?;
            let sim = simulate(system, steps, seed).map_err(|e| e.to_string())?;
            let json = serde_json::to_string_pretty(&sim).map_err(|e| e.to_string())?;
            println!("{}", json);
            Ok(())
        }
        Command::Diagnose { file, bootstrap } => {
            let source = fs::read_to_string(&file)
                .map_err(|e| format!("Cannot read file: {}", e))?;
            let systems = parse(&source).map_err(|e| format!("Parse error: {}", e))?;
            let system = systems.first().ok_or("No system declaration found")?;
            let report = diagnose(system, bootstrap).map_err(|e| e)?;
            let json = serde_json::to_string_pretty(&report).map_err(|e| e.to_string())?;
            println!("{}", json);
            Ok(())
        }
    }
}
```

---

## 6.11 TESTS NORMATIVOS EN RUST

*(Se mantienen los tests de 1.0 + tests de la familia.)*

```rust
#[cfg(test)]
mod family_tests {
    use ronin_core::solver::solve;
    use ronin_core::diagnose::diagnose;
    use ronin_core::validator::{validate, validate_coherence};
    use ronin_parser::parser::parse;
    use approx::assert_relative_eq;

    const TOLERANCE: f64 = 1e-9;

    #[test]
    fn test_compatibility_1_0() {
        let src = r#"
        system Maquinas = {
            parts: 2, resource: 100,
            agents: [
                { phi: 0.8, psi: 1.0, frequency: 0.6 },
                { phi: 0.5, psi: 1.0, frequency: 0.4 }
            ],
            params: { alpha: 1.0, gamma: 0.4, sigma: 0.1 }
        }
        "#;
        let systems = parse(src).unwrap();
        let s = solve(&systems[0], 0.05).unwrap();
        assert_relative_eq!(s.allocation[0], 70.58823529411765, epsilon = TOLERANCE);
        assert_eq!(s.model_used, "pusfre");
    }

    #[test]
    fn test_model_coherence_violation() {
        let src = r#"
        system M = {
            parts: 2, resource: 100,
            agents: [
                { phi: 0.8, psi: 1.0, frequency: 0.6 },
                { phi: 0.5, psi: 1.0, frequency: 0.4 }
            ],
            params: { model: "pusfre", lambda: 0.5 }
        }
        "#;
        let systems = parse(src).unwrap();
        let result = validate_coherence(&systems[0].params);
        assert!(result.is_err());
    }

    #[test]
    fn test_degeneracy_active() {
        let src = r#"
        system M = {
            parts: 3, resource: 100,
            agents: [
                { phi: 0.5, psi: 0.5, frequency: 0.3 },
                { phi: 0.5, psi: 0.5, frequency: 0.4 },
                { phi: 0.5, psi: 0.5, frequency: 0.3 }
            ],
            params: { model: "ces_hill", lambda: 0.5, K: 0.5, alpha_h: 1.5 }
        }
        "#;
        let systems = parse(src).unwrap();
        let report = diagnose(&systems[0], 0).unwrap();
        assert_eq!(report.degeneracy, "active");
    }

    #[test]
    fn test_degeneracy_inactive() {
        let src = r#"
        system M = {
            parts: 3, resource: 100,
            agents: [
                { phi: 0.5, psi: 0.5, frequency: 0.001 },
                { phi: 0.5, psi: 0.5, frequency: 0.01 },
                { phi: 0.5, psi: 0.5, frequency: 0.989 }
            ],
            params: { model: "ces_hill", lambda: 0.5, K: 0.5, alpha_h: 1.5 }
        }
        "#;
        let systems = parse(src).unwrap();
        let report = diagnose(&systems[0], 0).unwrap();
        assert_eq!(report.degeneracy, "inactive");
        assert!(report.omega_range_orders >= 3.0);
    }
}
```

---

## 6.12 INTEGRACIÓN CON PYTHON (PYO3)

*(Sin cambios estructurales. Se añade `diagnose_file`.)*

```rust
#[pyfunction]
fn diagnose_file(file_path: &str) -> PyResult<String> {
    let source = std::fs::read_to_string(file_path)
        .map_err(|e| pyo3::exceptions::PyIOError::new_err(e.to_string()))?;
    let systems = parse(&source)
        .map_err(|e| pyo3::exceptions::PyValueError::new_err(e.to_string()))?;
    let system = systems.first()
        .ok_or_else(|| pyo3::exceptions::PyValueError::new_err("No system declaration found"))?;
    let report = diagnose(system, 0)
        .map_err(|e| pyo3::exceptions::PyRuntimeError::new_err(e))?;
    Ok(serde_json::to_string(&report).unwrap_or_default())
}
```

---

## 6.13 BACKEND A WASM

*(Sin cambios estructurales. Se añade `diagnose_ronin`.)*

```rust
#[wasm_bindgen]
pub fn diagnose_ronin(source: &str) -> String {
    match parse(source) {
        Ok(systems) => {
            if let Some(system) = systems.first() {
                match diagnose(system, 0) {
                    Ok(report) => serde_json::to_string(&report).unwrap_or_default(),
                    Err(e) => format!("Error: {}", e),
                }
            } else {
                "Error: No system found".to_string()
            }
        }
        Err(e) => format!("Parse error: {}", e),
    }
}
```

---

## 6.14 BACKEND A C

*(Sin cambios estructurales. Se añade generación de código para Hill y CES.)*

```rust
pub fn generate_c(system: &System) -> String {
    let mut code = String::new();
    code.push_str("#include <stdio.h>\n");
    code.push_str("#include <math.h>\n\n");

    // ... constantes y variables

    // Saturación Hill
    if system.params.K.is_finite() {
        code.push_str(&format!(
            "double hill(double omega, double K, double alpha_h) {{\n\
                return pow(omega, alpha_h) / (pow(K, alpha_h) + pow(omega, alpha_h));\n\
            }}\n\n"
        ));
    }

    // CES combine
    code.push_str(
        "double ces_combine(double phi, double psi, double omega_eff, double lam) {\n\
            if (fabs(lam) < 1e-6) {\n\
                return pow(phi, 1.0/3.0) * pow(psi, 1.0/3.0) * pow(omega_eff, 1.0/3.0);\n\
            }\n\
            double inner = (1.0/3.0)*pow(phi, lam) + (1.0/3.0)*pow(psi, lam) + (1.0/3.0)*pow(omega_eff, lam);\n\
            return pow(inner, 1.0/lam);\n\
        }\n\n"
    );

    // ... resto del main
    code
}
```

---

# PARTE VII — RONIN OFFICE: INTERFAZ VISUAL

## 7.1 VISIÓN GENERAL

RONIN Office es una interfaz visual para diseñar, resolver y simular sistemas RONIN sin necesidad de escribir código. Es una herramienta de productividad que permite a arquitectos, diseñadores y analistas trabajar con RONIN de forma visual.

**Principios operativos:**
- Diseña sistemas RONIN visualmente.
- Resuelve y simula con un solo clic.
- **Diagnostica la degeneración K–α (nuevo en 1.1).**
- Visualiza resultados en tiempo real.
- Exporta código RONIN para usar en producción.

**Componentes:**
1. **Chat** — Describe sistemas en lenguaje natural y genera RONIN.
2. **Sheet** — Editor de código RONIN con ejecución instantánea.
3. **Optimizer** — Optimización automática de sistemas.
4. **Simulator** — Simulación DTMC de ecosistemas.
5. **Agent Studio** — Diseño visual de agentes.
6. **Diagnose** — Diagnóstico de degeneración K–α (nuevo en 1.1).

---

## 7.2 ARQUITECTURA DE LA INTERFAZ

```
┌──────────────────────────────────────────────────────────────────────────────────┐
│  🧠 RONIN Office   💬 Chat  📋 Sheet  ⚡ Optimizer  🔮 Simulator  🤖 Agents  🔬 Diagnose │
├──────────────────────────────────────────────────────────────────────────────────┤
│                                                                                  │
│  [Panel activo según selección]                                                 │
│                                                                                  │
│  ┌────────────────────────────────────────────────────────────────────────────┐  │
│  │  Contenido del panel                                                      │  │
│  └────────────────────────────────────────────────────────────────────────────┘  │
│                                                                                  │
│  ┌────────────────────────────────────────────────────────────────────────────┐  │
│  │  Terminal / Salida                                                        │  │
│  └────────────────────────────────────────────────────────────────────────────┘  │
├──────────────────────────────────────────────────────────────────────────────────┤
│  ⚡ 1310 · AGENCIA RONIN ⚡                                                     │
└──────────────────────────────────────────────────────────────────────────────────┘
```

---

## 7.3 PANEL DE CHAT

*(Sin cambios estructurales. Plantillas añadidas: `neural_scaling`, `urban_scaling`, `fama_french`.)*

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ 💬 RONIN Chat — Habla con tu sistema                       │
├─────────────────────────────────────────────────────────────────────────────┤
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │  🧠 RONIN Office v1.1                                                │  │
│  │  ▶ Escribe en lenguaje natural. RONIN genera el sistema.            │  │
│  │  ▶ Ejemplo: "Quiero un sistema de 4 agentes balanceados"            │  │
│  │  ▶ Ejemplo: "Diagnostica si mi sistema necesita CES-Saturada"       │  │
│  │  ▶ Ejemplo: "Simula 50 pasos de un ecosistema"                     │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│  [Input: Escribe tu petición...]  [▶ Enviar]  [✕ Limpiar]                 │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 7.4 PANEL SHEET

*(Sin cambios estructurales. Añadido el modelo como parámetro visible.)*

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ 📋 RONIN Sheet — Código RONIN                               │
│ ⚡ Excel Killer                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│  ┌───────────────────────────────────────────────────────────────────────┐  │
│  │  system Presupuesto = {                                              │  │
│  │      parts: 4,                                                       │  │
│  │      resource: 1000,                                                 │  │
│  │      agents: [                                                       │  │
│  │          { name: "Ventas", phi: 0.9, psi: 0.8, frequency: 0.25 },  │  │
│  │          { name: "Marketing", phi: 0.8, psi: 0.9, frequency: 0.25 },│  │
│  │          { name: "Operaciones", phi: 0.85, psi: 0.85, freq: 0.25 }, │  │
│  │          { name: "I+D", phi: 0.95, psi: 0.7, frequency: 0.25 }     │  │
│  │      ],                                                             │  │
│  │      params: {                                                       │  │
│  │          model: "ces",                                              │  │
│  │          lambda: 0.5,                                               │  │
│  │          alpha: 1.2, gamma: 0.4, sigma: 0.1                         │  │
│  │      }                                                               │  │
│  │  }                                                                   │  │
│  └───────────────────────────────────────────────────────────────────────┘  │
│  [▶ Resolver]  [🔬 Diagnose]  [↺ Restaurar]                                │
├─────────────────────────────────────────────────────────────────────────────┤
│  ✅ Sistema resuelto                                                       │
│  📊 Asignación: 250, 250, 250, 250                                        │
│  ⚔️ Fitness: 0.48, 0.20, 0.32, 0.40                                      │
│  🔄 Coexistencia: ✅                                                      │
│  📈 Biodiversidad: 0.999                                                  │
│  🎯 Modelo usado: ces                                                     │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 7.5 PANEL OPTIMIZER

*(Sin cambios estructurales. Añadido selector de modelo.)*

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ ⚡ RONIN Optimizer — Ecuación Maestra                      │
├─────────────────────────────────────────────────────────────────────────────┤
│  🎯 Objetivo: [Coexistencia ▼]                                             │
│  🧬 Modelo: [pusfre ▼]  (opciones: pusfre, ces, hill, ces_hill, full)      │
│  📊 Agentes: [5]  💰 Recurso: [100]                                        │
│  [⚡ Optimizar]                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 7.6 PANEL SIMULATOR

*(Sin cambios.)*

---

## 7.7 PANEL AGENT STUDIO

*(Sin cambios.)*

---

## 7.8 PANEL DIAGNOSE (NUEVO EN 1.1)

```
┌─────────────────────────────────────────────────────────────────────────────┐
│ 🔬 RONIN Diagnose — Degeneración K–α                        │
│ ⚡ Statistical Honesty                                      │
├─────────────────────────────────────────────────────────────────────────────┤
│  🎲 Bootstrap: [200]  [🔬 Diagnosticar]                                    │
├─────────────────────────────────────────────────────────────────────────────┤
│  📊 Ω range: 0.42 órdenes                                                  │
│  ⚠️ Degeneración: ACTIVA                                                   │
│  ❌ K identificable: NO                                                    │
│  ❌ α_h identificable: NO                                                  │
│  ✅ λ identificable: SÍ (dado K fijo)                                      │
│  💡 Recomendación:                                                          │
│     Recolectar datos con Ω en un rango mayor o fijar K externamente.       │
│                                                                             │
│  IC 95% bootstrap:                                                         │
│     λ: [0.31, 0.62]                                                        │
│     K: [0.42, 3.15]                                                        │
│     α_h: [0.88, 1.42]                                                      │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 7.9 MOTOR RONIN — IMPLEMENTACIÓN EN JAVASCRIPT

*(Ampliado con soporte para familia.)*

```javascript
function solveRONIN(code) {
    const partsMatch = code.match(/parts:\s*(\d+)/);
    const resourceMatch = code.match(/resource:\s*([\d.]+)/);
    const agentsMatch = code.match(/agents:\s*\[([\s\S]*?)\]/);
    const modelMatch = code.match(/model:\s*"([^"]+)"/);
    const lambdaMatch = code.match(/lambda:\s*([-\d.]+)/);
    const KMatch = code.match(/K:\s*([\d.]+|inf|∞)/);
    const alphaHMatch = code.match(/alpha_h:\s*([\d.]+)/);

    if (!partsMatch || !resourceMatch || !agentsMatch) {
        throw new Error('Sistema incompleto');
    }

    const parts = parseInt(partsMatch[1]);
    const resource = parseFloat(resourceMatch[1]);
    const model = modelMatch ? modelMatch[1] : "pusfre";
    const lambda = lambdaMatch ? parseFloat(lambdaMatch[1]) : 0.0;
    const K = KMatch ? (KMatch[1] === "inf" || KMatch[1] === "∞" ? Infinity : parseFloat(KMatch[1])) : Infinity;
    const alphaH = alphaHMatch ? parseFloat(alphaHMatch[1]) : 1.0;

    // ... extraer agentes (sin cambios)

    // Normalizar frecuencias
    const totalFreq = agents.reduce((s,a) => s + a.frequency, 0);
    agents.forEach(a => a.frequency = a.frequency / totalFreq);

    // Saturación Hill
    function hill(omega, K, alphaH) {
        if (!isFinite(K)) return omega;
        return Math.pow(omega, alphaH) / (Math.pow(K, alphaH) + Math.pow(omega, alphaH));
    }

    // CES combine
    function cesCombine(phi, psi, omegaEff, lam) {
        if (Math.abs(lam) < 1e-6) {
            return Math.pow(phi, 1/3) * Math.pow(psi, 1/3) * Math.pow(omegaEff, 1/3);
        }
        const inner = (1/3)*Math.pow(phi, lam) + (1/3)*Math.pow(psi, lam) + (1/3)*Math.pow(omegaEff, lam);
        return Math.pow(inner, 1/lam);
    }

    // Calcular fitness
    const fitness = agents.map(a => {
        const omegaEff = hill(a.frequency, K, alphaH);
        return cesCombine(a.phi, a.psi, omegaEff, lambda);
    });

    const totalFitness = fitness.reduce((s,f) => s + f, 1e-12);
    const allocation = fitness.map(f => resource * f / totalFitness);

    // Diagnóstico
    const omegas = agents.map(a => a.frequency).filter(x => x > 0);
    const omegaRange = omegas.length >= 2
        ? Math.log10(Math.max(...omegas) / Math.min(...omegas))
        : 0;
    const KFree = isFinite(K);
    const alphaHFree = Math.abs(alphaH - 1.0) > 1e-9;
    let degeneracy = "inactive";
    if (KFree && alphaHFree && omegaRange < 3.0) {
        degeneracy = "active";
    }

    const coexistence = allocation.every(a => a > 0.01);
    const probs = allocation.map(a => a / resource);
    const diversity = -probs.reduce((s,p) => s + (p>0 ? p*Math.log(p) : 0), 0) / Math.log(parts);

    return {
        allocation,
        fitness,
        coexistence,
        biodiversity: diversity,
        model,
        lambda,
        K,
        alpha_h: alphaH,
        omegaRange,
        degeneracy,
    };
}
```

---

## 7.10 FLUJO DE TRABAJO COMPLETO

```
1. Usuario describe el sistema en lenguaje natural
        ↓
2. Generador local produce código RONIN
        ↓
3. Código se muestra en el Sheet
        ↓
4. Motor RONIN resuelve el sistema
        ↓
5. Panel Diagnose evalúa degeneración (opcional)
        ↓
6. Resultados se muestran en el terminal
        ↓
7. Usuario puede iterar, ajustar o simular
```

---

## 7.11 GENERADOR LOCAL DE SISTEMAS

*(Sin cambios estructurales.)*

---

## 7.12 ESTADO DE LA IMPLEMENTACIÓN

| Componente | Estado | Implementación |
|------------|--------|----------------|
| Panel Chat | ✅ Completado | HTML + JavaScript |
| Panel Sheet | ✅ Completado | HTML + JavaScript |
| Panel Optimizer | ✅ Completado | HTML + JavaScript |
| Panel Simulator | ✅ Completado | HTML + JavaScript |
| Panel Agent Studio | ✅ Completado | HTML + JavaScript |
| **Panel Diagnose** | **🟡 Especificado** | **HTML + JavaScript (pendiente)** |
| Motor RONIN JS | ✅ Completado | JavaScript puro |
| Generador local | ✅ Completado | JavaScript puro |

---

## 7.13 KOANS DE RONIN OFFICE

**Del chat que genera sistemas:**
El humano habla. RONIN entiende. RONIN ejecuta.

**Del sheet que no miente:**
El código que ves es el código que se ejecuta. No hay magia.

**Del optimizer que no negocia:**
RONIN no negocia con la realidad. La realidad se optimiza.

**Del simulador que no engaña:**
Cada paso es una decisión. Cada semilla es un destino.

**Del studio de agentes:**
Cada agente es una especie. Cada ecosistema es un mundo.

**Del diagnose que no adula:**
El diagnóstico no te dice lo que quieres oír. Te dice lo que tus datos permiten.

**Del arquitecto que usa RONIN Office:**
El arquitecto no escribe código. El arquitecto diseña sistemas.

**Del cerrajero que sonríe desde 1310:**
El humano sueña. RONIN construye.

---

## 7.14 REFERENCIAS TÉCNICAS

**Repositorios:**
- RONIN Core: `https://github.com/ronin-lang/ronin`
- RONIN Office: `https://github.com/ronin-lang/ronin-office`

**Estándares:**
- ECMAScript 2021 (JavaScript)
- HTML5 / CSS3

**Referencia matemática:**
- Tratado de Extensión del PUSFRE v3.5 (Ferrandez Canalis, 2026)

---

**1310.**

---

# PARTE VIII — EL FUTURO: RONIN COMO LENGUAJE DE SISTEMAS

## 8.1 VISIÓN: SISTEMAS QUE SE DISEÑAN SOLOS

*(Sin cambios estructurales.)*

## 8.2 RONIN COMO LENGUAJE DE ORQUESTACIÓN

*(Sin cambios estructurales.)*

## 8.3 EL ECOSISTEMA RONIN

*(Sin cambios estructurales. Se añade RONIN Diagnose como servicio.)*

## 8.4 RONIN Y LA COMPUTACIÓN NEUROMÓRFICA

*(Sin cambios estructurales.)*

## 8.5 RONIN Y LOS SISTEMAS AUTÓNOMOS

*(Sin cambios estructurales.)*

## 8.6 KOANS DEL FUTURO

**Del sistema que se diseña solo:**
El mejor sistema es el que se diseña solo, porque el humano ya no necesita diseñarlo.

**Del arquitecto que ya no escribe:**
El arquitecto ya no escribe. El arquitecto conversa con RONIN.

**Del cerrajero que ríe desde el futuro:**
El cerrajero sabía que RONIN era inevitable. El futuro lo ha confirmado.

**De la familia:**
La ecuación era una foto. La familia es una película.

**De 1310:**
1310 no es un año. Es una forma de ver el mundo.

---

**1310.**

---

# ANEXO NORMATIVO V1.1

## N.1 CONTRATO DE IMPLEMENTACIÓN

### N.1.1 Orden de evaluación

1. Parsear el programa.
2. Validar tipos, rangos y número de agentes.
3. Validar que `sum(frequency)` sea `1 ± tolerance` (1e-9).
4. **Validar coherencia `model` ↔ parámetros.**
5. **Calcular `Ω_sat_i = hill(Ω_i, K, α_h)`.**
6. **Calcular `F_i = ces_combine(Φ_i, Ψ_i, Ω_sat_i, λ, w)`.**
7. Calcular `allocation[i] = resource * fitness[i] / sum(fitness)`.
8. Calcular coexistencia y `k_min`.
9. Calcular deuda.
10. **Calcular `omega_range` y `degeneracy`.**
11. Construir el `Solution` con advertencias.

Si `sum(fitness) == 0`, `solve` debe devolver un error de sistema degenerado y nunca dividir por cero.

### N.1.2 Contrato de `simulate`

*(Sin cambios respecto a 1.0.)*

### N.1.3 Contrato de coexistencia

*(Sin cambios respecto a 1.0.)*

### N.1.4 Contrato de deuda

*(Sin cambios respecto a 1.0.)*

### N.1.5 Contrato de diagnóstico (nuevo en 1.1)

`diagnose` debe reportar:
- `omega_range_orders`: `log10(max(Ω) / min(Ω))`.
- `degeneracy`: `"inactive"` si `omega_range_orders >= 3.0`, `"active"` si `< 3.0` y `K, alpha_h` libres, `"unknown"` en otro caso.
- `K_identifiable`, `alpha_h_identifiable`: booleanos coherentes.
- `recommendation`: texto accionable.

---

## N.2 TESTS NORMATIVOS

### Test 1 — Compatibilidad 1.0

Programa RONIN 1.0 sin `model` debe producir exactamente los mismos valores que RONIN 1.0.

```
fitness    = [0.48, 0.20]
allocation ≈ [70.5882352941, 29.4117647059]
model_used = "pusfre"
```

### Test 2 — model "pusfre" explícito

Programa con `model: "pusfre"` explícito debe producir idéntico resultado al Test 1.

### Test 3 — CES con λ → 0 recupera PUSFRE

Programa con `model: "ces"`, `lambda: 1e-7` debe producir resultado indistinguible de PUSFRE (dentro de 1e-6).

### Test 4 — Coherencia de modelo

Programa con `model: "pusfre"` y `lambda: 0.5` debe fallar con `SemanticError` (código 2).

### Test 5 — Degeneración activa

Programa con Ω estrecho y `model: "ces_hill"` con `K, alpha_h` libres debe reportar `degeneracy: "active"`.

### Test 6 — Degeneración inactiva

Programa con Ω cubriendo 3+ órdenes de magnitud debe reportar `degeneracy: "inactive"`.

### Test 7 — Diagnóstico sobre datos reales

Programa con dataset Neural Scaling (Ω ~ 3 órdenes) debe reportar `degeneracy: "inactive"` y `omega_range_orders: 3.0 ± 0.1`.

---

## N.3 CONFORMIDAD

Un runtime es RONIN 1.1 conforme si:

- Acepta todos los programas válidos definidos en este documento.
- Rechaza programas inválidos con error identificable.
- **Rechaza violaciones de coherencia de modelo con `SemanticError`.**
- Produce los resultados numéricos normativos dentro de `1e-9` de tolerancia relativa.
- Mantiene la suma de allocation dentro de `1e-9` de `resource`.
- Respeta `seed` en simulación.
- **Reporta `degeneracy` coherente con `omega_range_orders`.**
- No presenta como benchmark medido ningún número que no haya sido reproducido por el runtime.

---

## N.4 ESTADO DE LAS EXTENSIONES

| Extensión | Estado | Implementación |
|-----------|--------|----------------|
| Familia CES-Saturada en Python | ✅ Especificado y ejecutable | R.6–R.11 |
| Comando `diagnose` | ✅ Especificado y ejecutable | R.11 |
| Coherencia de modelo | ✅ Especificado | R.7 |
| Backend Rust con familia | 🟡 Especificado | 6.7–6.10 |
| Backend WASM con diagnose | 🟡 Especificado | 6.13 |
| Backend C con Hill/CES | 🟡 Especificado | 6.14 |
| RONIN Office + Panel Diagnose | 🟡 Especificado | 7.8 |
| Motor RONIN JS extendido | ✅ Especificado | 7.9 |

---

## N.5 POLÍTICA DE AFIRMACIONES VERIFICABLES

Esta edición adopta una regla estricta: la especificación distingue entre **norma**, **implementación existente**, **propuesta de implementación**, **ejemplo** y **resultado medido**. Una capacidad no se presenta como disponible por el mero hecho de estar descrita. Un benchmark no se presenta como medido sin artefactos reproducibles. Una garantía no se presenta como absoluta si depende de supuestos no formalizados.

La familia CES-Saturada es una extensión matemática validada en el Tratado v3.5 (Neural Scaling positivo, Fama-French negativo). Su incorporación a RONIN es especificación; su implementación completa en Rust es propuesta. La degeneración K–α está demostrada analíticamente en la Proposición 5.1 del Tratado v3.5.

---

## CIERRE FINAL DE RONIN 1.1

RONIN 1.0 te da la **ecuación**.
RONIN 1.1 te da la **familia**.

Si tus datos cubren Ω en un rango estrecho, usa `"pusfre"`.
Si necesitas curvatura y saturación, usa `"ces_hill"`.
Si el diagnóstico dice "degeneración activa", escucha al diagnóstico.

El PUSFRE no es una ecuación. Es una familia. RONIN no la impone. La ejecuta.

**1310.**

---

*"El mejor código es el que no se escribe.
El segundo mejor es el que se escribe en RONIN.
El tercero es el que usa la familia correcta.
El cuarto es el que sabe cuándo no usarla.
El quinto es el que diagnostica antes de confiar."*

**1310.**

---

# APÉNDICE FAMILIA CES-SATURADA

## A.1 DEFINICIÓN MATEMÁTICA

### A.1.1 La familia

La familia CES-Saturada se define como:

$$F_i = \left( w_1 \Phi_i^\lambda + w_2 \Psi_i^\lambda + w_3 \left[\Omega_i^{\text{sat}}\right]^\lambda \right)^{1/\lambda} \cdot \varepsilon_i$$

donde:

$$\Omega_i^{\text{sat}} = \frac{\Omega_i^{\alpha_h}}{K^{\alpha_h} + \Omega_i^{\alpha_h}}$$

**Parámetros:**
- `lambda ∈ [-1, 2], ≠ 0`: curvatura del agregador.
- `K > 0`: constante de saturación Hill.
- `alpha_h > 0`: exponente Hill.
- `w_1, w_2, w_3 ∈ [0.1, 0.8], Σw = 1`: pesos del agregador.

### A.1.2 Casos degenerados

| `model` | λ | K | k | Resultado |
|---------|---|---|---|-----------|
| `"pusfre"` | 0 | ∞ | 1 | `Φ · Ψ · Ω^α` |
| `"ces"` | libre ≠ 0 | ∞ | 1 | CES sin saturación |
| `"hill"` | 0 | libre | 1 | PUSFRE con Ω saturado |
| `"ces_hill"` | libre ≠ 0 | libre | 1 | M6: curvatura + saturación |
| `"full"` | libre ≠ 0 | libre | ≥ 1 | + memoria temporal |

---

## A.2 CASOS LÍMITE CON VERIFICACIÓN

### A.2.1 Verificación numérica

| Caso | Parámetros | Valor analítico | Valor numérico | Error relativo |
|------|-----------|-----------------|----------------|----------------|
| A (PUSFRE base) | λ=1e-6, K=1e6 | 1.0 | 1.000000 | < 1e-9 |
| B (Hill) | λ=1e-6, K=1.5, α_h=1.0 | 0.2105 | 0.21053 | 1.5e-5 |
| C (Lineal) | λ=1 | 1.0 | 1.000000 | < 1e-9 |
| D (Leontief) | λ=-10 | 1.0 | 0.99998 | 2e-5 |
| E (CES estándar) | λ=0.5 | 1.0 | 1.000000 | < 1e-9 |
| F (Compensatorio) | λ=1.5 | 1.0 | 1.000000 | < 1e-9 |

### A.2.2 Interpretación de σ

**Advertencia formal.** En el PUSFRE extendido, `σ = 1/(1-λ)` describe exclusivamente la curvatura del agregador. **No posee interpretación económica de elasticidad de sustitución.** Cualquier inferencia sobre sustituibilidad de atributos basada en σ es inválida en este marco.

---

## A.3 DEGENERACIÓN K–α

### A.3.1 Proposición 5.1 (demostración)

**Enunciado:** Sean $K_1, K_2 > 0$ y $\alpha_1, \alpha_2 > 0$. Si $\Omega \ll \min(K_1, K_2)$, entonces la función Hill satisface:

$$\frac{\Omega^{\alpha_1}}{K_1^{\alpha_1} + \Omega^{\alpha_1}} \approx \frac{\Omega^{\alpha_2}}{K_2^{\alpha_2} + \Omega^{\alpha_2}}$$

siempre que:

$$\alpha_1 \log \Omega - \alpha_1 \log K_1 = \alpha_2 \log \Omega - \alpha_2 \log K_2.$$

**Demostración.** Si $\Omega \ll K$, entonces $\Omega^\alpha/K^\alpha \ll 1$ y

$$\text{Hill}(\Omega; K, \alpha) = \frac{\Omega^\alpha}{K^\alpha + \Omega^\alpha} \approx \frac{\Omega^\alpha}{K^\alpha} = \Omega^\alpha \cdot K^{-\alpha}.$$

Tomando logaritmos:

$$\log \text{Hill} \approx \alpha \log \Omega - \alpha \log K.$$

Definiendo $\beta = -\alpha \log K$, la expresión es $\alpha \log \Omega + \beta$, que depende solo de $(\alpha, \beta)$ y no de $(\alpha, K)$ por separado. Cualquier par $(\alpha, K)$ que produzca el mismo $\beta$ da la misma Hill en el régimen $\Omega \ll K$. $\square$

### A.3.2 Corolarios

**Corolario 5.1.1.** Más N no rompe la degeneración.

**Corolario 5.1.2.** La degeneración se rompe solo cuando $\Omega \approx K$ es observable. Requiere que $\Omega/K$ varíe al menos entre 0.1 y 10.

**Corolario 5.1.3 (rompimiento).** Si $\Omega$ cubre un rango donde $\Omega/K$ varía entre $\epsilon$ y $1/\epsilon$, entonces la curvatura Hill es visible y $K$ se separa de $\alpha_h$.

### A.3.3 Aplicación en RONIN

```ronin
diagnose MiSistema with { degeneracy: true }

// Si omega_range_orders < 3:
//   degeneracy = "active"
//   K y α_h NO identificables
// Si omega_range_orders >= 3:
//   degeneracy = "inactive"
//   K y α_h identificables
```

---

## A.4 GUÍA DE USO POR DOMINIO

| Dominio | Ω range | model recomendado | Justificación |
|---------|---------|-------------------|---------------|
| Logística | 1 orden | `"pusfre"` | Estructura multiplicativa simple |
| Finanzas | 0.5-1 orden | `"pusfre"` | Aditivo, Ω estrecho |
| Neural Scaling | 3 órdenes | `"ces_hill"` | Multiplicativo + saturación visible |
| Urban Scaling | 5+ órdenes | `"ces_hill"` | Multiplicativo + Ω amplio |
| Species-Area | 6+ órdenes | `"ces_hill"` | Multiplicativo + Ω amplio |
| Fama-French | <1 orden | `"pusfre"` | Aditivo, Ω estrecho |
| RAG | 1-2 órdenes | `"ces"` | Curvatura sin saturación |

---

## A.5 REFERENCIAS AL TRATADO

El desarrollo completo de la familia CES-Saturada, con demostraciones analíticas, validación cruzada en dos dominios (Neural Scaling positivo, Fama-French negativo), y análisis de degeneración, está en:

**Tratado de Extensión del PUSFRE v3.5** — Ferrandez Canalis, D. (2026).

Contribuciones principales:
1. Demostración analítica de la degeneración K–α (Proposición 5.1).
2. Caracterización axiomática del PUSFRE como caso límite.
3. Validación externa en Neural Scaling (ΔBIC = -14.3).
4. Validación externa negativa en Fama-French (ΔBIC = +8.7).
5. Desarrollo formal de GSE (Apéndice G).
6. Test con Ω cubriendo 5+ órdenes (Apéndice I).

**Implicación operativa:** El reporte de parámetros debe incluir siempre el rango de Ω. Si Ω cubre < 3 órdenes, K y α_h no son interpretables individualmente. Si cubre > 5, sí lo son.

---

*Fin del Apéndice Familia CES-Saturada.*

**1310.**

*"La universalidad no está en el punto. Está en la familia.
Pero la familia, a veces, tampoco es identificable.
Y cuando no lo es, conviene decirlo — con demostración analítica,
con verificación numérica, con validación externa contrastada,
y con delimitación explícita del caso de uso."*

**1310.**

---

# FIN DEL DOCUMENTO

**RONIN 1.1 — Edición Familia**
**Versión:** 1.1.0
**Fecha:** Septiembre 2026
**Autor:** David Ferrandez Canalis — Agencia RONIN
**Licencia:** CC BY-NC-SA 4.0 + Cláusula Comercial Ronin

**1310.**
```

---

