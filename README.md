# rust-starter

Cargo workspace starter: a binary crate, a library crate, an mdBook, and GitHub Actions for CI, GitHub Pages, and releases.

## Layout

| Path | Purpose |
| --- | --- |
| `crates/app` | Binary. Not published. |
| `crates/lib` | Library. Release workflow **dry-runs** `cargo publish` for this crate. |
| `docs` | mdBook sources. Published to GitHub Pages from `main`. |
| `rust-toolchain.toml` | Pins Rust 1.99.1, Clippy, and rustfmt. |
| `.github/workflows/ci.yml` | Format, Clippy, and tests. |
| `.github/workflows/deploy.yml` | Build the book and deploy GitHub Pages. |
| `.github/workflows/release.yml` | Changelog and GitHub Release for `v*` tags. |

## Requirements

[Rust 1.99.1](https://www.rust-lang.org/) via rustup. The toolchain file selects it automatically.

mdBook 0.5.4 is only needed to preview the book locally:

```bash
cargo install mdbook --version 0.5.4 --locked
mdbook serve docs
```

## Commands

```bash
cargo fmt --check
cargo clippy --all-targets -- -D warnings
cargo test
```

## Before the first real release

- Rename `app` and `lib`. Those names will collide on crates.io.
- Replace `https://github.com/OWNER/REPO` in `cliff.toml`.
- In the repository settings, set Pages to deploy with GitHub Actions.
- Keep `--dry-run` on `cargo publish` until a crates.io token is configured. Conventional Commits (`feat:`, `fix:`, `doc:`) are what git-cliff turns into release notes.

Pushing a tag such as `v0.1.0` runs the release workflow.
