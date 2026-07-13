# Contributing to AI Agent Design Principles

Thank you for your interest in improving AI agent design! This project thrives on community contributions.

## How to Contribute

### Adding New Principles

1. **Evidence Required** — Every new principle must be backed by either:
   - Production experience (describe the problem it solved)
   - Analysis of a shipping AI system
   - Empirical testing (A/B test results, user feedback data)

2. **Format** — Follow the existing pattern in `SKILL.md`:
   - Clear principle statement
   - Good/bad example pairs
   - Practical implementation guidance

3. **Scope** — Principles should be:
   - Universal (applicable to any AI agent, not just one platform)
   - Actionable (engineers can implement them today)
   - Testable (you can verify compliance)

### Adding Examples

Good examples are the most valuable contributions. Each example should include:

- **Context:** What type of agent, what user scenario
- **Bad response:** What most agents do wrong (and why it's wrong)
- **Good response:** What the agent should do instead
- **Why:** The principle behind the improvement

### Translations & Localization

We welcome translations of the main `SKILL.md` into other languages. Place translations in `skills/ai-agent-design-principles/translations/` as `SKILL.{lang}.md` (e.g., `SKILL.tr.md` for Turkish).

**When translating, please adapt rather than just translate:**
- **Pronouns & Formality:** Provide clear guidance on formal vs. informal pronouns (e.g., *tu/vous*, *du/Sie*, *tú/usted*) based on the target language's standard professional norms.
- **Directness & Tone:** If translating into a high-context language (e.g., Japanese, Korean), add explicit branching logic for honorifics and polite preambles that would otherwise violate the English "anti-sycophancy" rules.
- **Examples:** Replace US/Western-centric examples with culturally relevant local examples.

### Bug Reports / Improvements

- Open an issue describing the problem or improvement
- Reference specific sections by heading
- Include examples of the current behavior vs. expected behavior

## Pull Request Process

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/add-new-principle`)
3. Make your changes
4. Ensure your additions follow the existing format and style
5. Submit a pull request with a clear description

## Code of Conduct

- Be respectful and constructive
- Focus on evidence-based improvements
- Acknowledge that different AI contexts may require different approaches
- Credit sources when referencing external work

## Questions?

Open an issue with the `question` label. We're happy to help!
