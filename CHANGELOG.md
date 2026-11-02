# Changelog

All notable changes to this project are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/) and the project uses
[Semantic Versioning](https://semver.org/). Preview releases (0.x) may change anything.

## [Unreleased]
### Added
- README rewrite (feature status labels, FAQ, comparison, roadmap, citation).
- Community files: Code of Conduct, feature request template, issue config, CITATION.cff, release notes config.
- `llms.txt`, `docs/README.md`, launch playbook and gh CLI cookbook.
- CodeQL workflow; social preview image `docs/assets/social-preview.png`.
### Fixed
- CI: removed the `--minWorkers` flag that current Vitest rejects; added minimal permissions.
- README quickstart port (the dev server listens on 4100, not 3000).
- SECURITY.md advisory link now points at this repository.

## [0.1.0] - 2026-11-02
First tagged preview of the hackathon entry.
### Added
- Discord-style Meta Server shell, registry-driven navigation and Agent Hub.
- Git-for-agents commit console; unified inbox, social and ad drafts (live sends need credentials).
- Jev approval gate with payload-bound approvals and `/api/dispatch`.
- Optional local Llama tier (Ollama, WebLLM), Llama Guard 3 check and Claw Swarm builder.
- MUSE voice assistant, 2D avatar and three.js fur simulator.
- Brain, read-only data tools, DPDP privacy export and writing library.
- SQLite business modules: invoicing, GST, inventory, CRM, POS, bookings.
### Known limitations
- Single-operator preview; not production-ready.
- Meta channels show "Not connected" without your own credentials.
- Some lab tests fail or time out (see open issues).

[Unreleased]: https://github.com/CodesbyFebin/Meta-Ai-OS/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/CodesbyFebin/Meta-Ai-OS/releases/tag/v0.1.0
