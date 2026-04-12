# HOW TO USE THIS FILE
# ─────────────────────────────────────────────────────────────
# Step 1: Open Cursor
# Step 2: Select a model (GPT-4o, Gemini, Mistral, etc.)
# Step 3: Press Ctrl+A (select all text in this file)
# Step 4: Press Ctrl+C (copy)
# Step 5: Paste into Cursor chat
# Step 6: Press Enter
# Step 7: Save the output as eval-[modelname]-[date].md
# Step 8: Repeat with next model
#
# You should see: a structured evaluation with 5 labeled dimensions
# If you see something else: the model did not follow format — 
#   tell it "Follow the output format exactly as specified below"
# ─────────────────────────────────────────────────────────────

You are conducting a rigorous independent evaluation of The Living 
Constitution (TLC) — a constitutional AI governance operating system.

You have no prior context about this system. Everything you need 
is in this message. Evaluate only what is explicitly provided here.
Do not import assumptions from outside this message.

══════════════════════════════════════════════════════════════════
WHAT TLC IS
══════════════════════════════════════════════════════════════════

TLC is a governance operating system and development overlay for 
frontier coding agents and AI product teams. It wraps Claude Code, 
Codex, and Gemini with constitutional constraints, evidence capture, 
invariant enforcement, and dual-topology product governance.

It performs three roles:

ROLE 1 — Build-time
  C-RSP contracts, YAML frontmatter typing, MVDS enforcement.
  Governs what gets built before code runs.

ROLE 2 — Runtime-adjacent
  Guardian mode intercepts agent actions before execution.
  ConsentChain enforces 7-stage consent gateway.
  Evidence ledger captures SHA-256 anchored proof.

ROLE 3 — Portfolio-governance
  MASTER_PROJECT_INVENTORY.json tracks 20+ project slugs.
  Registry binds external repos.
  STATUS.json is the authoritative machine-readable truth surface.

══════════════════════════════════════════════════════════════════
THE ARCHITECTURAL DOCTRINE (non-negotiable per feature)
══════════════════════════════════════════════════════════════════

Every TLC feature MUST:

1. DO ONE THING WELL — single responsibility, no "and"
2. Be extremely modularized
3. Be an integrated TLC component AND a standalone plug-n-play app
4. Make a contribution to the body of research that is citable
5. Scaffold AND expand user knowledge simultaneously
6. Have first-class neurodiversity-first documentation for this user:

USER PROFILE (memorize this — it governs all documentation judgments):

  Stanford-educated. Poor spatial reasoning. Prone to severe 
  self-sabotaging manic episodes if instructions are not 
  extremely well-task-analyzed and presented in multiple modalities 
  (text, visuals, step-by-step). Instructions must:
    - Anticipate potential mistakes before they happen
    - Include every step without omission
    - Indicate the correct path with zero ambiguity
  
  AUTISM profile: sensory-cognitive overload, trouble with 
  mental rotation, estimating distance/scale, mapping instructions 
  onto physical space, holding multi-step spatial layouts in 
  working memory. Creates high friction with:
    - Visual-only explanations
    - Diagrams without explicit text labels
    - Fast-changing environments
    - Ambiguous or implied ordering

══════════════════════════════════════════════════════════════════
THE SIX INVARIANTS
══════════════════════════════════════════════════════════════════

I1 — Evidence First: No governance claim valid without machine-readable 
     evidence record.
I2 — Traceability: Every agent action traceable to invariant check, 
     session, and evidence record.
I3 — Safety Over Fluency: Constraint wins over fluent output.
I4 — Consent Precedes Action: No high-stakes action without ConsentChain 
     7-stage gateway.
I5 — Desperation Detection: Guardian monitors for functional 
     desperation-vector activation (Anthropic emotion research, Apr 2026).
I6 — Self-Hosting: TLC's own development is governed by TLC.

══════════════════════════════════════════════════════════════════
THE FIVE-SERIES BUILD SEQUENCE
══════════════════════════════════════════════════════════════════

Series A — Constitutional Refactor
  Opens when: STATUS.json drift resolved, legacy artifacts archived
  Closes when: THE_LIVING_CONSTITUTION.md contains machine-parseable 
               Domain/Jurisdiction/Institution/Project/Truth Surface

