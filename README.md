# Love Sword Arena — Account + Stable Multiplayer

## What's new
- Username/password accounts stored in a Cloudflare Durable Object.
- Persistent server-side profile for level, XP, rebirths, core stats, gear, skills, passives and balance.
- Solo and multiplayer use the same authenticated profile.
- Server is authoritative for multiplayer progression; the client cannot overwrite multiplayer stats by sending fake join/progression values.
- Level-up stat gains are applied once to the persistent base stats. Reconnecting no longer reapplies level gains.
- Multiplayer movement uses fixed 20 Hz input samples, sequence acknowledgements, prediction and reconciliation.
- Remote arm/weapon aim uses a separate authoritative attack angle so walking does not rotate the arm away from the last attack direction.

## Deployment
Deploy the whole repository through Cloudflare Workers/Pages using `wrangler.toml`. The `v2` migration creates the `Auth` Durable Object alongside the existing `Room` object.

The account database is intentionally server-side; localStorage is only a cache/fallback and is no longer the source of truth once an account is logged in.
