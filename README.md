# Kerala Lottery Results Website

A modern, mobile-friendly, multilingual Kerala lottery results site powered by static files and real historical data.

## Features

- Google Sheets backend for easy editing
- Automated static site generation (HTML/JSON)
- Search, prediction, and scanner tools
- Beautiful, responsive UI with language support
- Fully automated publishing with GitHub Actions

## Workflow

1. **Edit results** in Google Sheets.
2. **Export or fetch** latest results as HTML into `githublotery/note/`.
3. **Run** `node generate-history.js` in `githublotery/` to update `history.json`.
4. **Push** changes to GitHub.
5. **GitHub Actions** auto-generates and deploys the site.

## Local Development

```sh
cd githublotery
node generate-history.js
# Open index.html in your browser
```

## Deployment

- All files in `githublotery/` are published as a static site (e.g., via GitHub Pages).
- The workflow in `.github/workflows/build-and-deploy.yml` automates build and deployment.
- Daily scraping can run automatically through `.github/workflows/fetch.yml`.

## Automated Daily Fetch (GitHub Actions)

1. Keep your repository on GitHub (public repos stay within free minutes easily).
2. Ensure `requirements.txt` and `package-lock.json` are up to date so the workflow installs dependencies cleanly.
3. (Optional) Add `SCRAPERAPI_KEY` / `SCRAPERAPI_ENDPOINT` in **Repo Settings → Secrets and variables → Actions** if you use a proxy.
4. The `fetch.yml` workflow runs every day at **16:45 IST (11:15 UTC)** or whenever you trigger it manually via **Actions → Run workflow**.
5. On each run it executes `python updateloto.py`, regenerates `history.json`, and commits/pushes changes back using the built-in `GITHUB_TOKEN`.

## Folder Structure

```
your-repo/
│
├─ githublotery/
│   ├─ index.html
│   ├─ prediction.html
│   ├─ search.html
│   ├─ scanner.html
│   ├─ resultgen3.html
│   ├─ history.json
│   ├─ generate-history.js
│   ├─ note/
│   │   └─ [draw HTML files...]
│   └─ [other assets, e.g. CSS, images, etc.]
│
├─ .github/
│   └─ workflows/
│       └─ build-and-deploy.yml
│
├─ README.md
└─ [other project files]
```

## License

MIT 