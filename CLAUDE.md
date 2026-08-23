# CLAUDE.md — LoPAS-LCA

Loaded automatically by Claude Code at session start. Status: **Draft v0.1**, small repo (README + 3 docs). LoPAS-SEED v1.16 independent module — this predates the v1.19 registry consolidation (DoQ-S/-R split, SCI-S rename, AHI 3-way split). If cross-referencing SEED indicators from here, check the Master Indicator Registry first rather than assuming this doc's terminology is current.

## One-line summary

LCA (Learning Claim Architecture) separates two functions that must not be conflated: **detecting whether learning may have occurred** (Learning Classification) vs. **testing whether claimed learning produced observable structural change** (Structural Validation). Conflating them produces an approval system, not a control system.

## Position in the wider LoPAS architecture

```
Layer 0  Data / Observation
Layer 1  DoQ / CCI / TRS / SCI / BCDI        (LoPAS-SEED core indicators)
Layer 2  CHD / CGM / HGD
Layer 3  LCA  ← this repo
Layer 4  Protocol Refinement / Intervention
```

LCA is external to LoPAS core. LoPAS validates LCA's outputs; LCA does not modify LoPAS indicators directly.

## Directory map

| Path | Role |
|---|---|
| `README.md` | This overview |
| `docs/LCA_module_v0.1.md` | Full specification |
| `docs/LCP_v0.2.md` | Learning Classification Protocol (System A) detail |
| `docs/Dual_Architecture_v0.2.md` | Coupling logic and feedback spiral detail |

## The two systems (do not merge their outputs)

**System A — LCP (generates claims, does not validate them):**
```yaml
output: {learning_valid, learning_labels[], confidence, preserve_unknown, candidate_protocol_update}
```

**System B — LoPAS Structural Validation (validates claims, does not generate them):**
```yaml
output: {learning_validated: TRUE/FALSE, structural_change_detected, validation_confidence}
```

## Hard rules

- **FALSE ≠ absence of learning.** A validation failure may mean unresolved structure, not "nothing happened." Route accordingly (see below), never collapse FALSE to "no learning occurred."
- **Validation failure routing is conditional, not automatic rejection:**
  | Route | Condition |
  |---|---|
  | A: Return to LCP | uncertainty high, signal retains structure |
  | B: Return to Unknown Retention | contradiction moderate |
  | C: Reject | contradiction severe, retention priority low |
- **Unknown Retention ≠ classification failure.** Retention is learning *preparation*, not a dead end — don't treat a `preserve_unknown` state as an error to be cleared away.
- **Do not let LCP self-validate.** Classification (System A) and Validation (System B) must stay institutionally separate even inside a single session's reasoning — don't let a claim confirm itself.

## Relationship to CHD

| CHD Layer | LCA Equivalent |
|---|---|
| Detection Layer | LCP |
| Containment Layer | LoPAS Validation |
| Redesign Layer | FALSE → Unknown Retention |

LCA extends CHD from hallucination control to learning-claim discrimination specifically.

## Quick task recipes

**"Did the system actually learn from this?"** → run LCP first for a claim (with `confidence` and `preserve_unknown` if warranted), then run Structural Validation independently against observable structural change. Report both outputs separately — never report only the LCP claim as if it were validated.

**"The claim failed validation, what now?"** → check contradiction severity and uncertainty level, then route via A/B/C above. Don't default to Reject; that's only for severe contradiction + low retention priority.

## Relationship to other repos in this ecosystem

Part of a wider set: `information-compost`, `lopas-protocol-foundry`, `classification-simulation-pack`, `LoPAS-Open-Translator-Core`, `Verifiable-Capability-Exchange`. Also compatible with `LoPAS-CHD-Protocol` (separate repo, not yet given its own CLAUDE.md). If a task needs the CHD repo directly, say so rather than assuming it's available here.
