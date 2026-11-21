# Documentation maintenance

## Purpose

This document states how the `docs/` tree is kept current, who owns it, and what must change in lockstep with the repository.

## Ownership

| Area | Owner |
|------|-------|
| `docs/` knowledge base | Repository maintainer |
| Root documents (`README.md`, `ARCHITECTURE.md`, `SECURITY.md`, `PRIVACY.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`) | Repository maintainer, under the template-fidelity contract |
| Coverage metrics | Repository maintainer, recomputed from the shipped corpus |
| Release workflows and their published identifiers | Repository maintainer |

## Documentation set

| Layer | Path | Authority |
|-------|------|-----------|
| Root documents | repository root | Canonical template-governed documents |
| Knowledge base | `docs/` | Elaboration of the root documents plus reference material |

`docs/` complements the root documents and does not duplicate them. Where a root document already states architecture, security, or privacy conduct, the corresponding `docs/` file elaborates on it and links back.

## When to update

| Change | Documents to revise |
|--------|---------------------|
| Add or remove override files | [repository-structure.md](./repository-structure.md), [localisation.md](./localisation.md), [components/mod-content.md](./components/mod-content.md), [INDEX.md](./INDEX.md) metrics |
| Change record or file format rules | [invariants.md](./invariants.md), [data-model.md](./data-model.md), [components/mod-content.md](./components/mod-content.md) |
| Change the descriptors | [components/mod-descriptor.md](./components/mod-descriptor.md), [configuration.md](./configuration.md) |
| Change a release workflow or identifier | [components/packaging-and-distribution.md](./components/packaging-and-distribution.md), [build-and-deployment.md](./build-and-deployment.md) |
| Change supported game version | [dependencies.md](./dependencies.md), [configuration.md](./configuration.md), root [README.md](../README.md) |
| Change the security scope | [security.md](./security.md), root [SECURITY.md](../SECURITY.md) |
| Change verification method | [testing.md](./testing.md), [change-guide.md](./change-guide.md) |

## Metric discipline

Every count in this tree (file counts, record counts, coverage percentages) must be recomputed from the shipped corpus rather than copied forward. The procedure is in [testing.md](./testing.md) under "Corpus-wide structural check". Cover counts drift: the tally is currently 153 files and 8,691 records against a baseline of 176 files and 62,528 records.

## Cross-reference discipline

- Use repository-relative links for repository paths and canonical HTTPS links for external resources.
- Verify every link target exists before committing.
- Keep the [INDEX.md](./INDEX.md) catalogue complete whenever a document is added, renamed, or removed.
- Keep the "Last reviewed" and "Source revision" fields in [INDEX.md](./INDEX.md) current.

## Template fidelity

Root documents follow a template-fidelity contract: fixed prose must be copied exactly, and only placeholders, conditionals, and evidenced content may change. When editing a root document, revise the whole corresponding section rather than a fragment.

## Review triggers

Review the tree when any of the following occurs:

- the game version changes and `supported_version` must move;
- a new distribution channel is added;
- the coverage tally changes materially;
- a new invariant or failure mode is discovered;
- a root document gains or loses a section.
