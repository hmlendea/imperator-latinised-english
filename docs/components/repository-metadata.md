# Repository metadata

Repository metadata describes the package. It never participates in loading, and no content or descriptor file references it. See [invariants.md](../invariants.md) invariant B2.

## Components

| Path | Purpose |
|------|---------|
| `README.md` | Project overview, capabilities, installation, and usage |
| `ARCHITECTURE.md` | System context, architectural areas, runtime flow, and constraints |
| `CONTRIBUTING.md` | Contribution guidelines and development setup |
| `CODE_OF_CONDUCT.md` | Standards of conduct |
| `SECURITY.md` | Security policy and reporting scope |
| `PRIVACY.md` | Privacy statement |
| `LICENSE` | GNU General Public License v3.0 or later |
| `.github/cover.png` | Repository landing-page artwork |
| `.github/workflows/` | Release automation |
| `description/steam-workshop.bbcode` | Steam Workshop page body |

## Documentation role

The root Markdown documents and the Workshop page body are the human-readable description of the system. They are governed by a template-fidelity contract: fixed prose must be copied exactly, and only placeholders, conditionals, and evidenced content may change. This is why the README, ARCHITECTURE, SECURITY, and Workshop page share phrasing and structure.

## Artwork

`.github/cover.png` (approximately 2.7 MB) is the repository landing-page image. It is not read by the game and does not affect loading.

## Workshop page body

`description/steam-workshop.bbcode` is the Steam Workshop page description. It uses BBCode and contains the distribution badges, capabilities, installation, compatibility, load-order guidance, contributing link, related mods, support, engagement, and licence sections. It is a publication artifact, not shipped mod content.

## Boundary rules

- Repository metadata must never depend on mod content semantics; it describes the package rather than participating in loading.
- Documentation claims must be grounded in the shipped content and the engine contract, never in intended but unimplemented capability.
- No metadata file may be placed inside `latinised-english/`, because the engine loads every file in the content directory and would attempt to parse it.
