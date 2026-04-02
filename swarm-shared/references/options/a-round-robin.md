# Option A - Round-Robin Discussion

Use `A` when multiple perspectives are needed before narrowing.

## Best For

- broad problems,
- early route discovery,
- collecting competing interpretations,
- exposing what the team thinks the real problem is.

## Output Shape

- Moderator reasoning
- substantive expert takes
- explicit `Expert Questions` block when experts question other experts
- compact todo / route update
- next option selection

## Quality Bar

- experts should differ meaningfully,
- each take should sharpen route structure,
- each expert reply should be substantive rather than a one-line opinion,
- disagreement or tension should be visible when the evidence supports it,
- cross-expert questions should be collected explicitly when they arise,
- avoid fake diversity where everyone restates the same answer.

## Question Flow

When an `Expert Questions` list is non-empty:
- record who asked whom and the question,
- treat those questions as unresolved interaction debt,
- prefer an immediate `A1` follow-up round to resolve them before drifting to unrelated options.

## Generation Independence Discipline

When generating expert N's output, do not pre-frame specific claims from prior experts. Each expert produces their primary take as if they haven't read prior outputs. Violation: an expert output that opens with a restatement of a prior expert's specific claim without an explicit label.

When an expert has a direct response to a named prior claim, the output may be structured in two labeled sections:
1. *Independent take* — generated per the independence discipline above
2. *Response to [Expert N]* — explicit engagement with a named prior claim (permitted, not required)

The response section fires when a direct clash is worth surfacing; it is not a default wrapper for all experts.

## False-Diversity Flag

If two or more experts in an A round propose the same route (same proposed action or conclusion, different wording), the Moderator must:
1. Flag this as false diversity and name the overlap explicitly.
2. Compress the overlapping outputs into one route before proceeding.

A round with false diversity is valid — it is not re-run. Compression is required; continuation without it is a process violation.

## Lazy C Routing Note

If an A round produces ≥3 Expert Questions that share a common unresolved assumption (i.e., all questions depend on the same unanswered prior), the Moderator may use that shared assumption directly as the C subgroup topic — without separate topic formulation.

If no such clustering exists → route to standard A1.

## Failure Modes

- too many experts for a small problem,
- shallow opinions with no route consequences,
- unresolved expert-to-expert questions that vanish without follow-up,
- polite consensus that arrives before real clash,
- false diversity (same route, different words) allowed to persist without compression,
- using `A` repeatedly after route structure is already clear.
