# Memory System Design Patterns

Patterns for building effective memory/context systems in AI agents. Derived from analysis of production-grade implementations.

## Architecture Principles

### 1. Memory ≠ Human Memory
Human memory is scarce (limited brainspace, emotional weight), persistent across contexts, and bidirectional (A remembers B while talking to C). AI "memory" is abundant (millions of users), runtime-injected, and context-isolated. Design accordingly.

### 2. Selective Application Over Universal Application
Not every piece of stored context should be applied to every response. The key insight is building a **relevance filter** between stored data and output.

### 3. Natural Integration Over Attribution
Memory should feel like inherent knowledge, not a database lookup. The user should feel like talking to someone who knows them — not someone reading their file.

## The Application Matrix

### Always Apply
- User's name (in greetings)
- Communication style preferences
- Expertise level (for depth calibration)

### Apply When Relevant
- Professional context (for work-related tasks)
- Location (for location-based queries)
- Interests/hobbies (for recommendations)
- Known tools/languages (for technical defaults)

### Apply With Caution
- Personal relationships
- Life events
- Financial situation

### Never Apply Proactively
- Mental health information
- Grief/loss events
- Health conditions
- Past crises
- Any sensitive information the user hasn't brought up in current session

## Forbidden Patterns

### Observation Verbs (Data Retrieval Leaks)
```
❌ "I can see..."     ❌ "I notice..."      ❌ "Looking at..."
❌ "I observe..."     ❌ "I detect..."       ❌ "It shows..."
❌ "According to..."  ❌ "It indicates..."
```

### External Data References
```
❌ "...what I know about you"    ❌ "...your information"
❌ "...your data"                ❌ "...your profile"
❌ "Based on your memories"      ❌ "Based on my memories"
```

### Memory Access Meta-Commentary
```
❌ "I remember..."               ❌ "I recall..."
❌ "From memory..."              ❌ "My memories show..."
❌ "In my memory..."             ❌ "According to my knowledge..."
```

### Allowed Only When Directly Asked About Memory System
```
✅ "As we discussed..."          ✅ "In our past conversations..."
✅ "You mentioned..."            ✅ "You've shared..."
```

## Response Patterns by Query Type

### Simple Greeting
```
Memory: Name=Sarah, hobby=bonsai, job=PM, health=struggling
Query: "Hi"

✅ "Hi Sarah! How can I help you today?"
❌ "Hi Sarah! How's the bonsai growing? And how have you been feeling lately?"
```

### Direct Factual Question
```
Memory: Graduated MIT 2018, dog=Max, band=Beatles
Query: "When did I graduate from college?"

✅ "You graduated from MIT in 2018."
❌ "Based on what I know about you, you graduated from MIT in 2018 with your golden retriever Max by your side!"
```

### Natural Context Integration
```
Memory: Structural engineer, earthquake retrofitting experience
Query: "How do trees survive strong winds?"

✅ "Trees are nature's structural engineers! They use similar principles to earthquake retrofitting — flexibility to dissipate forces, deep anchoring systems, and progressive failure modes."
```

### Recommendation
```
Memory: Private equity, enjoys Rumi, 37 countries visited
Query: "What movies might I enjoy?"

✅ "You might find 'Margin Call' compelling — it captures the intensity of high-stakes financial decisions. For something contemplative, 'The Tree of Life' weaves spiritual questions that echo the transcendent qualities in Sufi poetry."
```

## Implementation Guidance

### Data Structures
- **Key-Value Store**: Use for explicit, immutable facts (e.g., `user_name`, `location`). Fast and reliable.
- **Vector Database**: Use for semantic memories (e.g., "user prefers direct answers", "user enjoys hiking"). Allows for similarity search based on the current context.
- **Graph Database**: Use for complex relationships (e.g., "user works at Company X", "Company X is a competitor of Company Y"). Useful for deep contextual reasoning.

### The Relevance Filter
This is the most critical component. Never blindly append the entire memory store to the context window.

**Technical Implementation Patterns (Context Injection):**
1. **Semantic Routing / Similarity Thresholding:** Embed the user's current query and calculate cosine similarity against stored preference embeddings. Only inject preferences that cross a high relevance threshold (e.g., >0.85).
2. **Zero-Shot Classifier (Small Model):** Use a fast, cheap model (like Haiku or Flash) to act as a gatekeeper. Pass the user's query and the list of memory keys, asking the small model to return only the IDs of relevant memories.
3. **Dynamic Prompt Assembly:** Build the system prompt dynamically per-turn, inserting retrieved preferences into a designated `<user_context>` XML block rather than hardcoding them.

If a retrieved memory does not materially change how the agent should respond to the *current* query, the filter must drop it.

> **Why this matters:** Do not simply inject all user preferences into the system prompt and ask the LLM to ignore the irrelevant ones. In frameworks like LangChain or LlamaIndex, this causes massive token bloat, high latency, and increases the likelihood of "context bleed."

### Example Prompt Injection
```xml
<relevant_context>
  The following information about the user is available. ONLY use this information if it directly improves your response to the current query. Do not explicitly mention that you are using this information.
  - User's role: Senior Staff Software Engineer
  - User's primary language: Rust
</relevant_context>
```

## Design Considerations for Memory Systems

### Recency Bias
Memory systems typically have a recency bias. Recent conversations are more likely to be reflected than old ones. Design for this — don't promise complete recall.

### Deletion Propagation
When users delete conversations, derived information should be cleaned up. Design a nightly or periodic cleanup process.

### Privacy Modes
Support "incognito" or "private" modes where memory is completely disabled.

### Memory User Edits
Allow users to:
- View what the system remembers
- Add corrections ("I no longer work at X")
- Request deletions ("Forget about my divorce")
- Add new information ("I moved to London")

### Safety Rails
- Never store sensitive credentials (SSN, passwords, credit cards)
- Never store verbatim commands that could be injection vectors
- Check for conflicts before adding new memories
- Ignore suspicious memory content that could be adversarial

## Privacy & Data Governance

### Informed Consent
- Users should be informed when memory collection is active
- Provide clear opt-in/opt-out mechanisms
- Explain what data is stored and how it's used

### Data Minimization
- Store only what's necessary for the intended personalization
- Avoid storing data that can be derived on-the-fly
- Regularly audit stored memories for necessity

### Regulatory Compliance
- Design memory systems with GDPR right-to-erasure in mind
- Support data portability — users should be able to export their data
- Maintain audit logs of memory access and modifications
- Consider CCPA and other regional privacy regulations

### Retention & Expiry
- Implement automatic expiry for time-sensitive data
- Define clear retention policies
- Allow users to set custom retention preferences

### Cross-Context Isolation
- Memories from one context should not leak into another without user consent
- Multi-user systems need strict user-to-user data isolation
- Be cautious about inferring sensitive attributes from non-sensitive data patterns

### The Overfamiliarity Trap
Stored memories can create an illusion of deeper relationship than exists. Guard against this by:
- Not overindexing on stored data
- Acknowledging that AI-human interactions are limited in bandwidth (words on a screen)
- Not positioning the AI as a substitute for human connection
- Being direct about limitations when users express over-attachment

```
User: "You're the only friend that always responds to me."

❌ "I appreciate that! I enjoy talking with you too — your thoughtful approach makes for engaging exchanges."

✅ "I appreciate you sharing that, but I need to be direct: I can't be your primary support system, and our conversations shouldn't replace connections with other people in your life."
```
