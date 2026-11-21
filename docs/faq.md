# FAQ

## What does the mod do?

It replaces selected vanilla Imperator: Rome English strings with latinisations: British spellings, Latin-ancestry vocabulary, and context-sensitive substitutions. See [behaviour/localisation-override.md](./behaviour/localisation-override.md).

## Does it change any gameplay?

No. It changes displayed text only. No rule, value, unit, or mechanic is affected.

## Why is most of the text unchanged?

Coverage is partial by design. A string is overridden only when a latinisable substitution exists that preserves the original meaning and grammar. An unchanged string is a correct outcome, not a defect. See [design-decisions.md](./design-decisions.md).

## Why does enabling the mod disable achievements?

Any localisation override changes the game checksum, and a changed checksum disables achievements. This is inherent to localisation overrides and cannot be designed around.

## Can I use it on an ironman save?

It is strongly discouraged. Loading an ironman save with a checksum-changing mod can make the save unplayable. Disable the mod before starting an ironman campaign.

## Which game versions are supported?

Imperator: Rome `2.0.*`, declared as `supported_version` in the descriptors. See [dependencies.md](./dependencies.md).

## Where is the mod installed?

Into the Imperator mod directory:

- GNU/Linux: `~/.local/share/Paradox Interactive/Imperator/mod/`
- Windows and macOS: `~/Documents/Paradox Interactive/Imperator/mod/`

## How do I update it?

Delete the previous `latinised-english` directory and `latinised-english.mod` file, then reinstall. The game loads every file present, so a leftover file from a previous version collides with the new one.

## Can I translate it into another language?

No. The project is not a translation; it authors English substitutions and ships only English. A different language would be a different project. See [localisation.md](./localisation.md).

## Will it conflict with other mods?

Another mod that overrides the same key competes with this one. Because the overrides live under `localization/replace`, they win over default-tree localisation regardless of load order, but two mods both placing a record under `replace` resolve by load order. Place this mod after any localisation mod it should supersede.

## Why is a particular word not changed?

Possibilities, in order of likelihood: the word is a proper noun; the vocabulary record targets a different sense; the substitution would drop or reorder an engine token; or the file is not yet covered. See [troubleshooting.md](./troubleshooting.md).

## How do I contribute an override?

See [flows/override-authoring.md](./flows/override-authoring.md) and [CONTRIBUTING.md](../CONTRIBUTING.md).

## Is my data collected?

No. The mod has no runtime component, performs no network communication, and handles no personal data. See [security.md](./security.md) and the root [PRIVACY.md](../PRIVACY.md).

## Where do I report a problem?

[Open an issue](https://github.com/hmlendea/imperator-latinised-english/issues). For security matters, use the process in [SECURITY.md](../SECURITY.md).
