---
title: "Baseof"
date: "2024-10-16T17:31:21+07:00"
draft: false
weight: 5
---

## Baseof template & using `block` entities

All templates: single, list inherit from the `baseof.html`.

- Create `giraffe_site/layouts/_default/baseof.html`
  and define `main` and `footer` blocks.

```html {hl_lines=[11, 13]}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    Top of baseof.
    <hr />
    {{ block "main" . }} {{ end }}
    <br />
    {{ block "footer" . }} This is the default baseof Footer. {{ end }}
    <hr />
    Bottom of baseof.
  </body>
</html>
```

- Modify main and footer blocks in `giraffe_site/layouts/_default/single.html`

```
{{ define "main" }}
  This is the single template.
  {{end}}
{{define "footer"}}
  This is the single footer.
{{end}}
```

- Modify only main block in `giraffe_site/layouts/_default/list.html`
  <br/>
  (will use the default footer of `baseof.html`)

```
{{ define "main" }}
  This is the list template.
{{ end }}
```

- In browser the list pages are displayed something like:

```
Top of baseof.
---
This is the list template.
This is the default baseof Footer.
---
Bottom of baseof.
```

**_What other blocks there can be?_**
<br/>
(title, main, footer)
<br/>
<br/>
Parent template (`_default/baseof.html`):

```
<head>
  <meta charset="UTF-8" />
  <title>{{ block "title" . }}
  {{ end }}
  </title>
</head>
```

Child template

```
{{ define "title" }}
  {{ .Title }} | My Travel Blog
{{ end }}
{{ define "main" }}
<article>
  <h1>{{ .Title }}</h1>
  {{ .Content }}
</article>
  {{ end }}
{{ end }}
```
