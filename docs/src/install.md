# Install

`flowg` prebuilt binaries are attached to each
[GitHub Release](https://github.com/openIE-dev/flow-g/releases).

## Fastest: `cargo binstall`

```bash
cargo binstall flowg
```

`cargo-binstall` downloads the prebuilt archive for your platform from
GitHub Releases without compiling anything. If you don't have it yet:

```bash
cargo install cargo-binstall
```

## Direct download

Pick the archive for your platform from the
[latest release](https://github.com/openIE-dev/flow-g/releases/latest):

| Platform | Archive |
|---|---|
| macOS arm64 (Apple Silicon) | `flowg-<version>-aarch64-apple-darwin.tar.gz` |
| Linux x86_64 (glibc 2.39+, e.g. Ubuntu 24.04) | `flowg-<version>-x86_64-unknown-linux-gnu.tar.gz` |
| Linux aarch64 (glibc 2.39+, e.g. Ubuntu 24.04) | `flowg-<version>-aarch64-unknown-linux-gnu.tar.gz` |
| Windows x86_64 | `flowg-<version>-x86_64-pc-windows-msvc.zip` |

The Linux binaries link the system OpenBLAS: install it first
(`sudo apt install libopenblas0` on Debian/Ubuntu).

Each archive has a `.sha256` file next to it. Unpack and put the binary on
your `PATH`, e.g. on macOS arm64:

```bash
V=0.1.1
T=aarch64-apple-darwin
curl -fsSLO "https://github.com/openIE-dev/flow-g/releases/download/v$V/flowg-$V-$T.tar.gz"
tar xzf "flowg-$V-$T.tar.gz"
mv "flowg-$V-$T/flowg" /usr/local/bin/
```

## `cargo install flowg`

The `flowg` crate on crates.io is an installer stub. `cargo install flowg`
compiles that stub, which prints these instructions and exits; it does not
build flowG from source.

## Verify

```bash
flowg --version
flowg make-sample add.fg
flowg run add.fg --input '{"x": 1.5, "y": 2.25}'   # prints 3.75
```
