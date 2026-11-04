---
name: tool-preferences
description: Prefer rg (ripgrep) to search file contents and fd to find files by name, falling back to grep/find when unavailable. Cross-platform rule for choosing a search or file-lookup command on any OS.
---

# Tool preferences (cross-platform)

When you need to search file contents or find files by name, choose the best tool **available on the current host** — do not assume a fixed one is installed.

| Need | Preferred | Fallback | Why |
|---|---|---|---|
| Search file contents | `rg` | `grep -rn` | rg is faster, respects `.gitignore`, gives line numbers + highlighting by default |
| Find files by name/type | `fd` | `find` | fd is more concise and ergonomic than `find` |
| Preferred missing / portable scripts | — | `grep` / `find` | POSIX, guaranteed on nearly every Unix-like system |

## Always verify availability first

Do not assume a tool is present. Check at runtime:

```bash
command -v rg && command -v fd   # both present → use rg / fd
command -v rg || echo "rg missing; fall back to grep"
```

## Rule of thumb

Prefer the faster, better-default tool **when present**; only reach for `grep`/`find` when the preferred tool is unavailable, or when writing portable scripts that must run anywhere.

Recorded from a user correction: I defaulted to `grep`; the user pointed out rg/fd are better suited and that the guidance should hold across platforms.
