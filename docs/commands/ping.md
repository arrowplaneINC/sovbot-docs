# /ping

**Description:** Replies with bot statistics (latency, API ping, Mongo cluster).

## Current Behavior
- Public command; optionally role-gated if `config.botPerms` is set and the invoker lacks it.
- Replies "Pinging...", then edits with an embed showing:
  - Latency (message round-trip)
  - API WebSocket ping
  - Mongo cluster name derived from the MongoDB URI

## Expected Behavior
- ✅ Quick health check of the bot’s responsiveness.
- ✅ Optional role restriction via `config.botPerms`.

## Example
- `/ping` → embed with Latency, API Ping, and Mongo Cluster.

## Notes
- Source: `src/commands/utility/ping.js`
- Requires the bot to send embeds in the current channel.
