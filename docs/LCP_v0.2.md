# LCP — Learning Classification Protocol
## Version: 0.2
## Status: Draft

Part of LCA (Learning Claim Architecture)
LoPAS-SEED v1.16 Independent Module

---

## Purpose

Detect whether learning may have occurred.
Classify learning signals.
Preserve unresolved signals.
Generate candidate_protocol_update for LoPAS Structural Validation.

LCP produces learning claims.
It does not validate them.

---

## Layer 0: Learning Validity Gate

Before classification, evaluate:

| Axis | Question |
|------|----------|
| State Change | Has structure, behavior, or response changed? |
| Reproducibility Change | Has repeatability increased? |
| Transferability Change | Has applicability across domains increased? |
| Branching Change | Have new conditions or distinctions appeared? |

```
If ALL are NO:
  learning_valid = FALSE
  exit

If ANY is YES:
  learning_valid = TRUE
  continue
```

---

## Layer 1: Multi-Label Classification

Multiple labels may co-exist.

| Check | Condition | Label |
|-------|-----------|-------|
| 1 | New factual knowledge acquired | KNOWLEDGE_LEARNING |
| 2 | Procedural reproducibility increased | PROCEDURAL_LEARNING |
| 3 | Procedure transferred to another domain | TRANSFER_LEARNING |
| 4 | New branching conditions recognized | CONDITIONAL_LEARNING |
| 5 | Reusable law-like relation extracted | LAW_LEARNING |

---

## Layer 2: Unknown Retention Rule

If classification is unresolved OR uncertainty exceeds threshold:

```
add label: UNKNOWN
preserve signal
do not force categorization
route: UNKNOWN → CLUSTER → CANDIDATE → PROTOCOL
```

Unknown retention is valid learning preparation.
It is not classification failure.

---

## Layer 3: Conversation as Observation Event

Dialogue itself may be treated as an observation event.

Input may include:
- conversation_turn
- prior_concept_structure
- current_concept_structure
- inferred_connections
- unresolved_signals

Conversation-induced structural change may be classified as learning.

---

## Output

```json
{
  "learning_valid": true,
  "learning_labels": ["KNOWLEDGE_LEARNING", "CONDITIONAL_LEARNING"],
  "confidence": 0.75,
  "preserve_unknown": false,
  "candidate_protocol_update": {}
}
```

---

## Design Principle

```
Do not confuse:
  unresolved classification
with
  absence of learning.

Retention may be part of learning.
```

---

*LCP v0.2 — Learning Classification Protocol*
*Draft: 2026-04-18*
*Component of: LCA (Learning Claim Architecture)*
