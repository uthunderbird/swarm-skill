# Option E - Executor Action

Use `E` when a bounded tool-backed action can ground the next decision.

## Best For

- checking local files,
- running commands,
- searching the environment,
- modifying files or writing code when the task calls for it,
- writing and running scripts,
- verifying assumptions,
- performing a concrete implementation step,
- discriminating among routes with evidence rather than discussion.

`E` is not limited to reading files. The Executor may use the full tool surface available to the agent when that is the best way to answer the bounded task.

## Output Shape

- Moderator reasoning
- bounded executor task
- executor questions
- scope of work
- execution plan
- real tool calls
- tool-backed findings
- result-type labeling where useful
- route update
- next option selection

## Execution Preflight

Before calling tools, the Executor should briefly make explicit:
- the key questions being answered,
- the scope of work,
- and the execution plan.

Keep this preflight compact for simple tasks, but do not skip it.

The point is to make clear:
- what the Executor is trying to discriminate,
- why this scope is sufficient,
- and why these tools are the right next move.

## Adaptive Rendering

The preflight should scale with task size.

For small `E` actions:
- one compact line is enough if it clearly covers question, scope, and plan.

For normal `E` actions:
- prefer 2-4 short bullets, usually:
  - `Questions: ...`
  - `Scope: ...`
  - `Plan: ...`

For broader or riskier `E` actions:
- use an explicit mini-block with all three labels,
- especially when the action involves multiple tools, repo-wide search, edits plus verification, scripts, or higher-cost execution.

## Preflight Style

Explain the discriminator, not the obvious mechanics.

Good:
- `Executor plan: verify whether the setting is global or variant-local by checking config and its call sites.`
- `Questions: is the failure caused by missing data model fields or by aggregation logic?`
- `Scope: models + scoring path only, not the whole repo.`

Weak:
- `Plan: run rg, read files, and think about them.`
- `Scope: look around the project.`
- `Questions: figure out what is going on.`

## Quality Bar

- the executor action is specific and discriminative,
- the preflight is clear enough to show what is being tested and why,
- the scope is bounded rather than sprawling,
- the tool calls are real when tools would materially help,
- findings are concrete,
- findings are clearly separated from interpretation,
- interpretation does not outrun the evidence.

## Scope Discipline

- Narrow the scope before exploring the environment broadly.
- Prefer the smallest search, edit, script, or command sequence that can discriminate among live routes.
- If the task is too large for one bounded executor action, say so and reduce the scope rather than flailing.

## Tool Discipline

- When tools would materially help, do not simulate executor findings from reasoning alone.
- Use the real tools available to the agent rather than treating `E` as a placeholder.
- If the Executor is asked to implement something, it may edit files, write code, run scripts, and verify the result within the bounds of the selected task.

## Failure Modes

- using `E` for a vague fishing expedition,
- starting tool calls without first making the questions and scope explicit,
- choosing tools without explaining what they are meant to discriminate,
- reporting pseudo-findings without real tool use when tool use was available and useful,
- reporting guesses as findings,
- stopping after executor output without integrating it into the route state.
