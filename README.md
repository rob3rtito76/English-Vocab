# Lexicon — deployment guide

A spaced-repetition vocabulary trainer for English words and phrases. Runs entirely in the browser, stores your progress on-device, and installs to your iPad's Home Screen as a real app.

## What you have

Five files. That's the entire app.

```
index.html       ← the app itself (HTML + React + styling, all inline)
manifest.json    ← tells iPad it's an installable app
sw.js            ← service worker — makes it work offline after first load
icon.svg         ← the home-screen icon
README.md        ← this file
```

No build step. No `npm install`. No server. Open `index.html` in any modern browser and it just runs.

## Deploying to GitHub Pages

### 1. Create the repository

On github.com, click **New repository**.
- **Name:** anything you like (e.g., `lexicon`).
- **Public** — Pages requires it on the free plan.
- Tick **Add a README file** so the repo isn't empty.
- Click **Create**.

### 2. Upload the files

In your new repo, click **Add file → Upload files**.

Drag in all five files from this folder:
- `index.html`
- `manifest.json`
- `sw.js`
- `icon.svg`
- `README.md` (will replace the auto-generated one)

Scroll down, click **Commit changes**.

### 3. Turn on Pages

In the repo, go to **Settings → Pages** (left sidebar).
- Under **Source**, choose **Deploy from a branch**.
- Branch: **main**, folder: **/ (root)**.
- Click **Save**.

Wait about a minute. The page will refresh and show a green box with your URL — something like:

```
https://YOUR-USERNAME.github.io/lexicon/
```

### 4. Install it on your iPad

1. Open Safari on your iPad.
2. Go to your GitHub Pages URL.
3. Tap the **Share** button (the square with an up-arrow).
4. Scroll down and tap **Add to Home Screen**.
5. Name it (or keep "Lexicon"), tap **Add**.

Now you have an icon on your Home Screen. Tap it — the app launches full-screen, no Safari chrome, no address bar. It works offline. Your progress is saved on the iPad.

## Updating the app later

When you change a file (e.g., add words to the seed list inside `index.html`):

1. In your GitHub repo, click the file name.
2. Click the pencil icon (edit).
3. Make your changes, scroll down, **Commit changes**.

Pages rebuilds automatically in about a minute. On your iPad, close the app fully (swipe up from the dock and flick it away) and reopen — the service worker will pick up the new version.

## Troubleshooting

**"It just shows a 404 on GitHub Pages."** Pages takes 1–2 minutes after first enabling. Refresh in a minute. If it persists, check Settings → Pages and verify the branch is `main` and the folder is `/ (root)`.

**"It loads but the page is blank."** Open Safari's Web Inspector (Settings → Safari → Advanced → Web Inspector, then connect to a Mac), or just try a different network — most likely the CDN scripts (Tailwind, React) are being blocked. The app needs internet on first load.

**"Add to Home Screen doesn't show up."** That option only appears in **Safari**, not Chrome on iPad. Use Safari for the install step. After installing, the app itself works regardless.

**"My words disappeared after I cleared Safari data."** Progress is stored in the browser's localStorage. Clearing site data wipes it. If you want sync across devices later, that's a Supabase or Firebase add-on — see the roadmap.

## What's next

If/when you want to extend it:
- **Auto-fill word data** from the [Free Dictionary API](https://dictionaryapi.dev/) when adding new words.
- **Better pronunciation** via the ElevenLabs API (replace the `speak()` function).
- **Cross-device sync** via Supabase (free tier, ~50 lines of code to add).
- **Import from Kindle highlights** — paste in a `.txt` export and bulk-add.
- **Cloze deletion mode** — show the example with the word blanked out.
