# Love Sword Arena — Account Login Fixed v2

Based on the supplied ACCOUNT_MOVEMENT_STABLE build.

## Account system
- Username: 3–24 chars, A-Z/a-z/0-9/_/-
- Password: 6–72 chars
- Registration and login are handled by the existing Auth Durable Object.
- Auth data uses the existing SQLite-backed Durable Object and SQL tables.
- PBKDF2-SHA256 password hashing with a random salt.
- 30-day server-side sessions.
- Profile is stored as a single canonical JSON record.
- New accounts never import local progression, preventing stat inflation.
- All auth failures return JSON instead of an unhandled HTTP 500 where possible.

## Deployment
Keep the existing Durable Object migration history from this supplied build. Do not add a new Room/Auth migration just for this revision.
