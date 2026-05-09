<div align="center">
	<h1>TinLynk</h1>
	<p><strong>Open, local‑first AI agent stack</strong> – typed protocol, lightweight SDK, routing daemon (Connect), and user app (Chat).</p>
</div>

## Overview
TinLynk provides a cohesive set of components to build and run AI agents with explicit tool use, stable contracts, and local control of model routing and secrets.

## Core Repositories
| Repo | Purpose | Key Tech |
|------|---------|----------|
| `protocol` | Canonical types + JSON Schemas (`@tinlynk/protocol`) | TypeScript (no runtime deps) |
| `sdk` | Client runtime: models, tools, routing (`@tinlynk/sdk`) | TypeScript ESM |
| `connect` | Local daemon: profiles, model catalog, routing | Node HTTP |
| `chat` | End‑user chat app | (WIP) |
| `.github` | Shared workflows & org docs | GitHub Actions |

## Architecture (High Level)

```
User → Chat → SDK
            └─ Model path: Connect (routing + secrets) → Model Provider(s)
```

Protocol sits beneath everything: stable messages, tool descriptors, streaming event shapes.

## Why TinLynk?

- **Explicit Contracts**: Protocol first; fewer breaking surprises.
- **Local Control**: Connect keeps provider keys & routing decisions local.
- **Tool Contracts**: SDK and Protocol keep tool calls explicit and typed.
- **Simple SDK**: Thin, typed layer—no heavy framework lock‑in.
- **ESM & Modern Node**: Node ≥ 22, fast startup, minimal build complexity.

## Getting Started

```bash
git clone https://github.com/tinlynk/<repo>.git   # clone desired repo
cd protocol && npm install && npm run build       # example: build protocol
```

Add more components as needed (sdk → connect).

## Contributing

See `CONTRIBUTING.md` (org‑wide). Key points:

- MIT License + SPDX headers (`// SPDX-License-Identifier: MIT`)
- Recency Rule for dependencies (updated within 6 months)
- Minimal, focused tests; avoid over‑mocking
- Conventional commits encouraged (e.g. `feat:`, `fix:`)

## Roadmap (Early)

- Chat application hardening
- Expanded tool contracts and policy checks
- Routing heuristics (cost, latency signals)
- Protocol conformance & golden tests
- Packaging for self‑host / Docker quick start

## License

MIT – see the root `LICENSE` file. Third‑party notices will be added as needed.

## Security

Report vulnerabilities privately: [security@tinlynk.dev](mailto:security@tinlynk.dev).

---
Built with a protocol-first mindset. Contributions welcome.
