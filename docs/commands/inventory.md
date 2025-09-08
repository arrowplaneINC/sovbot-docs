# /inventory

**Description:** View your owned items.

## Current Behavior
- Ephemeral reply with an embed titled "<username>'s Inventory".
- Lists each owned item (quantity > 0) with name, emoji, quantity, and description.
- Data source: `UserItem` documents populated with `ShopItem`.
- If you have no items, replies ephemerally with a hint to `/shop`.

## Expected Behavior
- ✅ Respond ephemerally and list all items with quantities.
- ✅ If none, provide a helpful message.

## Example
- `/inventory` → embed listing items with descriptions.

## Notes
- Dependencies: `src/commands/economy/inventory.js`, `src/models/UserItem.js`, `src/models/ShopItem.js`.
- Global command guard from `src/index.js` applies (Marketplace or Rank Leaderboard).
