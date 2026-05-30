# L'encre de mes nuits

A simple, hand-built website for sharing poems alongside images.
Warm, textured, typewriter aesthetic — like a small paper notebook.

---

## What's inside

```
poetry-site/
├── index.html          ← homepage: list of your poems
├── loved.html          ← "loved" page: others' poems you cherish
├── about.html          ← about page
├── style.css           ← all the design
├── poems/
│   ├── _template.html  ← copy this for new poems
│   └── [15 poem files] ← your poems, one per file
└── images/
    └── placeholder.svg ← shown until you add real images
```

---

## Part 1 — Put it online (one-time setup)

You will publish this site for free using **GitHub Pages**. About 15 minutes the first time.

### Step 1. Create a free GitHub account
Go to <https://github.com/signup>. Pick a username you don't mind being part of your URL.

### Step 2. Create a new repository
1. Sign in → click **+** (top right) → **New repository**.
2. **Name**: your username followed by `.github.io` (e.g. `clara.github.io`).
   This exact name gives you `clara.github.io` as your URL.
3. Set to **Public**.
4. Check **Add a README file**.
5. **Create repository**.

### Step 3. Upload your site files
1. On the repo page: **Add file** → **Upload files**.
2. Drag everything inside the `poetry-site` folder (index.html, loved.html, about.html, style.css, the `poems` folder, the `images` folder) into the upload area.
3. **Commit changes**.

### Step 4. Turn on GitHub Pages
1. In the repo: **Settings** (top right).
2. Left menu: **Pages**.
3. Under "Build and deployment": **Source** = "Deploy from a branch", **Branch** = `main` / `/ (root)`.
4. **Save**.
5. Wait 1–2 minutes, then go to `https://YOUR-USERNAME.github.io`. Live.

---

## Part 2 — Adding a new poem

### Step 1. Add the image
1. In your repo, open the `images` folder.
2. **Add file** → **Upload files** → drop in your image.
3. Use a lowercase name with dashes, like `april-bridge.jpg`.

### Step 2. Create the poem page
1. Open the `poems` folder.
2. Open `_template.html` → click **Raw** → copy everything.
3. Back in the `poems` folder → **Add file** → **Create new file**.
4. Name it `your-poem-title.html` (lowercase, dashes).
5. Paste the template into the editor.
6. Replace the all-caps placeholders. The template has comments explaining each section.

**What each section does:**

- **Title & date**: Always required.
- **Thumbnail image** (`<figure class="poem-thumb">`): A small image that sits next to the title, like a stamp. The poem itself runs full-width below, so line breaks stay natural. Delete the figure if you don't want an image.
- **Dedication** (`<div class="poem-dedication">`): Like "to Pinsky's Savior" — optional, delete the line if not needed.
- **Epigraph** (`<blockquote class="poem-epigraph">`): A quote that opens the poem, with attribution. Optional.
- **Poem body**: Type your poem inside `<div class="poem-text">…</div>`. Line breaks, blank lines, and indentation are all preserved exactly as you type them.
- **Notes** (in `poem-extras`): A short paragraph of context below the poem. Optional — delete the whole `<section>` if not needed.
- **Versions / drafts**: Each `<details class="poem-version">` block becomes a click-to-expand earlier draft. Copy more blocks for more versions, or delete them all if not needed.
- **Previous / next links**: Update `PREVIOUS.html` and `NEXT.html` at the bottom to the slugs of neighbouring poems.

7. **Commit changes**.

### Step 3. Add it to the homepage list
1. Open `index.html` → pencil icon ✏️.
2. Find `<!-- ============== NEWEST POEM AT THE TOP ============== -->`.
3. Add a new `<li>…</li>` block right under it, copying the format.
4. **Commit changes**.

Your new poem appears on the live site in about a minute.

---

## Part 3 — Adding a loved poem (someone else's)

1. Open `loved.html` → pencil icon.
2. Copy any existing `<li data-author="…" data-themes="…">…</li>` block.
3. Edit it:
   - **`data-author`**: a slug for the author, like `"alejandra-pizarnik"`. Use the same slug if the author is already in the filters; otherwise add a new author button at the top.
   - **`data-themes`**: space-separated list of themes, like `"love grief"`. Same rule for adding new ones.
   - The author name, title, excerpt, link, and notes are obvious — just rewrite them.
4. **Important — copyright**: For poems still in copyright (most 20th- and 21st-century poets), keep excerpts SHORT (a few lines at most) and link to a legitimate source (Poetry Foundation, the publisher, etc.) for the full text. For public-domain poets (pre-1929 generally, or Dickinson / Whitman / etc.), you can quote freely.

### Adding a new author or theme filter button

At the top of `loved.html`, inside `.loved-filters`, add a new button:

```html
<button class="filter-btn" data-filter="author" data-value="federico-garcia-lorca">Federico García Lorca</button>
```

Then use the same `data-value` ("federico-garcia-lorca") in the `data-author` attribute of the poem's `<li>`.

Same pattern for themes — add a button with `data-filter="theme"` and use the matching value in `data-themes`.

---

## Part 4 — Tweaking the design

Open `style.css`. The variables at the very top control the whole site:

```css
:root {
  --paper: #f4ead5;        /* main background */
  --ink: #2b241a;          /* main text */
  --ink-soft: #5a4d3a;     /* secondary text */
  --accent: #a0522d;       /* links, highlights */
  --rule: #c9b896;         /* dashed lines */
}
```

Other things to tweak:
- **Tagline**: edit the `<p class="tagline">` line in `index.html`, `loved.html`, `about.html`, and each poem file.
- **About text**: edit `about.html`, inside `<section class="about">`.
- **Fonts**: at the top of `style.css`, swap the Google Fonts import URL, then update `--font-mono` and `--font-serif`.

---

That's everything. Quiet and small, like the poems it holds.

---

## Part 5 — Adding comments (Giscus)

Each poem in the `poems/` section has a Comments area, currently showing a placeholder. To make it live, use **Giscus** — a free service that stores comments as GitHub Discussions in your repository. (Visitors need a free GitHub account to comment, which keeps spam away.)

### One-time setup

1. Make sure your repository is **public** (it is, if you followed Part 1).
2. Go to your repo **Settings → General → Features** and tick **Discussions** to enable it.
3. Visit **https://github.com/apps/giscus** and click **Install**, granting it access to your repository.
4. Go to **https://giscus.app**. In the configuration page:
   - Enter your repo (e.g. `yourname/yourname.github.io`).
   - Under "Page ↔ Discussions Mapping", choose **"Discussion title contains page pathname"**.
   - Under "Discussion Category", pick **Announcements** (or make a category called "Comments").
   - Leave the rest as default.
5. The site will generate a `<script>` block for you. It looks like:

   ```html
   <script src="https://giscus.app/client.js"
           data-repo="yourname/yourname.github.io"
           data-repo-id="..."
           data-category="Announcements"
           data-category-id="..."
           data-mapping="pathname"
           data-theme="light"
           crossorigin="anonymous"
           async>
   </script>
   ```

### Activating it on each poem

In each poem file inside `poems/`, find this block:

```html
<div class="giscus"></div>
<div class="giscus-placeholder"> ... </div>
```

Replace the `<div class="giscus-placeholder"> ... </div>` line with the `<script>` block you copied from giscus.app. Leave `<div class="giscus"></div>` in place — Giscus uses it.

Do this once per poem. Comments will then appear at the bottom of each poem, and you'll be notified in your repo's Discussions tab whenever someone comments.

> Tip: if that feels like a lot of editing, you can instead move the comments into a small shared snippet later — but copy-pasting the script into each poem is the simplest way to start.
