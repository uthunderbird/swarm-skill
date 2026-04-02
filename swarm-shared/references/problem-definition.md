# Problem Definition

Load this file at the start of any nontrivial Swarm-family run.

## Purpose

Phase 1 exists to define the problem before route exploration begins.

Good problem definition reduces wasted iterations, weak expert assembly, and fake disagreement.

## Required Outputs

State these explicitly:
- core problem,
- scope / out of scope,
- success criteria,
- uncertainties / missing information.

For substantial or unusual tasks, also consider recording a compact:
- `Swarm Configuration Snapshot`

## Quality Bar

- The problem statement is specific enough to discriminate among routes.
- Scope excludes obvious distractions.
- Success criteria are concrete enough to know what "better" means.
- Missing information is stated clearly rather than silently assumed away.

## Failure Modes

Avoid:
- starting route adjudication before the problem is actually framed,
- treating a symptom as the core problem,
- leaving success criteria implicit,
- hiding uncertainty inside vague wording.

## Optional Swarm Configuration Snapshot

For substantial tasks, Phase 1 may include a short configuration block such as:

```text
Swarm Configuration Snapshot
- preset: Research / Discovery
- overrides: route branching budget = narrow
- rationale: high rigor and grounding, but search space is tighter than the default preset assumes
```

Use this when:
- the task clearly fits one preset,
- a preset mostly fits but needs one or two overrides,
- or the task is mixed enough that the swarm should record its tuning explicitly.

Do not require this block for small or straightforward tasks.

## Profile-Sensitive Setup Hooks

Use these hooks when `configuration.md` indicates that the task materially departs from default Swarm behavior.

### Setup Escalation Hook

If `problem ambiguity` is `high`, or `rigor / stakes` is high enough that poor framing could sink the task:
- make non-goals explicit,
- surface hidden assumptions,
- consider alternative framings,
- and clarify the actual decision target before route exploration expands.

### Failed-Search Hook

If `closure strictness` is `high`, or the task is truth-seeking enough that an unresolved result is acceptable:
- define early what would count as a failed or incomplete search,
- so the swarm can stop honestly instead of forcing tidy closure later.

### Speculation-Boundary Hook

If `creativity need` is `high` but `grounding need` is not:
- clarify whether the task is seeking scenarios, hypotheses, options, or claims,
- so later exploration is not mistaken for stronger evidence than it actually is.

If `grounding need` is `high`:
- make the evidence expectations visible early,
- so Phase 3 does not drift into unsupported framing narratives.

## Relation To Phase 2

Phase 1 defines the problem.
Phase 2 selects the expert mix and evidence boundary appropriate to that problem.

For substantial or unusual tasks, consult `configuration.md` to decide whether Phase 1 should also make explicit:
- non-goals,
- candidate framings,
- hidden assumptions,
- decision target,
- or failed-search conditions.
