# Error handling

Failures originate in the engine and the launcher, not in the repository, and they are silent or near-silent. The repository cannot catch a failure at runtime; it prevents one by validating every shipped value against its vanilla counterpart.

## Failure taxonomy

| # | Failure | Origin | Detectability | Effect |
|---|---------|--------|---------------|--------|
| E1 | Descriptor unreadable or mislocated | Launcher | Silent | The mod is invisible in the mod list |
| E2 | `path` does not resolve to the content directory | Launcher | Silent | The content is undiscoverable |
| E3 | File name does not match `<name>_l_english.yml` | Engine | Silent | The file is ignored entirely |
| E4 | File missing its BOM | Engine | Warning in `error.log` | The file may fail to resolve |
| E5 | Header line is not `l_english:` | Engine | Warning or silent | The language header cannot be parsed |
| E6 | Malformed record (`key:tracker "value"` violated) | Engine | Possibly silent | The record is discarded |
| E7 | Override key not present in vanilla | Engine | Silent | The record overrides nothing |
| E8 | Value contains an altered engine token | Engine | Silent or misrendered | The consuming string renders incorrectly |
| E9 | Value identical to vanilla | None | Silent | The record is inert and inflates the diff |
| E10 | Duplicate key within one file | Engine | Engine-defined | Typically the last record wins |
| E11 | Vanilla key removed by a game update | Engine | Silent | The override overrides nothing |

## Handling pattern

Because failure detection is weak, the repository's error strategy is **prevention at authoring time** rather than recovery at runtime:

```text
author value
  -> compare key against vanilla            (prevents E7)
  -> compare value against vanilla          (prevents E9)
  -> compare token sequence against vanilla (prevents E8)
  -> verify BOM and header                  (prevents E4, E5)
  -> verify file mirror and name            (prevents E3)
  -> verify record shape and uniqueness     (prevents E6, E10)
```

## Why prevention is the only option

| Reason | Consequence |
|--------|-------------|
| No runtime component | The repository cannot intercept or repair a failure |
| No assertion surface | The engine exposes no programmatic error signal |
| Silent failures | An altered key or token produces no diagnostic |
| Vanilla drift | A game update can invalidate a record without any signal |

## Recovery

Recovery is total and repository-side:

- **Disable the mod**: recovers everything instantly, because the mod owns no external state.
- **Delete the mod directory and descriptor**: removes every trace.
- **Revert a defective record**: edit the value back to the vanilla value, or remove the record entirely.

## Escalation

When a string does not change as expected, distinguish the E-cases in order:

1. Confirm the mod is enabled and the workspace is English (E1, E2).
2. Confirm the file is present, correctly named, and BOM-encoded (E3, E4, E5).
3. Confirm the key is shipped and matches vanilla (E6, E7, E10).
4. Confirm the token sequence matches vanilla (E8).
5. Confirm the value differs from vanilla (E9).

See [troubleshooting.md](./troubleshooting.md) for the diagnostic procedure.
