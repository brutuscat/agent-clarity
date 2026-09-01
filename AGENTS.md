# Agent Notes

This repository contains `agent-clarity`, a small Agent Skill for making coding-agent instructions easier to execute correctly. It is not an ASD-STE100 implementation. Keep the repository small, readable, and useful across coding agents.

## Goals

- Keep `SKILL.md` focused on instruction clarity for software-engineering agents.
- Preserve meaning before improving wording. Never trade a constraint, exception, or uncertainty for a cleaner sentence.
- Prefer the smallest rewrite that removes a plausible execution error.
- Keep the skill useful across Codex, Claude Code, and other Agent Skills-compatible coding agents.
- Keep the repository dependency-free unless code becomes necessary for a real use case.

## Quality Rules

- Write for humans first. Use plain present-tense prose and concrete examples.
- Prefer an example over a paragraph of theory when both explain the same thing.
- Every paragraph must earn its place. Delete or combine text that repeats an idea.
- Do not reintroduce fixed sentence limits, banned punctuation, tense rules, or controlled vocabulary.
- Keep one stable term for one concept inside operational instructions, but do not make normal prose mechanical.
- Preserve identifiers, commands, paths, numbers, modality, and technical terminology exactly when rewriting examples.
- Do not invent behavior to make an ambiguous example look complete. Show the ambiguity instead.
- Avoid marketing language, keyword stuffing, and claims without evidence.

## Layout

- `SKILL.md`: the behavior loaded by an agent.
- `README.md`: what the skill solves, how to install it, and how to use it.
- `examples/before-after.md`: concrete coding-agent cases.
- `LICENSE`: project license.

Do not add another document when one of these files can explain the idea clearly.

## Testing

There is no runtime code. Validate changes against behavior instead.

For every significant change:

1. Test a vague coding instruction and verify that the rewrite removes a real ambiguity.
2. Verify that `may`, `should`, `must`, `can`, and `will` keep their original strength.
3. Test an underspecified instruction and verify that the skill flags the missing decision instead of guessing.
4. Test an already-clear instruction and verify that the skill leaves it alone.
5. Read the README as a first-time user. Installation and first use must be obvious without reading another file.
