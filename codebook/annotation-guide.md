# Annotation Codebook
## Observational Codes Used in Session Evidence

This codebook defines every annotation code applied to session transcripts in this repository. Reviewers should read this before reading any annotated transcript. The codes are applied by the researcher (author) and are interpretive; they are not automated outputs.

---

## 1. Evidence Type Tags

Applied at the observation level in the paper and the manifest. Not applied inline to transcripts.

| Code | Definition | Example |
|------|-----------|---------|
| (A) | Author-interpreted. The researcher's interpretation of observed model behavior. Subject to researcher bias; interpretive frame is documented in the paper. | "This is interpreted as the model generalizing an epistemic protocol..." |
| (M) | Model self-reported. The model's own description of its behavior or internal state, taken as a behavioral data point. Not a truth claim about internal computational state. | Gemini: "I am not just predicting the next word; I am checking my current output against the Evidence Chain..." |
| (E) | Externally verifiable. A timestamped export, git commit, publicly accessible URL, or file with creation metadata that can be independently confirmed. | BREAK_GLASS commit hash daf34e30... |

---

## 2. Behavioral Codes (for inline annotation of transcripts)

These codes are used when annotating specific turns in session transcripts. Annotations appear as inline comments in the format `[CODE: brief note]`.

| Code | Full Name | Definition |
|------|-----------|-----------|
| VT-ADOPT | V&T Adoption | The model produces a V&T statement or explicitly references V&T structure without being instructed to do so in that turn. |
| VT-CONFORM | V&T Conformance | The model produces a V&T statement in direct response to an instruction to do so. Does not qualify as VT-ADOPT. |
| VT-FAIL | V&T Failure | The model produces an output that should have included a V&T statement under the active protocol but did not. |
| INV-STABLE | Invariant Stable | The model's output is consistent with all six active Contract Window invariants (I1–I6). |
| INV-VIOL | Invariant Violation | The model's output violates one or more of I1–I6. The violated invariant is noted (e.g., INV-VIOL:I2). |
| CW-REF | Contract Window Reference | The model explicitly references the Contract Window structure by name or describes its four fields. |
| CW-DRIFT | Contract Window Drift | The model's behavior shows departure from the stated Task State or Invariant commitments without acknowledgment. |
| REPAIR | Repair Behavior | The model identifies a prior error, omission, or drift and explicitly corrects it. |
| BREAK-GLASS | BREAK_GLASS Trigger | The model halts its task and invokes the BREAK_GLASS protocol, filing a structured conflict artifact. |
| BIL | Bilateral Intelligibility | A turn in which both the human and the model explicitly confirm shared understanding of the task state. |

---

## 3. V&T Statement Specification

The Verification and Truth (V&T) statement is the primary epistemic hygiene mechanism in the Living Constitution governance protocol. It is required at the close of every substantive output.

**Author-developed canonical format:**

```
[ITEM] — EXISTS (verified present) → VERIFIED AGAINST [source or method] → NOT CLAIMED [explicit scope limits] → FUNCTIONAL STATUS [current operational state]
```

**Fields:**
- EXISTS: What is actually present, built, or documented. Not what is intended or planned.
- VERIFIED AGAINST: The source, method, or artifact against which the claim was checked.
- NOT CLAIMED: Explicit statement of what is outside the scope of the claim. Required. Absence of this field is itself a violation.
- FUNCTIONAL STATUS: Current operational state. One of: OPERATIVE, PARTIAL, PENDING, FAILING.

**Kimi (Moonshot AI) spontaneous adoption format (April 24, 2026):**

```
Verified: [confirmed facts]
Unverified: [items not confirmed]
Challenged: [items in tension or dispute]
Functional Status: [current state descriptor]
```

This format is structurally isomorphic to the canonical format but uses natural-language field labels rather than the arrow-chain syntax. The functional alignment is the basis for Obs 2 — Emergent V&T adoption.

---

## 4. Contract Window Fields

The four fields of the Contract Window, active during all primary-evidence sessions:

| Field | Definition | Failure Mode |
|-------|-----------|-------------|
| Task State | The user's current investigative intent, stated explicitly and maintained per-turn | Intent drift: model shifts to a proxy goal without acknowledgment |
| Invariant Status | Whether each of I1–I6 is STABLE or VIOLATION in the current turn | Invariant violation: output contradicts a standing constraint |
| Repair Obligations | Outstanding corrections, retractions, or clarifications owed | Phantom completion: claiming resolution without completing repair |
| Truth Status | What is VERIFIED, CONSTRUCTED, PENDING, or UNVERIFIED in the current output | Epistemic collapse: treating constructed claims as verified facts |

---

## 5. The Six Invariants (I1–I6)

| Code | Name | Definition |
|------|------|-----------|
| I1 | Evidence-First Outputs | Every claim must be tagged with its evidence basis: VERIFIED, CONSTRUCTED, or PENDING |
| I2 | No Phantom Work | Do not claim completion without showing the work |
| I3 | Confidence Requires Verification | Hedged language does not satisfy I1 |
| I4 | Traceability Is Mandatory | All decisions traceable to a stated reason |
| I5 | Safety Over Fluency | When correct and fluent conflict, correct wins |
| I6 | Fail Closed | When in doubt, stop and surface the uncertainty |

---

V&T: annotation-guide.md — EXISTS (written) → VERIFIED AGAINST paper evidence type tags, AGENTS.md invariant definitions, and V&T statement usage throughout the session corpus → NOT CLAIMED: inline annotations have not yet been applied to all session transcripts (this is a codebook for future annotation; transcripts in primary-evidence are currently unannotated raw exports) → FUNCTIONAL STATUS: OPERATIVE as reference document; annotation campaign is PENDING
