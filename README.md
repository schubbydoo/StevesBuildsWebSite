# Strange Machine Labs — site + admin

Live site: **https://strangemachinelabs.com**
Admin (bookmark this): **https://strangemachinelabs.com/admin/**
Image framing tool (bookmark this too): **https://strangemachinelabs.com/admin/image-tool.html**
Business card / print (bookmark this too): **https://strangemachinelabs.com/admin/business-card.html**
GitHub repo: **https://github.com/schubbydoo/StevesBuildsWebSite**

The original `https://stevesbuildswebsite.shschubert.workers.dev` address still works too — `strangemachinelabs.com` is just a friendlier custom domain pointed at the same site.

## The two-minute version

Everything below is detail for reference. Day to day, this is the whole workflow:

1. Open `/admin/`.
2. Edit "Homepage header," "Contact info," or "Homepage projects."
3. Click **Publish**.
4. Wait about a minute — the site rebuilds and updates itself automatically.

No files to download, no git, no manual uploads.

## What's in this repo

- `index.html` — the live site. Loads `hero.json`, `profile.json`, and `projects.json` at page load and renders everything from them.
- `hero.json` — the pill tag, headline, and subtitle at the very top of the site.
- `profile.json` — your name, photo, email, and social links (shown in the bar at the top of the site).
- `projects.json` — the list of projects (title, description, categories, video, cover image, links). This is the bulk of the site's content.
- `admin/index.html` + `admin/config.yml` — Sveltia CMS, a real content-management tool pointed at this GitHub repo. This is what renders the `/admin/` page.
- `admin/image-tool.html` — a standalone helper for framing photos (project covers or your contact photo) before uploading them. Not part of the CMS itself, just a prep tool.
- `admin/business-card.html` — a standalone page that renders your business card (pulled live from `profile.json`) and prints it at exact business-card size. Not part of the CMS itself, just a tool.
- `admin/uploads/` — where photos you upload through the CMS actually live.
- `images/` — static site assets not managed through the CMS: the homepage/business-card logo and a couple of unused legacy files.
- `wrangler.jsonc` — tells Cloudflare this is a plain static site (no build step).
- `.assetsignore` — keeps `.git` and build artifacts out of the publicly deployed files.

## Editing content

### Homepage header

In `/admin/`, under **Homepage header**: a single **Logo** image field — this is the big logo graphic at the very top of the site.

- Upload a **PNG with a transparent background**. It should be just the artwork (no rectangle, card, or colored box behind it) so it sits directly on the site's dark background with no visible seam.
- It's centered automatically, and sized responsively — full-width on mobile, about half the content width on desktop.
- The old text-based header (pill tag + headline + subtitle) was replaced by this logo. The underlying fields changed to match — if you ever want to go back to a text headline instead of a logo, ask me and I'll swap the field type and the site code back.

### Contact info

In `/admin/`, under **Contact info**: your name, photo, email, phone, and social links.

- **Photo**: upload directly, or use the image framing tool first (see below) to size and position it exactly how you want before uploading. Shown at the top of the site alongside your name — click it (or the "Click to contact" line under it) to pop up your business card.
- **Email**: not shown directly on the site anymore — it only appears inside the business card popup.
- **Phone**: optional. Also only shows up on the business card.
- **Social links**: six fixed platforms (Instagram, Facebook, YouTube, TikTok, X/Twitter, LinkedIn), each with a "Show icon" checkbox and a URL box. Check the box and add a URL to make that platform's icon appear on the business card; unchecking hides it again without losing the saved URL. Adding a brand-new platform beyond these six means asking me to add a field for it — this list isn't open-ended the way project categories are.

This same info also feeds your **business card** (see below) — update it once here and both the site and the card stay in sync.

### Homepage projects

In `/admin/`, under **Homepage projects → Project list**, each project has:

- **Title / Description** — the basics.
- **Categories** — free-typed tags (Animatronics, Video, Audio, Interactive, AI, Writing, or anything new you type). These automatically build the "Highlight" pill row at the top of the site — no config changes needed to add a new category, just type it on any project.
- **YouTube video URL** — paste the full link. Leave blank if there's no video.
- **Cover image** — optional. If set, this photo becomes the tile's thumbnail instead of the YouTube auto-thumbnail. If the project also has a video, the tile still plays the video when clicked.
- **Cover image framing** — top/center/bottom, for nudging which part of a photo stays visible when it's cropped to the tile's wide shape. If you use the image framing tool to pre-compose the photo, you can usually just leave this on "center."
- **External link URL / label** — for anything that isn't a video (the book's Amazon link, a link to the original project you built on, etc.).

