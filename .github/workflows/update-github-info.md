---
name: update-github-info
description: Refresh Mona's GitHub Info page with useful updates from the GitHub Blog and Changelog.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
engine:
  id: copilot
  copilot-sdk: true
tools:
  edit: true
  web-fetch: {}
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    max: 1
    draft: false
    allowed-files:
      - site/content/github-info.md
---

Read `notes/mona-notes.md` first. Then use web fetch to read both:

- https://github.blog/latest/
- https://github.blog/changelog/

Use only verifiable, recent information from those official sources to decide
whether `site/content/github-info.md` needs an update. Keep any additions short,
practical, and useful to developers, follow Mona's editorial notes, and include
a source link for every change based on the Blog or Changelog. Do not invent
details or make unrelated edits.

If there is a worthwhile, supported update, edit only
`site/content/github-info.md` and use the `create-pull-request` safe output to
open one pull request describing the changes and sources for Mona to review.
Do not write directly to the default branch. If there is no worthwhile update,
use `noop` with a brief reason instead of opening an empty pull request. If
either source cannot be fetched or verified, stop without making changes or
opening a pull request.
