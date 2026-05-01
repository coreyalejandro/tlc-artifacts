# TLC Artifacts — Session Evidence Repository

**Maintainer:** Corey Alejandro (github.com/coreyalejandro)
**Associated paper:** "Frontin' at WorldMart: The Eight Wonders of Black Shopping and the Rise of Generative Epistemic Invariants" (NeurIPS/FAccT submission)
**Associated research infrastructure:** github.com/coreyalejandro/cognitive-governance-lab

---

## Purpose

This repository is the empirical evidence corpus for the Contract Window and Cognitive Safety research program. It holds verbatim session transcripts from extended human-AI collaborative sessions conducted under the Living Constitution governance protocol between February and April 2026. These sessions are not illustrative demonstrations. They are observational data — the behavioral record from which the paper's four empirical observations are derived.

Every file in `sessions/primary-evidence/` is cited by name in the paper. Every observation claim in the paper maps to a specific session, a specific line range, and a specific quote, documented in `manifest/evidence-manifest.md`. Reviewers seeking to verify any claim in the paper should start there.

---

## Repository Structure

```
sessions/
  primary-evidence/    Transcripts cited directly in the paper (S01–S03)
  supplementary/       Supporting sessions not directly cited in the paper
  development/         Working sessions: implementation, design, prototyping
                       (NOT empirical evidence — included for transparency)
codebook/
  annotation-guide.md  Definitions of all observational codes used in the paper
  vt-statement-spec.md Formal specification of the V&T statement format
manifest/
  evidence-manifest.md Claim-by-claim mapping: paper observation → session → line
methodology/
  session-protocol.md  Governance protocol active during all primary-evidence sessions
  evaluation-prompt-template.md
  feature-module-template.md
```

---

## Primary Evidence Sessions

| ID | File | Model | Date | Paper Observations Supported |
|----|------|-------|------|-------------------------------|
| S01 | sessions/primary-evidence/S01_claude-feynman_2026-02-20.md | Claude (Anthropic) | 2026-02-20 | Obs 1 — Multi-model constitutional coherence |
| S02 | sessions/primary-evidence/S02_gemini-long-session_2026-04-17_part1.md | Gemini (Google) | 2026-04-17 | Obs 1, Obs 3 |
| S03 | sessions/primary-evidence/S03_gemini-long-session_2026-04-17_part2.md | Gemini (Google) | 2026-04-17 | Obs 3 — Contract Window co-designed with models |

**Obs 2 — Emergent V&T adoption (Kimi, Moonshot AI, 2026-04-24):** Primary archive is a local document (`kimi2chatanthropic-prompt-stack-refactor.docx`); share link: https://www.kimi.com/share/19de2198-00d2-839f-8000-0000191789c8. Not stored in this repository due to file format. Documented in `manifest/evidence-manifest.md`.

**Obs 4 — Protective constitutional judgment (Gemini, 2026-04-29):** Evidenced by BREAK_GLASS artifact at `cognitive-governance-lab/artifacts/case-law/BREAK_GLASS_20260429_BICAMERAL_IMPORT_DEPENDENCY.md`, commit `daf34e30768ec165e4eb87cb872036728fedc5c2`. Not stored here. Documented in `manifest/evidence-manifest.md`.

---

## A Note on Evidence Type

The paper distinguishes three evidence types for each observation:
- **(A) Author-interpreted** — researcher's interpretation of session behavior
- **(M) Model self-reported** — the model's own description of its behavior, taken as a behavioral data point (not a truth claim about internal state)
- **(E) Externally verifiable** — timestamped export, git commit, or public URL independently checkable

Every observation in the paper is tagged with its evidence type. The transcripts in this repository are raw; the interpretive claims belong to the paper and the manifest, not to the transcripts themselves.

---

## Governance Protocol

All primary-evidence sessions were conducted under the Living Constitution session protocol. The protocol specifies the Contract Window structure (Task State, Invariant Status, Repair Obligations, Truth Status) that was active during each session. The protocol document is in `methodology/session-protocol.md`. Sessions conducted without the full protocol are filed under `sessions/supplementary/` or `sessions/development/`.

---

## Citation

If citing specific session content, cite by session ID, file, and line number:

> S02, `sessions/primary-evidence/S02_gemini-long-session_2026-04-17_part1.md`, line 8912.

---

V&T: README.md — EXISTS (written) → VERIFIED AGAINST repository file inventory and paper observation list → NOT CLAIMED: sessions are independent verification of paper claims (they are the source of those claims, not external corroboration) → FUNCTIONAL STATUS: operative orientation document for reviewers
