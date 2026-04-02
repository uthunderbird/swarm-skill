# Option B - Clarifying Questions

Use `B` when missing user information blocks safe continuation.

## Best For

- locking scope before the swarm commits to the wrong frame,
- resolving a critical ambiguity the environment cannot answer,
- confirming a user preference that materially changes route choice,
- pausing before the process would otherwise start guessing.

## Output Shape

- Moderator reasoning
- precise blocking uncertainty
- 1-3 focused user questions
- brief note on what will resume once the answer is known

## Quality Bar

- the missing information is genuinely user-owned,
- the question set is minimal and concrete,
- the swarm does not delegate strategic choice that it can already make,
- the blocking uncertainty is named explicitly rather than implied vaguely.

## Constraints

- ask only what materially changes the route,
- prefer one strong question over a list of soft prompts,
- do not use `B` to avoid doing available grounding or adjudication work,
- stop after `B` and wait for user input.

## Failure Modes

- asking for information that the environment can provide,
- asking broad open-ended questions instead of targeted blockers,
- using `B` as a menu of strategic choices the Moderator should make,
- piling multiple optional preferences into one blocking round.
