---
title: "Install Theme"
date: "2024-10-14T11:12:44+07:00"
draft: false
cascade:
  type: docs
weight: 11
---

### Prerequisites

You went through the [quick start](https://gohugo.io/getting-started/quick-start/) of the official Hugo documentation (the quick start part is very terse).

### Create a new site

```bash
hugo new site travel_blog
cd travel_blog/
```

You can call the site anything you want, we are not really making a travel blog. Just will look at the site structure.

### Installing & Using Themes

1. Get the theme custom made for this course.
   Go to https://github.com/giraffeacademy/ga-hugo-theme.
   Click on green button `code`, copy theme .git:
   `https://github.com/giraffeacademy/ga-hugo-theme.git`

**zip extracting you can do without git:**

- download the zip file, extract. By extracting means: double click on the zip, in the opened folder drag the main listed folder into the `themes` folder of your project.
- rename theme to `ga-hugo-theme`
- add theme to `hugo.toml`:

```toml
theme = 'ga-hugo-theme'
```

**using git**

- hugo docs pattern

```shell
git init
git submodule add https://github.com/giraffeacademy/ga-hugo-theme.git themes/ga-hugo-theme
echo "theme = 'ga-hugo-theme'" >> hugo.toml
hugo server
```

- giraffe pattern

```shell
cd themes
git clone https://github.com/giraffeacademy/ga-hugo-theme.git
```
