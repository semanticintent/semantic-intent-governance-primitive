# Semantic Intent as Governance Primitive for Agentic Systems

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Status: Working Draft](https://img.shields.io/badge/Status-Working%20Draft-orange.svg)]()

**Author:** Michael Shatny  
**ORCID:** [0009-0006-2011-3258](https://orcid.org/0009-0006-2011-3258)  
**Version:** 0.1 (working draft — not yet peer-reviewed)  
**Date:** May 2026  
**Extends:** [Semantic Intent as Single Source of Truth](https://doi.org/10.5281/zenodo.17114972) (Shatny, 2025)

---

## Abstract

**Background:** Shatny (2025) established Semantic Intent as Single Source of Truth (SSOT) — a unified pattern combining semantic anchoring (WHAT) and intent mapping (WHY) into an immutable governance contract for AI-assisted development. That work addressed a two-party problem: one developer, one AI assistant, one codebase.

**Problem:** As AI systems evolve from coding assistants to autonomous agents operating in multi-agent pipelines, the governance problem changes in kind, not just in scale. Multiple agents — each stateless, each operating without memory of prior sessions — must coordinate without a human mediating every decision. The question is no longer how a developer keeps an AI anchored. It is how agents keep each other anchored.

**Contribution:** This paper extends the Semantic Intent SSOT thesis to multi-agent systems, proposing Semantic Intent as a *governance primitive* — a cross-agent contract with three required properties: immutability, addressability, and provenance. A working ecosystem of five independently developed tools (Rune Protocol, Wake Intelligence, RECALL, Mere, EMBER) provides convergent empirical evidence that this primitive emerges naturally from practice. Two consequences are examined: authorship attribution as a runtime governance dimension, and generative UI as a derived artifact of a stable semantic contract.

**Keywords:** semantic intent, agentic systems, governance primitive, multi-agent coordination, authorship attribution, generative UI, temporal memory, reactive binding

---

## 1. Introduction

In September 2025, the problem driving the original SSOT paper was concrete: an enterprise reporting system where executive briefs and full reports generated identical PDF output despite different content types. Weeks of debugging had failed. The root cause was a semantic violation — the analysis domain was overriding the document type domain — and the fix was to unify WHAT and WHY into an atomic semantic contract, protected by immutable governance [1].

The lesson was generalizable: when AI assists with code generation, refactoring, or architectural decisions, the primary failure mode is not incorrect logic. It is *semantic drift* — the gradual divergence between what a developer intended and what successive AI-assisted transformations produce. The SSOT pattern provided a structural answer: declare intent explicitly, co-locate it with the artifact it governs, make it immutable, and AI has something stable to read rather than something ambiguous to reconstruct.

Eight months later, the problem has evolved.

AI is no longer positioned primarily as a coding assistant responding to prompts. Production systems now deploy AI agents that generate artifacts, evaluate outputs, trigger downstream actions, and pass context to other agents — without a human in the loop at each step. The two-party model (developer + assistant) is being replaced by pipeline models where an orchestrating agent delegates to specialist agents, each of which may produce artifacts that feed the next.

In this architecture, the SSOT pattern remains necessary but is no longer sufficient. An individual agent reading a well-annotated codebase can reconstruct intent from structural declarations. But when Agent B receives a context package from Agent A, it has no memory of why Agent A made the decisions it made. It cannot distinguish a governance constraint from an optimisation preference. It cannot know whether a prior decision was made by a human, an upstream agent, or a machine-generated pipeline step.

Semantic drift in the multi-agent case is not a code-level problem. It is a coordination problem. The governance contract must operate at the layer where agents communicate, not just at the layer where humans write code.

---

## 2. The Agentic Shift

### 2.1 From Tool to Agent

The distinction between an AI tool and an AI agent is structural. A tool responds to a prompt and produces output. An agent maintains goals, takes sequences of actions, evaluates intermediate results, and coordinates with other agents to achieve outcomes that neither could achieve alone.

In the tool model, governance is a human responsibility — semantic drift is caught in review. In the agent model, governance cannot wait for human review at every step. By the time a human reviews the final output, many intermediate decisions have already been made, compounded, and rendered difficult to trace. This shifts the governance problem from *evaluation* to *contract enforcement*.

### 2.2 The Multi-Agent Coordination Problem

Consider a representative pipeline: an orchestrating agent delegates a code analysis task to a specialist agent, which produces a structured finding. A second specialist agent generates a migration plan from that finding. A third executes the first step and logs the result. A fourth prepares a human-readable summary.

At each handoff, context is passed but reasoning is lost. Agent 2 knows what Agent 1 found — it does not know why Agent 1 prioritised that finding, what constraints it was operating under, or whether the finding is a hard requirement or a suggestion. A misreconstruction at step 2 propagates through steps 3 and 4 as if it were ground truth.

### 2.3 What the Problem Requires

A solution to multi-agent semantic drift must satisfy three requirements:

1. **Survive handoffs** — Intent declared at step 1 must be structurally readable at step 4 without loss or reinterpretation.
2. **Machine-readable, not prose** — Agents do not read README files. The contract must be in a form agents can query, not summarise.
3. **Carry provenance** — An agent receiving context must determine what was decided by a human, an upstream agent, or a pipeline compositor — because these have different governance standing.

---

## 3. Semantic Intent as Governance Primitive

### 3.1 Definition

A governance primitive is a structural unit — below the level of a pattern or framework — that can be composed to build governance systems, referenced by any layer of a stack, and relied upon as a stable contract.

In the context of multi-agent systems, Semantic Intent as a governance primitive is defined as:

> **An immutable, machine-addressable declaration of intent, co-located with the artifact it governs, carrying the provenance of its origin.**

Three properties are required:

**Immutability.** The declared intent does not change when passed through agents or transformation layers. If modification is necessary, a new node is created with a causal reference to the original — preserving the chain rather than overwriting it.

**Addressability.** The intent is structurally accessible — not inferred from naming conventions or prose comments, but readable directly from a machine-queryable field. An agent that needs to know why a constraint exists should be able to query for it, not reconstruct it.

**Provenance.** The intent carries its origin: who declared it (human, AI agent, or AI compositor), when, and what caused it. This is a governance dimension — an agent making decisions downstream must be able to determine the standing of prior decisions, not just their content.

### 3.2 Relationship to the SSOT Pattern

The SSOT pattern [1] addressed immutability at the code level. The governance primitive extends this in two directions.

First, it adds addressability as an explicit requirement. In the code-level pattern, intent was co-located with the code construct. In the multi-agent case, intent must be queryable across systems — by agents with no access to the original codebase, at different times, in different contexts.

Second, it adds provenance as a first-class property. The SSOT pattern did not distinguish who declared an intent — the developer was the implicit single author. In multi-agent systems, authorship is a governance question: a constraint approved by a human risk committee has different standing than an optimisation inferred by an agent.

---

## 4. Empirical Evidence: An Ecosystem in Convergence

The strongest argument for Semantic Intent as a governance primitive is not theoretical. It is the observation that five independent tools — built for different purposes, by the same author, across eight months — all converged on the same structural answer to the same underlying question.

None were designed as a system. Each solved an immediate problem. The convergence was discovered retrospectively, and it is the convergence itself that constitutes the evidence.

### 4.1 Rune Protocol: The Binding-Level Primitive

Rune Protocol [2] is a reactive binding grammar expressed through four sigils: `@` (read), `~` (sync), `!` (act), `?` (intent). The `?` sigil is the governance primitive at the binding level — co-located with the binding it governs, versioned in the same commit, runtime-queryable by binding ID.

```json
{
  "bindings": [
    {
      "id": "risk-threshold",
      "sigil": "~",
      "intent": "Approved by risk committee Q1-2025. Floor of 0.10 non-negotiable — below that, position sizing model breaks.",
      "metadata": { "author": "human", "approved": "2025-03-14" }
    }
  ]
}
```

A `rune.schema.json` is a machine-readable governance contract: immutable (versioned), addressable (queryable by ID), carrying provenance (`metadata.author`).

### 4.2 Wake Intelligence: Temporal Governance

Wake Intelligence [3] is a five-layer temporal intelligence MCP server that preserves the causal history of decisions across sessions — solving the *temporal gap*: the space between a decision made in one session and an agent beginning a new session with no memory of it.

| Layer | Dimension | Function |
|---|---|---|
| 1 — Causality Engine | Past — WHY | Every context records what caused it. Causal chains are traversable backward from any point. |
| 2 — Memory Manager | Present — HOW | Tier classification (ACTIVE / RECENT / ARCHIVED / EXPIRED). Relevance is a function of time. |
| 3 — Propagation Engine | Future — WHAT | Prediction scoring from temporal decay, causal position, and access frequency. |
| 4 — Meta-Learning | Adaptive — HOW WELL | Per-project weight tuning. Weights learn from access outcomes. |
| 5 — Personality Modes | Presentation — HOW FRAMED | Temporal posture at retrieval: historian, prophet, archaeologist, minimalist, auditor. |

Wake v3.5.0 introduced `ingest_rune_manifest` — a tool that ingests a `rune.schema.json` and saves every `?` annotation as a Wake causal context. Governance declared in Rune becomes temporal memory in Wake: the binding ID is the node identifier, the `?` intent annotation is the causal rationale.

### 4.3 RECALL: Authorship as Compile-Time Constraint

RECALL [4] is a COBOL-inspired publishing language for structured artifacts. Its governance contribution is `CREATED-BY`: an enum field accepting exactly three values (`Human`, `AI compositor`, `AI agent`). A RECALL document that does not declare authorship does not compile — authorship is enforced structurally at creation, not tagged after the fact.

### 4.4 Mere: Reactive Governance at the UI Layer

Mere [5] is a workbook format using the same four Rune sigils, predating their formalisation as Rune Protocol. Mere is the origin point: the sigils were discovered in Mere, extracted as Rune Protocol, and formalised as a governance primitive. The UI layer is where the primitive was first put into practice.

### 4.5 EMBER: Intent Declarations for the Third Reader

EMBER [6] is the Semantic Intent Language for legacy modernisation. Its semantic vocabulary (`INTENT`, `DIMENSION`, `THRESHOLD`, `SIGNAL`) is designed for the third reader — not the human who wrote the code, not the human who inherits it, but the AI agent that must transform it. EMBER is an antecedent form of the governance primitive: intent declared in structure, readable by agents with no other way to reconstruct the original reasoning.

### 4.6 The Convergence

| Tool | Layer | Primitive implementation |
|---|---|---|
| Rune Protocol | Binding | `?` sigil in `rune.schema.json` — co-located, versioned, queryable by binding ID |
| Wake Intelligence | Context / Memory | `causedBy` chain + `authorType` field — causal graph as governance record |
| RECALL | Document / Artifact | `CREATED-BY` enum — compile-time authorship enforcement |
| Mere | UI / Reactive | `?` sigil on reactive bindings — governance at the execution surface |
| EMBER | Legacy / Archaeology | `INTENT` construct — structural annotation for AI transformation agents |

When the same fundamental structure re-emerges independently across multiple problem domains, the structure is expressing something true about the problem, not something intentional about the solution.

---

## 5. The Authorship Dimension

### 5.1 Why Authorship Is a Governance Question

In multi-agent systems, authorship becomes a runtime concern. A risk threshold approved by a human committee has different governance standing than a threshold inferred by an optimisation agent. Both may appear as structured data in the same context package. Without authorship, they are indistinguishable.

### 5.2 Three Independent Implementations

The authorship dimension appeared independently in three tools:

- **RECALL** — `CREATED-BY` as a compile-time constraint. Three values: Human, AI compositor, AI agent.
- **Rune Protocol** — `metadata.author` on each binding annotation in `rune.schema.json`.
- **Wake Intelligence** — `authorType` parameter on `save_context`. Surfaced via the `auditor` personality mode, which groups retrieved contexts by author class.

Three implementations, different syntax, different layers — the underlying model is identical: authorship is a structural field, declared at creation, enforced by the receiving layer, preserved through transformations.

### 5.3 The Auditor Mode

```
load_context({ project: "trading-engine", personality_mode: "auditor" })
→ human: 3 contexts (risk threshold, OAuth decision, compliance boundary)
→ ai-agent: 7 contexts (optimisation decisions, inferred preferences)
→ ai-compositor: 4 contexts (ingested from Rune manifest, pipeline-generated)
→ unattributed: 12 contexts (pre-v3.5.0 entries)
```

An agent entering a new session can immediately distinguish which prior decisions are human-authorised constraints (load-bearing) and which are agent-generated optimisations (negotiable).

---

## 6. Generative UI as Derived Artifact

### 6.1 The Current State

The most visible early form of generative UI in production today is the HTML artifact produced by large language models during conversations — derived at runtime from semantic context, not from a pre-built template. The rendering is a consequence of meaning.

What is not yet in place is the infrastructure that makes it production-grade: persistent, auditable, reproducible, and tech-agnostic.

### 6.2 The Missing Infrastructure

The conversational HTML artifact has four properties that prevent production use:

1. **Stateless** — exists for the conversation, then gone. No causal node, no memory of why this shape was chosen.
2. **Unattributed** — no authorship declaration. Indistinguishable from a human-designed template.
3. **Unanchored** — no reference to the semantic contract that made this derivation valid. The same agent with slightly different context may produce a structurally incompatible artifact.
4. **Technology-bound** — cannot be re-rendered as a voice interface, a printed report, or a terminal view without rebuilding.

These are not properties of generative UI as a concept. They are properties of generative UI *without a governance primitive*.

### 6.3 What the Primitive Enables

When Semantic Intent is in place as a governance primitive:

- **Wake** provides memory: this UI shape was relevant here, for this reason. The causal graph records which prior decisions made this derivation valid.
- **RECALL** provides structure: the shape of information is declared as a typed schema, independent of rendering form. The schema is the specification; the UI is downstream.
- **Rune** provides governance: `?` annotations on the bindings feeding the UI declare the constraints the rendering must respect.
- **Mere** provides the reactive execution surface: two-way binding, computed chains, event handling.

### 6.4 The Shifted Role

The conventional model: a developer designs a UI, writes components, hardcodes the layout. Intelligence is optional.

The model the governance primitive enables: a developer declares a semantic contract. An AI agent derives the appropriate surface at runtime, based on current semantic state. The developer's job shifts from *designing interfaces* to *declaring contracts*. The interface is the AI's output, not the developer's artifact.

"Tech-agnostic" in the original sense: the contract does not know whether it will be rendered as React, HTML, a voice interface, or a structured report. The rendering is downstream of the meaning.

---

## 7. Discussion

### 7.1 Relationship to the Prior Work

This paper does not supersede [1]. The SSOT pattern remains the correct description of the two-party problem. The governance primitive is an extension: the same underlying structure, operating at the layer where agents communicate. The relationship is additive.

### 7.2 On the Emergence of the Primitive

The five-tool convergence was not designed. Each tool was built for an immediate, concrete problem. The observation that all five implement the same three-property primitive is a retrospective finding. When the same structure appears independently across multiple implementations of a domain problem, it is expressing something the domain requires.

### 7.3 Limitations

The ecosystem is young — deployed at the scale of individual projects, not enterprise pipelines. The authorship taxonomy (human / ai-agent / ai-compositor) is a starting point; the governance implications of each category remain underspecified. The generative UI thesis has not been tested as a production architecture.

### 7.4 Future Directions

1. **Formal specification of the governance primitive** — analogous to the mathematical formalisation in [1].
2. **Cross-organisation semantic contracts** — how Semantic Intent functions across organisational and regulatory boundaries.
3. **The generative UI toolkit** — building the compositional layer that wires Wake, RECALL, Rune, and Mere into a coherent generative UI pipeline.

---

## 8. Conclusion

Shatny (2025) established Semantic Intent as Single Source of Truth: a unified WHAT+WHY contract that eliminates semantic drift in AI-assisted development. The result was a structural answer to a two-party problem.

The agentic era has changed the problem. Multi-agent pipelines require governance that operates at the layer where agents communicate — before decisions are made, not in review after. This paper has proposed Semantic Intent as a governance primitive defined by three properties: immutability, addressability, and provenance.

The empirical case rests on convergence: five independently developed tools — Rune Protocol, Wake Intelligence, RECALL, Mere, and EMBER — each arrived at an implementation of the same primitive from different directions and different problem domains.

Two consequences follow directly from the primitive being in place: authorship becomes a tractable runtime governance dimension, and generative UI becomes a derived artifact of semantic state — not a template pre-built by a developer, but a surface produced by intelligence from a stable, machine-readable contract.

Semantic Intent was first a pattern. Then a SSOT. It is now a primitive. A primitive is not applied to a domain; it is what the domain is built from.

---

## References

1. Shatny, M. (2025). *Semantic Intent as Single Source of Truth: Immutable Governance for AI-Assisted Development*. DOI: [10.5281/zenodo.17114972](https://doi.org/10.5281/zenodo.17114972)
2. Shatny, M. (2026). *Rune Protocol: A Reactive Binding Grammar for Human-AI Collaborative Systems*. DOI: [10.5281/zenodo.20007883](https://doi.org/10.5281/zenodo.20007883)
3. Shatny, M. (2026). *Wake Intelligence MCP: A Five-Layer Temporal Intelligence Server for AI Agents*. npm: @semanticintent/semantic-wake-intelligence-mcp v3.5.0. [wake.semanticintent.dev](https://wake.semanticintent.dev)
4. Shatny, M. (2026). *RECALL: A COBOL-Inspired Publishing Language for AI-Auditable Artifacts*. npm: @semanticintent/recall-compiler v1.0.2.
5. Shatny, M. (2026). *Mere: A Workbook Format for Self-Contained Reactive Applications*. DOI: [10.5281/zenodo.19751778](https://doi.org/10.5281/zenodo.19751778)
6. Shatny, M. (2026). *EMBER: A Semantic Intent Language for Legacy System Modernisation*. DOI: [10.5281/zenodo.19751387](https://doi.org/10.5281/zenodo.19751387)
7. Anthropic. (2024). *Model Context Protocol Specification*. [modelcontextprotocol.io](https://modelcontextprotocol.io)
8. Shatny, M. (2026). *Strata: A Database Archaeology Methodology for Legacy SQL Systems*. DOI: [10.5281/zenodo.19768151](https://doi.org/10.5281/zenodo.19768151)

---

*© 2026 Michael Shatny / semanticintent. Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).*  
*ORCID: [0009-0006-2011-3258](https://orcid.org/0009-0006-2011-3258)*
