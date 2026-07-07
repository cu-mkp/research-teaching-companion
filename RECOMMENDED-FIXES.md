# Research and Teaching Companion — Review Findings & Recommended Fixes

Review of the Hugo theme (layouts, CSS), content Markdown (linting), and link
integrity (internal + external), performed 2026-07-07. Fixes marked ✅ are
already applied on the branch `fix/theme-css-baseurl-and-stray-div`; everything
else is recommended follow-up work.

## 1. Already fixed on the branch

### ✅ Header background image 404s on the GitHub Pages dev site (`a541829`)

`themes/rtc/assets/scss/main.scss` hardcoded `url("/img/text-bg.png")`. The
site's `canonifyURLs = true` rewrites root-relative URLs in **HTML** for each
deployment's base URL, but never touches compiled **CSS**, so on the dev site
(`cu-mkp.github.io/research-teaching-companion/`) the page-title banner
background resolved to `cu-mkp.github.io/img/text-bg.png` → 404. Now built
with `{{ "img/text-bg.png" | absURL }}` via the existing
`resources.ExecuteAsTemplate` pipeline; verified correct in builds against both
base URLs.

### ✅ Stray `</div>` on every list page (`a541829`)

`themes/rtc/layouts/_default/list.html` and `layouts/resources/list.html` ended
with an unconditional `</div>` that had no matching opening tag (confirmed live:
5 `<div>` vs 6 `</div>` on `/resources/`). Removed; open/close counts now
balance on top-level and sub-section pages.

### ✅ Broken internal asset links + typo'd domain (`691f26d`)

- `content/resources/student-projects/fa24_mckeever_dying-azur.md` — all 36
  figures pointed at `./media-mckeever/…` (a Docs-export artifact) which
  resolves under the page URL; the images live at `/images/media-mckeever/…`.
- `content/resources/activity-sheets/su22_fld_cunningham_annika_onion-skin-dyeing.md`
  — 4 download links said `template+notes`; the files in `static/documents/`
  are named `template-notes`.
- `content/resources/student-projects/sp22_arocho_alejandra_herodotus-workshop.md`
  — PDF link had a stray `static/` prefix and no leading slash
  (`static/documents/pdf/…` → `/documents/pdf/…`).
- `content/resources/activity-sheets/azurite-assignment.md` and
  `su17_rosenkranz_azurite-preparation-cambridge.md` — external domain typo
  `cameo.mfa.o` → `cameo.mfa.org`. (The corrected host bot-blocks automated
  checks — worth one manual click to confirm the target PDF exists.)

Verified with a local `hugo` build + link check: broken internal targets
dropped from 44 to 2 (the two genuinely missing PDFs below).

## 2. Missing files (need to be tracked down, not just re-linked)

Two PDFs are referenced but exist nowhere in `static/`:

| Missing file | Referenced from |
|---|---|
| `documents/pdf/rosenkranz_2019_dyes_handout_general-mordant-and-dye-processes.pdf` | `activity-sheets/su22_fld_cunningham_annika_onion-skin-dyeing.md` |
| `documents/pdf/rosenkranz_2019_dyes_handout_reconstruction-exchange_dyeing-with-natural-colorants.pdf` | `activity-sheets/dyes-cochineal_assignment.md`, `activity-sheets/su22_fld_cunningham_annika_onion-skin-dyeing.md` |

Other `rosenkranz_2019_*` PDFs are present in `static/documents/pdf/`, so these
two were likely never uploaded. Locate and add them (or remove/replace the
links).

## 3. Content fixes (from Markdown linting)

Of 10,149 raw markdownlint findings across 88 pages, ~99.5% is stylistic noise
for this site (inline HTML is intentional per `unsafe = true`; no line-length
policy). The 50 that affect rendering, semantics, or accessibility:

- **Malformed tables (7)** — rows with missing/extra cells silently drop or
  misalign data: `activity-sheets/verdigris-assignment.md` (lines ~29–51),
  `student-projects/su21_macomber_sophie_final-project-figures.md` (line ~80).
- **Broken emphasis (5)** — spaces inside `*`/`**` markers render literal
  asterisks: `student-projects/fa24_mckeever_dying-azur.md` (line ~148),
  `student-projects/fa25_kerwin_sophie_final-project_horn.md` (line ~829).
