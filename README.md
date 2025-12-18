# Doyaken Prompt Library

A small web app for storing, finding, and reusing your AI prompts without turning your notes app into a junk drawer.

Prompts live in your GitHub repo (as Markdown). The app is just a better interface for capture, search, variants, and “most used”.

## What it does

* GitHub login (OAuth) and connect a repo + folder (default: `.prompts/`). ([GitHub Docs][1])
* Browse your prompt library with search, filters, and sort by “most used” or “recently used”.
* Open a prompt, fill in fields from front-matter, select a preset, copy the final compiled prompt.
* Add new prompts via an inbox flow that creates a PR in your repo (no direct pushes). ([GitHub Docs][2])
* Optional AI assist (tagging, suggesting inputs/variants) using an OpenAI key stored server-side.

## Why GitHub is the source of truth

GitHub gives you:

* version history (and rollbacks)
* sharing (private or public)
* portability (stop using the app, keep the prompts)

The app adds what GitHub doesn’t:

* fast retrieval (indexed search)
* usage-driven organisation (“most used”, “last used”)
* templates with structured inputs and presets
* low-friction capture (inbox + PR)

## Prompt format

Prompts are Markdown with YAML front-matter.

Example:

```md
---
id: code
variant: default
title: Code - build, fix, improve, review
tags: [code, qa]
inputs:
  - key: what
    label: What should I work on?
    type: textarea
---

Input: {{what}}

...prompt body...
```

Folder conventions (recommended):

```
.prompts/
  code/
    default.md
    short.md
  create/
    default.md
    short.md
  .inbox/
    <new prompts land here via PR>
```

## How the app works

1. **Connect repo**
   User signs in with GitHub OAuth and selects:

* repo (`owner/name`)
* default branch
* prompts folder (eg `.prompts/`)

Keep OAuth scopes minimal and explicit. ([GitHub Docs][3])

2. **Index prompts**
   The app pulls Markdown files from the folder, parses front-matter, and caches metadata for fast search.

3. **Use prompts**
   Open prompt - fill inputs - choose preset - compile placeholders - copy. A usage event is recorded for sorting.

4. **Add prompts safely**
   New prompts go to `.prompts/.inbox/…` via branch + commit + PR. ([GitHub Docs][2])

## Tech outline

* **Next.js** web app (server-side for anything involving tokens/secrets). Next.js environment variables are server-only unless explicitly exposed with `NEXT_PUBLIC_`, so don’t do that for secrets. ([Next.js][4])
* **Auth.js** (GitHub provider) for login and callbacks. ([authjs.dev][5])
* **Postgres** for cached prompt index + usage events + user settings.
* **GitHub REST API** for reading files, creating commits, and opening PRs. ([GitHub Docs][6])
* **Vercel** deploy, using sensitive environment variables for secrets. ([Vercel][7])

## Security and safety basics

* Treat the GitHub callback URL as security-critical (ownership of that URL is part of what stops token leakage). ([GitHub Docs][8])
* Request the minimum GitHub scopes you can get away with. ([GitHub Docs][3])
* Store secrets as Vercel sensitive env vars (and rotate when needed). ([Vercel][7])
* If you enable OpenAI features, never expose the API key client-side. ([OpenAI Help Center][9])

## Roadmap

* “Save preset” button that stores a named snapshot of inputs (and optionally updates front-matter presets)
* “Blueprints” folder: pre-filled prompts that capture a full discovery trail, not just a snippet
* Public sharing: publish selected prompts from a public repo/folder
* Lightweight leaderboard (optional, only if you care)

## Reference docs

```txt
Auth.js GitHub provider: https://authjs.dev/getting-started/providers/github
GitHub OAuth scopes: https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/scopes-for-oauth-apps
GitHub PR REST API: https://docs.github.com/en/rest/pulls
GitHub contents API: https://docs.github.com/en/rest/repos/contents
Vercel sensitive env vars: https://vercel.com/docs/environment-variables/sensitive-environment-variables
OpenAI API key safety: https://help.openai.com/en/articles/5112595-best-practices-for-api-key-safety
```

[1]: https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/authorizing-oauth-apps?utm_source=chatgpt.com "Authorizing OAuth apps"
[2]: https://docs.github.com/en/rest/pulls?utm_source=chatgpt.com "REST API endpoints for pull requests"
[3]: https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/scopes-for-oauth-apps?utm_source=chatgpt.com "Scopes for OAuth apps"
[4]: https://nextjs.org/docs/pages/guides/environment-variables?utm_source=chatgpt.com "Guides: Environment Variables"
[5]: https://authjs.dev/getting-started/providers/github?utm_source=chatgpt.com "GitHub Provider"
[6]: https://docs.github.com/en/rest/repos/contents?utm_source=chatgpt.com "REST API endpoints for repository contents"
[7]: https://vercel.com/docs/environment-variables/sensitive-environment-variables?utm_source=chatgpt.com "Sensitive environment variables"
[8]: https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/authenticating-to-the-rest-api-with-an-oauth-app?utm_source=chatgpt.com "Authenticating to the REST API with an OAuth app"
[9]: https://help.openai.com/en/articles/5112595-best-practices-for-api-key-safety?utm_source=chatgpt.com "Best Practices for API Key Safety | OpenAI Help Center"
