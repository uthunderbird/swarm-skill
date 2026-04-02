# Option H - Finalization

Use `H` when the process has clearly converged and stopping is justified.

## Preconditions

- the answer is stable,
- key uncertainties are resolved or explicitly bounded,
- another iteration is unlikely to materially improve the result.

## Output Shape

- compact readiness check,
- brief justification for stopping,
- final synthesis or recommendation,
- remaining uncertainties or risks if relevant,
- concrete next step when applicable.

If a durable artifact will be written, write it in the same response as `H`, after the readiness check and stopping justification are already established.

## Pre-Mortem Pass

Before writing H output, each expert states one way the current proposed answer could be wrong. The Moderator checks: does any pre-mortem identify a route not yet explored?

- If yes → defer H, open that route, run one more iteration.
- If no → proceed to finalization.

This adds three to five lines before H executes — it is not a separate option.

## Finalization Mode Check

Before writing H output (after the pre-mortem pass), determine which mode applies:

| Prior-check | Mode | Required output shape |
|-------------|------|----------------------|
| Unresolved competing routes entering H | **Best-route close** | State the chosen route + what was sacrificed from alternatives |
| Answer is incomplete for reasons that can't be resolved in this session | **Bounded-incomplete close** | State what is known, what isn't, and why the gap is permanent |
| Neither | **Convergent close** | Single answer with full supporting reasoning |

Producing a convergent-close output when the mode is actually best-route or bounded-incomplete is a finalization error.

## Compact Readiness Check

Before finalizing, verify explicitly that:
- enough information exists to answer the request usefully,
- key uncertainties are resolved or clearly bounded,
- the active route is stable enough that another iteration is unlikely to change the practical result.

If unresolved questions remain:
- state whether they were intentionally deferred,
- explain why that deferral is acceptable,
- and distinguish them from issues the swarm actually resolved.

## Quality Bar

- stopping is argued, not assumed,
- the answer reflects the actual route history,
- the readiness check is explicit rather than implicit,
- the final synthesis distinguishes established conclusions from downstream recommendations or implementation guesses,
- unresolved uncertainties are not hidden.

## Failure Modes

- finalizing immediately after a broad exploration round,
- skipping route closure logic,
- finalizing because the current answer merely sounds tidy,
- writing the artifact before finalization is justified,
- pretending stronger certainty than the process earned.
