# Steve's Builds — site + admin

## Files

- `index.html` — the live site. Fetches `projects.json` at load time and renders the project grid.
- `projects.json` — the project content (title, description, video, links). This is what you'll actually edit day to day, through the admin page below.
- `admin/index.html` + `admin/config.yml` — a real content-management page (Sveltia CMS) pointed at your GitHub repo. This is the bookmarkable "log in, edit, hit Publish" page.

## One-time setup

### 1. Get the files into your GitHub repo

Repo: `https://github.com/schubbydoo/StevesBuildsWebSite`

Easiest way, no git required: on the repo's GitHub page, click "Add file" → "Upload files", then drag in `index.html` and `projects.json`. Then create the `admin` folder the same way — GitHub lets you type `admin/index.html` as the filename when uploading/creating a file, which creates the folder automatically. Do the same for `admin/config.yml`.

(If you'd rather use git directly, clone the repo, copy all four files into it preserving the `admin/` folder, then `git add . && git commit -m "initial site" && git push`.)

### 2. Connect Cloudflare Pages

1. In the Cloudflare dashboard, go to Workers & Pages → Create → Pages → Connect to Git.
2. Select the `StevesBuildsWebSite` repo.
3. Build settings: framework preset "None", build command blank, build output directory `/`.
4. Save and deploy. Cloudflare gives you a `*.pages.dev` URL — that's your live site.

### 3. Log into the admin page

1. Go to `https://<your-site>.pages.dev/admin/` and bookmark it.
2. Click "Sign In with Token."
3. It'll link you to a GitHub page with the right permissions pre-selected — generate the token, copy it, and paste it back into the CMS prompt.
4. You're in. This only stores the token in your browser, so you'll do this once per browser/device you use.

## Ongoing workflow (this is the part you'll actually use)

1. Open your bookmarked `/admin/` page.
2. Click into "Homepage projects" → "Project list."
3. Add, edit, delete, or reorder projects in the form.
4. Click Publish.

That's it — Publish commits straight to GitHub, and Cloudflare redeploys automatically, usually live within a minute. No downloading files, no manual uploads, no git.

## Getting a YouTube video ID

From a video URL like `https://www.youtube.com/watch?v=CFMEgACaiTo`, the ID is the part after `v=` — here, `CFMEgACaiTo`.

## Notes

- `admin/uploads` is set up as a media folder in case you ever want to add an image field (e.g. project photos) later — nothing needs to be there now.
- If you want a custom domain instead of `*.pages.dev`, that's a one-time addition in the Cloudflare Pages project settings whenever you're ready.
