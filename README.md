# Love Sword Arena — Cloudflare Server-Authoritative Co-op

This archive is based on the original game build and preserves the existing game UI, single-player combat, progression, shop and assets.

## Multiplayer architecture

Cloudflare Durable Objects own the live room:
- player positions and HP
- enemy spawning and movement
- waves and upgrade phase
- attack validation and damage
- authoritative 20 Hz game tick
- 10 Hz state snapshots

Clients send only input/intent and render the server state.

## Important fixes
- Co-op render/input loop starts immediately when the room connects (the previous build could show a static arena).
- Server movement stops after 450 ms without an input packet, so a backgrounded tab cannot keep moving forever.
- Returning to a tab immediately sends current input and resumes rendering.
- Unexpected WebSocket loss triggers a reconnect.
- Closing/leaving the game disables reconnect.
- The original game files and assets are retained.

## Deploy
Replace the repository files with this archive's contents and deploy the Worker.
