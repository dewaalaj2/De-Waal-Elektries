# De Waal Electrical — website

Static site. No build step, no framework, no dependencies. Everything the site
needs is in this folder.

```
index.html          the whole page (markup, CSS and JS inline)
img/                job photographs, webp at 3 widths + jpg fallback
fonts/              Archivo, self-hosted (latin subset, 35 KB)
favicon.svg  favicon.ico  favicon-32.png  apple-touch-icon.png
robots.txt  sitemap.xml
vercel.json         cache headers only
```

## Deploying to Vercel

Deploy **this folder** as the project root. There is no build command and no
output directory — Vercel serves it as-is.

```bash
npx vercel --prod
```

Or connect the repo in the Vercel dashboard and set the Root Directory to
`dewaal-site`, Framework Preset to **Other**, and leave the build command empty.

If the custom domain is not already attached, add `dewaalelectrical.co.za` and
`www.dewaalelectrical.co.za` under Settings → Domains.

## Changing things

**The phone number** appears in several places and must be changed in all of
them. It is written two ways:

- `082 573 8465` — what people read
- `+27825738465` in `tel:` links and `27825738465` in `wa.me` links — the
  machine-readable form. Keep the `27` country code and drop the leading `0`.

Search `index.html` for `8465` to find every occurrence, including the one in the
structured-data block at the bottom.

**Adding a job photo.** Put the original in `../_source-photos/`, then generate
the web versions (requires ffmpeg):

```bash
ffmpeg -i _source-photos/photo-12.jpg -vf scale=1200:-2 -c:v libwebp -quality 80 dewaal-site/img/photo-12-1200.webp
```

Repeat for widths 800 and 480, plus a `.jpg` fallback, then copy an existing
`<figure class="mod">` block in `index.html` and change the filenames, the
`width`/`height` to the photo's real pixel dimensions, the `alt` text, and the
caption.

**What must not be added:** reviews, star ratings, testimonials, certification
badges, licence numbers, awards, or customer names. None of these exist for this
business yet, and inventing them is both dishonest and a real legal risk for
electrical compliance work. If genuine ones are obtained later, they are worth
adding prominently — see the notes in `../PRODUCT.md`.

## Things worth doing later

1. **Find the original of the roof photograph.** The only surviving copy is
   1000px wide, so the hero image is an upscale and is slightly soft on large
   screens. The original phone file will be several times larger and would sharpen
   the most important image on the site.
2. **Google Business Profile.** For a local trade, this drives more enquiries
   than the website itself. The structured data in `index.html` is already set up
   to match it.
3. **A real registration or licence number**, if there is one, replacing the
   current general "Registered at the Electrical Bargaining Council" line.
