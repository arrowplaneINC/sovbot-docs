# /coins

**Description:** Admin coin management (add/remove coins for a user).

## Current Behavior
- Admin-only command (`PermissionFlagsBits.Administrator` + role gate via `config.botPerms`).
- Subcommands:
  - `add user:<user> amount:<int> reason:<text>`
  - `remove user:<user> amount:<int> reason:<text>`
- Adjusts coins through `userManager.addCoins()` and logs to:
  - Currency logs channel (`config.currencyLogsChannel`) via embed
  - `economyManager.logCurrency()` for consistency
- Ephemeral confirmation to the invoker.

## Expected Behavior
- ✅ Only permitted users can run the command.
- ✅ Clear logging with before/after balances and reason.

## Example
- `/coins add user:@Jay amount:250 reason:"Event prize"`

## Notes
- Source: `src/commands/admin/coins.js`
- Dependencies: `userManager`, `economyManager`, `config.currencyLogsChannel`.
