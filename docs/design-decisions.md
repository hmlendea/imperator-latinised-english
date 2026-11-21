# Design decisions

Each decision records the choice, the evidence that it is the current state, and its consequences.

## Content-only package with no executable component

**Decision.** Ship nothing that executes. The mod is localisation data and a descriptor.

**Rationale.** Imperator: Rome localisation overrides require no code. Introducing code would add a build step, a runtime, and a failure surface with no benefit.

**Consequence.** The repository cannot compute a substitution; every change must be expressible as a static record. This bounds the type of change the project can ever ship.

## Path mirroring with a `_latinised` marker

**Decision.** Each override sits at the vanilla relative path with `_latinised` inserted before the language suffix.

**Rationale.** The correspondence between a vanilla file and its override becomes mechanical rather than recorded in an index. The marker keeps the override distinct from the vanilla file name while preserving the engine-recognised `_l_english.yml` pattern.

**Consequence.** A renamed vanilla file invalidates the mirror, so file names are dictated by the installation rather than by the repository. The stray space in `seleukid_missions_events_latinised_l_english .yml` is preserved for this reason.

## Minimal override sets

**Decision.** Ship only records whose value differs from vanilla.

**Rationale.** A record identical to vanilla carries no information and inflates the diff. Shipping only differences makes the override set reviewable and keeps the mod's change surface equal to its diff against vanilla.

**Consequence.** Absence of an override is indistinguishable from a deliberate suppression without reading the files. There is no metadata recording why a record was left alone.

## Placement under `localization/replace`

**Decision.** Every override lives under `localization/replace/`.

**Rationale.** The `replace` subtree is applied after every other localisation source, so a record placed there wins over a duplicate key in the vanilla tree or in another mod's default tree without depending on file order or playset position.

**Consequence.** The repository's only lever over precedence is placement. A record placed anywhere else would be order-dependent.

## Authoring by judgement rather than mechanical substitution

**Decision.** Apply substitutions individually against the vocabulary record that covers the sense in use.

**Rationale.** A mechanical whole-word pass produces ungrammatical results, such as a plural verb form substituted into a nominal position. Semantic accuracy requires reading the string.

**Consequence.** Coverage is partial by design and the effort scales with the corpus. Records carry no mechanical provenance; a reviewer must compare the pair to understand the change.

## Preserved engine token sequences

**Decision.** Never reorder, add, or remove a hover command, variable, text icon, colour code, or `\n` escape.

**Rationale.** The consuming string depends on the token sequence. A reordered or dropped token renders incorrectly rather than failing loudly.

**Consequence.** Rewrites that reflow a span are prohibited even when they read better. This is the single most common reason a candidate substitution is rejected.

## Two descriptors with identical content

**Decision.** Ship both `latinised-english.mod` (repository root) and `latinised-english/descriptor.mod` (content root) with the same fields.

**Rationale.** The launcher lists a local mod from the root descriptor, while the content-root descriptor is what the Workshop updater reads when publishing and what the release workflows archive.

**Consequence.** The two must stay in sync; a mismatch misrepresents the mod in one of the two contexts. See [components/mod-descriptor.md](./components/mod-descriptor.md).

## No automated test suite

**Decision.** Verification is manual and comparative against the vanilla source.

**Rationale.** There is no test runner and the engine exposes no assertion surface. The verifiable boundary is the pair of a shipped override and its vanilla source.

**Consequence.** No regression is caught without running the check. A documented shell check performs the structural part of the verification. See [testing.md](./testing.md).

## Coverage tracked outside the repository

**Decision.** Keep the vanilla corpus inventory in `.temp/vanilla_files.md`, which is git-ignored.

**Rationale.** It is a maintainer workspace artifact derived from an installed game, not shipped content.

**Consequence.** The coverage tally is not versioned, so it can drift from the shipped corpus. Every metric in this documentation was recomputed from the shipped files rather than trusted from that file.
