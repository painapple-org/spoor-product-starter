# CLAUDE.md

Auto-loaded by Claude Code for any session working in this repo. This is the
file every Spoor pipeline prompt means when it says "this deployment's own
conventions doc."

Right now it is a skeleton. The `spoor-init` skill fills it in from an
interview with this product's owner; each section below says what belongs in
it and what a wrong answer costs, so that the filled-in version is a real
decision rather than a default nobody chose.

Write it in the present tense, describing how things are. It is not a
changelog, and it is not a place to record that something used to be
different.

## The product

What this is, who it is for, and what it actually does. One or two
paragraphs. Enough that a session opening a file here knows what the file is
in service of.

## Where the facts live

Every fact has exactly one home; everything else names that home and goes and
reads it. A copied fact is indistinguishable from a true one right up until
it is wrong, and by then the copy is what gets acted on.

So: list the sources of truth for this codebase and what each one owns
(service topology, routing, schedules, design tokens, deployment). Name the
file or the constant, never its current value. A session that needs the value
reads it from the owner.

## Autonomy and the stop-and-ask list

The single most important section, and the one with no safe default.

Two things to write down:

- **What ships without asking.** For most deployments this is routine,
  reversible work: bug fixes, config maintenance, implementing a refined
  issue. The shape is branch, commit, push, open a PR, merge it. The PR is
  there to give a reviewable diff and a clean revert point, not to wait for a
  human.
- **What always stops and asks.** Anything genuinely destructive or hard to
  reverse. A starting list to accept, extend, or cut: force-push, deleting
  branches or volumes or backups, `git reset --hard` over someone else's
  work, rotating or revoking credentials, DNS and domain changes, editing
  live production data, spending money, and anything that commits this
  business to a third party.

Tighten or loosen both deliberately. Requiring sign-off before every merge is
a valid answer; so is carving out a specific category that may act
unsupervised. What is not valid is leaving it unstated, because then it gets
guessed at, once per session, differently each time.

## Git and process conventions

- Branch naming, commit message shape, and whether commits carry a
  process-attribution trailer.
- Never add AI attribution: no `Co-Authored-By`, no "generated with Claude",
  anywhere in a commit, PR description, or issue comment.
- Note the `gh pr merge --delete-branch` caveat if this repo is ever worked on
  from multiple worktrees at once (see this repo's README).

## Code style

Whatever is actually true here: language and framework conventions, naming,
testing expectations, how much abstraction is welcome. Two conventions worth
adopting on purpose rather than inheriting by accident:

- **No state that isn't real right now, in either direction.** No legacy
  compatibility code for something already gone, no placeholder or stub for
  something that does not exist yet. Git holds both directions.
- **A decision to remove something is not done until the code is gone.** The
  same pass that records "X is dead" deletes X, its config, and its
  references. A note records intent; the codebase is what the next reader
  believes.

## Failure behavior

How this product behaves when it cannot do its job. Quietly broken is worse
than a crash: it produces confusion with no handle to grab. Say where errors
are supposed to surface, and that swallowing an exception to keep going is
not an acceptable shape.

## Anything else a session should already know

Domain vocabulary, a product name that is spelled unusually, an external
system with a quirk, a person whose sign-off matters for a particular area.
Things that would otherwise be re-explained in every conversation.
