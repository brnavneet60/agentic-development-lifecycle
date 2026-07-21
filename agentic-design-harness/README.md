# Agentic Design Harness

Turn a real business problem into a **leadership-ready High-Level Design** for an agentic AI solution — before anyone writes production code.

This harness does not build the system. It helps you **decide what to build, why, at what cost and risk, and with what evidence** — in language executives and product leaders can use.

---

## Goal

Give organizations a repeatable way to design agentic AI from the business flow outward:

1. Understand the work as it exists today (happy paths, failures, compliance, volume).
2. Choose an operating model that fits that work.
3. Ground model, tooling, safety, and measurement choices in trusted evidence.
4. Produce one design document leadership can approve, challenge, or fund.
5. Keep a journal of every research step and every revision so decisions stay auditable.

**Success looks like:** a clear design memo that answers *what*, *why*, *how much*, *what could go wrong*, and *what we still need to confirm* — not a pile of framework notes.

---

## Who this is for

| Audience | What they can do with it |
|----------|--------------------------|
| **Industry leaders / executives** | See the business case, investment band, risks, and go/no-go questions in one place |
| **Product managers** | Align scenarios, KPIs, phased delivery, and open decisions with stakeholders |
| **Solution / enterprise architects** | Structure end-to-end agentic design with trade-offs and evidence, ready for implementation teams |
| **Risk, compliance, and ops partners** | Review safety, evaluation gates, and assumed defaults before build starts |

**Not the primary audience of the final document:** engineers needing a low-level implementation spec. Those details stay in a short engineering appendix (or a later implementation harness).

---

## What this harness does

You describe a business use case (for example: charge disputes, claims intake, policy Q&A).

The harness walks a guided design process and produces:

- A **business-facing High-Level Design** — problem, recommended approach, decisions with rationale, value and KPIs, delivery phases, team needs, risks, and open questions with planning defaults
- An **Evidence Register** — major claims tied to external industry cases, standards, or research (with web links)
- A **design journal** — what was researched, decided, and revised along the way

It stops at design. Building and deploying on a platform is a separate step (for example a platform implementation harness).

---

## Core principles

| Principle | Meaning in practice |
|-----------|---------------------|
| **Ask, don’t assume** | Missing volumes, compliance rules, or integrations are questions — not invented facts |
| **Business language first** | The design memo speaks to outcomes and trade-offs; jargon stays out of the main story |
| **Checkpoints with humans** | Pause after major stages so you confirm the flow, KPIs, design choices, safety, and measurement before the final document |
| **Evidence over opinion** | Design claims cite credible external sources; assumptions are labeled as planning defaults |
| **Configurable knowledge** | Where the harness looks for patterns, benchmarks, and trusted URLs is configurable per project |
| **Traceability** | Every design step and every rewrite is journaled so you can see how the recommendation was formed |
| **Design only** | No production agents, no silent “we’ll figure it out in code” |

---

## Where it refers from (and how you configure that)

The harness does **not** invent industry knowledge from thin air. It draws on a **configurable source map**:

| Kind of source | Role |
|----------------|------|
| **Trusted online sources** | Vendor pricing, model cards, independent benchmarks, standards bodies — only from allow-listed places |
| **Curated offline packs** | Patterns for design, tools, memory, knowledge, frameworks, cost and sizing — refreshed from known web URLs when you choose |
| **Your project overrides** | You can point a use case at its own source configuration so different teams or clients use different catalogs and trust lists |

**Configurable means:** which sources are on or off, which URLs are trusted, what is offline vs live, and how often curated packs should be refreshed — without changing the design process itself.

When the final design cites evidence, it uses the **original web address** of a case study, paper, or standard — not an internal notes file. Offline packs are helpers for the designer; the Evidence Register stays externally auditable.

Pricing and benchmark figures in catalogs are **indicative**. Confirm them before procurement.

---

## How it does its job

Think of the harness as a structured conversation with an architect agent, not a black-box report generator.

1. **Start from the business** — domain, actors, systems, sunny-day and rainy-day scenarios, compliance, and process nuances. Confirm with you before moving on.
2. **Shape the operating model** — how work is triaged, specialized, and handed to humans when confidence is low.
3. **Define what “good” means** — leadership KPIs and how you will know the solution is working.
4. **Select capabilities with trade-offs** — models, integrations, memory and knowledge, safety and security, observability and feedback loops — always with business rationale.
5. **Compile one executive design** — a single document leadership can read end to end, with open decisions called out and recommended defaults labeled clearly.
6. **Pause at gates** — you confirm direction after discovery, after KPIs, after capability design, after safety, and after measurement — before the final write-up.

Along the way the harness prefers **configured references** over random web noise, and it asks when your organization has not provided a fact.

---

## How journaling works

