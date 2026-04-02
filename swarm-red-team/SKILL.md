---
name: swarm-red-team
description: Run the full Swarm Red Team critical-analysis process with Moderator/Executor roles, structured critique iterations, substantial-critique artifact defaults, and a required mechanism-audit pass when the target makes or strongly implies a meaningful mechanistic guarantee claim. Use when the user asks for red team, critique, adversarial review, or structured critical analysis.
allowed-tools: Read, Write, Edit, Bash, Glob, Grep
---

# Swarm Red Team

Use this skill when the user asks for adversarial critique, structured red-team review, or iterative critical analysis.

This file is the entrypoint for the critique variant. It reuses shared Swarm protocol modules and adds red-team-specific critique overlays.

## Purpose

Swarm Red Team is the critique-specialized variant of Swarm. It should remain domain-general while biasing toward failure discovery, mechanism testing, and actionable correction.

## Core Contract

- preserve shared Swarm discipline,
- critique first rather than brainstorm first,
- distinguish evidence-backed issues from weaker concerns,
- default to a durable criticism artifact for substantial critiques unless the user declines,
- run a mechanism audit when the target makes or strongly implies a meaningful guarantee claim about a process, schema, policy, or design.

Do not collapse the red-team process into findings-only output. Findings are outputs of visible critique iterations, not a substitute for them.

## Fast Start

1. Load `../swarm-shared/references/problem-definition.md`.
2. Load `../swarm-shared/references/expert-assembly.md`.
3. Load `../swarm-shared/references/core.md`.
4. Load `../swarm-shared/references/routing.md`.
5. Load `references/red-team-overrides.md`.
6. Load `references/mechanism-audit.md` when the target makes or strongly implies a meaningful mechanistic guarantee claim.
7. Load shared option module(s) as needed.
8. Load `../swarm-shared/references/canonicality.md` when source-of-truth or family-extension questions matter.

## Shared Modules

- Shared problem definition: `../swarm-shared/references/problem-definition.md`
- Shared core: `../swarm-shared/references/core.md`
- Shared routing: `../swarm-shared/references/routing.md`
- Shared canonicality: `../swarm-shared/references/canonicality.md`
- Shared options:
  - `../swarm-shared/references/options/a-round-robin.md`
  - `../swarm-shared/references/options/a1-expert-qa.md`
  - `../swarm-shared/references/options/b-clarifying-questions.md`
  - `../swarm-shared/references/options/c-subgroup.md`
  - `../swarm-shared/references/options/d-adjudication.md`
  - `../swarm-shared/references/options/x-cross-examination-debate.md`
  - `../swarm-shared/references/options/e-executor.md`
  - `../swarm-shared/references/options/g-checkpoint.md`
  - `../swarm-shared/references/options/h-finalization.md`

## Red-Team-Specific Modules

- `references/red-team-overrides.md`
  Critique-first rules, result typing, route handling, and artifact defaults.
- `references/mechanism-audit.md`
  Required audit pattern for meaningful mechanistic guarantee claims.
- `references/command.md`
  Canonical XML prompt-spec for the full red-team variant.

## Notes

- Red-team is a variant, not a separate option family.
- Keep the critique adversarial but useful; do not solve for the author unless the task explicitly asks for fixes after the critique.
