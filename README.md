# Love Sword Arena — Cloudflare Server-Authoritative Co-op

GitHub + Cloudflare Workers + Durable Objects + WebSockets.

## Multiplayer architecture
- The **Cloudflare Durable Object is the game server**.
- There is **no host-authoritative gameplay** and no player is the simulation host.
- Player browsers only send input/attack events and render the authoritative server state.
- Server time drives countdowns, wave transitions, enemy movement, enemy HP, damage, rewards and upgrade synchronization.
- The server simulates at 20 Hz and sends compact state snapshots at 10 Hz.
- If a player Alt+Tabs, the server keeps running; when that player returns, the client receives the current server state.
- Other players are not affected by another player's tab being backgrounded.
- Wave upgrade offers are sent to every connected player. Each player chooses independently; the next wave begins only after every connected player has chosen.
- Attack FX are broadcast as server events so remote attack animations do not depend on the attacker's render loop.

## Co-op flow
1. Click **CO-OP**. The solo battle stops immediately.
2. Create a room or join with the same room code.
3. The **START BATTLE** button is available in the server lobby; there is no host authority.
4. Any connected player can press START BATTLE.
5. Cloudflare schedules the synchronized battle start.
6. Cloudflare controls the battle from then on.

## Deploy
Cloudflare Workers Builds:
- Build command: leave blank
- Deploy command: `npx wrangler deploy`
- Root directory: `/`

The Worker name is `multiplayer-game1` to match the existing Cloudflare project.


## Background-tab resilience
- The browser is never the authoritative simulation host.
- Player input is treated as transient input; the server stops applying stale input after 750 ms.
- Client WebSockets automatically reconnect after an unexpected disconnect while co-op is active.
- Returning from a background tab requests a fresh authoritative snapshot from Cloudflare.
- Other players continue to be simulated by the Durable Object even if one browser is throttled or disconnected.
