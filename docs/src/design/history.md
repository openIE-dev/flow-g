# History — an idea the field has been building toward

> **▶ Interactive version:** [flowg-lang.dev/history](https://flowg-lang.dev/history) — the same lineage with a live interaction-net reducer you can poke at.

"Code is structure" is one of computing's oldest and most beautiful ideas —
explored by brilliant people for fifty years, each generation advancing it and
each right for its time. flowG doesn't claim to have invented it. It builds on all
of it, and the moment is finally right: parallel silicon everywhere, compute in
the browser, and energy worth measuring.

## Text built the modern world (1945)

When von Neumann described the stored-program computer, the teletype made text the
natural way to write and read code — and it was exactly right. For eighty years a
whole civilization of wonderful tools grew on it: editors, parsers, formatters,
diffs, version control. flowG keeps all of that. Text stays the surface people
love; **the graph it represents becomes shared too.**

## Everything else became a graph (today)

The silicon is parallel. The computation is a parallel graph. The intelligence we
built on top — attention — is graph-structured. At every layer the world is
relational and multidimensional. flowG lets the source code share that shape too —
working at the structure directly, while text stays the surface you read and write.

## The lineage — six threads, fifty years

flowG is a synthesis, not a bolt from the blue. Each of these communities found a
piece of it; the contribution is connecting them — and adding energy as the spine.

### 01 · Dataflow & visual programming (1970s →)
**Jack Dennis & Arvind (MIT dataflow) · LabVIEW "G" (1986) · Prograph · Max/MSP · Pure Data · Simulink · Node-RED · Enso.**
The first machines and languages where computation is a graph of operations that
fire when their inputs are ready.
*Lesson:* graphs win where the work is dataflow (signal, instrumentation, control,
ETL). They stalled on branchy, stateful control — a UX problem, not a theory one.

### 02 · Graph reduction & interaction nets (1990 →)
**Lévy & Lamping (optimal reduction) · Yves Lafont (interaction nets 1990, combinators 1997) · HVM / Bend.**
The most rigorous form of "the graph is the program": computation is local graph
rewriting that is inherently parallel.
*Lesson:* a reduction model maps onto parallel silicon more naturally than a
sequential one ever could.

### 03 · Content-addressed code (2010s →)
**Unison (Paul Chiusano, Rúnar Bjarnason) · cousins: Git, Nix, IPFS.**
Every definition is identified by the hash of its syntax tree; names are labels,
so there are no merge conflicts, perfect caching, trivial code mobility.
*Lesson:* the closest existing answer to "let a machine mutate code without
breaking the build."

### 04 · Projectional & structural editing (1981 →)
**Cornell Program Synthesizer (Teitelbaum, 1981) · Intentional Programming (Simonyi, MSR) · JetBrains MPS · Hazel (typed holes) · Lamdu.**
Edit the tree, not the characters — so a program is never syntactically broken.
Simonyi's "intentional tree with text as one projection" is almost exactly flowG's
thesis, thirty years early.
*Lesson:* people rightly loved text — fast to write, and the whole toolchain
speaks it. flowG keeps text as a first-class surface and adds the graph beneath, so
people and machines each work in the form that suits them. That is why the idea is
ready now.

### 05 · ML graph IRs (2015 →)
**Theano / TF1 · PyTorch & JAX (jaxpr) · ONNX · MLIR (Lattner, 2019) · XLA / StableHLO · TVM · IREE · Triton · GGML · MLX.**
Machine learning rebuilt all of this for tensors: trace a program into a graph,
lower one graph to many backends. JAX is explicit — Python is a frontend to a graph.
*Lesson:* one-graph-many-silicons is table stakes for tensors. flowG's contribution
is generalizing it beyond tensors — to all code — with resource-typed wires and
energy as a first-class unit.

### 06 · The energy basis (2014 →)
**Mark Horowitz — "Computing's Energy Problem" (ISSCC 2014).**
The much-cited table putting hard picojoule numbers on primitive operations: an
8-bit add costs a sliver of a pJ; a DRAM access, hundreds to thousands of times
more. Data movement, not arithmetic, is where the joules go.
*Lesson:* flowG operationalizes that table as a placement pass — route each op to
the lowest-joule silicon, and hand back a receipt.

## The evidence — the field keeps rediscovering the substrate

Recent research keeps finding, empirically, that under the syntax of every language
there is a shared, language-agnostic structure — and that operating on it works
better. These aren't flowG's results; they're the ground it's built on.

| Work | Where | Finding |
|---|---|---|
| **LACE** | IBM, NAACL 2024 ([arXiv:2310.16803](https://arxiv.org/abs/2310.16803)) | Code embeddings contain separable syntax and language-agnostic semantics. |
| **Semantic Hub** | 2024 ([arXiv:2411.04986](https://arxiv.org/abs/2411.04986)) | LLMs develop a shared representation across languages and modalities. |
| **IRCoder** | UKP Lab, ACL 2024 ([arXiv:2403.03894](https://arxiv.org/abs/2403.03894)) | Forcing models through a shared IR gives consistent multilingual gains. |
| **ProGraML** | ETH Zürich, ICML 2021 ([arXiv:2003.10536](https://arxiv.org/abs/2003.10536)) | Language-agnostic graphs reach 94% F1 on compiler analysis across six languages. |
| **CodeGRAG** | 2024 ([arXiv:2405.02355](https://arxiv.org/abs/2405.02355)) | Control-/data-flow graphs from one language improve generation in another. |
| **UniCoder** | ACL 2024 ([arXiv:2406.16441](https://arxiv.org/abs/2406.16441)) | Routing through a universal pseudocode improves generation. Even a naïve substrate helps. |

Each validated a piece in isolation — embeddings, intermediate representations,
read-only graphs, pseudocode. The remaining work was to make the graph the source
of truth, give it resource-typed wires, and meter it in joules.

## Why now — the moment is right

Text earned its place: people write it fast, and the whole toolchain — diff,
review, blame, the terminal — speaks it beautifully. flowG keeps every bit of that
and adds a shared graph beneath, so people keep their surface while every language
and every chip gain one too. What's new is the timing: parallel silicon
everywhere, WebGPU putting compute in the browser, and energy finally something we
can measure and save.

So this is not a claim of novelty. It's a claim of timing — and of cause. We're
building the thing fifty years of brilliant work has been circling, in the open,
because energy-efficient compute is worth building. **Stand on the shoulders;
carry it the last step.**

See also: [The math under the graph](./math.md) · [Why flowG](./why.md).
