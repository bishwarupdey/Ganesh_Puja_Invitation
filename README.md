# Ganesh Chaturthi Invitation

An animated, four-language invitation card (English, Hindi, Marathi, Bengali)
built as a single static page. Ready to publish on GitHub Pages.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole card — layout, styling and behaviour |
| `ganesh.jpg` | The artwork the text is laid over |
| `music.mp3` | **You add this** — the background music (see below) |

## 1. Add your music

Drop your audio file into this folder named exactly **`music.mp3`**.

That's the only step — nothing in `index.html` needs editing.

- A speaker button appears at the right of the language bar. Visitors tap it to
  start the music; it loops, and fades in and out rather than cutting abruptly.
- It never plays on its own. Browsers block autoplay with sound, and a page that
  starts making noise unprompted is a poor experience.
- **If `music.mp3` is missing, the button hides itself** and the card works
  normally — so it is safe to publish before you have the audio ready.

A few practical notes:

- **Format:** MP3 is the safest choice; every browser plays it. To use `.m4a`
  or `.ogg` instead, edit the `<source>` line near the top of `index.html`.
- **Size:** keep it under about 5 MB. It downloads over mobile data, and GitHub
  warns above 50 MB per file. A 2–3 minute track at 128 kbps lands around 2–3 MB.
- **Looping:** the track restarts seamlessly only if it is written to loop.
  Any track works, but one that ends where it began sounds best.
- **Rights:** whatever you upload becomes publicly downloadable from your site.
  Use music you own or are licensed to distribute — commercial recordings and
  film songs are not safe to host publicly.

## 2. Publish on GitHub Pages

1. Create a new repository on GitHub (public — Pages requires it on free plans).
2. Upload `index.html`, `ganesh.jpg` and your `music.mp3` to the repository root.
3. Go to **Settings → Pages**.
4. Under **Source**, choose **Deploy from a branch**; pick branch `main` and
   folder `/ (root)`. Save.
5. Wait about a minute. Your card is live at:
   `https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/`

## 3. Make the WhatsApp link preview work

When you paste the link into WhatsApp it shows a preview card. For the artwork
to appear there, the address has to be spelled out in full — relative paths are
not enough for link scrapers.

Open `index.html`, find the two lines containing `REPLACE_WITH_YOUR_URL`, and
substitute your published address:

```html
<meta property="og:image" content="https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/ganesh.jpg">
<meta property="og:url"   content="https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/">
```

No trailing slash on the image line. WhatsApp caches previews aggressively — if
you edit these after sharing, the old preview may persist for a while.

## Mobile compatibility

Tested at every common phone and tablet size from 320 px (iPhone SE, Galaxy S9)
up to tablets — no horizontal scrolling, and the text stays clear of the artwork
at every width.

The card is sized proportionally: all overlay text is measured against the
artwork's own width rather than the screen's, so the layout is identical at
every size instead of drifting into the picture on small phones. That is done
with a CSS custom property set by a few lines of script, which works on old iOS
and Android too — CSS container queries would have been tidier but are
unsupported on iOS 15 and earlier.

Also handled: `color-mix`, `inset` and `background-clip:text` all have plain
fallbacks, so nothing disappears on an older browser; `100svh` keeps the layout
steady while mobile toolbars slide; and the tap targets are enlarged to a
comfortable size without changing how the controls look.

## Changing the details

All the wording lives in `index.html` as plain text, four blocks of it, one per
language. Search for the phrase you want to change and edit it in place. The
date, time and venue sit together in the `hero-info` section.
