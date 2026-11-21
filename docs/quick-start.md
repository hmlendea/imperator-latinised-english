# Quick start

## Install the mod

Pick a distribution channel:

There is no package-manager route. Choose one of the following.

**Steam Workshop:** subscribe through the [Workshop page](https://steamcommunity.com/sharedfiles/filedetails/?id=3843565947). The launcher downloads and maintains the mod automatically.

**Nexus Mods:** download from [nexusmods.com/imperatorrome/mods/35](https://nexusmods.com/imperatorrome/mods/35) and follow the site's mod-manager instructions.

**GitHub Releases:** download `latinised-english_<version>.zip` from the [releases page](https://github.com/hmlendea/imperator-latinised-english/releases) and extract it manually.

## Manual installation

1. Obtain the repository contents, either by cloning them or by downloading an archive.
2. Place the `latinised-english` directory and the `latinised-english.mod` descriptor file into the Imperator: Rome mod directory.
3. Select **Latinised English** in the launcher Mods tab.

The mod directory is located at:

- GNU/Linux: `~/.local/share/Paradox Interactive/Imperator/mod/`
- Windows and macOS: `~/Documents/Paradox Interactive/Imperator/mod/`

When replacing an existing installation, delete the previous `latinised-english` directory and `latinised-english.mod` file first, because the game loads every file present in the mod directory.

## Verify the installation

1. Open the launcher Mods tab and confirm **Latinised English** appears at version `1.0.0` and that its enabled state survives a launcher restart.
2. Launch the game and confirm an affected string shows the overridden wording. A reliable example is the `War` alert heading, which reads `Armed Conflict`.
3. Read `<user data>/Imperator/logs/error.log` and confirm no encoding or parse warning names a shipped file.

## Use the mod

Enable the mod and play. No configuration is required. The overrides load after vanilla localisation and replace the affected strings wherever they are displayed.

To compare an override against its vanilla source, open the pair side by side:

| Override | Vanilla source |
|----------|----------------|
| `latinised-english/localization/replace/alerts_latinised_l_english.yml` | `<game>/localization/english/alerts_l_english.yml` |

## Author an override

1. Locate the vanilla source under `<game>/localization/english/` and note its exact relative path and file name.
2. Create the override at the mirrored path under `latinised-english/localization/replace/`, inserting `_latinised` before the language suffix, with a UTF-8 BOM and an `l_english:` header.
3. Add only the records whose value differs from vanilla, applying the vocabulary substitution that matches the sense in use and preserving every engine token in its original position.
4. Verify the pair against the structural and token checks described in [testing.md](./testing.md).

See [flows/override-authoring.md](./flows/override-authoring.md) for the full procedure and [change-guide.md](./change-guide.md) for modification safety.

## Next steps

- Newcomer: [repository-overview.md](./repository-overview.md).
- Contributor: [components/mod-content.md](./components/mod-content.md) and [invariants.md](./invariants.md).
- Diagnosing a missing substitution: [troubleshooting.md](./troubleshooting.md).
