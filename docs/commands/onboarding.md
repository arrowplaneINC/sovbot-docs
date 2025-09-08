# /onboarding

**Description:** Admin tools for user onboarding flow (reset a user's flow or mark it complete).

## Current Behavior
- Admin-only via default member permissions.
- Subcommands:
  - `reset user:<user>` — Clears key flags and re-triggers onboarding from Step 1 for the target member.
  - `markascomplete user:<user>` — Marks all onboarding steps complete without sending any messages.
- Implementation:
  - `reset` clears flags on `User` and calls `onboardingFlowManager.studentRoleAssigned(member)` to kick off Step 1.
  - `markascomplete` sets `introDone`, `marketplaceIntroDone`, `xpIntroDone`, `onboardingCompleted` to `true`.
- Ephemeral replies with success or error.

## Expected Behavior
- ✅ Only admins can run.
- ✅ `reset` safely re-runs the initial onboarding flow.
- ✅ `markascomplete` prevents any further onboarding messages.

## Example
- `/onboarding reset user:@Member`
- `/onboarding markascomplete user:@Member`

## Notes
- Source: `src/commands/admin/onboarding.js`
- Related: `src/managers/onboardingFlowManager.js`, `src/events/guildMemberUpdate.js`.
