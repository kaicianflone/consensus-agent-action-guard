---
name: consensus-agent-action-guard
description: Pre-execution governance for high-risk agent actions. Uses persona-weighted consensus to decide ALLOW/BLOCK/REQUIRE_REWRITE before external or irreversible side effects occur, with board-native audit artifacts.
homepage: https://github.com/kaicianflone/consensus-agent-action-guard
source: https://github.com/kaicianflone/consensus-agent-action-guard
---

# consensus-agent-action-guard

`consensus-agent-action-guard` is the final safety gate before autonomous action execution.

## What this skill does

- evaluates proposed agent actions (risk, irreversibility, side effects)
- applies hard-block and weighted consensus logic
- returns one of: `ALLOW | BLOCK | REQUIRE_REWRITE`
- emits required follow-up actions (e.g., human confirmation)
- writes decision and persona updates to board artifacts

## Why this matters

Most catastrophic automation failures happen at execution time. This skill inserts explicit governance before side effects.

## Ecosystem role

Built on the same consensus stack as communication and merge guards, giving one policy language across agent operations.

## Typical usage

- gating destructive operations
- controlling external messaging/posting actions
- requiring human confirmation for irreversible high-risk tasks

## Quick start

```bash
node --import tsx run.js --input ./examples/input.json
```

## Tool-call integration

This skill is wired to the consensus-interact contract boundary (via shared consensus-guard-core wrappers where applicable):
- readBoardPolicy
- getLatestPersonaSet / getPersonaSet
- writeArtifact / writeDecision
- idempotent decision lookup

This keeps board orchestration standardized across skills.

## Invoke Contract

This skill exposes a canonical entrypoint:

- `invoke(input, opts?) -> Promise<OutputJson | ErrorJson>`

`invoke()` starts the guard flow, which then executes persona evaluation and consensus-interact-contract board operations (via shared guard-core wrappers where applicable).

## external_agent mode

Guards support two modes:
- `mode="persona"` (default): guard loads/generates persona_set and runs internal persona voting.
- `mode="external_agent"`: caller supplies `external_votes[]` from real agents; guard performs deterministic aggregation, policy checks, and board decision writes without requiring persona harness.
