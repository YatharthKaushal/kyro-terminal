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

[![Status](https://img.shields.io/badge/status-early%20development-orange?style=flat-square)](https://github.com/YatharthKaushal/kyro-terminal)
[![Rust](https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white)](https://www.rust-lang.org/)
[![Tauri](https://img.shields.io/badge/Tauri-24C8DB?style=flat-square&logo=tauri&logoColor=black)](https://tauri.app/)
[![Svelte](https://img.shields.io/badge/Svelte-FF3E00?style=flat-square&logo=svelte&logoColor=white)](https://svelte.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![License](https://img.shields.io/badge/license-PolyForm%20Noncommercial-blue?style=flat-square)](LICENSE.md)

[Overview](#overview) ·
[Planned Features](#planned-features) ·
[Tech Stack](#tech-stack) ·
[Structure](#project-structure) ·
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
├── engine/                 # Terminal engine (Rust)
│   ├── parser/             #   ANSI/VT parsing
│   ├── platforms/          #   Platform-specific PTY layers
│   │   ├── windows/
│   │   ├── linux/
│   │   └── macos/
│   ├── core/               #   Buffer, sessions, core logic
│   └── integrations/       #   Git, SSH, AI
│
└── ui/                     # Desktop app (Tauri + Svelte)
    ├── src/                #   Svelte frontend
    └── src-tauri/          #   Tauri shell
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

## Contributing

Contributions are welcome. Before submitting a pull request:

1. **Fork** the repository.
2. **Create** a feature branch.
3. **Keep commits focused** and descriptive.
4. **Follow** the existing project structure.
5. **Test** your changes before submitting.
6. **Open a PR** with a clear description of your changes.

> [!TIP]
> For larger features or architectural changes, open an issue first so the
> implementation can be discussed before development begins.

---

## Code of Conduct

Help keep the project welcoming and productive.

| Do | Don't |
| :--- | :--- |
| Be respectful and constructive | Harass or discriminate |
| Discuss ideas, not people | Make personal attacks |
| Provide helpful feedback | Engage in abusive behavior |
| Keep discussions professional | |
| Respect differing opinions and technical approaches | |
| Assume good intent from contributors | |

Harassment, discrimination, personal attacks, or any form of abusive behavior
will not be tolerated.

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
