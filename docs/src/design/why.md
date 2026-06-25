# Why flowG

Most toolchains treat a program as text, compile it to one target, and forget
what it cost to run. flowG makes three different choices.

## 1. A program is a typed graph, not text

flowG's IR is a **FunctionGraph** — a typed dataflow graph of nodes and wires,
not an AST or a flat token stream. Functions are first-class graph nodes with
typed signatures. Control flow, data flow, ownership, concurrency, and
capability gating are all edges in the same graph.

Storing code as what it actually *is* — a graph — means the structure a
compiler normally has to *recover* from text is already present. Analysis,
rewriting, and dispatch operate on the graph directly.

## 2. One graph, many silicons — heterogeneous by default

Kernels are addressed by `(op, dtype, layout, target)` tuples through the
**OpDispatch** backend. The same FunctionGraph runs on CPU, Apple-silicon
Metal, WGPU, and AMX — the runtime selects the kernel that fits the target.
There is no "GPU port": you dispatch the same graph at a different target, and
the device-resident path is the same typed object the CPU ran.

This is what lets a model runtime, a numerical kernel, and a compiled
application share one substrate instead of one stack per device.

## 3. Energy is a first-class output

Every op carries a measured picojoule cost — IOReport-backed on Apple
Silicon, NVML on NVIDIA, RAPL on x86_64 Linux. The runtime can pick the
lowest-joule kernel that matches a dispatch, and every run can emit an
**energy receipt**: a per-op accounting of what the work actually cost.

Energy stops being invisible. It becomes something you can budget at compile
time, measure at run time, and optimize against — the same way you'd optimize
for latency or memory.

## What that buys you

- **One graph, many surfaces.** lux, JMax, and Joule are different syntaxes
  over the same IR — the graph is canonical, the language is a projection.
- **Materialize to dozens of languages.** From the same graph, flowG emits
  source in ~38 languages (Rust, Python, Go, Haskell, C, Swift, …) — a
  deterministic graph→text function, roundtrip-tested, no model in the loop.
- **Lower to many silicons.** CPU, Metal, WGPU, AMX share the IR; the compute
  emitters target WGSL, WASM, ONNX, StableHLO, MLIR-linalg, Triton, and .fg.
- **Meter every operation.** Picojoule receipts, first-class.

flowG is the substrate the openIE-dev language family compiles to — see
[How flowG fits the ecosystem](./ecosystem.md).
