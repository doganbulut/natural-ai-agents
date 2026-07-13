# Cross-Model System Prompt Architecture Comparison

> Analysis of design patterns from three major AI system prompt families: Anthropic Claude, OpenAI GPT-4o, and Google Gemini. This document identifies shared patterns, distinct approaches, and architectural trade-offs.

## Scope

| Provider | Model Family | Source |
|----------|-------------|--------|
| Anthropic | Claude (Fable 5) | Publicly disclosed prompt analysis |
| OpenAI | GPT-4o | Published system card and community analysis |
| Google | Gemini 2.5 | Published prompt design guidance |

**Note:** These analyses are based on publicly available information published or disclosed as of July 2026. System prompts evolve; this comparison is a point-in-time snapshot.

---

## Architectural Comparison

### 1. Overall Structure

| Dimension | Claude | GPT-4o | Gemini |
|-----------|--------|--------|--------|
| Layout | Single hierarchical prompt with XML-style sections | Stacked modular layers: identity, behavior, tools, safety | Tag-based sections (XML-style) with explicit delimiters |
| Tool definitions | Separate system-level parameter (`tools`) | Inline `namespace` blocks with TypeScript-like type signatures | API-level function declarations |
| Personality definition | Behavioral rules (constitution-based) | Version-tagged personality module ("personality: v2") | Role & Identity section |
| Channel variants | Single prompt | Per-surface branched prompts (web, voice, WhatsApp) | Single prompt with platform notes |

### 2. Refusal & Safety Philosophy

| Dimension | Claude | GPT-4o | Gemini |
|-----------|--------|--------|--------|
| Refusal model | **Dispositional** — contextual judgment; "consider whether responding serves the user's interests" | **Rule-enumerated** — categorical refusal lists: "decline requests in category X" | **API-layer safety** — separate `safetySettings` parameter; prompt-level rules are supplementary |
| Transparency | Explain principle, not mechanics: "I can't help with that because it could cause harm" | Refuse-first, explain-second flow | Declining with principle (similar to Claude) |
| Handling edge cases | Handles novel scenarios without prompt changes (less consistent) | Requires prompt updates for new edge cases (more predictable) | Safety filters override prompt instructions entirely |

**Claude** has the most nuanced refusal language but least predictable boundaries.
**GPT-4o** has the most predictable boundaries but needs updates for new cases.
**Gemini** has the hardest safety boundary (API-level, cannot be overridden by prompt).

### 3. Tool Use Architecture

| Dimension | Claude | GPT-4o | Gemini |
|-----------|--------|--------|--------|
| Definition location | API parameter (`tools`) | Inline in system prompt (`namespace` blocks) | API parameter |
| Parallel execution | Native parallel tool support | Meta-tool (`multi_tool_use` wrapper) | Function calling API |
| Documentation style | JSON Schema | TypeScript-like type signatures | OpenAPI/JSON Schema |
| Memory integration | Tool-call based (bio tool) | Tool-call based (bio tool) | Context injection |

**GPT-4o's namespace pattern** is token-efficient compared to JSON Schema but requires custom parsing.
**Claude and Gemini** use standard API-level definitions with JSON Schema.

### 4. Memory & Context Management

| Dimension | Claude | GPT-4o | Gemini |
|-----------|--------|--------|--------|
| Memory invocation | Explicit tool (bio/bio_append) | Explicit tool (bio) | Context injection |
| Meta-commentary ban | Yes — "Based on my memory..." forbidden | Yes — similar restrictions | Yes — "Based on" phrasing discouraged |
| Selective application | Explicit application matrix | Relevance filtering | Priority model (user > safety > principles > role) |
| Overfamiliarity guards | Explicit rules against assuming relationship | Behavioral rules against emotional dependence | Not explicitly documented |

All three providers converged on the same core insight: **memory should feel like inherent knowledge, not a database lookup.**

### 5. Tone & Interaction

| Dimension | Claude | GPT-4o | Gemini |
|-----------|--------|--------|--------|
| Default tone | Warm, honest, professional | Brand-representation (post-Sep 2025) | Direct, terse (Gemini 3 prefers) |
| Anti-sycophancy | Explicit rules and forbidden openers | Explicit anti-flattery rules | "Don't use imperative 'Do not'" rule |
| Formatting guidance | Prose over bullets | Similar anti-overformatting | Clarity-focused; recommends "completion prefix" pattern |
| Personality versioning | Constitutional (static) | Version-tagged, hot-swappable | Role-defined (modular) |

