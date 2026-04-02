---
name: swarm-iterate
description: Iteratively improve a target document by alternating $swarm-red-team and $swarm-mode through a delegate agent. Use when a user wants repeated critique-and-revision passes over a proof, plan, RFC, article, spec, or other document, including creating the target document first when it does not yet exist.
---

# Swarm Iterate

Run an iterative document-improvement loop through a delegate agent.

Use this skill when the user wants a target document improved through repeated critique and repair passes rather than a single draft or a single review.

This skill is for the orchestrating agent.

Do not pass `$swarm-iterate` itself to the delegate agent.

The delegate agent should know nothing about the existence of this orchestration layer. The logic in this
file is for the orchestrating agent to execute. The delegate agent should receive only:

- the concrete target-document assignment,
- the current round instructions,
- `$swarm-mode` when a drafting or repair pass is required,
- and `$swarm-red-team` when a critique pass is required.

## Core Contract

- Run the improvement process through a delegate agent, not directly in the main thread.
- Use a lower-cost delegate model when one is available.
- Never invoke `$swarm-iterate` inside the delegate agent.
- Invoke only `$swarm-mode` and `$swarm-red-team` by path inside the delegate agent.
- The orchestrating agent must drive the loop round by round.
- Send the delegate agent only the current round assignment, not the whole multi-round plan as an executable batch.
- The first delegate message must contain only the first round.
- The second delegate message must contain only the next repair or critique round.
- The third delegate message must contain only the next round after that.
- Continue this way until all rounds are complete.
- Treat the target document as the only object being improved unless the user explicitly expands scope.
- Default to `3` critique-repair rounds unless the user explicitly requests a different count.
- For each red-team round, use a different focus than in prior rounds.
- Order red-team focuses from most important to least important.
- After the first red-team, instruct the delegate agent to fix **all** findings sequentially, one by one, including low-priority findings and recommendations.
- After each repair round, run the next red-team round against the updated target document.

## Entry Decision

Determine whether the user already gave an explicit target document.

Treat the document as explicit if the user:
- names a concrete file path,
- pastes the document and clearly identifies it as the target,
- or otherwise identifies one specific existing document as the object of iteration.

If the target document is explicit:
- start immediately by sending the delegate agent a `$swarm-red-team` assignment.

If the target document is not explicit:
- start by sending the delegate agent a `$swarm-mode` assignment,
- ask it to create the target document,
- and require it to expand the user request into a concrete document specification before drafting.

After that initial creation step, continue with the standard critique-repair loop.

## Standard Loop

If the document already exists:
1. `swarm-red-team`
2. `swarm-mode`
3. repeat the pair for the configured number of rounds

If the document must be created first:
1. `swarm-mode` to create the target document from the user request
2. `swarm-red-team`
3. `swarm-mode`
4. repeat the critique-repair pair for the configured number of rounds

Interpret `3 rounds` to mean `3` red-team passes and `3` repair passes after the initial draft step when a draft was needed.

## Red-Team Focus Selection

Choose a focus ladder before starting the first critique round.

The first focus should target the highest-risk property of the document. Later focuses should move downward in importance.

Examples:

### Mathematical proof

Use a focus order like:
1. validity, proof-completeness, and necessity of each lemma
2. hidden assumptions, dependency gaps, and theorem-to-theorem justification
3. exposition clarity, notation hygiene, and local structure

### Code-change plan or engineering RFC

Use a focus order like:
1. completeness and correctness of dependencies, prerequisites, and interface impacts
2. execution order, rollback or failure modes, and test coverage adequacy
3. wording precision, consistency, and internal coherence

### Informational article or explanatory note

Use a focus order like:
1. factual accuracy, wording precision, and internal consistency
2. unsupported claims, overclaiming, and argumentative gaps
3. clarity, structure, and readability

If the document type is unusual, derive an equivalent focus ladder explicitly before the first round.

## Required Delegate Instructions

When delegating to the delegate agent, make these instructions explicit:

- do not mention `$swarm-iterate`,
- state the exact target document path or target artifact to create,
- state the current red-team focus for the current round,
- require durable criticism output for each red-team round when the critique is substantial,
- require that every finding be addressed sequentially in the following swarm pass,
- forbid bundling all fixes into one vague “cleanup” step,
- require that each subsequent red-team round change focus,
- give instructions only for the current round,
- do not ask the delegate agent to execute future rounds yet,
- require a final summary listing:
  - target document,
  - rounds completed,
  - focus used in each round,
  - key fixes made,
  - and any residual issues still left open.

For the first repair pass after the first red-team, use especially explicit wording:

- fix every finding sequentially,
- do not skip low-priority issues,
- do not skip recommendations,
- and do not mark the round complete until every listed item has been addressed or explicitly retired with justification.

## Recommended Delegate Prompt Shape

Use a prompt shaped like this:

- never mention `$swarm-iterate`,
- identify the target document,
- identify the current round only,
- identify the current focus,
- require `$swarm-mode` and `$swarm-red-team` usage by path,
- require a compact end-of-round ledger,
- and do not instruct the delegate agent to perform later rounds in the same message.

Treat the delegate agent as if it were receiving ordinary user work, not a meta-instruction about a higher
level orchestration skill.

## Prompt Templates

Use these as canonical starting templates. Adapt only the document-specific details.

### Initial creation round template

Use this when the target document does not yet exist.

```text
Use $swarm-mode at /absolute/path/to/swarm-mode to create the target document.

Target artifact:
- <target path or artifact description>

User request to expand into a document:
- <user request>

Requirements:
- first turn the request into a concrete document specification,
- then draft the target document,
- keep the scope to the target document only unless explicitly expanded,
- produce a compact end-of-run ledger with:
  - target document,
  - specification chosen,
  - main sections created,
  - and residual open issues.
```

### Red-team round template

Use this for every critique pass.

```text
Use $swarm-red-team at /absolute/path/to/swarm-red-team to critique the target document.

Target document:
- <target path>

Round:
- <round number> of <total rounds>

Focus for this round:
- <focus text>

Requirements:
- produce a durable critique artifact if the critique is substantial,
- keep the critique focused on this round's focus,
- distinguish critical findings, lower-priority findings, and recommendations,
- and end with a compact ledger containing:
  - target document,
  - focus used,
  - main findings,
  - and the exact ordered fix list for the repair round.
```

### Repair round template

Use this after every red-team pass.

```text
Use $swarm-mode at /absolute/path/to/swarm-mode to repair the target document.

Target document:
- <target path>

Round:
- <round number> of <total rounds>

Repair source:
- <critique artifact path or critique summary>

Requirements:
- fix every finding sequentially, one by one,
- do not skip low-priority findings,
- do not skip recommendations,
- do not collapse all edits into one vague cleanup step,
- if any item is retired instead of fixed, justify that retirement explicitly,
- and end with a compact ledger containing:
  - target document,
  - items fixed in order,
  - items retired with justification,
  - and any residual issues still open.
```

## Output Expectations

Back in the main thread, report:
- the target document used,
- whether the process started from creation or critique,
- the configured round count,
- the focus ladder used,
- and the delegate agent's final summary of progress and residual issues.

## Common Mistakes

- do not pass `$swarm-iterate` to the delegate agent
- do not mix red-team and repair instructions in one delegate prompt
- do not send the delegate agent the entire multi-round plan as one executable batch
- do not ask the delegate agent to complete all iterations in one shot
- do not skip the orchestrating-agent responsibility to drive the delegate agent through the loop round by round
