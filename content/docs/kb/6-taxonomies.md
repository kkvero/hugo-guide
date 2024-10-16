---
title: "Taxonomies"
date: "2024-10-16T16:52:30+07:00"
draft: false
weight: 16
---

Ways to organize, logically group content.
For that Hugo provides:

#### Tags, Category

Built in taxonomies.
{{< badge content="tags = keywords, categories = groups" type="warning" >}}

To implement taxonomies, we use the front matter.

- _Add tags, categories taxonomies_ in a content file like `content/a.md`

```markdown
---
title: "A"
tags: ["tag1", "tag2"]
categories: ["cat1"]
---
```

_Display taxonomies._
Then you can display tags and categories of a page when e.g. displaying a card for each page.

_Hugo creates pages for taxonomies._
Clicking on a tag name brings you to a list page of this tag e.g. that lists all related posts. The url will look like: `tag/tags3`

#### Custom taxonomies

- **Use in content .md files**

```markdown
---
title: "A"
tags: ["tag1", "tag2"]
categories: ["cat1"]
moods: ["Happy", "Upbeat"] #added
---
```

Unlike the default taxonomies (Hugo creates urls for tags, categories), Hugo will not create e.g. moods/happy page.

- **Make url pages for custom taxonomies**
  <br/>
  To remedy this, in `hugo.toml` add `[taxonomies]` section (note must list the default taxonomies as well):

```toml
baseURL = 'https://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'ga-hugo-theme'
[taxonomies]
  tag = "tags"         #singular = plural
  category = "categories"
  mood = "moods"
```

- **Displaying content with the same taxonomy term**
  <br/>
  (E.g. for a custom taxonomy 'languages', with value 'english'.)

```
{{ range .Site.Taxonomies.languages.english }}
    // in here we can access the page’s information
    {{ .Title }}
    {{ .Description }}
{{ end }}
```

- **What other custom taxonomies we could make**
  <br/>
  -language (for a travel blog. So show all posts where the spoken language in a country is English)
  <br/>
  -color (show all works of that color)
