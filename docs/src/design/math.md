# The math under the graph

> **▶ Interactive version:** [flowg-lang.dev/math](https://flowg-lang.dev/math) — the same five results with live diagrams.

flowG's claims aren't aesthetic. They fall out of five well-understood results —
from information theory, computation theory, type theory, and physics. Here is the
reasoning, including where a claim is a theorem and where it's an empirical bet.

## 01 · Information theory — the graph is the structure text represents

A program is a typed graph `G = (V, E)`: nodes are operations and values, edges
carry how those values relate. Writing it to a file is a serialization
`s : G → Σ*` onto a one-dimensional string. Compiling is the inverse `p : Σ* → G` —
the round trip a compiler runs on every build:

```text
source text  ──parse──▶  tokens
   ──name resolution──▶  bindings     (which definition does this name mean?)
   ──type inference────▶ types        (what is the type of this expression?)
   ──flow analysis─────▶ data & control edges
   ──borrow / lifetime─▶ ownership    (who owns, who borrows)
   = G                                (the graph the author already had in mind)
```

Two properties make the graph the natural shared form. First, text **is
redundant**: many strings denote the same graph (whitespace, ordering, names form
equivalence classes with no semantic content), so `s` is not injective in reverse.
Second, text **is structure-implicit**: bindings, types, ownership, and flow are
not written down — the compiler re-derives them every build, and that re-derivation
*is* the reconstruction of `G`.

flowG stores `G` — the canonical, structure-explicit form — and derives text on
demand. The re-derivation every build repeats becomes a one-time, reusable fact, so
the whole toolchain shares one source instead of rebuilding it from text.

## 02 · Computation theory — a closed kernel of 22 primitives

The structured program theorem (Böhm–Jacopini, 1966) showed all computable control
flow reduces to sequence, selection, iteration. flowG extends that spine across the
other axes a real program needs and closes the set at **22**:

| Category | Primitives |
|---|---|
| Computation (10) | Bind, Apply, Mutate, Branch, Iterate, Match, Sequence, Compose, Abstract, Import |
| Resource (3) | Acquire, Release, Observe |
| Error (2) | ErrorPropagate, CodeBlock |
| Concurrency (4) | Spawn, JoinAwait, YieldSuspend, Listen |
| Data / State (2) | Transact, TypeDefine |
| Temporal (1) | FeedbackDelay |

**Theorem vs. bet, said plainly:** Turing-completeness from a small set is trivial
and proves nothing interesting. The real claim is *ergonomic completeness* — that
these 22 express every *pattern* across paradigms without awkward encodings. That
is an empirical bet, not a theorem, and the evidence for it is the omni-language
round trip: parse real code in any language with a tree-sitter grammar into these
primitives, and materialize it back. *(The kernel is
`inv-ai-codegraph::flowg::FlowgNodeKind`, pinned at 22 by test.)*

## 03 · Determinism — materialization is a pure function

Emitting a language is a referentially transparent function of the graph and the
target — no hidden state, no sampling, no model in the loop:

```text
emit : Graph × Language → Text
```

- **Deterministic** — same graph, same output, byte for byte. No temperature, no seed.
- **Idempotent** — re-materializing changes nothing; there is nothing to "regenerate."
- **Drift-free** — all *N* projections are `emit(G, Lᵢ)` of one `G`, so they cannot disagree.

"Zero drift across languages" is therefore not a process discipline you maintain —
it's a property of pure functions. Change `G`; every projection follows by
construction. *(This documentation set and the website are built the same way: one
canonical source, every page a projection of it.)*

## 04 · Type theory — wires are a substructural algebra

Each of the 11 wire kinds is a typing rule on how a value passes from producer to
consumer — the same substructural type theory (Girard's linear logic; Wadler,
"linear types can change the world") that underlies Rust's ownership, lifted onto
the edge itself.

| Wire | Discipline |
|---|---|
| Move | linear — consumed exactly once |
| Borrow | non-consuming read; source retained |
| MutBorrow | exclusive — at most one at a time |
| Copy | unrestricted — freely duplicable |
| Shared / Weak | counted ownership; cycle-breaking |
| Stream / Lazy / Feedback | temporal & deferred discipline |

Whole bug classes become **structurally impossible**:

- **Use-after-move** — a `Move` consumes the source; it has no output port to wire from.
- **Data race** — `MutBorrow` is exclusive; a second mutable edge is rejected at edit time, not run time.
- **Deadlock** — circular `Acquire` chains are caught by cycle detection (Kahn's topological sort, 1962).

## 05 · Physics — energy is a first-class cost

Every operation carries a picojoule cost, modeled as a linear function of the work
it does and fit from measured silicon. Data movement dominates arithmetic by orders
of magnitude (Horowitz, 2014):

```text
E(op) ≈ a·flops + b·bytes + c        with  b ≫ a
```

Placement is then an optimization — route each op to the backend minimizing
estimated joules, preferring measured calibration over the analytical prior — and
the receipt is the sum:

```text
place(op) = argmin_backend  Ê(op, backend)
receipt   = Σ E(op)
```

This is not theory on a slide. On real hardware, a resident decode reported a
whole-SoC receipt of **~445 mJ/token**, and the linear coefficients above were fit
by ordinary least squares from measured joules — confirming, as the model predicts,
that weight movement (the `b·bytes` term) dominates the energy.

## Five results, one object

The graph is canonical, the kernel is closed, materialization is pure, the wires
are typed, and every op is costed in joules. None of these are bolted together —
they're five views of a single structure. That's why flowG is a substrate and not
a feature.

See also: [History](./history.md) · [Why flowG](./why.md) · [Reference](../reference/index.md).
