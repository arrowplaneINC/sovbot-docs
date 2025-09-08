# Onboarding Workflow

1. Member joins the server.
2. Step 1/6 — Welcome
   - Triggered by either:
     - Student role gets added (preferred trigger), or
     - User sends their first message in any guild channel (backup trigger)
   - Bot posts a welcome embed in **#general** (persistent; not auto-deleted).
   - Flag set: `User.welcomeSent = true` to prevent duplicates.
3. Step 2/6 — Roles set
   - When member gains any role from `SELECTABLE_SELF_ROLES`:
     - Post an embed in **#marketplace** to congratulate and guide next step.
     - Post an intro template in **#introductions** pinging the user.
       - The template message is retained until the user posts in **#introductions**, then the bot deletes its template and clears `introPromptMessageId`.
     - Flag set atomically: `User.rolesAcknowledged = true` (prevents duplicates under rapid role changes).
4. Step 3/6 — Introductions
   - When the user posts in **#introductions**:
     - Bot deletes the stored intro template (if present).
     - Flag set atomically: `User.introDone = true`.
     - Private "intro task" channel exists for staff follow-up (Reminders ➜ Intro). Completion archive + 8h deletion via scheduler.
5. Step 4/6 — Marketplace
   - When the user runs any slash command in **#marketplace**, send XP/leaderboard guidance embed (current behavior via `onboardingFlow.marketplaceCommand`).
6. Step 5/6 — General
   - When the user runs any slash command in **#general**, DM video/link and award an item (Coffee). Flags maintained: `xpIntroDone`, etc.
7. Step 6/6 — Completion
   - All flags indicate completion. Subsequent onboarding posts do not repeat.

## Notes
- Auto-delete: All onboarding messages are auto-deleted after 24 hours except the Step 1 welcome in **#general** and the **#introductions** template (which is deleted immediately when the user posts in that channel).
- Persistence: The cleanup scheduler runs hourly and survives restarts.
- Data model fields used: `welcomeSent`, `rolesAcknowledged`, `introPromptMessageId`, `introPromptChannelId`, `introDone`, `introTaskDone`, `weekCheckDone`, `monthlySummaryDone`.
- Reminders category contains Intro/Week tasks; completion locks/renames channel and schedules deletion after 8 hours.
