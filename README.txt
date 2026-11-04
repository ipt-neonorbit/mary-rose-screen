MARY ROSE RECEPTION SCREEN
Created by Interpro Technology

WHAT THIS IS
A portrait (1080 x 1920) screen for the Mary Rose Museum reception. 22 pages
rotate on a timer above a footer that stays put. Nobody needs to touch it.

RUNNING IT
Upload the whole folder to the web server and open index.html full screen on
the player. Keep index.html, content.json and the images, fonts and js folders
together.

The page must be opened from the web server (an address starting http:// or
https://). Opened straight from a computer's disk, browsers refuse to read
content.json and the screen shows an error.

If the player reports a landscape screen and the picture comes out sideways,
add #cw or #ccw to the end of the address (for example index.html#cw).

CHECKING IT AT A DESK
Right and left arrow keys (or a click) step through the pages. Space pauses.


CHANGING THE CONTENT
====================
Everything shown on the screen is in content.json. You never need to touch
index.html.

TO MAKE A CHANGE
  1. Open content.json in any plain text editor (Notepad, TextEdit, VS Code).
  2. Change the words.
  3. Add 1 to the version number on the second line, e.g. "version": 1
     becomes "version": 2. The screen ignores your changes until you do.
  4. Save and upload it over the old content.json.

HOW THE SCREEN PICKS IT UP
Every 5 minutes the screen reads the version number in content.json.
  - The same number as it is showing: it does nothing.
  - A different number: it quietly loads the new pictures and words in the
    background, then brings them in at the next page change, as part of the
    normal slide. The page never reloads, blanks or flickers, and the footer
    stays put. Changes appear within about 5 minutes of uploading.
  - A file with a mistake in it: it ignores it and carries on as it was.

When you change a picture while the screen is running, upload it under a new
file name (for example tours-2.jpg) and change its path in the images
section, rather than overwriting the old file. Otherwise the screen may keep
showing the copy of the old picture it already has.

THE RULES OF THE FILE
- Change only the words inside "quote marks", and numbers.
- Keep every quote mark, comma, bracket and colon exactly where it is.
- Every item in a list is followed by a comma, except the last one.
- Use curly apostrophes (’) as the file already does, or plain ones ('). Never
  type a plain double quote (") inside the words.
- Words between *asterisks* are set in semi bold italic.

IF YOU MAKE A MISTAKE
The screen keeps showing the last version that worked, so a typo will not
take it off the air. To find out whether your upload is correct, open the
screen's address with ?check on the end (for example .../index.html?check).
A red bar at the top explains the problem if there is one. You can also paste
the file into jsonlint.com to see which line is wrong.

WHAT EACH SECTION DOES

  version
    the number the screen checks. Add 1 every time you upload a change.

  settings
    defaultSeconds           how long a page shows if it doesn't set its own
    checkForUpdatesMinutes   how often the screen checks the version number
                             (takes effect the next time the screen is started)

  openingHours
    seasons      each season's months (1 = January ... 12 = December), its
                 opening hours and last entry. Today's month picks the season.
                 Winter is currently 10:00am – 4:15pm, last entry 3:15pm.
    specialDays  one-off dates that override the season, such as closures,
                 Christmas hours or late openings. For example:
                   "specialDays": [
                     { "date": "2026-12-24", "open": "10:00am – 2:00pm", "lastEntry": "1:00pm" },
                     { "date": "2026-12-25", "open": "Closed today", "lastEntry": "–" }
                   ]
                 Dates are written year-month-day. Old dates can be left in;
                 they are simply ignored.

  footer
    supportHeading, supportAsk, supportText   the donation wording
    supportUrlShown   the web address printed next to the QR code
    qrLink            where the QR code goes. Change this and the QR code
                      redraws itself.
    openTodayHeading, lastEntryHeading, timeNowHeading   the three labels
    notes             the line along the bottom ("No flash photography").
                      Add more in the list, separated by commas.
    creditBy, creditName   the Interpro credit

  logos    which image files are used for the three logos

  images   the picture names used by the pages, and the file each one points
           to. To swap a picture, either replace the file in the images
           folder keeping its name, or upload a new file and change the path
           here. band-navy, band-purple, band-maroon and band-teal sit behind
           the titles of the supporter pages.

  screens  every page, in running order. To reorder pages, move a whole
           { ... } block. To remove a page, delete its block (and the comma
           after it). To add one, copy a similar block and change it.

  Fields on a picture page ("type": "feature"):
    image       a picture name from the images section
    text        "top" or "bottom" puts the words over the picture;
                "band" puts the picture across the top
    band        with "band", how tall the picture is, in pixels (of 1536)
    wash        true tints the picture in brand colour
    seconds     how long the page shows
    label       the small heading top right
    tag         the red label above the title
    big         a large gold number or phrase ("1545", "10% off")
    eyebrow     a small heading above the title
    title       the main heading; titleSize sets its size in pixels
    lede        the paragraph under the title (loud: true makes it larger)
    facts       a list of { "k": "name", "d": "detail" } rows, e.g. tour prices
    note        the small line at the end
    dates       the three dates on the Welcome page

  Fields on a supporter page ("type": "list"):
    theme       navy, purple, maroon or teal
    page        the "1 / 3" counter
    title, sub, eyebrow, lede, label, seconds   as above
    lottery     true shows the Heritage Lottery Fund logo
    tiers       groups of names; size is the type size for that group
    founder     the Founder Member line
    ranks       Flag Officer ranks: rank, names, size, pad (gap between
                names) and range (the "A – F" note)
    officers    the "Flag Officers of the Mary Rose" heading on mixed pages
    side        two columns of ranks side by side
    closing     the closing line in italics
    compact, airy   tighter or looser spacing

  If a list of names is too long for its column, the screen steps the type
  size down until it fits. If a page gets too full, move some names to a new
  page or lower that group's size.


STILL TO DO
- Four pages use colour-washed stand-in pictures until real photographs are
  supplied: hatch.jpg, objects.jpg, life.jpg and tours.jpg.
- The Mary Rose logo was supplied at 222 pixels wide and reversed to off-white
  for dark backgrounds. Replace images/mary-rose-logo.png with an official
  white version if there is one.
- The serif is EB Garamond, standing in for Adobe Garamond Pro. The page uses
  Adobe Garamond Pro automatically if it is installed on the player.
- Supporter names follow the installed wall panels, which differ from the Word
  document in several spellings. Please have the Trust confirm them.
- Tour prices and the Patron price were taken from maryrose.org in October
  2026 and will need updating in content.json when they change.

CREDITS
QR codes are drawn by qrcode-generator by Kazuhiko Arase (MIT licence),
in js/qrcode.js. Fonts are EB Garamond and Open Sans (SIL Open Font Licence).
