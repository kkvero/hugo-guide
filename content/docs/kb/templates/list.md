---
title: "List"
date: "2024-10-16T17:29:58+07:00"
draft: false
weight: 1
---

## List page templates

- With this structure of `content` dir:
  <br/>
  (`_index.md` in each dir)

```
content
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

- `_index.md` - are our list pages
- They use `themes/ga-hugo-theme/layouts/_default/list.html` template.

#### To override a theme template

- Create a file with exactly the same name and path as in the theme that you use.
  <br/>
  In theme:
  <br/>
  `themes/ga-hugo-theme/layouts/_default/list.html`
  <br/>
  Create:
  <br/>
  `layouts/_default/list.html`
  <br/>
  So we don't change the template in themes, but perhaps copy/paste from there and modify.

#### Making our custom list.html

A simple way to list all the containing pages (inside a dir) and link page titles to their urls:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    {{.Content}}
    <!--It is a list page so: Display the list of pages-->
    <ul>
      {{ range .Pages }}
      <li><a href="{{ .Permalink }}"> {{ .Title }}</a></li>
      {{ end }}
    </ul>
  </body>
</html>
```

Will display in browser at `http://localhost:1313/dir1/`:

```
Welcome to dir1.

- Dir2  #and those are links
- B
- C
```

Troubleshooting:
<br/>
-Note the link to dir2 is dir1/dir2/
<br/>
-Use .Permalink not .URL, deprecated.
