# /shop

**Description:** Browse and purchase items from the SovBot shop.

## Current Behavior
- Public, paginated catalog with buttons.
- Data source: `ShopItem` documents filtered for availability (see below) and sorted by `sortOrder`.
- Pagination size: 5 items per page.
- Each item shows name, emoji, cost, description, and optional remaining availability.
- Buy flow:
  - Re-checks availability and user coin balance.
  - Deducts coins and increments `UserItem.quantity`.
  - Confirms via an ephemeral reply.
- Session lifetime: 5 minutes; components are removed on timeout.

### Availability Rules
- Global expiry: `expiresAt` on the `ShopItem` hides it once past.
- Per-user expiry: `swift_sword` is available only for the first 4 weeks after a member joined the guild.
- “Available for” label displays the nearest remaining time (global or per-user window).

## Expected Behavior
- ✅ Items reflect real-time availability at selection.
- ✅ Deduct coins only if the user has enough.
- ✅ Error feedback is ephemeral.

## Example
- `/shop` → interactive list with Buy buttons and Prev/Next.

## Notes
- Dependencies: `src/commands/economy/shop.js`, `src/models/ShopItem.js`, `src/models/UserItem.js`, `src/managers/userDataManager.js`.
- Global command channel guard applies (Marketplace or Rank Leaderboard); ensure bot can send embeds and use components in that channel.
