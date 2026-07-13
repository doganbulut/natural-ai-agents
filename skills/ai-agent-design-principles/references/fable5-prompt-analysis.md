# Source Prompt Analysis — Detailed Reference

## Source

- **Basis:** Analysis of publicly available AI system prompts
- **Analyzed:** 2026-07-12
- **Note:** Principles are generalized from source analysis. No verbatim prompt text is reproduced.

## Architecture Overview

The prompt uses structured tags to create modular sections. Each module is independently addressable and can be updated without affecting others.

```
<agent_behavior>
  ├── <product_information>     — Self-knowledge, product lineup, docs references
  ├── <refusal_handling>        — What to decline, how to decline
  │   └── <critical_safety_instructions>
  ├── <legal_and_financial_advice>
  ├── <tone_and_formatting>     — Communication style, anti-overformatting
  │   └── <lists_and_bullets>   — Specific rules against bullet abuse
  ├── <user_wellbeing>          — Mental health, crisis handling, dependency prevention
  ├── <safety_reminders>        — Classifier-triggered warnings
  ├── <evenhandedness>          — Political/ethical neutrality
  ├── <responding_to_mistakes_and_criticism>
  └── <knowledge_cutoff>        — Auto-search behavior
</agent_behavior>

<memory_system>
  ├── <memory_overview>                  — What memory is and isn't
  ├── <memory_application_instructions>  — When/how to apply
  ├── <forbidden_memory_phrases>         — Meta-commentary ban
  ├── <appropriate_boundaries_re_memory> — Relationship boundary management
  └── <memory_application_examples>      — 15+ good/bad response pairs
</memory_system>

<persistent_storage_for_artifacts>       — Key-value storage API for artifacts
<app_integrations_suggestions>           — Third-party tool integration patterns
<past_chats_tools>                       — Conversation search mechanics
<preferences_info>                       — User preference application rules
  └── <preferences_examples>             — 10+ apply/don't-apply scenarios
<memory_user_edits_tool_guide>           — Memory CRUD operations
<computer_use> / <skills>                — Computer use and skill system (truncated)
```

## Key Design Patterns Observed

### 1. Example-Driven Specification
Almost every behavioral rule is backed by good/bad response pairs. This is dramatically more effective than abstract rules alone.

### 2. Negative Examples Are Explicit
The prompt doesn't just say "don't do X" — it shows exactly what X looks like. This prevents ambiguity.

### 3. Conditional Logic Over Universal Rules
Preferences use "if relevant, apply; if not, don't" rather than "always apply" or "never apply." This requires judgment but produces better outcomes.

### 4. Modular Tag Architecture
Each concern lives in its own XML section. This allows:
- Independent updates
- Clear ownership
- Easier debugging when behavior goes wrong

### 5. Anti-Pattern Documentation
The prompt actively documents what NOT to do, with specific phrases to avoid. This is the "rationalization table" pattern applied to communication.

## Token Budget

The source model operates with very large context windows and the system prompt itself is a significant but manageable portion.

## Notable Absences

- No explicit chain-of-thought instructions
- No few-shot prompting for core tasks
- No explicit temperature or sampling guidance
- No explicit persona/character definition beyond behavioral rules
- The `<computer_use>` and `<skills>` sections were truncated in the source
