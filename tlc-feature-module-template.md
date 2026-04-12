# TLC FEATURE MODULE TEMPLATE
## Cognitive Mode Prompt + Programmatic Scaffold

---

## PART 1 — COGNITIVE MODE PROMPT FOR NEW FEATURE CREATION

Use this prompt in Claude Code or any model when designing a new TLC feature.
Paste SECTION A + SECTION B as a single message.

---

### SECTION A — DOCTRINE CONTEXT

```
You are designing a new feature for The Living Constitution (TLC).

Before writing a single line of code or documentation, you must pass 
the Feature Gate. Every TLC feature is governed by the Architectural 
Doctrine. There are no exceptions.

Use Synthetic + Operator + Practitioner modes.

Synthetic: Unify the feature's TLC integration role, standalone 
application identity, and consumer-facing product into one coherent 
design — no seams between the three.

Operator: Every design decision must land as a named file, a numbered 
step, an install command, or a binary criterion. No prose-only 
specifications.

Practitioner: Filter for what actually ships. If a design decision 
cannot be executed by a solo developer in a single session, it is 
deferred — not included.
```

---

### SECTION B — THE FEATURE GATE (answer every question before proceeding)

```
GATE 1 — ONE THING WELL

State the feature's single responsibility in this exact format:
  "This feature [active verb] [specific object]."

Rules:
  - No "and" allowed
  - No "also" allowed  
  - If you cannot state it without "and" — split the feature
  - The verb must describe what the feature PRODUCES, 
    not what it DOES INTERNALLY

Examples of PASSING:
  "This feature enforces invariants at the agent action boundary."
  "This feature detects behavioral absence as a safety signal."
  "This feature requires consent before every agent action."

Examples of FAILING:
  "This feature enforces invariants AND logs violations." ← split it
  "This feature manages governance." ← too vague
  "This feature integrates with TLC." ← that's component 1, not the thing

Your one thing: _______________________________________________

---

GATE 2 — THREE COMPONENT TEST

Answer all three. Each must be a complete sentence.

COMPONENT 1 — TLC Integration:
  "Within TLC, this feature is consumed by _____________ 
   and registered in _____________ with domain_binding: _____."

COMPONENT 2 — Standalone Installation:
  "A developer installs this without cloning TLC by running: 
   [exact command]
   After running that command and [exact next step], they will see: 
   [exact output]."

COMPONENT 3 — Consumer-Facing Product:
  "The user who is NOT a developer can [specific action] 
   at [URL or entry point] to [specific outcome]."
  "The value to that user in plain language is: _____________."
  "The pricing model is: _____________."

---

GATE 3 — RESEARCH CONTRIBUTION

State the citable finding in this exact format:
  "This feature demonstrates that [measurable outcome] 
   [increases/decreases/changes] when [the feature's intervention] 
   is applied, compared to [the baseline condition], 
   in a study of [population] using [methodology]."

The finding must be:
  - Falsifiable (someone could prove it wrong)
  - Novel (not already published with this specific intervention)
  - Executable (a solo researcher with limited resources can run it)

Your citable finding: _______________________________________________

What dataset or benchmark will you use? ____________________________
What is the control condition? _____________________________________
What would falsify this finding? ___________________________________

---

GATE 4 — DOCUMENTATION STANDARD

The default user has:
  - Poor spatial reasoning (prone to manic episodes from unclear instructions)
  - Autism profile: sensory-cognitive overload, navigation difficulties,
    trouble with mental rotation and multi-step spatial layouts
  - High friction from: visual-only explanations, diagrams without 
    explicit text labels, fast-changing environments, ambiguous paths

Your documentation MUST include ALL SIX of these elements. 
Check each when complete:

  [ ] WHAT THIS DOES — one sentence, active verb, no jargon
  
  [ ] WHAT THIS DOES NOT DO — explicit list of adjacent things 
      this feature is NOT responsible for
  
  [ ] STEP-BY-STEP INSTALLATION
      Every step numbered. No steps combined. Ever.
      Every step ends with: "You should see: [exact output]"
      Every potential mistake named BEFORE it can happen:
      "If you see [X], that means [Y] happened. Do [Z] to fix it."
  
  [ ] VISUAL ANCHOR — one diagram maximum
      Every element in the diagram labeled in text
      Caption explains every element explicitly
      No "see above" or "as shown" references
      Alternative text description of the diagram provided
  
  [ ] EXPLICIT PATH + NON-PATH
      "The correct path is: Step 1 → Step 2 → Step 3"
      "Do NOT do [X] before [Y]. [X] will fail silently."
      No implied ordering. Every dependency stated explicitly.
  
  [ ] WORKED EXAMPLE
      Input shown. Output shown. Both labeled.
      Format: "Input: [exact value]  →  Output: [exact value]"
      Example must be runnable as-is (no placeholder values)

---

GATE 5 — KNOWLEDGE SCAFFOLD + EXPANSION TEST

Answer both:

SCAFFOLD (what does the user understand after using this for 5 minutes?):
  "After 5 minutes with this feature, a user who knew nothing about 
   [domain] will understand: _______________"

EXPANSION (what does the user understand after using it for a week?):
  "After a week, that same user will have built toward: _______________"

The scaffold must be the foundation the expansion builds on.
The expansion must not be reachable without the scaffold.

---

GATE 6 — SELF-HOSTING CHECK

Every TLC feature is governed by TLC. Answer:

  "This feature's own build process is governed by Guardian mode: 
   [ ] YES — describe the invariant check: _______________
   [ ] NOT YET — this is the implementation step: _______________"

  "This feature is registered in projects/governance/registry.json:
   [ ] YES — registry entry path: _______________
   [ ] NOT YET — this is the Series B step: _______________"
```

