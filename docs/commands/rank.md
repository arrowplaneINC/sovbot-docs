# /rank

**Description:** Show a user's rank card as an image.

## Current Behavior
- Commands are globally restricted to run only in `#marketplace` or `#rank-leaderboard` per `src/index.js` (channel guard at interactionCreate).
- Renders a rank card using `src/utils/rankCard.js` with:
  - Avatar, gradient panel, rank badge, level text, and XP progress bar.
  - Uses the member's display role color as accent.
- Data source: `userManager.getOrCreate()` for `level` and `xp`.
- First-time hook (Onboarding Step 5):
  - If `userDoc.xpIntroDone === false`, sends a rank progression image and a follow-up embed to `config.rankLeaderboardChannel`.
  - Persists those posts in `OnboardingMessage` for 24h cleanup.
  - Sets `userDoc.xpIntroDone = true`.

## Expected Behavior
- ✅ Always renders the card and replies with an image attachment.
- ✅ Sends the Step 5 follow-up only once per user.
- ✅ Honors the global command channel restriction.

## Example
- Reply includes an image named `rank.png` with XP bar and level.

## Notes
- Dependencies: `src/utils/rankCard.js`, `src/utils/rankInfo.js`, `src/utils/xpCurve.js`, `src/managers/userDataManager.js`.
- Permissions: needs permission to upload files in the channel.
