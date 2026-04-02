---
name: swarm-mode
description: Run the full Swarm Mode problem-solving process with Moderator/Executor roles, iterative options, and structured continuation. Use for requests that explicitly ask for swarm mode or disciplined multi-expert problem solving.
allowed-tools: Read, Write, Edit, Bash, Glob, Grep
---

# Swarm Mode — Entrypoint

This file is the complete operational guide. All modules are lazy-loaded: read them only when the embedded summary here is insufficient for the current step.

**Shared module root:** `../swarm-shared/references/`

---

## Core Contract

These properties must never be violated:

- Do not skip the process once invoked — no synthesized shortcuts
- Keep the Moderator / Executor split throughout
- Choose exactly one option per iteration; decide the next only after the current finishes
- Ground uncertain claims when files, tools, or data can discriminate
- Checkpoint honestly — a checkpoint must reflect real state change
- Finalize only when convergence is justified

---

## Phase 1 — Problem Definition

Frame the problem before route exploration begins. State explicitly:
- core problem
- scope / out of scope
- success criteria
- uncertainties / missing information

Read `problem-definition.md` upon entering Phase 1. This is unconditional.

Path: `problem-definition.md`

---

## Phase 2 — Expert Assembly

Default: 3–5 experts, at least 2 critics and 1 evangelist. Adjust critic/evangelist balance by rigor vs creativity need.

Read `expert-assembly.md` upon entering Phase 2. This is unconditional.

If the task complexity or type warrants tuning, also read `configuration.md` immediately after `expert-assembly.md`.

Path: `expert-assembly.md`

---

## Phase 3 — Dynamic Iteration

Run iterative options until a stop condition is reached. Each iteration:
1. **Backlog scan** — at the top of Moderator Reasoning, before any analysis: scan Open Items for aged or blocked entries. One line if nothing requires action; explicit escalation if blocked-user-owned item is present (see Open Items below).
2. **Moderator Reasoning** — name the specific unresolved gap and why the next option addresses it (causal, not transitional).
3. **Execute one option.**
4. **Update route and Open Items** — state any route state changes (with all four elements: route, prior state, new state, justification) and update Open Items states.
5. **Choose the next option.**

Every 4–5 iterations: include a Status Summary (progress, unresolved questions, route priorities).

**Open Items** tracks all unresolved questions, missing information, and decisions across iterations. It replaces "Todo List." See `core.md` for the full lifecycle (7 states, age counters, escalation rules).

**Tool preference:** If task-management tools are available (e.g. TaskCreate / TaskUpdate / TaskList), use them as the Open Items implementation and narrate state in Moderator output. If no native tools: maintain a self-written list updated at each iteration boundary.

### Options — when to use each

| Option | Use when |
|--------|----------|
| `A` Round-Robin | Problem is broad; multiple expert perspectives needed; route structure unclear |
| `A1` Expert Q&A | Prior `A` round produced explicit expert-to-expert questions that need resolution |
| `B` Clarifying Questions | Key user-owned information is missing and cannot be safely assumed |
| `C` Subgroup | Field is clear; one sub-question needs deeper refinement by a smaller group |
| `D` Adjudication | Two routes genuinely compete; tradeoff needs explicit resolution |
| `X` Cross-Examination | Two positions are genuinely incompatible; adversarial burden-of-proof testing needed |
| `E` Executor | Local files, tools, or data can ground an uncertain claim; prefer over speculative discussion |
| `F` Expert Interview | Team is at the limit of its competence; an external expert with privileged knowledge can answer a specific question or validate a hypothesis |
| `G` Checkpoint | Enough state change to reassess route priorities honestly |
| `H` Finalization | Answer is stable; stopping is more useful than another iteration |

### Module Load Rule (MLR)

Immediately after "Next Decision: Option X", before executing the option, read the corresponding module. This is unconditional — do not check whether the module was read in a prior iteration. The read happens in the same response as the Next Decision block, before the option executes.

| Option | Module |
|--------|--------|
| `A`  | `options/a-round-robin.md` |
| `A1` | `options/a1-expert-qa.md` |
| `B`  | `options/b-clarifying-questions.md` |
| `C`  | `options/c-subgroup.md` |
| `D`  | `options/d-adjudication.md` |
| `X`  | `options/x-cross-examination-debate.md` |
| `E`  | `options/e-executor.md` |
| `F`  | `options/f-expert-interview.md` |
| `G`  | `options/g-checkpoint.md` |
| `H`  | `options/h-finalization.md` |

Repeated use of the same option in one session: read again — do not assume the prior read is still in context (compaction may have removed it).

### Cross-Iteration Invariants

