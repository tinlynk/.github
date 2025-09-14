# Contributing to TinLynk

Thank you for your interest in contributing. These guidelines apply org‑wide to all TinLynk repositories unless a repository overrides a section explicitly.

## Core Principles

- **Simplicity first**: prefer clear, minimal solutions over clever abstractions.
- **Stability of contracts**: protocol & public SDK APIs follow SemVer; breaking changes require a major version bump and a migration note.
- **Security & safety**: never commit secrets; validate only what impacts correctness and safety; apply least privilege for any external access.
- **Recency Rule**: use only technologies / libraries with a public release in the last 6 months (or an active LTS). If in doubt, open an issue before introducing a dependency.

## License & Copyright

- All contributions are under the project license: **MIT**.
- Add SPDX headers to all new source files:
  ```ts
  // SPDX-License-Identifier: MIT
  ```
- Do not submit code you do not have the right to license under MIT.

## Repository Layout Expectations

- `protocol`: canonical types & JSON Schemas (no runtime deps).
- `sdk`: lightweight client runtime (depends only on `@tinlynk/protocol`).
- `connect`: local daemon (depends on `@tinlynk/sdk`).
- `mcp-server`: tool host (depends on `@tinlynk/protocol`).
- Apps / extensions depend on `@tinlynk/sdk`.

## Development Environment

- Node.js **>= 22**.
- ESM only (no dual CJS build). Avoid transpiling for older Node versions.
- TypeScript strict mode enforced.

## Adding Dependencies

1. Justify necessity (performance, security, or substantial dev productivity).
2. Confirm recent activity (commit / release in last 6 months).
3. Prefer smaller, well‑maintained libs over monolith frameworks.
4. Avoid transitive license conflicts (we are MIT; ensure compatibility).

## Coding Standards

- Keep functions small & cohesive. Extract when branching logic obscures intent.
- Avoid unnecessary indirection, base classes, or meta‑programming.
- Logging: only at boundaries (startup, external I/O, errors). No noisy debug logs in mainline paths.
- Errors: throw or return structured errors; never silently swallow.
- Use descriptive names; avoid abbreviations except well‑known (e.g. `id`, `URL`, `JSON`).

## Commit & PR Guidelines

- Conventional commit style (recommended but not enforced): `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`.
- One logical change per PR. Large refactors split into reviewable steps.
- Reference related issues (e.g. `Closes #123`).
- Include a short rationale in the PR description (why, not just what).
- Mark breaking changes clearly with `BREAKING CHANGE:` section.

## Testing

- Add or update minimal tests for new public behaviors.
- Favor integration-style tests for I/O boundaries; use unit tests for critical pure logic.
- Avoid over-mocking; mock only external services or expensive calls.

## Protocol & Schema Changes

1. Update TypeScript types and JSON Schemas together.
2. Increment version (SemVer). Breaking schema changes => major version.
3. Provide sample payload(s) in the PR description for reviewers.
4. Ensure downstream packages (`sdk`, `connect`, `mcp-server`) still build.

## Performance Considerations

- Measure before optimizing. Provide a brief comment if using a non‑obvious algorithmic trade‑off.
- Keep allocations low in hot paths; prefer streaming for large data.

## Security Practices

- Never log secrets or tokens. Mask or omit sensitive fields.
- Validate untrusted input at boundary layers only.
- Use parameterized queries / safe APIs for any persistence (when added later).

## Documentation

- Update README / usage snippets when adding or changing public APIs.
- Keep docs concise; focus on the why and shape of data.

## Issue Reporting

- Security vulnerabilities: DO **NOT** open a public issue. Email: `security@tinlynk.dev`.
- Bugs: include reproduction steps, expected vs actual, and environment.
- Feature requests: outline use case & success criteria.

## Release Process (High Level)

1. Merge PRs to `main` after approval & CI green.
2. Automated versioning / publishing pipeline (planned) builds & tags artifacts.
3. Changelog updates summarize user‑visible changes.

## Style & Formatting

- Follow existing formatting. Avoid mass reformatting unrelated code.
- No trailing console logs or leftover debug scaffolding.

## Contributor Workflow (Quick Start)

```bash
git clone <repo-url>
cd repo
nvm use 22
npm install
npm run build
```

## FAQ

**Why MIT?** Simplicity and broad adoption; patent concerns handled via community norms.

**Why ESM only?** Modern Node (>=22) supports ESM natively; reduces build complexity and maintenance overhead.

**Can I add CommonJS support?** Only with a strong compatibility case—open an issue first.

## Code of Conduct

Treat all participants with respect. Report unacceptable behavior to `support@tinlynk.dev`.

---
Thank you for helping build TinLynk.