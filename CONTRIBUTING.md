# Contributing to ONTO Protocol

ONTO Protocol is an open specification. We welcome contributions that strengthen epistemic discipline in AI systems.

## What We Accept

**New Reference Domains**
If you have domain expertise and can define evidence standards, theses, and verified sources for a new domain (e.g., climate science, psychology, education), submit a proposal as an issue.

**Language-Specific Scoring Patterns**
The scoring engine uses regex patterns to detect R1-R7 compliance markers. Currently EN-only. Contributions for other languages are welcome. See `spec/SCORING_METHODOLOGY.md` for pattern taxonomy (EM1-EM5).

**Independent Case Studies**
Run your own controlled experiment: same model, same API, with/without R1-R7 enforcement. Report the results. We will review methodology and include valid studies in the `studies/` directory.

Requirements for case studies:
- Controlled methodology (with/without, same model, same parameters)
- Full prompt and response text preserved
- Scoring version noted
- Model version and API parameters documented
- Timestamp recorded

**Integration Guides**
How to implement R1-R7 with specific providers (OpenAI, Anthropic, Google, etc.) or frameworks (LangChain, LlamaIndex, etc.).

**Bug Reports and Spec Clarifications**
If R1-R7 are ambiguous or contradictory in a specific case, file an issue with a concrete example.

## What We Don't Accept

- Changes to R1-R7 core rules (these are immutable in the current version)
- Prompt templates that "game" the scoring without genuine epistemic compliance
- Marketing materials or promotional content
- Contributions that restrict AI capabilities rather than disciplining them

## Process

1. Open an issue describing what you want to contribute
2. Discussion and feedback
3. Submit a PR if approved
4. Review and merge

## Code of Conduct

Be factual. Cite your sources. State your uncertainty. Follow R1-R7 in your communications, not just in your code.

---

*ONTO Protocol*
*Apache License 2.0*
