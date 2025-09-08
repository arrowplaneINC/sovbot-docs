# /wallet

**Description:** Show your current coin balance as a styled image.

## Current Behavior
- Ephemeral reply with an attached image `wallet.png`.
- Pulls coin balance via `userManager.getCoins()`.
- Fetches rank name from the user's level for the card styling.
- Renders with `src/utils/walletCard.js`.

## Expected Behavior
- ✅ Always respond ephemerally with the wallet image.

## Example
- `/wallet` → returns wallet card image.

## Notes
- Dependencies: `src/utils/walletCard.js`, `src/managers/userDataManager.js`, `src/utils/rankInfo.js`.
