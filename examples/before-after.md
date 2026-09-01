# Before / After

These examples are about execution risk, not style. A rewrite is useful only when it makes a coding agent less likely to take the wrong action.

## Make a decision boundary explicit

**Before**

> Inspect the failing test and, if the cause is obvious, make the smallest fix; if it is not, report the evidence instead of changing code.

**After**

> Inspect the failing test first. If the cause is obvious, make the smallest fix. If the cause is not obvious, report the evidence and do not change code.

The rewrite keeps the same two branches and makes the modification boundary obvious.

## Make recovery order explicit

**Before**

> If the cache is stale, clear it before retrying the request, and if that retry fails report the error instead of retrying again.

**After**

> If the cache is stale, clear it and retry the request. If that retry fails, report the error. Do not retry again.

The sequence and stop condition are now hard to attach to the wrong action.

## Keep scope close to the action

**Before**

> Update the README and docs for the new config keys, but don't touch examples that are still valid.

**After**

> Document the new config keys in the README and docs. Leave existing examples unchanged when they are still valid.

The constraint now sits beside the thing it protects.

## Preserve modality

**Before**

> The migration should keep the old column for now, and we may remove it after the backfill.

**After**

> The migration should keep the old column for now. We may remove it after the backfill.

`Should` and `may` stay unchanged. Turning either one into `must` or `will` would change the instruction rather than clarify it.

## Keep one name for one thing

**Before**

> The worker reads the job from the queue. If the task is cancelled, the processor records the cancellation and stops.

**After**

> The worker reads the job from the queue. If the job is cancelled, the worker records the cancellation and stops.

This rewrite is correct only when `worker`, `processor`, `job`, and `task` really refer to the same two concepts. If that is not known from context, flag the terminology instead of merging it.

## Do not guess when the source is underspecified

**Before**

> Use the new parser when enabled and fall back to the legacy parser if it errors, but don't swallow errors from user input.

**Correct review**

> The fallback condition is ambiguous. The text does not say which parser errors trigger the legacy parser or whether invalid user input must bypass fallback. Define those cases before rewriting this as an executable rule.

A confident rewrite would have to invent an error taxonomy. Agent Clarity stops and exposes the missing decision instead.

## Leave clear instructions alone

**Input**

> Run `make test` after changing the parser. Do not merge if any parser test fails.

**Result**

> Run `make test` after changing the parser. Do not merge if any parser test fails.

Changing text is not the goal. Removing plausible misreadings is.
