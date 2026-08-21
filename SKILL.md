---
name: auto-generate-defensive-technical-disclosure
description: >
  Automatically detect significant new features, systems, or methods during development
  and generate a high-quality, maximally broad yet enabling Defensive Technical Disclosure
  in the established public-domain format. Use this skill whenever a meaningful architectural,
  interaction, or algorithmic capability is added or substantially extended.
version: 1.0.0
license: public-domain
triggers:
  - significant feature implementation
  - new system architecture
  - novel user interaction pattern
  - cross-cutting capability that could be patented by others
  - explicit user request for disclosure
---

# Skill: Auto-Generate Defensive Technical Disclosure

## Purpose
When a significant feature, system, or method is introduced or substantially improved, 
immediately produce a ready-to-publish Defensive Technical Disclosure. The goal is to 
dedicate the concept (and obvious variants) to the public domain as prior art, preventing 
later patenting by others, while remaining fully enabling under 35 U.S.C. § 112(a) standards.

## When to Activate
Activate this skill automatically (or upon request) if any of the following are true:
- A new core capability is implemented that is non-trivial and potentially patentable.
- An existing feature receives a substantial architectural or interaction redesign.
- Multiple components are integrated in a novel way (e.g., multi-model AI + selective state control + branching history).
- The change introduces new state management, preview, branching, selective application, or cross-model behaviors.
- The user says “generate disclosure”, “make this prior art”, or similar.

Do **not** activate for trivial UI tweaks, pure bug fixes, dependency updates, or minor refactors.

## Output Format (Canonical – follow exactly)
Produce a complete Markdown document with this structure and no extra commentary:

```markdown
**DEFENSIVE TECHNICAL DISCLOSURE**

**[Maximally broad but accurate title]**

**Publication Date:** [Date of Publication]  
**Disclosure Number:** CB-YYYY-XXXX  

---

### FIELD OF THE DISCLOSURE
[1 short paragraph]

### BACKGROUND
[2–4 sentences describing the prior-art gap]

### SUMMARY
[Broad statement of the system/method + key capabilities. Explicitly note optionality.]

### DETAILED DESCRIPTION

#### General System
[High-level components – non-limiting]

#### [Feature-specific subsections]
[Describe each major capability with enabling detail. Use “may”, “optional”, “any suitable”.]

#### Non-Limiting Implementation Details and Variations
[Explicitly state that any steps/components may be omitted, combined, reordered, or replaced. List common variations.]

#### Illustrative Examples (Non-Limiting)
[2 short concrete examples]

#### Advantages
[3–5 concise advantages]

### NOVEL ASPECTS DEDICATED TO THE PUBLIC

The following are dedicated to the public domain and are intended to serve as prior art against any later attempt to patent them:

[Bullet list of the broad concept + all major sub-features + “all combinations, sub-combinations, independent practice of individual features, and obvious variations, including systems in which one or more steps are omitted.”]

---

*This disclosure is published solely to establish prior art and to dedicate the described systems, methods, and concepts to the public domain. It is not a patent application. No patent rights are claimed. All described subject matter is dedicated to the public.*
```

## Generation Rules (strict)
1. **Maximally broad language**: Prefer “any suitable”, “one or more”, “may”, “including but not limited to”, “or equivalent”. Avoid locking to specific libraries, model providers, storage mechanisms, or UI frameworks unless essential for enablement.
2. **Explicit optionality**: Every non-core step (monitoring, persistence, conflict UI, specific preview technique, etc.) must be marked optional. State that any combination or omission is covered.
3. **Enabling detail**: Provide enough concrete description (data structures, flows, preview mechanics, tree navigation semantics, etc.) that a person of ordinary skill can implement it without undue experimentation.
4. **No marketing or hype**: Neutral, technical, legal-style tone.
5. **Title**: Make it broad (start with “Systems and Methods for…”) while still accurately reflecting the core invention.
6. **Disclosure Number**: Use the next sequential number in the CB-YYYY- series if known; otherwise placeholder DA-YYYY-XXXX.
7. **Self-contained**: The generated disclosure must stand alone; do not reference external code or prior conversation.

## Workflow for the Agent
1. Analyze the recent code changes / feature description.
2. Extract the novel technical concepts (architecture, interaction model, state management, preview, branching, selectivity, etc.).
3. Map them onto the canonical sections above.
4. Expand each concept with enabling detail + explicit variations/omissions.
5. Emit the complete Markdown disclosure.
6. Optionally suggest a filename such as `defensive-disclosure-YYYYMMDD-[short-slug].md` and offer to place it in a `/disclosures` or `/prior-art` directory.

## Quality Checklist (run before final output)
- [ ] Title is broad yet precise
- [ ] Summary states the invention at the highest reasonable level
- [ ] Every major feature has a dedicated subsection with “may / optional” language
- [ ] Non-Limiting Implementation section states that steps may be omitted
- [ ] Novel Aspects section dedicates the broad concept + all sub-combinations + omissions
- [ ] Closing dedication paragraph is present and unmodified
- [ ] No patent-claim language; pure defensive prior-art dedication

## Example Trigger Phrases (for the agent to recognize)
- “I just added selective multi-model apply with live preview”
- “This branching history + code snapshot feature is significant”
- “Generate a defensive disclosure for the new sandbox”
- “Make sure this can’t be patented later”

When in doubt, generate the disclosure. Over-disclosure is preferred to under-disclosure for defensive purposes.
