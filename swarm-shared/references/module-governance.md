# Swarm Shared Module Governance

This file defines how to extend `swarm-shared` without creating drift or accidental overreach.

## Purpose

Use this file when deciding:
- whether a new rule belongs in `swarm-shared`,
- whether a new file should be added to the shared layer,
- or whether a change should stay inside a variant-specific overlay.

## Shared-vs-Variant Rule

Add a rule or module to `swarm-shared` only if all of the following are true:
- it applies across more than one Swarm-family variant,
- it changes shared workflow behavior rather than one variant's specialized objective,
- and it would create duplication or drift if kept separately in multiple variants.

Keep the change out of `swarm-shared` if any of the following are true:
- it changes only critique behavior,
- it changes only mini-mode compression behavior,
- it depends on one variant's specialized semantics,
- or it is mostly user-facing trigger phrasing for a specific entrypoint skill.

## New Module Test

Before adding a new shared module, check:
1. Does this content represent a distinct knowledge type?
2. Would it otherwise make an existing shared file materially harder to maintain?
3. Will it be reused often enough to justify another file?
4. Can it be described in one sentence in `swarm-shared/SKILL.md`?

If the answer to 2 or 3 is no, prefer extending an existing shared module instead.

## Preferred Growth Order

When adding capability, prefer this order:
1. extend an existing shared module,
2. add a new shared reference module,
3. add a variant-specific overlay,
4. add a new top-level variant skill only if user-facing trigger semantics truly differ.

Do not jump to a new top-level skill just because a new file would be inconvenient.

## Drift Prevention

When changing a shared behavior:
1. update the relevant file in `swarm-shared/references/`,
2. check whether affected variant overlays need adjustment,
3. check whether the relevant `command.md` XML spec should be synchronized,
4. update `swarm-shared/SKILL.md` if the reference map changed.

Do not silently patch only one variant if the rule is actually family-wide.

## Anti-Bloat Rule

Do not add a shared module just because the family might need it later.

Shared modules should be created for:
- repeated workflow logic,
- repeated decision logic,
- repeated configuration logic,
- or repeated governance logic.

They should not be created for:
- one-off examples,
- variant-local narration,
- speculative future structure,
- or cosmetic reorganization with no maintenance benefit.
