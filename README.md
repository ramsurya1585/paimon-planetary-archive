# P.A.I.M.O.N.

**Planetary Archive, Irminsul Memory, and Observational Network**

An interactive lore archive for the world of Teyvat (Genshin Impact). It is a constellation of eight regions on a night sky. Each region opens a full-page chat with a lore chatbot, and a timeline slider lets you look at the world in earlier ages.

> Unofficial fan project. It is not affiliated with, endorsed by, or connected to HoYoverse. Genshin Impact and all related names belong to their owners.

**Live site:** https://ramsurya1585.github.io/paimon-planetary-archive/

## What it does

- **Constellation map.** Eight nodes (Snezhnaya, Mondstadt, Natlan, Sumeru, Liyue, Inazuma, Fontaine, Nod-Krai) sit at different heights around a lens-flare star. Hovering or focusing a node lights it up with a ring, glow and sparkle.
- **Ages of Teyvat.** A slider at the bottom switches between five ages: Primordial, Ancient, Archon War, Cataclysm and Present. Nations that did not yet exist fade out, and ruin sites are tagged.
- **Full-page chat.** Clicking a node opens a chat for that region. The region and the chosen age are sent to the bot with each question as a hidden context tag, so answers match the place and the time.
- **Fallback.** If the bot does not answer within 30 seconds, the page shows a built-in sample reply. If it has nothing, it says: "Information not found. The ley lines that carry this record are damaged."
- **Keyboard and motion.** Nodes and the age slider work with the keyboard, and animations respect the reduced-motion setting.
- **Question limit.** Each browser can ask 10 questions per rolling 24 hours. It is a soft limit kept in the browser, so it only slows casual use. Real limits belong in Botpress.

## How it is built

- A single static file, `index.html`, with no build step.
- Tailwind CSS (CDN), GSAP for animation, and Lucide icons.
- Fonts: Pirata One for headings and labels, and Noto Sans for text, both from Google Fonts.
- Background: a layered gradient, a star-particle canvas, light streaks and an SVG lens flare.
- Chat: the page uses the Botpress Webchat embed in the background (its own bubble is hidden). The page sends each question with `window.botpress.sendMessage` and shows the replies in its own drawer.

The two Botpress script tags at the bottom of `index.html` carry a public bot ID and client ID. These are the public embed values that Botpress intends for web pages. They are not secrets, but do not put any API keys or tokens in this repo.

## Project layout

```
index.html    The whole site
README.md     This file
.nojekyll     Tells GitHub Pages to serve the files as they are
.gitignore    Keeps private working files out of the repo
```

## Run it locally

Any static file server works. From this folder:

```bash
python -m http.server 8765
```

Then open http://localhost:8765/index.html.

## Deploy

The site is served by GitHub Pages from the `main` branch, root folder. Push to `main` and the site updates in about a minute.

## The lore knowledge base is not in this repo

The bot's knowledge base is kept out of this repository on purpose. It lives only in the Botpress workspace and on the maintainer's computer, and it is listed in `.gitignore`, so it is never committed or published here. The repo contains only the front end.

The knowledge base is written in the maintainer's own words from public wiki pages (the Genshin Impact Wiki on Fandom, whose text is licensed CC BY-SA 3.0) and is marked draft. It can be wrong or out of date, so check the wiki or the game for anything that matters.

## Security and privacy

- **Static site.** There is no server, database, login or payment on this site, so most web-app risks do not apply.
- **Scripts.** GSAP and Lucide are pinned to exact versions and checked with Subresource Integrity. The two Botpress scripts cannot be pinned because Botpress controls them. The unused Tailwind script was removed.
- **Headers.** GitHub Pages cannot set HTTP headers, so the page uses a content-security meta tag and a small script that stops it being framed by other sites.
- **No secrets.** The repo has no API keys or tokens. The Botpress bot and client IDs live in Botpress's hosted embed file, not in this repo. Never commit keys.
- **Chat privacy.** Questions are sent to the bot and processed by Botpress. The page itself sets no tracking or analytics. The page says this in the chat window and footer.
- **Accounts.** Turn on two-factor authentication for the GitHub and Botpress accounts. That is the main way a site like this gets taken over.
- **Botpress settings to keep.** The bot should have no connected tools or actions, no secrets in its prompt, a message or rate limit, and a spending alert.

## Credits and attribution

Lore is summarized in the maintainer's own words from the Genshin Impact Wiki on Fandom (text under CC BY-SA 3.0, https://creativecommons.org/licenses/by-sa/3.0/). Fonts: Pirata One and Noto Sans (SIL Open Font License). Libraries: GSAP and Lucide icons.

## Status

- Front end: working.
- Bot: connected through Botpress. Answers depend on the knowledge base uploaded there, and some regions and ages are still thin.
- Known gaps are tracked privately and filled in as the knowledge base grows.

## License

No license has been chosen yet, so all rights are reserved by the author for now. The game's names, text and art are not part of this project and are not licensed here.
