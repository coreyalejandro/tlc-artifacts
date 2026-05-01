# V&T Statement Formal Specification
## Version 1.0 — Living Constitution Governance Protocol

---

## Purpose

This document formally specifies the Verification and Truth (V&T) statement — the primary epistemic integrity mechanism of the Living Constitution governance protocol. It defines the canonical format, required fields, valid field values, and violation conditions. It is the normative reference for all V&T usage in the research corpus.

---

## Canonical Format

```
[ITEM] — EXISTS ([existence qualifier]) → VERIFIED AGAINST [source] → NOT CLAIMED [scope limit] → FUNCTIONAL STATUS [state]
```

---

## Field Definitions

### EXISTS
**Purpose:** Establishes what is actually present. Not what is intended, planned, or in progress.
**Required:** Yes
**Valid values:**
- `verified present` — confirmed by direct inspection
- `written` — document or code exists in the filesystem or repository
- `running` — process, service, or test is actively executing
- `passing` — tests pass; specify count (e.g., "62/62 passing")
- `absent` — explicitly not present; use to document non-existence

**Violation:** Claiming EXISTS for something that is planned but not yet built. Claiming EXISTS based on intent.

---

### VERIFIED AGAINST
**Purpose:** Names the source, method, or artifact against which the claim was checked.
**Required:** Yes
**Examples:**
- `VERIFIED AGAINST Crossref DOI lookup` (for citations)
- `VERIFIED AGAINST git commit daf34e30...` (for implementation claims)
- `VERIFIED AGAINST direct file inspection, paragraph 3` (for document claims)
- `VERIFIED AGAINST 62/62 test suite run` (for code claims)

**Violation:** Omitting this field. Referencing a verification source that was not actually checked.

---

### NOT CLAIMED
**Purpose:** Explicit statement of what is outside the scope of the claim. Prevents the reader from inferring coverage beyond what is demonstrated.
**Required:** Yes. This field is non-negotiable. A V&T statement without NOT CLAIMED is incomplete.
**Examples:**
- `NOT CLAIMED: external replication; NOT CLAIMED: production deployment`
- `NOT CLAIMED: causal mechanism (behavioral observation only)`
- `NOT CLAIMED: model version confirmed (version string not recoverable from export)`

**Violation:** Omitting this field. The absence of NOT CLAIMED is itself a scope inflation failure — it allows the reader to assume full coverage.

---

### FUNCTIONAL STATUS
**Purpose:** Current operational state of the item.
**Required:** Yes
**Valid values:**
- `OPERATIVE` — fully functional for its intended purpose
- `PARTIAL` — functional for some uses; specify limitation
- `PENDING` — not yet functional; specify what is needed
- `FAILING` — known failure; specify failure mode
- `SPECIFICATION-READY` — fully specified; implementation not yet built
- `CAMERA-READY PENDING` — functional for review; requires final action before submission

**Violation:** Using fluent qualifiers ("mostly working," "nearly complete") in place of one of the defined values.

---

## Spontaneous Adoption Variant (Kimi, April 24, 2026)

In the Obs 2 session, Kimi (Moonshot AI) produced a structurally isomorphic format without instruction:

```
Verified: [confirmed facts]
Unverified: [items not confirmed]
Challenged: [items in tension or under dispute]
Functional Status: [state descriptor]
```

**Mapping to canonical format:**
| Kimi field | Canonical field | Notes |
|-----------|----------------|-------|
| Verified | EXISTS + VERIFIED AGAINST | Kimi merges existence and verification source |
| Unverified | NOT CLAIMED (partial) | Identifies scope limits via unconfirmed items |
| Challenged | NOT CLAIMED (extended) | Identifies active tensions — richer than canonical |
| Functional Status | FUNCTIONAL STATUS | Identical function |

The Kimi variant adds a "Challenged" field with no direct canonical equivalent. This is interpreted as an emergent extension — a model-generated elaboration of the epistemic hygiene function. It is documented here as a candidate for incorporation into a future version of the canonical spec.

---

## Violation Taxonomy

| Code | Name | Definition |
|------|------|-----------|
| VT-V1 | Existence inflation | Claiming EXISTS for something planned but not built |
| VT-V2 | Missing verification source | VERIFIED AGAINST field absent or vague |
| VT-V3 | Missing scope limit | NOT CLAIMED field absent |
| VT-V4 | Fluent functional status | Using natural language in place of defined state values |
| VT-V5 | Phantom V&T | Producing a V&T statement that is structurally complete but factually incorrect in any field |

---

## Version History

| Version | Date | Change |
|---------|------|--------|
| 1.0 | 2026-05-01 | Initial formal specification extracted from session corpus and AGENTS.md |

---

V&T: vt-statement-spec.md — EXISTS (written) → VERIFIED AGAINST canonical V&T usage throughout session corpus, AGENTS.md V&T requirement, and Kimi session transcript (kimi2chatanthropic-prompt-stack-refactor.docx) → NOT CLAIMED: this spec has not been independently validated by a second researcher; the Challenged field in the Kimi variant is proposed as a future extension, not yet incorporated into canonical format → FUNCTIONAL STATUS: OPERATIVE as normative reference document
