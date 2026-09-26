# Kolaru Voice Bot Host

Web dashboard and voice bot host. The dashboard accepts individual tokens or a `.txt` file containing one token per line (comma-separated tokens are also accepted).

## Render configuration

Use these values in Render:

- Runtime: Node
- Build Command: `npm install`
- Start Command: `npm start`
- Environment Variables:
  - `HOST=0.0.0.0`
  - `PORT=10000`
  - `MAX_BOTS=5`
  - `BOT_TOKENS=your-token-here`
  - `VOICE_CHANNEL_IDS=your-channel-id-here`
  - `DASHBOARD_PASSWORD` set to a long, unique secret in Render

## Notes

The app starts from [kolaru.js](kolaru.js). The dashboard and all management endpoints require the configured dashboard password; `/health` remains public for health checks. Production startup fails if `DASHBOARD_PASSWORD` is missing.

Tokens imported through the dashboard are written to the service's local `.env` file. Render's default filesystem is ephemeral, so those imported tokens and uploaded audio do not survive a restart or redeploy. Configure `BOT_TOKENS` in Render for durable token configuration, or use a persistent disk on a plan that supports it. The included free service can spin down while idle and is not suitable for guaranteed always-on voice connections; use an always-on plan for that requirement.

After creating the Render service, set `DASHBOARD_PASSWORD` in its Environment settings before opening the public dashboard. Never put real tokens or the dashboard password in the repository.
