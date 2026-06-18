<div align="center">

<img src="https://raw.githubusercontent.com/sova-lang/sova/main/logo.png" alt="Sova logo" width="160" height="160" />

# Sova

**One codebase. Two runtimes. No boilerplate between them.**

[Website](https://sova-lang.dev) · [Docs](https://sova-lang.dev/intro) · [Install](https://sova-lang.dev/getting-started/install) · [Compiler](https://github.com/sova-lang/sova)

[![Alpha](https://img.shields.io/badge/status-alpha-orange)](https://github.com/sova-lang/sova)
[![License](https://img.shields.io/badge/license-MIT-blue)](https://github.com/sova-lang/sova/blob/main/LICENSE)

</div>

---

Sova is a multi-tier programming language. You write **one** codebase; the compiler emits a Go binary that runs the backend and a JavaScript bundle that runs in the browser. Both halves share the same types, packages, standard library, and mental model.

The defining feature is **wiring**: declare a function `wire`, host it on one side, call it from the other — the compiler synthesises transport, serialisation, routing, and authentication.

```sova
// src/backend/counter.sova
package myapp on backend

let __value: int = 0

wire func tick(): int {
    __value = __value + 1
    return __value
}
```

```sova
// src/frontend/app.sova
package myapp on frontend

import "myapp"

func boot() {
    let next, _ = tick()              // typed RPC under the hood
    println("counter: " + next)
}
```

No REST handlers, no API client, no schema duplication — the cross-side call is just a typed function call.

## Highlights

- **One language, two runtimes** — backend → Go, frontend → JavaScript bundled by esbuild.
- **Wire-first** — every `wire func` is a real cross-side call: typed, authenticated, serialised, routed.
- **Strong static types** — generics with constraints, options, payload enums, interfaces + mixins, type-safe casts (`as` / `as?` / `instanceof`).
- **Native interop** — `extern` blocks bind Go modules and npm packages with the same syntax; versions and specs pinned in `sova.toml`.
- **First-class frontend** — Strix is a reactive composable framework with views, effects, scoped styles, router, and stores.
- **Production-grade tooling** — single-binary deploys, embedded prod assets, dotenv autoload, SQL ORM, browser API bindings, dev server with hot reload, VS Code extension.

## Status

Alpha — surface syntax can change between releases. Use it for exploration and personal projects today; production hardening is the focus of the upcoming `0.x → 1.0` cycle.

Found a bug? [Open an issue](https://github.com/sova-lang/sova/issues/new/choose) on the compiler repo.
