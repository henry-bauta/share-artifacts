# Advanced Features

## Live data binding

Artifacts can fetch live data without redeploying. Use `bind_data_source` to attach a JSON snapshot to an artifact — the artifact's code reads it from `/data/<bindingId>`.

Good for dashboards and reports that show fresh numbers while keeping the same layout and URL.

- Max snapshot size: 2 MB
- Optional: set `refresh_schedule` for periodic updates, or `source_url` to pull from an API
- Re-binding replaces the data immediately

## Version history and rollback

Every `update_artifact` or `deploy_artifact` (to an existing slug) creates a new revision. Previous revisions are kept.

- `rollback` moves the live version back to any prior revision number
- No revision is deleted — rollback just moves the pointer
- Immediately affects what viewers see

Use rollback when an update has issues: "roll back my dashboard to the previous version."

## Analytics

`get_analytics` returns view and deploy counts for an artifact:

- Total views and deploys
- Time buckets: hourly (24h), daily (7d or 30d)
- Cookieless, privacy-respecting estimates

Use when the user asks "how many people viewed this" or "is anyone looking at my dashboard."

## URL management

- `rename_slug` re-rolls the random URL (free tier) or renames a vanity slug (paid). Use to kill a leaked link.
- `claim_subdomain` claims a branded subdomain like `team.bauta.app` (paid plans only, one-time, permanent).

## Team and org features (paid plans)

- `list_members` and `set_member_role` manage organization members with roles: admin, member, viewer
- `get_team_analytics` shows org-wide view counts across all artifacts
- `export_audit_logs` exports a complete audit trail of all actions (Business plan)

## Data export and deletion

- `export_artifact` returns everything stored for an artifact (GDPR self-serve export): metadata, all revision source code, sharing config
- `delete_artifact` permanently and irreversibly removes an artifact and all its revisions

## Ephemeral deploys

Pass `ephemeral: true` to `deploy_artifact` for content that should auto-expire. Good for:

- One-time previews
- Temporary demos
- Content with a natural shelf life

The first `set_sharing` call on an ephemeral artifact clears the expiry, making it permanent.
