# Build and deployment

There is no build. The repository ships static files, so deployment is packaging and publication rather than compilation and installation.

## Build

The repository has no compilation, bundling, or asset generation step. The content directory is the artefact. Nothing must be regenerated before shipping.

| Concern | State |
|---------|-------|
| Compiler | None |
| Package manager | None |
| Build script | None |
| Generated files | None committed or produced |
| Dependency restoration | None |

## Packaging

The release workflows create an archive from two paths:

```text
latinised-english/
latinised-english.mod
```

`github-release.yml` names the archive `latinised-english_<version>.zip`, with `<version>` derived from the tag by stripping a leading `v`. The Nexus and Steam workflows name it `release.zip` and are used only as an intermediate.

## Deployment targets

| Target | Unit | Method | Trigger |
|--------|------|--------|---------|
| GitHub Releases | `latinised-english_<version>.zip` | `softprops/action-gh-release@v2` | Published release or manual dispatch |
| Nexus Mods | `release.zip` uploaded to file `8432532` | `Nexus-Mods/upload-action@v1.0.0-beta.11` | `v*.*.*` tag or manual dispatch |
| Steam Workshop | `release/latinised-english/` uploaded to item `3843565947` | `hmlendea/steam-workshop-update@latest` | `v*.*.*` tag or manual dispatch |
| End user (manual) | `latinised-english/` + `latinised-english.mod` | Copy into the Imperator mod directory | Manual |

## Environments

There is a single environment: the published release. No staging or preview environment exists.

## Versioning and tags

| Property | Detail |
|----------|--------|
| Descriptor version | `version="1.0.0"` in both descriptors |
| Tag convention | `v*.*.*` (for example `v1.0.0`) |
| Archive version | The tag with any leading `v` removed |
| Current tag | `v1.0.0` |

## Release procedure

1. Update `version` in both descriptors to the release version, and commit.
2. Create and push a tag matching `v*.*.*`.
3. The tag-triggered workflows package and publish to Nexus Mods and the Steam Workshop.
4. Publish a GitHub release (or dispatch the workflow manually), which attaches the archive to the release.

The three workflows are independent; each channel can be published or retried on its own.

## Persistent state and migrations

None. There is nothing to migrate, no database, and no service to roll back. A defective publication is corrected by publishing a new revision.

## Operational consequences

| Concern | Detail |
|---------|--------|
| Process topology | None; the engine hosts all execution |
| Deployment mechanism | Copying the content directory and descriptor, or subscribing through a store |
| Availability | Continuous; static files are either present or absent |
| Recovery | Delete the mod directory and descriptor; recovery is total |
| Checksum effect | Any localisation override alters the checksum, disabling achievements and risking ironman saves |
| Operator-visible output | The launcher mod list and the engine log |

## Prerequisites for publication

Publishing requires the repository secrets `NEXUSMODS_API_KEY`, `STEAM_USERNAME`, `STEAM_PASSWORD`, and `STEAM_2FA_SEED`. Without them the corresponding workflow fails and the other channels remain unaffected. See [components/packaging-and-distribution.md](./components/packaging-and-distribution.md).
