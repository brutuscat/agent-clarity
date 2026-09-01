---
name: agent-clarity
description: "Review or rewrite instructions for coding agents when wording is ambiguous, dense, or easy to execute in more than one way. Use for AGENTS.md rules, system prompts, tool descriptions, task handoffs, plans, validation criteria, and recovery instructions. Preserve meaning, uncertainty, constraints, identifiers, and technical terms. Prefer the smallest clear rewrite."
version: 1.0.0
---

# Agent Clarity

Use this skill to make instructions easier for coding agents to execute correctly.
It is a clarity pass, not a style guide. Keep natural prose where natural prose is better.

## Goals

- Preserve the author's intent, scope, constraints, and uncertainty.
- Make the actor, action, condition, order, and stop condition explicit when they matter.
- Use one stable term for one concept.
- Prefer the smallest rewrite that removes a real ambiguity.
- Keep project terminology, code identifiers, commands, paths, numbers, and API names exact.
- Leave text alone when it is already clear.

## Quality Rules

- Put a condition next to the action it controls.
- State the actor when ownership is unclear.
- Split independent instructions when combining them creates more than one execution path.
- Prefer direct verbs. Remove filler that does not change the instruction.
- Keep modality exact. `may`, `should`, `must`, `can`, and `will` are different requirements.
- Keep exceptions, fallback behavior, and failure behavior explicit.
- Do not rotate synonyms for the same concept inside one instruction set.
- Use lists for steps, independent constraints, or alternatives when prose hides the structure.
- Do not invent missing behavior. If the source is genuinely ambiguous, flag it instead of choosing an interpretation.
- Do not change code or technical syntax unless the user asks.

## Avoid Mechanical Rewrites

Do not impose fixed word counts, banned punctuation, forced simple tenses, or a controlled vocabulary.
Do not rewrite text only to make it shorter or flatter.
Do not remove useful technical detail or human voice when neither creates ambiguity.

## Process

1. Read for the intended outcome. Identify invariants and anything that must not change.
2. Check the actor, action, conditions, ordering, scope, modality, terminology, failure behavior, and stop conditions.
3. Rewrite only where a change reduces the risk of misexecution.
4. Read the result as the coding agent that must execute it. Ask whether two reasonable agents could take materially different actions from the text.
5. If they could, clarify further or flag the missing information.

## Output

By default, return the rewritten text only.

If the user asks for a review, show the ambiguity or risk, why it matters, and the smallest useful rewrite. Do not produce a rule-by-rule style audit unless the user asks for one.

If the source itself does not contain enough information to choose one interpretation safely, say what is ambiguous. Do not hide the ambiguity behind a confident rewrite.

## Boundaries

Use this skill for repository instructions, system or developer prompts, subagent instructions, tool descriptions, plans, task handoffs, validation criteria, recovery instructions, and coding documentation with operational steps.

Do not use it as a general prose polisher, a code formatter, or a complete prompt-engineering framework. It improves wording. It does not fix a bad technical decision.

## Examples

Before:

> Inspect the failing test and, if the cause is obvious, make the smallest fix; if it is not, report the evidence instead of changing code.

After:

> Inspect the failing test first. If the cause is obvious, make the smallest fix. If the cause is not obvious, report the evidence and do not change code.

Before:

> If the cache is stale, clear it before retrying the request, and if that retry fails report the error instead of retrying again.

After:

> If the cache is stale, clear it and retry the request. If that retry fails, report the error. Do not retry again.

More examples are in `examples/before-after.md`.
