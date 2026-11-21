# Configuration

Configuration for a content-only mod is the descriptor plus the launcher-owned settings that decide whether and how the content loads.

## Configuration areas

| Area | Source | Responsibility | Supersede or secret policy |
|------|--------|----------------|---------------------------|
| Mod identity and target version | `latinised-english.mod`, `latinised-english/descriptor.mod` | Declares the name, version, tags, `supported_version`, and content path the launcher reads | No secrets; `supported_version` must track the game version the mod targets |
| Enablement and load order | Launcher playset | Determines whether the mod loads and its position relative to other mods | Owned by the user; the `replace` subtree makes precedence independent of order |
| Active language | Game settings | Selects which language table is composed | Only `l_english` records are shipped, so the overrides apply to English play only |

## Descriptor fields

The descriptor is the only file the repository controls that affects loading. See [components/mod-descriptor.md](./components/mod-descriptor.md) for the field reference.

| Key | Type | Value | Required | Effect |
|-----|------|-------|----------|--------|
| `name` | string | `Latinised English` | Yes | The display name the launcher lists |
| `version` | string | `1.0.0` | Yes | The version listed and published |
| `supported_version` | string | `2.0.*` | Yes | Compatibility range |
| `tags` | list | `Interface` | No | The category the mod appears under |
| `path` | string | `mod/latinised-english` | Yes | The content root relative to the Imperator user data directory |

## Precedence

There is no layered configuration. The only precedence that matters is filesystem-level between localisation sources:

1. `localization/replace` subtree — highest, applied last;
2. mod default localisation trees — applied in playset order;
3. vanilla `localization/english` — baseline.

Placing a record under `replace` is therefore the entire configuration lever the repository has over precedence.

## Reload behaviour

Configuration is read at launcher start and at game start. Changing descriptor fields requires restarting the launcher or the game; there is no hot reload. Changing a localisation value requires restarting the game.

## Validation

To validate effective configuration:

1. The launcher lists **Latinised English** at the declared version and supported version.
2. An overridden string renders the override rather than the vanilla wording.
3. `error.log` contains no encoding or parse warning naming a shipped file.

## Secrets

None. The mod handles no credentials and reads no configuration containing secrets. Steam and Nexus credentials used for publication are GitHub repository secrets, not mod configuration. See [components/packaging-and-distribution.md](./components/packaging-and-distribution.md).
