# hermes-skill-task-decomposition

Hermes skill that turns a clarified goal (with subgoals) into a parallel
**TaskTree** and a topologically-ordered **Plan** (DAG). Pure WHAT layer —
it never picks agents, profiles, or MCP servers.

Part of the [hermes-skills-collection](https://github.com/nnnet/hermes-skills-collection).

## What it does

- Decomposes a `goal.json` (output of `desire-to-goal`) into a `tasks_spec`
- Validates the spec: unique output names, no orphan/phantom edges, slug-cased names
- Builds a `TaskTree` + `Plan` using `chief-manager`'s graph dataclasses
- Supports a retry loop (EvoAgentX pattern) and an in-place **Repair** mode for broken trees

Runs in two modes: `self` (you decompose in your own context) or `subagent`
(delegate to a `task-decomposer` profile via Kanban).

## When to use

- After `desire-to-goal` produces a goal with non-empty subgoals
- Before `chief-manager` builds the capability matrix
- Standalone: when you need a validated DAG plan and don't care about agent assignment yet

Before decomposing from scratch, check `workflow-templates` for a matching pattern.

## Layout

- `SKILL.md` — full skill specification (load this in your agent context)
- `scripts/decomposer.py` — prompt builders, parsers, retry loop, builder
- `scripts/validator.py` — pre-build validation
- `references/prompts.md` — LLM prompt templates
- `references/patterns.md` — common DAG patterns
- `references/examples.md` — worked examples
- `references/repair-recipes.md` — Phase 5 in-place repair recipes

## License

See `LICENSE`.
