<div align="center">

<pre>
    ┌──────────────────────────────────────────────┐
    │  ●  ●  ●                            kyro  ─ □ ×
    ├──────────────────────────────────────────────┤
    │                                              │
    │   ██╗  ██╗██╗   ██╗██████╗  ██████╗          │
    │   ██║ ██╔╝╚██╗ ██╔╝██╔══██╗██╔═══██╗         │
    │   █████╔╝  ╚████╔╝ ██████╔╝██║   ██║         │
    │   ██╔═██╗   ╚██╔╝  ██╔══██╗██║   ██║         │
    │   ██║  ██╗   ██║   ██║  ██║╚██████╔╝         │
    │   ╚═╝  ╚═╝   ╚═╝   ╚═╝  ╚═╝ ╚═════╝          │
    │                                              │
    │   $ a terminal worth looking at_             │
    │                                              │
    └──────────────────────────────────────────────┘
</pre>

### Kyro Terminal

**A modern, fast, and highly customizable terminal emulator**<br/>
built from the ground up with Rust, Tauri, and Svelte.

<br/>

[![CI](https://img.shields.io/github/actions/workflow/status/YatharthKaushal/kyro-terminal/ci.yml?branch=main&style=flat-square&label=CI)](https://github.com/YatharthKaushal/kyro-terminal/actions/workflows/ci.yml)
[![Status](https://img.shields.io/badge/status-early%20development-orange?style=flat-square)](https://github.com/YatharthKaushal/kyro-terminal)
[![Rust](https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white)](https://www.rust-lang.org/)
[![Tauri](https://img.shields.io/badge/Tauri-24C8DB?style=flat-square&logo=tauri&logoColor=black)](https://tauri.app/)
[![Svelte](https://img.shields.io/badge/Svelte-FF3E00?style=flat-square&logo=svelte&logoColor=white)](https://svelte.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![License](https://img.shields.io/badge/license-PolyForm%20Noncommercial-blue?style=flat-square)](LICENSE.md)

[Overview](#overview) ·
[Planned Features](#planned-features) ·
[Getting Started](#getting-started) ·
[Tech Stack](#tech-stack) ·
[Structure](#project-structure) ·
[Docs](#documentation) ·
[Contributing](#contributing) ·
[License](#license)

</div>

---

## Overview

Kyro aims to be a beautiful, extensible, and performant terminal that goes beyond
traditional emulators — a modern user experience that stays lightweight and
cross-platform.

Unlike terminals that stop at themes and config files, **Kyro makes the interface
itself customizable**, so new layouts and workflows can be built without
sacrificing performance.

> [!NOTE]
> **Current status: early development.** The features below are the roadmap, not a
> shipping changelog. Expect breaking changes.

---

## Planned Features

<table>
<tr>
<td valign="top" width="33%">

**Core Engine**

- Fast native terminal engine
- Native ConPTY / PTY integration
- GPU-accelerated rendering
- Search and scrollback
- Session persistence

</td>
<td valign="top" width="33%">

**Interface**

- Multiple tabs
- Split panes
- Customizable sidebar
- Workspace management
- Command palette

</td>
<td valign="top" width="33%">

**Extensibility**

- Plugin system
- Git integration
- SSH integration
- AI integrations
- Theme support
- Keyboard shortcut customization

</td>
</tr>
</table>

**Platforms:** Windows · Linux · macOS

---

## Getting Started

> [!IMPORTANT]
> There is no release build yet. The steps below build from source and launch a
> development window — the terminal itself is not functional.

### Prerequisites

| Tool | Version | Notes |
| :--- | :--- | :--- |
| [Rust](https://rustup.rs/) | 1.85+ | The `engine` crate uses `edition = "2024"` |
| [Node.js](https://nodejs.org/) | 20+ | |
| [pnpm](https://pnpm.io/) | 10+ | `npm install -g pnpm` |

Plus the platform dependencies required by Tauri v2:

- **Windows** — [C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/) and [WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) *(preinstalled on Windows 11)*
- **Linux** — `libwebkit2gtk-4.1-dev`, `build-essential`, `libxdo-dev`, `libssl-dev`, `libayatana-appindicator3-dev`, `librsvg2-dev`
- **macOS** — Xcode Command Line Tools (`xcode-select --install`)

Full list: [Tauri prerequisites](https://tauri.app/start/prerequisites/).

### Run

```bash
git clone https://github.com/YatharthKaushal/kyro-terminal.git
cd kyro-terminal/ui

pnpm install
pnpm tauri dev
```

### Build

```bash
# from ui/ — binary and installer land in ui/src-tauri/target/release/
pnpm tauri build
```

### Checks

```bash
cd ui && pnpm check                                       # frontend types
cargo fmt    --manifest-path engine/Cargo.toml --all --check
cargo clippy --manifest-path engine/Cargo.toml --all-targets -- -D warnings
cargo test   --manifest-path engine/Cargo.toml --all-targets
cargo check  --manifest-path ui/src-tauri/Cargo.toml       # tauri shell
```

---

## Tech Stack

| Layer | Built with |
| :--- | :--- |
| **UI** | Tauri · Svelte · TypeScript |
| **Engine** | Rust · ConPTY (Windows) · PTY (Linux/macOS) |
| **Terminal** | ANSI/VT escape sequences · Alacritty / WezTerm parser *(planned)* |

---

## Project Structure

```text
Terminal/
├── engine/                     # Terminal engine (Rust crate)
│   ├── Cargo.toml
│   └── src/
│       ├── lib.rs              #   Crate root
│       ├── core/               #   Buffer, sessions, core logic
│       ├── parser/             #   ANSI/VT parsing
│       ├── platforms/          #   Platform-specific PTY layers
│       │   ├── windows/        #     ConPTY
│       │   ├── linux/          #     PTY
│       │   └── macos/          #     PTY
│       └── integrations/       #   Git, SSH, AI
│
└── ui/                         # Desktop app (Tauri + Svelte)
    ├── src/                    #   Svelte frontend
    └── src-tauri/              #   Tauri shell — depends on `engine`
```

<details>
<summary><b>Directory overview</b></summary>

<br/>

### `engine/`

The terminal engine, responsible for:

- PTY management
- ANSI parsing
- Terminal buffer
- Sessions
- Platform-specific implementations
- Terminal core logic

### `ui/`

The desktop application built with Tauri and Svelte, responsible for:

- Rendering
- Window management
- Sidebar
- Tabs
- Split panes
- Settings
- User interface

</details>

---

## Documentation

<table>
<tr>
<td width="30%">

**[Architecture](./ARCHITECTURE.md)**

</td>
<td>

Project architecture, folder structure, technology stack, design philosophy, and
development roadmap.

</td>
</tr>
<tr>
<td>

**[Contributing](./CONTRIBUTING.md)**

</td>
<td>

Prerequisites, local setup, project layout, and the checks CI runs.

</td>
</tr>
<tr>
<td>

**[Code of Conduct](./CODE_OF_CONDUCT.md)**

</td>
<td>

Expected behavior in issues, pull requests, and discussions.

</td>
</tr>
<tr>
<td>

**[Security Policy](./SECURITY.md)**

</td>
<td>

How to report a vulnerability privately.

</td>
</tr>
</table>

---

## Contributing

Contributions are welcome. Read **[CONTRIBUTING.md](CONTRIBUTING.md)** for setup,
project layout, and the checks CI runs.

1. **Fork** the repository.
2. **Create** a feature branch.
3. **Keep commits focused** and descriptive.
4. **Follow** the existing project structure.
5. **Run the checks** before submitting.
6. **Open a PR** with a clear description of your changes.

> [!TIP]
> For larger features or architectural changes, open an issue first so the
> implementation can be discussed before development begins.

Also see the [Code of Conduct](CODE_OF_CONDUCT.md) and, for vulnerabilities, the
[Security Policy](SECURITY.md) — please don't report those in public issues.

---

## Acknowledgements

Kyro stands on the work of others:

- **[Tauri](https://tauri.app/)** — the desktop shell and native layer.
- **[Svelte](https://svelte.dev/)** and **[SvelteKit](https://kit.svelte.dev/)** — the frontend.
- **[Rust](https://www.rust-lang.org/)** — the engine.
- **[Alacritty](https://github.com/alacritty/alacritty)** and **[WezTerm](https://github.com/wez/wezterm)** — prior art for terminal emulation and VT parsing, and the reference for Kyro's planned parser.
- **[Microsoft ConPTY](https://devblogs.microsoft.com/commandline/windows-command-line-introducing-the-windows-pseudo-console-conpty/)** — pseudoconsole support on Windows.

---

## License

Licensed under the **PolyForm Noncommercial 1.0.0 License** — see [LICENSE.md](LICENSE.md).

- **Personal & community use** — free to fork, modify, contribute to, and
  redistribute for personal or non-commercial purposes.
- **Commercial use** — any commercial use, paid distribution, or monetization
  requires an explicit commercial license or permission.

Commercial licensing inquiries: **[theyatharthk@gmail.com](mailto:theyatharthk@gmail.com)**

---

<div align="center">

<sub>◇ ─────────────── ◇ ─────────────── ◇</sub>

### built with ❤️

<sub><b>Kyro Terminal</b> · <a href="https://github.com/YatharthKaushal/kyro-terminal">github.com/YatharthKaushal/kyro-terminal</a></sub>

<br/>

</div>
