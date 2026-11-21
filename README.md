[![Build Status](https://github.com/hmlendea/imperator-latinised-english/actions/workflows/github-release.yml/badge.svg)](https://github.com/hmlendea/imperator-latinised-english/actions/workflows/github-release.yml)
[![License](https://img.shields.io/github/license/hmlendea/imperator-latinised-english)](https://github.com/hmlendea/imperator-latinised-english/blob/master/LICENSE)

# Latinised English

A localisation mod for Imperator: Rome that overrides selected vanilla English strings with latinisations drawn from the `english-language` vocabulary rules.

## 📑 Table of Contents

- [Capabilities](#-capabilities)
- [Usage](#-usage)
- [Known Limitations](#-known-limitations)
- [Installation](#-installation)
  - [Manual Installation](#manual-installation)
  - [Verification](#verification)
- [Localisation](#-localisation)
- [Compatibility](#-compatibility)
- [Privacy and Data](#️-privacy-and-data)
- [GitHub Actions](#-github-actions)
- [Project Structure](#️-project-structure)
  - [Directories](#directories)
- [Architecture](#️-architecture)
- [Data Formats and Protocols](#-data-formats-and-protocols)
- [Contributing](#-contributing)
- [Code of Conduct](#-code-of-conduct)
- [Acknowledgements](#-acknowledgements)
- [Security](#-security)
- [Support](#-support)
- [Project Engagement](#-project-engagement)
- [License](#-license)

## ✨ Capabilities

- Replaces vanilla English strings with latinisable equivalents, including British spellings, wider Latin-ancestry vocabulary, and context-sensitive word substitutions.
- Preserves every engine construct inside a value, including hover commands, variables, text icons, colour codes, and literal newlines, so tooltips continue to resolve.
- Ships only records that differ from vanilla, keeping the override set minimal and reviewable.
- Mirrors the vanilla localisation tree, so each override sits at the identical relative path with the `_latinised` marker inserted before the language suffix.

## 🚀 Usage

Enable the mod in the Imperator: Rome launcher and play. No configuration is required; the overrides load after vanilla localisation and replace the affected strings anywhere they are displayed.

To compare an override against its vanilla source, open the pair side by side:

| Override | Vanilla source |
|----------|----------------|
| `latinised-english/localization/replace/alerts_latinised_l_english.yml` | `<game>/localization/english/alerts_l_english.yml` |

## ⚠️ Known Limitations

- Coverage is partial. Only a subset of the vanilla localisation files currently carries overrides, so most in-game text remains unchanged.
- Records are only overridden where a latinisable substitution exists that preserves the original meaning and grammar. Strings whose dictionary record targets a different sense than the one in use are deliberately left untouched.
- Enabling the mod changes the game checksum, which disables achievements. Loading an ironman save with a checksum-changing mod can make the save unplayable, so the mod should not be enabled on ironman campaigns.
- Every value must keep its engine tokens byte-identical. Reordering, adding, or removing a hover command, variable, text icon, colour code, or `\n` escape breaks the string that consumes it.

## 📦 Installation

[![Get it from the Workshop](https://raw.githubusercontent.com/hmlendea/readme-assets/master/badges/stores/steam-workshop.png)](https://steamcommunity.com/sharedfiles/filedetails/?id=3843565947)
[![Get it from GitHub](https://raw.githubusercontent.com/hmlendea/readme-assets/master/badges/stores/github.png)](https://github.com/hmlendea/imperator-latinised-english/releases)

### Manual Installation

1. Obtain the repository contents, either by cloning it or by downloading it as an archive.
2. Place the `latinised-english` directory and the `latinised-english.mod` descriptor file into the Imperator: Rome mod directory.
3. Select **Latinised English** in the launcher Mods tab.

The mod directory is located at:
- GNU/Linux: `~/.local/share/Paradox Interactive/Imperator/mod/`
- Windows and macOS: `~/Documents/Paradox Interactive/Imperator/mod/`

When replacing an existing installation, delete the previous `latinised-english` directory and `latinised-english.mod` file first, because the game loads every file present in the mod directory.

### Verification

The launcher lists **Latinised English** in the Mods tab with version `1.0.0`, and the mod's enabled state survives a launcher restart. In game, strings such as the `War` alert heading read `Conflict` instead of the vanilla wording.

## 🌍 Localisation

The repository is itself a localisation resource. It ships only the English language and only the records it overrides.

| Language | Locale | Status |
|----------|--------|--------|
| English | `l_english` | Partial, expanded file by file |

## 🧩 Compatibility

| Component | Supported Versions | Notes |
|-----------|--------------------|-------|
| Imperator: Rome | `2.0.*` | Declared as `supported_version` in the mod descriptor |

The mod targets the vanilla English localisation tree. Other mods that override the same keys win or lose according to launcher load order, so place this mod after localisation mods it should supersede.

## 🛡️ Privacy and Data

Latinised English collects no personal data and contains no runtime component.

For the detailed description of how the application handles privacy and personal data, see the [Privacy Statement](./PRIVACY.md).

The mod is a set of static localisation files executed by the game. It performs no collection, transmission, or storage of data, and it does not read any application data produced by the game.

## ⚙️ GitHub Actions

| Workflow | Purpose | What it does |
|----------|---------|--------------|
| [ github-release.yml ](https://github.com/hmlendea/imperator-latinised-english/blob/master/.github/workflows/github-release.yml) | GitHub Release | Builds `latinised-english_<version>.zip` from the published tag and attaches it to the GitHub release |
| [ steam-workshop-release.yml ](https://github.com/hmlendea/imperator-latinised-english/blob/master/.github/workflows/steam-workshop-release.yml) | Release to Steam Workshop | Runs on a `v*.*.*` tag push or manual dispatch: checks out the tag, zips and extracts the descriptor and content directory, and uploads the content directory to Workshop item `3843565947` with a changelog link |

## 🗂️ Project Structure

### Directories

| Directory | Purpose |
|-----------|---------|
| `latinised-english/` | Mod content directory, referenced by the launcher descriptor |
| `latinised-english/localization/replace/` | English localisation overrides, which load after all other localisation |
| `.github/` | Repository artwork used by the repository landing page |

## 🏗️ Architecture

Latinised English is a content-only localisation mod whose architecture is the file and key resolution contract of the Imperator: Rome engine.

See the [Architecture Documentation](./ARCHITECTURE.md) for the system context, principal components, runtime flows, ownership boundaries, dependencies, constraints, and extension points.

## 🧾 Data Formats and Protocols

| Format or Protocol | Specification | Purpose |
|--------------------|---------------|---------|
| Localisation file | [Imperator: Rome localisation](https://imperator.paradoxwikis.com/Localisation) | Carries the `l_english` key and value records that override vanilla strings |
| Mod descriptor | [Imperator: Rome mod file](https://imperator.paradoxwikis.com/Mod_file) | Declares the mod name, version, supported game version, and content path |

## 🤝 Contributing

You are welcome to submit any suggestion, feedback, or modification to this project.

When doing so, please:
- Maintain cross-platform compatibility
- Preserve the existing public contract unless a breaking change is intentional
- Submit focused pull requests that conform to the existing code style
- Maintain your branch synchronised with `master`
- Revise the documentation when functionality changes
- Raise a new [issue](https://github.com/hmlendea/imperator-latinised-english/issues) for problems or suggestions

See the [Contributing Guidelines](./CONTRIBUTING.md) for details on how to report issues, suggest enhancements, and submit changes.

## 📜 Code of Conduct

See the [Code of Conduct](./CODE_OF_CONDUCT.md) for the standards of conduct expected in all project spaces.

## 🙏 Acknowledgements

- **Paradox Development Studio** for Imperator: Rome and the vanilla English localisation this mod overrides.

## 🔒 Security

Latinised English performs no network communication, executes no code, and handles no credentials.

For information on reporting security vulnerabilities, see the [Security Policy](./SECURITY.md).

## 💬 Support

For support, please [open an issue](https://github.com/hmlendea/imperator-latinised-english/issues).

## 💝 Project Engagement

Discovered a problem with Latinised English or have a suggestion for it? [Open an issue](https://github.com/hmlendea/imperator-latinised-english/issues)!

If you find this project useful, consider starring ⭐️ it on GitHub!

## 📄 License

This project is being distributed under the `GNU General Public License v3.0` or later.
See [LICENSE](./LICENSE) for additional information.
