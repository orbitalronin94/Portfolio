# ```markdown
# RONIN DYNAMICS — Corpus Técnico v1.0

> La teoría sin implementación es literatura.
> La implementación sin teoría es artesanía.
> Esto es ingeniería.

---

## Qué es esto

Cuatro documentos. Un sistema unificado. Cero metáforas decorativas.

| # | Documento | Fecha | Dominio |
|---|-----------|-------|---------|
| 01 | **La Geometría del Olvido** | Jun 2026 | Topología de la atención en ventanas finitas |
| 02 | **Ecología de Agentes** | Jul 2026 | Dinámicas poblacionales en sistemas multi-agente |
| 03 | **La Deuda Ontológica** | Ago 2026 | Contradicciones silenciosas en bases RAG |
| 04 | **Dinámica Unificada** | Ago 2026 | Tratado de acoplamiento, calibración y validación |

Los tres primeros son la **Tríada RONIN 2026**: diagnóstico.
El cuarto es el **Tratado de Dinámica Unificada**: ejecución.

Sin el 04, los otros tres son taxonomías elegantes.
Sin los tres primeros, el 04 no tiene nada que unificar.
Se leen juntos o no se leen.

---

## Estructura de la carpeta

```
.
├── README.md                          ← Estás aquí
├── LICENSE                            ← CC BY-NC-SA 4.0 + Cláusula Comercial
│
├── docs/
│   ├── 01-geometria-del-olvido.md     ← Capa cero. Topología de la atención.
│   ├── 02-ecologia-de-agentes.md      ← Capa uno. Competencia y extinción.
│   ├── 03-deuda-ontologica.md         ← Capa dos. Contradicción y colapso.
│   └── 04-dinamica-unificada.md       ← Capa tres. El motor. Cero poesía.
│
├── src/
│   └── ronin_dynamics/
│       ├── __init__.py
│       ├── unified_engine.py          ← Ecuación Maestra: Φ × Ψ × Ω × ε
│       ├── discrete_ecology.py        ← DTMC estocástico. Lotka-Volterra está muerto.
│       ├── calibration.py             ← Optimización Bayesiana sobre logs reales
│       ├── benchmark.py               ← ronin-bench: 4 ablaciones reproducibles
│       ├── audit.py                   ← Hoeffding estratificado. n=1060. Garantizado.
│       ├── drift.py                   ← ΔN post-model-update. CI/CD gate.
│       └── tests/                     ← Si un test falla, la teoría está mal. Arréglala.
│
├── notebooks/
│   ├── ablation_a_quadratic_debt.ipynb
│   ├── ablation_b_sandwich.ipynb
│   ├── ablation_c_resilience.ipynb
│   └── ablation_d_model_drift.ipynb
│
├── configs/
│   ├── params_gpt4o.yaml
│   ├── params_claude35.yaml
│   ├── params_llama3_70b.yaml
│   └── params_mistral_large.yaml
│
└── scripts/
    ├── run_full_calibration.py        ← Apéndice C
    ├── run_ablation_suite.py          ← Sección 4 completa
    ├── run_ontological_audit.py       ← Sección 5 con garantías
    └── post_model_update_check.py     ← Apéndice F. Gate de despliegue.
```

---

## Orden de lectura

No leas en el orden que quieras. Hay una razón para el orden.

1. **01-geometria** → Sin esto no entiendes por qué el contexto es un recurso finito con topología.
2. **02-ecologia** → Sin esto no entiendes por qué tus agentes se matan entre sí.
3. **03-deuda** → Sin esto no entiendes por qué tu RAG miente sin que nadie lo haya envenenado.
4. **04-dinamica** → Sin esto los otros tres son PDFs bonitos. Con esto son un sistema.

Si solo tienes una hora: lee el Abstract del 04, la Sección 1.4 (Ecuación Maestra) y el Apéndice G (tablas de parámetros). Luego vuelve y lee el resto. O no. Pero no me vengas con preguntas sobre "por qué mi agente se extinguió" si no has leído el Teorema de Coexistencia-k.

---

## Instalación

```bash
git clone https://github.com/[redacted]/ronin-dynamics.git
cd ronin-dynamics
pip install -e ".[dev]"
```

