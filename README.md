# An exponential lower bound for syntactically multilinear circuits

> **All contents of this repository are AI generated.** The writeup, its
> proofs, and this README were produced by AI models. Nothing here has been
> peer reviewed.

The writeup is [multilinear-circuit-lower-bound.tex](multilinear-circuit-lower-bound.tex).
It first proves a lower bound in characteristic two, with consequences
for two Boolean models, and then a lower bound in every characteristic,
including zero.

## Characteristic two

Let `n ≥ 4` be even, `k = n/2`, and `N = n² + n + 1`. The inputs are a
selector bit `ζ`, a vector `x ∈ {0,1}^n`, and a matrix `Y ∈ {0,1}^{n×n}`.
Write `I(x)` for the set of positions where `x` is 1.

- If `ζ = 0`, then `f_n(ζ, x, Y) = 1` exactly when `Y` is the permutation
  matrix of a single `n`-cycle.
- If `ζ = 1` and `|I(x)| = k`, then `f_n(ζ, x, Y)` is the determinant over
  `F_2` of the first `k` rows of `Y` restricted to the columns in `I(x)`.
- If `ζ = 1` and `|I(x)| ≠ k`, then `f_n(ζ, x, Y) = 0`.

`f_n` is computable in polynomial time. `F_n` denotes its unique
multilinear representative over `F_2`, viewed over any field of
characteristic two.

A circuit is syntactically multilinear if the two inputs of every
multiplication gate depend on disjoint sets of variables. Depth and
fan-out are unrestricted, and size is the number of wires.

**Theorem 1 (characteristic two).** There is a `δ > 0` such that for all
sufficiently large even `n` and every field of characteristic two, any
syntactically multilinear circuit computing `F_n` has at least `2^{N^δ}`
wires. If characteristic two does not admit ports, the main proof gives
`log s = Ω(N^{1/6})`. Appendix A sharpens this to
`log s = Ω(N^{1/4} / (log N)^{5/4})`.

**Corollary 2 (deterministic decomposable circuits).** Every d-D
computing `f_n` requires `2^{N^{Ω(1)}}` wires, allowing arbitrary fan-out
and negations at any gate.

**Corollary 3 (read-once parity branching programs).** Every syntactic
read-once parity branching program computing `f_n` requires
`2^{N^{Ω(1)}}` edges, allowing each path its own query order.

Both corollaries follow from Theorem 1, because each model computes `F_n`
as a syntactically multilinear circuit with linear overhead. The same
form of bound holds for the number of gates of a d-D and the number of
vertices of a read-once parity branching program, and at every
sufficiently large input length.

**Upper bound.** `f_n` has a read-once parity branching program with
`2^n n^{O(1)}` edges, and hence a syntactically multilinear circuit over
characteristic two with `2^{O(√N)}` wires. So the exponent `δ` in
Theorem 1 is at most `1/2`.

## All characteristics

The second function does not involve a field. Let `D(x, Y)` be the
integer determinant of the first `k` rows of `Y` restricted to the
columns in `I(x)` if `|I(x)| = k`, and `0` otherwise. Since `|D| ≤ k!`,
the integer `D` has a two's-complement representation with
`r = 1 + ⌈log₂(k! + 1)⌉` digits. The function `f*_n` has one more input,
a digit index `j` in binary.

- If `ζ = 0`, then `f*_n = 1` exactly when `Y` is the permutation matrix
  of a single `n`-cycle.
- If `ζ = 1` and `j < r`, then `f*_n` is digit `j` of `D(x, Y)` in two's
  complement.
- If `ζ = 1` and `j ≥ r`, then `f*_n = 0`.

It has `N = n² + n + 1 + ⌈log₂ r⌉` inputs and is computable in polynomial
time. `F*_n` denotes its multilinear representative, which has integer
coefficients and is read in any field. At digit index `j = 0` the
function is `f_n`, so Theorem 1 and its corollaries hold for `f*_n` too.
The definition of `f*_n` involves neither a characteristic nor any
constant from the proof.

**Theorem 4 (all characteristics).** For every characteristic `χ`, zero
or a prime, there is a `δ_χ > 0` such that for all large even `n` and
every field of characteristic `χ`, any syntactically multilinear circuit
computing `F*_n` has at least `2^{N^{δ_χ}}` wires. If `χ` does not admit
ports, `log s = Ω(N^{α/(6+3α)})` for an absolute constant `α > 0`.

