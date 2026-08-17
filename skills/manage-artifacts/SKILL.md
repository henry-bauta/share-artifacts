---
name: manage-artifacts
description: >
  Manage published artifacts: list, update, roll back, rename, check analytics,
  change sharing, or delete. Use when the user asks "show my artifacts",
  "list my published pages", "update my site", "roll back", "how many views",
  "who has access", "rename the URL", "delete my artifact", "change sharing",
  "make it public", "make it private", "check analytics", or wants to manage
  something they previously published with Bauta.
---

# Manage Artifacts

Help the user manage their published Bauta artifacts.

## Before you start

Confirm Bauta is connected. If its tools are not available, tell the user to connect Bauta via Settings > Connectors.

## Common tasks

### List artifacts

Call `list_artifacts`. Present results as a clean list showing:

- Title and URL
- Sharing mode (private / unlisted / public / password / email_otp)
- Last updated

If the user has many artifacts, ask which one they want to work with.

### Update content

1. Identify which artifact to update (ask or match by title/slug from `list_artifacts`)
2. Call `update_artifact` with the artifact ID and new source code
3. Confirm: "Updated — the new version is live at [URL]"

### Roll back

1. Call `list_artifacts` to find the artifact
2. Call `rollback` with the artifact ID and the target revision number
3. Confirm: "Rolled back to revision [N]. The previous version is live again."

If the user doesn't specify a revision, roll back to the one before current (revision N-1).

### Change sharing

1. Identify the artifact
2. Call `set_sharing` with the desired mode: `private`, `unlisted`, `public`, `password`, or `email_otp`
3. Confirm the change and explain what it means for viewers

### Share with someone

1. Identify the artifact
2. Call `share_via_email` with the recipient's email
3. Confirm: "Invite sent to [email]"

Use `list_share_recipients` for autocomplete if the user has shared before.

### Check analytics

1. Identify the artifact
2. Call `get_analytics` with the artifact ID
3. Present: total views, recent trend (daily buckets), and deploy count

### Rename URL

1. Identify the artifact
2. Call `rename_slug`
   - Free tier: re-rolls to a new random URL (old link dies immediately)
   - Paid: accepts a chosen new slug (old link 301-redirects for 30 days)
3. Confirm the new URL and warn about the old link behavior

### Export data

Call `export_artifact` to download all stored data for an artifact: metadata, every revision's source code, sharing config, and share grants.

### Delete

1. Warn that deletion is **permanent and irreversible**
2. Confirm the user wants to proceed
3. Call `delete_artifact`
4. Confirm: "Deleted. The URL no longer serves any content."

## Disambiguation

When the user's request is ambiguous about which artifact, call `list_artifacts` first and ask them to pick. Never guess.