Check these at the boundary of every iteration — after Moderator Reasoning, before Next Decision.

**Invariant 1 — Route State Monotonicity**
Every iteration must change the state of at least one active route. A valid state change names: (a) the route, (b) its prior state, (c) its new state, (d) the justifying evidence or reasoning. Generic expert agreement without these four elements does not count.
- *If violated:* insert a mini-G before Next Decision — state what the iteration produced, why no route changed, and what the next iteration must do differently.

**Invariant 2 — Evidence Debt**
Any claim labeled `[assumption: X]` or `[uncertain: X]` must be grounded via Option E within two iterations, or carried as named debt in the route ledger. Unlabeled speculation is not permitted — experts must tag assumptions and uncertain claims inline.
- *If violated:* open an E-targeted route for the oldest unresolved debt before choosing the next option.

**Invariant 3 — Compression Gate**
After every 4 iterations, if open routes exceed the branching budget set in Phase 1, a compression pass is required before the next iteration — explicitly close or merge routes that have not produced discriminating evidence.
- Default branching budget: moderate (≤3 open routes). Use Phase 1's stated budget if different.

**Invariant 4 — Causal Moderator Reasoning**
Every Moderator Reasoning block must name a specific unresolved gap and state why the chosen next option addresses it. Transition-line reasoning ("we've heard from experts, now let's...") is a process violation.
- *If violated:* rewrite before proceeding. Next Decision does not execute until Moderator Reasoning is causal.

---

## Configuration — when to tune

Default behavior is sufficient for most tasks. Load configuration modules when the task materially departs from defaults.

**Six demand axes** (each: low / medium / high, or narrow / moderate / wide for branching):
- **rigor / stakes** — cost of wrong answer; high → more critics, stricter finalization
- **grounding need** — how tightly claims must tie to evidence; high → bias toward `E` early
- **creativity need** — route generation and novelty; high → more evangelist energy
- **problem ambiguity** — clarity of framing itself; high → more Phase 1 effort
- **route branching budget** — how many live routes to tolerate; wide → slower compression
- **closure strictness** — how strong the stop condition must be; high → "answer not found" is acceptable

**Five workflow presets** (choose by workflow demand, not subject label):
- **Audit / Critique** — test adequacy, surface risks, invalidate weak claims
- **Research / Discovery** — truth-seeking with open questions and strong evidence coupling
- **Diagnosis / Engineering** — implementation-heavy, debug-heavy, tool-grounded
- **Ideation / Product** — option generation, framing, prioritization
- **Scenario / Strategic Exploration** — speculative, future-oriented, not directly verifiable

**When to load configuration modules:**
- Task is substantial and default behavior needs explicit tuning → `configuration.md` (index + cheatsheet)
- Need axis definitions → `configuration-axes.md`
- Need preset details and selection heuristics → `configuration-presets.md`
- Need trigger conditions for when tuning is required/recommended/optional → `configuration-conditions.md`
- Need axis→behavior mappings (team shape, grounding posture, branching, closure) → `configuration-mappings.md`

---

## Invariants — when to load `core.md`

The embedded rules above cover normal operation. Load `core.md` when you need:
- full hard invariants list (evidence type labels, route status labels, stop rules)
- lightweight ledger format for medium/long investigations
- standard header format

Path: `core.md`

---

## Routing detail — when to load `routing.md`

The option table above covers normal routing. Load `routing.md` when you need:
- Profile-Sensitive Routing Hooks (grounding urgency, branching compression, closure pressure, post-debate resolution, post-cross-examination)
- Pivot rules (when abandoning an active route is justified)
- Failure recovery procedures (circular discussion, missing user info, executor failure)

Path: `routing.md`

---

## Artifacts — when to load `artifacts.md`

Load when the task is long-running, SSOT-sensitive, or likely to be resumed, and you need guidance on when durable artifacts help vs when they are noise.

Path: `artifacts.md`

---

## Canonicality — when to load `canonicality.md`

Load when source-of-truth or family-extension questions arise (e.g., which file is authoritative, how to extend the swarm family without creating drift).

Path: `canonicality.md`

---

## Domain-specific overrides

Domain-specific skill variants may override any section of this entrypoint by providing their own:
- Phase 1 framing guidance (problem types, non-goals, success criteria specific to the domain)
- Phase 2 expert assembly (domain-specific expert roles, evidence boundaries)
- Option routing preferences (e.g., bias toward `E` for code tasks, bias toward `D` for strategy tasks)
- Configuration preset defaults

When a domain variant is active, it takes precedence over the generic guidance in this file for the sections it explicitly overrides. Sections not overridden fall back to this file.
