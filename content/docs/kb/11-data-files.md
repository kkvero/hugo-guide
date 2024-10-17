---
title: "Data Files"
date: "2024-10-17T11:26:18+07:00"
draft: false
weight: 21
---

Partials ant layouts can pull information from data files.
<br/>
`data` folder is a mini read-only DB.

1. Create `data/states.json`

```json
{
  "AL": {
    "name": "Alabama",
    "capital": "Montgomery",
    "lat": "32.361538",
    "long": "-86.279118"
  },
  "AK": {
    "name": "Alaska",
    "capital": "Juneau",
    "lat": "58.301935",
    "long": "-134.419740"
  }
}
```

2. Loop through data in `layouts/_default/single.html`
   {{< callout >}}
   _Access data via `.Site.Data.states`_
   {{< /callout >}}

```
{{ define "main" }}
<h3>Using json data file.</h3>
{{ range .Site.Data.states }}
  {{ .name }} - {{.capital}} <br />
{{ end }}
{{ end }}
```

In browser:

```
Using json data file.
Alaska - Juneau
Alabama - Montgomery
```
