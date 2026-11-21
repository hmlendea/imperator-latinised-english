# Localisation

The repository is itself a localisation resource. It ships only the English language and only the records it overrides.

## Locale coverage

| Language | Locale | Status |
|----------|--------|--------|
| English | `l_english` | Partial, expanded file by file |

No other language is shipped. A game running in a language other than English is unaffected by this mod, because only `l_english` records are present.

## Coverage figures

| Metric | Value |
|--------|-------|
| Override files shipped | 153 |
| Override records shipped | 8,691 |
| Vanilla files in the baseline | 176 |
| Vanilla records in the baseline | 62,528 |
| Approximate record coverage | 14% |

The vanilla corpus comprises 150 files at the `localization/english` root, 23 under `deities/`, and 3 under `missions/`.

## Coverage by directory

| Override directory | Files | Notes |
|--------------------|-------|-------|
| `replace/` (root) | 127 | Interface, events, missions, modifiers, and everything else |
| `replace/deities/` | 23 | Deity names and faith-flavour text |
| `replace/missions/` | 3 | Diadochi and Seleukid mission trees |

## Files that ship nothing

Three vanilla files hold no records and therefore cannot be shipped: `hints_l_english.yml`, `newtexts_l_english.yml`, and `oldeffects_l_english.yml`. They contain only separators or blank lines.

Proper-noun-only files also ship nothing. `provincenames_l_english.yml` holds only place names (`Upper Epirus`, `Great Kavir`, `High Atlas`, `Side`), so the dictionary words `upper`, `great`, `high`, and `side` are proper-noun components there, not vocabulary.

## Locale identifier use

The header line `l_english:` in every file declares the locale. The engine recognises the file by the `_l_english.yml` suffix. The `_latinised` marker sits before that suffix so the override stays distinct from the vanilla file while remaining discoverable.

## Contributing translations

There is no translation contribution process, because the project is not a translation. It authors English substitutions and ships only English. A contribution to a different language would be a different project. See [CONTRIBUTING.md](../CONTRIBUTING.md).
