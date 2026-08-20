# rohangumaste.github.io

Personal academic homepage. Jekyll + the
[minimal-light](https://github.com/yaoyao-liu/minimal-light) remote theme,
served by GitHub Pages.

Content lives in:

| Path | What |
|---|---|
| `index.md` | About Me, Research Interests, News |
| `_data/publications.yml` | Publications & Preprints list |
| `_includes/` | Publications / services templates |
| `_config.yml` | Title, links, avatar, CV link |
| `assets/img/` | Profile picture and paper thumbnails |

---

## ⚠️ The CV source is NOT in this repo

**Do not add the CV LaTeX here.** This repo is public, so anything committed
becomes permanently public — including in git history. The CV source contains a
phone number, so it lives in a **private** repo instead:

> **https://github.com/rohangumaste/cv-private**

This repo carries only the built PDF, at `assets/files/cv.pdf`
(linked from `_config.yml` via `cv_link`).

### To update the CV

```bash
git clone https://github.com/rohangumaste/cv-private.git
cd cv-private
```

Edit `main.tex` / `myfile.bib` there, then build and install the **phone-free**
variant into this repo:

```bash
make install SITE=/path/to/rohangumaste.github.io
```

That builds the public variant (no phone number), verifies the PDF really has no
phone number, and copies it to `assets/files/cv.pdf`. Then publish from here:

```bash
git add assets/files/cv.pdf
git commit -m "Update CV"
git push
```

For applications you want the version *with* the phone number — that's
`make private` in `cv-private`, which produces `cv-private.pdf`. Never copy that
one, or `phone.tex`, into this repo.

See `cv-private/README.md` for details.

---

## Running the site locally

Needs Ruby **3.2** specifically. The system Ruby (2.6) is too old for the
`github-pages` gem, and Ruby 4.x is too new — it drops stdlib gems that the
pinned old Jekyll still expects.

```bash
brew install ruby@3.2
export PATH="/opt/homebrew/opt/ruby@3.2/bin:$PATH"
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve --host 127.0.0.1 --port 4000
```

Then open http://127.0.0.1:4000.

Notes:

- `vendor/` and `.bundle/` are gitignored — they're the local gem install.
- `vendor/` is in `exclude` in `_config.yml`; without that, Jekyll tries to
  build the gems' own site templates and the build fails on an invalid date.
- Edits to `index.md`, `_data/`, and `_includes/` hot-reload. Changes to
  `_config.yml` require restarting the server.
