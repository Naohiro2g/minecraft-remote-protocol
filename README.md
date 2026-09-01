# Minecraft Remote Protocol

Executable projections and shared conformance fixtures for the Minecraft Remote
wire protocol.

This repository owns the dependency-free TypeScript package
`@mc-remote/protocol` and the machine-readable fixtures consumed by McRemote,
Minecraft Remote for Python, Scratch Client, Java Client Library, and future
independent implementations.

The human-readable protocol source of truth remains
[`mc-remote-knowledge/10-protocol`](https://github.com/Naohiro2g/mc-remote-knowledge/tree/main/10-protocol).
Changes here project an approved contract; they do not independently define new
wire behavior.

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

Protocol 23.1's predecessor fixture is
`test/fixtures/direction-lightning-v23.1.json`. Its imported bytes match
`scratch-editor@607cda40588ec4579c503d457c3784385419ac65` at
`mc-remote/protocol/test/fixtures/direction-lightning-v23.1.json`. A successor
revision will incorporate the approved session-permission contract before b7
release.

## Boundaries

- This repository does not own Scratch blocks, Bridge, WireScope, McRemote
  handlers, or language-specific Client APIs.
- Runtime compatibility is negotiated through the protocol version in `hello`,
  not inferred from a shared source-code dependency.
- The npm package remains private until publication and versioning are separately
  approved. Consumers may pin a Git commit and fixture digest.

See [MIGRATION_ja.md](MIGRATION_ja.md) for the ownership transfer record.
