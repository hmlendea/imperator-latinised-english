# Packaging and distribution

Three GitHub Actions workflows package and publish the mod. Each is an independent file with its own trigger, so a failure in one channel does not block the others.

## github-release.yml

| Property | Value |
|----------|-------|
| Name | GitHub Release |
| Triggers | `release: published`, `workflow_dispatch` with a `tag` input |
| Permissions | `contents: write` |

Steps:

1. Check out the repository at the resolved `VERSION` (`inputs.tag` or `github.event.release.tag_name`).
2. Strip a leading `v` from the tag to derive the version (`VERSION="${VERSION#v}"`).
3. Build `latinised-english_<version>.zip` by archiving `latinised-english/` and `latinised-english.mod`.
4. Attach the archive to the GitHub release with `softprops/action-gh-release@v2`, using `GITHUB_TOKEN`.

## nexus-mods-release.yml

| Property | Value |
|----------|-------|
| Name | Nexus Mods |
| Triggers | `push` of a `v*.*.*` tag, `workflow_dispatch` with a `tag` input |
| Secret | `NEXUSMODS_API_KEY` |

Steps:

1. Check out the tag.
2. Build `release.zip` from `latinised-english/` and `latinised-english.mod`.
3. Upload with `Nexus-Mods/upload-action@v1.0.0-beta.11` to file identifier `8432532`, display name `latinised-english.zip`, with `archive_existing_version: true` and `update_mod_version: true`. The description links to the GitHub release changelog.

## steam-workshop-release.yml

| Property | Value |
|----------|-------|
| Name | Steam Workshop |
| Triggers | `push` of a `v*.*.*` tag, `workflow_dispatch` with a `tag` input |
| Secrets | `STEAM_USERNAME`, `STEAM_PASSWORD`, `STEAM_2FA_SEED` |

Steps:

1. Check out the tag.
2. Build `release.zip` from the same two paths.
3. Extract the archive into `release/`.
4. Upload with `hmlendea/steam-workshop-update@latest` to appid `859580`, item identifier `3843565947`, with the upload path set to `release/latinised-english/` and a changenote linking to the tagged GitHub release.

## Why the Steam workflow extracts before uploading

The Workshop updater takes a content directory, not an archive. The workflow therefore builds an archive for consistency with the other channels and then extracts it, uploading only `release/latinised-english/`. This keeps the content directory as the upload root. See [invariants.md](../invariants.md) invariant P2.

## Publication identifiers

| Channel | Identifier | Source |
|---------|------------|--------|
| Steam Workshop | `3843565947` (appid `859580`) | `steam-workshop-release.yml` |
| Nexus Mods | file `8432532` on `imperatorrome` | `nexus-mods-release.yml` |
| GitHub Releases | `latinised-english_<version>.zip` | `github-release.yml` |

These identifiers are publication contracts. Changing one redirects the release to a different published item. See [invariants.md](../invariants.md) invariant P3.

## Secrets

No secret value appears in the repository. The workflows reference GitHub repository secrets by name only:

| Secret | Consumer | Purpose |
|--------|----------|---------|
| `GITHUB_TOKEN` | GitHub release | Provided automatically; authorises the release asset upload |
| `NEXUSMODS_API_KEY` | Nexus Mods | Authorises the Nexus upload |
| `STEAM_USERNAME` | Steam Workshop | Steam account identity |
| `STEAM_PASSWORD` | Steam Workshop | Steam account credential |
| `STEAM_2FA_SEED` | Steam Workshop | Steam two-factor seed |

Steam credentials are Steam Guard secrets and must never be committed. See [security.md](../security.md).

## Failure semantics

| Failure | Effect |
|---------|--------|
| Missing or invalid secret | The affected channel fails; the others are unaffected |
| Tag does not match `v*.*.*` | The tag-triggered workflows do not run |
| `path` in the descriptor diverges from the archived directory name | The archive contains a directory the launcher cannot resolve; installation fails |
