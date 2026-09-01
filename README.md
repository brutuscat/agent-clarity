# Agent Clarity

A small Agent Skill for rewriting ambiguous coding-agent instructions into clear, executable English.

## The problem

Coding agents can still misread vague instructions. The problem is usually not grammar. It is a hidden condition, an unclear actor, inconsistent names, or wording that turns an option into a requirement.

Agent Clarity is a final pass for those instructions. It preserves technical meaning while removing wording that lets two reasonable agents take different actions.

## Quick example

Before:

> Inspect the failing test and, if the cause is obvious, make the smallest fix; if it is not, report the evidence instead of changing code.

After:

> Inspect the failing test first. If the cause is obvious, make the smallest fix. If the cause is not obvious, report the evidence and do not change code.

The rewrite does not add a workflow. It makes the existing decision boundary explicit.

## Install

With the [Agent Skills CLI](https://www.skills.sh/docs/cli):

```bash
npx skills add brutuscat/agent-clarity -a codex
```

Install it globally if you want it in every Codex project:

```bash
npx skills add brutuscat/agent-clarity -g -a codex
```

The same skill works with other Agent Skills-compatible coding agents. For example, replace `codex` with `claude-code`.

## Use it

Call it when wording is part of the interface between you and a coding agent, or between two agents.

```text
$agent-clarity review this AGENTS.md section. Preserve every constraint.

$agent-clarity rewrite this handoff so the execution order is unambiguous.

$agent-clarity tighten this tool description. Do not change its behavior or confidence level.
```

Use it after you know what you want to say. It works best as a review or rewrite pass, not as a substitute for thinking through the task.

## What it looks for

It checks whether the text makes clear who acts, what happens first, which condition controls which action, what is optional or required, and whether the same concept changes names halfway through.

It preserves technical terms, identifiers, paths, commands, numbers, exceptions, and uncertainty. If the source is genuinely ambiguous, it reports the ambiguity instead of inventing the missing behavior.

It also prefers simpler tense when the meaning stays the same. Compound tense stays when it carries useful state, order, or uncertainty.

There are deliberately no fixed sentence lengths, banned punctuation marks, or controlled vocabulary. Those rules can make technical prose more mechanical without making the instruction safer.

## Where it helps

Use it on `AGENTS.md`, system or developer instructions, subagent handoffs, tool descriptions, plans, validation criteria, recovery instructions, and operational sections of technical documentation.

Do not run normal prose through it by default. A README introduction, design discussion, or explanation can stay natural unless the wording itself creates an execution risk.

See [the examples](examples/before-after.md) for common coding-agent failures and minimal rewrites.

## What it doesn't do

- It does not make a bad technical decision correct.
- It does not replace tests, validation, or code review.
- It does not claim ASD-STE100 compliance.
- It does not rewrite clear text merely to make it shorter.

## Where this came from

This repository started as a fork of [danyuchn/asd-ste100-skill](https://github.com/danyuchn/asd-ste100-skill). The original applies ideas from [ASD-STE100 Simplified Technical English](https://www.asd-ste100.org/) to agent output.

Agent Clarity keeps the parts that transfer well to software agents: stable terminology, explicit actors and conditions, direct instructions, preserved modality, and refusal to invent missing facts. It drops the mechanical controlled-English rules because they are not the goal here.

The repository guidance also takes inspiration from [antirez/ds4 `AGENT.md`](https://github.com/antirez/ds4/blob/main/AGENT.md): state the goal, keep the rules small and operational, and make validation part of the instructions instead of adding a long methodology document.

## Contributing

Keep changes small. Prefer a concrete before/after case over another paragraph of theory. If a new rule does not prevent a plausible coding-agent mistake, it probably does not belong here.

See [`AGENTS.md`](AGENTS.md) for the maintenance rules used by coding agents working on this repository.

## License

MIT. See [LICENSE](LICENSE).
