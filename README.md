# LCA — Learning Claim Architecture

**LoPAS-SEED v1.16 Independent Module**
Status: Draft v0.1 | 2026-04-18

---

## What is LCA

LCA is a control architecture that separates two functions that must not be conflated:

1. **Learning Classification** — detecting whether learning may have occurred
2. **Structural Validation** — testing whether claimed learning produced observable structural change

Conflating these produces approval systems, not control systems.

---

## Position in LoPAS Architecture

```
Layer 0  Data / Observation
Layer 1  DoQ / CCI / TRS / SCI / BCDI
Layer 2  CHD / CGM / HGD
Layer 3  LCA  ← THIS MODULE
Layer 4  Protocol Refinement / Intervention
```

LCA is external to LoPAS core.
LoPAS validates LCA outputs.
LCA does not modify LoPAS indicators directly.

---

## Two Systems

### System A: LCP (Learning Classification Protocol)

Detects whether learning may have occurred.
Produces learning claims.
Does not validate them.

```
Output:
{
  learning_valid,
  learning_labels[],
  confidence,
  preserve_unknown,
  candidate_protocol_update
}
```

### System B: LoPAS Structural Validation

Tests whether claimed learning produced observable structural change.
Validates claims.
Does not generate them.

```
Output:
{
  learning_validated: TRUE/FALSE,
  structural_change_detected,
  validation_confidence
}
```

---

## Feedback Spiral

```
Observation
→ LCP
→ candidate_protocol_update
→ LoPAS Validation

if TRUE:
  → Protocol Refinement → Observation

if FALSE:
  → Reclassification / Retention / Rejection → Observation
```

Repeated retention + refinement generates Learning Spiral dynamics.

---

## Validation Failure Handling

FALSE does not mean absence of learning.
It may mean unresolved structure.

| Route | Condition |
|-------|-----------|
| A: Return to LCP | uncertainty high, signal retains structure |
| B: Return to Unknown Retention | contradiction moderate |
| C: Reject | contradiction severe, retention priority low |

---

## Relationship to CHD

LCA is architecturally compatible with [LoPAS-CHD-Protocol](https://github.com/hanabokur0/LoPAS-CHD-Protocol).

| CHD Layer | LCA Equivalent |
|-----------|----------------|
| Detection Layer | LCP |
| Containment Layer | LoPAS Validation |
| Redesign Layer | FALSE → Unknown Retention |

LCA extends CHD from hallucination control to learning claim discrimination.

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

## Files

```
README.md                          — this file
docs/
  LCA_module_v0.1.md               — full specification
  LCP_v0.2.md                      — Learning Classification Protocol
  Dual_Architecture_v0.2.md        — coupling logic and feedback spiral
```

---

## Compatibility

- LoPAS-SEED v1.15+
- LoPAS-CHD-Protocol
- Derived from: LCP v0.2, Dual Architecture Draft v0.2

---

## Author

花黒子 (Hanabokur0)
Part of the LoPAS Civilization OS initiative.

## License

MIT

