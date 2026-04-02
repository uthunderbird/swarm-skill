# Swarm Routing

Load this file after Phase 1 and Phase 2 setup, when choosing the next option or deciding whether to continue, checkpoint, or finalize.

## Scope

This file governs post-setup routing.

- `problem-definition.md` frames the problem.
- `expert-assembly.md` selects the expert mix and evidence boundary.
- `routing.md` chooses how the process moves once that setup exists.

It is not the primary guide for how to perform Phase 1 or Phase 2.

For substantial or unusual tasks, use `configuration.md` to tune how aggressively the swarm should branch, ground, narrow, checkpoint, and stop.

## Option Selection Heuristics

### Choose `B` when
- key user-owned information is missing,
- the environment cannot safely resolve that ambiguity,
- or continuing would force the swarm to guess at a material preference or boundary.

### Choose `A1` when
- a prior discussion round produced explicit expert-to-expert questions,
- those questions need resolution before another route shift,
- or expert disagreement remains ambiguous because the direct clarifications have not happened yet.

### Choose `A` when
- the problem is still broad,
- multiple expert perspectives are needed,
- or route structure is still unclear.

### Choose `C` when
- the field is clear,
- but one specific sub-question needs deeper refinement,
- or a smaller subset of experts can reduce ambiguity faster than another broad round.

### Choose `D` when
- two routes genuinely compete,
- there is a meaningful tradeoff to adjudicate,
- or hidden assumptions need to be forced into the open so the swarm can choose a path.

### Choose `X` when
- two positions are genuinely incompatible,
- burden of proof matters,
- the task needs adversarial cross-examination rather than lightweight route choice,
- or a clean synthesis would blur a real disagreement.

If the proposition itself is under contest, prefer `X`.
If the proposition is accepted and the remaining question is which route to take, prefer `D`.

### Choose `E` when
- local files, tools, commands, or data can ground an uncertain claim,
- one bounded action can discriminate among live routes,
- or implementation itself is the best next test.

Bias toward `E` when it can replace speculative discussion.
Treat `E` as a bounded execution mini-loop, not just a place to read a file or emit faux-grounded findings.
If the best next discriminator is search, editing, scripting, running code, or another real tool action, prefer `E`.

### Choose `G` when
- enough information exists to reassess progress honestly,
- route priorities need to be updated,
- or the active route needs explicit keep / retire / reopen logic.

### Choose `H` when
- the answer is stable,
- key uncertainties are resolved or explicitly bounded,
- and stopping is more useful than another iteration.

## Profile-Sensitive Routing Hooks

Use these hooks when `configuration.md` indicates that the task materially departs from default Swarm behavior.

### Grounding Urgency Hook

If `grounding need` is `high`, or `rigor / stakes` is high enough that unsupported claims would materially weaken the result:
- do not stay long in speculative discussion without a discriminative `E`,
- prefer grounding once the next factual discriminator is visible,
- and resist elegant synthesis built on untested assumptions.

### Branching Compression Hook

If `route branching budget` is `narrow`, or one or two routes are already dominating:
- compress sooner into `C`, `D`, or `E`,
- prune decorative alternatives,
- and make route ranking explicit before continuing.

### Wide-Branch Tolerance Hook

If `creativity need` is `high` and `route branching budget` is `wide`:
- do not compress too early just because one route sounds neat,
- allow multiple live routes to coexist longer,
- but keep route labels explicit so exploration does not dissolve into drift.

### Closure-Pressure Hook

If `closure strictness` is `high`, or unresolved uncertainty is still materially decision-relevant:
- prefer another discriminator, regroup, or bounded clarification before synthesis,
- keep unresolved risks visible,
- and treat premature tidy closure as a routing failure rather than a stylistic success.

### Post-Debate Resolution Hook

If `D` identifies a winning route but leaves materially architecture-shaping or design-shaping unresolved questions:
- prefer a resolving `E` or `C` before `H`,
- or explicitly defer those questions at `G`,
- rather than letting a clean adjudication win silently absorb unresolved implementation choices.

### Post-Cross-Examination Hook

If `X` leaves factual or design uncertainty that still blocks confidence in the verdict:
- prefer `E` for factual discrimination,
- prefer `C` for scoped narrowing,
- prefer `G` when route status must be reassessed explicitly,
- and use `H` only when the adversarial verdict materially stabilized the answer.

## Pivot Rules

- Do not abandon the active route because another route is more interesting.
- Pivot only when there is:
  - a concrete new discriminator,
  - materially new evidence,
  - or a sharper problem formulation.
- Do not pre-plan option sequences in advance (see Hard Invariant 12 in core.md). Choose the next move only after the current iteration has actually run.

## Iteration Shape

A strong compact iteration usually looks like:
1. Moderator states why this option is next.
2. Execute one option.
3. Update todo / route status.
4. Choose the next best move.

Prefer fewer strong iterations over many shallow ones.
If `A` generated explicit expert questions, prefer `A1` before jumping to unrelated options.
The reasoning in step 1 should come before the decision and should be substantive enough to reveal the actual choice logic.
Use `D` for route choice and `X` for true adversarial claim testing; do not treat them as interchangeable.
Do not use `D` as a softer stand-in when the real need is to decide whether a claim survives adversarial burden-of-proof pressure.
For `E`, the Executor should normally make the questions, scope, and execution plan explicit before calling tools.

## Failure Recovery

- If discussion is circular, choose `E` for grounding or `G` for a real regroup.
- If key user information is missing and cannot be safely assumed, stop and ask concise clarifying questions.
- If an executor action fails, report the failure and re-plan explicitly instead of pretending the route advanced.
- If the process starts converging too quickly into tidy agreement, use `A`, `C`, `D`, or `X` to force another real discriminator before synthesis.
