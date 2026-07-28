# frank — personal website

Static site, no build step. Two faces:

- `index.html` — academic homepage (tensor networks, papers, vita, contact)
- `book/index.html` — the book site (Why Nobody Understands Quantum Physics)
- `assets/papers/` — first-page images of papers (optional; cards degrade gracefully)
- `assets/covers/` — book cover photos (English cover + translations)

## Deploy on the quantumghent GitHub organisation

One-time setup (5 minutes):

1. Go to https://github.com/organizations/quantumghent/repositories/new
   - Repository name: `frank`
   - Public. Do NOT add a README (this folder has one).
2. On your machine, in this folder:

   ```bash
   git init
   git add .
   git commit -m "personal website"
   git branch -M main
   git remote add origin git@github.com:quantumghent/frank.git
   git push -u origin main
   ```

3. On GitHub: repo **Settings → Pages → Build and deployment**:
   - Source: *Deploy from a branch*
   - Branch: `main`, folder `/ (root)` → Save.
4. After ~1 minute the site is live at

   **https://quantumghent.github.io/frank/**

   (and the book at https://quantumghent.github.io/frank/book/)

All links in the site are relative, so it works under any repo name or domain.
To link it from the group site, add the URL to the People page of
quantumghent.github.io.

## Updating the site later

Edit the HTML (it is plain text, sections are clearly marked), then:

```bash
git add . && git commit -m "update" && git push
```

The page refreshes within a minute. Nothing can break: there is no build step.

## Dropping in the images

**Book covers** — put photos in `assets/covers/`:

- `english.jpg` — the Pan Books cover (used on the homepage band and the book hero)
- `cover-1.jpg` … `cover-8.jpg` — the eight editions, in the order of the gallery.
  Edit the captions in `book/index.html` (search for `class="cap"`) to name each
  language and publisher.

Portrait orientation, ~600×900 px is plenty. JPG or PNG (if PNG, change the
filename in the HTML accordingly).

**Paper first pages** — the paper cards show a typographic placeholder until an
image exists. To generate real first-page thumbnails, with the PDFs on your
machine (poppler installed, `brew install poppler` on a Mac):

```bash
pdftoppm -png -f 1 -l 1 -r 80 fourqubits.pdf assets/papers/fourqubits
mv assets/papers/fourqubits-1.png assets/papers/fourqubits.png
```

Expected filenames: `fourqubits.png`, `peps.png`, `faithful.png`,
`dissipation.png`, `cmps.png`, `tdvp.png`, `mpo.png`, `dualities.png`.

## Adding a paper card

Copy one `<div class="paper"> … </div>` block in `index.html`, change the
title/venue/arXiv link and the one-line note, and (optionally) add a thumbnail
with a new filename.
