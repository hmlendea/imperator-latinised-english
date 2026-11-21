# Repository structure

## Tree

```text
imperator-latinised-english/
├── .github/
│   ├── cover.png                     # Repository landing-page artwork
│   └── workflows/
│       ├── github-release.yml        # GitHub Release packaging and attachment
│       ├── nexus-mods-release.yml    # Nexus Mods publication
│       └── steam-workshop-release.yml# Steam Workshop publication
├── .temp/                            # Ignored working directory (not shipped)
│   └── vanilla_files.md              # Vanilla corpus inventory and coverage tally
├── description/
│   └── steam-workshop.bbcode         # Steam Workshop page body
├── latinised-english/
│   ├── descriptor.mod                # Mod content descriptor
│   └── localization/
│       └── replace/                  # All English overrides
│           ├── *.yml                 # 127 root-level override files
│           ├── deities/              # 23 deity-name override files
│           └── missions/             # 3 mission override files
├── latinised-english.mod             # Local-mod descriptor (launcher)
├── ARCHITECTURE.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
├── PRIVACY.md
├── README.md
└── SECURITY.md
```

## Directory inventory

| Directory | Files | Purpose |
|-----------|-------|---------|
| `latinised-english/localization/replace/` | 127 | Root-level English override files |
| `latinised-english/localization/replace/deities/` | 23 | Deity-name and faith-flavour overrides |
| `latinised-english/localization/replace/missions/` | 3 | Mission-tree overrides |
| `.github/workflows/` | 3 | Release automation |
| `.temp/` | 1 | Ignored coverage-tracking notes |

Total shipped override files: **153**, carrying **8,691** records. The vanilla corpus contains 176 files and 62,528 records, so the shipped set covers approximately 14% of the baseline record count.

## Naming convention

Every override mirrors its vanilla source at the same relative path, with the `_latinised` marker inserted before the `_l_english` suffix:

```text
vanilla:  localization/english/alerts_l_english.yml
override: latinised-english/localization/replace/alerts_latinised_l_english.yml
```

The marker keeps the file name distinct from the vanilla name while leaving the engine-recognised `_l_english.yml` pattern intact. The mirror correspondence is mechanical and is not recorded anywhere else.

One vanilla file, `missions/seleukid_missions_events_l_english .yml`, contains a stray space before the extension. The override preserves it exactly as `missions/seleukid_missions_events_latinised_l_english .yml`.

## Files that do not exist

The repository deliberately contains none of the following, and their absence is not an omission:

- build manifests, package manifests, or compilation scripts;
- test projects or test runners;
- runtime source code in any language;
- a `docs/` API reference, because there is no API;
- a `ROADMAP.md` or `CHANGELOG.md`.

## Ignored working data

`.temp/vanilla_files.md` holds an inventory of all 176 vanilla files with a per-file override count and a grand total. It is excluded from the repository by `.gitignore` (`.temp/`) and is a maintainer workspace artifact rather than shipped content.
