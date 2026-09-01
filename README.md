# Agent Clarity

A small Agent Skill that rewrites coding-agent instructions so there is one obvious way to execute them.

## The problem

Coding agents are good at code and still easy to misdirect with vague prose. The failure is usually not grammar. It is a hidden condition, an unclear actor, unstable terminology, or wording that accidentally changes an option into a requirement.

Agent Clarity is a final pass for those interfaces. It keeps the technical meaning and removes the parts that make two reasonable agents do different things.

## Quick example

Before:

> Refactor the parser and update tests as needed, but don't change behavior unless you have to.

After:

> Refactor the parser. Preserve current behavior unless the refactor requires a behavior change. Update tests for any behavior you change.

The rewrite is not trying to sound simpler. It makes the invariant and the exception explicit.

## Install

With the Agent Skills CLI:

```bash
npx skills add brutuscat/asd-ste100-skill -a codex
```

Install it globally if you want it in every Codex project:

```bash
npx skills add brutuscat/asd-ste100-skill -g -a codex
```

The same skill also works with other Agent Skills-compatible coding agents. For example, replace `codex` with `claude-code`.

## Use it

Call it when wording is part of the interface between you and a coding agent, or between two agents.

```text
$agent-clarity review this AGENTS.md section. Preserve every constraint.

$agent-clarity rewrite this handoff so the execution order is unambiguous.

$agent-clarity tighten this tool description. Do not change its behavior or confidence level.
```

Use it after you know what you want to say. It is most useful as a review or rewrite pass, not as a substitute for thinking through the task.

## What it looks for

It checks whether the text makes clear who acts, what happens first, which condition controls which action, what is optional or required, and whether the same concept changes names halfway through.

It preserves technical terms, identifiers, paths, commands, numbers, exceptions, and uncertainty. If the source is genuinely ambiguous, it reports the ambiguity instead of inventing the missing behavior.

There are deliberately no fixed sentence lengths, banned punctuation marks, tense rules, or controlled vocabulary. Those rules can make technical prose more mechanical without making the instruction safer.

## Where it helps

Use it on `AGENTS.md`, system or developer instructions, subagent handoffs, tool descriptions, plans, validation criteria, recovery instructions, and operational sections of technical documentation.

Do not run normal prose through it by default. A README introduction, design discussion, or explanation can be natural English unless the wording itself creates an execution risk.

See [the examples](examples/before-after.md) for common coding-agent failures and minimal rewrites.

## What it doesn't do

- It does not make a bad technical decision correct.
- It does not replace tests, validation, or code review.
- It does not claim ASD-STE100 compliance.
- It does not rewrite clear text merely to make it shorter.

## Where this came from

This repository started as a fork of [danyuchn/asd-ste100-skill](https://github.com/danyuchn/asd-ste100-skill). The original applies ideas from [ASD-STE100 Simplified Technical English](https://www.asd-ste100.org/) to agent output.

This fork keeps the parts that transfer well to software agents: stable terminology, explicit actors and conditions, direct instructions, preserved modality, and refusal to invent missing facts. It drops the mechanical controlled-English rules because they are not the goal here.

The repository guidance also takes inspiration from [antirez/ds4 `AGENT.md`](https://github.com/antirez/ds4/blob/main/AGENT.md): state the goal, keep the rules small and operational, and make validation part of the instructions rather than adding a long methodology document.

## Contributing

Keep changes small. Prefer a concrete before/after case over another paragraph of theory. If a new rule does not prevent a plausible coding-agent mistake, it probably does not belong here.

See [`AGENTS.md`](AGENTS.md) for the maintenance rules used by coding agents working on this repository.

## License

MIT. See [LICENSE](LICENSE).
