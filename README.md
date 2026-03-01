# consensus-agent-action-guard

Pre-execution governance for high-risk autonomous actions.

`consensus-agent-action-guard` evaluates proposed actions before side effects happen and returns:

- `ALLOW`
- `BLOCK`
- `REQUIRE_REWRITE`

## Best use cases

Use this guard when an agent is about to perform actions that are:

- irreversible,
- externally visible,
- high-risk,
- or operationally sensitive.

Examples: destructive operations, external posting/messaging, privileged automation steps.

## Core capabilities

- strict schema validation (reject unknown fields)
- deterministic policy aggregation through `consensus-guard-core`
- persona-weighted voting (or external vote ingestion)
- idempotent retries via stable request hashing
- board-native audit artifacts for replayability

## Quick start

```bash
npm i
node --import tsx run.js --input ./examples/input.json
```

## Decision model

The guard combines:

1. hard-block flag detection,
2. weighted vote aggregation,
3. policy thresholding,
4. explicit required follow-up actions.

This allows consistent governance under automation pressure.

## Tool-call alignment

This skill follows the shared consensus tool boundary for board reads/writes and idempotency lookups, keeping orchestration compatible with the broader guard family.

## Test

```bash
npm test
```

## Continuous improvement

See `AI-SELF-IMPROVEMENT.md` for quality loops and refinement strategy.