- **Blank line inside blockquote (6)** — splits one quotation into multiple
  `<blockquote>`s: `activity-sheets/activitysheet_lake-pigments.md`,
  `dyes-cochineal_assignment.md`, `pigment-cochineal-lake_assignment.md`,
  `student-projects/sp23_brown_reece_…lab-guide.md` (×2),
  `sp23_oberem-lukas_final-project_varnish.md`.
- **Missing image alt text (9)** — accessibility:
  `activity-sheets/sp23_dyes_tamu.md` (6), `case-studies.md` (3).
- **Multiple H1s per page (17)** — body `# Headings` duplicate the template's
  page-title H1 and are invisible to the sidebar TOC (which only lists H2/H3).
  Demote to `##`: `credits.md`, `introduction.md`, `case-studies.md`,
  `syllabi.md`, several `_index.md` files, and student projects
  (`fa21_alberts_naomi…`, `fa25_kumar_chinmay…`, `sp23_brown_reece…`,
  `sp23_oberem-lukas…`, `activitysheet_sample-hcr-discussion-document.md`).
- **Unused footnote definition (1)** — `[^2]` in
  `student-projects/fa25_gao_xin_final-project_heather-reinforced-earth.md`
  (line ~661) is defined but never referenced, so it won't render as a
  footnote.
- **Minor**: trailing spaces inside link text (`about.md` social links,
  `activity-sheets/_index.md`), one skipped heading level
  (`sp23_brown_reece…`), one bare "here" link
  (`activitysheet_hcr-historical-recipe-collection.md`).

## 4. External link failures (22 of 1,189 unique URLs)

Confirmed hard failures (HTTP 404, unreachable, or 500), with source pages:

| URL | Source page(s) |
|---|---|
| `http://cool.conservation-us.org/coolaic/sg/bpg/annual/v23/bp23-07.pdf` | `activity-sheets/azurite-assignment.md` |
| `http://www.history.org/foundation/journal/Summer12_newformat/dye.cfm` | `activity-sheets/dyes-cochineal_assignment.md` |
| `http://www.kookhistorie.nl/index.htm` (host dead) | `activity-sheets/breadmolding_resources-for-the-instructor.md`, `breadmolding-student-activity-sheet.md`, `activitysheet_hcr-historical-recipe-collection.md` |
| `https://www.staff.uni-giessen.de/gloning/kobu.htm` (unreachable) | both breadmolding pages |
| `https://artechne.hum.uu.nl/node/94995` | `student-projects/fa24_roya-chu_final-project_redden.md` |
| `https://doi.org/10.7208/chicago/9780226818238.001` (DOI not found) | `student-projects/fa24_roya-chu_final-project_redden.md` |
| `https://burgundianblack.tome.press/` (host dead) | `reflection/bibliography.md` |
| `https://www.upress.pitt.edu/books/9780822965770/` (unreachable) | `reflection/bibliography.md` |
| `https://www.cambridge.org/core/journals/renaissance-quarterly/article/…45366084…` (500) | `activity-sheets/activitysheet_jasper.md`, `reflection/bibliography.md` |
| `https://caitlynirwin.com/blog/beginners-guide-to-dyeing-with-onion-skins` | `activity-sheets/su22_fld_cunningham…onion-skin-dyeing.md` |
| `https://crafternoontreats.com/2018/06/12/natural-dyeing-with-onion-skins/` | same |
| `https://christchurchartgallery.org.nz/collection/69279/item/…` | `student-projects/sp22_lang_theodora_counterproofing.md` |
| `https://guides.library.columbia.edu/prf.php?account_id=14513` | `syllabi/syllabus_sp23_gu4962-hands-on-history.md` |
| `https://www.college.columbia.edu/core/core` | `student-projects/sp22_arocho_alejandra_herodotus-workshop.md` |
| `https://www.artcons.udel.edu/outreach/kress` | `activity-sheets/painting-assignment.md` |
| `https://www.naturalpigments.com/artist-materials/…/how-to-make-water-based-paint/` | `activity-sheets/painting-assignment.md` |
| `https://www.naturalpigments.com/glass-muller.html?___store=default` | `activity-sheets/painting-assignment.md` |
| `https://www.ams-net.org/ojs/index.php/jmhp/article/view/216` | `student-projects/fa21_zayas-waters_elliot-mac_final-project-soundscape.md` |
| `https://www.knoxgarden.org/events-all/herbal-bath-teas` | `student-projects/sp23_brown_reece_…lab-guide.md` |
| `https://www.knoxgarden.org/events-all/history-of-black-soapmaking` | same |
| `https://www.crassh.cam.ac.uk/research/projects-centres/genius-before-romanticism/` (unreachable) | `student-projects/fa24_mckeever_dying-azur.md` |

