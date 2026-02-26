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
