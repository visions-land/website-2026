# Visions, Chapter II — static site

The public-facing pages of **Visions, Chapter II — I popoli del mare**, as plain
HTML and CSS. No build step, no framework, no dependencies: the files in this
repository are the website.

This is a static port of the homepage and the prize-information page from the
original Lovable/React app (`Visions-Application-Form`). The application form,
login and voter dashboard are deliberately **not** included — they need Supabase
and cannot be static, and applications are closed.

## Contents

| File | What it is |
| --- | --- |
| `index.html` | Homepage — the synopsis |
| `info.html` | Prize information — intro text, FAQ accordion, documentation download |
| `styles.css` | The whole design system; all colour/font/radius tokens live in the `:root` block |
| `assets/` | ctrlshift logo, logomark, hero image |
| `Visions_Chapter_II.pdf` | The downloadable call documentation |
| `favicon.ico`, `robots.txt` | Carried over from the original app |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is, without Jekyll |

## Local preview

Open `index.html` in a browser, or serve the folder so that relative paths and
the PDF behave exactly as they will in production:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploying to GitHub Pages

1. Create an empty repository on GitHub and push this folder to it:

   ```sh
   git remote add origin git@github.com:<owner>/<repo>.git
   git push -u origin main
   ```

2. In the repository, go to **Settings → Pages**, set **Source** to *Deploy from
   a branch*, and pick branch `main` with folder `/ (root)`.

3. The site goes live at `https://<owner>.github.io/<repo>/` — or at your own
   domain if you add one under **Settings → Pages → Custom domain**, which also
   writes a `CNAME` file into the repository.

All internal links are relative, so the site works at a repository subpath
(`/<repo>/`) and at a domain root without any changes.

### One thing to update after the first deploy

The `og:image` / `twitter:image` tags in `index.html` and `info.html` currently
point at `assets/hero-medinet-habu.jpg` as a relative path. Social-media
crawlers need an absolute URL, so once the final address is known, replace those
four values with the full URL, e.g.
`https://<owner>.github.io/<repo>/assets/hero-medinet-habu.jpg`. Everything else
works untouched.

## Notes on the port

- **Styling** is a hand-written translation of the Tailwind classes the React
  components produced. Every design token in `styles.css` is copied verbatim from
  the original `src/index.css`, so the palette is identical.
- **The FAQ accordion** uses native `<details>`/`<summary>` elements sharing a
  `name="faq"` attribute, which gives single-open behaviour with no JavaScript in
  current browsers. The small inline script in `info.html` only adds three
  conveniences: the same exclusivity for older browsers, the in-text
  cross-reference links (“application requisites”, “in scope”, “relevant
  dates”), and support for deep links such as `info.html#relevant-dates`. With
  JavaScript disabled, every section still opens and reads correctly.
- **The hero image** was downloaded from Wikimedia Commons instead of being
  hotlinked, so the site has no external runtime dependencies. It is a drawing of
  the northeast wall of the Ramesses III temple at Medinet Habu; check its
  [Commons file page](https://commons.wikimedia.org/wiki/File:Medinet_Habu_Ramses_III._Tempel_Nordostwand_Abzeichnung_01.jpg)
  for the licence terms and add the attribution it requires before publishing.
- **Dropped routes.** `/apply`, `/login` and `/vote` have no static equivalent.
  The “Applications closed.” button on the info page is rendered disabled, as it
  was in the app.

## Contact

<visions@ctrlshift.events>
