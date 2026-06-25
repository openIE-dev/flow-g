# Reference

flowG's kernel is small: **22 universal primitives** and **11 wire kinds** — a
closed, fixed vocabulary for every programming pattern. This reference documents
the `FunctionGraph` IR that realizes them; the Lux/compute projection extends the
22 with tensor and aggregate nodes (`TensorLiteral`, `StructCreate`, …) and an
`Custom(op)` extension point for kernels.

For the embedding API (the Rust `flowg` crate), see
[docs.rs/flowg](https://docs.rs/flowg).

## Core types

| Type | What it is |
|---|---|
| **FunctionGraph** | The IR. A DAG of nodes and wires with a name, an output node, and a return type. `ProgramGraph` bundles functions, an entry point, and per-function effect-allow declarations. |
| **GraphNode** | The node kinds: `Param`, `Literal`, `TensorLiteral`, `Apply{op}`, `Select`, `WhileLoop`, `Call`, `Match`, `CodeBlock`, plus capability and concurrency nodes. |
| **OpKind** | The operation an `Apply` performs: arithmetic / comparison / logic primitives, plus `Custom(String)` — the open extension point every kernel hooks (`matmul`, `ssm_scan`, `rms_norm`, …). |
| **WireKind** | Edge semantics: `Move` (default), `Borrow`, `MutBorrow`, `Copy`, `Channel`, `Shared`, `Weak`, `Stream`, `Error`, `Lazy`, `Feedback`. Ownership, generalized. |
| **TensorLiteralData** | A shaped, typed constant. Weights stay out of band in a safetensors sidecar and are reattached by name. |
| **CapabilityRef** | A gated call: capability id + version + slot + method + effects. No ambient authority; effects are checked at dispatch. |

## Targets

The same graph dispatches across targets through OpDispatch, addressed by
`(op, dtype, layout, target)`:

| Target | Backing |
|---|---|
| CPU | reference kernels + BLAS (Accelerate / OpenBLAS / MKL) |
| Apple Silicon | Metal / MPS fused kernels |
| NVIDIA | CUDA (cuBLAS) |
| Portable GPU | WGPU (Vulkan / Metal / DX12) and the browser (WASM + WebGPU) |
| AMX | Apple matrix coprocessor |

Uncovered ops fall through to the CPU reference path, so a graph always runs.

## Energy receipts

Every dispatch carries an `EnergyEstimate { picojoules, measured }`. Placement
prefers measured calibration (IOReport on Apple Silicon, NVML on NVIDIA, RAPL
on x86_64 Linux) over the analytical prior. A run can emit a per-op receipt —
see the [`energy-receipt` example](https://github.com/openIE-dev/flow-g/tree/main/examples/energy-receipt).

## Emitters

flowG can lower the same graph to source for other ecosystems — WGSL, WASM,
ONNX, StableHLO, MLIR-linalg, Triton — and to its own `.fg` binary format. See
the [`wgsl-codegen` example](https://github.com/openIE-dev/flow-g/tree/main/examples/wgsl-codegen).

## See also

- [Install](../install.md) · [Hello, flowG](../hello.md)
- [Examples](https://github.com/openIE-dev/flow-g/tree/main/examples) — runnable programs per backend
- [docs.rs/flowg](https://docs.rs/flowg) — embedding API
