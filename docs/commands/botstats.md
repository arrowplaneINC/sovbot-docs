# /botstats

**Description:** Show stats about the bot codebase (excluding node_modules).

## Current Behavior
- Ephemeral reply with an embed that includes:
  - Files: count of .js files under `src/`
  - Characters: total bytes across those files
  - Approx. Lines: rough estimate (bytes/50)
- Scans the repository recursively from `src/` and skips `node_modules` and `.git`.

## Expected Behavior
- ✅ Ephemeral summary of codebase size at the time of command execution.

## Example
- `/botstats` → embed showing Files, Characters, Approx. Lines.

## Notes
- Source: `src/commands/utility/botstats.js`
- Requires permission to read files from disk (bot process user).
