# ltzhao.github.io

Personal academic homepage. Plain HTML and one CSS file — no Jekyll, no build
step, no dependencies. Edit a file, commit, push; the site updates in about a
minute.

---

## Contents

1. [Files in this folder](#files-in-this-folder)
2. [Part 1 — Putting the site on GitHub](#part-1--putting-the-site-on-github)
3. [Part 2 — Uploading PDFs and linking to them](#part-2--uploading-pdfs-and-linking-to-them)
4. [Before you publish: things to fill in](#before-you-publish-things-to-fill-in)
5. [Adding a paper or a talk](#adding-a-paper-or-a-talk)
6. [Custom domain](#custom-domain-optional)
7. [Previewing locally](#previewing-locally)
8. [Troubleshooting](#troubleshooting)

---

## Files in this folder

```
index.html          Home — bio, portrait, contact, background
publications.html   Papers, preprints, thesis
talks.html          Invited talks and seminars
teaching.html       Teaching, course list, worksheets
transcriptions.html LaTeX transcriptions and translations (PDF + source)
seminar.html        Sheldon's Student Seminar, 2017–2020 (94 talks)
                    — not in the nav; reached from the Talks page
archive.html        Older writing, seminars, LaTeX transcriptions
404.html            Not-found page
assets/style.css    All styling (light + dark, responsive)
assets/portrait.jpg Homepage photo — REPLACE THIS PLACEHOLDER
assets/archive/     PDFs linked from the archive page (currently empty)
assets/teaching/    Worksheets linked from the teaching page (currently empty)
assets/transcriptions/  PDFs and .tex sources for the transcriptions page
.nojekyll           Tells GitHub Pages to serve files as-is
README.md           This file — not published, just notes for you
```

---

## Part 1 — Putting the site on GitHub

There are two routes. **Route A** uses only your browser and is the one to pick
if you don't already use git. **Route B** is the command line, which is faster
once set up. Both give an identical result.

### Route A — browser only (no git, no terminal)

**1. Make a GitHub account** at <https://github.com> if you don't have one. Your
username matters: it becomes part of your web address. If you sign up as
`ltzhao`, the site will live at `https://ltzhao.github.io`.

**2. Create the repository.**

   - Click **+** in the top-right → **New repository**
   - **Repository name:** `<your-username>.github.io` — using your *exact*
     username, all lowercase. If your username is `ltzhao`, the repo is named
     `ltzhao.github.io`. This exact name is what gives you the short URL.
   - Set it to **Public**. (GitHub Pages needs public on a free account.)
   - Do **not** tick "Add a README file" — this folder already has one.
   - Click **Create repository**.

**3. Upload the files.**

   On the empty repository page, click the **uploading an existing file** link
   (it's in the line "…or upload an existing file"). Then:

   - Open the `ltzhao-site` folder on your computer
   - Select everything *inside* it — `index.html`, `publications.html`,
     `talks.html`, `teaching.html`, `archive.html`, `404.html`, `README.md`,
     and the `assets` folder
   - Drag them onto the GitHub upload area

   > **Important:** drag the *contents* of the folder, not the folder itself.
   > `index.html` must sit at the top level of the repository. If you upload the
   > `ltzhao-site` folder as a whole, your site will end up at
   > `ltzhao.github.io/ltzhao-site/` instead, with a blank page at the root.

   > **Also:** `.nojekyll` starts with a dot, which macOS Finder hides by
   > default. Press `Cmd + Shift + .` in Finder to show hidden files, then
   > include it. (If you miss it, the site still works — it only matters if you
   > later add a folder whose name starts with an underscore.)

   Scroll down, type a short message like `Initial site` in the description box,
   and click **Commit changes**.

**4. Turn on GitHub Pages.**

   - In the repository, click **Settings** (top bar, right side)
   - In the left sidebar, click **Pages**
   - Under **Source**, choose **Deploy from a branch**
   - Set branch to **`main`** and folder to **`/ (root)`**
   - Click **Save**

**5. Wait about a minute**, then visit `https://<your-username>.github.io`. The
first build can take up to ten minutes; after that, updates appear in under a
minute. You can watch progress on the **Actions** tab.

### Route B — command line

Install git if you don't have it (`brew install git` on macOS; on Ubuntu
`sudo apt install git`). Create the empty repository through the browser as in
step 2 above, then:

```sh
cd path/to/ltzhao-site
git init -b main
git add .
git commit -m "Initial site"
git remote add origin https://github.com/<your-username>/<your-username>.github.io.git
git push -u origin main
```

Then do step 4 (Settings → Pages) once. From then on, publishing a change is:

```sh
git add .
git commit -m "Add new paper"
git push
```

### A note on repository names

`<username>.github.io` is a special name that gives you the root URL. Any other
name works too — a repo called `homepage` publishes at
`https://<username>.github.io/homepage/`. If you go that route, everything below
still applies; the addresses just get the extra `/homepage/` segment.

---

## Part 2 — Uploading PDFs and linking to them

This is the part that replaces Google Drive. The idea is simple: **a file in the
repository is a file on the web.** Put `cv.pdf` in the `assets` folder and it is
immediately readable at `https://<username>.github.io/assets/cv.pdf`. There is
no sharing setting, no "anyone with the link", no Drive viewer wrapper — the URL
just serves the PDF.

The path in the repository *is* the path in the URL:

| File in the repository       | Address on the web                                    |
|------------------------------|-------------------------------------------------------|
| `index.html`                 | `https://ltzhao.github.io/`                           |
| `publications.html`          | `https://ltzhao.github.io/publications.html`          |
| `assets/cv.pdf`              | `https://ltzhao.github.io/assets/cv.pdf`              |
| `assets/archive/weyl.pdf`    | `https://ltzhao.github.io/assets/archive/weyl.pdf`    |

### Uploading a file through the browser

1. In your repository, click into the folder you want (click `assets`)
2. Click **Add file** → **Upload files**
3. Drag the PDF in
4. Click **Commit changes**

To create a folder that doesn't exist yet, use **Add file → Create new file** and
type `foldername/placeholder.txt` as the filename — the slash makes the folder.
(This is why `assets/archive/` contains a `.gitkeep` file: git won't track an
empty folder, so that file holds the folder open for you.)

### Uploading from the command line

Copy the file in, then commit:

```sh
cp ~/Downloads/cv.pdf assets/cv.pdf
git add assets/cv.pdf
git commit -m "Add CV"
git push
```

### Linking to an uploaded file

The pages already contain the links; you're supplying the files they expect.
The link in `index.html` looks like this:

```html
<dd><a href="assets/cv.pdf">Curriculum vitae (PDF)</a></dd>
```

`href="assets/cv.pdf"` is a **relative path** — it means "starting from where
this page is, go into `assets` and find `cv.pdf`." Because `index.html` sits at
the top of the repository, that resolves correctly.

To add a link somewhere new, follow the same shape:

```html
<a href="assets/notes/seminar-notes.pdf">Seminar notes</a>
```

Three rules keep relative links working:

- **No leading slash.** Write `assets/cv.pdf`, not `/assets/cv.pdf`. Without the
  slash the link also works when you preview the file locally.
- **Filenames are case-sensitive on the server.** `CV.pdf` and `cv.pdf` are
  different files. This bites people constantly, because it works on a Mac (case
  insensitive) and then breaks once published.
- **Avoid spaces in filenames.** Use `ample-line-bundle.pdf`, not
  `ample line bundle.pdf`. Spaces become `%20` in URLs and are a nuisance.

### The files these pages are already expecting

Drop these in with exactly these names and every link on the site resolves:

| Where it goes                                | What it is                          |
|----------------------------------------------|-------------------------------------|
| `assets/cv.pdf`                              | Your CV                             |
| `assets/archive/ample-line-bundle.pdf`       | 2015 bachelor's thesis              |
| `assets/archive/what-is-an-adinkra.pdf`      | 2014 talk                           |
| `assets/archive/weyl-calculus.pdf`           | 2014 Weyl calculus paper            |
| `assets/archive/kneser-conjecture.pdf`       | 2014 Kneser conjecture (Chinese)    |
| `assets/archive/lane-changing.pdf`           | 2014 lane-changing paper            |
| `assets/archive/three-coloring.pdf`          | 2013 3-coloring paper               |
| `assets/archive/mehta-subramanian.pdf`       | LaTeX transcription                 |
| `assets/archive/ngo.pdf`                     | LaTeX transcription                 |

Prefer different filenames? Upload under whatever name you like and edit the
`href` in the HTML to match. Nothing depends on these particular names.

### Getting the PDFs out of Google Drive

In Drive, select the files → right-click → **Download**. A multi-file download
arrives as a `.zip`; unzip it, then rename each PDF to the names above before
uploading. Google Docs files download as `.docx` by default — if you want a PDF,
open the document and use **File → Download → PDF Document**.

### Images

Same mechanism. Save a square portrait as `assets/portrait.jpg`, then uncomment
the line in `index.html`:

```html
<img class="portrait" src="assets/portrait.jpg" alt="Lutian Zhao">
```

Resize it to roughly 400×400 pixels first — a 5 MB photo straight from a phone
makes the page slow to load for no visible benefit.

### File size

GitHub warns above 50 MB per file and refuses above 100 MB. A repository should
stay under about 1 GB. PDFs of papers and slides are nowhere near these limits,
so in practice you will not run into them. Video is the exception — host that on
YouTube or Vimeo and link to it.

### One caveat worth knowing

Everything in a public repository is public and stays in the history. If you
commit a file and delete it later, it remains recoverable in past commits. So
don't upload anything — a draft with private comments, an unredacted reference
letter — that you wouldn't want read. This is different from Drive, where
unsharing a file actually revokes access.

---

## Before you publish: things to fill in

- **CV** — put your PDF at `assets/cv.pdf`. The home page already links to it.
  (Delete that row in `index.html` if you'd rather not host it.)
- **Author page link** — there's a commented-out row in `index.html` for an
  arXiv author page / ORCID / Google Scholar. Uncomment it and paste your real
  link, or leave it out.
- **Archive PDFs** — see the table above.
- **Seminar archive link** — one link in `archive.html` is marked
  `data-todo="seminar-archive"` and points nowhere yet. Paste the real URL.
- **Transcription titles** — the two LaTeX transcriptions are listed by author
  only; add the paper titles if you remember them.
- **Journal links** — the published papers have no DOI links. Add them inside
  the `<span class="pub-links">` blocks, same pattern as the arXiv links.
- **Photo** — `assets/portrait.jpg` is currently a grey placeholder that says
  "Your photo". Replace it with your own; see *The portrait* below.
- **New preprint** — the arXiv:2608.25397 entry at the top of `publications.html`
  uses the working title you gave me; I couldn't reach arXiv to verify it.
  Check the title and coauthor list against the posting and fix the line marked
  with a `TODO` comment.
- **Recent talks** — `talks.html` currently stops at 2023. There's a commented
  template at the top of the list to copy.

---

## Adding a paper

Copy an existing `<li>` block and edit it. In `publications.html`:

```html
<li>
  <span class="pub-title">Title of the paper</span>
  <span class="pub-meta">with Coauthor. <em>Journal</em> <strong>12</strong> (2026), 1–20.</span>
  <span class="pub-links"><a href="https://arxiv.org/abs/0000.00000">arXiv:0000.00000</a></span>
</li>
```

Numbering is automatic — the CSS counts list items, so you never renumber by
hand. When a preprint gets accepted, move its block from the first list to the
second and the numbers on both lists fix themselves.

### Adding a talk

`talks.html` is grouped by year, newest first, with an **Organizing** section at
the top for conferences and seminars you run (currently the 2026 Kavli IPMU
workshop and Sheldon's Student Seminar, which links through to `seminar.html`).

Nothing is left pending — every talk on the page is published and linked to its
source. Find the right year heading and copy a block:

```html
<li>
  <span class="when">March</span>
  <span class="what">
    <span class="title">Title of the talk</span>
    <span class="where">Seminar name, Institution, City</span>
  </span>
</li>
```

The left column takes the month as a word. For a new year, add
`<h2>2027</h2>` followed by its own `<ul class="timeline">` in the right place.
To link a talk to its seminar page, wrap the title in an `<a href="...">`. A
template with both variants is in a comment at the bottom of the file.

You can edit these directly on GitHub: open the file in the repository, click
the pencil icon, make the change, click **Commit changes**. The site updates a
minute later. No terminal needed for a one-line fix.

---

## Custom domain (optional)

If you own a domain, create a file called `CNAME` in the repository root
containing just the domain, e.g.:

```
lutianzhao.com
```

Then at your registrar, add a CNAME DNS record pointing `www` at
`<your-username>.github.io`, and for the bare domain add A records to GitHub's
four IPs (185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153).
Back in Settings → Pages, enter the domain and tick **Enforce HTTPS** once the
certificate is issued (GitHub says this can take up to 24 hours).

---

## Previewing locally

From inside the folder:

```sh
python3 -m http.server 8000
```

Open <http://localhost:8000>. This serves the files the same way GitHub does, so
what you see is what you'll get. Opening `index.html` by double-clicking also
mostly works, but a local server is a truer test.

---

## Troubleshooting

**The site shows a 404, or GitHub's "There isn't a GitHub Pages site here."**
Usually the first build hasn't finished — check the **Actions** tab. If it's
been ten minutes, confirm `index.html` is at the top level of the repository,
not inside a subfolder.

**The page loads but looks like unstyled text.**
`assets/style.css` didn't come through. Check the `assets` folder exists in the
repository with `style.css` inside, spelled exactly that way.

**A PDF link gives a 404.**
Check spelling and capitalization against the actual filename in the repository,
and confirm the file is in the folder you think it is. Clicking the file in
GitHub's file browser shows you its real path.

**I pushed a change but the site looks the same.**
Give it a minute, then hard-refresh: `Cmd + Shift + R` on macOS,
`Ctrl + Shift + R` elsewhere. Browsers cache CSS aggressively.

**Changes work locally but break when published.**
Almost always capitalization — the server is case-sensitive, your Mac is not.


---

## The portrait

`index.html` shows `assets/portrait.jpg` beside your name. To use your own
photo, save it over that file with the same name — nothing else to change.

**Why a photo often looks wrong on a page like this, and what the CSS does
about it.** Three things go wrong when a photo is dropped into a text layout:

1. *It leaves a hole.* A tall image next to two short paragraphs pushes the
   next section down and strands white space. Here the photo is paired with the
   contact table, so the left column has enough height to sit level with it.
2. *It arrives at whatever shape the camera produced.* A 3:4 phone photo next
   to a square-ish column reads as an accident. The CSS forces a square with
   `aspect-ratio: 1 / 1` and `object-fit: cover`, so any photo you supply is
   cropped to a square rather than stretched.
3. *It's too saturated for the page.* A bright snapshot next to restrained
   serif text pulls all the attention. A slight `saturate(0.94)` settles it
   into the palette.

Practical advice for the file itself:

- Roughly square, at least 500×500 pixels. 760×760 is ideal — twice the
  displayed size, so it stays sharp on a retina screen.
- Keep it under about 300 KB. Export at JPEG quality 80–85; a 4 MB photo
  straight from a phone makes the page slow for no visible gain.
- The crop favours the upper part of the image (`object-position: center 22%`),
  which is right for a head-and-shoulders portrait. If your photo is framed
  differently and the crop cuts badly, change that percentage in
  `assets/style.css` — lower shows more of the top, higher shows more of the
  bottom.
- To change the size, edit `width` on `.portrait-fig` (currently `200px`).
- The caption under the photo says "Kavli IPMU, Kashiwa". Edit or delete the
  `<figcaption>` line in `index.html`.

To remove the photo entirely, delete the whole `<figure class="portrait-fig">`
block from `index.html`; the layout falls back to full-width text on its own.

---

## The seminar page

`seminar.html` reproduces Sheldon's Student Seminar: 94 talks over 7 semesters,
with the 59 abstracts and 80 reference links that survived. It was rebuilt from
the Internet Archive's copy of the original UIUC page, and the reference links
were rewritten to point at the original sources rather than through the archive.

The page is generated but plain — no build step, just HTML like the rest of the
site. Two behaviours come from a small inline script at the bottom of the file:

- **Filter box** — matches against title, speaker *and* abstract text, so
  searching "wall crossing" finds talks whose titles don't contain the phrase.
  Semester headings and their counts update to match; empty semesters hide.
- **Expand all / Collapse all** — toggles every abstract at once.

If JavaScript is off, everything still works: the filter box does nothing, but
each talk is a native `<details>` element that opens on click.

To add a talk, copy an existing `<li>` block. The `data-search` attribute is
what the filter reads — keep it in sync with the visible text, lowercased:

```html
<li data-search="title speaker any abstract words">
  <details>
    <summary>
      <span class="sem-date">03/15/26</span>
      <span class="sem-main">
        <span class="sem-title">Title of the talk</span>
        <span class="sem-speaker">Speaker Name</span>
      </span>
    </summary>
    <div class="sem-body">
      <p class="sem-abstract">Abstract text.</p>
      <span class="sem-refs"><a href="https://example.org/paper.pdf">Reference I</a></span>
    </div>
  </details>
</li>
```


---

## Adding worksheets to the teaching page

`teaching.html` has a **Worksheets & notes** section ready for the files on your
disk. Three steps:

1. **Name and upload the PDF.** Put it in `assets/teaching/` with a name that has
   no spaces and says what it is, e.g. `math406-quadratic-reciprocity.pdf`.
   (Remember: click *into* the `assets/teaching` folder on GitHub first, then
   Add file → Upload files.)
2. **Un-hide the list.** In `teaching.html`, delete the paragraph with
   `id="worksheets-empty"` and remove the word `hidden` from
   `<ul class="timeline" id="worksheets" hidden>`.
3. **Fill in an entry.** The template block is already there — edit it, then
   copy it for each further worksheet:

```html
<li>
  <span class="when">MATH 406</span>
  <span class="what">
    <span class="title"><a href="assets/teaching/math406-quadratic-reciprocity.pdf">Quadratic reciprocity</a></span>
    <span class="where">One line on what it covers or when it was used.</span>
  </span>
</li>
```

The left column takes the course code; if you'd rather show a date or week
number, put that there instead — it's just text.

If the list grows past a dozen or so, group it by course with an `<h3>` heading
before each block, and give each course its own `<ul class="timeline">`.

### Course terms

The course list currently shows course codes but not the semesters. If you want
terms, either add them to the `<span class="where">` line
("University of Maryland, College Park — Fall 2022") or move the code into the
title and put the term in the left column.


---

## Adding a transcription

`transcriptions.html` expects **two files per entry** — the compiled PDF and the
source — both in `assets/transcriptions/`, named the same apart from the
extension:

```
assets/transcriptions/ngo-support.pdf
assets/transcriptions/ngo-support.tex
```

If the source is more than one file (figures, a bibliography, several chapters),
zip it and upload `ngo-support.zip` instead, then change the second link's text
from "TeX source" to "Source (zip)".

Then copy the template block — it's in a comment at the bottom of the file:

```html
<li>
  <span class="when">1998</span>
  <span class="what">
    <span class="title">Title of the paper</span>
    <span class="where">Original Author. <em>Journal</em> 12 (1998), 1–40.
      Translated from the French.</span>
    <span class="filelinks">
      <a href="assets/transcriptions/slug.pdf">PDF</a>
      <a href="assets/transcriptions/slug.tex">TeX source</a>
    </span>
  </span>
</li>
```

The left column takes the **original paper's** year, not the year you typed it
up, so the page reads as a bibliography.

**Uploading many at once.** The browser uploader takes up to 100 files per
commit, so you can drag a whole folder of PDFs and sources in one go — but
remember to click *into* `assets/transcriptions` first, or they land at the repo
root. If you find yourself doing this often, git from the command line is much
less fiddly: `git add assets/transcriptions && git commit -m "Add transcriptions" && git push`.

The two existing entries are listed by author only — their titles were never on
the old site. Search `transcriptions.html` for `TODO` to find them.
