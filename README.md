# Amazon Listing Optimizer

A single-file, Claude-powered tool for the July 2026 Amazon 75-character title policy. Upload a product photo,
paste your current title/bullets and hero keywords (with search volume + relevancy), and Claude drafts:

- 5 title options (≤ 75 characters, including spaces)
- 3 Item Highlights options (≤ 125 characters, comma-separated phrases)
- 5 revamped bullet points (≤ 250 characters each, headline + natural supporting sentence)
- 1 product description (≤ 1000 characters, keyword-reinforcing, Alexa-for-Shopping aware)

You pick your favorite title/highlights, tweak the bullets and description inline, and see it all assembled in a
live preview panel. Nothing is ever submitted to Amazon — this only produces copy for you to paste into Seller
Central yourself.

## How it works

This is a single `index.html` file — no build step, no server, no framework. It calls the Anthropic API
(`api.anthropic.com/v1/messages`) directly from your browser using the `anthropic-dangerous-direct-browser-access`
header.

**About your API key:** there's no backend to hide it behind, so you paste your key into the box at the top of the
page and click Save. It's stored only in your browser's `localStorage` — it is never written into this file, never
committed to the repo, and is sent only to `api.anthropic.com`. Anyone using this page in their own browser needs to
paste in their own key.

## Running it

Just open `index.html` in a browser — double-click it, or drag it into a browser tab. That's it.

## Hosting it on GitHub

1. Push this folder to a new GitHub repository:

   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin <your-repo-url>
   git push -u origin main
   ```
2. To use it as a live web page (instead of opening the file locally), enable **GitHub Pages**:
   - On GitHub, go to your repo → **Settings** → **Pages**.
   - Under "Build and deployment", set Source to **Deploy from a branch**, branch **main**, folder **/(root)**.
   - Save. GitHub will give you a URL like `https://<username>.github.io/<repo>/`.
3. Open that URL, paste your Anthropic API key into the box at the top, click Save, and use the tool.

Since your API key only ever lives in your own browser's local storage, it's safe to make the GitHub repo (and the
Pages site) public — the page itself contains no secret, and nobody else's visit to the page will have or use your
key.

## Notes

- The character-limit rules (title/highlights/bullet/description formulas, brand-first ordering, no promotional
  language, etc.) are baked into the `SYSTEM_PROMPT` constant inside `index.html`. If Amazon's policy changes again,
  edit that string.
- Bullet fields on Amazon are plain text — the bold headline shown in this app's preview panel is for your own
  reference while reviewing, not literal formatting that carries over when pasted into Seller Central.
- Always double-check generated character counts and keyword placement against your own keyword research before
  publishing — this tool drafts, you approve.
