# Repository overview

## Purpose

The repository exists to supply a set of English localisation override files that replace selected vanilla Imperator: Rome strings with latinisations. A latinisation is one of three changes, applied by a maintainer:

1. a British spelling replacing a Germanic- or Latin-American-style variant;
2. a word of Latin ancestry replacing a word of Germanic ancestry that carries the same sense;
3. a context-sensitive substitution chosen from the `english-language` vocabulary rules for the sense actually in use in the string.

The mod is a data package. It owns no executable code and defines no runtime. The product is the file tree the game engine reads.

## Scope

The repository owns:

- the localisation override corpus under `latinised-english/localization/replace/`;
- the two descriptors that declare the mod identity and content path;
- the release automation that packages and publishes the corpus;
- the documentation that describes all of the above.

## Deliberate non-scope

The repository does **not** own:

- the game engine, its parser, its merge precedence, or its renderer;
- the vanilla localisation corpus that supplies the baseline keys and file names;
- the launcher, playset, or load order;
- any state, cache, database, or persistence;
- any network communication or credential handling;
- the `english-language` vocabulary rules themselves, which are an authoring input rather than shipped content.

## Entry points

There is no process entry point. The integration entry points are files:

| Entry point | Reader | Purpose |
|-------------|--------|---------|
| `latinised-english.mod` | Paradox launcher | Registers the mod when the repository is used as a local mod |
| `latinised-english/descriptor.mod` | Paradox launcher and Steam Workshop updater | Declares identity, version, supported game version, tags, and content path |
| `latinised-english/localization/replace/*.yml` | Imperator: Rome engine | Carries every override record |
| `.github/workflows/*.yml` | GitHub Actions | Packages and publishes releases |

## Boundary in one sentence

The boundary is the content directory and its descriptor: everything inside `latinised-english/` is loaded by the game, and nothing outside it executes.

## Success criteria

The repository is functioning correctly when:

- the launcher lists **Latinised English** at version `1.0.0` with supported version `2.0.*`;
- an enabled playset containing the mod renders the overridden strings instead of the vanilla wording;
- every shipped file parses without an encoding or parse warning in `error.log`;
- every shipped record differs from its vanilla counterpart and preserves every engine token in order.

See [invariants.md](./invariants.md) for the enforceable form of these criteria.