---

## PART 2 — FEATURE_TEMPLATE.md

Copy this file to `features/[feature-name]/FEATURE_TEMPLATE.md` 
for every new TLC feature. Fill it in completely before writing code.

---

```markdown
# FEATURE: [name]
<!-- Fill every field. No field may be left blank or "TBD" -->

## Document Status
- Version: 0.1.0
- Gate status: [ ] PASSED / [ ] IN PROGRESS
- Last updated: [date]
- Author: [name]

---

## ONE THING WELL

> This feature [active verb] [specific object].

**Verification:** Read this sentence aloud. If it contains "and" 
or "also" — split the feature.

---

## THREE COMPONENTS

### Component 1 — TLC Integration
- Consumes from: 
- Registered in: projects/governance/registry.json
- Domain binding: [ ] Human / [ ] Cognitive / [ ] Epistemic / [ ] Empirical
- Invariant set: [list invariant IDs from invariant-registry.json]
- Evidence paths: docs/evidence/[feature-name]/

### Component 2 — Standalone Installation
```
# Exact install command — no placeholders
[install command]

# Exact next step
[next command]

# You should see:
[exact output]
```

### Component 3 — Consumer-Facing Product
- User who is NOT a developer: [description]
- Entry point: [URL or command]
- Value in plain language: [one sentence, no jargon]
- Pricing: [model and tiers]

---

## RESEARCH CONTRIBUTION

### Research Question
> What happens to [measurable outcome] when [intervention] is applied 
> vs. [baseline condition]?

### Study Design
- Dataset/benchmark:
- Sample size (n):
- Control condition:
- Primary metric:
- Secondary metrics:
- What would falsify this:

### Citable Finding (projected)
> This feature demonstrates that [measurable outcome] [direction] 
> when [intervention], compared to [baseline], in [population] 
> using [methodology].

### Publication Target
- Venue:
- Track:
- Deadline:

---

## DOCUMENTATION

### WHAT THIS DOES
[One sentence. Active verb. No jargon. No "and".]

### WHAT THIS DOES NOT DO
- This feature does NOT: [item 1]
- This feature does NOT: [item 2]
- This feature does NOT: [item 3]
<!-- Add more as needed. Be specific. -->

### INSTALLATION — STEP BY STEP

> Read this before starting:
> - You will need: [exact prerequisites, one per line]
> - This will take approximately: [time estimate]
> - If anything goes wrong, start at Step 1 again. Do not skip steps.

**Step 1: [action verb] [exact thing]**

```
[exact command or action]
```

You should see:
```
[exact expected output]
```

⚠️ If you see `[error message]` instead:
That means [plain language explanation of what went wrong].
Fix it by: [exact remediation steps]

**Step 2: [action verb] [exact thing]**

```
[exact command or action]
```

You should see:
```
[exact expected output]
```

<!-- Continue for every step. Never combine two actions into one step. -->

### VISUAL ANCHOR

[Diagram — maximum 1]

[Explicit text description of every element in the diagram:]
- Box labeled "[A]" means: [plain language]
- Box labeled "[B]" means: [plain language]
- Arrow from [A] to [B] means: [plain language]
- [Continue for every element]

### CORRECT PATH

The correct sequence is:
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Do NOT do [X] before completing Step [N].** [X] will [specific failure].
**Do NOT skip Step [N].** Skipping it causes [specific consequence].

### WORKED EXAMPLE

```
Input:  [exact value — no placeholders]
        
