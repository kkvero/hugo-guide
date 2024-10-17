---
title: "Functions"
date: "2024-10-17T10:46:42+07:00"
draft: false
weight: 19
---

#### Syntax

`{{  func-name arg1, arg2, … , argX }}`

#### Common functions

- `{{ truncate N }}` (Truncates to N characters long, counting spaces. )
  <br/>
  `{{ truncate 10 "This is a really long string."}} `
  <br/>
  Displays in browser as: This is a …
- Arithmetic
  <br/>
  `{{ add 1 5 }}` (also: `sub`)
  <br/>
  In browser: 6
- `range`

```html
{{ range .Pages }}
<!--Here can access variables of that page-->
{{ .Title }} <br />
{{ end }}
```

Used in list pages to iterate over all pages in a section.
<br/>
_All pages on the site: `{{range .Site.Pages}}`_

- `first`, `last`
  <br/>
  `{{ range first 3 .Pages }}` Show only first 3.
- `where`

```
{{ .Range .Site.Sections.Asia.Pages where “Title” contains “Korea” }}
	{{ .Title }}
{{ end }}
```

FYI couldn't get even this part alone to work `.Range .Site.Sections.Asia.Pages`
<br/>
`.Range .Site.Sections.dir1.Pages`
<br/>
Supposed to be all pages in dir 'Asia' or dir 'dir1'.
