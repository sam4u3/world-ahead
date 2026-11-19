# World Ahead Check

Independent, animated scorecards that check famous year-ahead forecasts, and the viral "cover decoding" theories about them, against what actually happens.

- `/` landing page
- `/2026` scored: forecasts vs reality, plus the cover theory checked
- `/2027` live tracker: baselines, the events that settle each forecast, and the "month wheel" theory

Not affiliated with or endorsed by The Economist. No cover artwork is reproduced.

## Structure

```
public/
  index.html   landing
  2026.html    2026 scorecard
  2027.html    2027 tracker
  404.html     not-found page
wrangler.toml  Cloudflare Worker (static assets), name: world-ahead
.github/workflows/deploy.yml  auto-deploy on push to main
```

Each page is self-contained HTML/CSS/JS. The data lives in the `TRENDS`, `EVENTS` and `MONTHS` arrays inside each page's `<script>`. To update a verdict, edit the array and push.

## Deploy

Pushes to `main` deploy automatically through GitHub Actions.

One-time setup, in GitHub → Settings → Secrets and variables → Actions:

| Secret | Value |
|---|---|
| `CLOUDFLARE_API_TOKEN` | A Cloudflare API token from the **Edit Cloudflare Workers** template |
| `CLOUDFLARE_ACCOUNT_ID` | Optional. Your account ID, needed only if the token covers several accounts |

Manual deploy:

```
npx wrangler login
npx wrangler deploy
```

The live site is at `https://world-ahead.<your-subdomain>.workers.dev`.
