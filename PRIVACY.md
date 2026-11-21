# Privacy and Personal Data

This document describes the personal-data conduct of the Latinised English mod for Imperator: Rome, a content-only localisation package that is copied into the game's mod directory and loaded by the game engine. The mod handles no personal data, performs no network communication, and owns no runtime component.

## 📑 Table of Contents

- [What This Document Covers](#-what-this-document-covers)
- [Data We Handle](#-data-we-handle)
  - [Data Provided to the Application](#data-provided-to-the-application)
  - [Data Generated or Collected by the Application](#data-generated-or-collected-by-the-application)
  - [Data Received from Integrations](#data-received-from-integrations)
- [Processing and Use](#-processing-and-use)
- [Storage, Retention, and Deletion](#️-storage-retention-and-deletion)
- [External Processing and Integrations](#-external-processing-and-integrations)
- [Data Protection and Security](#️-data-protection-and-security)
- [Document Changes](#-document-changes)
- [Contact](#-contact)

## 🔎 What This Document Covers

This document describes how Latinised English at https://github.com/hmlendea/imperator-latinised-english manages personal data. It covers the application conduct and verified integrations described below. Where the software is self-hosted, the instance operator may have separate responsibilities described below.

The mod consists of static localisation files and a launcher descriptor. Once installed, it is read by the Imperator: Rome engine and nothing else. There is no server, service, daemon, or background process associated with the project, so there is no data flow to describe beyond the game's own handling, which is outside this document's scope.

## 📥 Data We Handle

### Data Provided to the Application

- None. The mod presents no interface and requests no input. It reads only its own shipped localisation and descriptor files.

### Data Generated or Collected by the Application

- None. The mod generates and collects no server, application, access, audit, telemetry, crash, or update-check data. It writes no files and produces no logs; the log files consulted when diagnosing a load issue are written by the game engine, not by this project.

### Data Received from Integrations

- None. The mod is not connected to any external service and receives no personal data from integrations or third parties.

## 🧭 Processing and Use

The application processes the data described above for these verified functions:
- Localisation override resolution — the game engine reads the shipped key and value records and merges them into the active language table. No personal data is involved.

## 🗄️ Storage, Retention, and Deletion

The mod ships no store and retains nothing. Its localisation records and descriptor are static files placed in the game's mod directory by the user, and their storage and retention are determined entirely by the user's file system and by their decision to keep the mod installed. Deleting the mod directory and its descriptor removes the mod completely, because the project keeps no copy and owns no external state.

Any data produced by the game itself, such as save games, settings, and logs, is stored and retained under the game's own paths and is subject to the game's own practices. This project neither reads nor controls that data.

## 🔗 External Processing and Integrations

The mod has no built-in external data transfer. It contacts no service, sends no telemetry, and performs no update check at runtime.

| Service or integration | Purpose | Data involved | Configuration or documentation |
|-----------------------|---------|---------------|--------------------------------|
| None | — | — | — |

## 🛡️ Data Protection and Security

The project's relevant safeguard is data integrity rather than confidentiality, because no personal data is in scope. Each shipped value is validated to be a substitution of its vanilla counterpart with every engine token preserved in position, so the mod cannot corrupt the strings it overrides. The repository exposes no secret, credential, or private endpoint, and the distribution artefacts contain only localisation text and descriptor metadata.

The original maintainers are not responsible for changes, modifications, or privacy issues introduced by downstream forks.

## 🔄 Document Changes

Update this document when application data processes, storage, integrations, or deployment responsibilities change. The current version is published at https://github.com/hmlendea/imperator-latinised-english/blob/master/PRIVACY.md.

## 📬 Contact

For questions about application data handling, contact the project maintainers through the repository issue tracker. No deployment identifier or data-process identifier is needed for a request concerning this project, because the mod processes no personal data; do not send passwords, access tokens, or other secrets.
