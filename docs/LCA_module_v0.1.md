# LCA — Learning Claim Architecture
## LoPAS-SEED v1.16 Independent Module
## Version: 0.1
## Status: Draft

---

## Position in LoPAS Architecture

```
Layer 0  Data / Observation
Layer 1  DoQ / CCI / TRS / SCI / BCDI
Layer 2  CHD / CGM / HGD
Layer 3  LCA  ← THIS MODULE
           System A: LCP (Learning Classification Protocol)
           System B: LoPAS Structural Validation
           Coupling Logic
           Validation Failure Handling
           Feedback Spiral
Layer 4  Protocol Refinement / Intervention
```

LCA is external to LoPAS core.
LoPAS validates LCA outputs.
LCA does not modify LoPAS indicators directly.

---

## Purpose

LCA separates two functions that must not be conflated:

1. Learning Classification — detecting whether learning may have occurred
2. Structural Validation — testing whether claimed learning produced observable change

Conflating these produces approval systems, not control systems.

---

## Design Origin

LCA emerged from the observation that:

- automated pipelines can detect structural change (LoPAS)
- but learning signals precede structural change
- and unresolved signals may be valid precursors, not failures

The architecture formalizes the gap between claim and validation
as a productive control surface.

---

## System A: Learning Classification Protocol (LCP)

### Purpose
Detect whether learning may have occurred.

### Layer 0: Learning Validity Gate

Before classification, evaluate:

| Axis | Question |
|------|----------|
| State Change | Has structure, behavior, or response changed? |
| Reproducibility Change | Has repeatability increased? |
| Transferability Change | Has applicability across domains increased? |
| Branching Change | Have new conditions or distinctions appeared? |

If ALL are NO:
```
learning_valid = FALSE
exit
```

If ANY is YES:
```
learning_valid = TRUE
continue
```

### Layer 1: Multi-Label Classification

Multiple labels may co-exist.

| Check | Condition | Label |
|-------|-----------|-------|
| 1 | New factual knowledge acquired | KNOWLEDGE_LEARNING |
| 2 | Procedural reproducibility increased | PROCEDURAL_LEARNING |
| 3 | Procedure transferred to another domain | TRANSFER_LEARNING |
| 4 | New branching conditions recognized | CONDITIONAL_LEARNING |
| 5 | Reusable law-like relation extracted | LAW_LEARNING |

### Layer 2: Unknown Retention Rule

If classification is unresolved OR uncertainty exceeds threshold:

```
add label: UNKNOWN
preserve signal
do not force categorization
route: UNKNOWN → CLUSTER → CANDIDATE → PROTOCOL
```

Unknown retention is valid learning preparation.
It is not classification failure.

### Layer 3: Conversation as Observation Event

Dialogue itself may be treated as an observation event.

Input may include:
- conversation_turn
- prior_concept_structure
- current_concept_structure
- inferred_connections
- unresolved_signals

Conversation-induced structural change may be classified as learning.

### LCP Output

```json
{
  "learning_valid": true,
  "learning_labels": [],
  "confidence": 0.0,
  "preserve_unknown": true,
  "candidate_protocol_update": {}
}
```

LCP produces learning claims.
It does not validate them.

---

## System B: LoPAS Structural Validation

### Purpose
Test whether claimed learning produced observable structural change.

### Validation Indicators

| Indicator | Question |
|-----------|----------|
| CCI | Did cognitive connectivity increase? |
| TRS | Did resonance or meaning depth change? |
| BCDI | Did branching cognition increase? |
| SCI | Did structural rigidity reduce? |
| Phase | Was an observable phase shift detected? |

### Validation Output

```json
{
  "learning_validated": "TRUE/FALSE",
  "structural_change_detected": {},
  "validation_confidence": 0.0
}
```

LoPAS validates claims.
It does not generate them.

---

## Coupling Logic

```
LCP output:
  candidate_protocol_update

→ becomes →

LoPAS input:
  structural validation trigger
```

LCP and LoPAS share no internal state.
They communicate only through candidate_protocol_update.

---

## Validation Failure Handling

If validation = FALSE, route to one of:

### Route A: Return to LCP Reclassification
When uncertainty is high and the signal retains structure.
Learning may have occurred but was misclassified.

### Route B: Return to Unknown Retention
When structural contradiction is moderate.
Signal is preserved for future cycle.
Unknown Retention feeds the next observation.

### Route C: Reject candidate_protocol_update
When contradiction severity is high and retention priority is low.
Signal is discarded. Observation continues.

### Selection Criteria

| Factor | Influences Route |
|--------|-----------------|
| uncertainty_threshold | high → A or B |
| contradiction_severity | high → C |
| retention_priority | high → B |

### Design Rule

```
Validation failure ≠ absence of learning.
Validation failure may = unresolved structure.
Unresolved structure feeds Learning Spiral dynamics.
```

---

## Feedback Spiral

```
Observation
→ LCP
→ candidate_protocol_update
→ LoPAS Validation

if TRUE:
  → Protocol Refinement
  → Observation

if FALSE:
  → Route A / B / C
  → Observation
```

Repeated retention + refinement
generates Learning Spiral dynamics.

This spiral is the mechanism by which
Unknown Retention produces structural ascent
rather than accumulation without direction.

---

## Relationship to CHD

LCA is architecturally compatible with LoPAS-CHD-Protocol.

CHD treats hallucination as:
```
inevitable cognitive hazard
→ control, not elimination
```

LCA treats learning claims as:
```
inevitable cognitive assertions
→ validate, not approve by default
```

The structural parallel:

| CHD Layer | LCA Equivalent |
|-----------|----------------|
| Detection Layer | LCP (signal detection) |
| Containment Layer | LoPAS Validation |
| Redesign Layer | FALSE → Unknown Retention |

LCA may be deployed as an extension of CHD
for learning claim discrimination.

---

## Relation to LoPAS Core Dynamics

LoPAS measures structural change through indicator oscillation.
LCA provides the mechanism that generates that oscillation.

The core dynamic:

```
Fixed state = cognitive death
Oscillation = cognitive life
```

LCA's Unknown Retention maintains oscillation
by preventing premature closure of unresolved signals.

This is the same principle expressed in:
- TRS × SCI anti-correlation
- CGM ΔG oscillation
- CHD Redesign Layer

LCA makes this principle explicit as a control architecture.

---

## Design Principles

```
Do not confuse:
  learning classification
with
  learning validation.
Both are necessary.

Do not confuse:
  validation failure
with
  absence of learning.
Unresolved structure may remain valid.

Do not confuse:
  Unknown Retention
with
  classification failure.
Retention is learning preparation.
```

---

## Integration Notes for v1.16

- LCA is positioned at Layer 3, above CHD/CGM/HGD
- LCA does not modify core indicators (DoQ, CCI, TRS, SCI, BCDI) directly
- LCA outputs feed Protocol Refinement at Layer 4
- LCA's candidate_protocol_update format should be aligned with existing LoPAS protocol update schema
- FALSE handling routes (A/B/C) should be logged for Learning Spiral analysis

---

*LCA v0.1 — LoPAS-SEED Independent Module*
*Draft: 2026-04-18*
*Derived from: LCP v0.2, Dual Architecture Draft v0.2*
*Compatible with: LoPAS-SEED v1.15, LoPAS-CHD-Protocol*
