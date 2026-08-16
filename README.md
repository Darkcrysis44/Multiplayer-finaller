# Love Sword Arena — Co-op Combat Fix

- Fixed the co-op attack animation appearing twice for the attacking player.
- The server's attack FX echo is now ignored by the originating client because that client already renders its attack instantly.
- Attack cooldown is checked before any local swing/FX is created, so rapid clicks cannot create extra local swings.
- Kept the 0.5 second server/client attack cooldown.
- Other players still receive the server-confirmed attack FX normally.
