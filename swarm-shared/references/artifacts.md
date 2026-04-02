# Artifacts

Load this file only when deciding whether to create or update a durable artifact.

## Default Rule

Artifacts are optional. Do not create them just to satisfy the process.

## Good Reasons To Create One

- the investigation is long-running,
- continuity across sessions matters,
- the task has SSOT implications,
- route tracking would otherwise be lost,
- or the output needs to be reproducible.

## Good Artifact Types

- route plans,
- synthesis notes,
- criticism ledgers,
- status anchors,
- reproducible audit outputs.

## Bad Reasons

- to prove the process happened,
- to duplicate the final answer,
- to mirror transient external state without need,
- or to create documents that nobody will reopen.

## Practical Rule

Create or update an artifact only if it will make the next session or next decision materially easier.

Artifact choice may be made before finalization, but the actual file write should normally happen only at `H`.

Write earlier only if:
- the user explicitly asked for a file during the current run,
- or the file itself is the direct task outcome and the Moderator makes that explicit.