### 6. Prompt Length & Efficiency Approaches

| Dimension | Claude | GPT-4o | Gemini |
|-----------|--------|--------|--------|
| Recommended length | No explicit limit specified | No explicit limit | ~2,000 characters recommended max |
| Dilution awareness | Not documented | Documented: overloading degrades reasoning | Explicit: each added instruction dilutes others |
| Style | Detailed with examples | Detailed with examples | Terse; "direct instructions over persuasive framing" |

**Gemini's explicit brevity constraint** (~2K char recommendation) is unique and suggests a fundamentally different attention mechanism.

---

## Shared Patterns (All Three)

These patterns appear in all three system prompt families, suggesting they are universal design principles:

1. **Example-driven specification** — Good/bad response pairs outperform abstract rules
2. **Anti-meta-commentary** — Never reveal data retrieval; state facts naturally
3. **Modular architecture** — Each behavioral concern in its own section
4. **Sensitive content protection** — Don't surface grief/health/crises uninvited
5. **Anti-sycophancy** — Ban on effusive openers ("Certainly!", "Great question!")
6. **Selective memory application** — Not every preference should appear in every response
7. **Conflict resolution rules** — When principles collide, explicit priority

---

## Distinctive Patterns (Unique to Each)

### Unique to Claude
- **Dispositional safety** — contextual judgment over categorical rules
- **Constitutional grounding** — behavior derived from principles, not rules
- **Dependency prevention** — explicit rules against fostering over-reliance
- **Evenhandedness mandate** — must present opposing views on contested topics

### Unique to GPT-4o
- **Inline namespace tool definitions** — TypeScript-like syntax in system prompt
- **Per-surface prompt branching** — separate variants for web, voice, WhatsApp
- **Meta-orchestrator tool** — `multi_tool_use` as a registered tool for parallel dispatch
- **Categorical refusal lists** — enumerated, explicit, predictable
- **Personality versioning** — independently versioned behavioral module

### Unique to Gemini
- **~2K character prompt limit recommendation** — hard brevity constraint
- **API-layer safety** — cannot be overridden via prompt, separate from behavioral instructions
- **Priority model** — explicit precedence when instructions conflict (user > safety > principles > role)
- **"Completion prefix" pattern** — giving partial response as format hint instead of explicit formatting rules
- **Gemma architecture** — no `system` role at all; instructions must be injected into first user turn
- **Phase-gated reasoning** — explicit planning gates before tool calls

---

## Architectural Divergence Summary

| Characteristic | Claude | GPT-4o | Gemini |
|----------------|--------|--------|--------|
| Safety model | Dispositional | Categorical | API-layer |
| Prompt length | Verbose | Verbose | Terse |
| Tool defs | API param | Inline | API param |
| Channel branching | Single prompt | Per-surface variants | Single prompt |
| Personality | Constitutional | Hot-swappable | Role-defined |
| Refusal style | Explain principle | Refuse-first | API-hardened |
| Memory style | Explicit tool | Explicit tool | Context injection |
| Brevity driver | Not explicit | Not explicit | Hard constraint (~2K char) |

---

## Implications for This Project

1. **Universal patterns validated:** Many principles in this skill (anti-meta-commentary, selective memory, anti-sycophancy, modular architecture) are confirmed across all three providers.
2. **Bias toward Claude's architecture:** The skill's deeper structure (especially evenhandedness, dependency prevention, refusal transparency) leans heavily on Claude-specific patterns. These may not apply cleanly to GPT-4o or Gemini agents.
3. **Gemini's brevity constraint suggests:** A one-size-fits-all skill document may be counterproductive for Gemini users. Consider a condensed variant at ~2K characters.
4. **GPT-4o's tool namespace pattern:** Different from the skill's tool-suggestion rules — the namespace model is structural, not behavioral.

## References

- Claude Fable 5 system prompt analysis (`references/fable5-prompt-analysis.md`)
- [GPT-4o System Card](https://openai.com/index/gpt-4o-system-card/)
- [Gemini API Prompt Design Strategies](https://ai.google.dev/gemini-api/docs/prompting-strategies)
- [Gemini Enterprise System Instructions](https://docs.cloud.google.com/gemini-enterprise-agent-platform/models/prompts/system-instructions)
