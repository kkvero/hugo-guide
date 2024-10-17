---
title: "Single"
date: "2024-10-16T17:30:40+07:00"
draft: false
weight: 2
---

### Single Page Templates

To override the default template you would create
`layouts/_default/single.html`
<br/>
With content like:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <h1>Header</h1>
    <hr />
    <h3>{{ .Title }}</h3>
    <h4>{{.Date}}</h4>
    {{.Content}}
    <hr />
    <h2>Footer</h2>
  </body>
</html>
```
