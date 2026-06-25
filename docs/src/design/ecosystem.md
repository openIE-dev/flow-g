# How flowG fits the openIE ecosystem

Five public projects share a common substrate:

```
                       lux-lang   jmax    joule-lang
                            \     |     /
                             \    |    /
                              ▼   ▼   ▼
                             flow-g  ←  ← ← jouledb (metered persistence)
                                ▲
                                │
                          substrate-energy
                              (joules)
```

## flowG is the substrate

Everything else is a surface over, or a consumer of, the same typed
FunctionGraph IR. That is the whole point: one substrate, many fronts, one
energy model.

- **[lux-lang](https://openie-dev.github.io/lux-lang)** — a general-purpose,
  reactive language. Lux source compiles to flowG; the graph is what runs.
- **[jmax](https://openie-dev.github.io/jmax)** — a math-native language for
  numerical and scientific work, lowered to flowG so the same kernels and the
  same energy model apply.
- **[joule-lang](https://openie-dev.github.io/joule-lang)** — an
  energy-budgeted, self-hosted language: energy limits are part of the program,
  enforced through flowG's metered dispatch.
- **[jouledb](https://openie-dev.github.io/jouledb)** — the energy-metered
  database. It stores graphs and records inference receipts, closing the loop
  between *what ran* and *what it cost*.
- **substrate-energy** — the joule-accounting layer underneath flowG:
  IOReport on Apple Silicon, NVML on NVIDIA, RAPL on x86_64 Linux. Every op's
  picojoule cost flows from here.

## Why a shared substrate

Each language above could have shipped its own compiler, its own runtime, and
its own per-device backends. Instead they target one IR, which means:

- **One set of kernels.** A matmul, an SSM scan, an attention op is written
  once against OpDispatch and is available to every surface, on every target.
- **One energy model.** A Lux program, a JMax computation, and a model runtime
  are all metered the same way, in the same units, against the same receipts.
- **One heterogeneous story.** CPU / Metal / WGPU / AMX support is shared, not
  re-implemented per language.

flowG itself is the public release surface
([openIE-dev/flow-g](https://github.com/openIE-dev/flow-g)); the full source is
the private mirror
([openIE-dev/flow-g-core](https://github.com/openIE-dev/flow-g-core)).
