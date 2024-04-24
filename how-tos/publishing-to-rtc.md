> Last updated 2024-04-14 by NJR & THC

# Publishing to the Research and Teaching Companion Site
The publicly-available [Research and Teaching Companion (RTC) Site](https://cu-mkp.github.io/research-teaching-companion/) is powered through Github Pages. Input for site content is in Github-flavored Markdown. Whenever possible and appropriate, resources and pages for the Sandbox site should be in Markdown.

## Structure of the repo
The `/content/` directory contains all the pages in the RTC website in `.md` format which is automatically converted to `.html` when the site is built by Hugo. To edit any of the webpages of the site (e.g., ["About"](https://cu-mkp.github.io/research-teaching-companion/about/)).

The `/static/` directory contains files that are placed at the root of the website as is. These are principally files to be downloaded by visitors of the site (e.g., powerpoint presentations) and images to be embedded into the webpages.

In sum:
- Edit webpages: work in `/content/`
- Include images to webpages: upload to `/static/images`
- Provide downloadable content: upload to `/static/documents`

## File formats and location in Github repo

| Original file format               | Target File Format (in Github)                            | Location in Github repo       |
|------------------------------------|-----------------------------------------------------------|-------------------------------|
| New webpage                        | `.md` (Markdown)                                          | `/content/` or `/content/resources/`               |
| Googledoc, Word (`.docx`)          | `.docx` AND `.pdf`                                        | `/static/documents/`          |
| Googlesheets, Excel (`.xlsx`)      | `.csv` (if formatting is meaningful, ALSO upload `.xlsx`) | `/static/documents/`          |
| Googleslides, Powerpoint (`.pptx`) | `.pptx` AND `.pdf`                                        | `/static/documents/`          |
| PDF                                | `.pdf`                                                    | `/static/documents/`          |
| Images                             | `.jpg` or `.png`                                          | `/static/images/`             |


## Naming spec for files and pages

`[type]_[semester+year]_[lastname]_[firstname]_[subject or title or short description]`
delimited `-` within each field

`[semester]` format:
\["fa" | "sp" | "su" ] + [YY]
e.g., "fa17" for fall 2017, or "sp16" for spring 2016, or "su21" for summer 2021

`[type]` values:
  1. `syllabus`
  2. `casestudy`
  3. `activitysheet`
  4. `project`


# Images
Images to be used in the website should be uploaded to `/static/images/`. Note: Hugo will place this directory at the root of the website, e.g., `teaching640.makingandknowing.org/images`.

## Naming protocol for images:
Follow the basic protocols described in [Naming Protocols](naming-protocols.md#guidelines).


`[name of menu]-[short description of image].[file extension]`

e.g., `howtouse-del.png`

`[name of menu]-[menu item label]-[short description of image].[file extension]`

e.g., `about-sponsors-NSF.png`

## Naming protocol for webpages:
TBD. Follow the basic protocols described in [Naming Protocols](naming-protocols.md#guidelines).

`[type]_[date]_[name]_[brief title which can include course number and short name of course].md`

e.g., `casestudy_sp22_nielson_arth-295-ingenious-making.md`

## Naming protocol for static documents:
`[type]_[date]_[name]_[brief title which can include course number and short name of course].md`

e.g., `casestudy_sp22_nielson_arth-295-ingenious-making.docx`

Use the original name of the document in the title segment, but sanitize it to meet the requirements described in [Naming Protocols](naming-protocols.md#guidelines) and pre-pend type and date and name information (if decipherable).

## Including external URLs
Whenever we include links to external resources, we need to consider whether those URLs and resources meet our plans for digital sustainability.
- If possible, use a persistent identifier such as a DOI or "permanent URL."
- If possible, if the resource is also stored in a digital repository (e.g., Academic Commons, JSTOR, Internet Archive), cite that location for the resource.
- If you are citing a webpage that is not a formal pulication (such as a blog), look for a version in Internet Archive and include that link in addition to the original (e.g., but adding "archived at [link]). If there is no version available there, use the service provided by Internet Archive and the Wayback Machine to create an archivable link: [Save Pages in the Wayback Machine](https://help.archive.org/help/save-pages-in-the-wayback-machine/).

  

