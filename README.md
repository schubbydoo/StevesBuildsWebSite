# Steve's Builds — site + admin

Live site: **https://stevesbuildswebsite.shschubert.workers.dev**
Admin (bookmark this): **https://stevesbuildswebsite.shschubert.workers.dev/admin/**
Image framing tool (bookmark this too): **https://stevesbuildswebsite.shschubert.workers.dev/admin/image-tool.html**
GitHub repo: **https://github.com/schubbydoo/StevesBuildsWebSite**

## The two-minute version

Everything below is detail for reference. Day to day, this is the whole workflow:

1. Open `/admin/`.
2. Edit "Contact info" or "Homepage projects."
3. Click **Publish**.
4. Wait about a minute — the site rebuilds and updates itself automatically.

No files to download, no git, no manual uploads.

## What's in this repo

- `index.html` — the live site. Loads `profile.json` and `projects.json` at page load and renders everything from them.
- `profile.json` — your name, photo, email, and social links (shown in the bar at the top of the site).
- `projects.json` — the list of projects (title, description, categories, video, cover image, links). This is the bulk of the site's content.
- `admin/index.html` + `admin/config.yml` — Sveltia CMS, a real content-management tool pointed at this GitHub repo. This is what renders the `/admin/` page.
- `admin/image-tool.html` — a standalone helper for framing photos (project covers or your contact photo) before uploading them. Not part of the CMS itself, just a prep tool.
- `admin/uploads/` — where photos you upload through the CMS actually live.
- `images/` — a couple of static site assets that aren't managed through the CMS.
- `wrangler.jsonc` — tells Cloudflare this is a plain static site (no build step).
- `.assetsignore` — keeps `.git` and build artifacts out of the publicly deployed files.

## Editing content

### Contact info

In `/admin/`, under **Contact info**: your name, photo, email, and social links.

- **Photo**: upload directly, or use the image framing tool first (see below) to size and position it exactly how you want before uploading.
- **Social links**: add one entry per platform (label + URL). Leave this empty and the site shows three faint dashed placeholder circles reserving the space; add entries and they become real clickable links automatically — no code changes ever needed for this.

### Homepage projects

In `/admin/`, under **Homepage projects → Project list**, each project has:

- **Title / Description** — the basics.
- **Categories** — free-typed tags (Animatronics, Video, Audio, Interactive, AI, Writing, or anything new you type). These automatically build the "Highlight" pill row at the top of the site — no config changes needed to add a new category, just type it on any project.
- **YouTube video URL** — paste the full link. Leave blank if there's no video.
- **Cover image** — optional. If set, this photo becomes the tile's thumbnail instead of the YouTube auto-thumbnail. If the project also has a video, the tile still plays the video when clicked (a small play icon overlays the photo as a hint).
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

## Site features, briefly

- **Video playback**: clicking any tile with a video opens it in an on-page overlay (no new tab). Esc, the × button, or clicking outside closes it.
- **Category highlighting**: clicking a pill in the "Highlight" row scrolls to the first matching project, gives every matching tile a green glow, and dims everything else — nothing is hidden, just visually called out. Click the same pill again, or the "✕ clear" pill, to reset.
- **External links** (no video): shown with a small external-link icon instead of a broken-looking blank thumbnail.

## How publishing actually works

Clicking Publish in `/admin/` uses a GitHub token stored in your browser to commit directly to this repo (no server of mine involved). That push triggers Cloudflare's GitHub integration, which rebuilds and redeploys the site automatically, usually live within a minute or two.

**If a change doesn't show up after a few minutes**: open the Cloudflare dashboard → Workers & Pages → `stevesbuildswebsite` → **Deployments** tab, and check "Recent builds." If one shows an error or timeout, click its "···" menu → **Retry build**. This has happened once before (an infrastructure hiccup, not a real config problem) and a retry fixed it immediately.

## Signing into /admin on a new device

Click "Sign In with Token" → it opens a GitHub page with the right permissions pre-selected → generate a token → copy it → paste it into the CMS prompt. The token is stored only in that browser. You can revoke any token anytime from GitHub → Settings → Developer settings → Personal access tokens.

## Getting a YouTube video ID or URL

Just copy the full address bar URL from YouTube, e.g. `https://www.youtube.com/watch?v=CFMEgACaiTo` — paste the whole thing into the "YouTube video URL" field.

## Custom domain

Not set up yet. Whenever you want something other than the `.workers.dev` address, it's a one-time addition in the Cloudflare project's domain settings — ask me and I'll walk through it.
