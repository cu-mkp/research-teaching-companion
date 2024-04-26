> Last updated 2024-04-26 by NJR & THC

# Publishing to the Research and Teaching Companion Site
The publicly-available [Research and Teaching Companion (RTC) Site](https://cu-mkp.github.io/research-teaching-companion/) is powered through Github Pages. Input for site content is in Github-flavored Markdown. Whenever possible and appropriate, resources and pages for the Sandbox site should be in Markdown.

## Structure of the repo
The `/content/` directory contains all the pages in the RTC website in `.md` format which is automatically converted to `.html` when the site is built by Hugo. Work here to edit any of the webpages of the site (e.g., ["About"](https://cu-mkp.github.io/research-teaching-companion/about/)).

The `/static/` directory contains files that are placed at the root of the website as is. These are principally files to be downloaded by visitors of the site (e.g., powerpoint presentations) and images to be embedded into the webpages.

In sum:
- Edit webpages: work in `/content/`
- Include images in webpages: upload to `/static/images`
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

`[type]_[semester+year]_[lastname]_[firstname]_[subject or title or short description].[file extension]`

delimited `-` within each field

*File extensions*
- If you are working on a webpage, make sure the file extension is `.md`
- If you are working on a downloadable resource, make sure the file extension is correct for the type of file (e.g., `.pdf`, `.pptx`, `.xlsx`, etc)

If a file does not have one of these values (e.g., there is no "name" associated with it), simply omit that segment.

You can use the original name of the document in the title segment, but sanitize it to meet the requirements described in [Naming Protocols](naming-protocols.md#guidelines) and pre-pend type and date and name information (if decipherable).


### `[type]` values:
  1. `syllabus` = Making & Knowing Syllabi
  2. `casestudy`= Using M&K Resources
  3. `activitysheet`= Lesson Plans for Hands-On
  4. `project` = Student Projects
  6. `reflection` = Reflections on Hands-On
  7. `digital` = Digital Fr. 640

### `[semester]` and `[year]` format:

\["fa" | "sp" | "su" ] + [YY]
e.g., "fa17" for fall 2017, or "sp16" for spring 2016, or "su21" for summer 2021

| Name     | Label   |
|----------|---------|
| Fall     | `fa`    |
| Spring   | `sp`    |
| Winter   | `wn`    |
| Summer   | `su`    |

### Examples by type
Follow the basic protocols described in [Naming Protocols](naming-protocols.md#guidelines).

#### 1. Syllabus

`syllabus_[date]_[lastname]_[firstname]_[brief title which can include course number and short name of course].[file extension]`

e.g., `syllabus_sp22_nielson_christina_arth-295-ingenious-making.md`

#### 2. Casestudy

Webpage: `casestudy_[date]_[lastname]_[firstname]_[brief title which can include course number and short name of course].[file extension]`

e.g., `casestudy_sp22_nielson_christina_arth-295-ingenious-making.md`

#### 3. Activitysheet

Webpage: `activitysheet_[date]_[lastname]_[firstname]_[brief title or desription of activity].[file extension]`

e.g., `activitysheet_sp22_azurite-preparation.md`

#### 4. Project -- THESE ARE NAMED DIFFERENTLY TO THE OTHER TYPES

Leave these with their current names which follow the protocols for naming in the [M&K Sandbox](https://github.com/cu-mkp/sandbox/blob/main/publishing-to-sandbox.md).

Webpage: `[semester+year]_[last name]_[first name]_final-project_[short descriptive title].md`

e.g,: `sp22_nebolsin_victoria_final-project_animal-rationality.md`

#### 5. Reflection

Webpage: `reflection_[date]_[lastname]_[firstname]_[brief title or description].[file extension]`

e.g., `reflection_smith_pamela_reconstruction-insights.md`

#### 6. Digital

Webpage: `digital_[date]_[lastname]_[firstname]_[brief title or description].[file extension]`

e.g., `digital_rosenkranz_naomi_entry-categories.md`

### Naming protocol for static documents:
`[type]_[date]_[name]_[brief title which can include course number and short name of course].[file extension]`

e.g., `casestudy_sp22_nielson_arth-295-ingenious-making.docx`

## Adapted from the repo [readme.md](https://github.com/cu-mkp/research-teaching-companion/blob/main/README.md)

## Contributing

Content pages are stored in the `content/` directory. Each content page is a Goldmark-flavored Markdown (`.md`) file. To contribute to the site content, you may edit the Markdown files directly, or add new ones. The page's URL will be determined by its location in the folder structure.

### Front matter - mostly for NJR & THC

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

### Links

- To link to other pages on the site, use the `ref` tag surrounded by double brackets
     - `[`*Text you would like to link*`]({{<ref "`*name of file*`" >}})` 
     - e.g., `[Stucco for Molding Assignment Sheet]({{<ref "activity_sp22_azurite-preparation" >}})`
- To link to external links, use typical Markdown link syntax
     - `[`*Text you would like to link*`](`*URL*)` 
     - e.g., `[folio 120v in BnF Ms. Fr. 640](https://edition640.makingandknowing.org/#/folios/120v/f/120v/tl)`

Note that you do not need to give the entire path for `ref` tags, unless there are multiple Markdown files with the same name. You also do not need to include the `.md`. All of the following will work, but the first is much simpler!

```markdown
[Stucco for Molding]({{<ref "stucco-assignment" >}})
[Stucco for Molding]({{<ref "activity-sheets/stucco-assignment.md" >}})
[Stucco for Molding]({{<ref "/resources/activity-sheets/stucco-assignment.md" >}})
```

For more information about internal links, see the Hugo documentation on [Links and Cross References](https://gohugo.io/content-management/cross-references/).

#### Including external URLs (from NJR & THC about sustainability)
Whenever we include links to external resources, we need to consider whether those URLs and resources meet our plans for digital sustainability.
- If possible, use a persistent identifier such as a DOI or "permanent URL."
- If possible, if the resource is also stored in a digital repository (e.g., Academic Commons, JSTOR, Internet Archive), cite that location for the resource.
- If you are citing a webpage that is not a formal pulication (such as a blog), look for a version in Internet Archive and include that link in addition to the original (e.g., but adding "archived at [link]). If there is no version available there, use the service provided by Internet Archive and the Wayback Machine to create an archivable link: [Save Pages in the Wayback Machine](https://help.archive.org/help/save-pages-in-the-wayback-machine/).


### Images, documents, and other media

All non-markdown media should be placed in the `static/` directory. For ease of use, it is currently structured as two folders: `img` for images, and `documents` for all other media (e.g. `docx`, `pptx`, `pdf`).

These work differently from the other internal links. Instead of the `ref` tag, just use normal Markdown link or image syntax, treating `static/` as the base of the URL. It is important that each URL includes a leading slash. For example:

```markdown
![stucco-molded](/images/stucco-molded.jpg)
[PDF (student handout)](/documents/activity-sheets/stucco_assignment_student-handout.pdf)
```

### `_index.md` pages

There is a special kind of page at the root of each subfolder called `_index.md`. This represents the category root and can be used to list all the subpages. In RTC, we use them for three purposes:

1. Display the homepage (`content/_index.md`)
2. List the subpages of the "Resources" page (`content/resources/_index.md`) and indicate where the "Resources" page should appear in the main menu
3. Display content that should appear at the root of the "Activity Sheets" and "Student Projects" folders (the `_index.md` in each of those folders)

To achieve the RTC structure, there is a rule in place that these pages will only show a list of their subpages if:

1. they are not the homepage AND
2. they are a top-level category

In other words, only the "Resources" page currently matches that description. A developer may change this rule in the file `themes/rtc/layouts/_default/list.html`.

# Markdown cheatsheet

See also [M&K's introduction to Github and Markdown](/intro-to-github.md)
Markdown is the language used throughout Github and, as its name suggests, is a simplified markup language that allows you to style and format text and media, which converts readily to html, but is much easier to pick up and write with. See [Basic writing and formatting syntax in Markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) for details about how to format text (e.g., bold, italics, lists, headers, etc). See also [Programming Historian's Markdown Guide](https://programminghistorian.org/en/lessons/getting-started-with-markdown).

## Some often-used formatting

**Bold** = `**Bold**`

*Italics* = `*Italics*` or `_Italics_`

`code` = \` code \` [add a back-tick before and after]

> quotes or blockquotes

= `> quotes or blockquotes`

[Links](https://github.com/cu-mkp/research-teaching-companion) = `[Links](https://github.com/cu-mkp/research-teaching-companion)`

![image](https://github.com/cu-mkp/research-teaching-companion/assets/14779727/ab652440-8023-4085-9f66-d54a2bedfa93) = `![alt text for the image](/images/stucco-molded.jpg)` 

Or you can use html styling, `<img src="./images/image7.png" alt="A black and white drawing of a person holding a vase" />`


Headings:
- `#` indicates a header. Add additional `#` to create nested headings
- For example:

# Heading 1
## Heading 2
### Heading 3

This is styled as
```
# Heading 1
## Heading 2
### Heading 3
```



< -- WE NEED TO WORK ON THIS -- >
## Images
Images to be used in the website should be uploaded to `/static/images/`. Note: Hugo will place this directory at the root of the website, e.g., `teaching640.makingandknowing.org/images`.

## Naming protocol for images:
Follow the basic protocols described in [Naming Protocols](naming-protocols.md#guidelines).

`[name of menu]-[short description of image].[file extension]`

e.g., `howtouse-del.png`

`[name of menu]-[menu item label]-[short description of image].[file extension]`

e.g., `about-sponsors-NSF.png`
