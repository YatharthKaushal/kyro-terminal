# Security Policy

## Supported versions

Kyro is in early development and has no released versions. Only the `main`
branch is supported.

| Version | Supported |
| :--- | :--- |
| `main` | Yes |
| Everything else | No |

## Reporting a vulnerability

**Do not open a public issue for security vulnerabilities.**

Report privately through either channel:

- [GitHub Security Advisories](https://github.com/YatharthKaushal/kyro-terminal/security/advisories/new) — preferred.
- Email **[theyatharthk@gmail.com](mailto:theyatharthk@gmail.com)**.

Please include:

- A description of the issue and its impact.
- Steps to reproduce, or a proof of concept.
- Affected commit or branch.
- Your platform and version (Windows / Linux / macOS).

## What to expect

- Acknowledgement within **7 days**.
- An assessment and planned fix timeline within **30 days**.
- Credit in the advisory, unless you prefer to remain anonymous.

Because a terminal emulator executes shell input and parses untrusted output,
reports involving **escape sequence handling**, **PTY process spawning**, and
**IPC between the Tauri shell and the frontend** are especially valuable.
