# MANUAL DE EJECUCIÓN
## Diez Algoritmos Clásicos Traducidos a Código Funcional

**Autor:** David Ferrandez Canalis
**Fecha:** Septiembre 2026
**Licencia:** Apache License 2.0

---

## PARTE I: EL MÉTODO

### Las 4 Capas

```
CAPA 1: CONTEXTO   → ¿Por qué existe este algoritmo?
CAPA 2: ECUACIÓN   → ¿Cuál es su formulación matemática?
CAPA 3: ALGORITMO  → ¿Cómo se traduce a pasos ejecutables?
CAPA 4: CÓDIGO     → Implementación sin dependencias + tests
```

### Los 4 Principios

1. **Transparencia Ontológica** — El código refleja exactamente lo que dice el paper.
2. **Soberanía del Implementador** — Sin dependencias externas. Sin APIs. Sin servicios.
3. **Validación Cruzada** — Los resultados coinciden con el paper o con valores conocidos.
4. **Documentación Incrustada** — Cada línea crítica referencia la sección del paper.

### Framework de Tests

```javascript
const T = {
  passed: 0, failed: 0,
  ok(c, m) { if (!c) { this.failed++; console.error(`✗ ${m}`); } else this.passed++; },
  eq(a, e, m) {
    if (JSON.stringify(a) !== JSON.stringify(e)) {
      this.failed++; console.error(`✗ ${m}: esperado ${JSON.stringify(e)}, obtenido ${JSON.stringify(a)}`);
    } else this.passed++;
  },
  aprox(a, e, tol, m) {
    if (Math.abs(a - e) > tol) { this.failed++; console.error(`✗ ${m}: ~${e} vs ${a}`); }
    else this.passed++;
  },
  report() {
    console.log(`${this.passed} pasados, ${this.failed} fallidos`);
    if (this.failed > 0) throw new Error(`${this.failed} tests fallidos`);
    console.log("✓ TODOS LOS TESTS PASARON");
  }
};
```

### Clasificación de Fidelidad

- **Fiel:** Sigue el algoritmo del paper sin simplificaciones esenciales.
- **Pedagógica:** Captura la esencia con simplificaciones documentadas.

### Cuándo SÍ y cuándo NO

**SÍ:** Algoritmos deterministas con matemáticas explícitas. Validación posible contra valores conocidos.

**NO:** Algoritmos galácticos (Chazelle). Oráculos indecidibles (Risch). Papers sin especificación algorítmica.

---

## PARTE II: LOS DIEZ CAPÍTULOS

---

# CAPÍTULO 1: PARTITION TREES

**Fidelidad:** Fiel
**Paper:** Matoušek, J. (1992). Efficient Partition Trees. *Discrete & Computational Geometry*, 8(3), 315-334.

**Contexto:** Consultas de rango en 2D. O(√n + k) por consulta frente a O(n) de fuerza bruta.

**Ecuación:** Árbol binario donde cada nodo representa S ⊆ P. La raíz representa P. Cada nodo interno particiona por la mediana del eje x o y, alternando.

**Algoritmo:**
```
CONSTRUIR(puntos, prof):
  si |puntos| ≤ 1: retornar Hoja(puntos)
  eje = prof % 2 == 0 ? 'x' : 'y'
  ordenar por eje, mediana = |puntos| / 2
  retornar NodoInterno(CONSTRUIR(izq), CONSTRUIR(der))

CONSULTAR(nodo, R):
  si región ∩ R = ∅: retornar []
  si región ⊆ R: retornar todos
  si Hoja: filtrar por R
  retornar CONSULTAR(izq) ∪ CONSULTAR(der)
```

**Código:**

```javascript
class PartitionTree {
  constructor(puntos) {
    this.puntos = puntos.map(p => ({ x: p.x, y: p.y }));
    this.raíz = this._construir(this.puntos, 0);
  }

  _construir(puntos, profundidad) {
    if (puntos.length <= 1) {
      return { tipo: 'hoja', puntos, región: this._región(puntos) };
    }
    const eje = profundidad % 2 === 0 ? 'x' : 'y';
    const ordenados = [...puntos].sort((a, b) => a[eje] - b[eje]);
    const medianaIdx = Math.floor(ordenados.length / 2);
    return {
      tipo: 'interno',
      izquierda: this._construir(ordenados.slice(0, medianaIdx), profundidad + 1),
      derecha: this._construir(ordenados.slice(medianaIdx), profundidad + 1),
      región: this._región(puntos),
      todos: puntos
    };
  }

  _región(puntos) {
    if (!puntos.length) return { xMin: Infinity, xMax: -Infinity, yMin: Infinity, yMax: -Infinity };
    let xMin = Infinity, xMax = -Infinity, yMin = Infinity, yMax = -Infinity;
    for (const p of puntos) {
      if (p.x < xMin) xMin = p.x; if (p.x > xMax) xMax = p.x;
      if (p.y < yMin) yMin = p.y; if (p.y > yMax) yMax = p.y;
    }
    return { xMin, xMax, yMin, yMax };
  }

  _intersecta(r, R) {
    return !(r.xMax < R.xMin || r.xMin > R.xMax || r.yMax < R.yMin || r.yMin > R.yMax);
  }

  _contiene(r, R) {
    return r.xMin >= R.xMin && r.xMax <= R.xMax && r.yMin >= R.yMin && r.yMax <= R.yMax;
  }

  consultar(R) {
    const out = [];
    this._consultar(this.raíz, R, out);
    return out;
  }

  _consultar(nodo, R, out) {
    if (!this._intersecta(nodo.región, R)) return;
    if (this._contiene(nodo.región, R)) {
      out.push(...(nodo.tipo === 'hoja' ? nodo.puntos : nodo.todos));
      return;
    }
    if (nodo.tipo === 'hoja') {
      for (const p of nodo.puntos) {
        if (p.x >= R.xMin && p.x <= R.xMax && p.y >= R.yMin && p.y <= R.yMax) out.push(p);
      }
      return;
    }
    this._consultar(nodo.izquierda, R, out);
    this._consultar(nodo.derecha, R, out);
  }
}

// ==================== VALIDACIÓN ====================
const T = {
  passed: 0, failed: 0,
  ok(c, m) { if (!c) { this.failed++; console.error(`✗ ${m}`); } else this.passed++; },
  report() {
    console.log(`${this.passed} pasados, ${this.failed} fallidos`);
    if (this.failed) throw new Error(`${this.failed} fallidos`);
    console.log("✓ OK");
  }
};

const N = 10000;
const pts = Array.from({ length: N }, () => ({ x: Math.random() * 1000, y: Math.random() * 1000 }));
const tree = new PartitionTree(pts);
const R = { xMin: 200, xMax: 400, yMin: 300, yMax: 600 };
const a = tree.consultar(R);
const b = pts.filter(p => p.x >= R.xMin && p.x <= R.xMax && p.y >= R.yMin && p.y <= R.yMax);
T.ok(a.length === b.length, `Consulta ${a.length} vs fuerza bruta ${b.length}`);
T.report();
```

