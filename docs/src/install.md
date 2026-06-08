# Install

`flowg` is published to crates.io and to GitHub Releases.

## Fastest: `cargo binstall`

```bash
cargo binstall flowg
```

`cargo-binstall` fetches the prebuilt binary for your platform from [GitHub Releases](https://github.com/openIE-dev/flow-g/releases) without compiling anything.

If you don't have `cargo-binstall` yet:

```bash
cargo install cargo-binstall
```

## From source: `cargo install`

```bash
cargo install flowg
```

This compiles the source. Slower; useful if your platform isn't in our prebuilt list.

## Direct download

```bash
curl -fsSL -o flowg.tar.gz \
  https://github.com/openIE-dev/flow-g/releases/latest/download/flowg-$(uname -s)-$(uname -m).tar.gz
tar xzf flowg.tar.gz
mv flowg-*/flowg /usr/local/bin/
```

## Verify

```bash
flowg --version
```
