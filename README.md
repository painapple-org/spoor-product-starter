# spoor-product-starter

Starting point for the **product repo** a Spoor instance manages (`SPOOR_REPO`).

Spoor itself lives in its own repo and its own checkout. This one holds the
thing being built: the code, and the two files that tell every Spoor session
how this particular product wants to be worked on. The two are separate on
purpose, and the distinction is load-bearing enough that it is worth stating
once here: `SPOOR_HOME` is the agent, `SPOOR_REPO` is the product.

## Why this repo exists at all rather than an empty one

A brand-new empty GitHub repo has no commits and therefore no `main` branch.
Spoor's pipeline needs one from the very first run: its per-issue sub-agents
work in `git worktree`s branched off `main`, and every change it ships goes
out as a pull request against `main`. So the target repo has to be
initialized, not merely created.

That is the whole requirement. Everything below is a skeleton for the two
documents Spoor reads, not a framework or an opinion about how to build
software.

## What to do with it

1. Create your product repo from this template.
2. Point `SPOOR_REPO` at its local checkout in the Spoor instance's `.env`.
3. Run the `spoor-init` skill in the Spoor checkout. It interviews you and
   fills in `CLAUDE.md` here, wires up `.claude/settings.json`, and sets the
   rest of `.env`.
4. Replace this README with a real one describing the actual product.

## Repo settings to check

- **`delete_branch_on_merge` enabled.** Spoor's review stage merges its own
  PRs and deliberately does not pass `--delete-branch` to `gh pr merge` (that
  flag makes the CLI fast-forward `main` in a local checkout, which can race
  a concurrent worktree sharing the same ref). The repo setting does the same
  job server-side, and without it merged branches accumulate indefinitely.
- **Nothing on the branch-protection side is required.** Spoor's convention
  of shipping through a branch and a PR is a convention, kept because it
  produces a clean revert point, not something a rule has to enforce.
