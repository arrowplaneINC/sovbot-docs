# /boost

**Description:** Activate a Coffee or Espresso boost from your inventory.

## Current Behavior
- Ephemeral flow with a select menu when both boosts are available.
- Checks for existing active boost first (`UserItem.activeUntil > now`); if active, replies with remaining minutes.
- Filters usable items by quantity and `cooldownUntil < now`.
- If exactly one boost is usable, it calls `useItem` directly.
- If both are usable, shows a select menu with:
  - Coffee (1h, 10% boost)
  - Espresso (5h, 10% boost)
- On selection, calls `useItem` with the chosen slug.

## Expected Behavior
- ✅ Respect active boost (reject if one is active).
- ✅ Respect item cooldowns and quantities.
- ✅ Clear ephemeral feedback.

## Example
- `/boost` → Select menu → choose Espresso → ephemeral confirmation.

## Notes
- Dependencies: `src/commands/economy/boost.js`, `src/shop/useItem.js`, `src/models/ShopItem.js`, `src/models/UserItem.js`.
- Global channel guard from `src/index.js` applies (Marketplace or Rank Leaderboard channels).
