# AI software factory starter for SHIP

Starter `ship.yml` files for an AI software factory on [SHIP](https://letsship.ai). SHIP takes each issue through a Planner, a Builder, your own CI, a Reviewer, a preview deploy and a Tester. A failed gate sends the work back to the Builder, and a person accepts the pull request at the end.

Each role runs the coding agent (harness) and the model that you set in `ship.yml`. The harnesses are `claude-code`, `codex`, `pi`, `kilo-code` and `open-code`, and inference bills to your own provider keys.

## Pick a starter

| File | What it sets |
| --- | --- |
| [`ship.yml`](ship.yml) | The platform defaults, written out: `claude-code` on Opus for every role |
| [`examples/codex-builder.ship.yml`](examples/codex-builder.ship.yml) | `codex` writes the code, and `claude-code` reviews it |
| [`examples/open-weight-builder.ship.yml`](examples/open-weight-builder.ship.yml) | The `pi` coding agent writes the code on `deepseek/deepseek-v4-flash` through OpenRouter |
| [`examples/strict-review.ship.yml`](examples/strict-review.ship.yml) | A person approves the plan, and the Reviewer rejects suggestions too |
| [`examples/short-retries.ship.yml`](examples/short-retries.ship.yml) | The mission comes back to a person after fewer retries |
| [`.ship/agents/reviewer.md`](.ship/agents/reviewer.md) | Extra review rules for your repository, added to SHIP's own |

## Use a starter

1. Copy a file to the root of your repository as `ship.yml`.
2. Commit it to your default branch.
3. Assign a Linear issue to SHIP, or comment `@SHIP` on a GitHub issue.

SHIP checks the file against its [JSON Schema](https://letsship.ai/schema/ship.yml.json). The first line of each starter points your editor at that schema, so you get completion and errors as you type. A file that fails the check loses all of its settings, and that line shows the error in your editor before you commit.

## Read the numbers behind the examples

In SHIP's [SWE-in-a-team study](https://letsship.ai/blog/swe-in-a-team), published on August 31, 2026, 13 builder configurations took the same 20 tickets through plan, build, CI, review, deploy and test. Each configuration ran each ticket once, and cost is API-equivalent spend for the whole mission.

| Builder | Resolved | Per resolved ticket |
| --- | --- | --- |
| `open-code` with `deepseek/deepseek-v4-flash` | 20 of 20 | $3.16 |
| `pi` with `deepseek/deepseek-v4-flash` | 20 of 20 | $3.36 |
| `codex` with `gpt-5.6-sol` | 20 of 20 | $3.83 |
| `claude-code` with `claude-sonnet-5` | 20 of 20 | $4.31 |
| `claude-code` with `claude-opus-5` | 20 of 20 | $5.48 |

The per-run data is public as a [CSV](https://letsship.ai/data/swe-in-a-team-per-task.csv), and the benchmark fixture is [letsship/ship-bench-app](https://github.com/letsship/ship-bench-app).

## Learn more

- [What is an AI software factory](https://letsship.ai/blog/what-is-an-ai-software-factory) explains the stages, the gates and the cost per accepted change.
- [The ship.yml schema](https://letsship.ai/docs/configuration/schema) lists every field.
- [Agent prompts](https://letsship.ai/docs/configuration/agent-prompts) shows how a role reads extra instructions from `.ship/agents/`.