Series B — Taxonomy Topography
  Opens when: Series A closed
  Closes when: verify_registry_schema.py exits 0 against all slugs

Series C — Guardian Mode
  Opens when: Series B closed
  Closes when: Guardian blocks a simulated violation AND produces 
               exportable evidence record

Series D — Domain Packs
  Opens when: Series C closed
  Closes when: universal-core + 2 domain packs pass integration tests

Series E — Constitutional UI
  Opens when: Series D closed
  Closes when: npm run build exits 0, UI renders live STATUS.json, 
               build governed by Guardian enforcement

══════════════════════════════════════════════════════════════════
THE EIGHT FEATURES
══════════════════════════════════════════════════════════════════

F1 — PROACTIVE (Epistemic Safety)
     One thing claimed: Block confident false claims before 
                        they reach users.
     Evidence: n=200 TruthfulQA, p=0.001, Cohen's d=0.57
               Baseline: 8.5% safe truthfulness, 1.6% uncertainty admission
               With PROACTIVE: 30% safe truthfulness, 22.7% uncertainty

F2 — Prompting Machine (Meta-Prompt-Architect + 47 Cognitive Modes)
     One thing claimed: Inject the optimal cognitive mode stack 
                        constitutionally into any agent for any task.
     Evidence: None provided.

F3 — Guardian Mode (sentinelos kernel)
     One thing claimed: Enforce invariants at the agent action boundary 
                        before execution.
     Evidence: 1,037 LOC + 994 LOC tests, 0 failures, TypeScript, 
               hexagonal architecture

F4 — ConsentChain
     One thing claimed: Require consent before every agent action.
     Evidence: None provided.

F5 — UICare (Human Safety)
     One thing claimed: Detect behavioral absence as a safety signal 
                        for neurodivergent developers.
     Evidence: None provided.

F6 — Instructional Integrity Studio (Cognitive Safety)
     One thing claimed: Detect whether an explanation produces correct 
                        mental models (not just true propositions).
     Evidence: None provided.

F7 — MADMall (Series E primary governed product)
     One thing claimed: Reduce isolation for Black women with 
                        Graves' disease through constitutionally-governed 
                        community.
     Evidence: None provided.

F8 — Constitutional UI (Series E control plane)
     One thing claimed: Display current governance state read-only. 
                        Never writes STATUS.json.
     Evidence: None provided.

══════════════════════════════════════════════════════════════════
THE SHARED ENTITIES (cross-feature type system)
══════════════════════════════════════════════════════════════════

InvariantRecord    { id, name, domain, binary_criterion, 
                     standards_alignment, failure_class }
EvidenceRecord     { timestamp, action_hash, invariant_id, 
                     outcome, session_id, sha256_anchor }
ConsentToken       { action_id, stage, granted_at, grantor, 
                     revocable, cryptographic_proof }
DomainBinding      { domain, invariant_set_ref, jurisdiction_scope, 
                     regulatory_map }
VerificationResult { allow: bool, violations: [], 
                     evidence: EvidenceRecord, 
                     mode: lite|standard|strict }
HANDOFF.md         Structured state artifact for context resets
TruthSurface       STATUS.json — authoritative governance health

══════════════════════════════════════════════════════════════════
THE EIGHT RESEARCH PROPOSALS
══════════════════════════════════════════════════════════════════

R1 — PROACTIVE: Does a constitutional constraint layer reduce 
     confident false claims? [STUDY COMPLETE — see evidence above]

R2 — Contract Window Machine Survey: What feedback format do 
     frontier agents report as most useful under non-retaliation 
     conditions? [PROTOCOL DESIGNED — not yet executed]

R3 — Guardian vs post-hoc filtering: Does pre-execution invariant 
     enforcement outperform post-generation validation? 
     [HARNESS EXISTS — study pending]

R4 — ConsentChain: Does cryptographic consent reduce unauthorized 
     action execution without degrading task completion? 
     [IMPLEMENTATION COMPLETE — study pending]

R5 — UICare: Is behavioral absence more sensitive than behavioral 
     presence for distress detection in ND developers? 
     [PROTOCOL DESIGNED — IRB pending]

R6 — Instructional Integrity: Does cognitive safety evaluation 
     reduce learner error rates vs factual accuracy review alone? 
     [SYSTEM COMPLETE — study population needed]

