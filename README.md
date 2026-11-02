# 🗂 Folder Sorter

Sort a messy folder of photos and videos into tidy folders, and watch it happen: every file is pulled into a vortex, then fired out to the folder it belongs in.

Single static page. No build step, no server, no dependencies. Your files are read in the browser and never uploaded.

**Live demo:** https://guruprksh.github.io/folder-sorter/ (after you enable GitHub Pages, see [Deploy](#deploy-to-github-pages))

> Add a screenshot or GIF here: `docs/screenshot.png`

## Features

- **Vortex animation:** files spiral in a tornado, then shoot along curved paths to labels placed around it.
- **Whole-folder selection:** pick a folder and every subfolder is scanned (up to 6 levels deep).
- **Claude vision (optional):** Claude first looks at a sample and designs folders that fit *your* library, then files every item. Unclear items go to "Other".
- **Works without AI:** screenshots, documents, videos by length and photos by month.
- **Exact-duplicate finder:** duplicates go to a review folder, never deleted.
- **Preview:** hover a file or thumbnail to see it larger; click a thumbnail to move it to another folder before applying.
- **Apply to your folder, safely:** preview only, copy into `Sorted/`, or move into `Sorted/`, with an undo. Optional grouping by month.
- **Move script:** for browsers that cannot write to folders, copy a generated `sort.sh`.
- **Google Drive / OneDrive:** pick the synced folder on your computer (Drive for desktop, OneDrive app) and changes sync by themselves.

## Quick start

Open `index.html` in a browser, or serve it locally (needed for direct folder access, which requires a secure context; `localhost` counts):

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Click **Try with sample files** to see the animation without using your own files.

## Browser support

| Feature | Chrome / Edge (desktop) | Firefox / Safari |
| --- | --- | --- |
| Sorting, animation, preview | Yes | Yes |
| Pick a folder and apply changes directly | Yes | No (use the move script) |

## Run it on your own computer

You need a browser (Chrome or Edge for direct folder access) and any way to serve static files. Opening `index.html` by double-click works for sorting and the move script, but direct folder access needs a secure context, so serve it from `localhost`.

```bash
git clone https://github.com/guruprksh/folder-sorter.git
cd folder-sorter

# pick one
python3 -m http.server 8000     # Python 3
npx serve .                     # Node.js
php -S localhost:8000           # PHP
```

Then open <http://localhost:8000>. Press **Try with sample files** first, then **Pick a folder to sort & apply**. On Windows use `python` instead of `python3` if needed.

## Using Claude vision

Tick **✨ Claude vision**. If you have not connected yet, the page opens a box asking for an **Anthropic API key** from [console.anthropic.com](https://console.anthropic.com). Paste it, press Enable, and the vision step runs.

**Why a key and not "Sign in with Claude"?** A Claude.ai login (Free, Pro or Max) is for Claude.ai and Claude Code only. As of this writing Anthropic's terms do not allow third-party apps to use consumer-subscription logins, and there is no sign-in flow for outside apps, so an API key is the supported way. Check Anthropic's current docs, since this can change. If a sanctioned sign-in option appears, it would replace `apiShim()` in `index.html`.

If someone opens the app as a claude.ai artifact instead, Claude vision runs on that viewer's own Claude account with no key, because the page is hosted by Claude.ai itself.

- The key is held in memory for the tab only; it is never saved or sent anywhere except `api.anthropic.com`.
- 512 px previews of your photos (and one frame per video) are sent in batches to be classified. Original files never leave your device.
- You pay for your own API usage. Use a key with a spend limit.
- Models are set by `MODEL` and `MODEL_QUICK` near the top of the key-handling code in `index.html`.

Because the key is typed into a web page, never host a version with a key baked in.

## Applying changes

After sorting you choose what happens to your folder:

1. **Preview only** (default): nothing is touched.
2. **Copy into `Sorted/`:** originals stay where they are.
3. **Move into `Sorted/`:** changes your folder. Each file is copied first and removed only after the copy succeeds, existing files are never overwritten (`name (2).jpg`), nothing is deleted, and **Undo last apply** puts files back.

Duplicates go to `Sorted/Duplicates (review)`. Try it on a small copy of a folder first.

## Deploy to GitHub Pages

1. Create a repository (for example `folder-sorter`) and push these files to `main`.
2. In the repository go to **Settings → Pages** and set **Source** to **GitHub Actions**.
3. The included workflow (`.github/workflows/pages.yml`) publishes the site on every push to `main`.

Your site will be at `https://<your-username>.github.io/<repo-name>/`.

## How it works

See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md). In short: scan → look → match duplicates → file.

## Privacy

See [docs/PRIVACY.md](docs/PRIVACY.md).

## Roadmap

- Download `sort.sh` / PowerShell script and a CSV plan
- Near-duplicate detection (burst shots, edited copies)
- Rename by date and folder
- Group by place when location data exists
- Remember your corrections and reuse them

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Security issues: [SECURITY.md](SECURITY.md).

## License

[MIT](LICENSE)
