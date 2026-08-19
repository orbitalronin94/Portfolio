# RONIN 1.0 — Reference Runtime

This is the first executable reference implementation of the RONIN 1.0 core.

## Scope

Implemented:

- lexer
- parser for the core `system` declaration
- semantic validation
- normative `fitness`
- normative deterministic `solve`
- `allocation`
- `k_min`
- `Solution`
- stochastic `simulate` with reproducible seed
- CLI: `check`, `solve`, `simulate`

## Important semantic boundary

`solve` is normative:

`F_i = phi_i * psi_i * frequency_i ** alpha`

`A_i = resource * F_i / sum(F)`

The specification defines `simulate` as stochastic but does not uniquely specify a transition kernel. The included simulator therefore declares its kernel explicitly as an implementation-defined reference choice. It must not be mistaken for an additional normative equation of RONIN 1.0.

## Run without installation

```bash
python -m ronin check examples/maquinas.ronin
python -m ronin solve examples/maquinas.ronin
python -m ronin simulate examples/maquinas.ronin --steps 10 --seed 42
```

## Expected solve result for Maquinas

Fitness:

- A = 0.48
- B = 0.20

Allocation:

- A = 70.588235...
- B = 29.411764...

## Development

Run:

```bash
python -m unittest discover -s tests -v
```
