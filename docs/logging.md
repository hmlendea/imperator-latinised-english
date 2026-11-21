# Logging

The repository emits no logs. The only logging surface is the Imperator: Rome engine's own log, which is the sole diagnostics channel available for this mod.

## Logging framework

| Property | Detail |
|----------|--------|
| Producer | Imperator: Rome engine; the repository produces nothing |
| Destination | `<user data>/Imperator/logs/error.log` |
| Format | Engine-defined plain text |
| Configuration | Owned by the game, not the repository |

## What the engine logs for this mod

| Event | Log behaviour |
|-------|---------------|
| File missing its BOM | A load warning is written |
| Value with an invalid token | Rendered incorrectly rather than raising an error; may be silent |
| File name not matching the localisation pattern | The file is ignored entirely, with no output at all |
| Malformed record | The record is discarded |
| Duplicate key within a file | Engine-defined; generally the last record wins |

## Diagnostic gap

The practical diagnostic gap is that a suppressed substitution is invisible:

- an override that was never authored, and
- an override that was authored but not loaded,

both present as unchanged vanilla text. The log does not distinguish them, because neither produces an error. Distinguishing them requires reading the shipped files rather than observing the game. See [troubleshooting.md](./troubleshooting.md).

## What is not logged

| Absent signal | Reason |
|---------------|--------|
| Application logs | There is no application |
| Metrics or counters | There is no runtime to instrument |
| Traces or correlation IDs | There is no request flow |
| Health checks | There is no service |
| Audit log | The mod performs no security-relevant action |

## Verification use

The log has one positive verification use: after enabling the mod and launching the game, reading `<user data>/Imperator/logs/error.log` and confirming that no encoding or parse warning names a shipped file confirms the corpus loaded cleanly.
