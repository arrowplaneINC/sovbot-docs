# /leaderboard

**Description:** Show the top users for Coins or XP.

## Current Behavior
- Required option `type`: `coins` or `xp`.
- Queries top 10 users in the current guild from the `User` collection, sorted by the selected metric.
- Renders an embed with ordinal numbering and user mentions.
- Public reply.

## Expected Behavior
- ✅ Always reply with the top 10 for the chosen type.
- ✅ If no entries, reply ephemerally with "Leaderboard is empty."

## Example
- `/leaderboard type:coins` → lists the top coin balances.

## Notes
- Dependencies: `src/commands/economy/leaderboard.js`, `src/models/User.js`.
- Global command channel guard applies (Marketplace or Rank Leaderboard).
