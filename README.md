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

## Theme (dark / light)

The 🌙/☀️ button in the header (every page) toggles `data-theme="dark"|"light"` on `<html>`. **Dark is the default** — a page loads dark unless the visitor has explicitly switched to light before (stored in `localStorage` under `m1-theme`). The toggle logic lives in `page-transitions.js` (loaded in `<head>` on every page, so the theme applies before first paint, avoiding a flash).

Colors are driven by CSS custom properties in `styles.css` (`--paper`, `--lilac`, `--white`, `--line`, `--muted`, `--text`), overridden under `:root[data-theme="dark"]` using the same dark purple (`#170D28`) as the hero photo background, for visual continuity. A few hero-only elements (the floating station chips, the ghost button, the mobile bullet cards) sit permanently on the hero's dark photo and are intentionally pinned to fixed white/dark colors instead of the theme variables — don't route those through `--white`/`--text` if you touch them.

## Home page — Projects & Content Worlds

- **Projects** section: links out to the other Moral family projects (Moral4Good, Moral Together, Stage of Stars, Trust Moms, God's Will Ambassador). Projects without a live URL yet (Trust Moms App, Best News, VVIP, World Wide Event Production) are shown as "Coming soon" placeholders — do not invent URLs for these until the client supplies them.
- **Content Worlds** section: live broadcast, VOD, and the themed Moral channels (Kids, Teens, Seniors, Sport, Environment, Animals, Young Ambassadors, Neighborhoods). These currently link to the general channels page until dedicated channel pages exist.

## What's still placeholder (waiting on the client)

- App store links; Instagram / YouTube / WhatsApp socials (Facebook is live — see the footer and header social icon).
- Server-side form submission (currently a client-side success state).
- Real host and studio photos (except the hero, see below), real station logos, host names.

## Assets

`assets/` — logo, photo placeholders (`placeholders/`), app screenshots (`app/`). Once real media is available, just replace the files — the layout doesn't need to change.

The main hero background and the round host photo (`index.html`) use real TV-studio stock photos from Pexels (`assets/placeholders/backgrounds/bg-04-tv-camera-studio.jpg`, `assets/placeholders/people/person-06-smiling-tv-host.jpg` — see `assets/placeholders/README.md` for sourcing), replacing the earlier podcast-themed placeholders to match the Moral **TV** branding. The round photo is color-graded via CSS (`.disc-ph` filter + `.disc::after` overlay in `styles.css`) to match the background's blue-violet/magenta palette.

## Footer

Beyond navigation, the footer links to the other Moral family sites ("האתרים שלנו") and to each Moral channel's own Facebook page ("פייסבוק · ערוצי מורל"). Update these two columns (identical markup on all 9 pages) if a channel's Facebook page changes or a new one launches.
