---
title: "Configure Theme"
date: "2024-10-14T11:31:34+07:00"
draft: false
cascade:
  type: docs
---

#### Create site

```shell
hugo new site hugo-guide --format=yaml
cd hugo-guide
```

#### Start using theme

We will be using [Hextra theme](https://themes.gohugo.io/themes/hextra/).
Configure Hextra theme via module.

- Initialize hugo module:

```shell
../hugo-guide$
hugo mod init github.com/username/my-site
```

- Add hextra theme

```shell
hugo mod get github.com/imfing/hextra
```

Then `go.mod` first line will be
`module github.com/username/my-site`
<br/>
**Will need to change that later to real repo** for production.

- Add to your `hugo.yaml`

```yaml
module:
  imports:
    - path: github.com/imfing/hextra
```

#### Preview site

- Create content pages for the home page and the documentation page:

```shell
hugo new content/_index.md
hugo new content/docs/_index.md
```

- Preview site

```shell
hugo server -D   # OR hugo server --buildDrafts --disableFastRender
```

#### Update theme

Subsequently from time to time you will need to run:

```shell
hugo mod get -u github.com/imfing/hextra
```
