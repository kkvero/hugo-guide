---
title: "Templates"
date: "2024-10-16T17:23:31+07:00"
draft: false
weight: 17
---

### Template basics

Working with templates is like building your own theme.
<br/>
Layouts dir of the theme that we use:

```
themes/ga-hugo-theme/layouts
├── 404.html
├── _default
│   ├── list.html
│   └── single.html
└── partials
    ├── footer.html
    └── header.html
```

Layouts is the skeleton html for all of your content.

- Go ahead and add a line in `themes/ga-hugo-theme/layouts/_default/single.html` template.
  It will be displayed on all single pages.

```html
<body>
  {{ partial "header" (dict "Kind" .Kind "Template" "Single") }}
  <p>Welcome to a single page!</p>
  <!--***-->
  <div style="margin: 25px">
    <h1>{{.Title}}</h1>
  </div>
</body>
```
