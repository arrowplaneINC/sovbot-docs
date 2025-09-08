# /balance

**Description:** Shows a user's coin and XP balance as an image card.

## Current Behavior
- Global channel restriction enforced by `src/index.js` (only allowed in `#marketplace` or `#rank-leaderboard`).
- If no `user` option is provided, defaults to the invoking user.
- Builds an image via `src/utils/balanceCard.js` including coins and XP.
- Uses the member's display color as an accent.

## Expected Behavior
- ✅ Always render the balance card and reply with an image attachment.
- ✅ Honor global command channel restrictions.

## Example
- Reply includes an image named `balance.png` showing coins and XP.

## Notes
- Dependencies: `src/utils/balanceCard.js`, `src/managers/userDataManager.js`.
- Permissions: needs permission to upload files in the channel.
