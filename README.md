# Ganesh Chaturthi Invitation

An animated, four-language invitation card (English, Hindi, Marathi, Bengali)
published at <https://bishwarupdey.github.io/Ganesh_Puja_Invitation/>.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The whole card — layout, styling and behaviour |
| `ganesh.jpg` | The background artwork the text is laid over |
| `music.mp3` | The background music |
| `ganesh_preview_wide.jpg` | 1200×630 card used for link previews (WhatsApp etc.) |
| `ganesh_preview.jpg` | The portrait preview artwork, kept as a source image |

## Music

The page tries to start the music as soon as it opens. Browsers refuse audio
that begins without a user gesture — this is enforced everywhere, and there is
no way around it — so when the attempt is refused the page starts the music on
the visitor's **first tap, scroll or key press** instead. In practice it begins
the moment someone touches the card.

The speaker button in the language bar stops and restarts it, and the music
pauses automatically if the tab is backgrounded.

To change the track, replace `music.mp3`. Keep it under about 5 MB — it
downloads over mobile data. Whatever is here is publicly downloadable, so use
music you own or are licensed to distribute.

## Link previews (WhatsApp, iMessage, Facebook)

The preview uses `ganesh_preview_wide.jpg`. Two things matter and both are easy
to get wrong:

- **Shape.** Preview cards are landscape, roughly 1.91:1. A portrait image
  cannot produce a large card — services fall back to a small thumbnail, or crop
  the middle out of it. That file is 1200×630 so it renders as a full-width card.
- **Weight.** WhatsApp routinely fetches nothing at all when the image runs to
  several hundred kilobytes. That file is ~130 KB.

The `og:` tags in `index.html` carry the full absolute URL — relative paths do
not work, because the scrapers fetch the image independently of the page.

**Previews are cached.** If a link has already been shared and showed nothing,
WhatsApp may keep serving that empty preview for a while. Appending something
like `?v=2` to the link when you share it forces a fresh fetch.

## Publishing

The card is a plain static site — no build step and no server code.

**GitHub Pages** (current): push to `main`, then **Settings → Pages → Deploy from
a branch**, branch `main`, folder `/ (root)`.

**Cloudflare Pages**: **Workers & Pages → Create → Pages**. Either
**Upload assets** and drag the folder in, or **Connect to Git** to point it at
this repo — leave the build command empty and the output directory `/`.
Worth considering if the invitation goes to a large list: it has no bandwidth
cap, whereas GitHub Pages has a soft ~100 GB/month limit and the music file is
downloaded on every visit.

If you move hosts, update the `og:` URLs in `index.html` to the new address.

## Mobile compatibility

Checked from 320 px (iPhone SE, Galaxy S9) up to tablets: no horizontal
scrolling, and the text stays clear of the artwork at every width in all four
languages.

The overlay text is sized against the artwork's own width rather than the
screen's, via a CSS custom property set in script, so the layout is
proportionally identical at every size. Container queries would have been
tidier but are unsupported on iOS 15 and earlier. `color-mix`, `inset` and
`background-clip:text` all carry plain fallbacks so nothing disappears on an
older browser.

## Changing the wording

All the text lives in `index.html` as plain text, in four blocks, one per
language. Search for the phrase you want and edit it in place. The date, time
and venue sit together in the `hero-info` section.
