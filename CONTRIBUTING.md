# Contributing to Kyro Terminal

Thanks for your interest in Kyro. This document covers how to get the project
running locally and what is expected of a pull request.

Kyro is in **early development**. APIs, module boundaries, and directory layout
will change without notice.

---

## Prerequisites

| Tool | Version | Notes |
| :--- | :--- | :--- |
| **Rust** | 1.85+ | The `engine` crate uses `edition = "2024"` |
| **Node.js** | 20+ | |
| **pnpm** | 10+ | `npm install -g pnpm` |

Plus the platform dependencies required by Tauri v2:

- **Windows** — [Microsoft C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/) and [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) (preinstalled on Windows 11).
- **Linux** — `libwebkit2gtk-4.1-dev`, `build-essential`, `curl`, `wget`, `file`, `libxdo-dev`, `libssl-dev`, `libayatana-appindicator3-dev`, `librsvg2-dev`.
- **macOS** — Xcode Command Line Tools (`xcode-select --install`).

See the [Tauri prerequisites guide](https://tauri.app/start/prerequisites/) for
the authoritative, up-to-date list.

---

## Setup

```bash
git clone https://github.com/YatharthKaushal/kyro-terminal.git
cd kyro-terminal/ui
pnpm install
```

## Running

```bash
# from ui/ — launches the desktop app with hot reload
pnpm tauri dev

# frontend only, in a browser (no PTY, no native APIs)
pnpm dev
```

## Building

```bash
# from ui/ — produces a release binary + installer in ui/src-tauri/target/release/
pnpm tauri build
```

## Checks

Run these before opening a pull request — CI runs the same set on Windows,
Linux, and macOS.

```bash
# frontend types
cd ui && pnpm check

# engine
cargo fmt   --manifest-path engine/Cargo.toml --all --check
cargo clippy --manifest-path engine/Cargo.toml --all-targets -- -D warnings
cargo test  --manifest-path engine/Cargo.toml --all-targets

# tauri shell
cargo check --manifest-path ui/src-tauri/Cargo.toml
```

---

## Project layout

| Path | Contains |
| :--- | :--- |
| `engine/src/core/` | Terminal buffer, sessions, core logic |
| `engine/src/parser/` | ANSI/VT escape sequence parsing |
| `engine/src/platforms/` | Platform PTY layers — ConPTY on Windows, PTY elsewhere |
| `engine/src/integrations/` | Git, SSH, AI |
| `ui/src/` | Svelte frontend |
| `ui/src-tauri/` | Tauri shell — depends on `engine` as a path dependency |

Keep platform-specific code inside `engine/src/platforms/`. Everything above it
should compile on all three targets.

---

## Pull requests

1. **Fork** the repository.
2. **Create a feature branch** off `main`.
3. **Keep commits focused** and descriptive — one logical change per commit.
4. **Follow the existing project structure.**
5. **Run the checks above** before submitting.
6. **Open a PR** with a clear description of what changed and why.

> [!TIP]
> For larger features or architectural changes, open an issue first so the
> implementation can be discussed before development begins. This avoids
> throwing away work that doesn't fit the direction of the project.

### Commit messages

No strict format enforced. Prefer an imperative subject under ~72 characters,
with a body explaining *why* when the change isn't self-evident.

```
Add ConPTY resize handling

Windows requires ResizePseudoConsole to be called before the child
process observes the new dimensions; without it, TUI apps redraw at
the old size.
```

---

## Code of Conduct

By participating you agree to the [Code of Conduct](CODE_OF_CONDUCT.md).

## Licensing of contributions

Kyro is licensed under [PolyForm Noncommercial 1.0.0](LICENSE.md). By submitting
a pull request you agree that your contribution is licensed under those same
terms.
