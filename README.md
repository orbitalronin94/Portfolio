```markdown
# .

---

## Antes de leer

Esto no es un framework. No es una librería. No es un curso.
No hay `npm install`. No hay `pip install`. No hay quickstart.

Lo que hay aquí tardó tres años en existir.
No porque fuera difícil de escribir.
Sino porque nadie lo había pensado antes.

Si buscas cinco tips para mejorar tus prompts, cierra la pestaña.
Si buscas entender por qué tu sistema de agentes colapsa a las 3 AM sin que ningún componente haya fallado, sigue leyendo.

---

## Condiciones de entrada

Esto no está optimizado para ser entendido rápido.
Está optimizado para ser entendido bien.

La estructura no es arbitraria. El orden no es sugerencia.
Hay una razón por la que las cosas están donde están y se llaman como se llaman.
Si reordenas, pierdes el argumento. Si saltas, pierdes la demostración.

No hay glosario. Los términos se definen donde se necesitan.
Si un término aparece y no lo entiendes, es porque no has leído lo anterior.
Vuelve. No hay atajo.

---

## Sobre el estado de esto

Esto está terminado. No está "en desarrollo". No hay roadmap público.
Las ecuaciones están cerradas. Los tests pasan. Los parámetros están calibrados.

Si encuentras un error, no es un error de concepto.
Es un error de implementación. Repórtalo con la sección exacta y el test que falla.
Si no puedes señalar el test, no es un error. Es que no lo entendiste.

---

## Para quién NO es esto

No es para quien quiere que le resuelvan el problema.
No es para quien quiere copiar y pegar sin entender.
No es para quien mide el valor de un trabajo por el número de estrellas que tiene.
No es para quien necesita que alguien le explique por qué es importante.

Si necesitas que te convenzan de leer algo, no estás listo para leerlo.

---

## Para quién ES esto

Para quien tiene un sistema multi-agente en producción y no entiende por qué degrada.
Para quien tiene un RAG que responde cosas diferentes a la misma pregunta y no hay ningún error en los logs.
Para quien ha intentado escalar de 3 a 15 agentes y el sistema se comporta como si tuviera voluntad propia.
Para quien sospecha que hay una geometría debajo del caos y quiere verla.

Esto es para ti si ya intentaste todo lo obvio y nada funcionó.

---

## Licencia

CC BY-NC-SA 4.0 + Cláusula Comercial Ronin.

Puedes leerlo. Puedes aprender de él. Puedes usarlo para diagnosticar tus sistemas.
Puedes citarlo con atribución.

No puedes venderlo como tuyo.
No puedes usarlo comercialmente sin autorización.
No puedes fork-earlo y borrar el nombre.

Si lo usas y te salva de un colapso en producción, no me debes nada.
Si lo usas y construyes algo que funciona, eso es suficiente.

---

## Contacto

No hay soporte. No hay consultoría gratuita. No hay "¿puedo hacerte una pregunta rápida?"

Si hay un error técnico demostrable: issue.
Si hay una consulta comercial: DM.
Si hay silencio tras leer esto: eso también es una respuesta válida.

---

## Nota del autor

Esto existe porque tenía que existir.
No porque alguien lo pidiera. No porque hubiera mercado para ello.
No porque fuera rentable escribirlo.

Existe porque los sistemas que estamos construyendo son más complejos que las metáforas que usamos para describirlos. Y alguien tenía que escribir las ecuaciones en lugar de las metáforas.

Si llegaste hasta aquí y no entendiste nada, cierra la pestaña sin culpa.
No es para todos. Nunca fue para todos.

Si llegaste hasta aquí y algo resonó, entonces ya sabes qué hacer.

---

1310.

---

*Última actualización: agosto 2026.*
*Versión del tratado: 1.0*
*Estado: Completo. Operativo. Sin deuda.*
```
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
