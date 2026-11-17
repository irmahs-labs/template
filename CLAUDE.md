# CLAUDE.md

<!-- The sections down to "Checks before pushing" (the context graph and
the notes included) are the same in every irmahs-labs repo; change them in
irmahs-labs/template first. Replace the examples and the sections after it
for this app. -->

## Git branches

Always pull before making changes: run `git fetch origin` and start from the latest `origin/main` before the first edit.

- On a branch whose PR is open, bring it up to date with `origin/main` first
- On `main`, or on a branch whose PR is already merged, create a new branch from `origin/main` instead

Always name the branch after the feature or fix it contains, never a random or generated name.

- Format: `<type>/<feature-name>` in lowercase kebab-case
- Types: `feat`, `fix`, `chore`, `docs`, `refactor`
- Examples: `feat/contact-form`, `fix/dark-mode-contrast`, `docs/claude-md`
- If the session assigns a generic branch (for example `claude/<random-words>`), create a feature-named branch instead and push there

## Pull requests

- Never push to `main`. Every change goes in through a pull request.
- Open the PR and stop there: never merge it, not even when CI is green. Irma reviews and clicks merge.
- Deploys run on merge to `main`. Re-run a deploy only when Irma asks.

## The context graph and the notes

Irma's notes on every irmahs.dev app are in her Obsidian notes, the repo irmahs/my-obsidian-notes (checked out at `~/Dev/my-obsidian-notes`), under `Self Hosted/`.

- Before starting work, read `Self Hosted/Context Graph.md` from that repo's `origin/main`: how irmahs.dev and every subdomain fit together (the proxy, the account service, which app talks to which, where each keeps its data). Without a checkout, read it with `gh api repos/irmahs/my-obsidian-notes/contents/Self%20Hosted/Context%20Graph.md -H "Accept: application/vnd.github.raw"`.
- When a change alters what the app is or does, update the notes too:
  - `Apps.md`, the app's section;
  - `Technologies.md`, if it adds, removes or changes a technology;
  - `Context Graph.md`, if it changes a subdomain, a redirect, a link between apps, who asks whom (sign-in, admin checks, internal calls), or where data lives. Update both the graph and the table.
- The notes go in through their own pull request, like any other change: a branch from the notes repo's `origin/main`, never their `main`. The local checkout is often left on an old branch, so work in a `git worktree` of `origin/main` rather than touching it. Link the app's PR in the notes PR.

## Checks before pushing

```sh
npm run check      # Ultracite (oxlint + oxfmt); CI fails on it
npm run typecheck
npm test           # vitest
npm run build
```

The PostToolUse hook in `.claude/hooks/ultracite.sh` runs Ultracite and the typecheck on every file you edit.

## What this is

What the app is, where it runs (`<name>.irmahs.dev`), and what it is built with.

## Design

Apps use Cute Matcha's app look (the _Apps_ section of Irma's Cute Matcha design system), in both of its themes, with colours from its role tokens. Say here which parts of the app follow it and how.