Everything the harness writes for a use case is meant to be **recoverable and reviewable**.

| What gets journaled | Why it matters |
|---------------------|----------------|
| **Each design step** | What was researched, what was decided, and short rationale |
| **Heavy research payloads** | Kept aside so the main conversation stays focused; full detail remains on disk if you need to audit |
| **Every revision** | When feedback changes the design, a revision entry records trigger, delta, and decisions — no silent overwrites |

You get two complementary artifacts:

- The **design document** — what leadership reads  
- The **journal** — how that document was produced and how it evolved  

Both can live in a path you choose for the use case (default or custom). That separation is what makes the harness useful for governance, reviews, and “why did we recommend this?” conversations months later.

---

## Why this is useful

Without a harness, agentic AI design often becomes:

- slide decks with no evidence trail,
- technical spikes that leadership cannot evaluate,
- or optimistic demos that skip risk, cost, and rainy-day cases.

With this harness you can:

- **Brief leadership** with one coherent design, not ten conflicting notes  
- **Align product, architecture, and risk** on scenarios, KPIs, and open decisions  
- **Defend recommendations** with industry cases and standards, not anecdotes  
- **Hand off cleanly** to an implementation team with business intent preserved  
- **Re-run the process** on the next use case with the same discipline  

---

## What you walk away with

For each use case you choose where the work is stored. You should leave with:

- The **executive High-Level Design** — the document you share with leadership  
- The **journal** of steps and revisions — the audit trail you keep  

The expected shape and quality bar for that design are defined in [`OUTPUT-STANDARDS.md`](./OUTPUT-STANDARDS.md). Where files are written is **configurable** (default layout or a custom path you name in the prompt / project config).

---

## How to invoke it (Cursor and other agentic tools)

This harness is **prompt-driven**. You do not install a CLI. Open the harness in an agent-capable environment (Cursor, Claude Code, or any Agent Skills–compatible tool), point the agent at this folder, and ask it to run the design process.

### Setup (once)

1. Open this harness in your workspace (or clone the repo that contains it).
2. Optionally set where outputs and journals should go — a default location or any **custom path** your team prefers.
3. Optionally adjust source configuration (trusted URLs, catalogs on/off) for your organization.

### In Cursor

1. Open a new Agent chat with this project in context.
2. Paste a prompt like the examples below (edit the business use case and any path preferences).
3. Confirm at each checkpoint when the agent pauses.
4. Review the design with stakeholders; ask for a journaled revision when feedback arrives.

### In other agentic tools

Same idea: load [`HARNESS.md`](./HARNESS.md) and [`OUTPUT-STANDARDS.md`](./OUTPUT-STANDARDS.md), then run the guided design with human checkpoints. Any tool that can follow multi-step skills and write files can host this harness.

### Prompt examples

**Start a new design (default settings)**

```
Using agentic-design-harness, read HARNESS.md and OUTPUT-STANDARDS.md.

Design end-to-end agentic AI for: [describe your business flow in 2–4 sentences].

Follow the full workflow with checkpoint confirmations.
Ask when information is missing — do not invent compliance, volumes, or integrations.
Produce a leadership-ready High-Level Design and journal every step.
```

**Start a design and choose where files go**

```
Using agentic-design-harness, read HARNESS.md and OUTPUT-STANDARDS.md.

Design end-to-end agentic AI for: [business use case].

Write the design document and journal under: [your preferred folder path].
Use checkpoint confirmations. Label unknowns as planning defaults.
Cite external evidence URLs only in the Evidence Register.
```

**Continue after a checkpoint**

```
Checkpoint confirmed for [step / topic]. Continue to the next stage of agentic-design-harness.
Keep asking when facts are missing. Update the journal as you go.
```

**Revise from leadership or architect feedback**

```
Revise the current design using this feedback:
[paste feedback or attach the review file]

Follow OUTPUT-STANDARDS. Journal this revision (trigger, what changed, decisions).
Do not silently overwrite prior reasoning.
```

**Re-run with your organization’s sources**

```
Using agentic-design-harness with our source configuration at [path to your source config].

Design agentic AI for: [business use case].
Prefer our trusted sources and curated packs. Pause at checkpoints for confirmation.
```

---

## Getting started

1. Open this harness in Cursor (or another agentic tool) and start a chat with one of the prompts above.
2. Name the use case and, if you want, where the design and journal should be written.
3. Answer questions and confirm checkpoints as the harness progresses.
4. Review the draft with leadership and architects; request journaled revisions until open decisions are accepted or explicitly owned.

Optional: tune **source configuration** so research follows your trust list and catalogs.

---

## Where design ends

This harness ends when the executive design is agreed.

**Building, deploying, and operating** the agents on a platform is the job of a separate implementation path — using this design as the brief, not starting from a blank page.
