# State and persistence

The repository owns no state. This document records why, and what transactional state exists at runtime and where it is owned.

## Owned state

None. The repository contains only:

- static localisation files;
- static descriptors;
- documentation, licence, and artwork;
- CI workflow definitions.

No file is mutated by the game, and no file records runtime state.

## Runtime state ownership

Any state that exists at runtime is owned by the engine, not the repository:

| State | Owner | Representation | Lifecycle |
|-------|-------|----------------|-----------|
| Composed language table | Engine | In-memory map from key to resolved value | Rebuilt on every load; lost on exit |
| Enabled playset and order | Launcher | Launcher settings | Persists across sessions; owned by the user |
| Active language selection | Game settings | Game configuration | Persists across sessions; owned by the user |
| Engine log | Engine | `<user data>/Imperator/logs/error.log` | Engine-managed |

## Why there is no persistence concern

| Property | Consequence |
|----------|-------------|
| Data is static | There is no migration, no schema version, no write path |
| State is rebuilt per load | There is no cache invalidation problem |
| No external store | There is nothing to back up or restore |
| No identifiers written | There is nothing to reconcile across releases |

## Installation state

The one persistent artifact the repository causes is the installed mod directory:

```text
<Imperator user data>/mod/latinised-english/
<Imperator user data>/mod/latinised-english.mod
```

Replacing an installation requires deleting both first, because the game loads every file present in the mod directory and a leftover file from a previous version collides with the new one. See [troubleshooting.md](./troubleshooting.md).

## Recovery

Recovery is total: deleting the mod directory and descriptor returns the game to its vanilla state, because the mod owns no external state and mutates nothing outside its own files.
