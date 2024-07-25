# The Making and Knowing Project: Research and Teaching Companion

https://cu-mkp.github.io/research-teaching-companion/

Webpage content and navigation for the [Making and Knowing Project](https://makingandknowing.org/)'s Research and Teaching Companion (RTC), built on the [Hugo](https://gohugo.io/) framework.

For Making and Knowing Editors, see also [Publishing to the RTC](https://github.com/cu-mkp/research-teaching-companion/blob/main/how-tos/publishing-to-rtc.md).

- [Contributing](#contributing)
  * [Front matter](#front-matter)
  * [Content text](#content-text)
  * [Internal links](#internal-links)
  * [Images, documents, and other media](#images-documents-and-other-media)
  * [`_index.md` pages](#_indexmd-pages)
- [Publishing](#publishing)
- [Development](#development)
  * [Requirements](#requirements)
  * [Commands](#commands)
  * [Theming and templates](#theming-and-templates)

## Contributing

Content pages are stored in the `content/` directory. Each content page is a Goldmark-flavored Markdown (`.md`) file. To contribute to the site content, you may edit the Markdown files directly, or add new ones. The page's URL will be determined by its location in the folder structure.

### Front matter

At the top of each Markdown file is metadata called "[front matter](https://gohugo.io/content-management/front-matter/)", separated from the rest of the file by three dashes (`---`) on either side. The following front matter information will be used by the site:

-   `title` populates the heading/banner at the top of the page, and if the page will appear in the top navigation, this value will appear there as well.
-   `menu` indicates which, if any, menu(s) the page should appear in.
    -   Currently, the only supported values are `"main"` (the top navigation that appears on every page) and `"resources"` (the buttons that appear on the homepage and the Resources page to link to the available resources).
-   `weight` determines the order of the page in a menu.
    -   Higher values are "more" weight, which means the item "falls" to the bottom of the list, and lower values are "less" weight, which means the item "floats" to the top of the list. A bit counter-intuitive, but the items that should appear first should have lower numbers.
-   `draft` indicates whether or not this page should be public (`false`) or hidden (`true`).
-   `slug` determines the page's URL, but this will be generated automatically so there is no need to provide it unless you wish to override the generated URL.

Other front matter metadata, such as `tags`, `date`, and `author`, may be used in the future, but will currently be ignored.

### Content text

After the front matter, the rest of the page must be formatted as Goldmark-flavored Markdown. [Markdown Guide](https://www.markdownguide.org/tools/hugo/) provides a handy guide for the Markdown syntax supported by Goldmark.

Headings of levels `## Two` and `### Three` will populate the table of contents on the left side of each document. Headings of level two will also have a thin horizontal rule beneath them.

### Images, documents, and other media

All non-markdown media should be placed in the `static/` directory. For ease of use, it is currently structured as two folders: `img` for images, and `documents` for all other media (e.g. `docx`, `pptx`, `pdf`).

These work differently from the other internal links. Instead of the `ref` tag, just use normal Markdown link or image syntax, treating `static/` as the base of the URL. It is important that each URL includes a leading slash. For example:

```markdown
![stucco-molded](/images/stucco-molded.jpg)
[PDF (student handout)](/documents/activity-sheets/stucco_assignment_student-handout.pdf)
```
### Links to resources and content in this repository
- make sure you include the full filepath, starting from either `/static/` or `/content/`
     - So if you want to link to [research-teaching-companion/content/resources/activity-sheets/activitysheet_jasper.md](https://github.com/cu-mkp/research-teaching-companion/blob/main/content/resources/activity-sheets/activitysheet_jasper.md?plain=1), use the path `/resources/activity-sheets/activitysheet_jasper/`
- make sure to include a leading `/`
     - RIGHT: `/resources/activity-sheets/activitysheet_jasper/`
     - WRONG: `resources/activity-sheets/activitysheet_jasper/`  
- for markdown pages, do not include `.md`,  but do include a trailing `/`
     - So `resources/activity-sheets/activitysheet_jasper.md` becomes `/resources/activity-sheets/activitysheet_jasper/`
     - RIGHT: `/resources/activity-sheets/activitysheet_jasper/`
     - WRONG: `/resources/activity-sheets/activitysheet_jasper.md`
- for static resources, include the file extension and do not include a trailing `/`
     - RIGHT: `/documents/pdf/activitysheet_Jasper_preparation-of-horn.pdf`
     - WRONG: `/documents/pdf/activitysheet_Jasper_preparation-of-horn.pdf/`

#### Links to other pages (i.e., `.md` files under `content/`):
`[Making Varnishes](/resources/activity-sheets/activitysheet_varnishes/)` <br><br>
`[Digital Project](/resources/digital/EXAMPLEPAGE/)` <br><br>
`[Bibliography](/resources/reflection/bibliography/)` <br><br>
`[Student Project - Alberts](/resources/student-projects/fa21_alberts_naomi_final-project_ph-lesson/)` <br><br>
`[Syllabus SP23](/resources/reflection/syllabi/syllabus_sp23_gu4962-hands-on-history/)`

#### Links to pdfs, handouts, etc (i.e., files under `static/`):
`[pdf example](/documents/pdf/activitysheet_Jasper_preparation-of-horn.pdf)` <br><br>
`[docx example](/documents/docx/activitysheet_Jasper_preparation-of-horn.docx)`

#### Images:
`![jasper-part3](/images/jasper-part3.png)`

For more information about internal links, see the Hugo documentation on [Links and Cross References](https://gohugo.io/content-management/cross-references/).

### `_index.md` pages

There is a special kind of page at the root of each subfolder called `_index.md`. This represents the category root and can be used to list all the subpages. In RTC, we use them for three purposes:

1. Display the homepage (`content/_index.md`)
2. List the subpages of the "Resources" page (`content/resources/_index.md`) and indicate where the "Resources" page should appear in the main menu
3. Display content that should appear at the root of the "Activity Sheets" and "Student Projects" folders (the `_index.md` in each of those folders)

To achieve the RTC structure, there is a rule in place that these pages will only show a list of their subpages if:

1. they are not the homepage AND
2. they are a top-level category

In other words, only the "Resources" page currently matches that description. A developer may change this rule in the file `themes/rtc/layouts/_default/list.html`.

## Publishing

Every time changes are pushed to the `main` branch, a GitHub action will execute and publish content to the `gh-pages` branch. Make sure not to modify or remove this branch.

## Development

### Requirements

-   [Hugo](https://gohugo.io/) v0.104.2+

### Commands

#### `hugo server`

Run this command to serve the site over localhost, with hot-reloading.

#### `hugo`

Run this command to build the static site and output into the `public/` directory.

### Theming and templates

The custom theme is based on the Edition 640 theme and is composed of Go Templates HTML and SASS-flavored CSS. It can be edited in `themes/rtc/`, under `layouts/` for Go Templates/HTML and `assets/scss/` for CSS. See [Hugo documentation on templating](https://gohugo.io/templates/introduction/) for more information.

### NOTES from NJR+THC about building site on NJR's WSL (2024-07-17)

1. `git pull`
2. `rm -rf public/` to clear anything in the `public/` directory [[we have tested this -- without wiping this directory first, the build takes MUCH longer]]
3. `hugo`
4. `aws s3 sync ./public/ s3://teaching640-dev/ --delete` to push build to the bucket in AWS S3 of `teaching640-dev` which is now routing to teaching640.makingandknowing.org
