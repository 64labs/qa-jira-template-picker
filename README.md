# qa-jira-template-picker

One page app to copy Jira templates for QA work.

Templates are copied as **rich HTML with Atlassian editor panels** — paste into a Jira description or comment and the colored panels, tables and lists appear natively. Fill in your session context once (environment, browsers, initial steps) and it spreads across the relevant templates.

Hosted version: `https://64labs.github.io/qa-jira-template-picker/`

## Templates

- **Bug**: Bug report, Multi bug, Bug acceptance, Bug reopen
- **Story**: Story acceptance
- **QA review**: No questions, Tests linked, Tests linked (Asics ZA), QA notes, Questions raised

## Session context

- **Environment name + URL** → inserted into the Environment column of acceptance/reopen tables as a clickable link (plain text if only one field is filled)
- **Browsers multi-select** → comma-separated list in the Browsers column
- **Initial steps** (optional) → prepended to *Steps to reproduce* in Bug report / Multi bug (e.g. a common checkout flow)
- **Auto-save** — session state persists in localStorage, survives page reloads
- **Clear session** — one click to reset everything
- **Unfilled placeholders highlighted** — `{{env}}` / `{{browsers}}` stay visible in the preview so you never paste a half-empty template

## Editing the browser list

The browser list lives in [`config.json`](./config.json) — edit it right on GitHub, no build step, no deploy. Changes go live on next page load.

Templates themselves are rich Atlassian HTML and live in `index.html` (`templates` object in the script).

## GitHub Pages setup

1. Settings → Pages
2. Source: **Deploy from a branch**
3. Branch: `main`, folder: `/ (root)`
4. Save — the page appears at `https://64labs.github.io/qa-jira-template-picker/` within a minute

## Local use

`index.html` also works opened directly as a file — it falls back to the built-in browser list when `config.json` can't be fetched (browsers block `fetch` on `file://`). For the config to load locally, serve the folder: `npx serve` or `python3 -m http.server`.
