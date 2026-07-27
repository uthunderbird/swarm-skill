# swarm-skill

Swarm-family skills packaged as an `Agent Skills` repository for compatible
agent clients.

**What you get.** Point your agent at a hard, open question — a plan, an
architecture decision, a design you are not sure about — and instead of one
confident answer you get a structured multi-expert pass over it: the angles you
did not think of, the objections your idea has to survive, and a document you
can defend. Two of the skills go further and run adversarial rounds until the
idea either crystallizes or visibly collapses.

> Warning
> Use these prompts with `effort=low`, or `none` when that option is
> available. Higher effort usually does not improve quality here and can
> sometimes make the result worse.

## Motivation

These skills are for cases where you want an LLM agent to spend one pass on a
large, difficult, open-ended question and examine it from many different
angles.

The goal is not just to get a short answer. The goal is to make the agent
generate a large amount of explicit context for both itself and for you, so
that the next decision can be made on top of a much richer map of the problem.

This is useful when:

- the question does not have one obvious correct answer
- the problem is broad, ambiguous, or poorly framed
- you want structured exploration before committing to a plan
- you want a better decision, not just a faster one

## Included skills

- `swarm-mode`
  - full multi-expert problem-solving workflow
- `swarm-red-team`
  - critique-first adversarial variant
- `swarm-iterate`
  - iterative critique-and-repair wrapper
- `grill-me-well-done`
  - human-in-the-loop crucible: interview, deepen, then attack until the idea
    crystallizes or dies
- `polish`
  - convergence loop that hardens a finished document to a defined bar
- `swarm-shared`
  - shared protocol package used by the Swarm skills

## Which skill to choose

- `swarm-mode`
  - use for open exploration, planning, decomposition, brainstorming, and
    difficult questions that need a broad multi-angle pass
- `swarm-red-team`
  - use when you want critique first: stress-testing a plan, argument, design,
    proposal, or document for weaknesses, risks, and unsupported claims
- `swarm-iterate`
  - use when one pass is not enough and you want repeated critique-and-repair
    rounds on the same document or artifact
- `grill-me-well-done`
  - use when the idea is still mostly in your head and you want to be
    interviewed out of it: the skill grills you round after round, builds the
    document from your answers, then attacks it until it either crystallizes or
    dies. The most expensive skill here — it announces its cost before starting
- `polish`
  - use when the document already exists and is finished: it runs cold,
    no-parent-context critique rounds from rotating angles and repairs every
    must-fix and should-fix finding until a fresh cold reader finds nothing left

The three hardening skills differ in what they assume you already have.
`swarm-iterate` improves openly, `polish` converges a finished draft to a bar,
and `grill-me-well-done` starts before the draft exists.

## Format

Each skill lives in its own directory and uses the standard `Agent Skills`
layout:

- `SKILL.md`
  - required entrypoint with YAML frontmatter and instructions
- `references/`
  - optional detailed reference material
- `agents/`
  - optional agent-specific support material

The repository keeps shared Swarm protocol references linked via relative paths.

## How to use

Ask the swarm an open question: a question without a single deterministic
answer.

Good use cases:

- building a plan under specific constraints
- brainstorming ideas
- creating or polishing a product or technical vision
- deep decomposition of a large problem
- understanding what to do next in a project
- getting a contextual breakdown of an area you do not understand well yet
- exploring a hard practical question such as:
  `Which CI/CD best practices fit my project best, and why?`

Bad use cases:

- questions with a short factual answer
- tasks that are already well specified and mostly mechanical
- simple edits where you already know what to change
- situations where speed matters more than breadth
- requests where a long exploratory answer would be noise rather than leverage

You can also use it for difficult general questions that genuinely benefit from
multi-angle analysis rather than one-shot advice.

Typical prompts look like:

- `Use $swarm-mode to help me decide how to structure CI/CD for my project.`
- `Use $swarm-mode to brainstorm product directions for this tool under these constraints.`
- `Use $swarm-mode to figure out what we should do next in this project.`
- `Use $swarm-mode to deeply decompose this architecture question before recommending a plan.`

## What you get back

The result is usually a very large body of text.

In practice:

- Anthropic models often produce the largest and, subjectively, the most
  useful wide-angle explorations
- OpenAI models usually produce a drier, more compact, and less expansive
  answer
- Gemini is best treated as an idea generator for unusual angles that should
  then be checked carefully; with this style of prompting it is more prone to
  fast unsupported conclusions
- these prompts are best used with `effort=low`, or `none` when that option is
  available; higher effort usually does not improve quality here and can
  sometimes make the result worse

The first few times, it can be useful to read the full output. After a while,
you may find that reading just the final answer is enough unless you want to
inspect how the context was built.

## Notes

- `swarm-shared` is a shared support skill used by the Swarm variants
- if you publish this repository, keep the skill directory names aligned with
  the `name:` field in each `SKILL.md`
- support for fields such as `allowed-tools` depends on the client
- `grill-me-well-done` and `polish` invoke `swarm-mode` and `swarm-red-team` as
  subagents. Their prompt templates carry `/absolute/path/to/<skill>`
  placeholders — replace them with the real install paths on your machine
- `grill-me-well-done` is named to avoid collision with the unrelated and more
  common `grill-me` skill name

## License

MIT.

## Who builds this

Built by Daniyar Supiyev. I consult on AI agent systems — building them, and
fixing the ones that misbehave in production — at
[Forbidden Fundamentals](https://forbiddenfundamentals.com).
