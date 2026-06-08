# wgsl-codegen

Take the same `add_one` graph from [`hello-graph`](../hello-graph) and lower it to WGSL for WebGPU dispatch.

```bash
flowg emit --target wgsl examples/wgsl-codegen/add.fg > add.wgsl
```

What this shows:
- Same source graph → different target
- The `flowg-emit-wgsl` backend
- How OpDispatch picks WGPU-friendly kernels

## Generated WGSL

The output is a complete WGSL compute shader that you can drop into wgpu-rs.

## Next

- [`../energy-receipt`](../energy-receipt) — measure picojoule cost on the WGPU target
