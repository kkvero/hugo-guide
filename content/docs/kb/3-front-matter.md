---
title: "Front Matter"
date: "2024-10-16T14:27:06+07:00"
draft: false
weight: 13
---

- Metadata, data about our content files, in YAML, TOML, JSON markdown languages. Here you specify page attributes that you can later use in layouts.

```yaml {filename="a.yaml"}
---
title: "A"
---
```

```markdown {filename="a.toml"}
+++
title = 'A'
+++
```

- Can create custom front matter variables.
  `content/a.md`:

```markdown
+++
title = 'A'
date = 2024-10-10T20:37:08+07:00
draft = true
author = 'Mike'  # added
+++
```

Remember to do so for all .md files that will be using this variable (for `content/dir1/b.md` etc.)
<sub>Humans have front matter: name, age, weight etc.</sub>

- How you would use front matter variables in a layout:

```html
<html>
  <head>
    <meta charset="UTF-8" />
    <title>{{ .Params.Title }}</title>
  </head>
  <body>
    <p>Written By : {{ .Params.Author }}</p>
    {{ .Content }}
  </body>
</html>
```
