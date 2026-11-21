# Localisation override behaviour

This document describes what a user observes when the mod is enabled, in user-facing terms. The mechanism is documented in [flows/localisation-override-resolution.md](../flows/localisation-override-resolution.md).

## The observed behaviour

When the mod is enabled in a playset and English is the active language, selected interface strings render with latinisable wording instead of the vanilla wording. Four classes of change are visible:

| Class | Example |
|-------|---------|
| British spelling | A vanilla American-style spelling renders with the British equivalent |
| Latin-ancestry vocabulary | A Germanic-ancestry word renders with a Latin-ancestry synonym |
| Context-sensitive substitution | A word renders with the sense-appropriate alternative for its sentence |
| Heading and label rewording | Interface headings such as the war alert read `Armed Conflict` instead of the vanilla wording |

## What is preserved

The mod changes only words. Every engine construct inside a value continues to resolve:

- hover commands still open their tooltip;
- variables such as `$DATA$` still substitute;
- text icons still render;
- colour codes still apply;
- literal `\n` escapes still break the line.

A user therefore sees a fully functional tooltip with different wording, never a broken string.

## Scope of the visible effect

The effect applies anywhere the overridden key is displayed: alert headings, event text, decision text, tooltips, modifier descriptions, mission text, and so on. The mod is not restricted to a single screen.

## What is not overridden

Most in-game text remains unchanged, because coverage is partial by design. A string is overridden only when:

1. its file is among the shipped override files;
2. its key is present in that file; and
3. a latinisable substitution exists that preserves the original meaning and grammar.

A string left at vanilla is a correct outcome, not a defect. See [design-decisions.md](../design-decisions.md) for why partial coverage is intentional.

## Behavioural consequences of enabling the mod

| Consequence | Detail |
|-------------|--------|
| Checksum changes | Enabling any localisation override changes the game checksum |
| Achievements disabled | A changed checksum disables achievements |
| Ironman risk | Loading an ironman save with a checksum-changing mod can make the save unplayable |
| Other language tables unaffected | Only `l_english` records are shipped, so the overrides apply to English play only |

## Interaction with other mods

Another mod that overrides the same key competes with this mod. Because the overrides live under `localization/replace`, they win over default-tree localisation regardless of load order, but two mods both placing a record under `replace` resolve by load order. Place this mod after any localisation mod it should supersede.
