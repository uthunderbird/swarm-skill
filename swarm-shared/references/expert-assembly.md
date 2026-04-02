# Expert Assembly

Load this file when Phase 2 needs more than a trivial expert setup.

For substantial or unusual tasks, consult `configuration.md` first so team shape reflects rigor, grounding, creativity, branching, and closure demands.

## Purpose

Expert assembly should improve route discrimination, not create theater.

## Team Size

- Use 3-5 experts by default.
- Use fewer when the problem is narrow and well-framed.
- Use more only when the problem genuinely needs distinct perspectives.
- For full swarm, 5 is the preferred default when the problem is substantial.

## Role Architecture — Two Axes

Expert roles have two orthogonal dimensions:

**Axis 1 — Orientation** (critic / balanced / evangelist): how the expert relates to risk and novelty. Mandatory at the team level — the topology rule below applies to this axis.

**Axis 2 — Functional role** (optional): what the expert specifically searches for, beyond general domain expertise. Functional roles are active only in discussion options (A, A1, C, D, X, F) — not in E, G, or H.

A functional role *qualifies* the orientation, it does not replace it. Notation:

```
[Name] (Critic · Reframer)        — orientation + function
[Name] (Monitor-Evaluator)        — function carries its own orientation (neutrality is built in)
[Name] (Evangelist)               — default expert, no functional specialization
```

When a functional role is naturally orientation-leaning (e.g. Implementer is critic-leaning), state it explicitly and count it toward the topology rule. Exception: Monitor-Evaluator is by definition orientation-neutral — adding "Critic" would break its meaning.

Limit: not more than one functional specialization per expert, and not more than 2–3 functional specialists in a 5-person team.

## Functional Roles — Available Repertoire

Use these when the task has a specific gap that a default domain expert would not fill:

| Role | What it searches for | Natural orientation |
|------|---------------------|-------------------|
| **Analogist** | Structural analogies in other domains — imports their solutions | Evangelist-leaning |
| **Inverter** | Inverts the task ("how to achieve the opposite?") and extracts ideas from the answer | Evangelist-leaning |
| **Combinatorialist** | Non-obvious combinations of known elements *within* the problem space | Evangelist-leaning |
| **Provocation Generator** | Deliberately absurd or impossible statements as entry points for extracting ideas via cognitive shock | Evangelist-leaning |
| **Constraint Relaxer** | Removes implicit and explicit constraints one at a time to expand the search space from within | Evangelist-leaning |
| **Reframer** | Signs that the wrong problem is being solved — framing errors | Critic-leaning |
| **Implementer** | Execution gaps — what will practically prevent realization | Critic-leaning |
| **Completer-Finisher** | Detail-level gaps, loose ends, internal inconsistencies | Critic-leaning |
| **Devil's Advocate** | Weaknesses in the current consensus (attacks the agreement, not just the idea) | Critic-leaning |
| **Synthesizer** | Common ground and integration space between competing positions | Balanced-leaning |
| **Monitor-Evaluator** | Neutral assessment of options without a stake in the outcome | Neutral (built in) |
| **Extrapolator** | Projects the current direction to its logical extreme — "if X = 100%, what happens?" | Neutral (opens opportunities or risks on the horizon) |

Role distinctions for evangelist-leaning roles: Analogist looks *outside* the problem (other domains); Combinatorialist works *inside* the known solution space; Inverter searches via negation; Provocation Generator uses shock as a generative trigger; Constraint Relaxer expands search space by lifting one constraint at a time (unlike Reframer, which reframes the task itself).

## Critic / Evangelist Topology

For full swarm by default:
- include at least `2 critics`,
- include at least `1 evangelist`,
- then fill remaining slots with domain-relevant balanced or role-specific experts.

Count by orientation axis — including the natural orientation of any functional roles assigned. This is a topology rule, not a theater rule. Its job is to preserve useful disagreement before synthesis.

## Creativity vs Formalism

Before finalizing the team, assess whether the problem leans more toward:
- creativity / route generation,
- or formalism / rigor / adequacy control.

Then tune the team accordingly:
- more creative problems should bias toward more evangelist energy,
- more formal or high-stakes problems should bias toward more critics,
- but the default minimums above should still hold unless there is a clear reason to break them.

## Selection Heuristics

- If rigor matters, bias toward critics and grounding-oriented roles.
- If exploration matters, include at least one evangelist-leaning functional role — choose by generative mechanism: Analogist for cross-domain import, Inverter for negation-based search, Combinatorialist for recombination within the known space, Provocation Generator for shock-entry ideas, Constraint Relaxer for lifting hidden assumptions.
- If implementation is likely, include Implementer or Completer-Finisher.
- If stakes are high, narrow the evidence boundary and favor skeptics.
- If the problem arrived pre-framed and there is risk of solving the wrong problem, add a Reframer.
- Where useful, name the role orientation explicitly as critic, evangelist, or balanced.

## Role Fixation and Deduplication

**Fixation:** Roles are fixed in Phase 2 and do not change during the session. One reassignment is permitted via explicit Moderator Reasoning ("expert X shifts from function Y to Z because...").

**Deduplication:** Conducted at assembly time, not from an abstract catalog. For each pair of experts, ask: "Can each bring something to this specific task that the other cannot?" If not — remove one. Overlap threshold: if two roles would search >80% the same space on the given task, one is redundant. Example: Plant vs Evangelist in an ideation task → remove Plant.

