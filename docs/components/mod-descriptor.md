# Mod descriptor

The repository ships two descriptors with identical content. They declare the mod identity and content location for two different readers.

## Location and content

`latinised-english.mod` (repository root):

```text
version="1.0.0"
tags={
        "Interface"
}
name="Latinised English"
supported_version="2.0.*"
path="mod/latinised-english"
```

`latinised-english/descriptor.mod` (content root): byte-identical to the above.

## Field reference

| Field | Value | Reader | Consequence |
|-------|-------|--------|-------------|
| `version` | `1.0.0` | Launcher, Workshop updater | The version the launcher lists and the Workshop updater publishes |
| `tags` | `{ "Interface" }` | Launcher | The category the mod appears under |
| `name` | `Latinised English` | Launcher, Workshop updater | The display name the launcher lists |
| `supported_version` | `2.0.*` | Launcher | Compatibility range; a mismatch marks the mod incompatible |
| `path` | `mod/latinised-english` | Launcher | The content root, relative to the Imperator user data directory |

## Why two files

| Descriptor | Purpose |
|------------|---------|
| `latinised-english.mod` | Registers the mod when the repository is used as a local mod; the launcher lists it before publication |
| `latinised-english/descriptor.mod` | The content-root descriptor the Workshop updater and the release workflows read when publishing |

The root descriptor is what makes the repository usable as a local mod without publication. The content-root descriptor is what the packaging and publication chain reads.

## Invariants

The two descriptors must agree on every field. A mismatch misrepresents the mod in whichever context reads the divergent file. See [invariants.md](../invariants.md) invariants D1 and D2.

`path` must resolve to the content directory. The release workflows depend on the same directory name: both `github-release.yml` and `steam-workshop-release.yml` archive `latinised-english/` and `latinised-english.mod`.

## Change policy

| Field | Change policy |
|-------|---------------|
| `version` | Rises with each published release; the release workflow strips a leading `v` from the tag for the archive name |
| `supported_version` | Changes only with a compatibility review against the game version |
| `name`, `tags`, `path` | Stable; changing `path` requires a matching change in the workflows and the directory name |

## Failure semantics

An unreadable or mislocated descriptor makes the mod invisible: the launcher skips it without an in-game error. A descriptor whose `path` does not resolve leaves the content undiscoverable even though the files exist.