Output: [exact value — no placeholders]
```

**What happened:** [plain language explanation of what the feature 
did between input and output, one sentence per action]

---

## KNOWLEDGE SCAFFOLD + EXPANSION

### After 5 minutes (scaffold):
A user who knew nothing about [domain] will understand:
[one concrete concept, stated as a sentence]

### After one week (expansion):
That same user will have built toward:
[one concrete capability, stated as a sentence]

The scaffold is the prerequisite for the expansion. 
If the expansion is reachable without the scaffold — rewrite both.

---

## SELF-HOSTING STATUS

- [ ] Guardian mode governs this feature's build process
  - Invariant check: [description]
  - Evidence record location: docs/evidence/[feature]/
  
- [ ] Registered in projects/governance/registry.json
  - Entry: [path to registry entry]
  
- [ ] Passes verify_registry_schema.py
  - Command: `python scripts/verify_registry_schema.py`
  - Expected output: `[feature]: PASS`

---

## V&T STATEMENT

**Exists:**
- [list what is built and working]

**Non-Existence:**
- [list what is planned but not built]

**Unverified:**
- [list what is claimed but not yet evidenced]

**Functional Status:**
- Gate: [ ] PASSED / [ ] IN PROGRESS
- Component 1 (TLC): [ ] COMPLETE / [ ] PARTIAL / [ ] NOT STARTED
- Component 2 (Standalone): [ ] COMPLETE / [ ] PARTIAL / [ ] NOT STARTED
- Component 3 (Consumer): [ ] COMPLETE / [ ] PARTIAL / [ ] NOT STARTED
- Research: [ ] COMPLETE / [ ] DESIGN ONLY / [ ] NOT STARTED
- Documentation: [ ] ND-COMPLIANT / [ ] IN PROGRESS / [ ] NOT STARTED
```

---

## PART 3 — GATE CHECKER SCRIPT (run before committing any feature)

Save as `scripts/check_feature_gate.py` in the TLC repo.

