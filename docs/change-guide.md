# Change guide

This guide describes how to modify the repository safely. Each change type lists the affected areas, the steps, and the verification required.

## Decision table

| Change | Affected paths | Risk | Verification |
|--------|----------------|------|--------------|
| Add an override record | One file under `localization/replace/` | Medium | Structural and token checks |
| Edit an override value | One file under `localization/replace/` | Medium | Structural and token checks |
| Add an override file | New file under `localization/replace/` | Medium | Mirror, naming, BOM, header checks |
| Remove an override record | One file under `localization/replace/` | Low | The file must not become empty; delete it if it does |
| Change the mod version | Both descriptors | Low | Both descriptors agree; release tag matches |
| Change `supported_version` | Both descriptors | High | Compatibility review against the game version |
| Rename a content file | File name and possibly the descriptor `path` | High | Engine naming pattern and mirror correspondence |
| Edit a release workflow | `.github/workflows/` | High | Verify identifiers and secrets are unchanged |
| Edit documentation | Root Markdown or `docs/` | Low | Links resolve; prose matches template |

## Adding an override record

1. Open the mirrored override file, or create it if absent (see [flows/override-authoring.md](./flows/override-authoring.md)).
2. Confirm the vanilla key exists and the tracker matches vanilla.
3. Write `KEY:tracker "value"` with the value fully quoted on one line.
4. Confirm every engine token appears in the same order and form as in vanilla.
5. Confirm the new value differs from vanilla.
6. Run the structural and token checks in [testing.md](./testing.md).

## Adding an override file

1. Note the exact vanilla relative path and file name, including any quirk (for example the stray space in `seleukid_missions_events_l_english .yml`).
2. Create the file at the mirrored path with `_latinised` inserted before `_l_english`, encoded as UTF-8 with a BOM.
3. Write the `l_english:` header.
4. Add only the records whose value differs from vanilla.
5. Confirm the file contains at least one record; otherwise do not ship it.

## Editing the descriptors

Both descriptors must stay in agreement. After editing:

1. Diff `latinised-english.mod` against `latinised-english/descriptor.mod`; the files must be identical.
2. Confirm `path` still resolves to `latinised-english/`.
3. Confirm `version` matches the intended release tag.

## Editing the release workflows

1. Preserve the publication identifiers: Workshop item `3843565947`, appid `859580`, Nexus file `8432532`.
2. Preserve the secret names and never inline a secret value.
3. Confirm the archive still contains `latinised-english/` and `latinised-english.mod`.
4. Confirm the Steam upload path is the extracted content directory, not the archive root.

## Editing documentation

1. Keep the root documents' fixed prose intact; only placeholders and evidenced content may change.
2. Keep `docs/` links repository-relative and verify every target exists.
3. Keep coverage figures consistent with a recomputed count.

## Safety rules

- Never edit a vanilla file. The repository overrides; it never modifies the game installation.
- Never place a non-localisation file inside `latinised-english/`, because the engine loads every file it finds.
- Never change a key name to something absent from vanilla; the override would be inert.
- Never reorder, add, or remove an engine token; the consuming string would break.
- Never commit a credential. Publication secrets live in GitHub repository secrets.

## Verification before completion

Every change must satisfy the relevant invariants in [invariants.md](./invariants.md) and pass the checks in [testing.md](./testing.md).
