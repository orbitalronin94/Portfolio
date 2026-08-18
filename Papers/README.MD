
# README — EL CORPUS RONIN

## *Guía de Navegación para el Arquitecto, el Crítico y el Curioso*

**Versión:** 2.0  
**Autor:** David Ferrandez Canalis — Agencia RONIN  
**Fecha:** Agosto de 2026  
**Propósito:** Que entres, te orientes y sepas exactamente qué estás leyendo. Sin rodeos.  
**Actualización:** Se han incorporado dos nuevos tratados: el *Tratado de la Fatiga de Enrutamiento* (extensión formal del SDDA) y la *Segunda Parte del Atlas de Reducciones* (48 teoremas adicionales).

---

## 1. ¿Qué es esto?

El Corpus RONIN es un **programa de investigación formal** que aspira a una teoría general de **sistemas finitos con recursos escasos**. Su núcleo es el **PUSFRE** (Principio Universal de Sistemas Finitos con Recursos Escasos), que postula que cualquier sistema compuesto por partes que compiten por un recurso limitado puede describirse con las mismas ecuaciones, independientemente del dominio.

El corpus está compuesto por **quince documentos** que se relacionan entre sí como capas de un edificio: desde los cimientos (papers fundacionales) hasta la culminación (teorema fundamental, manual y extensiones). No es una colección de ensayos sueltos. Es una **jerarquía lógica**.

---

## 2. ¿Cómo está estructurado?

El corpus se organiza en **cinco niveles**:

### Nivel 0: Los Papers Fundacionales (La Tríada)
Tres documentos que sientan las bases conceptuales. Cada uno aborda una dimensión de los sistemas RAG multi-agente:

- **Geometría del Olvido** → cómo se retiene (o no) la información en el contexto.
- **Ecología de Agentes** → cómo los agentes compiten por recursos.
- **Deuda Ontológica** → cómo se acumulan las contradicciones en las bases de conocimiento.

### Nivel 1: Unificación
Un documento que **acopla** los tres pilares en un sistema dinámico único y presenta la **Ecuación Maestra** como modelo de fitness.

### Nivel 2: Fundamentación y Teorema
Dos documentos que **demuestran** formalmente la Ecuación Maestra a partir de axiomas (Teorema Fundamental) y sistematizan todos los teoremas del corpus con sus condiciones de validez (Fundamentación Matemática).

### Nivel 3: Manual Operativo
El **Manual Práctico** que traduce el PUSFRE en un protocolo paso a paso y lo valida en **30 dominios** y **25 crisis históricas**. También incluye un anexo comparativo que enfrenta el PUSFRE a modelos clásicos (Schaefer, Markowitz, SIR, VRP…).

### Nivel 4: Extensiones Computacionales y Formales
Tres documentos que demuestran la **universalidad** del PUSFRE:

- **Tratado de Extensión Computacional (Parte I)** → resuelve 5 problemas fuera del ámbito de la IA: logística, finanzas, energía, salud, ciberseguridad, etc.
- **Tratado de Extensión Computacional (Parte II)** → añade 12 aplicaciones adicionales (rutas, segmentación, tráfico, etc.).
- **Tratado de la Fatiga de Enrutamiento** → extiende la Ecuación Maestra con el coste de conmutación entre agentes, añadiendo seis teoremas sobre frecuencia crítica, permanencia mínima, distancia semántica máxima, relajación contextual, topología óptima y coste de estancamiento.

### Nivel 5: Autorrevisión y Reducción
Tres documentos que **cierran el ciclo**:

- **Autorrevisión** → el autor examina críticamente su propia obra, señala sus limitaciones y degrada lo que debe degradarse.
- **Parlamento de los Vivos** → reduce seis teorías contemporáneas (Wolfram, Kauffman, West, Wolpert, Schmidhuber, Venkatasubramanian) a casos límite del PUSFRE.
- **Atlas de Reducciones (Primera y Segunda Parte)** → demuestra formalmente que **96 teoremas clásicos** (desde Nash y Shannon hasta Boltzmann y Black-Scholes, pasando por física, economía, finanzas y filosofía) son casos límite del PUSFRE.

---

## 3. Listado de Archivos y su Rol

| Archivo | Rol | Nivel | Formalidad |
|---------|-----|-------|------------|
| `# LA GEOMETRÍA DEL OLVIDO...md` | Fundacional (cómo se olvida) | 0 | Modelo + hipótesis |
| `# ECOLOGÍA DE AGENTES...md` | Fundacional (competencia ecológica) | 0 | Modelo + conjeturas |
| `# LA DEUDA ONTOLÓGICA...md` | Fundacional (contradicciones RAG) | 0 | Modelo + métricas |
| `# DINÁMICA UNIFICADA...md` | Unificación y SDDA | 1 | Modelo unificado + DTMC |
| `# TRATADO DE FUNDAMENTACIÓN MATEMÁTICA...md` | Teoremas y condiciones | 2 | Formalización de teoremas |
| `# TEOREMA FUNDAMENTAL...md` | Demostración axiomática del PUSFRE | 2 | Teorema demostrado |
| `# EL PRINCIPIO UNIVERSAL...PUSFRE.md` | Manual del arquitecto | 3 | Guía operativa |
| `# MANUAL PRÁCTICO DE APLICACIONES...txt` | 30 casos de uso + anexo histórico | 3 | Aplicación práctica |
| `# TRATADO DE EXTENSIÓN COMPUTACIONAL...md` | 5 aplicaciones transversales | 4 | Demostración de universalidad |
| `# TRATADO DE EXTENSIÓN COMPUTACIONAL — PARTE II.md` | 12 aplicaciones adicionales | 4 | Extensión de la anterior |
| `# TRATADO DE LA FATIGA DE ENRUTAMIENTO.md` | Coste de conmutación entre agentes (6 teoremas) | 4 | Extensión formal del SDDA |
| `# AUTORREVISIÓN DEL CORPUS RONIN — VERSIÓN AMPLIADA.md` | Crítica interna y correcciones | 5 | Autoevaluación |
| `# EL PARLAMENTO DE LOS VIVOS...md` | Reducción de seis autores vivos | 5 | Ejercicio de reducción |
| `# EL ATLAS DE REDUCCIONES...md` | Primera parte: 48 teoremas clásicos | 5 | Cartografía de casos límite |
| `# EL ATLAS DE REDUCCIONES — SEGUNDA PARTE.md` | Segunda parte: 48 teoremas adicionales | 5 | Cartografía extendida |

