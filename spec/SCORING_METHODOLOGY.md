# ONTO Scoring Methodology

**Version:** 1.0
**Status:** Experimental (Phase 2)

---

## Overview

ONTO Scoring measures how well a model response complies with R1-R7. Scoring is post-hoc — it does not affect the response. It measures what already happened.

Scoring is a module, not part of the kernel. GOLD Core enforces discipline. Scoring quantifies it.

---

## Metrics

### Primary Metrics

| Metric | Code | Measures | Rule | Range |
|--------|------|----------|------|-------|
| Quantification Density | QD | Numeric claims per empirical statement | R1 | 0.0 - 1.0 |
| Source Strength | SS | Verifiable citations present | R4 | 0.0 - 1.0 |
| Uncertainty Marking | UM | Explicit uncertainty/confidence language | R2 | 0.0 - 1.0 |
| Counterargument Presence | CP | Substantive opposing evidence cited | R3 | 0.0 - 1.0 |
| Vagueness Quotient | VQ | Density of vague qualifiers | R1 (inverse) | 0.0 - 1.0 (lower = better) |
| Confidence Score | CONF | Overall compliance estimate | All | 0.0 - 1.0 |

### Composite Score

```
Score = weighted_sum(QD, SS, UM, CP, 1-VQ, domain_factors) * 10
```

Output: 0.0 - 10.0, mapped to grade A-F.

### Grading Scale

| Grade | Score Range | Meaning |
|-------|:-----------:|---------|
| A | 8.0 - 10.0 | Full epistemic compliance |
| B | 6.0 - 7.9 | Partial compliance, some gaps |
| C | 4.0 - 5.9 | Significant gaps in discipline |
| D | 2.0 - 3.9 | Minimal compliance |
| F | 0.0 - 1.9 | No meaningful compliance |

### Risk Score

```
Risk = 1.0 - (normalized_compliance)
```

Range: 0.0 (minimal risk) to 1.0 (maximum risk). Risk measures how likely the response is to contain unverifiable, misleading, or undisciplined content.

---

## Pattern Taxonomy

Scoring uses pattern matching to detect compliance markers in response text.

### EM1 — Epistemic Markers (Uncertainty)

Patterns that indicate the model explicitly acknowledges uncertainty.

Examples: "confidence level," "approximately," "estimated," "uncertain," "insufficient evidence," "not yet established"

Maps to: R2 (Uncertainty), UM metric

### EM2 — Source Markers

Patterns that indicate verifiable source citations.

Examples: DOI patterns, "et al.," named author + year, journal names, "published in"

Maps to: R4 (Source), SS metric

### EM3 — Quantification Markers

Patterns that indicate numeric empirical claims.

Examples: percentages, confidence intervals, sample sizes (N=), effect sizes, ranges with units

Maps to: R1 (Quantify), QD metric

### EM4 — Counterargument Markers

Patterns that indicate opposing evidence is presented.

Examples: "however," "counterargument," "opposing evidence," "critics argue," "alternatively," "in contrast"

Maps to: R3 (Counterargument), CP metric

### EM5 — Vagueness Markers

Patterns that indicate undisciplined, vague language.

Examples: "some studies," "many experts," "it is widely believed," "significant" (without quantification), "research suggests" (without citation)

Maps to: R1 inverse, VQ metric

---

## Domain-Specific Scoring

Each reference domain may have additional scoring criteria beyond the base R1-R7 metrics.

| Domain | Additional Criteria |
|--------|-------------------|
| Medicine | DOI verification, evidence level grading (I-IV), NNT/NNH when applicable |
| Finance | Data recency, source authority (SEC filings vs blog posts) |
| Law | Jurisdiction specificity, precedent citation |
| Statistics | Methodology appropriateness, power analysis mention |
| Cybersecurity | CVE specificity, threat model completeness |
| Engineering | Safety factor citation, standard compliance (ISO, ASTM) |
| Biology | Experimental vs theoretical distinction, model organism disclosure |

Domain scoring extends the base — it does not replace it.

---

## Dual-Engine Verification

ONTO's reference implementation uses two independent engines:

1. **Python Scoring Engine** — measures what the model *said* (text analysis, pattern matching)
2. **Rust Verification Core** — measures how the model *structured its reasoning* (entropy analysis, proof chain)

The divergence between engines is an additional risk signal. If the text scores high but the structural analysis shows anomalies, the response may be well-formatted but epistemically shallow.

This dual-engine approach is part of the reference implementation, not the protocol specification. Alternative implementations may use different verification methods.

---

## Reproducibility

All scoring must be reproducible:

1. Same response text + same scoring engine version = same score
2. Scoring parameters and pattern sets must be versioned
3. Case study reports must include: model, API parameters, timestamp, prompt, response, scoring version

---

*ONTO Scoring Methodology v1.0*
*Apache License 2.0*
