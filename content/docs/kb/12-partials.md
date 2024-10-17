---
title: "Partials"
date: "2024-10-17T11:34:00+07:00"
draft: false
weight: 22
---

Implement modularity with partials.
Possible modules/parts: header, main body, footer, navigation/menu, table of contents, social media links, breadcrumbs.

- Create `layouts/partials/header.html` (creating `partials` dir)

#### Version 1

```html {filename="layouts/partials/header.html"}
<h3>Header partial</h3>
<h1>{{ .Title }}</h1>
<p>{{ .Date }}</p>
Written By : {{ .Params.author }}
<hr />
```

```html {filename="layouts/_default/single.html"}
{{ partial "header" . }}
```

{{< callout >}}
**Passing . to partial**
<br/>
Passing the current page as context to the partial so that it would use _this_ page's title and date. I.e. passing the scope of this page, i.e. all the variables of this scope/page so that the partial can use these variables.

{{< /callout >}}

#### Version 2

```html {filename="layouts/_default/single.html"}
<h3>Header partial</h3>
<h1>{{ .myTitle }}</h1>
<p>{{ .myDate }}</p>
<hr />
```

Note that we also use a . (.myTitle)

- `layouts/_default/single.html`
  Pass in a dictionary, instead of the current page context.

```html {filename="layouts/_default/single.html"}
{{ partial "header" (dict "myTitle" "myCustomTitle" "myDate" "myCustomDate") }}
```

#### Example 3

To pass in a custom CSS color into the partial.
<br/>
Partial:

```html
<header style="”background-color:" {{ .color }}”>
  <h1>Mike's Travel Blog</h1>
  <hr />
</header>
```

Layout template that includes this partial:

```html
{{ partial “header.html” (dict “color” “blue” )}}
```
