# Pimperel

A single-file training companion, served as static HTML from GitHub Pages.
No dependencies, no build step, no backend, no account.

`index.html` is the whole application. `version.txt` carries the same
version string as the `VERSION` constant inside it: the page polls that
file and reloads itself when the two disagree, so an installed home-screen
shortcut never serves a stale build. The two must always be bumped
together.

## What it does

Measurements are never typed in. The app reads Apple Health Auto Export
archives directly — a dependency-free ZIP reader, hourly-to-daily
aggregation, workouts, and per-session heart-rate series — and everything
the watch records is shown read-only with its source. The daily form asks
only for what no export contains.

Each week it runs a review: the archive goes in, a structured analysis and
a fourteen-day plan come back, and applying the plan is a deliberate
second tap.

## What is not in this repository

No personal data of any kind. No measurements, no targets, no health
history, no doctrine, no API key. All of that lives in the browser's local
storage on the owner's device, and in the backups they keep themselves.
Export archives are git-ignored.

This is a hard rule, not a preference: the repository is public. Anything
that identifies a person or describes their health belongs on the device,
never in a commit — not in the source, not in a comment, not in a commit
message.

## Deploying

Pages is set to deploy from `main` at the repository root, through the
managed `pages build and deployment` workflow. That workflow has no
`workflow_dispatch` trigger, so it cannot be started by hand.

Observed since the history was rewritten: pushes made over an HTTP proxy
do not fire it. The commits arrive, `main` moves, and no build runs. A
commit created through the GitHub API fires it immediately, and the build
publishes the whole tree at that commit — including anything pushed
earlier by git.

So: push the work however you like, then finish with one small commit
through the API. Check the run before assuming the site moved, because a
push that lands silently looks exactly like a successful deploy.
