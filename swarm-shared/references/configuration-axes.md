# Swarm Configuration Axes

This file defines the core task-demand axes used to tune Swarm behavior.

## 1. Rigor / Stakes

How costly would a wrong answer or weak process be?

- `low`
- `medium`
- `high`

High values increase:
- critic share,
- demand for explicit assumptions and non-goals,
- tolerance for "answer not found",
- and finalization strictness.

## 2. Grounding Need

How strongly should claims be tied to files, tools, data, or other evidence?

- `low`
- `medium`
- `high`

High values increase:
- bias toward `E`,
- evidence-boundary strictness,
- and pressure to distinguish verified facts from hypotheses.

## 3. Creativity Need

How much route generation, novelty, or speculative ideation is required?

- `low`
- `medium`
- `high`

High values increase:
- evangelist share,
- route branching tolerance,
- and tolerance for exploratory hypotheses.

## 4. Problem Ambiguity

How unclear is the problem framing itself?

- `low`
- `medium`
- `high`

High values increase:
- Phase 1 effort,
- value of explicit non-goals,
- value of listing candidate framings or hidden assumptions,
- and resistance to early narrowing.

## 5. Route Branching Budget

How many live routes is it worth exploring before compression?

- `narrow`
- `moderate`
- `wide`

Wide values increase:
- repeated `A` use,
- tolerance for multiple live routes,
- and slower convergence to `C`, `D`, or `H`.

## 6. Closure Strictness

How strong must the stop condition be?

- `low`
- `medium`
- `high`

High values increase:
- checkpoint scrutiny,
- finalization readiness threshold,
- willingness to stop with unresolved uncertainty visible,
- and willingness to say the answer was not found.
