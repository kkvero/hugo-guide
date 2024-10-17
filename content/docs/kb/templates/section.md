---
title: "Section"
date: "2024-10-16T17:31:14+07:00"
draft: false
weight: 4
---

### Section templates

By default all single pages use `layouts/_default/single.html`, list pages use `layouts/_default/list.html` (be it html in your themes/ dir or if you override them in `layouts` dir.)
<br/>
But **if you want some pages to use a different template.**
<br/>
Use section templates.

- With a structure like this

```
content/
├── a.md
├── dir1
│   ├── b.md
│   ├── c.md
│   ├── dir2
│   │   ├── d.md
│   │   └── _index.md
│   └── _index.md
└── _index.md
```

- To make pages in dir1 use a different template-layout. Create a section-folder for dir1 in layouts.
  _Note that files in /dir1/dir2/../ will also use this layout_

```
layouts/
├── _default
│   ├── list.html
│   └── single.html
└── dir1              <==
    └── single.html   <==
```

And make a custom `layouts/dir1/single.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <!--adding-->
    <p>This is in dir1.</p>
    {{.Content}}
  </body>
</html>
```
