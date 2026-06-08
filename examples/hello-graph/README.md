# hello-graph

The minimum FunctionGraph: take an `f32` input, add a constant, return the result.

```bash
# embed in Rust
cargo run --example hello-graph
```

What this shows:
- The `flowg::Graph` builder API
- A single typed function with one `Param`, one `TensorLiteral`, one `Add`
- Running on the CPU backend

## Source

```rust
use flowg::Graph;

fn main() {
    let mut g = Graph::new("add_one");
    let x = g.param("x", flowg::dtype::F32);
    let one = g.literal_f32(1.0);
    let out = g.add(x, one);
    g.set_output(out);

    let runner = g.compile().unwrap();
    let result = runner.run_f32(&[41.0]).unwrap();
    println!("41 + 1 = {:?}", result);
}
```

## Next

- [`../wgsl-codegen`](../wgsl-codegen) — lower the same graph to WGSL for WebGPU
- [`../energy-receipt`](../energy-receipt) — record picojoule cost per op
