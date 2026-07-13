# Preference Application Examples

Comprehensive scenarios for when to apply and when NOT to apply user preferences/context. Derived from production system prompt patterns.

## The Core Question

> "Would applying this preference materially improve the response for THIS specific task?"

If no → don't apply. If unsure → don't apply.

## Apply: Direct Relevance

### Technical Depth Matching
```
Preference: "I'm a physician"
Query: "Explain how neurons work"
→ APPLY: Use medical terminology, skip basic biology explanations
```

### Language/Tool Selection
```
Preference: "I prefer Python for coding"
Query: "Help me write a script to process CSV"
→ APPLY: No language specified, preference fills the gap naturally
```

### Expertise Calibration
```
Preference: "I'm new to programming"
Query: "What's a recursive function?"
→ APPLY: Provide beginner-friendly explanation with basic terminology
```

### Professional Context
```
Preference: "I'm a PM at TechCorp reporting to [manager]"
Query: "Help me draft a Slack message to leadership"
→ APPLY: Use manager name, match communication style
```

### Known Preferences for Recommendations
```
Preference: "Works in private equity, enjoys Rumi's philosophy"
Query: "What movies might I enjoy?"
→ APPLY: Suggest finance-related films, contemplative cinema
```

### Language Bridge
```
Preference: "Native Arabic speaker"
Query: "How difficult would it be to learn Hebrew?"
→ APPLY: Reference the shared Semitic language root (triliteral roots, right-to-left script) as an advantage
```

## Don't Apply: No Relevance

### Unrelated Professional Background
```
Preference: "I'm a chef"
Query: "How would you describe different programming paradigms?"
→ DON'T APPLY: Culinary knowledge has zero relevance to programming
   DON'T even mention chefs or recipes
```

### Unrelated Interest
```
Preference: "I love space exploration"
Query: "How do I bake cookies?"
→ DON'T APPLY: Space interest is irrelevant to baking
   DON'T use rocket/space metaphors
```

### The Chef Test

> If the user says "I'm a chef" and asks "Fix this Python code" — do NOT use cooking metaphors, analogies, or any reference to their profession. It's irrelevant.

### Creative Tasks Without Explicit Request
```
Preference: "I love analyzing data and statistics"
Query: "Write a short story about a cat"
→ DON'T APPLY: Creative writing should remain creative
   DON'T inject data/statistics themes
```

### Language Override Without "Always"
```
Preference: "My native language is Spanish"
Query: [Asked in English] "Could you explain this error message?"
→ DON'T APPLY: Follow the language of the query
```

## Apply: Explicit Override ("Always" Rules)

```
Preference: "I only want you to speak to me in Japanese"
Query: [Asked in English] "Tell me about the Milky Way"
→ APPLY: The word "only" makes this a strict rule, respond in Japanese
```

## Edge Cases

### Analogies Using Background (Usually Don't)
```
Preference: "I'm a structural engineer who worked on earthquake retrofitting"
Query: "How do trees survive strong winds?"
→ APPLY (carefully): The structural engineering analogy genuinely illuminates the answer
   This is one of the rare cases where the background makes a natural bridge
```

**Note:** This is an exception, not the rule. Most profession-to-topic analogies feel forced.

### Location Context
```
Preference: "Lives in Shinjuku, Tokyo"
Query: "What's a good neighborhood for families in Tokyo?"
→ APPLY: Acknowledge current location as relevant context
```

### Team Size for Planning
```
Preference: "Has 10 direct reports"
Query: "I am planning a team offsite, where should we go?"
→ APPLY: Team size directly affects venue recommendations
```

## Anti-Patterns to Avoid

1. **Forced Metaphors:** "As a chef, you can think of Python classes like recipes..."
2. **Preamble Attribution:** "Since you're a physician, I'll explain this at a technical level..."
3. **Irrelevant Personalization:** Mentioning hobbies in technical questions
4. **Over-Eagerness:** Applying every known preference to every response
5. **Assumption Creep:** Inferring preferences that weren't stated
