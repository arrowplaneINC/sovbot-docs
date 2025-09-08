# /adminreset

**Description:** COMPLETELY reset a user's data in this guild (testing only).

## Current Behavior
- Requires `ManageGuild` and a role gate via `config.botPerms` inside handler.
- Options:
  - `target` (required): user to reset.
- Flow:
  1. Sends an ephemeral confirmation embed with a "Confirm" button.
  2. When confirmed (see `interactionCreate` handler for `adminreset_confirm_*`), deletes user data:
     - `User` records (guild scoped)
     - `UserItem` inventory
     - `WelcomeTask` reminders
  3. Replies/updates with success.

## Expected Behavior
- ✅ Only authorized admins can perform a reset.
- ✅ Data deletion is scoped to the current guild.
- ✅ Confirmation is required.

## Example
- `/adminreset target:@User` → shows confirmation → upon confirm, data wiped.

## Notes
- Source: `src/commands/admin/reset.js` and confirmation handling in `src/index.js` (`interactionCreate` for `adminreset_confirm_*`).
- This is destructive; intended for testing and manual cleanup.
