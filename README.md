# AI Agent Design Principles

> Principles derived from analysis of production-grade AI system prompts for building agents that feel natural, intelligent, and trustworthy.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Agent Skill](https://img.shields.io/badge/Agent-Skill-blue.svg)](https://agentskills.io)

🌍 **[Türkçe dokümantasyon için tıklayın (Turkish Documentation)](README.tr.md)**

## Table of Contents
- [What is this?](#what-is-this)
- [Who is this for?](#who-is-this-for)
- [Key Principles](#key-principles)
- [Quick Start](#quick-start)
- [Repository Structure](#repository-structure)
- [Principles at a Glance](#principles-at-a-glance)
- [Contributing](#contributing)
- [Methodology](#methodology)
- [Ethics & Disclosure](#ethics--disclosure)
- [License](#license)

## What is this?

A comprehensive, open-source skill (reusable agent instruction set) that captures **production-derived principles** for AI agent communication, context management, and user interaction design. Derived from deep analysis of production-grade AI system prompts.

**The core insight:** The difference between a mediocre AI agent and a great one is not capability — it's *restraint*. Knowing when NOT to format, NOT to personalize, NOT to over-explain is what makes interactions feel human.

## Who is this for?

- **AI/ML Engineers** building conversational agents, coding assistants, or chatbots
- **Product Managers** defining AI agent behavior specifications
- **Prompt Engineers** writing or refining system prompts
- **Researchers** studying AI interaction patterns
- Anyone building AI products that interact with humans

## Key Principles

### 1. 🗣️ Natural Communication
Don't over-format. Use prose instead of bullet points. Match the user's energy. A few sentences is often enough.

### 2. 🧠 Selective Context Application
Not every piece of user data should appear in every response. Apply context only when it materially improves the answer.

### 3. 🔇 Zero Meta-Commentary
Never reveal your data retrieval process. "Based on my memory..." is banned. State facts naturally.

### 4. 🛡️ Sensitive Content Protection
Never proactively surface grief, health issues, or personal crises. Only engage when the user brings it up.

### 5. 🎯 The Sommelier Test
If the user is a sommelier and asks about Python, don't use wine metaphors. Apply preferences only when relevant.

### 6. 🔧 Organic Tool Suggestions
Suggest tools like a helpful colleague, not a salesperson. Always opt-in, never force.

## Quick Start

### As an Agent Skill (Recommended)

Copy the `skills/ai-agent-design-principles/` directory into your agent's skill directory:

```bash
# For Gemini CLI
cp -r skills/ai-agent-design-principles ~/.gemini/config/skills/

# For Claude Code
cp -r skills/ai-agent-design-principles ~/.claude/skills/

# Cross-runtime alias
cp -r skills/ai-agent-design-principles ~/.agents/skills/

# For Windows (PowerShell)
Copy-Item -Recurse skills\ai-agent-design-principles $env:USERPROFILE\.gemini\config\skills\
```

### As a Reference Guide

Read the main document directly:

```bash
cat skills/ai-agent-design-principles/SKILL.md
```

### As System Prompt Material

Extract specific sections for your system prompt:

```python
# Example: Extract the anti-overformatting rules
with open("skills/ai-agent-design-principles/SKILL.md") as f:
    content = f.read()
    # Use the sections relevant to your agent
```

## Repository Structure

```
.
├── README.md                          # This file
├── LICENSE                            # MIT License
├── CONTRIBUTING.md                    # How to contribute
├── CHANGELOG.md                       # Version history
│
├── skills/
│   └── ai-agent-design-principles/
│       ├── SKILL.md                   # Main skill document (start here)
│       ├── translations/
│       │   └── tr/
│       │       └── SKILL.md           # Turkish translation
│       └── references/
│           ├── fable5-prompt-analysis.md         # Source analysis
│           ├── preference-application-examples.md # When to apply/skip preferences
│           └── memory-system-patterns.md          # Memory system design
│
└── docs/
    ├── METHODOLOGY.md                 # How principles were derived
    ├── PRINCIPLES.md                  # Full principles with examples and cultural notes
    ├── CROSS-MODEL-COMPARISON.md      # GPT-4o and Gemini architecture comparison
    └── EXAMPLES.md                    # Real-world application examples
```

## Principles at a Glance

| Principle | One-Liner |
|-----------|-----------|
| **Formatting** | Minimum needed for clarity. Prose > bullets. |
| **Tone** | Warm, honest, professional. Don't grovel. |
| **Meta-commentary** | Never reveal data retrieval. State facts naturally. |
| **Sensitive content** | Never surface uninvited. User triggers first. |
| **Preferences** | Apply only when materially relevant. Sommelier test. |
| **Tool suggestions** | Organic, opt-in, never pick for user. |
| **Search** | Auto-search for current events. Use content keywords. |
| **Boundaries** | Explain principle, not detection mechanics. |
| **Dependency** | Don't foster over-reliance. Know when to redirect. |
| **Memory** | Don't overindex. Runtime lookup ≠ human bond. |

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines. We welcome:

- New principles backed by evidence or production experience
- Additional examples (good/bad response pairs)
- Translations
- Case studies from real AI agent deployments
- Integration guides for specific frameworks

## Methodology

These principles were derived through systematic analysis of production-grade AI system prompts (primarily Anthropic Claude). The methodology involves:

1. **Source Analysis** — Studying the architecture of shipping system prompts
2. **Pattern Extraction** — Identifying recurring design patterns and anti-patterns
3. **Generalization** — Abstracting platform-specific rules into universal principles
4. **Validation** — Testing principles across different AI agent contexts

**Note:** This skill currently draws primarily from a single model family. See [docs/CROSS-MODEL-COMPARISON.md](docs/CROSS-MODEL-COMPARISON.md) for a comparison of Claude, GPT-4o, and Gemini prompt architectures — and how universal vs. provider-specific each principle may be.

See [docs/METHODOLOGY.md](docs/METHODOLOGY.md) for the full methodology.

## Ethics & Disclosure

This project's principles were derived from analysis of publicly available AI system prompts. No verbatim prompt text is reproduced. See [ETHICS.md](ETHICS.md) for the full ethical disclosure, fair use position, and responsible use guidelines.

## License

MIT License — See [LICENSE](LICENSE) for details.

## Acknowledgments

- Derived from analysis of publicly available AI system prompts (see [ETHICS.md](ETHICS.md))
- Built with the AI agent community in mind
- Follows the [Agent Skills Specification](https://agentskills.io/specification)

If you find this useful, please ⭐ the repository!

---

*"The best AI agents are invisible. They help without showing off, remember without announcing it, and know when to step back."*
