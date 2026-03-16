# Conformance Run Matrix (Proposed)

Date: 2026-03-16

## Goals

- Ensure that a team's Jam implementation is conformant to the M1 milestone.
- Define test programme that all teams have to satisfy with explicit parameters and acceptance criteria

## Test structure

- Teams have to satisfy different tests to cover as much as possible about the Jam specification.
- We use our own Fuzzer as part of this test programme as a best-effort tool to determine correct behaviour, but this is not the only test.
- The test programme is divided in different lanes and teams have to pass all of them.

- Lanes:
    * L1 -- Known Test Vectors: run implementation against all published and well-known test vectors.
    * L2 -- Mutations: testing happy-path import and mutation/error handling, without Safrole.
        - L2a -- Tiny profile (1M steps, 5 work items)
        - L2b -- Full profile (10K steps, 16 work items)
    * L3 -- Safrole: exercising Safrole with slot-skipping, no mutations.
        - L3a -- Tiny profile (10K steps)
        - L3b -- Full profile (10K steps)

## L1 -- Known Test Vectors

### Acceptance Criteria

- 100% pass of required known vectors.
- Any mismatch is a hard conformance failure.
- Self-assessed by the implementor; no explicit assessment performed during evaluation.

## L2 -- Mutations

Testing both happy-path import and mutation/error handling, without Safrole.

### L2a -- Tiny

| Parameter | Value |
|-----------|-------|
| jam_profile | full |
| profile | full |
| fuzzy_profile | full |
| max_mutations | 5 |
| mutation_ratio | 0.1 |
| max_work_items | 5 |
| max_steps | 1000000 |
| safrole | false |
| skip_slots | false |
| seeds | 10 random |

### L2b -- Full

| Parameter | Value |
|-----------|-------|
| jam_profile | full |
| profile | full |
| fuzzy_profile | full |
| max_mutations | 5 |
| mutation_ratio | 0.1 |
| max_work_items | 16 |
| max_steps | 10000 |
| safrole | false |
| skip_slots | false |
| seeds | 10 random |

### Acceptance Criteria (L2a/L2b)

- Expected state root matches target state root on every step.
- Session reaches `max_steps`.

## L3 -- Safrole

Two sub-runs escalating from minimal to full profiles. Both enable `skip_slots` alongside `safrole`.

### L3a -- Tiny

| Parameter | Value |
|-----------|-------|
| jam_profile | tiny |
| profile | empty |
| fuzzy_profile | empty |
| safrole | true |
| max_mutations | 0 (forced) |
| mutation_ratio | 0.0 |
| max_work_items | 0 |
| max_steps | 10000 |
| skip_slots | true |
| seeds | 10 random |

### L3b -- Full

| Parameter | Value |
|-----------|-------|
| jam_profile | full |
| profile | full |
| fuzzy_profile | full |
| safrole | true |
| max_mutations | 0 (forced) |
| mutation_ratio | 0.0 |
| max_work_items | 5 |
| max_steps | 10000 |
| skip_slots | true |
| seeds | 10 random |

### Acceptance Criteria (L3a/L3b)

- Expected state root matches target state root on every step.
- Session reaches `max_steps`.

## Final Acceptance

After all test lanes pass, two additional steps are required before complete acceptance:

1. Fellowship code review
2. Final interview

## References

- JAM tiny profile: https://docs.jamcha.in/basics/chain-spec/tiny
- JAM full profile: https://docs.jamcha.in/basics/chain-spec/full
