# Dual Architecture for Learning Classification and Structural Validation
## Version: 0.2
## Status: Draft

Part of LCA (Learning Claim Architecture)
LoPAS-SEED v1.16 Independent Module

---

## Overview

This architecture separates:

1. Learning Classification
2. Structural Validation

into two coupled systems under CHD.

---

## System A: LCP (Learning Classification Protocol)

Purpose: Detect whether learning may have occurred.

Functions:
- classify learning signals
- preserve unresolved signals
- generate candidate_protocol_update

Output:
```json
{
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

Purpose: Test whether claimed learning produced observable structural change.

Validation indicators:
- CCI increased?
- TRS changed?
- BCDI increased?
- rigidity reduced?
- phase shift detected?

Output:
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

## Coupling

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

**Route A: Return to LCP Reclassification**
When uncertainty is high and the signal retains structure.

**Route B: Return to Unknown Retention**
When structural contradiction is moderate.
Signal preserved for future cycle.

**Route C: Reject candidate_protocol_update**
When contradiction severity is high and retention priority is low.

Selection criteria:

| Factor | Influences Route |
|--------|-----------------|
| uncertainty_threshold high | → A or B |
| contradiction_severity high | → C |
| retention_priority high | → B |

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
```

---

*Dual Architecture v0.2*
*Draft: 2026-04-18*
*Component of: LCA (Learning Claim Architecture)*
