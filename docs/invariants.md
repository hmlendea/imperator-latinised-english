# Invariants

Invariants are statements that must remain true for the repository to function. Each records the owner, the observable consequence of violation, and the verification method.

## Content invariants

| # | Invariant | Owner | Violation consequence | Verification |
|---|-----------|-------|-----------------------|--------------|
| C1 | Every shipped file is UTF-8 with a BOM | Mod content | The engine may fail to resolve the file; a load warning is written | Inspect the first three bytes (`ef bb bf`) |
| C2 | Every shipped file's first content line is `l_english:` | Mod content | The engine cannot parse the language header | Read the first line |
| C3 | Every shipped file name matches `<name>_latinised_l_english.yml` | Mod content and engine | A name that does not match the pattern is ignored entirely, with no output | Compare against the naming pattern |
| C4 | Every shipped file mirrors a vanilla file at the same relative path | Mod content | The override has no baseline, so keys may not exist and the file has no effect | Map each file to `<game>/localization/english/<vanilla name>` |
| C5 | Every shipped key exists in the corresponding vanilla file | Mod content | An unknown key is inert; it overrides nothing | Key-set comparison against vanilla |
| C6 | Every shipped value differs from its vanilla counterpart | Mod content | A redundant record inflates the diff and carries no information | Value comparison against vanilla |
| C7 | Every shipped record has the shape `key:tracker "value"` with the value fully quoted on one line | Mod content and engine | A malformed record is discarded | Line-level regular-expression check |
| C8 | The tracker number is preserved from vanilla (or set to the vanilla convention) | Mod content | A tracker mismatch can change how the string is interpreted | Compare the tracker against vanilla |
| C9 | Every hover command, variable, text icon, colour code, and `\n` escape appears in the shipped value in the same order and form as in vanilla | Mod content and engine | The string consuming the token renders incorrectly rather than raising an error | Token-sequence comparison against vanilla |

## Descriptor invariants

| # | Invariant | Owner | Violation consequence | Verification |
|---|-----------|-------|-----------------------|--------------|
| D1 | `name`, `version`, `supported_version`, `tags`, and `path` are present in both descriptors | Launcher and Workshop updater | The mod is invisible or misrepresented | Read both descriptors |
| D2 | The two descriptors agree on every field | Launcher and Workshop updater | The mod is listed or published inconsistently | Diff the descriptors |
| D3 | `path` resolves to the content directory (`mod/latinised-english`) | Launcher | The launcher cannot locate the content | Read the field and compare to the directory name |
| D4 | `supported_version` tracks the game version the mod targets | Launcher | The mod is marked incompatible | Compare against the game version |

## Packaging invariants

| # | Invariant | Owner | Violation consequence | Verification |
|---|-----------|-------|-----------------------|--------------|
| P1 | The release archive contains `latinised-english/` and `latinised-english.mod` | Release workflows | Users cannot install the archive | Inspect the archive listing |
| P2 | The Steam Workshop upload path is the content directory, not the archive | Steam workflow | The Workshop item receives a nested or wrong structure | Inspect the workflow `path` input |
| P3 | The Nexus file identifier and Workshop item identifier remain the published ones | Release workflows | The release is uploaded to the wrong item or fails | Compare against the published identifiers |

## Boundary invariants

| # | Invariant | Owner | Violation consequence | Verification |
|---|-----------|-------|-----------------------|--------------|
| B1 | The content directory contains no file the engine cannot parse | Mod content | The loader processes every file it finds, so an unparseable file adds warnings | Enumerate the directory and confirm every file is `.yml` or `.mod` |
| B2 | No repository metadata participates in loading | Repository metadata | A metadata change would alter runtime behaviour | Confirm no descriptor or localisation file references metadata |
| B3 | No ground truth is inferred from naming alone | Maintainer | Incorrect architectural or behavioural claims | Cross-check every claim against a second source |

## Correctness criteria

The repository is correct when, for every shipped record:

```text
key exists in vanilla
AND value != vanilla value
AND token-sequence(shipped value) == token-sequence(vanilla value)
AND encoding is UTF-8 with BOM
AND file mirrors a vanilla path
```

If any conjunct fails for a record, that record is defective. See [testing.md](./testing.md) for the check that evaluates these conjuncts.
