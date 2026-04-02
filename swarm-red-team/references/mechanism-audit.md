# Mechanism Audit

Load this file when the target claims or strongly implies that a process, schema, model, protocol, or design guarantees something important.

## Purpose

Test whether the target's stated mechanism actually delivers the claimed or strongly implied guarantee.

## Required Questions

1. What does the target explicitly promise?
2. What does the mechanism actually guarantee?
3. Where does the stronger reading fail?
4. What is the minimal fix set?

## Minimal Fix Set

- `P0`: required fixes without which the guarantee claim should not stand.
- `P1`: strengthening fixes that improve robustness but are not strictly required for the weaker claim.

## Quality Bar

- Separate promise from guarantee.
- Point to the exact missing constraints, steps, fields, assumptions, or enforcement layer.
- Keep the audit domain-general; avoid domain-specific ritual unless the target itself requires it.
