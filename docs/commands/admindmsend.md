# /admindmsend

**Description:** Send a direct message to a specified user from the bot (Admins only).

## Current Behavior
- Defined in `src/commands/admin/admindmsend.js`.
- Restricted to administrators via default permissions and a runtime guard.
- Options:
  - `user` (required): target user to DM.
  - `content` (required, 1–2000 chars): message text.
- Sends DM via `targetUser.send({ content })`.
- Replies ephemerally with success or a clear failure message (e.g., DMs disabled).

## Expected Behavior
- ✅ Only admins can execute and the target receives the DM.
- ✅ Graceful error if DMs are closed or bot is blocked.

## Example
- `/admindmsend user:@Airen content:"Welcome aboard!"`
- Ephemeral reply: `✅ Sent DM to Airen#1234.`

## Notes
- Dependencies: `discord.js` DM API.
- Ensure the bot and the target share a guild and the target allows server DMs.
