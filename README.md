# flow-g

**A typed FunctionGraph IR for heterogeneous inference.**

[![Release](https://github.com/openIE-dev/flow-g/actions/workflows/release.yml/badge.svg)](https://github.com/openIE-dev/flow-g/actions/workflows/release.yml)
[![Quality](https://github.com/openIE-dev/flow-g/actions/workflows/quality.yml/badge.svg)](https://github.com/openIE-dev/flow-g/actions/workflows/quality.yml)
[![Docs](https://github.com/openIE-dev/flow-g/actions/workflows/docs.yml/badge.svg)](https://openie-dev.github.io/flow-g)
[![crates.io](https://img.shields.io/crates/v/flowg.svg)](https://crates.io/crates/flowg)
[![License](https://img.shields.io/badge/license-BSL--1.1-blue.svg)](./LICENSE)


flowG is the compiler IR + runtime substrate behind the openIE-dev ecosystem. It takes typed function graphs and dispatches them across CPU, Apple-silicon Metal, WGPU, AMX, and the OpDispatch backend family — with picojoule-budgeted per-op energy measurement built in.

This is the **public release surface**. Source is private at [`openIE-dev/flow-g-core`](https://github.com/openIE-dev/flow-g-core) — 99 crates spanning the IR, codegen passes, OpDispatch leaves, model runtimes, and benchmarks.

## Status

> Release binaries + examples + documentation. flowG is **free to use software**, not an open-source project. See [LICENSE](./LICENSE) for the Business Source License 1.1 terms — converts to Apache-2.0 four years after each binary's release date.

## What you get

| Binary | Purpose |
|---|---|
| `flowg` | The CLI: make-sample, inspect, run (with energy receipts), import PyTorch FX, bench |
| `flowg-serve` | HTTP serving for compiled graphs (model runtimes, kernels) |
| `flowg-bench` | Per-op + per-graph benchmarking with energy receipts |

Plus a Rust library, [`flowg`](https://crates.io/crates/flowg), for embedding.

## Install

```bash
# via cargo
cargo install flowg

# via cargo-binstall (prebuilt binary)
cargo binstall flowg

# direct download
curl -fsSL https://github.com/openIE-dev/flow-g/releases/latest/download/flowg-$(uname -s)-$(uname -m).tar.gz | tar xz
```

Platform support:

| Platform | Status |
|---|---|
| macOS arm64 (Apple Silicon) | shipping |
| macOS x86_64 | shipping |
| Linux x86_64 (musl) | shipping |
| Linux aarch64 (musl) | shipping |
| Windows x86_64 | shipping |

## Hello, flow-g

```bash
# write a sample graph (a two-input `add`)
flowg make-sample add.fg

# inspect the typed graph — its nodes and resource-semantic wires
flowg inspect add.fg

# run it — prints the energy receipt (total µJ, placement, determinism)
flowg run add.fg
```

See [`examples/`](./examples/) for runnable programs spanning every backend.

## What makes flow-g different

- **Typed FunctionGraph IR** — not an AST, not a SSA, not a tensor program. Functions are first-class graph nodes with typed signatures, designed for energy-cost-aware dispatch.
- **OpDispatch backend** — kernels are addressed by `(op, dtype, layout, target)` tuples. The runtime picks the lowest-joule kernel that matches.
- **Heterogeneous by default** — CPU + Metal + WGPU + AMX share the same IR. No "GPU port" — just dispatch the same graph at a different target.
- **Energy substrate** — every op has measured picojoule cost on Apple Silicon (IOReport-backed), NVML for Linux NVIDIA, RAPL for x86_64 Linux. Energy receipts are first-class output.
- **70+ model runtimes** — Llama family, Qwen family, Mamba2, Bamba, Jamba, Hunyuan, Gemma 4, LFM2 family, Whisper, Moonshine, V-JEPA, and more — all using the same IR.

## How it fits

flowG is the **substrate**. The openIE-dev language family compiles to it:

- [Lux](https://github.com/openIE-dev/lux-lang) — general-purpose reactive language → flowG
- [JMax](https://github.com/openIE-dev/jmax) — math-native language → flowG
- [Joule](https://github.com/openIE-dev/joule-lang) — energy-aware self-hosted language → flowG

And the substrate is metered by [JouleDB](https://github.com/openIE-dev/jouledb) — the energy-metered HDC database that records inference receipts.

## Documentation

- Getting started → <https://openie-dev.github.io/flow-g>
- Examples → [`examples/`](./examples/)
- API reference → <https://docs.rs/flowg>
- Source mirror → [`openIE-dev/flow-g-core`](https://github.com/openIE-dev/flow-g-core)

## Releases

[GitHub Releases](https://github.com/openIE-dev/flow-g/releases) — tagged versions with prebuilt binaries for every supported platform, plus a SHA-256 checksums file per release.

## Community

- [Discussions](https://github.com/openIE-dev/flow-g/discussions) — Q&A, design discussion
- [Issues](https://github.com/openIE-dev/flow-g/issues) — bug reports
- Security: see [SECURITY.md](./SECURITY.md)

## License

- **Binaries** — Business Source License 1.1; see [LICENSE](./LICENSE). Free for non-commercial use, internal use by orgs under $1M revenue, security/academic research. Converts to Apache-2.0 four years after each release.
- **Documentation** — CC-BY-4.0
- **Examples** — Apache-2.0
