# Before / After

These examples are about execution risk, not style. A rewrite is useful only when it makes a coding agent less likely to take the wrong action.

## Preserve behavior during a refactor

**Before**

> Refactor the parser and update tests as needed, but don't change behavior unless you have to.

**After**

> Refactor the parser. Preserve current behavior unless the refactor requires a behavior change. Update tests for any behavior you change.

The important part is the invariant: preserve behavior. The exception stays an exception.

## Make recovery branches explicit

**Before**

> If the cache is stale, clear it and retry, otherwise report the error if it still fails.

**After**

> If the cache is stale, clear it and retry. If that retry fails, report the error. If the cache is not stale, report the error.

`Otherwise` could attach to the stale-cache check or to the retry result. The rewrite names both branches.

## Separate investigation from permission to modify

**Before**

> Investigate the flaky test and fix it if the cause is obvious, otherwise report what you find before changing anything.

**After**

> Investigate the flaky test first. If the cause is obvious, fix it. If the cause is not obvious, report what you found and do not change code.

The rewrite makes the modification boundary explicit without adding a new requirement.

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
