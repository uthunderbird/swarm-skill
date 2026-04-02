---
name: swarm-shared
description: Shared protocol package for the Swarm skill family. Contains common references for core rules, routing, expert assembly, artifacts, and option modules used by the Swarm variants.
---

# Swarm Shared

This skill holds the shared protocol layer reused by:
- `swarm-mode`
- `swarm-red-team`
- `swarm-iterate`

## Purpose

`swarm-shared` is the single shared home for:
- setup guidance,
- core protocol invariants,
- routing heuristics,
- artifact guidance,
- configuration guidance,
- option modules reused across variants,
- family-level canonicality policy.

## Contract

- Variants should reference shared modules here instead of copying them into each skill.
- New family-wide protocol rules should be added here unless they are variant-specific.
- User-facing trigger semantics belong in the variant entrypoint skills, not here.
- If a rule changes only critique behavior, mini compression behavior, or another variant-specific behavior, keep it out of `swarm-shared`.

## Reference Map

### Setup

- `references/problem-definition.md`
  Phase 1 framing of the problem.
- `references/expert-assembly.md`
  Phase 2 team construction and evidence boundary.

### Core Protocol

- `references/core.md`
  Shared invariants, ledger discipline, and protocol shape.
- `references/routing.md`
  Post-setup option selection and route movement.
- `references/artifacts.md`
  When durable artifacts help and when they are noise.

### Configuration

- `references/configuration.md`
  Index and cheatsheet for Swarm tuning.
- `references/configuration-axes.md`
  Axis definitions.
- `references/configuration-mappings.md`
  Behavior mappings from axes to protocol decisions.
- `references/configuration-presets.md`
  Workflow presets and preset selection heuristics.
- `references/configuration-conditions.md`
  Trigger-style condition rules.

### Governance

- `references/canonicality.md`
  Family-level source-of-truth and extension policy.
- `references/module-governance.md`
  Rules for deciding when new logic belongs in the shared layer versus a variant.

### Option Modules

- `references/options/a-round-robin.md`
- `references/options/a1-expert-qa.md`
- `references/options/b-clarifying-questions.md`
- `references/options/c-subgroup.md`
- `references/options/d-adjudication.md`
- `references/options/x-cross-examination-debate.md`
- `references/options/e-executor.md`
- `references/options/g-checkpoint.md`
- `references/options/h-finalization.md`

## Notes

- If the family grows, prefer extending shared references here before creating new top-level skills.
