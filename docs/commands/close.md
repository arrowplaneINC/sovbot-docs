# /close

**Description:** Close a modmail ticket.

## Current Behavior
- Can be used in DMs or in a server ticket channel.
- If used in DMs (no `interaction.guild`): calls `modmailManager.closeTicketByUser()` to close the current user's open ticket, if any, and replies ephemerally with success/failure.
- If used in a guild channel: checks whether the current channel corresponds to an open `Ticket` and calls `modmailManager.closeTicket()`.
- DMs permission is enabled (`setDMPermission(true)`).

## Expected Behavior
- ✅ In DMs, close the user's open ticket if one exists.
- ✅ In a modmail thread/channel in the guild, close that open ticket.
- ✅ Provide clear ephemeral feedback on failure.

## Example
- User DMs `/close` → "Ticket closed." or "You have no open ticket."
- Staff uses `/close` inside a ticket channel → ticket is closed.

## Notes
- Source: `src/commands/admin/close.js`
- Related: `src/managers/modmailManager.js`, `src/models/Ticket.js`.
