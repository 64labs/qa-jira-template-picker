# qa-jira-template-picker

One page app to copy Jira templates for QA work.

Fill in your session context once (environment, browsers, initial steps) — it spreads across all templates instantly. Copy, paste into Jira, done.

## Features

- **Environment name + URL** → rendered as clickable Jira link markup `[staging|https://staging.site.com]`
- **Browser multi-select** — selected browsers listed in every template
- **Initial steps** — reusable steps prefix for bug/regression descriptions (e.g. common checkout flow steps)
- **Auto-save** — session state persists in localStorage, survives page reloads
- **Clear session** — one click to reset everything
- **Unfilled placeholders highlighted** — `{{env}}`, `{{browsers}}` stay visible so you never paste a half-empty template

## Usage

Open the page, fill the sidebar, hit Copy on any template.

Hosted version: `https://64labs.github.io/qa-jira-template-picker/`

## Editing templates

All templates and the browser list live in [`config.json`](./config.json) — edit it right on GitHub, no build step, no deploy. Changes go live on next page load.

Template format:

```json
{
  "id": "unique-id",
  "title": "Card title",
  "tag": "description | comment",
  "body": "Template text with {{env}}, {{browsers}}, {{steps}} placeholders"
}
```

Available placeholders:

| Placeholder | Replaced with |
|---|---|
| `{{env}}` | `[name\|url]` Jira link (or plain name/URL if only one is filled) |
| `{{browsers}}` | Comma-separated selected browsers |
| `{{steps}}` | Initial steps textarea content + newline (empty if not filled) |

## GitHub Pages setup

1. Settings → Pages
2. Source: **Deploy from a branch**
3. Branch: `main`, folder: `/ (root)`
4. Save — the page appears at `https://64labs.github.io/qa-jira-template-picker/` within a minute

## Local use

`index.html` also works opened directly as a file — it falls back to built-in default templates when `config.json` can't be fetched (browsers block `fetch` on `file://`). For the config to load locally, serve the folder: `npx serve` or `python3 -m http.server`.
