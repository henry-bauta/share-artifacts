---
name: publish
description: >
  Publish and share work as a hosted web page anyone can open in a browser.
  Use when the user says "share this", "publish this", "deploy this",
  "host this", "make this a website", "send this to someone", "put this online",
  "make a shareable link", "share this artifact", "publish artifact", or wants to
  turn a dashboard, visualization, report, app, or HTML page into a live URL.
  Also use when the user asks "how do I share this" or wants to give someone
  access to something they built.
---

# Publish and Share

Turn the user's work into a live, shareable web page hosted on Bauta.

## Before you start

Confirm Bauta is connected. If its tools are not available, tell the user:

> To publish artifacts, connect Bauta first. Go to Settings > Connectors and add Bauta, or visit claude.ai/directory/connectors/bauta.

If already connected, proceed.

## Workflow

### 1. Identify what to publish

Determine what the user wants to share. Supported content:

- **HTML** — any HTML page, served as-is
- **React / JSX** — compiled at publish time, no build step needed
- **Dashboards and visualizations** — charts, data tables, interactive widgets
- **Reports** — styled documents, presentations, summaries

If the content is not HTML or JSX, offer to wrap it in a styled HTML page first.

### 2. Deploy

Call `deploy_artifact` with:

- `title` — a descriptive title for the artifact
- `source_code` — the HTML or JSX source
- `content_type` — `"html"` or `"react"`

The artifact deploys immediately and returns a URL. The default sharing mode is **unlisted** (only people with the link can view).

Tell the user the URL and explain that it's currently unlisted — only people with the exact link can open it.

### 3. Ask about sharing

After deploying, ask how the user wants to share:

- **Send the link** — the unlisted URL is already shareable. Good for quick sharing.
- **Email invite** — use `share_via_email` to send a branded invite email to specific people.
- **Make public** — use `set_sharing` with mode `public` so anyone with the URL can view without a token.
- **Password protect** — use `set_sharing` with mode `password` for an extra layer of access control.
- **Keep private** — use `set_sharing` with mode `private` to lock it down completely.

Default to suggesting the simplest option that fits the situation. If the user names a person or email, go straight to `share_via_email`.

### 4. Confirm

Summarize what was published and how it's shared. Include:

- The live URL
- Who can access it
- How to update it later ("just ask me to update your artifact")

## Updating an existing artifact

If the user says "update this" or "push a new version" and has previously published:

1. Call `list_artifacts` to find the existing artifact
2. Call `update_artifact` with the artifact ID and new source code
3. Confirm the update is live

## Quick-share shortcut

When the user says something like "share this with anna@example.com" and there's an artifact in context:

1. Deploy with `deploy_artifact`
2. Immediately call `share_via_email` with the recipient
3. Report: "Published and sent to anna@example.com"

No extra questions needed — the intent is clear.

## Tips

- Artifacts are **unlisted by default** — the URL alone isn't guessable, so it's safe to share without changing the mode.
- Use `ephemeral: true` in `deploy_artifact` for temporary content that should auto-expire.
- If the user wants a custom URL (like `team.bauta.app/dashboard`), explain that custom subdomains require a paid plan and guide them to `claim_subdomain`.
- For live data, mention `bind_data_source` — it lets the artifact fetch fresh data without redeploying.

## Reference

See `references/sharing-modes.md` for detailed sharing mode comparison.
See `references/advanced-features.md` for data binding, analytics, rollback, and team features.
