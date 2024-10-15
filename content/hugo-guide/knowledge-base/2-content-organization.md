---
title: "Content Organization"
date: "2024-10-14T16:46:46+07:00"
draft: false
weight: 11
---

**Hugo has 3 content types: Home, List and Single.** <br/>
Home: because we often want to style Home different from the rest.
Single: for articles, posts.
List: table of content for single pages (the `_index.md` file in a folder with single pages), e.g.:

```
content/posts
├── 2024-10-01-i-like-to-roar.md
├── 2024-10-02-today-i-made-friends.md
├── 2024-10-03-vegan-experiment.md
└── _index.md
```

**Sections = folders** <br/> (`posts` folder above)
Many websites are separated into sections, generally a section of a website will have a landing page, this is basically a page that introduces the section and links to content in the section.
E.g. a travel blog can have sections: Europe, Asia etc.

{{% steps %}}

### Create some content

```shell
hugo new content content/a.md
hugo server -D   #to display drafts
```

**List pages, sublists/submenus for nested dirs**.
Note that if we create nested folders in `content`, like:

```
content
  dir1
    b.md
    c.md
     dir2
       d.md
  a.md
```

- On home page you will see:
  ```
  dir1
  a
  ```
- Hugo will also create list pages for folders at the root of content, like `content/dir1`:
  b,c,d (nothing about dir2)
  but not for `content/dir1/dir2` _by default_ anyway.
- But you can manually.

```shell
hugo new content content/dir1/dir2/_index.md
hugo server -D
```

- Now dir2 is listed:

```
  b
  c
  dir2
```

### Adding text to `_index.md` will appear on the list page of dir2.

### Add text to dir1 list page.

Because dir1 uses the default list page, to add text to it, we need to manually create `_index.md` for it too:

```shell
hugo new content content/dir1/_index.md
```

{{% /steps %}}

### Home page

- Again, just create `_index.md` for it, this time at the root of `content`.

```shell
hugo new content content/_index.md
```

Home page is treated as a list page.

{{< callout type="info" >}}
Home page and list pages are called `_index.md`
{{< /callout >}}
