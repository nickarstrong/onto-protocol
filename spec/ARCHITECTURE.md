# ONTO OS Architecture

**Version:** 1.0
**Status:** Experimental (Phase 2)

---

## Design

```
┌─────────────────────────────────────────────────┐
│                                                 │
│              G O L D   C O R E                  │
│                                                 │
│   R1 Quantify    R2 Uncertainty   R3 Counter    │
│   R4 Source      R5 Evidence      R6 Falsify    │
│   R7 Scope                                      │
│                                                 │
│   Immutable. Self-sufficient. Every request.    │
│                                                 │
├─────────────────────────────────────────────────┤
│                                                 │
│              M O D U L E S                      │
│         (all optional, all pluggable)           │
│                                                 │
│  Routing    │  Reference Domains  │  Audit      │
│  Security   │  Transport          │  Access     │
│  Memory     │  Language                         │
│                                                 │
├─────────────────────────────────────────────────┤
│                                                 │
│              H O S T   M O D E L                │
│       Any LLM. Replaceable. Model-agnostic.     │
│                                                 │
└─────────────────────────────────────────────────┘
```

## Three Layers

**GOLD Core = Kernel.** Immutable behavioral law. R1-R7 on every request. Self-sufficient — works without any modules.

**Modules = Userland.** Optional, pluggable, independently deployable. Any combination works. None required. See [MODULE_INTERFACE.md](MODULE_INTERFACE.md).

**Host Model = Hardware.** Any LLM. Replaceable. ONTO OS runs on all of them. The model is a resource, not a dependency.

## Data Flow

### Minimal (kernel only)

```
User message → GOLD Core (R1-R7) → Any LLM → Disciplined response
```

### Full (all modules loaded)

```
User message
  → Access Control (validate tier)
  → Router (detect domains)
  → Scheduler (allocate context budget)
  → GOLD Core (R1-R7) — always
  → Reference modules (domain knowledge)
  → Host Model (generate)
  → Audit (score, grade)
  → Security (proof chain)
  → Transport (deliver)
```

## Design Principles

**P1. Core is immutable.** R1-R7 never change at runtime. They are law.

**P2. Everything else is a module.** The OS works without any of them.

**P3. Model-agnostic.** Any LLM is a valid host.

**P4. Discipline over capability.** ONTO does not make models smarter. It makes them disciplined. DeepSeek + ONTO (8.9) beats Grok raw (8.6). Same weights.

**P5. Measure everything.** Every response can be scored and proof-signed — if the Audit and Security modules are loaded.

## Analogy

ONTO OS is to AI what POSIX is to operating systems.

POSIX defines what a compliant OS must do. It doesn't implement the OS — Linux, macOS, and Solaris each implement it differently. But any POSIX-compliant program runs on any POSIX-compliant OS.

ONTO Protocol defines what a disciplined AI response must contain. It doesn't implement the discipline — any system that enforces R1-R7 is a valid implementation. But any ONTO-compliant response is verifiable, falsifiable, and honest about its limitations.

---

*ONTO OS Architecture v1.0*
*Apache License 2.0*
