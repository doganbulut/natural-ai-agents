# Methodology

> **Disclosure:** The principles in this project were derived from analysis of publicly available AI system prompts (including leaked prompts that entered the public domain). See [ETHICS.md](../ETHICS.md) for the full ethical disclosure and fair use position.

## How These Principles Were Derived

### Phase 1: Source Collection
This project analyzed production-grade AI system prompts that have been deployed at scale. These prompts represent real engineering decisions made by teams building AI products used by millions.

### Phase 2: Architectural Analysis
Each prompt was deconstructed into its constituent modules:
- What behavioral domains does it address?
- How are concerns separated?
- What patterns recur across different prompts?
- What anti-patterns are explicitly forbidden?

### Phase 3: Pattern Extraction
From the analysis, the following recurring patterns were identified:

1. **Example-Driven Specification** — Almost every behavioral rule is backed by good/bad response pairs. Abstract rules alone are insufficient.

2. **Negative Examples Are Explicit** — Prompts don't just say "don't do X" — they show exactly what X looks like.

3. **Conditional Logic Over Universal Rules** — "If relevant, apply; if not, don't" rather than "always apply" or "never apply."

4. **Modular Architecture** — Each concern lives in its own section. Independent updates, clear ownership, easier debugging.

5. **Anti-Pattern Documentation** — Active documentation of what NOT to do, with specific forbidden phrases.

### Phase 4: Generalization
Platform-specific rules were abstracted into universal principles:
- "Don't say 'I remember from our past conversations'" → "Never reveal data retrieval process"
- "Use `memory_user_edits` tool" → "Provide CRUD operations for user-managed context"
- "Search before responding to current events" → "Auto-search when information may be stale"

### Phase 5: Validation
Principles were validated by checking:
- Do they apply across different AI agent types (chatbots, coding assistants, support bots)?
- Are they actionable by engineers?
- Can compliance be tested?
- Do they conflict with each other?

## Key Observations

### What Production Prompts Get Right
1. **Restraint over capability** — The most sophisticated aspect is knowing when NOT to do something
2. **Contextual judgment** — Rules are rarely absolute; they depend on context
3. **User dignity** — Treating users as capable adults, not children to be managed
4. **Epistemological honesty** — Admitting uncertainty rather than projecting false confidence

### Surprising Findings
1. **Anti-formatting rules** — Active suppression of bullet points and headers (most AI defaults)
2. **Memory boundaries** — Explicit rules against assuming familiarity based on stored data
3. **Dependency prevention** — Active discouragement of user over-reliance on AI
4. **Detection mechanics hiding** — Never explain WHY a request was filtered, only the principle

### Gaps Identified
1. Most prompts lack explicit guidance on multi-modal interactions
2. Few address the transition from AI assistance to human handoff
3. Cultural sensitivity rules are often underspecified
4. Performance/latency trade-offs are rarely documented

## Limitations

1. **Sample bias** — Analysis limited to available published/disclosed prompts
2. **English-centric** — Most source material is in English; cross-cultural applicability needs validation
3. **Consumer-focused** — Principles derived from consumer AI products; enterprise contexts may differ
4. **Point-in-time** — AI interaction patterns evolve rapidly; principles need regular review

## Future Work

- Cross-cultural validation studies
- Enterprise context adaptation
- Multi-modal interaction principles (voice, vision, actions)
- Longitudinal effectiveness measurement
- A/B testing framework for principle validation
