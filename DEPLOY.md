# GFN Game Day — going live and staying updated

## Launch checklist (this week)

Do these in order. Nothing below blocks going live — the site looks finished with photos or without.

- [ ] **1. Push the files to GitHub** (Step 1 below, ~10 min)
- [ ] **2. Connect Hostinger to the repo** (Step 2, ~5 min) — site is live at this point
- [ ] **3. Sign in to Pages CMS** (Step 3, ~2 min)
- [ ] **4. Point the domain at the plan + turn on SSL** in hPanel
- [ ] **5. Paste in your real affiliate links** — Tickets and Gear under *Default affiliate links*. Until then those buttons read "Link coming soon" rather than going nowhere.
- [ ] **6. Upload photos as you get them** — four city photos, three travel-card photos, four shop photos. Missing ones show a clean dark panel, so add them whenever.

### Do NOT put these in the repo

`_ds/` and `uploads/` are design-tool scratch space. `GFN Game Day.dc.html` and `Photo Framing Tool.dc.html` are my design sources — harmless to include, but the live site only needs `index.html` and `frame.html`.

---


Three one-time setups, then a simple loop. Repo: `deeonblast/GFN-website`, branch `main`.

```
You or a teammate edit in Pages CMS
        ↓  (saves a commit)
      GitHub repo
        ↓  (webhook)
   Hostinger pulls and serves
        ↓
      Live site
```

---

## Step 1 — Get the files into GitHub

### Easiest route: GitHub Desktop

1. Install **GitHub Desktop** (desktop.github.com) and sign in.
2. **File → Clone repository → GFN-website**. Pick a folder on your computer.
3. Download this project (I can hand you a zip), unzip it, and copy everything into that cloned folder **except** the `_ds` and `uploads` folders — those are design-tool scratch space and are not part of the website.
4. Back in GitHub Desktop you'll see the file list. Type a summary like `Initial site` and click **Commit to main**, then **Push origin**.

That's it — the repo now has the site.

### Alternative: drag and drop in the browser

Go to github.com/deeonblast/GFN-website → **Add file → Upload files** → drag the folders in → **Commit changes**. Works, but folders can be fiddly; Desktop is less error-prone for the first load.

### What has to be in the repo

```
index.html            ← the site itself
support.js            ← runtime it needs
image-slot.js
content/site.json     ← ALL editable content lives here
styles/gfn-ds.css
assets/               ← logo, masthead, uploaded photos
.pages.yml            ← tells Pages CMS what the fields are
GFN Game Day.dc.html  ← design source (optional, harmless to include)
```

---

## Step 2 — Point Hostinger at the repo

In hPanel, open your website dashboard → **Advanced → Git**.

1. Click **Connect with GitHub** and approve the Hostinger GitHub App, granting it access to `GFN-website`.
2. Pick the repository, set the branch to **main**, and leave the install path at the root (`public_html`).
3. Click **Deploy**.

From then on every push to `main` deploys automatically — GitHub pings Hostinger, Hostinger pulls, files are replaced. There is no build step: what's in the repo is exactly what gets served, which is why `index.html` sits at the top level.

If the first pull fails saying the directory isn't empty, clear `public_html` in File Manager and deploy again. If a change doesn't show up, use **Redeploy** on the Git page and clear the Hostinger cache.

---

## Step 3 — Set up the content editor (Pages CMS)

1. Go to **app.pagescms.org** and sign in with GitHub.
2. Grant it access to `deeonblast/GFN-website`.
3. Open the repo in Pages CMS. It reads `.pages.yml` and builds the edit forms automatically — you'll see **GFN Game Day** with sections for Hero, Travel guide cards, Season schedule, Fan shop, and so on.

To add a teammate: give them **write access** to the repo (GitHub → Settings → Collaborators), then they sign in to Pages CMS with their own GitHub account. Nothing to install, works from anywhere.

---

## The update loop

1. Open app.pagescms.org, pick the repo, edit fields.
2. **Save.** That writes a commit to `main`.
3. Hostinger deploys within a minute or two. Refresh the live site.

Every change is version-controlled, so anything can be rolled back from the repo's commit history.

### Rolling over to a new season

1. Change **Season year**.
2. Edit the **Season schedule** entries in place — dates, opponents, venues, overviews. Add or delete rows as needed.
3. Keep the `id` values (`g1`, `g2`…) or update the **Travel guide cards** so their "Opens which game?" still points at a real ID.
4. Update **Season panel text → Heading** ("2027 Season") and the season-over message.
5. Save. Done — the site re-sorts itself and picks the new "Next Up" game automatically.

### Photos

Upload them in Pages CMS itself — any image field has a picker that uploads into `assets/uploads` and commits it.

Pages CMS has no crop tool, so every cropped photo has two fields next to it instead:

- **Photo framing** — which part of the photo to keep when the frame is narrower than the image (center, top, bottom left, and so on). Use this when a subject sits off-center, or a skyline is getting cut off at the top.
- **Photo zoom** — `1` fits the frame; `1.3` zooms in 30%. Combine with framing to crop in tight on something.

Set both, save, look at the live page, adjust. It's a couple of numbers rather than dragging, but unlike a drag it publishes.
 Recommended sizes: city photos 2400 × 920, travel card photos 1200 × 600, masthead 2400 × 900 wide plus a square version for phones, shop photos square.

---

## When I change the design

Content you can change yourself. Design changes (layout, colors, new sections) still come through me. When I make one I regenerate `index.html`; you copy the updated files into your GitHub Desktop folder, commit, push, and Hostinger does the rest.

## Custom domain

Hostinger handles it — point the domain at the hosting plan in hPanel and enable the free SSL certificate. No change to the repo.
