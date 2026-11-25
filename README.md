# A stretched-exponential lower bound for syntactically multilinear circuits

> **All contents of this repository are AI generated.** The writeup, its
> proofs, and this README were produced by AI models. Nothing here has been
> peer reviewed.

The writeup is [multilinear-circuit-lower-bound.tex](multilinear-circuit-lower-bound.tex).

## The function

Let `d ≥ 4` be even, `k = d/2`, and `N = d² + d + 1`. The inputs are a bit
`b`, a vector `x ∈ {0,1}^d`, and a matrix `Y ∈ {0,1}^{d×d}`. Write `I(x)`
for the set of positions where `x` is 1.

- If `b = 0`, then `f_d(b, x, Y) = 1` exactly when `Y` is the permutation
  matrix of a single `d`-cycle.
- If `b = 1` and `|I(x)| = k`, then `f_d(b, x, Y)` is the determinant over
  `F_2` of the first `k` rows of `Y` restricted to the columns in `I(x)`.
- If `b = 1` and `|I(x)| ≠ k`, then `f_d(b, x, Y) = 0`.

`f_d` is computable in polynomial time. `P_d` denotes its unique multilinear
representative over `F_2`, viewed over any field of characteristic two.

## Main result

**Theorem 1 (arithmetic lower bound).** There is a `δ > 0` such that for all
sufficiently large even `d` and every field `F` of characteristic two, any
syntactically multilinear arithmetic circuit over `F` computing `P_d` has at
least `2^{N^δ}` wires.

The bound allows arbitrary depth and shared gates. A circuit is
syntactically multilinear if the two inputs of every multiplication gate
depend on disjoint sets of variables.

## Corollaries

**Corollary 2 (deterministic decomposable circuits).** Every d-D computing
`f_d` requires `2^{N^{Ω(1)}}` wires, allowing arbitrary fan-out and
negations at any gate.

**Corollary 3 (read-once parity branching programs).** Every syntactic
read-once parity branching program computing `f_d` requires `2^{N^{Ω(1)}}`
edges, allowing each path its own query order.

Both follow from Theorem 1, because each model computes `P_d` as a
syntactically multilinear circuit with linear overhead.

## Prior work

**Before the [OpenAI papers](https://github.com/openai/math/blob/main/CONTENTS.md).** The best lower bounds for these models were
polynomial.

- Syntactically multilinear circuits: `Ω(n²/log² n)` by Alon, Kumar and
  Volk, improving the `Ω(n^{4/3}/log² n)` of Raz, Shpilka and Yehudayoff.
- Read-once parity branching programs: `Ω(n²/log² n)` by Volk (2026),
  improving `Ω(n^{3/2}/log n)`. Exponential bounds were an open problem.

**The OpenAI bounds.** *Circuit lower bounds for Hamiltonian cycle and the
permanent* treats general arithmetic circuits, which include the
syntactically multilinear ones.

- Its Theorem 1.1 shows that the Hamiltonian cycle polynomial of order `N`
  needs `exp(c (log N)² / (log log N)²)` gates over every field, and the
  same for the permanent outside characteristic two.
- Its Theorem 12.2 improves this to `2^{N^ε}` over fields whose
  characteristic "admits ports". Which characteristics do is not known.

The result here raises the unconditional quasi-polynomial bound to
`2^{N^δ}` in characteristic two, for the three restricted models above.

## Building

```bash
tectonic multilinear-circuit-lower-bound.tex
```

Any standard LaTeX engine also works; the file uses only `amsmath`,
`amssymb`, `amsthm`, `geometry`, `xcolor` and `hyperref`.

## References

- OpenAI. *Circuit lower bounds for Hamiltonian cycle and the permanent*.
  November 24, 2026 edition.
  <https://github.com/openai/math/tree/main/preprints/Circuit-lower-bounds-for-Hamiltonian-cycle-and-the-permanent-November-24-2026>
- M. Monet and D. Olteanu. *Towards deterministic decomposable circuits for
  safe queries*. AMW, 2018.
- N. Alon, M. Kumar and B. L. Volk. *Unbalancing sets and an almost
  quadratic lower bound for syntactically multilinear arithmetic circuits*.
  Combinatorica, 2020. <https://arxiv.org/abs/1708.02037>
- B. L. Volk. *A lower bound for read-once parity branching programs*. 2026.
  <https://arxiv.org/abs/2607.05944>