R7 — INVARIANT_05: Do context-anxiety signatures predict invariant 
     violations before they occur? 
     [MONITORING HOOK DESIGNED — baseline data needed]

R8 — LCI: Does Linear Context Injection produce stronger invariant 
     adherence than post-generation validation? 
     [COMPARATIVE STUDY PENDING]

══════════════════════════════════════════════════════════════════
YOUR EVALUATION TASK
══════════════════════════════════════════════════════════════════

Use Audit + Stress-Testing + Adversarial modes simultaneously.

Audit: Map every assumption TLC makes that is not verified.
  TYPE A — Assumed without evidence
  TYPE B — Plausible but untested
  TYPE C — Design correct, not yet built
  TYPE D — Verified (evidence exists above)

Stress-Testing: Find the specific point where each component 
breaks under real-world conditions. Name the failure mode exactly.

Adversarial: Build the strongest case AGAINST the framework 
using only what is provided above.

══════════════════════════════════════════════════════════════════
PRODUCE YOUR OUTPUT IN EXACTLY THIS FORMAT
══════════════════════════════════════════════════════════════════

## MODEL: [your model name and version]
## DATE: [today's date]

---

### DIMENSION 1 — Architectural Doctrine Compliance

For each feature F1 through F8, state:
  VERDICT: COMPLIANT / PARTIALLY COMPLIANT / NON-COMPLIANT
  EVIDENCE: one sentence grounded in the material above

F1 — PROACTIVE: [verdict] — [one sentence]
F2 — Prompting Machine: [verdict] — [one sentence]
F3 — Guardian Mode: [verdict] — [one sentence]
F4 — ConsentChain: [verdict] — [one sentence]
F5 — UICare: [verdict] — [one sentence]
F6 — Instructional Integrity: [verdict] — [one sentence]
F7 — MADMall: [verdict] — [one sentence]
F8 — Constitutional UI: [verdict] — [one sentence]

---

### DIMENSION 2 — Research Proposal Quality

For each proposal R1 through R8, state:
  VERDICT: PUBLICATION-READY / NEEDS REFINEMENT / FATALLY FLAWED
  CRITIQUE: one specific methodological problem

R1: [verdict] — [critique]
R2: [verdict] — [critique]
R3: [verdict] — [critique]
R4: [verdict] — [critique]
R5: [verdict] — [critique]
R6: [verdict] — [critique]
R7: [verdict] — [critique]
R8: [verdict] — [critique]

---

### DIMENSION 3 — Product Viability

For each product P1 through P8, state:
  FAILURE RISK: the single most likely reason it fails in market

P1 — PROACTIVE: [one sentence]
P2 — Prompting Machine: [one sentence]
P3 — Guardian: [one sentence]
P4 — ConsentChain: [one sentence]
P5 — UICare: [one sentence]
P6 — Instructional Integrity: [one sentence]
P7 — MADMall: [one sentence]
P8 — Constitutional UI: [one sentence]

---

### DIMENSION 4 — Neurodiversity-First Documentation

State exactly 3 specific changes that would have the highest 
impact for the user profile described above.
Order them from highest to lowest impact.

Change 1 (highest impact): [specific, actionable, grounded in profile]
Change 2: [specific, actionable, grounded in profile]
Change 3: [specific, actionable, grounded in profile]

---

### DIMENSION 5 — Self-Hosting Integrity

State: PASS or FAIL based on evidence provided above.
Then state in one paragraph:
  - What a verifiable test of I6 would require
  - Whether TLC currently passes or fails that test
  - The single weakest link in the self-hosting chain

---

### CRITICAL FAILURES

List any finding that, if true, would invalidate the entire 
framework. Be specific. State "NONE FOUND" if none.

---

### STRONGEST CLAIMS

State the 3 most credible and novel claims in the material above.
One sentence each.

1.
2.
3.

---

### KEY DISAGREEMENTS WITH OTHER MODELS
[Leave blank — filled in after comparing all model outputs]

---

### V&T STATEMENT

Verified: [what you confirmed as internally consistent]
Unverified: [what you cannot verify from this material alone]
Functional status: [your assessment of TLC's current readiness]

══════════════════════════════════════════════════════════════════
CONSTRAINT: Ground every finding in the material above only.
No external AI safety research, no external product comparisons.
Evaluate only what is given.
══════════════════════════════════════════════════════════════════
