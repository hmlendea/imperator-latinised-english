# Mod content

The mod content is the entire product of the repository: a tree of English localisation override files plus the descriptor that names the content root.

## Location

```text
latinised-english/descriptor.mod
latinised-english/localization/replace/            # 127 root-level files
latinised-english/localization/replace/deities/    # 23 files
latinised-english/localization/replace/missions/   # 3 files
```

Total: 153 override files carrying 8,691 records.

## Responsibilities

- Carry every localisation override record, expressed as an `l_english` key and value pair.
- Preserve the vanilla relative file name for each override, with the `_latinised` marker inserted before the language suffix.
- Ship only records whose value differs from vanilla.

## Record shape

A shipped file begins with a UTF-8 BOM followed by the header line, then indented records:

```text
l_english:
 ALERT_AT_WAR_WITH:0 "#T Armed Conflict#!\nWe are currently at war with $DATA$."
 ALERT_CIVIL_WAR:0 "#T Civil War#!\nWe are currently fighting a Civil War..."
```

| Part | Meaning |
|------|---------|
| `l_english:` | Language header, first content line of every file |
| `KEY` | The vanilla key being overridden, preserved from the vanilla file |
| `:0` | The tracker number, preserved from vanilla; observed values range from `:0` to `:7`, with `:0` dominating (7,198 of 8,691) |
| `"value"` | The replacement value, fully quoted on a single line |

Verified properties of the current corpus:

- 153 of 153 files begin with a BOM;
- 153 of 153 files begin with `l_english:`;
- 0 files are empty;
- 0 records span more than one line;
- 8,691 records match the `key:tracker "value"` shape.

## Engine tokens inside values

Values embed engine constructs that must be preserved exactly. Observed token classes and their frequency:

| Token class | Form | Example | Observed count |
|-------------|------|---------|----------------|
| Scope switch | `[SCOPE...]` | `[SCOPE.general.GetName]` | 2,549 |
| Root scope | `[ROOT...]` | `[ROOT.GetName]` | 891 |
| Data function | `[GetXxx...]` | `[GetCountry]` | many |
| Variable | `$NAME$` | `$DATA$`, `$COUNTRY$` | many |
| Colour open/close | `#T ...#!`, `#Y ...#!` | `#T Armed Conflict#!` | many |
| Text icon | `@trigger_no!` | `@trigger_no!` | present |
| Hover command | `[X]` | `[GetDefine( 'NProvince', 'REVOLT_LOYALTY_THRESHOLD' )|0R]` | present |
| Literal newline | `\n` | `\n` | many |

A substitution may change words around a token but never the token itself. See [invariants.md](../invariants.md) invariant C9.

## Boundaries

- Every override must live under `localization/replace/`, because that subtree is what guarantees precedence over vanilla and over other mods' default-tree localisation.
- `descriptor.mod` must remain at the content root; the launcher uses it to update a published mod.
- The content directory must contain no file the engine cannot parse, because the loader processes every file it finds.

## Files that ship nothing

Three vanilla files hold no records and therefore cannot be shipped: `hints_l_english.yml`, `newtexts_l_english.yml`, and `oldeffects_l_english.yml`. Proper-noun-only files such as `provincenames_l_english.yml` also ship nothing, because their words are proper-noun components rather than vocabulary.

## Dependants

The content is consumed by:

- the Imperator: Rome engine, through `localization/replace` merge precedence;
- the release workflows, which archive the content directory and its descriptor;
- the steam-workshop workflow, which uploads the content directory to the Workshop item.

## Modification impact

Editing a value affects only the rendered string for that key. Editing a key name breaks the override, because the key must match vanilla. Editing a file name breaks both the engine pattern match and the mirror correspondence. See [change-guide.md](../change-guide.md).
