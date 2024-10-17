---
title: "Using Theme"
date: "2024-10-17T13:45:59+07:00"
draft: false
weight: 2
---

Getting started with a theme is all right but how to actively use its components. See the full description in the [theme docs](https://imfing.github.io/hextra/). Here is the summary of the most used features.

### Directory structure

- To modify the format of the front matter being generated in your .md content files. If we want it to be in .yaml. Modifying `hugo-guide/archetypes/default.md` to (just using the .yaml syntax):

```markdown
---
title: '{{ replace .File.ContentBaseName "-" " " | title }}'
date: "{{ .Date }}"
draft: false
---
```

- Generate new md files with e.g.

```shell
hugo-guide$ hugo new content/about.md
```

- The beginning of the content folder will look something like:

```shell
content
├── hugo-guide
│   ├── about
│   │   └── _index.md
│   ├── deploy
│   │   ├── configure-theme.md
│   │   └── _index.md
│   ├── _index.md
│   └── knowledge-base
│       ├── 1-install-theme.md
│       └── _index.md
└── _index.md
```

It might look over nested but the purpose is to display the main sections in the left menu like:

```
Knowledge base
  Install
Deploy
  Use theme
About
```

Otherwise the section titles "Knowledge base", "Deploy" are not displayed.

{{< callout type="info">}}
**Alternative menu layout.**
<br/>
Alternative without nesting in subdir `hugo-guide`. Would display:

- Main menu horizontally above.
- Left menu would show only the contents of the current section, plus sections that we specify in `hugo.yaml` (read on for details).
  {{< /callout >}}

### Menu

- To make the left menu display in your desired order (and not the alphabetical order by default), add to the front matter of each section, i.e. to each `_index.md` of folders like `content/hugo-guide/knowledge-base/_index.md`:

```markdown
weight: 1
```

- Add menu at the top. In `hugo.yaml`:

```yaml
menu:
  main:
    - name: Knowledge Base
      pageRef: /hugo-guide/knowledge-base
      weight: 1
    - name: Deploy
      pageRef: /hugo-guide/deploy
      weight: 2
    - name: About
      pageRef: /hugo-guide/about
      weight: 3
```

#### Sidebar

Add to hugo.yaml. To display pages that are external links or pages that don't make a section, e.g. if we had:

```shell {hl_lines=[7]}
content
├── hugo-guide
│   ├── _index.md
│   └── knowledge-base
│       ├── 1-install-theme.md
│       └── _index.md
|-- about.md
└── _index.md
```

```yaml {filename="hugo.yaml"}
menu:
  sidebar:
    - name: "| Go to Hugo Docs Website"
      url: "https://gohugo.io/documentation/"
      weight: 4
    - name: "About"
    - url: /about
    - weight: 3
```

- When on a single page, to make the side bar visible.
  <br/>
  In your single pages like `content/knowledge-base/1-install-theme.md` add to front matter:

```markdown
cascade:
type: docs
```

Then this page will use the [hextra theme layout](https://imfing.github.io/hextra/docs/guide/organize-files/#layouts) type `docs`.

### Logo

The "Hextra" round logo.
<br/>
Logo is displayed by default. However adding the following to `hugo.yaml` makes sure a different logo is used for the dark mode (otherwise logo is invisible in dark mode), plus can resize logo image.

```yaml
params:
  navbar:
    displayTitle: true
    displayLogo: true
    logo:
      path: images/logo.svg
      dark: images/logo-dark.svg
      link: /hugo-guide
      width: 40
      height: 20
```

### Footer

- Copyright
  <br/>
  Create `i18n/en.yaml` (in the existing `i18n` folder) and specify your copyright text:

```yaml
copyright: "&copy; 2024 Veronika Kirichenko"
poweredBy: "Powered by Hugo and Hextra"
```

- To make this show up, add to `hugo.yaml` `params` section:

```yaml
params:
  footer:
    displayCopyright: true
    displayPoweredBy: true
    width: normal
```

{{< callout >}}
Be sure not to add another `params` section, but to add to an _existing_ `params` section.
{{< /callout >}}

### Syntax Highlighting

- Add filename to code snippets.
  Hextra theme feature. E.g.:

````markdown
```yaml {filename='hugo.yaml'}
# your code
```
````

### Shortcodes

The following features are implemented as shortcodes in theme Hextra.
To make sure shortcodes work, add to `hugo.yaml`:

```yaml
enableInlineShortcodes: true
```

##### Callout

```markdown
{{</* callout type="info" */>}}
Some text.
{{</* /callout */>}}
```

Types: info, warning.

##### Badge

To make small buttons.

{{< badge content="Badge" link="https://imfing.github.io/hextra/docs/guide/shortcodes/others/#badge" >}}

- Also on this page: insert pdfs, youtube.

### Landing Page

- Code for the landing page is [here](https://github.com/imfing/hextra/discussions/411).
  Take whatever you need and use it in your `content/_index.md`.
- How to use the "wide" layout for the landing page.
  <br/>
  Trying out Hextra settings for the [layout](https://imfing.github.io/hextra/docs/guide/organize-files/#layouts) did not work for me.
  So had to go by the book. As we've learned in "Knowledge base" section: the home page is also a list page, so by default it uses list.html template.

  To create a separate template for the home page, create `layouts/index.html`
  Hextra theme provides wide layout html [here](https://github.com/imfing/hextra/blob/main/layouts/_default/wide.html). Paste it into the created `layouts/index.html`.

  Or try meddling with [page width](https://imfing.github.io/hextra/docs/guide/configuration/#page-width).
