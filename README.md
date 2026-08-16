# Love Sword Arena — Server Authoritative Co-op

This build keeps the existing game and moves the online battle simulation to the Cloudflare Durable Object.

## Important fixes
- The co-op runtime/render loop is started when the server starts the battle.
- WASD / arrow input is continuously sent to the Cloudflare server.
- The server owns player positions, enemies, waves, damage, attacks and upgrades.
- Cloudflare Durable Object alarms drive the authoritative game tick.
- Alarm scheduling checks Durable Object storage, so a stale in-memory flag cannot stop the server loop.
- Returning from an inactive/background tab immediately resends current input.
- A lost WebSocket reconnects while the co-op arena is still open.
- Backgrounded clients cannot leave stale movement input running forever.

## Deploy
Upload the contents of this archive to the GitHub repository and let the connected Cloudflare Worker deployment build it.
