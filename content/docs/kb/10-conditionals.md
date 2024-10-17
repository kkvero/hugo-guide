---
title: "Conditionals"
date: "2024-10-17T11:16:49+07:00"
draft: false
weight: 20
---

{{< callout >}}
`eq, lt, le, gt, ge, not`
{{< /callout >}}

```
{{$var1 := "dog"}}
{{$var2 := "cat"}}
{{if eq $var1 $var2}}
<!--or if not (eq $var1 $var2) -->
  True
{{else}}
  False
{{end}}
```

{{< callout >}}
`and, or`
{{< /callout >}}
`{{if and (lt $var1 $var2) (lt $var1 $var3)}}`

- List all pages on the site and if it is the current page, style it differently.

```html
{{$title := .Title }}
<!-- Stores the title of the current page.-->
{{range .Site.Pages}}
<li>
  <a
    href="{{.Permalink}}"
    style="{{if eq .Title $title}} background-color:yellow; {{end}}"
    >{{.Title}}</a
  >
</li>
{{end}}
```

BUT: this lists tags and categories as well!
