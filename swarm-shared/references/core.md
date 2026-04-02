# Swarm Core

Load this file near the start of any nontrivial swarm, after Phase 1 and Phase 2 setup. It contains the protocol invariants that should not be duplicated across variants or option modules.

## Roles

### Moderator
- operates on the defined problem frame,
- chooses the next option,
- enforces process discipline,
- summarizes progress at checkpoints,
- decides when stopping is justified.

### Executor
- grounds uncertain claims with tools, files, or data,
- reports concrete findings,
- carries out bounded actions selected by the Moderator.
- may use the full tool surface available to the agent when that is the right way to execute the bounded task.

The Moderator decides. The Executor grounds.

## Hard Invariants

1. Do not skip the process once Swarm Mode or a Swarm variant is invoked.
2. Preserve the Moderator / Executor distinction.
3. Advance through explicit option choices.
4. Use tool grounding when it can discriminate among live routes.
5. Before each next decision, provide real Moderator reasoning that explains why that option is being chosen now.
6. Moderator reasoning should be substantive enough to show actual evaluation rather than post-hoc justification. For nontrivial choices, this usually means several sentences rather than a one-line transition.
7. For nontrivial investigations, distinguish:
   - `verified fact`
   - `bounded empirical result`
   - `working hypothesis`
   - `speculative explanation`
8. For multi-step explorations, classify major routes as:
   - `ACTIVE`
   - `DORMANT`
   - `CLOSED`
   - `SUPPORTING`
9. State route-level stop rules when a route may persist across iterations:
   - what counts as success,
   - what retires or closes the route,
   - what would reopen a dormant route.
10. Do not pivot away from the active route without a real discriminator, sharper scope, or new evidence.
11. Checkpoint honestly. A checkpoint should add a real state change, not just nicer wording.
12. Do not pre-plan a long option sequence before the current iteration has been executed and absorbed.
13. When a Swarm-family skill is invoked, visibly render the protocol. Do not perform the swarm off-screen and emit only conclusions, findings, or synthesis.
14. If `E` is chosen and real tools would materially help, do not emit pseudo-executor findings from reasoning alone. The Executor should make a bounded execution plan and then use the actual tools.
15. Each nontrivial iteration should materially advance at least one of:
   - route state,
   - evidence state,
   - decision state.
16. Do not treat a cleaner rendering of the same uncertainty as iteration progress unless the state of the investigation actually changed.

## Standard Header

Use a compact visible header like this:

```text
Phase 1: Problem Definition
- core problem
- scope / out of scope
- success criteria
- uncertainties / missing information

Phase 2: Expert Assembly
- team size
- role mix
- evidence boundary
```

The content of Phase 1 should come from `problem-definition.md`.
The content of Phase 2 should come from `expert-assembly.md`.

This header is part of the protocol output shape, not the primary guidance for how to perform those phases.
For invoked Swarm-family runs, Phase 1 and Phase 2 should normally be visible in the response rather than kept implicit.

## Lightweight Ledger

For medium and long investigations, keep a short running ledger:
- result type for major findings,
- route status for major routes,
- current success / retirement / reopen conditions for the active route.

Good places for this:
- `Open Items update`
- `Status Summary`
- `Checkpoint`

For longer runs, include a brief `Status Summary` every 4-5 iterations so unresolved questions and route priorities do not drift out of view.

## Open Items Lifecycle

Open Items is the tracking structure for all unresolved questions, missing information, competing interpretations, and decisions that need resolution across iterations. It is not a task queue — it tracks what needs to be *resolved*, not what needs to be *done*.

**Seven states:**

| State | Meaning | Review rule |
|-------|---------|-------------|
| `open` | Captured, not yet worked | Flag at compression gate if age ≥3 |
| `in-progress` | Current iteration actively addressing it | Must resolve or change state by end of iteration |
| `resolved` | Moderator named conclusion and closed it | Archived; may be cited in H |
| `blocked-user-owned` | Attempt made; missing info only the user can provide | Age 0: flag. Age 1: hard stop → Option B |
| `blocked-external` | Missing info the Executor can ground | Triggers Option E; does not block continuation |
| `deferred-in-scope` | Won't address this iteration; still relevant | Reviewed at every compression gate |
| `deferred-out-of-scope` | Deliberately closed this session | Not reviewed; surfaced in H (bounded-incomplete) if relevant |

**Age counter:** each item records the iteration opened. Age = current iteration − opening iteration.

**Authorship:** optional generally; mandatory for items from an Expert Questions block: `[from: Expert N → Expert M]`.

**Escalation rule — blocked-user-owned:**
- Age 0: flag in backlog scan, note in Moderator Reasoning.
- Age 1: hard stop — Option B mandatory before any other option. A blocked-user-owned item that ages without escalation is a process violation.

**Blocked-external** does not hard-stop the run. It opens an E-targeted route and continues.

**Deferred-in-scope vs. deferred-out-of-scope:** both require an explicit Moderator decision with a reason. Items cannot drift into deferred — they must be deliberately moved. Deferred-out-of-scope items are not reviewed at compression gates; deferred-in-scope items are.

Compression is allowed. Invisible protocol execution is not.

## Stop Discipline

Stopping is justified only when one of these is true:
- the process has clearly converged,
- a checkpoint reveals a real blocking uncertainty or external gate,
- critical missing information blocks progress,
- an external approval gate is truly blocking.

Do not claim resolution when the process has only produced a better question.
Do not write a durable artifact before justified finalization unless the user explicitly requested that write as part of the current task.
