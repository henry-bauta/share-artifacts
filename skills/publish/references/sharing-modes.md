# Sharing Modes

Bauta artifacts support five sharing modes, set via the `set_sharing` tool.

| Mode | Who can view | How it works |
|------|-------------|-------------|
| **Private** | Nobody | URL returns 404. Use to take something offline without deleting it. |
| **Unlisted** (default) | Anyone with the full link | The URL includes a secret access token. Safe for sharing — the token is unguessable. |
| **Public** | Anyone with the URL | No token required. The bare URL works. Good for portfolios, public dashboards. |
| **Password** | Anyone who enters the password | Visitors see a password prompt before the content loads. Good for client previews. |
| **Email OTP** | Verified email addresses only | Visitors verify their email with a one-time code. Requires a paid plan. |

## When to suggest each mode

- **Quick share with a colleague** — keep unlisted (default), share the link or use `share_via_email`
- **Public portfolio or blog post** — set to public
- **Client deliverable** — password protect, or use email OTP for tighter control
- **Internal draft** — keep unlisted, share via email with specific people
- **Taking something offline temporarily** — set to private

## Changing modes

Modes can be changed at any time with `set_sharing`. The change takes effect immediately for all viewers.

Going from unlisted to public does NOT invalidate existing token links — they still work.
Going from public to unlisted generates a new token — old bare URLs stop working.

## Email sharing details

`share_via_email` sends a branded invite email from Bauta. For unlisted artifacts, each recipient gets a unique access token. The sender's verified email appears as the "shared by" identity.

Recipients who were previously shared with can be listed via `list_share_recipients` — useful for re-sharing updated artifacts with the same group.
