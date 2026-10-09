# The Tony Verse Directory

A single-page, dark neon-green cyberpunk hub for the Tony Verse streaming community. The page itself is one file, `index.html`, with images and music in `assets/`. No build step, no dependencies to install.

## What's on the page

| Section | What it does |
|---|---|
| Hero | Site emblem and "Watch Live" button |
| HR Department | Collapsible clip sections |
| Most Recent Streams | Latest stream cards with live view counts |
| Johnny Apple Clipz / Tony Schitzo | Clip-channel sections |
| Channel Stats | Live subscriber and view tiles per channel, with trend history |
| Schedule | Weekly stream schedule table with a "Live" badge |
| The Crew / Reoccurring Guests | Host cards with YouTube, Instagram and TikTok links and copy-to-clipboard Discord handles |
| Tapes / Creator Toolkit | Banner links to the linked tool artifacts |
| Movie Night / Spider-Man Corner | Upcoming movie banner and Marvel section |
| Send a Tip | Streamlabs tip links |
| The Server | Discord invite and live member-count tracker |
| Biography | Click-to-expand story cards |
| Music player | Floating player ("The Tony Verse Directory Mix") |

## Run it

Open `index.html` in any modern browser. For a more realistic test, serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

Live stats, view counts and the Discord tracker need an internet connection. If a request fails, the page keeps the last known values.

## Edit it

- **Text, links and cards:** edit the HTML directly. Each section has an `id` (for example `#crew`, `#schedule`, `#stats`).
- **Stats tiles:** each `.stat-tile` is configured with `data-handle`, `data-channel-id`, `data-last-video-id`, `data-history-key` and `data-poll-ms` (poll interval in milliseconds).
- **Stats history:** the `<script id="stats-history">` JSON block stores dated subscriber/view snapshots used for trends. Keys must match each tile's `data-history-key`.
- **Schedule rows:** each `<tr>` is keyed by `data-history-key` so a host's "Live" badge lights up with their channel.
- **Biographies:** each person is one `<details class="bio-card">` block. Add or remove a whole block to add or remove a person.

## Put it on GitHub Pages

1. Create a new repository on GitHub (for example `tony-verse-directory`) and leave it empty.
2. Upload everything in this folder, keeping the structure below, either by dragging the files into the GitHub web page ("Add file" > "Upload files") or with git:

   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/tony-verse-directory.git
   git push -u origin main
   ```

3. In the repo, go to **Settings > Pages**. Under "Build and deployment", set Source to **Deploy from a branch**, choose branch `main` and folder `/ (root)`, then Save.
4. After a minute or two the site is live at `https://YOUR-USERNAME.github.io/tony-verse-directory/`.

If you want a custom domain, add it under Settings > Pages and point your DNS at GitHub Pages.

## Project structure

```
index.html          the whole site (HTML, CSS and JavaScript)
assets/img/         avatars, portraits and emblem (WebP)
assets/audio/       music player tracks (MP3)
.nojekyll           tells GitHub Pages to serve files as-is
README.md           this file
```

## Things to know

- **API keys are in the page source.** The YouTube Data API keys are in each tile's `data-keys` attribute, so anyone can read them. Restrict them to your site's domain in the Google Cloud Console (HTTP referrer restrictions), or move the calls to a small backend.
- **Large files.** The five music tracks add up to about 10 MB. That is fine for GitHub (100 MB per-file limit), but keep an eye on the repo's total size if you add more.
- **Public CORS relays.** Some requests go through free proxy services (allorigins, corsproxy.io, codetabs, cors.eu.org) as fallbacks. They can be slow or go down; a backend would be more reliable.
- **Emblem artwork.** The hero emblem image is baked in and still shows the older cobra artwork. Replace the `<img>` in the hero section to update it.
- **Removed content.** Houdini's cards, stats, schedule row, bio and tape banner, and all Maximus mentions, were removed from this version.
