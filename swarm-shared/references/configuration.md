# Swarm Configuration

Load this file when the task is substantial enough that Swarm behavior should be tuned rather than run with default assumptions.

## Purpose

This module is the index and cheatsheet for Swarm parameterization.

Parameterization should be based on task demands, not on subject labels like "biology" or "product" alone.

## Quick Cheatsheet

Swarm tuning is organized around six demand axes:
- rigor / stakes
- grounding need
- creativity need
- problem ambiguity
- route branching budget
- closure strictness

## Practical Usage Order

1. Choose a workflow preset if one clearly fits.
2. Override one or two axes if needed.
3. Use full custom tuning only for unusually mixed or high-stakes problems.

## Module Map

- `configuration-axes.md`
  Core axis definitions and what each axis means.
- `configuration-mappings.md`
  How the axes influence team shape, grounding posture, branching, closure, and persona mode.
- `configuration-presets.md`
  Workflow presets, preset selection heuristics, and when overrides are worth it.
- `configuration-conditions.md`
  Required / recommended / optional trigger rules for setup, topology, grounding, branching, persona mode, closure, snapshots, and artifacts.

## Notes

- Prefer presets over full manual tuning.
- Prefer trigger-style conditions over rigid deterministic mappings.
- Do not add domain-specific variants here unless repeated usage proves they are really needed.
