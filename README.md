# Mary Rose reception screen

A portrait (1080 × 1920) digital sign for the Mary Rose Museum reception, made by Interpro Technology. It is a single static web page: 22 pages rotate on a timer above a fixed footer showing today's opening hours, last entry, the time and a donation QR code. All the words, pictures and timings come from `content.json`.

There is no build step, framework, server code or package manager.

**For the people who edit the content, the full guide is [`README.txt`](README.txt)**: how to change `content.json`, what every field does, and what is still outstanding. This file is a short technical summary.

## Files

| Path | What it is |
|---|---|
| `index.html` | The whole screen: layout, styles and script inline |
| `content.json` | Everything shown: version, settings, opening hours, footer, logos, images, and the 22 pages (11 picture pages, `"type": "feature"`, and 11 supporter pages, `"type": "list"`) |
| `images/` | Photographs, supporter-page title bands, and the Mary Rose, Heritage Lottery Fund and Interpro logos |
| `fonts/` | EB Garamond and Open Sans (WOFF2), served from the site |
| `js/qrcode.js` | qrcode-generator by Kazuhiko Arase (MIT), used to draw the QR code |
| `README.txt` | Content editor's guide |

## Running it

Upload the folder to any web server and open `index.html` full screen on the player. The page has to be served over `http://` or `https://`: opened from disk, the browser won't let it read `content.json`.

To look at it locally, serve the folder, for example:

```bash
python3 -m http.server 8000
```

then open `http://localhost:8000/`.

| Address | Effect |
|---|---|
| `index.html#cw` / `#ccw` | Rotates the 1080 × 1920 stage 90° clockwise / anticlockwise, for a player that reports a landscape screen |
| `index.html?check` | Shows a red bar at the top if `content.json` has a problem |

At a desk: the right and left arrow keys step through the pages, a click moves to the next one, and Space pauses.

## How content updates work

- On start the page loads `content.json`. A copy of the last file that parsed is kept in the browser's `localStorage`, so if a later file has a mistake the screen keeps running on that copy.
- Every `settings.checkForUpdatesMinutes` minutes (5) it reads `content.json` again. If `version` is different from the one showing, it preloads the new pictures and swaps the content in at the next page change, without reloading the page.
- **Bump `version` with every change**, or the screen ignores it. A changed interval only takes effect when the screen is restarted.
- Upload a changed picture under a new file name and point to it in `images`, rather than overwriting the old file, so the player doesn't keep a cached copy.
- The opening hours shown come from `openingHours.seasons` (picked by today's month) unless `openingHours.specialDays` has an entry for today's date.

## Fonts

The display serif is `"Adobe Garamond Pro"` if the player has it installed, otherwise the bundled EB Garamond. Body text is Open Sans. Both bundled fonts are under the SIL Open Font Licence.

## Outstanding items

See *STILL TO DO* in `README.txt`: stand-in photographs, the logo version, supporter name spellings to be confirmed by the Trust, and prices to keep in step with maryrose.org.
