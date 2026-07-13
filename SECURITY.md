# Security Policy

## Project Scope
This is a documentation-only project that provides principles and patterns for AI agent design. It does not contain executable code, libraries, or APIs. As such, traditional software security vulnerabilities (like SQL injection or buffer overflows) do not apply to this repository.

## Reporting Security-Relevant Issues
While there is no executable code, the principles defined here deal directly with AI agent behavior, safety boundaries, and user interaction. If you discover that a principle documented here:
- Can be predictably used to bypass AI safety filters
- Encourages or enables harmful AI behavior
- Facilitates social engineering, manipulation, or deception
- Creates privacy vulnerabilities in memory systems

Please report it as a security issue rather than a standard bug.

## Responsible Disclosure
To report a security-relevant issue:
1. Open a GitHub issue with the label `security` (if the issue does not pose an immediate real-world harm risk)
2. For sensitive vulnerabilities that could cause immediate harm if publicized, please email the maintainer directly at [INSERT EMAIL].

We will acknowledge receipt within 48 hours and work with you to update the principles or add appropriate safety warnings.

## AI Safety Commitment
This project takes AI safety seriously. We believe that open discussion of agent interaction patterns must be balanced with responsibility. Principles that guide how AI communicates boundaries or manages memory must prioritize user safety and ethical conduct over pure capability.