```python
#!/usr/bin/env python3
"""
TLC Feature Gate Checker
Validates that a feature's FEATURE_TEMPLATE.md passes all 
Architectural Doctrine requirements before code is committed.

Usage:
    python scripts/check_feature_gate.py features/[feature-name]/FEATURE_TEMPLATE.md
"""

import sys
import re
from pathlib import Path


REQUIRED_SECTIONS = [
    "ONE THING WELL",
    "THREE COMPONENTS",
    "Component 1",
    "Component 2",
    "Component 3",
    "RESEARCH CONTRIBUTION",
    "Research Question",
    "Citable Finding",
    "DOCUMENTATION",
    "WHAT THIS DOES",
    "WHAT THIS DOES NOT DO",
    "INSTALLATION",
    "VISUAL ANCHOR",
    "CORRECT PATH",
    "WORKED EXAMPLE",
    "KNOWLEDGE SCAFFOLD",
    "SELF-HOSTING STATUS",
    "V&T STATEMENT",
]

FORBIDDEN_PATTERNS = [
    (r"This feature .+ and .+\.", "ONE THING WELL contains 'and' — split the feature"),
    (r"TBD", "Template contains TBD — fill in all fields"),
    (r"\[placeholder\]", "Template contains placeholder — fill in with real values"),
    (r"TODO", "Template contains TODO — complete before gate"),
    (r"Coming soon", "Template contains 'Coming soon' — not acceptable"),
]

REQUIRED_STEP_PATTERN = re.compile(
    r"\*\*Step \d+:.*\*\*.*You should see:", 
    re.DOTALL
)

REQUIRED_VT_FIELDS = [
    "Exists:", "Non-Existence:", "Unverified:", "Functional Status:"
]


def check_gate(filepath: str) -> bool:
    path = Path(filepath)
    if not path.exists():
        print(f"FAIL: File not found: {filepath}")
        return False

    content = path.read_text()
    failures = []

    # Check required sections
    for section in REQUIRED_SECTIONS:
        if section not in content:
            failures.append(f"MISSING SECTION: {section}")

    # Check forbidden patterns
    for pattern, message in FORBIDDEN_PATTERNS:
        if re.search(pattern, content, re.IGNORECASE):
            failures.append(f"FORBIDDEN PATTERN: {message}")

    # Check that installation has "You should see:" for each step
    steps = re.findall(r"\*\*Step \d+:", content)
    see_count = content.count("You should see:")
    if len(steps) > 0 and see_count < len(steps):
        failures.append(
            f"DOCUMENTATION: {len(steps)} steps found but only "
            f"{see_count} 'You should see:' confirmations. "
            f"Every step requires a confirmation."
        )

    # Check V&T statement completeness
    for field in REQUIRED_VT_FIELDS:
        if field not in content:
            failures.append(f"V&T STATEMENT: Missing field: {field}")

    # Check "one thing well" has no "and"
    one_thing_match = re.search(
        r"This feature (.+?)\.", content
    )
    if one_thing_match:
        one_thing = one_thing_match.group(1)
        if " and " in one_thing.lower():
            failures.append(
                f"ONE THING WELL: Contains 'and': '{one_thing}' — split the feature"
            )

    # Check worked example has no placeholder
    example_section = re.search(
        r"WORKED EXAMPLE.*?```(.*?)```", content, re.DOTALL
    )
    if example_section:
        example_text = example_section.group(1)
        if "[" in example_text and "]" in example_text:
            failures.append(
                "WORKED EXAMPLE: Contains placeholder values — "
                "replace with exact runnable values"
            )

    if failures:
        print(f"\n{'='*60}")
        print(f"FEATURE GATE: FAILED — {path.name}")
        print(f"{'='*60}")
        for f in failures:
            print(f"  ✗ {f}")
        print(f"\n{len(failures)} failure(s). Fix all before committing.")
        print(f"{'='*60}\n")
        return False
    else:
        print(f"\n{'='*60}")
        print(f"FEATURE GATE: PASSED — {path.name}")
        print(f"{'='*60}")
        print(f"  ✓ All {len(REQUIRED_SECTIONS)} required sections present")
        print(f"  ✓ No forbidden patterns")
        print(f"  ✓ All installation steps have confirmations")
        print(f"  ✓ V&T statement complete")
        print(f"  ✓ One thing well — no 'and' detected")
        print(f"{'='*60}\n")
        return True


if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python check_feature_gate.py <path/to/FEATURE_TEMPLATE.md>")
        sys.exit(1)
    
    passed = check_gate(sys.argv[1])
    sys.exit(0 if passed else 1)
```

---

## HOW TO DETERMINE "ONE THING WELL" FOR ANY FEATURE

Run this three-question protocol before designing any feature:

```
QUESTION 1 — What does it produce?
State the output as one noun phrase.
Test: Can you say it without "and"?
  YES → proceed to Q2
  NO  → split the feature

QUESTION 2 — Who depends on that output?
  "Everyone" → this is shared infrastructure, not a feature
  "One named system" → this is a feature, proceed to Q3

QUESTION 3 — What breaks if it doesn't run?
The specific thing that breaks IS the one thing it does.
Name the failure mode, not the function.
```

**Applied to each TLC feature:**

| Feature | One Thing Well | What breaks without it |
|---------|----------------|------------------------|
| PROACTIVE | Block confident false claims | Users act on unverified AI assertions |
| Prompting Machine | Inject optimal cognitive mode stack | Agents use generic reasoning instead of calibrated modes |
| Guardian | Enforce invariants at action boundary | Agent actions execute without invariant check |
| ConsentChain | Require consent before action | High-stakes actions execute without user consent |
| UICare | Detect behavioral absence as safety signal | ND developer distress goes undetected until crisis |
| Instructional Integrity | Detect false mental model induction | Learners build wrong mental models from correct content |
| MADMall | Reduce isolation for Black women with Graves' disease | Community has no governed safe space |
| Constitutional UI | Display governance state read-only | Governance health is opaque to operators and auditors |

**The test that validates "one thing well":**
Ask a 10-year-old: "If I turned this off, what specific bad thing would happen?"
If they can answer in one sentence — you have one thing.
If they say "many things" — you have multiple things.
