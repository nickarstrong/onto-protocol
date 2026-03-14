# ONTO Module Interface

**Version:** 1.0
**Status:** Experimental (Phase 2)

---

## Overview

ONTO OS is modular. The kernel (GOLD Core, R1-R7) is immutable and self-sufficient. Everything else is a pluggable module.

This document defines the interface that all ONTO-compatible modules must implement.

---

## Core Principle

**GOLD Core without modules = working system.**

The kernel enforces R1-R7 on every request. Modules extend the kernel's capabilities — routing, domain knowledge, scoring, verification, transport — but the kernel does not depend on any of them.

---

## Module Interface

Every ONTO module implements this interface:

```
Module:
    name        : string    # Unique identifier (e.g., "reference/medicine")
    category    : string    # One of: routing, reference, audit, security, transport, access, memory, language
    depends_on  : list      # Always includes "gold_core". May include other modules.
    tier_minimum: string    # Minimum client tier: OPEN | STANDARD | PROVIDER | WHITE_LABEL

    load(context) -> string
        # Called BEFORE model generation.
        # Returns content to inject into the prompt (or empty string).
        # Used by: routing, reference modules.

    process(response) -> dict
        # Called AFTER model generation.
        # Returns metadata extracted from the response (or empty dict).
        # Used by: audit, security modules.
```

### load(context)

Called before the host model generates a response. The return value is injected into the system prompt alongside GOLD Core.

**Input:** `context` — a dictionary containing at minimum:
- `message` (string): The user's message
- `tier` (string): Client tier
- `history` (list): Conversation history (if available)
- `domains` (list): Domains identified by the scheduler (if available)

**Output:** String content to inject, or empty string.

**Examples:**
- A reference module returns domain-specific theses and source citations
- A routing module returns nothing (it modifies context for downstream modules)
- An audit module returns nothing (it operates post-generation)

### process(response)

Called after the host model generates a response. Returns metadata about the response.

**Input:** `response` — a dictionary containing at minimum:
- `text` (string): The model's response text
- `model` (string): Host model identifier
- `context` (dict): Same context from load()

**Output:** Dictionary of metadata, or empty dict.

**Examples:**
- An audit module returns `{score: 9.2, grade: "A", risk: 0.03, gold_markers: {...}}`
- A security module returns `{proof_chain: "...", entropy: 0.87, merkle_root: "..."}`
- A reference module returns empty dict (it operates pre-generation)

---

## Module Categories

### routing
Determines which modules to load and how much context budget each receives.

| Module | Purpose | Phase |
|--------|---------|-------|
| Router | Keyword-based domain detection | load() returns domain list |
| Scheduler | Weighted classification + budget allocation | load() modifies context |

### reference
Domain-specific knowledge injected before generation.

| Module | Content |
|--------|---------|
| reference/medicine | Clinical methodology, evidence standards |
| reference/finance | Market evidence, financial reasoning |
| reference/law | Legal reasoning, jurisdiction frameworks |
| reference/statistics | Statistical methodology, significance standards |
| reference/cybersecurity | Security evidence, threat modeling |
| reference/engineering | Engineering methodology, safety standards |
| reference/biology | Biological evidence, research frameworks |

Each domain is independent. Loading one does not require others.

### audit
Post-generation measurement. Does NOT affect the response — measures it after generation.

| Module | Output |
|--------|--------|
| Scoring Engine | Score (0-10), grade (A-F), risk, compliance, gold_markers |

### security
Post-audit verification. Cryptographic proof of response integrity.

| Module | Output |
|--------|--------|
| Proof Chain | 104-byte proof, entropy analysis, Merkle root |

### transport
How the response reaches the client. Core is transport-agnostic.

| Module | Method |
|--------|--------|
| REST | JSON over HTTP |
| SSE | Server-Sent Events (streaming) |
| WebSocket | Bidirectional (future) |

### access
Tier-based permissions. Determines which modules a client can load.

### memory
Session and historical context.

| Module | Scope |
|--------|-------|
| Session | Within one conversation |
| Client history | Compliance trend per API key |

### language
Scoring pattern sets per language. Core R1-R7 are language-agnostic.

| Module | Patterns |
|--------|----------|
| language/en | 92 regex patterns |
| language/ru | Equivalent patterns (planned) |

---

## Loading Order

```
1. GOLD Core          (always, unconditional)
2. Access Control     (if present — validates tier)
3. Router             (if loaded — detects domains)
4. Scheduler          (if loaded — allocates budget)
5. Reference modules  (if selected by Router/Scheduler)
6. ── HOST MODEL CALL ──
7. Audit              (if loaded — scores response)
8. Security           (if loaded — signs proof)
9. Transport          (delivery method)
```

Core is step 1. Everything else wraps around it.

Modules at steps 1-5 use `load()`. Modules at steps 7-8 use `process()`.

---

## Adding a New Module

### New Reference Domain

1. Create `reference/{domain}/` with domain theses and source material
2. Add domain keywords to Router/Scheduler configuration
3. Register module with `tier_minimum`
4. Deploy. Core does not change.

### New Language

1. Create `language/{lang}/patterns.json` with scoring patterns
2. Register as Audit module extension
3. Core R1-R7 are language-agnostic — no Core change needed.

### New Transport

1. Implement transport interface (deliver response to client)
2. Register with `tier_minimum`
3. Core does not know or care how response is delivered.

### New Audit Capability

1. Extend scoring engine or create parallel scorer
2. Register as Audit module variant
3. Core does not change. Audit measures; Core enforces.

---

## Data Flow

### Minimal (Core only)

```
User message → GOLD Core (R1-R7) → Host Model → Response
```

### Full Stack (all modules)

```
User message
  → [Access Control] validate tier
  → [Router] detect domains
  → [Scheduler] allocate context budget
  → GOLD Core (R1-R7) — always, unconditional
  → [Reference modules] inject domain knowledge
  → Host Model generates response
  → [Audit] score and grade
  → [Security] proof chain
  → [Transport] deliver
```

---

*ONTO Module Interface Specification v1.0*
*Apache License 2.0*