For dead scholarly sources, consider Wayback Machine (`web.archive.org`)
snapshot URLs.

**Not broken (checker artifacts):** 134 × 403 are almost entirely bot-blockers
(doi.org ×49, JSTOR ×23, Kremer Pigments ×12, Gallica ×8, cameo.mfa.org ×8,
etc.) and work in a browser; 30 × 401 are all `player.vimeo.com` embeds, which
reject non-browser requests but embed fine; 6 × 429 were rate-limiting of the
checker itself.

## 5. Theme improvements (not yet applied)

In rough priority order:

1. **`<content>` is not an HTML element.** The theme's main wrapper everywhere
   is the deprecated Shadow-DOM-v0 tag, propped up with `display: block` in
   CSS. Replace with `<article>` or `<div class="content">` (rename the
   selector in `_page.scss`, `_toc.scss`, `_homepage.scss`, `_typography.scss`).
2. **Mobile nav toggle is invisible to assistive tech**
   (`layouts/partials/nav.html`): the checkbox is `display: none` (unfocusable;
   its `tabindex="0"` does nothing) and the label's only content is an
   `aria-hidden` SVG. Visually-hide the checkbox with the clip pattern instead,
   add `aria-label="Menu"` to the label, and a `:focus-visible` style.
3. **Footer CC license link has no accessible name**
   (`layouts/partials/footer.html`): `<a class="symbols">` contains only SVGs.
   Add `aria-label="Creative Commons BY-NC-SA 4.0"` and `aria-hidden="true"`
   on the icons.
4. **Homepage resource buttons are hardcoded in `layouts/index.html`**, but the
   README tells editors `menu: "resources"` front matter controls them — that
   mechanism doesn't exist. Either range over `.Site.Menus.resources` in the
   template or correct the README.
5. **Delete the anti-caching meta tags** in `layouts/_default/baseof.html`
   (`Cache-Control`/`Pragma`/`Expires` `http-equiv`): ignored by modern
   browsers, harmful if honored; CSS is already fingerprinted.
6. Housekeeping: delete the empty, unreferenced `layouts/partials/head.html`;
   plan the `resources.ToCSS` → `css.Sass` and internal
   `google_analytics.html` template migrations before the next Hugo upgrade
   (build currently pins 0.139.4); drop the never-shipped `-ms-`/`-o-` (and
   long-obsolete `-webkit-`/`-moz-`) keyframe prefixes in `_animation.scss`;
   hoist the repeated `#792421` maroon family into SCSS variables; load Google
   Fonts via `<link rel="preconnect">` + `<link>` instead of CSS `@import`
   (or self-host).
7. CI: bump `actions/checkout@v3` and the `peaceiris` actions to current
   majors, and add a `concurrency` group to `.github/workflows/gh-pages.yml`
   so rapid pushes can't race deploys.

## 6. Infrastructure note: production soft-404s

`teaching640.makingandknowing.org` returns **HTTP 200 with an HTML page for any
missing path** (the GitHub Pages dev site returns proper 404s). This hides
broken assets from status-code-based monitoring — every broken PDF/image above
"succeeded" with `text/html`. If the production host can be configured to
return real 404s, future link rot becomes much easier to catch; failing that,
any automated checks should validate `Content-Type`, not status.

## Re-running the checks

```sh
# Markdown lint (signal rules only — disable the stylistic bulk)
npx markdownlint-cli2 "content/**/*.md"

# Internal links: build, then verify every href/src resolves in the output
hugo --destination /tmp/rtc-build
# (see review notes: check each internal link target exists as a file,
#  <dir>/index.html, or <path>.html under /tmp/rtc-build)

# External links: extract unique outbound URLs from the build and curl them;
# treat 403 (bot-blocking) and vimeo 401s as needs-manual-check, not broken
```
