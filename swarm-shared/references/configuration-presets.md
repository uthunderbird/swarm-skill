# Swarm Configuration Presets

These are workflow presets, not domain presets.

## 1. Audit / Critique

- rigor / stakes: `high`
- grounding need: `high`
- creativity need: `low` to `medium`
- problem ambiguity: `medium`
- route branching budget: `narrow` to `moderate`
- closure strictness: `high`

Use when the goal is to test adequacy, surface risks, or invalidate weak claims.

## 2. Research / Discovery

- rigor / stakes: `high`
- grounding need: `high`
- creativity need: `medium`
- problem ambiguity: `high`
- route branching budget: `moderate` to `wide`
- closure strictness: `high`

Use when the task mixes open exploration with strong truth-seeking demands.

## 3. Diagnosis / Engineering

- rigor / stakes: `high`
- grounding need: `high`
- creativity need: `medium`
- problem ambiguity: `medium`
- route branching budget: `narrow` to `moderate`
- closure strictness: `medium` to `high`

Use when the task is implementation-heavy, debug-heavy, or operational.

## 4. Ideation / Product

- rigor / stakes: `medium`
- grounding need: `medium`
- creativity need: `high`
- problem ambiguity: `medium` to `high`
- route branching budget: `wide`
- closure strictness: `medium`

Use when the main value is option generation, framing, and prioritization.

## 5. Scenario / Strategic Exploration

- rigor / stakes: `medium`
- grounding need: `low` to `medium`
- creativity need: `high`
- problem ambiguity: `high`
- route branching budget: `wide`
- closure strictness: `low` to `medium`

Use when the task is exploratory, speculative, or future-oriented rather than directly verifiable.

## Preset Selection Heuristics

Choose a preset by workflow demand, not by subject label.

### Use `Audit / Critique` when
- the job is to test adequacy, invalidate weak reasoning, or surface risk,
- and error cost or rigor demand is high.

### Use `Research / Discovery` when
- the task is truth-seeking,
- open questions remain substantial,
- and exploration must stay tightly coupled to evidence.

### Use `Diagnosis / Engineering` when
- the task is implementation-heavy, debug-heavy, or operational,
- and concrete discrimination through files, tools, or behavior matters quickly.

### Use `Ideation / Product` when
- the job is to generate options, frames, or priorities,
- and novelty matters more than formal proof of correctness.

### Use `Scenario / Strategic Exploration` when
- the task is future-oriented, societal, or speculative,
- and the output is useful if it is disciplined, not necessarily directly verifiable.

## When Preset Alone Is Enough

A preset is usually enough when:
- one workflow style clearly dominates,
- the task does not mix very different demands,
- and no single axis obviously sits far from the preset default.

## When To Override One Or Two Axes

Override a small number of axes when:
- the preset mostly fits,
- but one demand is unusually strong or unusually weak.

Examples:
- product ideation with unusually high stakes -> start from `Ideation / Product`, raise `closure strictness` and maybe `grounding need`
- research with unusually narrow search scope -> start from `Research / Discovery`, reduce `route branching budget`

## When Full Custom Tuning Is Worth It

Do full tuning only when the task is:
- unusually mixed,
- unusually high-stakes,
- or likely to fail under a default preset.

Typical examples:
- high-stakes scientific or biomedical reasoning,
- mathematically deep work with partial empirical grounding,
- strategic analysis that mixes forecasting, critique, and concrete planning.
