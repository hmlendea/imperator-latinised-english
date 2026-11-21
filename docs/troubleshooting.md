# Troubleshooting

Recurring problems and their resolutions. The repository cannot catch a failure at runtime, so diagnosis proceeds by eliminating the candidate causes in order.

## Diagnostic procedure

```mermaid
flowchart TD
  Start["A string did not change"] --> E1{"Mod enabled and<br/>language is English?"}
  E1 -->|"no"| F1["Enable the mod;<br/>select English"]
  E1 -->|"yes"| E2{"File present and<br/>named correctly?"}
  E2 -->|"no"| F2["Check the mirrored name<br/>and the replace path"]
  E2 -->|"yes"| E3{"BOM and header correct?"}
  E3 -->|"no"| F3["Re-encode UTF-8 with BOM;<br/>restore the header"]
  E3 -->|"yes"| E4{"Key shipped and<br/>matches vanilla?"}
  E4 -->|"no"| F4["Correct or add the key"]
  E4 -->|"yes"| E5{"Token sequence<br/>matches vanilla?"}
  E5 -->|"no"| F5["Restore the token order"]
  E5 -->|"yes"| E6{"Value differs<br/>from vanilla?"}
  E6 -->|"no"| F6["Author a differing value<br/>or remove the record"]
  E6 -->|"yes"| F7["Check error.log and<br/>load order with other mods"]
```

## Problems

| Symptom | Probable cause | Resolution |
|---------|----------------|------------|
| The mod does not appear in the launcher | Descriptor missing, unreadable, or mislocated | Confirm `latinised-english.mod` and `latinised-english/descriptor.mod` exist and parse |
| The mod appears but has no effect | The content path does not resolve | Confirm `path="mod/latinised-english"` matches the installed directory name |
| A string is unchanged | The key is not shipped | Confirm the record exists in the mirrored override file |
| A string is unchanged | The value equals vanilla | Author a differing value or remove the redundant record |
| A string is unchanged | Another localisation mod wins | Place this mod after the competing mod; both using `replace` resolves by load order |
| A string renders incorrectly (broken tooltip) | An engine token was altered, dropped, or reordered | Restore the token sequence to match vanilla |
| A tooltip shows a raw token or placeholder | A malformed token in the value | Compare against vanilla and repair the token |
| The file loaded but nothing changed | A key not present in vanilla | Correct the key to match the vanilla key |
| A load warning names a shipped file | Missing BOM or invalid encoding | Re-encode the file as UTF-8 with a BOM |
| The game warns and the file is ignored | File name does not match `_l_english.yml` | Rename to mirror the vanilla file with the `_latinised` marker |
| Duplicate-key behaviour (only one value applies) | The key appears more than once in a file | Remove the duplicate record |
| Old content persists after updating | Leftover files from the previous version | Delete the `latinised-english` directory and `latinised-english.mod`, then reinstall |
| Achievements are disabled | The mod changes the checksum | Inherent to localisation overrides; disable the mod for achievement runs |
| An ironman save will not load | A checksum-changing mod on an ironman campaign | Do not enable the mod on ironman campaigns |

## Interpreting the log

Read `<user data>/Imperator/logs/error.log` after launching the game:

| Log entry | Meaning |
|-----------|---------|
| An encoding warning naming a file | That file lacks a BOM or has invalid encoding |
| A parse warning naming a file | A record in that file is malformed |
| No warning | The corpus loaded cleanly; a missing substitution is authoring-side, not load-side |

## Distinguishing absence from suppression

The hardest diagnostic case is a string that is unchanged by design versus one whose override failed to load. Both look identical in game. Resolve it by reading the shipped files:

1. Locate the vanilla file and its mirrored override.
2. Search the override for the key.
3. If the key is absent, the string was deliberately left unchanged.
4. If the key is present, the override exists and the problem is elsewhere in the diagnostic tree.
