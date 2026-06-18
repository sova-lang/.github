<div align="center">

<img src="https://raw.githubusercontent.com/sova-lang/sova/main/logo.png" alt="Sova logo" width="160" height="160" />

# Sova

**One codebase. Two runtimes. No boilerplate between them.**

[Website](https://sova-lang.dev) · [Docs](https://sova-lang.dev/intro) · [Compiler](https://github.com/sova-lang/sova) · [Discord](https://discord.gg/sova-lang)

[![Alpha](https://img.shields.io/badge/status-alpha-orange)](https://github.com/sova-lang/sova)
[![License](https://img.shields.io/badge/license-MIT-blue)](https://github.com/sova-lang/sova/blob/main/LICENSE)

</div>

---

## What is Sova?

Sova is a multi-tier programming language. You write **one** codebase; the compiler emits **two** artefacts: a Go binary that runs the backend and a JavaScript bundle that runs in the browser. Both halves share the same types, package layout, standard library, and mental model.

The defining feature is **wiring**: mark a function `wire`, declare which side hosts it, and the compiler synthesises the transport, serialisation, routing, and authentication for you.

```sova
package todo on shared

wire func addTodo(text: string): []Todo {
    let t = new Todo(id: nextId(), text: text)
    __todos.append(t)
    return __todos
}

func boot() {
    let items = addTodo("Buy milk")    // same call, frontend or backend
    println(items.size())
}
```

No REST handlers, no API client, no schema duplication — the cross-side call is just a function call.

---

## Highlights

- **One language, two runtimes** — backend → Go, frontend → JavaScript via esbuild bundling.
- **Wire-first** — every `wire func` is a real cross-side call: typed, authenticated, serialised, routed.
- **Strong static types** — generics with constraints, options, payload-carrying enums, interfaces + mixins, type-safe casts (`as` / `as?` / `instanceof`).
- **Native interop** — `extern` blocks bind Go modules and JS packages with the same syntax; pin Go versions and npm specs in `sova.toml`.
- **First-class frontend** — Strix is a reactive composable framework: views, effects, scoped styles, file-based routing, stores.
- **Production-grade tooling** — single-binary deploys, embedded prod assets, dotenv autoload, SQL ORM (GORM port), browser API bindings (browserx), tests, dev server with hot reload, VS Code language extension.

---

## Org map

| Repo | What it is |
| --- | --- |
| [**sova**](https://github.com/sova-lang/sova) | Compiler, CLI, standard library — the language itself |
| [**strix**](https://github.com/sova-lang/strix) | Frontend framework — composables, reactivity, router, stores, DOM helpers |
| [**browserx**](https://github.com/sova-lang/browserx) | Typed Web API bindings (DOM, fetch, WebGL, WebRTC, IndexedDB, …) generated from W3C WebIDL |
| [**browserx-generator**](https://github.com/sova-lang/browserx-generator) | The WebIDL → Sova translator that produces browserx |
| [**ts2sova-generator**](https://github.com/sova-lang/ts2sova-generator) | Generates Sova bindings from any npm package's TypeScript `.d.ts` |
| [**ported-libraries**](https://github.com/sova-lang/ported-libraries) | Curated Sova ports of popular libraries (GORM, Redis client, …) |
| [**vscode-sova**](https://github.com/sova-lang/vscode-sova) | VS Code language extension (syntax, LSP integration, formatter) |
| [**docs**](https://github.com/sova-lang/docs) | Source of [sova-lang.dev](https://sova-lang.dev) |

---

## Get started

```bash
# Install the compiler
curl -fsSL https://sova-lang.dev/install.sh | sh

# Scaffold a project
sova init my-app && cd my-app

# Dev server with hot reload
sova dev

# Production build → single Go binary embedding the JS bundle
sova build
```

Then walk the [Hello World](https://sova-lang.dev/getting-started/hello-world) and [First wired app](https://sova-lang.dev/getting-started/first-wired-app) guides.

---

## Status

Alpha — APIs and surface syntax can change between releases, and the compiler has known bugs tracked in each repo's `TODO.md`. Use it for exploration and personal projects today; production hardening is a goal of the upcoming `0.x → 1.0` cycle.

Found a bug or want a feature? [Open an issue](https://github.com/sova-lang/sova/issues/new/choose) on the compiler repo, or jump into the [Discord](https://discord.gg/sova-lang).
