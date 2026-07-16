# JupyterLite Site

A JupyterLite deployment that runs Jupyter notebooks entirely in the browser (via Pyodide/WASM) — no backend server needed. Good fit for Moodle courses since students just need a link.

## Repo layout

```
jupyterlite-site/
├── content/                     ← put your .ipynb notebooks here (any subfolders OK)
├── requirements.txt              ← build-time Python deps
├── jupyter_lite_config.json      ← tells the builder where content lives
└── .github/workflows/deploy.yml  ← auto-builds & deploys to GitHub Pages
```

## 1. Add your notebooks

Drop your `.ipynb` files (and any data files they need) into `content/`. Subfolders are preserved
in the final site, so you can organize by week/topic.

## 2. Push to GitHub

```bash
cd jupyterlite-site
git init
git add .
git commit -m "Initial JupyterLite site"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

## 3. Enable GitHub Pages (Actions-based)

In your GitHub repo: **Settings → Pages → Build and deployment → Source → GitHub Actions**.

That's it — the workflow in `.github/workflows/deploy.yml` will run automatically on every push
to `main`, build the site with `jupyter lite build`, and publish it.

Watch progress under the **Actions** tab. First build usually takes 2-4 minutes.

## 4. Get your URL

Once the workflow finishes, your site is live at:

```
https://<your-username>.github.io/<your-repo>/
```

(Check **Settings → Pages** for the exact URL — it's shown there once deployed.)

## 5. Add the URL to Moodle

In your Moodle course: **Add an activity or resource → URL**, paste the GitHub Pages link above,
give it a name (e.g. "Interactive Notebooks"), and save. Students click it and the notebooks load
and run right in their browser — nothing to install.

## Updating later

Just add/edit notebooks in `content/`, commit, and push to `main` — the site rebuilds and
redeploys automatically.

## Testing locally before pushing (optional)

```bash
pip install -r requirements.txt
jupyter lite build --contents content --output-dir dist
jupyter lite serve --output-dir dist
```

Then open the printed `localhost` URL to preview exactly what students will see.