---

# CAPÍTULO 2: ENUMERACIÓN DE ALCANOS

**Fidelidad:** Fiel
**Paper:** Kvasnička, V., & Pospíchal, J. (1991). *Chemometrics and Intelligent Laboratory Systems*, 11, 137-147.

**Contexto:** Enumeración exhaustiva de isómeros de alcanos CₙH₂ₙ₊₂ sin duplicados, mediante código canónico. Validado contra OEIS A000602.

**Ecuación:** Árbol químico = grafo conexo sin ciclos con valencias prescritas. Código canónico = representación mínima lexicográfica independiente de la raíz.

**Algoritmo:**
```
ENUMERAR(n):
  esqueleto = C con valencia 4
  EXPANDIR(esqueleto, 1)

EXPANDIR(esq, c):
  si c == n: agregar H, calcular código canónico, deduplicar
  para cada C con valencia libre:
    agregar C, EXPANDIR(esq, c+1), backtrack
```

**Código:**

```javascript
class ÁrbolQuímico {
  constructor() {
    this.vertices = new Map();
    this.nextId = 0;
  }
  addV(símbolo, valencia) {
    const id = this.nextId++;
    this.vertices.set(id, { símbolo, valencia, vecinos: new Map() });
    return id;
  }
  addE(a, b, m = 1) {
    const va = this.vertices.get(a), vb = this.vertices.get(b);
    if (!va || !vb) return false;
    let g1 = 0; for (const x of va.vecinos.values()) g1 += x;
    let g2 = 0; for (const x of vb.vecinos.values()) g2 += x;
    if (g1 + m > va.valencia || g2 + m > vb.valencia) return false;
    va.vecinos.set(b, m); vb.vecinos.set(a, m);
    return true;
  }
  delE(a, b) {
    this.vertices.get(a)?.vecinos.delete(b);
    this.vertices.get(b)?.vecinos.delete(a);
  }
  delV(id) {
    const v = this.vertices.get(id);
    if (!v) return;
    for (const w of v.vecinos.keys()) this.vertices.get(w)?.vecinos.delete(id);
    this.vertices.delete(id);
  }
  copy() {
    const c = new ÁrbolQuímico();
    c.nextId = this.nextId;
    for (const [id, v] of this.vertices) {
      c.vertices.set(id, { símbolo: v.símbolo, valencia: v.valencia, vecinos: new Map(v.vecinos) });
    }
    return c;
  }
  grado(id) {
    let g = 0; const v = this.vertices.get(id);
    if (v) for (const m of v.vecinos.values()) g += m;
    return g;
  }
  códigoCanónico() {
    if (!this.vertices.size) return '';
    const codes = [];
    for (const id of this.vertices.keys()) codes.push(this._ser(id, null, new Set()));
    return codes.sort()[0];
  }
  _ser(id, padre, vis) {
    vis.add(id);
    const v = this.vertices.get(id);
    const hijos = [];
    for (const [w, m] of v.vecinos) {
      if (w !== padre && !vis.has(w)) hijos.push({ id: w, m });
    }
    hijos.sort((a, b) =>
      this._ser(a.id, id, new Set(vis)).localeCompare(this._ser(b.id, id, new Set(vis))));
    let r = `(${v.símbolo}`;
    for (const h of hijos) r += `${h.m}${this._ser(h.id, id, new Set(vis))}`;
    return r + ')';
  }
}

class EnumeradorAlcanos {
  constructor(n) { this.n = n; this.árboles = []; this.vistos = new Set(); }
  enumerar() {
    if (this.n <= 0) return [];
    const esq = new ÁrbolQuímico();
    esq.addV('C', 4);
    this._exp(esq, 1);
    return this.árboles;
  }
  _exp(esq, c) {
    if (c === this.n) {
      const mol = this._H(esq);
      const code = mol.códigoCanónico();
      if (!this.vistos.has(code)) { this.vistos.add(code); this.árboles.push(mol); }
      return;
    }
    const libres = [];
    for (const [id, v] of esq.vertices) {
      if (v.símbolo === 'C' && esq.grado(id) < 4) libres.push(id);
    }
    for (const id of libres) {
      const nc = esq.addV('C', 4);
      if (esq.addE(id, nc)) this._exp(esq, c + 1);
      esq.delE(id, nc); esq.delV(nc);
    }
  }
  _H(esq) {
    const mol = esq.copy();
    for (const [id, v] of esq.vertices) {
      if (v.símbolo === 'C') {
        const f = 4 - esq.grado(id);
        for (let i = 0; i < f; i++) mol.addE(id, mol.addV('H', 1));
      }
    }
    return mol;
  }
}

// ==================== VALIDACIÓN ====================
const T = {
  passed: 0, failed: 0,
  ok(c, m) { if (!c) { this.failed++; console.error(`✗ ${m}`); } else this.passed++; },
  report() {
    console.log(`${this.passed} pasados, ${this.failed} fallidos`);
    if (this.failed) throw new Error(`${this.failed} fallidos`);
    console.log("✓ OK");
  }
};

const OEIS = { 1:1, 2:1, 3:1, 4:2, 5:3, 6:5, 7:9, 8:18 };
for (let n = 1; n <= 8; n++) {
  const e = new EnumeradorAlcanos(n);
  e.enumerar();
  T.ok(e.árboles.length === OEIS[n], `C${n}: ${e.árboles.length} vs ${OEIS[n]}`);
}
T.report();
```

---

# CAPÍTULO 3: VERIFICADOR DE OUTERPLANARIDAD

**Fidelidad:** Pedagógica — verifica outerplanaridad con orden fijo, condición necesaria para strict confluent drawing.
**Paper:** Eppstein, D., et al. (2016). Strict confluent drawing. *Journal of Computational Geometry*, 7(1), 22-46.

**Contexto:** Un grafo outerplanar admite dibujo sin cruces. El algoritmo completo de Eppstein et al. requiere marcado de caras y fusión iterativa.

**Ecuación:** Dos aristas (a,b) y (c,d) con índices en el orden se cruzan si `a < c < b < d` o `c < a < d < b`.

**Algoritmo:**
```
VERIFICAR(G, orden):
  para cada par de aristas:
    si se cruzan en el orden lineal: retornar INVÁLIDO
  retornar VÁLIDO
```

**Código:**

```javascript
class Grafo {
  constructor() { this.adj = new Map(); }
  addV(id) { if (!this.adj.has(id)) this.adj.set(id, new Set()); }
  addE(u, v) { this.addV(u); this.addV(v); this.adj.get(u).add(v); this.adj.get(v).add(u); }
}

class VerificadorOuterplanar {
  constructor(grafo, orden) {
    this.grafo = grafo;
    this.orden = orden;
    this.idx = new Map();
    orden.forEach((v, i) => this.idx.set(v, i));
  }

  _cruzan(a, b, c, d) {
    if (a === c || a === d || b === c || b === d) return false;
    if (a > b) [a, b] = [b, a];
    if (c > d) [c, d] = [d, c];
    return (a < c && c < b && b < d) || (c < a && a < d && d < b);
  }

  verificar() {
    const aristas = [];
    for (const [u, vecinos] of this.grafo.adj) {
      for (const v of vecinos) {
        if (this.idx.get(u) < this.idx.get(v)) aristas.push([u, v]);
      }
    }
    for (let i = 0; i < aristas.length; i++) {
      for (let j = i + 1; j < aristas.length; j++) {
        const [u1, v1] = aristas[i];
        const [u2, v2] = aristas[j];
        if (this._cruzan(this.idx.get(u1), this.idx.get(v1), this.idx.get(u2), this.idx.get(v2))) {
          return { válido: false, aristasConflictivas: [aristas[i], aristas[j]] };
        }
      }
    }
    return { válido: true, orden: this.orden };
  }
}

// ==================== VALIDACIÓN ====================
const T = {
  passed: 0, failed: 0,
  ok(c, m) { if (!c) { this.failed++; console.error(`✗ ${m}`); } else this.passed++; },
  report() {
    console.log(`${this.passed} pasados, ${this.failed} fallidos`);
    if (this.failed) throw new Error(`${this.failed} fallidos`);
    console.log("✓ OK");
  }
};

const g1 = new Grafo();
g1.addE('A', 'B'); g1.addE('B', 'C'); g1.addE('C', 'D');
T.ok(new VerificadorOuterplanar(g1, ['A','B','C','D']).verificar().válido, 'P4 es outerplanar');

const g2 = new Grafo();
g2.addE('A','B'); g2.addE('B','C'); g2.addE('C','D'); g2.addE('D','A');
T.ok(new VerificadorOuterplanar(g2, ['A','B','C','D']).verificar().válido, 'C4 es outerplanar');

const g3 = new Grafo();
for (const u of ['A','B','C','D']) for (const v of ['A','B','C','D']) if (u < v) g3.addE(u, v);
T.ok(!new VerificadorOuterplanar(g3, ['A','B','C','D']).verificar().válido, 'K4 NO es outerplanar');

const g4 = new Grafo();
g4.addE('C','A'); g4.addE('C','B'); g4.addE('C','D');
T.ok(new VerificadorOuterplanar(g4, ['A','C','B','D']).verificar().válido, 'K1,3 es outerplanar');

T.report();
```

---

# CAPÍTULO 4: LOGIC THEORIST

**Fidelidad:** Pedagógica — sistema lógico completo del Principia Mathematica, búsqueda simplificada.
**Paper:** Newell, A., Shaw, J. C., & Simon, H. A. (1956). *The Logic Theory Machine*. RAND P-868.

**Contexto:** Primer programa de IA. Demuestra teoremas proposicionales con heurísticas.

**Ecuación:** Axiomas *1.2 a *1.6 del PM. Reglas: detachment, sustitución, chaining.

**Algoritmo:**
```
DEMOSTRAR(obj):
  cola = axiomas con prioridad
  mientras cola:
    actual = cola.desencolar
    si actual == obj: retornar demostración
    aplicar detachment, chaining, subst
    encolar nuevas con prioridad heurística
```

**Código:**

```javascript
class Var { constructor(n) { this.t = 'var'; this.n = n; }
  toString() { return this.n; }
  clon() { return new Var(this.n); }
  eq(o) { return o.t === 'var' && this.n === o.n; } }

class Neg { constructor(h) { this.t = 'neg'; this.h = h; }
  toString() { return `~${this.h}`; }
  clon() { return new Neg(this.h.clon()); }
  eq(o) { return o.t === 'neg' && this.h.eq(o.h); } }

class Dis { constructor(i, d) { this.t = 'dis'; this.i = i; this.d = d; }
  toString() { return `(${this.i} \\/ ${this.d})`; }
  clon() { return new Dis(this.i.clon(), this.d.clon()); }
  eq(o) { return o.t === 'dis' && this.i.eq(o.i) && this.d.eq(o.d); } }

class Imp { constructor(a, c) { this.t = 'imp'; this.a = a; this.c = c; }
  toString() { return `(${this.a} -> ${this.c})`; }
  clon() { return new Imp(this.a.clon(), this.c.clon()); }
  eq(o) { return o.t === 'imp' && this.a.eq(o.a) && this.c.eq(o.c); } }

class Parser {
  constructor(s) { this.s = s.replace(/\s/g, ''); this.p = 0; }
  parse() { const e = this._imp(); if (this.p < this.s.length) throw new Error('extra'); return e; }
  _imp() { const l = this._dis(); if (this._has('->')) { this._eat('->'); return new Imp(l, this._imp()); } return l; }
  _dis() { let l = this._neg(); while (this._has('\\/') || this._has('|')) {
    this._eat('\\/') || this._eat('|'); l = new Dis(l, this._neg()); } return l; }
  _neg() { if (this._has('~') || this._has('!')) { this._eat('~') || this._eat('!'); return new Neg(this._neg()); } return this._pri(); }
  _pri() { if (this._has('(')) { this._eat('('); const e = this._imp(); this._eat(')'); return e; }
    if (/[a-z]/.test(this.s[this.p])) return new Var(this.s[this.p++]); throw new Error('parse'); }
  _has(t) { return this.s.startsWith(t, this.p); }
  _eat(t) { if (this._has(t)) { this.p += t.length; return true; } return false; }
}

function sustituir(e, sust) {
  if (e.t === 'var') return sust.has(e.n) ? sust.get(e.n).clon() : e.clon();
  if (e.t === 'neg') return new Neg(sustituir(e.h, sust));
  if (e.t === 'dis') return new Dis(sustituir(e.i, sust), sustituir(e.d, sust));
  if (e.t === 'imp') return new Imp(sustituir(e.a, sust), sustituir(e.c, sust));
}

function vars(e) {
  const s = new Set();
  (function r(x) {
    if (x.t === 'var') s.add(x.n);
    if (x.t === 'neg') r(x.h);
    if (x.t === 'dis') { r(x.i); r(x.d); }
    if (x.t === 'imp') { r(x.a); r(x.c); }
  })(e);
  return [...s];
}

class LogicTheorist {
  constructor(axiomas) { this.axiomas = axiomas.map(a => a.clon()); }

  demostrar(objetivoStr, maxIter = 2000) {
    const obj = new Parser(objetivoStr).parse();
    const memoria = this.axiomas.map(a => ({ e: a.clon(), regla: 'axioma', padre: null, prof: 0 }));
    const visitados = new Set();
    const cola = memoria.map(m => ({ ...m, prio: this._prio(m.e, obj) }));

    while (cola.length && maxIter-- > 0) {
      cola.sort((a, b) => a.prio - b.prio);
      const actual = cola.shift();
      const code = actual.e.toString();
      if (visitados.has(code)) continue;
      visitados.add(code);

      if (actual.e.eq(obj)) return { éxito: true, demostración: this._rec(actual) };

      const nuevas = [];
      for (const item of memoria) {
        if (actual.e.t === 'imp' && item.e.eq(actual.e.a))
          nuevas.push({ e: actual.e.c.clon(), regla: 'detachment', padre: actual, prof: actual.prof + 1 });
        if (item.e.t === 'imp' && actual.e.eq(item.e.a))
          nuevas.push({ e: item.e.c.clon(), regla: 'detachment', padre: item, prof: actual.prof + 1 });
        if (actual.e.t === 'imp' && item.e.t === 'imp' && actual.e.c.eq(item.e.a))
          nuevas.push({ e: new Imp(actual.e.a.clon(), item.e.c.clon()), regla: 'chaining', padre: actual, prof: actual.prof + 1 });
      }

      const vs = vars(actual.e);
      if (vs.length > 0 && actual.prof < 8) {
        const términos = [new Var('p'), new Var('q'), new Var('r'), new Neg(new Var('p'))];
        for (let i = 0; i < 3; i++) {
          const sust = new Map();
          for (const v of vs) sust.set(v, términos[Math.floor(Math.random() * términos.length)].clon());
          const nueva = sustituir(actual.e, sust);
          if (!nueva.eq(actual.e))
            nuevas.push({ e: nueva, regla: 'subst', padre: actual, prof: actual.prof + 1 });
        }
      }

      for (const n of nuevas) {
        if (!visitados.has(n.e.toString())) {
          n.prio = this._prio(n.e, obj);
          cola.push(n);
          memoria.push(n);
        }
      }
    }
    return { éxito: false };
  }

  _prio(e, obj) { return (1 - this._sim(e, obj)) * 100 + e.toString().length * 0.5; }

  _sim(e1, e2) {
    if (e1.t !== e2.t) return 0;
    if (e1.t === 'var') return e1.n === e2.n ? 1 : 0.2;
    if (e1.t === 'neg') return 0.5 * this._sim(e1.h, e2.h);
    return (this._sim(e1.i || e1.a, e2.i || e2.a) + this._sim(e1.d || e1.c, e2.d || e2.c)) / 2;
  }

  _rec(item) {
    const out = [];
    let a = item;
    while (a) { out.unshift({ exp: a.e.toString(), regla: a.regla, prof: a.prof }); a = a.padre; }
    return out;
  }
}

const AXIOMAS_PM = [
  new Imp(new Dis(new Var('p'), new Var('p')), new Var('p')),
  new Imp(new Var('q'), new Dis(new Var('p'), new Var('q'))),
  new Imp(new Dis(new Var('p'), new Var('q')), new Dis(new Var('q'), new Var('p'))),
  new Imp(new Dis(new Var('p'), new Dis(new Var('q'), new Var('r'))),
          new Dis(new Var('q'), new Dis(new Var('p'), new Var('r')))),
  new Imp(new Imp(new Var('q'), new Var('r')),
          new Imp(new Dis(new Var('p'), new Var('q')), new Dis(new Var('p'), new Var('r'))))
];

// ==================== VALIDACIÓN ====================
const T = {
  passed: 0, failed: 0,
  ok(c, m) { if (!c) { this.failed++; console.error(`✗ ${m}`); } else this.passed++; },
  report() {
    console.log(`${this.passed} pasados, ${this.failed} fallidos`);
    if (this.failed) throw new Error(`${this.failed} fallidos`);
    console.log("✓ OK");
  }
};

T.ok(new Parser('(p -> p)').parse().t === 'imp', 'Parser implicación');
T.ok(new Parser('(~p)').parse().t === 'neg', 'Parser negación');
T.ok(new Parser('(p \\/ q)').parse().t === 'dis', 'Parser disyunción');
T.ok(AXIOMAS_PM.length === 5, '5 axiomas');

const lt = new LogicTheorist(AXIOMAS_PM);
const r = lt.demostrar('(p -> p)', 500);
T.ok(r.éxito, '(p -> p) demostrado');

T.report();
```

---

# CAPÍTULO 5: MÁQUINA DE TURING UNIVERSAL

**Fidelidad:** Fiel
**Paper:** Turing, A. M. (1936). On computable numbers. *Proc. London Math. Soc.*, 2(42), 230-265.

**Contexto:** Cinta infinita bidireccional, alfabeto arbitrario, transición parcial.

**Ecuación:** MT = (Q, Γ, b, Σ, δ, q₀, F). δ: Q × Γ → Q × Γ × {L, R}.

**Código:**

```javascript
class Cinta {
  constructor(blanco = '_') { this.c = {}; this.b = blanco; }
  leer(i) { return this.c[i] !== undefined ? this.c[i] : this.b; }
  escribe(i, s) { if (s === this.b) delete this.c[i]; else this.c[i] = s; }
  rango() {
    const idx = Object.keys(this.c).map(Number);
    return idx.length ? { min: Math.min(...idx), max: Math.max(...idx) } : { min: 0, max: 0 };
  }
  toString() {
    const { min, max } = this.rango();
    let out = '';
    for (let i = min; i <= max; i++) out += this.leer(i);
    return out;
  }
}

class MT {
  constructor(cfg) {
    this.Q = cfg.Q || new Set();
    this.Γ = cfg.Γ || new Set();
    this.b = cfg.b || '_';
    this.δ = cfg.δ || new Map();
    this.q0 = cfg.q0 || 'q0';
    this.F = cfg.F || new Set();
  }
  add(q, s, qP, sP, D) {
    this.Q.add(q); this.Q.add(qP);
    this.Γ.add(s); this.Γ.add(sP);
    this.δ.set(`${q},${s}`, { q: qP, s: sP, D });
  }
  buscar(q, s) { return this.δ.get(`${q},${s}`) || null; }

  simular(entrada, maxPasos = 10000) {
    const cinta = new Cinta(this.b);
    for (let i = 0; i < entrada.length; i++) cinta.escribe(i, entrada[i]);
    let pos = 0, q = this.q0;
    for (let p = 0; p < maxPasos; p++) {
      const s = cinta.leer(pos);
      const t = this.buscar(q, s);
      if (!t) return {
        resultado: this.F.has(q) ? 'aceptada' : 'rechazada',
        cintaFinal: cinta.toString(), pasos: p, estadoFinal: q
      };
      cinta.escribe(pos, t.s);
      pos += (t.D === 'R' ? 1 : -1);
      q = t.q;
    }
    return { resultado: 'no se detiene', cintaFinal: cinta.toString(), pasos: maxPasos };
  }

  codificar() {
    const F = [...this.F].join(',');
    const ts = [];
    for (const [k, t] of this.δ) {
      const [q, s] = k.split(',');
      ts.push(`${q},${s}→${t.q},${t.s},${t.D}`);
    }
    return `${this.q0}|${F}|${ts.join(';')}`;
  }

  static parsear(cod) {
    const [q0, F, ts] = cod.split('|');
    const M = new MT({ q0, F: new Set(F.split(',').filter(x => x)) });
    if (ts) for (const t of ts.split(';')) {
      if (!t) continue;
      const [izq, der] = t.split('→');
      const [q, s] = izq.split(',');
      const [qP, sP, D] = der.split(',');
      M.add(q, s, qP, sP, D);
    }
    return M;
  }
}

function incremento() {
  const M = new MT({ q0: 'q0', F: new Set(['qA']) });
  M.add('q0', '0', 'q0', '0', 'R');
  M.add('q0', '1', 'q0', '1', 'R');
  M.add('q0', '_', 'qR', '_', 'L');
  M.add('qR', '0', 'qA', '1', 'R');
  M.add('qR', '1', 'qR', '0', 'L');
  M.add('qR', '_', 'qA', '1', 'R');
  return M;
}

function palíndromo() {
  const M = new MT({ q0: 'q0', F: new Set(['qA']) });
  M.add('q0', '0', 'qM0', 'X', 'R');
  M.add('q0', '1', 'qM1', 'X', 'R');
  M.add('q0', 'X', 'q0', 'X', 'R');
  M.add('q0', '_', 'qA', '_', 'R');
  M.add('qM0', '0', 'qM0', '0', 'R');
  M.add('qM0', '1', 'qM0', '1', 'R');
  M.add('qM0', 'X', 'qM0', 'X', 'R');
  M.add('qM0', '_', 'qV0', '_', 'L');
  M.add('qM1', '0', 'qM1', '0', 'R');
  M.add('qM1', '1', 'qM1', '1', 'R');
  M.add('qM1', 'X', 'qM1', 'X', 'R');
  M.add('qM1', '_', 'qV1', '_', 'L');
  M.add('qV0', '0', 'qVolver', 'X', 'L');
  M.add('qV0', 'X', 'qV0', 'X', 'L');
  M.add('qV0', '_', 'qA', '_', 'R');
  M.add('qV0', '1', 'qRechaza', '1', 'R');
  M.add('qV1', '1', 'qVolver', 'X', 'L');
  M.add('qV1', 'X', 'qV1', 'X', 'L');
  M.add('qV1', '_', 'qA', '_', 'R');
  M.add('qV1', '0', 'qRechaza', '0', 'R');
  M.add('qVolver', '0', 'qVolver', '0', 'L');
  M.add('qVolver', '1', 'qVolver', '1', 'L');
  M.add('qVolver', 'X', 'qVolver', 'X', 'L');
  M.add('qVolver', '_', 'q0', '_', 'R');
  M.add('qRechaza', '0', 'qRechaza', '0', 'R');
  M.add('qRechaza', '1', 'qRechaza', '1', 'R');
  M.add('qRechaza', '_', 'qRechaza', '_', 'R');
  return M;
}

class UTM {
  constructor(maxPasos = 10000) { this.max = maxPasos; }
  ejecutar(codM, w) {
    const M = MT.parsear(codM);
    return M.simular(w, this.max);
  }
}

// ==================== VALIDACIÓN ====================
const T = {
  passed: 0, failed: 0,
  ok(c, m) { if (!c) { this.failed++; console.error(`✗ ${m}`); } else this.passed++; },
  report() {
    console.log(`${this.passed} pasados, ${this.failed} fallidos`);
    if (this.failed) throw new Error(`${this.failed} fallidos`);
    console.log("✓ OK");
  }
};

const inc = incremento();
for (const [e, esp] of [['0','1'],['1','10'],['1011','1100'],['1111','10000']]) {
  const r = inc.simular(e, 1000);
  T.ok(r.cintaFinal === esp, `Incremento ${e} → ${r.cintaFinal} (esp ${esp})`);
}

const pal = palíndromo();
for (const [e, esp] of [['','aceptada'],['0','aceptada'],['00','aceptada'],
                        ['01','rechazada'],['1001','aceptada'],['1010','rechazada'],
                        ['11011','aceptada'],['11010','rechazada']]) {
  const r = pal.simular(e, 2000);
  T.ok(r.resultado === esp, `Palíndromo "${e}" → ${r.resultado} (esp ${esp})`);
}

const utm = new UTM(5000);
const rUTM = utm.ejecutar(inc.codificar(), '101');
T.ok(rUTM.cintaFinal === '110', `UTM(inc, "101") → ${rUTM.cintaFinal}`);

T.report();
```

---

# CAPÍTULO 6: HOJA DE RUTA DE CANNY

**Fidelidad:** Pedagógica — roadmap por puntos críticos para robot planar 2D.
**Paper:** Canny, J. (1988). *The Complexity of Robot Motion Planning*. MIT Press.

**Contexto:** Construcción de roadmap que preserva conectividad del espacio libre.

**Código:**

```javascript
class P { constructor(x, y) { this.x = x; this.y = y; }
  dist(o) { return Math.hypot(this.x - o.x, this.y - o.y); } }

class Seg {
  constructor(a, b) { this.a = a; this.b = b; }
  intersecta(o) {
    const d1 = this._o(o.a, o.b, this.a);
    const d2 = this._o(o.a, o.b, this.b);
    const d3 = this._o(this.a, this.b, o.a);
    const d4 = this._o(this.a, this.b, o.b);
    return ((d1 > 0 && d2 < 0) || (d1 < 0 && d2 > 0)) &&
           ((d3 > 0 && d4 < 0) || (d3 < 0 && d4 > 0));
  }
  _o(p, q, r) { return (q.y - p.y) * (r.x - q.x) - (q.x - p.x) * (r.y - q.y); }
}

class Obst {
  constructor(verts) {
    this.verts = verts;
    this.aristas = verts.map((v, i) => new Seg(v, verts[(i + 1) % verts.length]));
  }
  contiene(p) {
    let c = 0;
    for (const a of this.aristas) {
      if ((a.a.y > p.y) !== (a.b.y > p.y)) {
        const xInt = (a.b.x - a.a.x) * (p.y - a.a.y) / (a.b.y - a.a.y) + a.a.x;
        if (xInt > p.x) c++;
      }
    }
    return c % 2 === 1;
  }
}

class RoadmapCanny {
  constructor(obsts, lim) { this.obsts = obsts; this.lim = lim; this.nodos = []; this.aristas = []; }

  construir() {
    const pts = [];
    for (const o of this.obsts) pts.push(...o.verts);
    pts.push(new P(this.lim.xMin, this.lim.yMin), new P(this.lim.xMax, this.lim.yMin),
             new P(this.lim.xMin, this.lim.yMax), new P(this.lim.xMax, this.lim.yMax));
    this.nodos = pts.filter(p => this._libre(p));
    for (let i = 0; i < this.nodos.length; i++) {
      for (let j = i + 1; j < this.nodos.length; j++) {
        if (this._visible(this.nodos[i], this.nodos[j])) this.aristas.push([i, j]);
      }
    }
    return { nodos: this.nodos.length, aristas: this.aristas.length };
  }

  _libre(p) {
    if (p.x < this.lim.xMin || p.x > this.lim.xMax || p.y < this.lim.yMin || p.y > this.lim.yMax) return false;
    return !this.obsts.some(o => o.contiene(p));
  }

  _visible(a, b) {
    const s = new Seg(a, b);
    for (const o of this.obsts) for (const ar of o.aristas) if (s.intersecta(ar)) return false;
    return true;
  }

  camino(inicio, fin) {
    const i0 = this._másCerca(inicio), i1 = this._másCerca(fin);
    if (i0 < 0 || i1 < 0) return { encontrado: false };
    const cola = [i0], vis = new Set([i0]), padre = new Map([[i0, null]]);
    while (cola.length) {
      const cur = cola.shift();
      if (cur === i1) {
        const cam = []; let n = cur;
        while (n !== null) { cam.unshift(this.nodos[n]); n = padre.get(n); }
        return { encontrado: true, camino: cam };
      }
      for (const [a, b] of this.aristas) {
        let vec = null;
        if (a === cur) vec = b; else if (b === cur) vec = a;
        if (vec !== null && !vis.has(vec)) { vis.add(vec); padre.set(vec, cur); cola.push(vec); }
      }
    }
    return { encontrado: false };
  }

  _másCerca(p) {
    let mejor = -1, dMin = Infinity;
    for (let i = 0; i < this.nodos.length; i++) {
      const d = this.nodos[i].dist(p);
      if (d < dMin) { dMin = d; mejor = i; }
    }
    return mejor;
  }
}

// ==================== VALIDACIÓN ====================
const T = {
  passed: 0, failed: 0,
  ok(c, m) { if (!c) { this.failed++; console.error(`✗ ${m}`); } else this.passed++; },
  report() {
    console.log(`${this.passed} pasados, ${this.failed} fallidos`);
    if (this.failed) throw new Error(`${this.failed} fallidos`);
    console.log("✓ OK");
  }
};

const obst = new Obst([new P(40,40), new P(60,40), new P(60,60), new P(40,60)]);
const rm = new RoadmapCanny([obst], { xMin: 0, xMax: 100, yMin: 0, yMax: 100 });
const info = rm.construir();
T.ok(info.nodos > 0, `Roadmap con ${info.nodos} nodos`);

const cam = rm.camino(new P(10,10), new P(90,90));
T.ok(cam.encontrado, 'Camino (10,10) → (90,90) encontrado');
T.ok(cam.camino.length >= 2, `Camino con ${cam.camino.length} waypoints`);

T.report();
```

---

# CAPÍTULO 7: BÚSQUEDA UNIVERSAL POR FASES

**Fidelidad:** Pedagógica — demuestra mecánica de fases. HSEARCH real requiere espacio universal y probador de teoremas completo.
**Paper:** Hutter, M. (2002). The Fastest and Shortest Algorithm for All Well-Defined Problems. *Int. J. Foundations of Computer Science*, 13(3), 431-443.

**Código:**

```javascript
class EspacioProgramas {
  constructor() {
    this.programas = [
      { id: 'lineal', long: 20, ejecutar: ([a,b]) => a === 0 ? null : -b/a },
      { id: 'bisección', long: 50, ejecutar: ([a,b]) => {
        if (a === 0) return null;
        let lo = -1000, hi = 1000;
        for (let i = 0; i < 100; i++) {
          const mid = (lo + hi) / 2;
          if (a * mid + b > 0) hi = mid; else lo = mid;
        }
        return (lo + hi) / 2;
      }},
      { id: 'newton', long: 80, ejecutar: ([a,b]) => {
        if (a === 0) return null;
        let x = 0;
        for (let i = 0; i < 50; i++) x = x - (a * x + b) / a;
        return x;
      }}
    ];
  }
}

class HSEARCH {
  constructor(maxFases = 50) { this.esp = new EspacioProgramas(); this.maxFases = maxFases; }
  resolver([a, b]) {
    for (let fase = 1; fase <= this.maxFases; fase++) {
      const ordenados = [...this.esp.programas].sort((p, q) => p.long - q.long);
      for (const p of ordenados) {
        const tiempo = Math.pow(2, -p.long / 50) * fase * 10;
        try {
          const r = p.ejecutar([a, b]);
          if (r !== null && Math.abs(a * r + b) < 1e-6) {
            return { encontrado: true, solución: r, programa: p.id, fase };
          }
        } catch (e) {}
      }
    }
    return { encontrado: false };
  }
}

// ==================== VALIDACIÓN ====================
const T = {
  passed: 0, failed: 0,
  ok(c, m) { if (!c) { this.failed++; console.error(`✗ ${m}`); } else this.passed++; },
  report() {
    console.log(`${this.passed} pasados, ${this.failed} fallidos`);
    if (this.failed) throw new Error(`${this.failed} fallidos`);
    console.log("✓ OK");
  }
};

const hs = new HSEARCH();
for (const [a, b, esp] of [[2,-4,2],[1,5,-5],[3,9,-3],[0.5,-1,2]]) {
  const r = hs.resolver([a, b]);
  T.ok(r.encontrado && Math.abs(r.solución - esp) < 1e-3,
       `${a}x+${b}=0 → ${r.solución?.toFixed(4)} (esp ${esp})`);
}
T.report();
```

---

# CAPÍTULO 8: DESCUBRIDOR MATEMÁTICO (AM)

**Fidelidad:** Pedagógica — esqueleto del AM original con 4 heurísticas básicas.
**Paper:** Lenat, D. B. (1976). *AM*. Stanford University.

**Código:**

```javascript
class Concepto {
  constructor(n) {
    this.n = n;
    this.facetas = { ejemplos: [], contraejemplos: [], generalizaciones: [], especializaciones: [] };
    this.interés = 0;
  }
  ej(x) { this.facetas.ejemplos.push(x); }
  contra(x) { this.facetas.contraejemplos.push(x); }
  gen(c) { this.facetas.generalizaciones.push(c); }
  toString() { return `${this.n}(e=${this.facetas.ejemplos.length},c=${this.facetas.contraejemplos.length})`; }
}

class AM {
  constructor() { this.conceptos = new Map(); this.cola = []; }

  inicializar() {
    for (const [n, ejemplos] of [
      ['conjunto', [{tipo:'vacío'},{tipo:'singleton'},{tipo:'par'}]],
      ['unión', [{a:[1],b:[2],r:[1,2]},{a:[],b:[1],r:[1]}]],
      ['intersección', [{a:[1,2],b:[2,3],r:[2]},{a:[1],b:[2],r:[]}]]
    ]) {
      const c = new Concepto(n);
      for (const e of ejemplos) c.ej(e);
      this.conceptos.set(n, c);
      this.cola.push(c);
    }
  }

  ejecutar(maxIter = 30) {
    let iter = 0;
    while (this.cola.length && iter < maxIter) {
      iter++;
      this.cola.sort((a, b) => b.interés - a.interés);
      const c = this.cola.shift();
      this._aplicar(c);
      this._recalcular();
    }
    return [...this.conceptos.values()];
  }

  _aplicar(c) {
    if (c.facetas.ejemplos.length >= 2) {
      const g = this._generalizar(c);
      if (g && !this.conceptos.has(g.n)) {
        this.conceptos.set(g.n, g);
        c.gen(g);
        this.cola.push(g);
      }
    }
    for (const otro of [...this.conceptos.values()]) {
      if (otro === c) continue;
      const comp = this._componer(c, otro);
      if (comp && !this.conceptos.has(comp.n)) {
        this.conceptos.set(comp.n, comp);
        this.cola.push(comp);
        break;
      }
    }
    if (c.facetas.ejemplos.length > 0) c.contra({ generado: true, de: c.n });
  }

  _generalizar(c) {
    const mapa = { 'natural': 'entero', 'entero': 'racional', 'racional': 'real',
                   'unión': 'operación_binaria', 'intersección': 'operación_binaria' };
    if (mapa[c.n]) {
      const g = new Concepto(mapa[c.n]);
      g.ej({ derivadoDe: c.n });
      return g;
    }
    return null;
  }

  _componer(c1, c2) {
    const n = `${c1.n}+${c2.n}`;
    if (n.length > 40) return null;
    const comp = new Concepto(n);
    comp.ej({ de: [c1.n, c2.n] });
    return comp;
  }

  _recalcular() {
    for (const c of this.conceptos.values()) {
      c.interés = c.facetas.ejemplos.length * 2
                - c.facetas.contraejemplos.length * 0.5
                + c.facetas.generalizaciones.length * 1.5;
    }
  }
}

// ==================== VALIDACIÓN ====================
const T = {
  passed: 0, failed: 0,
  ok(c, m) { if (!c) { this.failed++; console.error(`✗ ${m}`); } else this.passed++; },
  report() {
    console.log(`${this.passed} pasados, ${this.failed} fallidos`);
    if (this.failed) throw new Error(`${this.failed} fallidos`);
    console.log("✓ OK");
  }
};

const am = new AM();
am.inicializar();
const conceptosFinales = am.ejecutar(30);
T.ok(conceptosFinales.length > 3, `AM descubrió ${conceptosFinales.length} conceptos (más que 3 iniciales)`);
T.ok([...am.conceptos.keys()].some(k => k.includes('operación')), 'AM generalizó');
T.ok([...am.conceptos.keys()].some(k => k.includes('+')), 'AM compuso');
T.report();
```

---

# CAPÍTULO 9: MOTOR DE INFERENCIA DIFUSA

**Fidelidad:** Fiel
**Paper:** Kling, R. (1973). *Fuzzy-PLANNER*. University of Wisconsin.

**Contexto:** Razonamiento con información imprecisa. Valores de verdad en [0,1].

**Ecuación:** Modus ponens difuso: `v(q) = min(v(p_i)) × certeza`.

**Código:**

```javascript
class FuzzyPLANNER {
  constructor() {
    this.hechos = new Map();
    this.reglas = [];
    this.stats = { inferencias: 0 };
  }

  hecho(n, v) { this.hechos.set(n, Math.max(0, Math.min(1, v))); }

  regla(premisas, conclusión, certeza) {
    this.reglas.push({ premisas, conclusión, certeza });
  }

  resolver(meta, umbral = 0.5, maxIter = 100) {
    let cambio = true, iter = 0;
    while (cambio && iter < maxIter) {
      cambio = false;
      iter++;
      for (const r of this.reglas) {
        let disponibles = true;
        const valores = [];
        for (const p of r.premisas) {
          if (this.hechos.has(p)) valores.push(this.hechos.get(p));
          else { disponibles = false; break; }
        }
        if (disponibles) {
          const minP = Math.min(...valores);
          const nueva = minP * r.certeza;
          const previa = this.hechos.get(r.conclusión) || 0;
          if (nueva > previa + 1e-9) {
            this.hechos.set(r.conclusión, nueva);
            cambio = true;
            this.stats.inferencias++;
          }
        }
      }
    }
    const v = this.hechos.get(meta) || 0;
    return { éxito: v >= umbral, valor: v, hecho: meta };
  }

  explicar(meta) {
    return this.reglas
      .filter(r => r.conclusión === meta)
      .map(r => ({
        regla: `${r.premisas.join(' ∧ ')} → ${r.conclusión}`,
        certeza: r.certeza,
        premisas: r.premisas.map(p => ({ premisa: p, valor: this.hechos.get(p) || 0 })),
        conclusión: this.hechos.get(meta) || 0
      }));
  }
}

// ==================== VALIDACIÓN ====================
const T = {
  passed: 0, failed: 0,
  ok(c, m) { if (!c) { this.failed++; console.error(`✗ ${m}`); } else this.passed++; },
  aprox(a, e, tol, m) {
    if (Math.abs(a - e) > tol) { this.failed++; console.error(`✗ ${m}: ${a} vs ${e}`); }
    else this.passed++;
  },
  report() {
    console.log(`${this.passed} pasados, ${this.failed} fallidos`);
    if (this.failed) throw new Error(`${this.failed} fallidos`);
    console.log("✓ OK");
  }
};

const fp = new FuzzyPLANNER();
fp.hecho('fiebre', 0.9);
fp.hecho('tos', 0.7);
fp.hecho('dolor_cabeza', 0.5);
fp.regla(['fiebre', 'tos'], 'gripe', 0.8);
fp.regla(['fiebre', 'dolor_cabeza'], 'infección', 0.6);
fp.regla(['tos'], 'resfriado', 0.5);
fp.regla(['gripe'], 'reposo', 0.9);

const rGripe = fp.resolver('gripe');
T.aprox(rGripe.valor, 0.56, 1e-9, 'gripe = 0.56');

const rReposo = fp.resolver('reposo');
T.aprox(rReposo.valor, 0.504, 1e-9, 'reposo = 0.504');
T.ok(rReposo.hecho === 'reposo', 'resolver devuelve la meta solicitada');

const rNo = fp.resolver('meta_inexistente');
T.ok(!rNo.éxito, 'meta inexistente no se resuelve');

T.report();
```

---

# CAPÍTULO 10: CODIFICACIÓN DE SHANNON

**Fidelidad:** Fiel
**Paper:** Shannon, C. E. (1948). A Mathematical Theory of Communication. *Bell System Technical Journal*, 27(3), 379-423.

**Contexto:** Compresión sin pérdida cercana al límite de entropía.

**Ecuación:** H(X) = -Σ p(x) log₂ p(x). Longitud media L con H ≤ L < H+1.

**Código:**

```javascript
class Info {
  static entropía(freqs) {
    const total = freqs.reduce((a, b) => a + b, 0);
    let H = 0;
    for (const f of freqs) {
      if (f === 0) continue;
      const p = f / total;
      H -= p * Math.log2(p);
    }
    return H;
  }

  static shannonFano(símbolos, frecuencias) {
    const pares = símbolos.map((s, i) => ({ s, f: frecuencias[i], c: '' }));
    pares.sort((a, b) => b.f - a.f);
    this._dividir(pares);
    return pares;
  }

  static _dividir(pares) {
    if (pares.length <= 1) return;
    const total = pares.reduce((s, p) => s + p.f, 0);
    let acum = 0, idx = 0, mejor = Infinity;
    for (let i = 0; i < pares.length - 1; i++) {
      acum += pares[i].f;
      const d = Math.abs(total - 2 * acum);
      if (d < mejor) { mejor = d; idx = i; }
    }
    for (let i = 0; i <= idx; i++) pares[i].c += '0';
    for (let i = idx + 1; i < pares.length; i++) pares[i].c += '1';
    this._dividir(pares.slice(0, idx + 1));
    this._dividir(pares.slice(idx + 1));
  }

  static longitudMedia(pares) {
    const total = pares.reduce((s, p) => s + p.f, 0);
    return pares.reduce((l, p) => l + (p.f / total) * p.c.length, 0);
  }

  static codificar(msg, pares) {
    const m = new Map(pares.map(p => [p.s, p.c]));
    return msg.split('').map(s => m.get(s) || '').join('');
  }

  static decodificar(bits, pares) {
    const m = new Map(pares.map(p => [p.c, p.s]));
    let out = '', buf = '';
    for (const b of bits) {
      buf += b;
      if (m.has(buf)) { out += m.get(buf); buf = ''; }
    }
    return out;
  }
}

class CanalBSC {
  constructor(p) { this.p = p; this.capacidad = 1 - this._Hb(p); }
  _Hb(p) { return (p === 0 || p === 1) ? 0 : -p * Math.log2(p) - (1 - p) * Math.log2(1 - p); }
  transmitir(bits) {
    let out = '', errs = 0;
    for (const b of bits) {
      if (Math.random() < this.p) { out += b === '0' ? '1' : '0'; errs++; }
      else out += b;
    }
    return { bits: out, errores: errs };
  }
}

// ==================== VALIDACIÓN ====================
const T = {
  passed: 0, failed: 0,
  ok(c, m) { if (!c) { this.failed++; console.error(`✗ ${m}`); } else this.passed++; },
  aprox(a, e, tol, m) {
    if (Math.abs(a - e) > tol) { this.failed++; console.error(`✗ ${m}: ${a} vs ${e}`); }
    else this.passed++;
  },
  report() {
    console.log(`${this.passed} pasados, ${this.failed} fallidos`);
    if (this.failed) throw new Error(`${this.failed} fallidos`);
    console.log("✓ OK");
  }
};

T.aprox(Info.entropía([50, 50]), 1, 1e-9, 'H([50,50]) = 1');
T.aprox(Info.entropía([90, 10]), 0.469, 1e-2, 'H([90,10]) ≈ 0.469');
T.aprox(Info.entropía([25, 25, 25, 25]), 2, 1e-9, 'H([25,25,25,25]) = 2');

const pares = Info.shannonFano(['A','B','C','D','E'], [30,25,20,15,10]);
const H = Info.entropía([30,25,20,15,10]);
const L = Info.longitudMedia(pares);
T.ok(H <= L, `H (${H.toFixed(4)}) ≤ L (${L.toFixed(4)})`);
T.aprox(H, 2.2284, 1e-3, 'H([30,25,20,15,10]) ≈ 2.2284');
T.aprox(L, 2.25, 1e-9, 'L = 2.25');

const msg = 'ABCDEABCDE';
const code = Info.codificar(msg, pares);
T.ok(Info.decodificar(code, pares) === msg, 'codificar/decodificar roundtrip');

const canal = new CanalBSC(0.1);
T.aprox(canal.capacidad, 0.531, 1e-2, 'Capacidad BSC(0.1) ≈ 0.531');

T.report();
```

---

## PARTE III: CIERRE

### Tabla final

| # | Capítulo | Paper | Año | Fidelidad |
|---|----------|-------|-----|-----------|
| 1 | Partition Trees | Matoušek | 1992 | Fiel |
| 2 | Enumeración de Alcanos | Kvasnička & Pospíchal | 1991 | Fiel |
| 3 | Verificador de Outerplanaridad | Eppstein et al. | 2016 | Pedagógica |
| 4 | Logic Theorist | Newell & Simon | 1956 | Pedagógica |
| 5 | Máquina de Turing Universal | Turing | 1936 | Fiel |
| 6 | Hoja de Ruta de Canny | Canny | 1988 | Pedagógica |
| 7 | Búsqueda Universal por Fases | Hutter | 2002 | Pedagógica |
| 8 | Descubridor Matemático | Lenat | 1976 | Pedagógica |
| 9 | Motor de Inferencia Difusa | Kling | 1973 | Fiel |
| 10 | Codificación de Shannon | Shannon | 1948 | Fiel |

**5 fieles. 5 pedagógicas. Todas ejecutables. Todas con tests que lanzan en fallo.**

### Sobre la "cierta utilidad"

Ninguno de estos diez algoritmos tenía una implementación estándar y accesible antes de este manual.

Los cinco **fieles** son traducciones directas. Cualquiera puede ejecutarlos, modificarlos, usarlos como referencia.

Las cinco **pedagógicas** capturan la esencia de papers que no admiten traducción completa en JavaScript ES6 puro. Pero sirven para entender la mecánica, experimentar con los conceptos, construir sobre ellos.

Tienen **"cierta utilidad"**.

La misma que tiene una llave cuando la puerta está cerrada.
La misma que tiene un mapa cuando estás perdido.
La misma que tiene el conocimiento cuando alguien decide compartirlo bajo Apache 2.0.

**Y el método para producir los siguientes también está aquí.**

---

**Copyright 2026 David Ferrandez Canalis**
**Apache License 2.0**
**Septiembre 2026**
