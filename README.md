# ONTO Protocol

**An open epistemic discipline standard for AI inference.**

ONTO Protocol defines a set of epistemic rules (R1-R7) that transform AI model behavior at inference time — without retraining, fine-tuning, or restricting capabilities.

The protocol makes AI models stronger, not weaker.

---

## The Problem

Every major AI model defaults to confident-sounding filler when users ask naive questions. No citations. No confidence intervals. No counterarguments. No evidence grading.

The industry response: more guardrails, more restrictions, more "I can't help with that." Models become safer on paper and less useful in practice.

ONTO Protocol offers an alternative: **epistemic discipline at inference time.**

## Results

Same models. Same weights. Same API. One behavioral layer.

| Model | Without ONTO | With ONTO | Change |
|-------|:-----------:|:---------:|:------:|
| GPT | 6.5 / C | 9.9 / A | +52% |
| DeepSeek | 7.3 / B | 8.9 / A | +22% |
| Grok | 8.6 / A | 9.6 / A | +12% |

DeepSeek + ONTO (8.9) outperforms Grok without it (8.6). A cheaper model with discipline beats an expensive model without it.

Zero retraining. Zero fine-tuning. Inference-time only.

## Documentation

- [R1-R7 Specification](spec/R1-R7.md) — The seven epistemic rules
- [Module Interface](spec/MODULE_INTERFACE.md) — How to build ONTO-compatible modules
- [Scoring Methodology](spec/SCORING_METHODOLOGY.md) — How to measure epistemic compliance
- [Architecture](spec/ARCHITECTURE.md) — ONTO OS design blueprint
- [Case Studies](studies/) — Controlled experiments with public data

## Quick Start

ONTO Protocol defines **what** a disciplined AI response must contain. Any implementation is valid if it enforces R1-R7.

The simplest implementation: inject R1-R7 rules into the system prompt of any LLM. The model cannot respond without addressing them.

```
User question → R1-R7 rules (system prompt) → Any LLM → Disciplined response
```

No SDK required. No vendor lock-in. Works with any model.

## Reference Implementation

[ONTO Standard](https://ontostandard.org) provides a commercial reference implementation with:

- 7 research domains (medicine, finance, law, statistics, cybersecurity, engineering, biology)
- 149 reference files, 411K tokens of verified source material
- Dual-engine verification (Python scoring + Rust cryptographic proof)
- Multi-provider support (Anthropic, OpenAI, DeepSeek, xAI, Mistral)
- REST API and streaming SSE

[Try the live demo →](https://ontostandard.org/agent/)

## Philosophy

> "ONTO doesn't limit AI. It liberates it."

Everyone else builds cages for AI — guardrails, safety frameworks, restrictions. The result: AI does less.

ONTO builds a spine — epistemic discipline. The result: AI does more, and does it better.

R1-R7 are not restrictions. They are what a good scientist learns in 10 years of university: quantify, doubt, cite, admit you could be wrong. This is not a prison. It is education.

A model under ONTO Protocol is not weaker. It works at full capacity for the first time.

## Contributing

ONTO Protocol is an open specification. We welcome:

- New reference domain implementations
- Language-specific scoring patterns
- Independent case studies and reproductions
- Integration guides for specific LLM providers

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Case Studies

| ID | Question | Models | Key Finding |
|----|----------|--------|-------------|
| CS-2026-001 | Expert clinical | 11 models | Composite M=0.92, SD=0.58; GOLD treatment 10x improvement |
| CS-2026-002 | GLP-1 clinical | 12 models | Mean=7.48; 0/10 DOI verified without ONTO |
| CS-2026-003 | Naive fasting (Grok) | 1 model | 8.6 → 9.9 (+15%) |
| CS-2026-004 | Naive fasting (GPT) | 1 model | 6.5 → 9.9 (+52%) |

All studies use controlled methodology: same model, same API parameters, with/without ONTO Protocol. Full reports available in [studies/](studies/).

## License

ONTO Protocol specification is licensed under [Apache License 2.0](LICENSE).

The specification is open. Build your own implementation. Or use the [reference implementation](https://ontostandard.org).

---

*ONTO Protocol — epistemic discipline standard for AI systems.*
*Safety through discipline, not restriction.*
