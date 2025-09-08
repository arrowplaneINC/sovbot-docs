# /postweekly

**Description:** Admin command to post weekly leaderboards (Coins & XP) immediately.

## Current Behavior
- Requires `ManageGuild` permission.
- Invokes `schedulers/weeklyLeaderboards.postWeekly(client)` to compute and post.
- Uses `config.rankLeaderboardChannel` as the target channel.
- Ephemeral confirmation to the invoker.

## Expected Behavior
- ✅ Posts both Coin and XP weekly rankings to the configured channel.
- ✅ Handles errors gracefully with an ephemeral error message.

## Example
- `/postweekly` → "Posted weekly leaderboards to #rank-leaderboard."

## Notes
- Source: `src/commands/admin/postweekly.js`
- Ensure `RANK_LEADERBOARD_CHANNEL_ID` is set in the environment and the bot has permission to post in that channel.
