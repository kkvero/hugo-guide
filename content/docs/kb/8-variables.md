---
title: "Variables"
date: "2024-10-17T10:22:20+07:00"
draft: false
weight: 18
---

### Built-in variables

All Hugo [built-in variables](https://gohugobrasil.netlify.app/variables/).
<br/>
(Site, Page, Taxonomy, Menu variables)

- Can use Go variables only in `layouts/` files.
- Can access variables defined in .md files front matter. E.g.:

```
  {{ .Title }}
  {{ .Date }}
  {{ .Permalink }}
  {{ .Kind }} // prints the kind of page
```

### Custom variables

##### 1. Vars Defined in front matter (.Params.var)

Access them with `{{ .Params.varName }}`.
<br/>
{{< callout >}}
_So default vars without `.Params`, custom vars with `.Params`._
{{< /callout >}}

- Define a default var in `content/a.md`

```markdown {hl_lines=[9]}
+++
title = 'A'
date = 2024-10-10T20:37:08+07:00
draft = true
author = 'Mike'
tags = ['tag1', 'tag2', 'tag3', 'сиреневый', 'tag4']
categories = ['cat1']
moods = ["Happy", "Upbeat"]
myVar = 'MyValueHere'        
+++
```

- Use a default var, `layouts/_default/single.html`

```html
{{ define "main" }} This is the single template.
<br />
{{.Title}}
<br />
{{.Params.myVar}} {{end}}
```

##### 2. Vars declared in .html layout templates

- Declare
  <br/>
  `{{ $myVarName := "aString" }}` (can be numeric, int, bool, string)
- Use
  <br/>
  `{{ $myVarName }}`

E.g., to change CSS styling using variables:
<br/>
(set this to different color in b.md etc)

```markdown {filename="content/a.md" hl_lines=[3]}
+++
title = 'A'
color = 'blue'        
+++
```

```html {filename="layouts/_default/single.html"}
{{ define "main" }}
<h1 style="color: {{.Params.color}};">This is the single template.</h1>
{{end}}
```
