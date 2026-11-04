<div align="center">

# pi-tool-preferences

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Version](https://img.shields.io/badge/version-v1.0.0-blue.svg)
[![GitHub stars](https://img.shields.io/github/stars/pingdongyi/pi-tool-preferences.svg)](https://github.com/pingdongyi/pi-tool-preferences)
[![GitHub issues](https://img.shields.io/github/issues/pingdongyi/pi-tool-preferences.svg)](https://github.com/pingdongyi/pi-tool-preferences)

A [Pi](https://pi.dev) skill that gives cross-platform guidance for choosing a **search / file-lookup command**: prefer `rg` (ripgrep) to search file contents and `fd` to find files by name, falling back to `grep`/`find` when the preferred tool is unavailable.

</div>

Install from Git:

```bash
pi install git:github.com/pingdongyi/pi-tool-preferences@v1
```

Or locally:

```bash
pi install ./pi-tool-preferences
```

Then load the skill in a session:

```
/skill:tool-preferences
```

## Why this skill exists

A common bad habit is defaulting to `grep`/`find` even on machines where `rg`/`fd` are installed. `rg` is faster, respects `.gitignore`, and gives line numbers + highlighting by default; `fd` is more concise and ergonomic than `find`. This skill records that preference so the model stops reaching for `grep` first.

## What it teaches

| Need | Preferred | Fallback | Why |
|---|---|---|---|
| Search file contents | `rg` | `grep -rn` | faster, `.gitignore`-aware, better default output |
| Find files by name/type | `fd` | `find` | more concise and ergonomic |
| Preferred missing / portable scripts | — | `grep` / `find` | POSIX, guaranteed on nearly every Unix-like system |

The rule is **cross-platform**: always check availability first (`command -v rg`), then use the best tool present. It never assumes a fixed tool is installed.

## Requirements

- A shell with `command -v` (any Unix-like system).
- `rg`/`fd` are optional — the skill degrades gracefully to `grep`/`find`.

## License

MIT
