# Publish this repository to GitHub

This folder contains a complete, commit-ready project (interactive site at the root, plus
`data/`, `docs/`, `build/`, `scripts/`). Publishing it takes about two minutes. Pick whichever
path you prefer.

> Heads-up on size: the largest files are `data/school_year_panel.csv` (~8.6 MB),
> `data/elwr_school_year_wide.csv` (~6.7 MB) and `data.js` (~3.4 MB) — all well within GitHub's
> limits. The ~12 GB of raw source data is intentionally excluded (see `.gitignore` and the
> README's "Data sources").

## Option A — GitHub Desktop (easiest, no terminal)

1. **GitHub Desktop → File → Add local repository…**, choose this folder.
2. If it says the folder isn't a Git repository yet, click **“create a repository”** (Desktop
   sets it up for you; this folder already includes a `.gitignore` and `LICENSE`).
3. Click **Publish repository**. Untick "Keep this code private" if you want it public.
4. Continue to **Enable GitHub Pages** below.

## Option B — Command line

1. On https://github.com create a **new, empty** repository (do **not** add a README,
   .gitignore, or license — this folder already has them). Copy its URL.
2. In a terminal, from inside this folder:

   ```bash
   git init
   git add -A
   git commit -m "Initial commit: UC merit admissions explorer + data pipeline"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<your-repo>.git
   git push -u origin main
   ```

   Over HTTPS, GitHub asks for your username and a **Personal Access Token**
   (Settings → Developer settings → Personal access tokens), not your account password.
   Or use an SSH remote: `git@github.com:<you>/<repo>.git`.

## Enable GitHub Pages (publishes the interactive site)

1. Repo page → **Settings → Pages**.
2. **Build and deployment → Source: “Deploy from a branch”**, **Branch: `main`**,
   **Folder: `/ (root)`**, then **Save**.
3. After ~1 minute the explorer is live at `https://<your-username>.github.io/<your-repo>/`.
4. Paste that URL into the README's "Live site" line and commit it, so visitors can find it.

## Updating later

```bash
python3 scripts/make_site_data.py        # only if the curated data changed
git add -A && git commit -m "Update" && git push
```
