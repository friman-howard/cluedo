# Murder Mystery Live

A single-file, offline web app for a live "assassin" party game. Ten players
take turns on one shared phone: each taps their name, confirms it's them, and
presses-and-holds to read their secret contract: a **victim**, a **place** and
an **object**.

Everything is in `index.html`: plain HTML/CSS/JS, no build step, no backend,
no external requests.

## Configure a game

Edit the constants at the top of the `<script>` block in `index.html`:

- `PLAYERS`: the player names (10)
- `PLACES`: the places (same count as players)
- `OBJECTS`: the objects (same count as players)
- `SEED`: any string. **Change it to deal a completely new game.**

The contracts come from a seeded PRNG (mulberry32 seeded from a hash of
`SEED`), so the same seed and lists always give the same contracts on any
device. Players are shuffled into one cycle: each player's victim is the next
player in the shuffled order, so there is exactly one loop and nobody targets
themselves.

"Briefed" flags are saved in the browser's `localStorage`, so they are
**per-device**. Pass one phone around. **Reset all briefings** (at the bottom,
behind a confirm) re-enables every name. The contracts stay the same, so
that's how you re-show someone who forgot theirs.

## Host it on GitHub Pages

1. Create a new repository on GitHub (it must be **public** on a free plan).
2. Add `index.html` (and this README) to the root of the default branch and push:
   ```sh
   git init
   git add index.html README.md
   git commit -m "Murder Mystery Live"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```
3. On GitHub, open the repo and go to **Settings → Pages**.
4. Under **Build and deployment**, set **Source** to **Deploy from a branch**,
   choose branch **main** and folder **/ (root)**, then click **Save**.
5. Wait a minute or two. The site is published at
   `https://<you>.github.io/<repo>/` (the URL is shown at the top of the Pages
   settings).

To start a new game, change `SEED` (and the lists if you like), then commit
and push. Pages redeploys automatically.

> Note: anyone who opens the page source can work out every contract, so this
> relies on players playing fair.

## Run locally

Open `index.html` directly in a browser. No server is needed.
