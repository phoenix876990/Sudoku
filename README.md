# Sudoku

Six real difficulty tiers (Easy → Extreme), each puzzle generated with a
guaranteed unique solution. No timer, anywhere. Fully offline — no network
calls, no external fonts, no analytics.

This project is set up to run three ways from the same `index.html`. Pick
whichever fits; you don't need to do all three.

---

## 1. Installable web app (PWA) — easiest, works everywhere

No build step. Just needs to be served over `http(s)://` (not `file://`) for
the install prompt and offline caching to kick in, since browsers require
that for service workers.

```bash
cd sudoku-app
python3 -m http.server 8080
```

Then open `http://localhost:8080` in your browser. Look for an install
icon in the address bar (Chrome/Edge) or "Install app" in the menu
(Firefox/GNOME Web) — it'll install like any native app, with its own
window and icon, and keep working with your network off.

If you just want to double-click and play with zero setup, open
`index.html` directly in a browser (`file://`) — the game itself works
fine that way too; you only lose the "install as app" affordance and
offline service-worker caching (which you don't need anyway when there's
no server involved).

---

## 2. Desktop app (Electron) — standalone binary, no browser needed

```bash
cd sudoku-app
npm install
npm start          # runs it as a real desktop window right away
```

To produce an installable Linux binary (AppImage / .deb / .rpm):

```bash
npm run build:linux
```

Output lands in `sudoku-app/dist/`. The AppImage is the most
Bazzite-friendly option — mark it executable and run it directly, no
install required:

```bash
chmod +x dist/Sudoku-1.0.0.AppImage
./dist/Sudoku-1.0.0.AppImage
```

---

## 3. Native Flatpak — fits Bazzite's app ecosystem

This one wraps the Electron build, so build step 2 first. Then see
`flatpak/BUILDING.md` for the full sequence — it needs `flatpak-builder`
and the Electron base app / freedesktop runtime, which this sandbox
can't fetch (they're on Flathub, not reachable from here), so that part
runs on your own machine.

Once built and installed, Sudoku shows up in your app grid like any
other installed Flatpak, sandboxed the same way.

---

## Project layout

```
index.html                        the whole game — UI, styling, fonts, puzzle engine
manifest.json, sw.js              PWA install + offline caching
icons/                            app icons at all needed sizes
main.js, package.json             Electron wrapper
flatpak/                          Flatpak manifest + desktop entry + metainfo
```
