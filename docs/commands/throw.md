# /throw

**Description:** Throw an item (e.g., tomato, rock) at another user.

## Current Behavior
- Options:
  - `item` (required): item slug to throw. Choices today: `tomato`, `rock`.
  - `target` (required): member to hit.
- Uses the generic item system: `useItem(interaction, <slug>, target)`.
- The concrete behavior (consumption, cooldown, effects) lives in `src/shop/items/<slug>.js`.

## Expected Behavior
- ✅ If the invoking user owns the selected item and can target, the action succeeds using that item's rules.
- ✅ If not, reply ephemerally with a clear reason (no item, invalid target, etc.).

## Example
- `/throw item:tomato target:@User` → performs item action as defined by `items/tomato.js`.

## Notes
- Dependencies: `src/commands/economy/throw.js`, `src/shop/useItem.js`, `src/shop/items/tomato.js`, `src/shop/items/rock.js`.
