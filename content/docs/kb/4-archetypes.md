---
title: "Archetypes"
date: "2024-10-16T15:46:55+07:00"
draft: false
weight: 14
---

_Archetype = prototype = template for content files._

Control what gets put into the markdown `.md` files when you create them with `hugo new content content/file.md` (the same as `hugo new file.md`).

#### Content template for specific directories

By default the archetype that is used is in:
`archetypes/default.md`
<br/>
To use another archetype, create e.g.:
`archetypes/dir1.md`
<br/>
To use this archetype:
`hugo new content content/dir1/c.md`
