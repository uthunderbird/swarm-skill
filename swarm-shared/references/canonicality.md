# Swarm Family Canonicality

This file defines the canonicality policy for the Swarm skill family.

## Scope

The family has two canonical layers with different jobs.

### 1. Workflow Canon

The canonical source for human-readable workflow semantics is:
- variant `SKILL.md` entrypoints,
- shared protocol references in `swarm-shared/references/`,
- variant-specific overlay references.

This layer defines:
- how the process should be run,
- what is shared vs variant-specific,
- how routing works,
- how options are used in practice,
- and how maintainers should extend the family.

When there is a workflow question, this layer wins.

### 2. XML Prompt-Spec Canon

The canonical source for XML prompt-spec serialization is:
- each variant's `references/command.md`.

This layer defines:
- XML schema representation,
- XML-specific protocol contract details,
- serialization examples,
- and any XML-facing compliance structure.

When there is an XML serialization question, this layer wins.

## Maintenance Rules

- Do not treat `command.md` as the primary human workflow guide.
- Do not duplicate shared protocol prose inside variant `command.md` files unless the XML spec genuinely requires it.
- When changing shared workflow behavior, update `swarm-shared/references/` first and then update affected XML prompt-spec files if needed.
- When changing only XML serialization details, update the relevant `command.md` without rewriting the shared workflow layer.
- If the two layers drift, resolve the inconsistency explicitly instead of silently treating both as equal canon.

## Variant Boundary

- Top-level skills correspond to user-facing variants.
- Option modules are internal shared protocol modules, not top-level skills.
- Variant-specific overlays should stay local to the variant unless reused by multiple variants.

## Extension Rule

Before adding a new top-level Swarm-family skill, check:
1. Is it a real user-facing intent or only an internal protocol step?
2. Can it be represented as an overlay on shared protocol modules?
3. Does it require new trigger semantics?

If the answer to 1 or 3 is no, it probably should not be a top-level skill.