**Corollary 5 (read-once algebraic branching programs).** The same form
of bound holds for syntactic read-once algebraic branching programs over
any field that agree with `f*_n` on the Boolean cube, even when each
path reads the variables in its own order. This covers mod-`p`
path-counting programs whose path count equals the Boolean output. It
does not cover semantic read-once programs, or programs that accept when
the path count is merely nonzero.

**Corollary 6 (probabilistic circuits with negative weights).** Every
decomposable probabilistic circuit over the reals, with weights of either
sign, that computes a nonzero multiple of `f*_n` on the Boolean cube (for
instance the uniform distribution on its accepted inputs) has at least
`2^{N^δ}` edges. Such a circuit is a syntactically multilinear circuit
over the reals, so this uses Theorem 4 in characteristic zero; Theorem 1
does not apply, because real weights cannot be reduced modulo two.

**Corollary 7 (single-cycle predicate).** For every characteristic `χ`
there is a `γ_χ > 0` such that, for all sufficiently large `m`, the
multilinear representative of “`Y` is the permutation matrix of a single
`m`-cycle” requires at least `2^{(m²)^{γ_χ}}` wires in any syntactically
multilinear circuit over a field of that characteristic. The proof
extracts the Hamiltonian-cycle polynomial and projects it to `F*_n`.
Each surviving variable labels one arc, so the projection preserves
syntactic multilinearity. The polynomial increase in matrix order
accounts for the smaller exponent.

Multilinear formulas and syntactically multilinear algebraic branching
programs are special cases of syntactically multilinear circuits, so
both theorems apply to them. Before the OpenAI paper, exponential lower
bounds were not known even for these: the best were `n^{Ω(log n)}` for
multilinear formulas (Raz) and the `Ω(n²/log² n)` circuit bound for
branching programs.

## How the results relate to the general circuit bound

"Admits ports" is a spectral property of a characteristic defined in the
OpenAI paper *Circuit lower bounds for Hamiltonian cycle and the
permanent*; which characteristics have it is not known.

That paper's Theorem 1.1 gives a quasi-polynomial lower bound for every
arithmetic circuit whose degree-`n` part is the Hamiltonian-cycle
polynomial. Setting `ζ = 0` exposes that polynomial, so the
quasi-polynomial bound already applies to all the models above. The
contribution here is the improvement to `2^{N^δ}`. When the
characteristic admits ports, this improvement already follows from
Theorem 12.2 of that paper. The arguments here handle the case without
ports, where syntactic multilinearity replaces the low-rank cut summands
of that paper by exact products.

## How the proofs go

Both proofs compare two estimates of the *price* of a table of maximal
minors of a matrix `C`. Prices are assigned to tensors whose legs sit at
sites of a metric space. The *star budget* is the cost of supplying all
legs from the tip of a cone, and it bounds the price of every tensor on
the given sites.

**Characteristic two.**

1. **Cuts (Lemma 9).** The circuit determines a list of at most `s + 1`
   balanced cuts of the bits `x`, and every minor table is a sum of
   products, one across each listed cut.
2. **Lower price (Lemma 11).** With one bit per site and independent biases
   sampled from a finite midpoint grid, some minor table has price within
   `O((log n)²)` of the star budget.
3. **Upper price (Proposition 12).** If `log(2L) ≤ n^{1/3}`, Hoeffding's
   inequality gives biases that work for all `L` cuts at once. At the
   placement from the binary lamp certificate, moving the suppliers by a
   scale of `n^{-1/2}` saves more than the cost of summing the cut products.
   This contradicts the lower price and proves `log s = Ω(N^{1/6})`.

Section 5 ends with the linear-size simulations for d-Ds and read-once
parity branching programs. Both Boolean lower bounds follow there.

**Other characteristics.** Outside characteristic two, exterior powers of
a minor table differ from its tensor powers by signs, and correcting them
costs at most `log 2` per site (Lemma 14), more than one bit per site can save.
Several bits per site amortize this, but a balanced cut may split the
bits of a site. The second proof avoids cuts.

