# Documentation Index

Master navigation for the Latinised English repository knowledge base. It catalogues every document under `docs/`, the root policy documents, and the recommended reading order for each audience.

## Repository summary

Latinised English is a content-only localisation mod for Imperator: Rome. It ships a mirror of the vanilla English localisation tree under `latinised-english/localization/replace/`, carrying only those records whose value differs from vanilla. It replaces selected Germanic-origin English words and phrases with Latin-origin alternatives: British spellings, wider Latin-ancestry vocabulary, and context-sensitive substitutions. The repository owns no runtime, no build step, and no executable code; every observable behaviour is produced by the Imperator: Rome engine reading these files.

Current state: 153 override files carrying 8,691 records against a vanilla corpus of 176 files and 62,528 records (roughly 14% coverage). The mod declares itself compatible with Imperator: Rome `2.0.*` and is distributed through the Steam Workshop, Nexus Mods, and GitHub Releases.

## Root document map

| Document | Purpose |
|----------|---------|
| [README.md](../README.md) | Project overview, capabilities, installation, and usage |
| [ARCHITECTURE.md](../ARCHITECTURE.md) | System context, architectural areas, runtime flow, and constraints |
| [SECURITY.md](../SECURITY.md) | Security policy and vulnerability reporting |
| [PRIVACY.md](../PRIVACY.md) | Privacy statement |
| [CONTRIBUTING.md](../CONTRIBUTING.md) | Contribution guidelines |
| [CODE_OF_CONDUCT.md](../CODE_OF_CONDUCT.md) | Standards of conduct |
| [LICENSE](../LICENSE) | GNU General Public License v3.0 or later |

The `docs/` tree complements these documents rather than duplicating them. Where a root document already states architecture, security, or privacy conduct, the corresponding `docs/` file elaborates on it and links back.

## Documentation catalogue

### Orientation

| Document | Description |
|----------|-------------|
| [quick-start.md](./quick-start.md) | Fastest path to using, verifying, and modifying the mod |
| [repository-overview.md](./repository-overview.md) | Purpose, scope, boundaries, and entry points |
| [repository-structure.md](./repository-structure.md) | Source tree layout and file inventory |

### Architecture and design

| Document | Description |
|----------|-------------|
| [architecture.md](./architecture.md) | Architectural decomposition and component relationships |
| [design-decisions.md](./design-decisions.md) | Key design choices and their rationale |
| [invariants.md](./invariants.md) | System-wide invariants and contracts |
| [dependencies.md](./dependencies.md) | External dependencies and their architectural consequence |

### Components

| Document | Description |
|----------|-------------|
| [components/mod-content.md](./components/mod-content.md) | The localisation override corpus |
| [components/mod-descriptor.md](./components/mod-descriptor.md) | Launcher and content descriptors |
| [components/repository-metadata.md](./components/repository-metadata.md) | Documentation, licence, and artwork |
| [components/packaging-and-distribution.md](./components/packaging-and-distribution.md) | Release workflows and distribution channels |

### Behaviour and flows

| Document | Description |
|----------|-------------|
| [behaviour/localisation-override.md](./behaviour/localisation-override.md) | What a user observes when an override applies |
| [flows/mod-discovery-and-load.md](./flows/mod-discovery-and-load.md) | How the launcher discovers and loads the mod |
| [flows/localisation-override-resolution.md](./flows/localisation-override-resolution.md) | How overrides win over vanilla keys |
| [flows/override-authoring.md](./flows/override-authoring.md) | How a maintainer authors and verifies an override |

### Reference

| Document | Description |
|----------|-------------|
| [data-model.md](./data-model.md) | Localisation records, descriptors, and the language table |
| [configuration.md](./configuration.md) | Descriptor fields and their effect |
| [integrations.md](./integrations.md) | Host, launcher, and distribution integrations |
| [logging.md](./logging.md) | Engine log surface and diagnostics |
| [error-handling.md](./error-handling.md) | Failure modes and their visibility |
| [security.md](./security.md) | Trust boundary and content-integrity concerns |
| [state-and-persistence.md](./state-and-persistence.md) | Why the repository owns no state |
| [localisation.md](./localisation.md) | Language coverage and locale identifiers |

### Operations and maintenance

| Document | Description |
|----------|-------------|
| [build-and-deployment.md](./build-and-deployment.md) | Packaging, release, and publication |
| [testing.md](./testing.md) | Verification strategy and coverage gaps |
| [change-guide.md](./change-guide.md) | Safe modification procedures |
| [troubleshooting.md](./troubleshooting.md) | Recurring problems and resolutions |
| [faq.md](./faq.md) | Frequently asked questions |
| [documentation-maintenance.md](./documentation-maintenance.md) | Keeping this tree current |
| [ambiguities-and-open-questions.md](./ambiguities-and-open-questions.md) | Unresolved items and known gaps |

## Navigation aids

### Start here

For a newcomer who wants to install and use the mod: [quick-start.md](./quick-start.md) then [repository-overview.md](./repository-overview.md).

### Deep dive

For a contributor who wants to author an override: [flows/override-authoring.md](./flows/override-authoring.md), [components/mod-content.md](./components/mod-content.md), [invariants.md](./invariants.md), and [change-guide.md](./change-guide.md).

### Flows

For a maintainer diagnosing why a string did or did not change: [flows/localisation-override-resolution.md](./flows/localisation-override-resolution.md) then [troubleshooting.md](./troubleshooting.md).

## Maintenance metadata

| Field | Value |
|-------|-------|
| Last reviewed | 2026-11-21 |
| Owner | Repository maintainer |
| Coverage status | Complete for the shipped content surface |
| Source revision | `c3c3bdb` |
