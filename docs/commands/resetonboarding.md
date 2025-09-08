# /resetonboarding

**Description:** Reset the onboarding experience for a specific user and retrigger it.

## Current Behavior
- Admin-only.
- Option `user` (required): the member whose onboarding to reset.
- Steps performed:
  1. Clears onboarding flags on the user doc: `onboardingCompleted`, `rolesAcknowledged`, `introDone`, `marketplaceIntroDone`, `xpIntroDone`.
  2. Attempts to remove manageable roles; then re-adds the Student role (`config.studentRoleId`).
  3. Relies on `guildMemberUpdate` to retrigger onboarding Step 1.
- Ephemeral confirmation with success or error.

## Expected Behavior
- ✅ Only admins can execute.
- ✅ Flags are reset and Student role is reapplied, safely handling role hierarchy.

## Example
- `/resetonboarding user:@NewMember` → "✅ Onboarding has been successfully reset…"

## Notes
- Source: `src/commands/admin/resetonboarding.js`
- Related: `src/events/guildMemberUpdate.js` (Step 1/2 triggers), `src/managers/onboardingFlowManager.js`.
