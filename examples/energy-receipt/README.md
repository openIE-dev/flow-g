# energy-receipt

Run a graph with the substrate-energy layer attached. Output a JSON receipt with picojoule cost per op.

```bash
flowg run examples/energy-receipt/add.fg --record-energy receipt.json
jq '.ops[] | {name, picojoules, target}' receipt.json
```

Sample receipt fragment:

```json
{
  "graph": "add_one",
  "target": "apple-silicon-cpu",
  "total_picojoules": 12480,
  "ops": [
    {"name": "Param.x", "picojoules": 0, "target": "host"},
    {"name": "Literal.one", "picojoules": 0, "target": "host"},
    {"name": "Add", "picojoules": 12480, "target": "neon"}
  ]
}
```

What this shows:
- The substrate-energy backend on Apple Silicon (IOReport)
- Per-op picojoule accounting
- Receipts as first-class output (suitable for piping to JouleDB)