1. **Realization (Lemma 15).** A weighted sum of the `r` digit
   restrictions of a circuit for `F*_n` computes the integer determinant.
   Treating the entries of `Y` as coefficients gives one syntactically
   multilinear circuit in the bits `x` over a polynomial ring.
   Specializing it to any matrix `C` gives the minor table of `C`.
2. **Dictionary (Lemma 16).** The depth reduction of Kumar, Oliveira and
   Saptharishi writes that circuit as a sum of products of factors with
   scopes of size at most `t`. The factors come from a fixed dictionary of
   polynomially many polynomials, and there are `s^{O(n/t)}` products.
3. **Lower price (Theorem 13).** Place `d·a` bits at `d` sites, `a` per
   site. The exterior near-star estimate of the OpenAI paper, with the
   sign correction, gives a minor table with price close to the star
   budget.
4. **Upper price (Theorem 17).** Nearest-point projections onto the convex
   hulls of the incident reports give a placement and one point for every
   dictionary factor. The factor's point is closer than the cone tip to
   every site it touches, by a uniform margin. Each bit with bias in
   `[-1,1]` saves at least a constant times that margin.

With `a = d^{α/2}` and `t = d^α` the two estimates contradict each other
unless `log s ≥ d^{α/3}`.

## Prior work

**Before the [OpenAI papers](https://github.com/openai/math/blob/main/CONTENTS.md).** The best lower bounds for these models were
polynomial, or required restrictions.

- Syntactically multilinear circuits: `Ω(n²/log² n)` by Alon, Kumar and
  Volk, improving the `Ω(n^{4/3}/log² n)` of Raz, Shpilka and Yehudayoff.
- Read-once parity branching programs: `Ω(n²/log² n)` by Volk (2026),
  improving `Ω(n^{3/2}/log n)`. Exponential bounds were known only for
  oblivious and graph-driven programs, and an exponential bound in
  general was an open problem of Jukna.
- Deterministic decomposable circuits: exponential bounds by Bova,
  Capelli, Mengel and Slivovsky hold only in negation normal form, where
  negations occur at the inputs.

**The OpenAI bounds.** *Circuit lower bounds for Hamiltonian cycle and the
permanent* treats general arithmetic circuits, which include the
syntactically multilinear ones.

- Its Theorem 1.1 shows that the Hamiltonian cycle polynomial of order `N`
  needs `exp(c (log N)² / (log log N)²)` gates over every field, and the
  same for the permanent outside characteristic two.
- Its Theorem 12.2 improves this to `2^{N^ε}` over fields whose
  characteristic admits ports.

## Building

```bash
tectonic multilinear-circuit-lower-bound.tex
```

This writes `multilinear-circuit-lower-bound.pdf` next to the source; a
compiled copy is committed in the repository. Any standard LaTeX engine also works; the file uses only `amsmath`,
`amssymb`, `amsthm`, `geometry`, `xcolor` and `hyperref`.

## References

- OpenAI. *Circuit lower bounds for Hamiltonian cycle and the permanent*.
  November 24, 2026 edition.
  <https://github.com/openai/math/tree/main/preprints/Circuit-lower-bounds-for-Hamiltonian-cycle-and-the-permanent-November-24-2026>
- M. Kumar, R. Oliveira and R. Saptharishi. *Towards optimal depth
  reductions for syntactically multilinear circuits*. ICALP, 2019.
  <https://doi.org/10.4230/LIPIcs.ICALP.2019.78>
- M. Monet and D. Olteanu. *Towards deterministic decomposable circuits for
  safe queries*. AMW, 2018.
- N. Alon, M. Kumar and B. L. Volk. *Unbalancing sets and an almost
  quadratic lower bound for syntactically multilinear arithmetic circuits*.
  Combinatorica, 2020. <https://arxiv.org/abs/1708.02037>
- B. L. Volk. *A lower bound for read-once parity branching programs*. 2026.
  <https://arxiv.org/abs/2607.05944>
- S. Bova, F. Capelli, S. Mengel and F. Slivovsky. *Knowledge compilation
  meets communication complexity*. IJCAI, 2016.
- S. Jukna. *Boolean Function Complexity: Advances and Frontiers*.
  Springer, 2012.
