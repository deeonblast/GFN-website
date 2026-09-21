repo: deeonblast/GFN-website
branch: main

## Last sync
date: 2026-09-20T00:00:00Z
note: Repo is the deployment source. Hostinger (hPanel → Advanced → Git) pulls `main` on every push and serves it as-is — no build step, so `index.html` must sit at the repo root. Content is edited through Pages CMS (app.pagescms.org), which reads `.pages.yml` and commits to `main`.

### Updated in this project
- All site copy, schedule, affiliate links and images moved out of code into `content/site.json`
- Site now fetches that JSON at load; removed the localStorage trip system entirely
- Added `.pages.yml` so Pages CMS generates the edit forms
- Added `index.html` (generated copy of the DC) and `DEPLOY.md`
- Added `frame.html` — a drag/zoom photo framing tool that outputs publishable framing values

## Screen map
| Project screen | Repo files |
| --- | --- |
| Home (hero, travel guides, shop, broadcast) | index.html, content/site.json, styles/gfn-ds.css |
| Season schedule + game plan | index.html, content/site.json |
| Photo framing tool | frame.html, Photo Framing Tool.dc.html |
| Content editor forms | .pages.yml |
