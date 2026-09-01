# Minecraft Remote Protocol

> **Parked bootstrap — not the active owner.** This repository was created as
> a migration candidate and is currently frozen. The active executable
> projection and shared-fixture owner remains
> `Naohiro2g/scratch-editor:mc-remote/protocol`. Do not issue successor
> fixtures, switch consumers, or treat this repository as a b7 release input.

Executable projections and shared conformance fixtures for the Minecraft Remote
wire protocol.

This repository contains an exact candidate bootstrap of the dependency-free
TypeScript package `@mc-remote/protocol` and its machine-readable fixtures. It
does not currently own them.

The human-readable protocol source of truth remains
[`mc-remote-knowledge/10-protocol`](https://github.com/Naohiro2g/mc-remote-knowledge/tree/main/10-protocol).
No contract or product changes are accepted while this bootstrap is parked.

## Commands

```sh
npm ci
npm test
npm run build
```

## Fixtures

Fixtures live in `test/fixtures/`. A consumer claiming shared conformance records
the owner commit, path, byte size, and SHA-256, then consumes those exact bytes.
Copying a fixture into a language-specific test-resource directory is allowed;
changing values or maintaining an independent replacement is not.

The imported Protocol 23.1 predecessor fixture is
`test/fixtures/direction-lightning-v23.1.json`. Its imported bytes match
`scratch-editor@607cda40588ec4579c503d457c3784385419ac65` at
`mc-remote/protocol/test/fixtures/direction-lightning-v23.1.json`. A successor
revision remains the responsibility of the active Scratch owner for b7.

## Boundaries

- This parked repository owns no active product or contract surface.
- A post-b7 review will evaluate Protocol, conformance, WireScope, Bridge, and
  TCP/browser connectivity together. A shared TypeScript-tooling monorepo is a
  strong candidate; the final topology is not decided.
- Runtime compatibility is negotiated through the protocol version in `hello`,
  not inferred from a shared source-code dependency.
- The npm package remains private until publication and versioning are separately
  approved. Consumers may pin a Git commit and fixture digest.

See [MIGRATION_ja.md](MIGRATION_ja.md) for bootstrap provenance and park status.
