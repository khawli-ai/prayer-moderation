# Prayer app — moderation review page

A single static page used to approve or reject prayer requests awaiting
review.

It exists as a separate static site because Supabase rewrites any
`text/html` response from `*.supabase.co` to `text/plain` with a CSP
sandbox, so the moderation Edge Function cannot serve a page with
buttons. The function does the work and returns JSON; this page is only
the UI.

**Nothing happens on load.** Opening the page performs a read-only
lookup. A decision is sent only when a button is pressed, as a POST —
which is what stops link previews (Discord, Slack, iMessage) from
approving posts merely by fetching the URL.

No credentials live here. The endpoint is public, and the per-post
review token arrives in the query string at review time and is
single-use.
