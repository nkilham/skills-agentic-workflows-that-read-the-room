---
name: Update GitHub Info
description: Refreshes Mona's GitHub info content from recent GitHub Blog and Changelog updates and opens a review pull request.
on:
  workflow_dispatch:
  schedule: daily
permissions:
  contents: read
  issues: read
  pull-requests: read
engine: copilot
strict: true
network:
  allowed:
    - defaults
    - github
    - github.com
    - awesome-copilot.github.com
tools:
  web-fetch:
  edit:
safe-outputs:
  create-pull-request:
    max: 1
    title-prefix: "[mona] "
    allowed-files:
      - site/content/github-info.md
    protected-files: blocked
    if-no-changes: ignore
  noop:
timeout-minutes: 20
---

# Update GitHub Info

You maintain Mona's GitHub Info page. Refresh the content with concise, practical GitHub updates and open a pull request for Mona to review.

## Required Research

1. Read `notes/mona-notes.md` first and follow its guidance.
2. Use `web-fetch` to fetch `https://github.blog/latest/`.
3. Use `web-fetch` to fetch `https://github.blog/changelog/`.
4. Use `web-fetch` to fetch `https://awesome-copilot.github.com/workflows/`.
5. Read `site/content/github-info.md` before editing so the update fits the existing style.

## Update Rules

- Update only `site/content/github-info.md`.
- Keep summaries short, practical, and useful for developers learning GitHub faster.
- Include or refresh a `## Latest GitHub Updates` section.
- Include at least one concise update sourced from the GitHub Blog, GitHub Changelog, or Awesome Copilot workflows (https://awesome-copilot.github.com/workflows/).
- Mention the source for each new update.
- Avoid broad rewrites unless the existing section is stale or duplicated.

## Pull Request

- Do not write directly to `main`.
- After editing, use the `create_pull_request` safe-output tool to open a pull request for Mona to review.
- Use a clear PR title and a brief body summarizing the sources checked and the content updated.
- If there are no useful updates to make, use `noop` with a concise explanation instead of opening a pull request.