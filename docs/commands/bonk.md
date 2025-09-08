# /bonk

**Description:** Bonk another user using the Bonk item.

## Current Behavior
- Options:
  - `target` (required): member to bonk.
- Invokes the item handler via `useItem(interaction, 'bonk', target)`.
- Actual effect, cooldowns, and inventory usage are implemented in `src/shop/items/bonk.js` through the generic `useItem` pipeline.
- Errors (e.g., missing item, no inventory) are surfaced ephemerally by the item system.

## Expected Behavior
- ✅ If the invoking user owns a Bonk item, the action succeeds and consumes/uses the item according to its item rules.
- ✅ If the user lacks the item or cannot target, respond ephemerally with a clear reason.

## Example
- `/bonk target:@User`
- Bot responds per item logic (e.g., a playful message, effect, or animation).

## Notes
- Dependencies: `src/shop/useItem.js`, `src/shop/items/bonk.js`, `src/models/ShopItem.js`, `src/models/UserItem.js`.
