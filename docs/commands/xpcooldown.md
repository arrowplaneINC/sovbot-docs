# /xpcooldown

**Description:** View or set the server XP cooldown in seconds (Admins only).

## Current Behavior
- Admin-only via default member permissions.
- Option `seconds` (optional, 1–600). If omitted, shows the current cooldown.
- Uses `xpManager.setCooldown(guildId, seconds)` to update DB and in-memory cache.
- Public confirmation response.

## Expected Behavior
- ✅ Omit `seconds` to display the current cooldown.
- ✅ Set within bounds (1–600).
- ✅ Applies immediately to message XP gating (via `xpManager.addXP(..., useCooldown=true)`).

## Example
- `/xpcooldown` → "Current XP cooldown is 8s."
- `/xpcooldown seconds:5` → "✅ XP cooldown updated to 5s for this server."

## Notes
- Source: `src/commands/admin/xpcooldown.js`
- Related: `src/managers/xpManager.js` (guild-specific cooldown), `src/models/GuildConfig.js`.
