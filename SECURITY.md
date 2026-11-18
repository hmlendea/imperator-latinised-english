# Security Policy

This policy states the objective, reporting principles, and supported-release coverage for the security of the Latinised English mod for Imperator: Rome. The mod is a content-only localisation package with no executable component, so the policy concentrates on the integrity of the shipped localisation data and the descriptor.

## 📑 Table of Contents

- [Supported Versions](#️-supported-versions)
- [Reporting a Vulnerability](#-reporting-a-vulnerability)
- [Scope](#-scope)
- [Disclosure Policy](#-disclosure-policy)

## 🛡️ Supported Versions

Use this table to indicate which project versions currently receive security maintenance.

| Version | Distribution Channel | Supported |
|---------|--------------------|-----------|
| Latest version | GitHub Releases | ✅ |
| Latest version | Unofficial third-party distribution channels | ❌ |
| Preceding versions | Any distribution channel | ❌ |

## 🚨 Reporting a Vulnerability

Please do not disclose suspected vulnerabilities publicly before maintainers have had an opportunity to validate and remediate them.

To report a vulnerability:
- [GitHub Security Advisories](https://github.com/hmlendea/imperator-latinised-english/security/advisories)
- Contact the maintainers directly

## 📌 Scope

The original maintainers are not responsible for changes, modifications, or security issues introduced by downstream forks.

The subsequent report categories are in scope for this repository:
- A localisation value that alters, drops, or reorders an engine token in a way that breaks the string consuming it.
- A localisation file that fails the engine's encoding or naming rules and therefore loads incorrectly or not at all.
- A descriptor value that misrepresents the mod identity, version, or supported game version.
- Malicious content introduced into the shipped localisation or descriptor files.

The subsequent categories are out of scope unless explicitly stated to the contrary:
- Vulnerabilities in Imperator: Rome or in the Paradox launcher.
- Vulnerabilities in other mods, including interactions arising from load order.
- Achievements or ironman saves disabled or damaged by enabling a checksum-changing mod.
- Text quality, coverage, or translation judgement disagreements.

## 📢 Disclosure Policy

This project follows coordinated disclosure:
1. Vulnerabilities are investigated privately.
2. A remediation plan is prepared and validated.
3. Public disclosure is published after a fix, mitigation, or agreed risk decision is available.
4. Credit is attributed in accordance with reporter preference and project policy.
