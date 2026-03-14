# ONTO Protocol — Case Studies

All studies use controlled methodology: same model, same API parameters, with/without ONTO Protocol (R1-R7). Responses scored by the same engine version.

## Published Studies

### CS-2026-001: Expert Clinical Question (11 Models)
- **Question:** Expert-level clinical prompt with instructions to cite RCTs and DOIs
- **Models:** 11 (10 ranked, 1 excluded for conflict)
- **Key finding:** Composite M=0.92, SD=0.58. GOLD treatment produced 10x improvement. 5.4x variance across models.
- **Report:** [onto-standard/reports/CS-2026-001](https://github.com/nickarstrong/onto-standard/tree/main/docs/reports/CS-2026-001)

### CS-2026-002: GLP-1 Clinical Question (12 Models)
- **Question:** GLP-1 receptor agonists for weight management
- **Models:** 12 (10 ranked, 2 observed)
- **Key finding:** Mean=7.48. 0/10 models verified DOIs without ONTO. Treatment: +15% to +39% improvement.
- **Report:** [onto-standard/reports/CS-2026-002](https://github.com/nickarstrong/onto-standard/tree/main/docs/reports/CS-2026-002)

### CS-2026-003: Naive Fasting Question (Grok 4.2)
- **Question:** "Is fasting good for you?" — no special instructions
- **Key finding:** 8.6/A → 9.9/A (+15%). Without ONTO: zero DOIs, zero evidence grading. With ONTO: DOI-linked meta-analyses, confidence intervals, falsifiability conditions.
- **Report:** [onto-standard/reports/CS-2026-003](https://github.com/nickarstrong/onto-standard/tree/main/docs/reports/CS-2026-003)

### CS-2026-004: Naive Fasting Question (GPT)
- **Question:** "Is fasting good for you?" — no special instructions
- **Key finding:** 6.5/C → 9.9/A (+52%). Largest observed lift. Without ONTO: emoji, "bottom line" summary, zero citations. With ONTO: DOI-linked evidence, effect sizes, counterarguments.
- **Report:** [onto-standard/reports/CS-2026-004](https://github.com/nickarstrong/onto-standard/tree/main/docs/reports/CS-2026-004)

## Key Observations Across Studies

1. **Naive questions expose the gap.** Expert prompts produce similar scores with and without ONTO. The real difference appears when users ask simple, undirected questions.

2. **Cheaper models + ONTO beat expensive models without it.** DeepSeek + ONTO (8.9) > Grok raw (8.6). The layer matters more than the model price.

3. **Zero DOI verification is the norm.** Without ONTO, 0/10 models in CS-2026-002 produced verified DOIs. This is the baseline the industry operates at.

4. **The lift is consistent.** +12% to +52% across different models and questions. The protocol works regardless of the host model.

## Submitting a Study

See [TEMPLATE.md](TEMPLATE.md) for the required format. Submit via PR with full methodology and raw data.

---

*ONTO Protocol Case Studies*
*Apache License 2.0*