---

## 4. Orden de Lectura Recomendado

### Ruta 1: Para Ingenieros y Arquitectos (quiero herramientas que funcionen)
1. **Manual Práctico** → lee el capítulo 0 y el protocolo de las 5 P.
2. **Dinámica Unificada** → secciones 1 y 3 (Ecuación Maestra y calibración).
3. **Manual Práctico – Anexo** (dentro del mismo archivo) → los 30 casos de uso.
4. **Tratado de la Fatiga de Enrutamiento** → para entender el coste de conmutar entre agentes (imprescindible para orquestadores).
5. Vuelve a los fundacionales solo si necesitas profundizar en un dominio concreto.

### Ruta 2: Para Teóricos y Matemáticos (quiero el núcleo formal)
1. **Teorema Fundamental** → los cinco axiomas y la demostración.
2. **Fundamentación Matemática** → los teoremas con sus condiciones de validez.
3. **Atlas de Reducciones (Primera Parte)** → para ver cómo el PUSFRE contiene a Nash, Shannon, Boltzmann, etc.
4. **Atlas de Reducciones (Segunda Parte)** → para ver cómo se extiende a física, finanzas, filosofía y 48 teoremas más.
5. **Parlamento de los Vivos** → para entender la relación con seis teorías contemporáneas.
6. **Autorrevisión** → para conocer los límites y las correcciones.

### Ruta 3: Para Críticos y Evaluadores (quiero entender sus debilidades)
1. **Autorrevisión** → lee el resumen y la tabla de supervivencia.
2. **El Mapa de Corrección** (apéndice de la Autorrevisión) → donde se indica cómo se han abordado o corregido cada una de las críticas.
3. **Manual Práctico – Anexo Histórico** (dentro del manual) → para ver la validación en crisis reales.
4. **Teorema Fundamental** → para evaluar si la demostración axiomática es sólida.

---

## 5. Cómo navegar por las correcciones

El corpus no es un documento estático. La **Autorrevisión** señala explícitamente qué afirmaciones eran excesivas y las degrada a conjeturas. Pero **no se queda ahí**: el apéndice final, el **"Mapa de Corrección"**, enlaza cada crítica con el archivo donde se ha abordado o solucionado.

Si encuentras una afirmación que te parece dudosa, busca su entrada en la **tabla de supervivencia** de la Autorrevisión. Allí verás si está marcada como:

- 🟢 **Demostrada** (tiene demostración formal en algún tratado).
- 🔵 **Definición válida** (operativa y coherente).
- 🟡 **Modelo plausible** (útil pero no demostrado).
- 🟠 **Insuficientemente justificado** (pendiente de validación externa).
- 🔴 **Degradado o retirado**.

Luego, si tiene una corrección, el **Mapa de Corrección** te dirá exactamente en qué archivo se ha reparado.

---

## 6. Los "Koans" y la retórica

El corpus incluye **koans** al final de varios documentos. Son formulaciones literarias de los conceptos clave. **No son afirmaciones técnicas adicionales**. Están claramente separados del contenido formal. Si buscas rigor, ignóralos; si buscas memorabilidad, léelos.

---

## 7. ¿Qué queda por hacer?

El corpus no está cerrado. Las tareas pendientes, reconocidas por el autor, son:

1. **Publicar los logs de calibración** (o un subconjunto anonimizado) para permitir replicación independiente.
2. **Realizar validación predictiva prospectiva** (no solo postdicción histórica).
3. **Extender el PUSFRE a arquitecturas no Transformer** (SSMs, modelos de difusión, etc.).
4. **Formalizar completamente el coste de la información** en la Ecuación Maestra (diálogo abierto con Wolpert).
5. **Validar empíricamente los seis teoremas de la fatiga de enrutamiento** en sistemas multi-agente de producción.

El corpus es un **programa de investigación en marcha**, no una verdad revelada.

---

## 8. Epílogo del autor

> He escrito esto para que quien quiera construir, construya. Para que quien quiera criticar, critique con precisión. Para que quien quiera entender, tenga un mapa. El Corpus RONIN no es un destino. Es un punto de partida. Ahora, con el Tratado de la Fatiga de Enrutamiento y el Atlas extendido, el mapa cubre el coste de moverse entre agentes y la totalidad de los teoremas de asignación de recursos conocidos. Quien quiera navegar, tiene brújula.

**— David Ferrandez Canalis**  
**Agencia RONIN, Agosto de 2026**  
**1310.**
