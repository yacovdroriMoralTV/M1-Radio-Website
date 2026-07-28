# Moral TV — Website

Public website for **Moral TV** (Moral Together): live broadcast channels (radio + video), 24/7.
Channel = host: the main channel is the live broadcast, other channels are themed with their own host.

**How to open:** open `index.html` in a browser — the site works straight from disk, no build needed.

---

## Stack

Static site: HTML + CSS + JS, no framework. Rubik font, RTL (Hebrew).
The site only **reads** data from the public API (station catalog, blog posts) and never writes. If the API is unavailable, a built-in data snapshot is used, so the page always works.

## Pages

| File | Section |
|---|---|
| `index.html` | Home |
| `stations.html` | Channels — player (radio / video) + station grid |
| `hosts.html` | Hosts |
| `blog.html` | מה חדש — News / blog |
| `about.html` | About |
| `ads.html` | Advertising — inquiry form |
| `apps.html` | App |

Menu: `דף הבית · ערוצים · פרויקטים · שדרנים · מה חדש · אפליקציה · אודות · פרסום`.

## Data

- **Stations** — public API `GET /api/public/stations?type=radio`. Station key is `slug`, audio stream in `stream_url`, video follows the pattern `{slug}/index.m3u8`. Logos are picked up from `logo_url` as soon as real ones are uploaded in the admin panel.
- **Blog** — `GET /api/v1/posts` (no posts yet — sample articles are shown in the exact format of the future API; once real posts exist they will replace them automatically).
- The catalog is edited only in the admin panel; the site and app only read it.

## Player

Clicking a station starts the live stream; at the bottom is a player dock (play/pause, volume, status). On the "Channels" page there's a "theater" player with a radio/video switch (video via HLS, hls.js).

## Home page — Projects & Content Worlds

- **Projects** section: links out to the other Moral family projects (Moral4Good, Moral Together, Stage of Stars, Trust Moms, God's Will Ambassador). Projects without a live URL yet (Trust Moms App, Best News, VVIP, World Wide Event Production) are shown as "Coming soon" placeholders — do not invent URLs for these until the client supplies them.
- **Content Worlds** section: live broadcast, VOD, and the themed Moral channels (Kids, Teens, Seniors, Sport, Environment, Animals, Young Ambassadors, Neighborhoods). These currently link to the general channels page until dedicated channel pages exist.

## What's still placeholder (waiting on the client)

- App store / social media links, privacy policy page (text exists).
- Server-side form submission (currently a client-side success state).
- Real host and studio photos, real station logos, host names.

## Assets

`assets/` — logo, photo placeholders (`placeholders/`), app screenshots (`app/`). Once real media is available, just replace the files — the layout doesn't need to change.
