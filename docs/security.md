# Security

This document elaborates on the root [SECURITY.md](../SECURITY.md) without duplicating it. It records the trust boundary, the security-relevant properties of the shipped content, and the categories that are in and out of scope.

## Trust boundary

The trust boundary is the game installation. The repository ships text that the engine parses within the same trust domain as vanilla content. There is:

- no network communication;
- no credential handling;
- no personal data;
- no executable payload.

The relevant safety concern is therefore **content integrity** rather than adversarial input: the risk is that a shipped value breaks the string that consumes it, not that an attacker injects code.

## Security-relevant properties

| Property | Detail |
|----------|--------|
| No code execution | The mod is data only; the engine executes nothing from it |
| No network | No file causes any network access |
| No credentials | No file contains or references a credential |
| No personal data | No file contains personal data |
| Same trust domain as vanilla | The mod is text the engine parses like vanilla text |
| Integrity by token preservation | Safety is maintained by keeping every engine token byte-identical |

## Content-integrity threats

| Threat | Effect | Mitigation |
|--------|--------|------------|
| Altered engine token | The consuming string renders incorrectly | Token-sequence comparison against vanilla |
| Dropped or reordered token | The string breaks | Invariant C9 |
| Invalid encoding or missing BOM | The file loads incorrectly or warns | Invariant C1 |
| Malformed record | The record is discarded silently | Invariant C7 |
| Misleading descriptor | The mod is misrepresented or mislocated | Descriptor invariants D1–D4 |
| Malicious content introduced into the shipped files | Unexpected interface behaviour | Review before release; scope stated in `SECURITY.md` |

## Publication secrets

The release workflows require credentials that must never be committed:

| Secret | Consumer | Handling |
|--------|----------|----------|
| `GITHUB_TOKEN` | GitHub release | Provided automatically by GitHub |
| `NEXUSMODS_API_KEY` | Nexus Mods | Repository secret, referenced by name only |
| `STEAM_USERNAME` | Steam Workshop | Repository secret |
| `STEAM_PASSWORD` | Steam Workshop | Repository secret |
| `STEAM_2FA_SEED` | Steam Workshop | Steam Guard secret; highly sensitive |

No secret value appears anywhere in the repository. See [components/packaging-and-distribution.md](./components/packaging-and-distribution.md).

## Scope

In scope for this repository, per the security policy:

- a localisation value that alters, drops, or reorders an engine token in a way that breaks the consuming string;
- a localisation file that fails the engine's encoding or naming rules and therefore loads incorrectly or not at all;
- a descriptor value that misrepresents the mod identity, version, or supported game version;
- malicious content introduced into the shipped localisation or descriptor files.

Out of scope:

- vulnerabilities in Imperator: Rome or the Paradox launcher;
- vulnerabilities in other mods, including load-order interactions;
- achievements or ironman saves disabled by a checksum-changing mod;
- text quality, coverage, or translation judgement disagreements.

## Reporting

Report through [GitHub Security Advisories](https://github.com/hmlendea/imperator-latinised-english/security/advisories) or by contacting the maintainers directly, following coordinated disclosure. See the root [SECURITY.md](../SECURITY.md).
