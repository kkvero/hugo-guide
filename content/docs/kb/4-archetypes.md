---
title: "Archetypes"
date: "2024-10-16T15:46:55+07:00"
draft: false
weight: 14
---

_Archetype = prototype = template for front matter._

Control what gets put into the front matter of .md files when you create them with `hugo new content content/file.md`.

#### Front matter for specific directories.

By default the archetype used for front matter is in:
`archetypes/default.md`
<br/>
To use another archetype, create e.g.:
`archetypes/dir1.md`
<br/>
To use this archetype:
`hugo new content content/dir1/c.md`