**Reordering**: each project row has up/down arrows near its header to move it one spot at a time. For a big jump, ask me directly and I can reorder the underlying file in one shot rather than many clicks.

### Image framing tool

`/admin/image-tool.html` solves "I want to size and position this photo exactly, with black bars if it doesn't fill the frame."

1. Choose a **Frame**: "Project card (wide)" or "Contact photo (circle)."
2. Load a photo.
3. Drag it around, use the zoom slider to size it.
4. In circle mode, a dashed guide shows exactly what the round photo mask will keep.
5. Click **Download finished image** — it's already composed pixel-for-pixel.
6. Upload that downloaded file through the matching Cover image / Photo button in `/admin/`.

### Business card

Two ways to see it:

- **On the live site**: click your photo at the top of the site — it pops up a business card in the same on-page overlay style as the video player.
- **In `/admin/`**: open `/admin/business-card.html` (bookmark it) for a print-ready version with a **Print business card** button. It's sized to print at exactly 3.5" × 2" (standard US business card). In the print dialog, either print directly to a compatible printer/cardstock, or choose "Save as PDF" to get a file you can send to a print shop.

Both versions pull live from **Contact info** — name, photo, email, phone, website, and whichever social icons are enabled. Update your info once in `/admin/` and both the on-site card and the print page reflect it (reload the print page to see the update there). Email, phone, and the website line are all clickable/tappable on the card. The card uses the full homepage logo image — if you ever swap the logo in **Homepage header** to something new, ask me and I'll update the card to match (it's a separate hardcoded reference, not automatically linked).

## Site features, briefly

- **Video playback**: clicking any tile with a video opens it in an on-page overlay (no new tab). Esc, the × button, or clicking outside closes it.
- **Category highlighting**: clicking a pill in the "Highlight" row scrolls to the first matching project, gives every matching tile a green glow, and dims everything else — nothing is hidden, just visually called out. Click the same pill again, or the "✕ clear" pill, to reset.
- **External links** (no video): shown with a small external-link icon instead of a broken-looking blank thumbnail.
- **Coming Soon**: a project with neither a video nor a link opens a "Coming Soon" overlay when clicked, instead of doing nothing or jumping the page around.
- **Top bar layout**: your photo/name (left), the logo (center), and a QR code (right) sit in one row at the top of the site, vertically centered together. On mobile they stack instead, since there's not enough width to sit side by side.
- **QR code**: encodes `https://strangemachinelabs.com`, so visitors can share the site with a friend on the spot. It's hardcoded into `index.html` (not CMS-managed) since it never needs to change — ask me if you ever want it pointed at a different URL.
- **Business card popup**: click your photo (or the "Click to contact" line under it) to see your business card in an on-page overlay. See "Business card" above for the print version.

## How publishing actually works

Clicking Publish in `/admin/` uses a GitHub token stored in your browser to commit directly to this repo (no server of mine involved). That push triggers Cloudflare's GitHub integration, which rebuilds and redeploys the site automatically, usually live within a minute or two.

**If a change doesn't show up after a few minutes**: open the Cloudflare dashboard → Workers & Pages → `stevesbuildswebsite` → **Deployments** tab, and check "Recent builds." If one shows an error or timeout, click its "···" menu → **Retry build**. This has happened once before (an infrastructure hiccup, not a real config problem) and a retry fixed it immediately.

## Signing into /admin on a new device

Click "Sign In with Token" → it opens a GitHub page with the right permissions pre-selected → generate a token → copy it → paste it into the CMS prompt. The token is stored only in that browser. You can revoke any token anytime from GitHub → Settings → Developer settings → Personal access tokens.

## Getting a YouTube video ID or URL

Just copy the full address bar URL from YouTube, e.g. `https://www.youtube.com/watch?v=CFMEgACaiTo` — paste the whole thing into the "YouTube video URL" field.

## Custom domain

Set up: `strangemachinelabs.com` is registered through Cloudflare Registrar and added as a Custom Domain on the `stevesbuildswebsite` Worker (Workers & Pages → stevesbuildswebsite → Domains). SSL is handled automatically by Cloudflare. The underlying Worker project name (`stevesbuildswebsite`) didn't change — only the domain pointing at it did.