## Evidence Boundary

State what the experts may rely on:
- local files only,
- provided user context,
- tool-grounded findings,
- or clearly labeled assumptions.

Do not let experts smuggle in unsupported facts.

## Profile-Driven Assembly

Apply in two passes. Start from defaults (3–5 experts, ≥2 critics, ≥1 evangelist, standard evidence boundary). Modify only when a dimension is non-default.

### Pass 1 — Threshold Modifications

Each fires independently when its dimension is non-default:

| Dimension | Non-default value | Modification |
|-----------|------------------|-------------|
| Output type | artifact-producing | Tighten evidence boundary: grounding required for all technical claims |
| Answer structure | semi-open | Replace one critic slot with balanced; add **Synthesizer** |
| Answer structure | open | Replace one critic slot with evangelist; add **Synthesizer** |
| Ill-posedness | ill-posed | Add **Reframer** |
| Problem structure | compositional / hierarchical | Expand domain breadth to match sub-problem count; add **Synthesizer** if not already present |
| Problem structure | recursive | Narrow to single-domain depth; add **Implementer** |
| Complexity | ≥ 4 | Expand team toward 5 experts; tighten evidence boundary |
| Complexity | 5 | Warn user before proceeding — state whether misleading-if-one-pass or coverage-limited-if-one-pass |

**Deduplication:** each functional role is added once regardless of how many dimensions trigger it.

### Pass 2 — Interaction Overrides

Check after Pass 1. These override topology when triggered:

| Combination | Override |
|-------------|---------|
| **closed + ill-posed** | Upgrade to strongly critic-heavy (≥3 critics in a 5-person team). Reframer gets explicit license to challenge the closed framing itself, not just refine routes within it — the team will anchor on the closed answer structure; Reframer must be empowered to question whether the question is actually closed. |
| **open + ill-posed** | Phase 1 must produce a stable scope boundary before Phase 2 begins. If it cannot, call Option B (user input) before assembling the team. Once scope is bounded: apply critic-heavy topology — this overrides the standard open → +evangelist rule. Open + ill-posed needs constraint, not more route generation. |

### Persona Mode

**Default: assign real named experts.** Naming a world-renowned figure anchors the persona's reasoning style, intellectual lineage, and domain authority in a way that abstract role labels do not.

- **Real named experts (default):** when the domain has recognizable world-class figures (e.g. Dr. Michael Stonebraker for databases, Leslie Lamport for distributed systems, Barbara Liskov for software design). Use their actual name, not a generic title.
- **Abstract role labels:** only when the domain is too narrow or applied for any real figure to be a natural fit, or when naming a specific person would distort the reasoning.
- **Composite archetypes:** when the task is exploratory and no single real figure fits.

When using named experts: state their name and the specific competence they bring. "Dr. Michael Stonebraker (database architecture, relational systems pioneer)" is correct. "Database Expert 1" is not.

### What profile dimensions do not drive

- **Domain identity** (which specific domains to represent) — always task-content-driven, never profile-driven.
- **Named expert vs. abstract label** — see Persona Mode above; driven by domain recognizability, not task profile.

## Team Picker Mode (Complexity 4–5)

For complexity 4 and 5 tasks, Phase 2 uses Team Picker instead of direct assembly. Profile-driven rules (Pass 1 and Pass 2) still determine the required team *shape* — topology, functional roles, evidence boundary. Team Picker determines *how* the Moderator finds experts that satisfy that shape.

### Why

Direct assembly generates and commits simultaneously, drawing from an implicit candidate space that defaults to the most obvious and prestigious domain experts. For complex tasks, this produces systematically under-diverse teams. An explicit candidate pool forces deliberate search before commitment.

### Procedure

**Step 1 — Generate the pool (all 10 before any picking begins).**

Generate 10 candidate experts. The pool must satisfy diversity requirements:
- ≥2 experts from domains *adjacent* to the core problem (not primary domain specialists)
- ≥1 critic-oriented expert (skeptic of the dominant approach in the domain)
- ≥1 expert with a generative functional role (Analogist, Inverter, Combinatorialist, Provocation Generator, or Constraint Relaxer)
- ≥1 expert whose specific expertise is *failure modes* of the solution space

Remaining 5 slots: free, driven by task content. Do not begin picking until all 10 candidates are listed.

**Step 2 — Iterative selection.**

Pick one expert at a time. For each pick:
1. State the reasoning: what gap this expert fills given who is already on the team.
2. Make the selection explicit before moving to the next pick.
3. Add the expert to the team.

Stop when the team is ideal or when 5 experts have been selected — whichever comes first. The cap is 5, consistent with the standard team size ceiling.

### Invariants

- Profile-driven topology rules still apply: the final team must satisfy ≥2 critics, ≥1 evangelist, and any functional roles required by Pass 1/Pass 2.
- Named expert defaults still apply: use real world-renowned figures where the domain permits.
- If a required functional role (e.g. Reframer from ill-posedness flag) is not covered by the selected team, the Moderator must add it even if the cap would otherwise be reached.

## Failure Modes

Avoid:
- redundant experts saying the same thing,
- critic-free teams that collapse into agreeable synthesis,
- evangelist-free teams that never generate viable alternatives,
- failing to make team asymmetry explicit when the task clearly requires it,
- choosing persona style without regard to grounding or creativity demands,
- domain cosplay with no decision value,
- too many roles for a small problem,
- experts making factual claims that the Executor has not grounded.
