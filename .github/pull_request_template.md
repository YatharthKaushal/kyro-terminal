## What changed

<!-- A short description of the change and why it's needed. -->

## Related issue

<!-- Closes #123 — or "none" for small, self-evident changes. -->

## How it was tested

<!-- Platforms tested on, and what you ran. -->

- [ ] Windows
- [ ] Linux
- [ ] macOS

## Checklist

- [ ] `cd ui && pnpm check` passes
- [ ] `cargo fmt --manifest-path engine/Cargo.toml --all --check` passes
- [ ] `cargo clippy --manifest-path engine/Cargo.toml --all-targets -- -D warnings` passes
- [ ] `cargo test --manifest-path engine/Cargo.toml --all-targets` passes
- [ ] `cargo check --manifest-path ui/src-tauri/Cargo.toml` passes
- [ ] Platform-specific code lives under `engine/src/platforms/`
