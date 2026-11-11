# Lore Keeper Worker

A small Cloudflare Worker that sits between the site and Gemini. It holds the
Gemini API key as a secret, so the key never appears in the page or the repo.

## Deploy

Run these from the `worker` folder. You need a free Cloudflare account and a
Gemini API key from Google AI Studio.

1. Log in to Cloudflare: `npx wrangler login`
2. Store the key as a secret (paste it when asked): `npx wrangler secret put GEMINI_API_KEY`
3. Deploy: `npx wrangler deploy`
4. Copy the `https://paimon-lore-keeper.<your-name>.workers.dev` address that
   wrangler prints and paste it into `GEMINI_URL` in `index.html`.

The knowledge base is read from `../knowledge/teyvat_lore_knowledge_base.md` on
your machine at deploy time. Redeploy after you edit it.

## Local testing

Create `worker/.dev.vars` (ignored by git) with:

```
GEMINI_API_KEY=your-key
ALLOWED_ORIGINS=http://localhost:8000
```

Then run `npx wrangler dev`.

## What protects the key

- The key is a Worker secret. It is not in this repo and is never sent to the browser.
- Only origins in `ALLOWED_ORIGINS` (`wrangler.toml`) can call the Worker from a browser.
- Each IP address is limited to 5 questions per minute.
- The browser can only send a region, an age and a question of up to 400 characters.
  The instructions and knowledge base are fixed on the server.
- Answer length is capped, and Google's error details are never passed on.

Also restrict the key itself in Google AI Studio / Cloud Console to the
Generative Language API, and keep the project on the free tier (no billing)
so misuse can only exhaust the daily quota and can never cost money.

Never commit the key, and never paste it into `index.html` or `wrangler.toml`.
