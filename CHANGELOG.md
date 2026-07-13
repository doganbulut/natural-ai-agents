# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2026-07-13

### Added
- Cross-model comparison: Claude vs GPT-4o vs Gemini architecture analysis (`docs/CROSS-MODEL-COMPARISON.md`)
- Turkish SKILL.md translation (`translations/tr/SKILL.md`)
- GitHub Actions CI workflow (format check, frontmatter validation, banned phrases, link checking)
- `docs/PRINCIPLES.md` — full reference with all examples and cultural notes

### Changed
- **SKILL.md trimmed to ~5KB** for token-efficient skill loading; details moved to `docs/PRINCIPLES.md`
- Terminology: "Production-tested" → "Derived from analysis of production-grade AI system prompts"
- "leaked" → "publicly available/disclosed" in ETHICS.md and METHODOLOGY.md
- ETHICS.md: expanded source attribution and scope limitations
- Updated repository structure diagrams in README and README.tr.md
- README.md methodology section now references cross-model comparison

### Added (infrastructure)
- Update strategy documented in CHANGELOG
- CI workflow in `.github/workflows/test.yml`

## [1.0.0] - 2026-07-12

### Added
- Initial release of AI Agent Design Principles skill
- 6 core principle areas: Communication, Context Management, Preferences, Tool Suggestions, Knowledge/Search, Safety/Boundaries
- Reference documents:
  - Source analysis (`fable5-prompt-analysis.md`)
  - Preference application examples with 10+ scenarios
  - Memory system design patterns
- Good/bad response pairs for each principle
- Quick reference card for rapid lookup
- Common mistakes table
- Methodology documentation
- Contributing guidelines

## Update Strategy

### Analyzed Model Version
- **Primary source:** Anthropic Claude (Fable 5 model family) — system prompt analyzed 2026-07-12
- **Scope:** Single model family (primary); cross-model comparison added (see `docs/CROSS-MODEL-COMPARISON.md`)

### Update Cadence
- **Major review:** Triggered when a new frontier model family is released (e.g., Claude 5, GPT-5, Gemini 3)
- **Minor review:** Triggered when significant behavioral changes are observed in existing models
- **Community-triggered:** When a substantiated analysis of a different model's prompt architecture is submitted via PR

### Detection Mechanism
- **Release monitoring:** Track major AI model releases through official channels
- **Behavioral regression testing:** If a principle stops producing expected results with a newer model version, flag for review
- **Community reports:** GitHub issues reporting principle ineffectiveness trigger investigation

### Versioning
- Principles validated against a new model family → minor version bump
- Principles revised or removed → major version bump
- Documentation-only updates, translations, examples → patch version bump
