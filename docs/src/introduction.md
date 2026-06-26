# Introduction

**flowG**: The flowG FunctionGraph IR: types, codegen, runtime, OpDispatch backends, energy receipts.

This is the official documentation for flowG. The full source code lives in the [private `-core` mirror](https://github.com/openIE-dev/flow-g-core); the public release surface is at [openIE-dev/flow-g](https://github.com/openIE-dev/flow-g).

## What you'll find here

- **[Install](./install.md)**: get the `flowg` binary on your machine
- **[Hello, flowG](./hello.md)**: first program in 30 seconds
- **[Tutorial](./tutorial/index.md)**: a 30-minute hands-on guided tour
- **[Reference](./reference/index.md)**: every feature, every flag, every API
- **[Cookbook](./cookbook/index.md)**: task-oriented recipes
- **[Design](./design/why.md)**: why flowG exists and how it fits with the rest of openIE-dev

## The openIE-dev ecosystem

flowG is one of five public openIE-dev projects. All five share a common substrate (flowG) and energy-metering layer (substrate-energy):

- **[flow-g](https://openie-dev.github.io/flow-g)**: the IR + runtime substrate
- **[lux-lang](https://openie-dev.github.io/lux-lang)**: reactive language compiling to flowG
- **[jmax](https://openie-dev.github.io/jmax)**: math-native language
- **[joule-lang](https://openie-dev.github.io/joule-lang)**: energy-budgeted compiled language
- **[jouledb](https://openie-dev.github.io/jouledb)**: energy-metered database

## License

flowG binaries are distributed under [BSL-1.1](https://github.com/openIE-dev/flow-g/blob/main/LICENSE). Documentation under CC-BY-4.0. Examples under Apache-2.0.
