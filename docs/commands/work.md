# /work

**Description:** Work to earn coins in the marketplace. Has a cooldown.

## Current Behavior
- Only usable in the channel with ID set in `config.marketplaceChannel`.
- 12-hour cooldown enforced via `User.lastWork` in `src/commands/economy/work.js`.
- Rewards a random amount between **15–85** coins.
- Logs the transaction using `economyManager.logCurrency()`.

## Expected Behavior
- ✅ Enforce 12h cooldown with a clear remaining time message (`Xh Ym`).
- ✅ Reject when used outside the marketplace channel (ephemeral message).
- ✅ Persist `lastWork` timestamp and updated coin balance.

## Example
User runs `/work` in the marketplace channel and receives a confirmation message like:
> Great job! You earned **72 coins** from your work! 🎯

## Notes
- Dependencies: `src/managers/userDataManager.js`, `src/managers/economyManager.js`.
- Data fields touched: `User.lastWork`, `User.coins`.
- Cooldown message is ephemeral; reward confirmation is public.