Python ≥ 3.11. No me preguntes por qué no soporto 3.9. Los type aliases con `Annotated` y el `match` statement no son negociables.

```bash
# Verificar que todo funciona
pytest src/ronin_dynamics/tests/ -v --tb=short
```

Si los tests no pasan en tu máquina, el problema es tu máquina. O tu numpy. O tu conciencia.

---

## Uso rápido

### Simular dinámica de agentes

```python
from ronin_dynamics.unified_engine import UnifiedDynamicsEngine
from ronin_dynamics.discrete_ecology import StochasticEcologySimulator

engine = UnifiedDynamicsEngine(n_agents=5)
result = engine.find_equilibrium(
    attention_profile=phi_matrix,
    importance_weights=w_matrix,
    mean_contradiction_severity=debt_vector
)
print(result['equilibrium'])  # Quién sobrevive. Quién no.
```

### Auditar deuda ontológica con garantía estadística

```python
from ronin_dynamics.audit import GuaranteedOntologicalAuditor

auditor = GuaranteedOntologicalAuditor()
n = auditor.hoeffding_sample_size(epsilon=0.05, delta=0.01)
# n = 1060. No 10.000. No "todos los pares". 1.060.
# Con confianza del 99%. Léete la Sección 5 antes de discutir.
```

### Diagnosticar drift tras actualización de modelo

```python
from ronin_dynamics.drift import ModelDriftDetector

detector = ModelDriftDetector()
diagnosis = detector.diagnose(embeddings_old, embeddings_new)

if diagnosis['level'] == 'CRITICAL':
    # No despliegues. Recalibra primero.
    # El Apéndice F existe por una razón.
    raise SystemExit("DRIFT CRITICAL. Recalibración requerida.")
```

---

## Lo que esto NO es

- No es un framework de agentes tipo LangChain/AutoGen/CrewAI. No construyo pipelines. Construyo ecosistemas.
- No es un wrapper de OpenAI. No hay `import openai` en ninguna parte del código de producción.
- No es un paper académico con "future work" en la conclusión. Todo el código está aquí. Ejecutable. Testeado.
- No es para ti si buscas "5 tips para mejorar tus prompts". Esto es topología, ecología y teoría de la información aplicadas. O estás aquí para eso o estás en el repo equivocado.

---

## Lo que esto SÍ es

La primera formalización matemática completa de:

1. Por qué los LLMs olvidan selectivamente (y cómo diseñar contra ello).
2. Por qué los sistemas multi-agente colapsan sin que ningún agente falle individualmente.
3. Por qué tu base RAG acumula contradicciones que ningún test detecta hasta que es tarde.
4. Cómo unificar los tres problemas en una sola ecuación de estado con parámetros calibrados empíricamente.

Cuatro ablaciones reproducibles. Tablas de parámetros para cuatro modelos. Código de producción. Tests que verifican cada teorema.

---

## Licencia

**CC BY-NC-SA 4.0 + Cláusula Comercial Ronin**

- Uso académico, investigación, aprendizaje: libre con atribución.
- Uso comercial: contactar. La cláusula existe porque alguien tiene que pagar el alquiler mientras escribe estas cosas.
- No, no puedes fork-ear esto, borrar mi nombre y venderlo como tu "framework innovador de agentes". Sí, me enteraré.

---

## Contacto

David Ferrandez Canalis
Agencia RONIN

Para preguntas técnicas: abre un issue. Si la pregunta demuestra que no has leído la Sección relevante, será cerrada sin respuesta.
Para consultas comerciales: DM.
Para decirme que las mates están bien: gracias, ya lo sabía.
Para decirme que las mates están mal: demuestra dónde. Si tienes razón, lo corrijo. Si no, aprende.

---

## Nota final

Este repo tiene 0 estrellas.
No me importa.
La geometría del olvido no depende de la atención que reciba.

Lo que está aquí es correcto.
Lo que está aquí funciona.
Lo que está aquí estará aquí cuando tu pipeline de LangChain haya colapsado por tercera vez y busques una explicación que no sea "sube la temperatura".

Cuando ese día llegue, ya sabes dónde está.

---

1310.
```
