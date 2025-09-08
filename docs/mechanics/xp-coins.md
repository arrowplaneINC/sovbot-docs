# XP & Coins Mechanics

**Description:** Deep dive into how XP and coins are earned, cooldowns, limits, and level computation.

## XP Sources (Current Behavior)
- **Messages** (`src/managers/economyManager.js`)
  - Per-message XP: `guildConfig.xpPerMessage` or default **20 XP** per eligible message.
  - Anti-spam: 60s per-user cooldown via `Cooldown` helper (keyed by guild+user).
  - Additional: Media posts in `ACHIEVEMENTS_CHANNEL_ID` earn +5 XP per message with attachments.
  - After each eligible message, `xpManager.addXP(..., useCooldown=true)` is used and level-up is checked.
- **Voice Sessions** (`src/managers/voiceManager.js`)
  - Earn **5 XP/minute** of active voice time (not muted/deafened).
  - Activity tracking: session starts on join; `activeStart` pauses when muted/deafened.
  - On leave, total active minutes are computed and XP is granted in one batch.
- **Commands / Other**
  - Some onboarding steps grant XP indirectly through normal message actions; not direct XP grants.

## Coins Sources (Current Behavior)
- **Messages** (`economyManager.processMessage`)
  - First **10** messages per day per user award **5 coins** each.
  - Daily counter reset: `User.messagesDay` and `User.messagesToday`.
- **Voice Sessions** (`voiceManager._onLeave`)
  - Coins based on session length: **10 coins** for ≥5 minutes, **30 coins** for ≥30 minutes of active time.
- **/work** (`src/commands/economy/work.js`)
  - Usable only in `#marketplace` (`config.marketplaceChannel`).
  - **12h cooldown** using `User.lastWork`.
  - Random reward **15–85** coins.
  - Logged via `economyManager.logCurrency()`.

## XP Cooldown Behavior
- `src/managers/xpManager.js` uses a per-guild cooldown for spammy actions when `useCooldown=true`.
  - Guild value from `GuildConfig.xpCooldownSeconds` (default **8s** if not set).
  - `xpManager.addXP(guild, userId, amount, reason, useCooldown)` gates via an in-memory `Cooldown` helper.

## Level Calculation
- Core functions in `src/utils/xpCurve.js`.
  - `xpForLevel(level)`:
    - Levels 1–10: linear-ish, returns `50 + 10 * level` (e.g., L1=60, L10=150).
    - Levels 11+: quadratic growth `150 + round(0.6 * (level-10)^2)`.
  - `totalXpToReach(level)`: sum of `xpForLevel(i)` for `i=1..level`.
- Display & recomputation on rank card: `src/utils/rankCard.js` recomputes level from total XP to ensure displayed level matches cumulative XP.

## Level-Up Announcements
- When a level increase is detected in `src/managers/levelingManager.js`:
  - Updates the stored `user.level`.
  - Sends a "🎉 Level Up!" embed to `config.botUpdateChannel` (env: `BOT_UPDATE` or `BOT_UPDATE_CHANNEL`), falling back to the guild system channel.
  - Logs: `[Level] userId now level X`.

## Currency Logging
- `economyManager.logCurrency()` posts a rich embed to `config.currencyLogsChannel` if configured.
- Includes amount, reason, and new balance.

## Configuration Surface
- `GuildConfig` (DB): `xpPerMessage`, `xpCooldownSeconds`, optional `channels.logs`.
- `.env`/`config/index.js`:
  - `CURRENCY_LOGS_CHANNEL`, `XP_LOGS_CHANNEL`, `MARKETPLACE_CHANNEL_ID`, `ACHIEVEMENTS_CHANNEL_ID` (media XP), `BOT_UPDATE`.

## Expected Behavior
- ✅ XP: respect guild cooldowns to prevent spam.
- ✅ Coins: message daily limit of 10; `/work` 12h cooldown; voice session coin thresholds apply.
- ✅ Level-ups: immediate announcement to the configured updates channel.

## Notes
- Cooldowns are in-memory; on restart, per-user XP cooldowns reset (message cooldown also resets). Daily message limits persist in the user doc.
- If you want role-based multipliers or boosts (e.g., Coffee/Expresso items) to affect rewards, we can document and implement that next.
