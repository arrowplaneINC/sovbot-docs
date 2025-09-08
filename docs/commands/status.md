# /status

**Description:** Update the bot's presence text (Admins only).

## Current Behavior
- Slash command defined in `src/commands/admin/status.js`.
- Restricted to administrators via `setDefaultMemberPermissions(PermissionFlagsBits.Administrator)` and a runtime guard.
- Updates the presence with `client.user.setPresence({ activities: [{ name: <text>, type: Playing }], status: 'online' })`.
- Replies ephemerally with success or failure.

## Expected Behavior
- ✅ Only server admins can execute.
- ✅ Presence updates immediately.
- ✅ Handles errors and responds ephemerally.

## Example
- `/status text:"Helping the server"`
- Ephemeral reply: `✅ Bot status updated to: Helping the server`

## Notes
- Dependencies: `discord.js` Activity API.
- Edge cases: overly long strings are truncated to 128 characters by the command.
