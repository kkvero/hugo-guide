---
title: "Deploy With GitHub Pages"
date: "2024-10-17T13:30:34+07:00"
draft: false
weight: 3
---

## Steps

Assuming you are done designing, structuring and filling in your project site with content. The following steps will guide you through getting your project ready for production and deploying on [GitHub Pages](https://pages.github.com/).

{{% steps %}}

### Add License, Readme

Adding some files at the root of your project customary for a repository.

- Add `LICENSE`, [MIT License example](https://github.com/imfing/hextra/blob/main/LICENSE)
- Add `README.md`

### Create a public repository

Go to your GitHub account and create a new **public** repository (without Pro account can publish to GitHub pages only from a public repo), e.g. on my side it is `https://github.com/kkvero/hugo-guide.git`
Then the base URL for the site will be according to the template naming:
`https://<USERNAME>.github.io/<REPO>/`
On my side it is:
`https://kkvero.github.io/hugo-guide/`

### Setting up gitHub Actions

After creating a repository GitHub gives you hints on how to make your first commit. Don't do it yet.
<br/>
Go to your main page >
your public repo will be visible >
click on it >
inside repo find "Settings" >
choose "Pages" on the left menu.
In the opened "GitHub Pages" in "Source" set to _"GitHub Actions"_.
No need to Save, it applies instantly.

### Modify baseURL

In your `hugo.yaml` modify baseURL, e.g.:

```yaml
baseURL: https://kkvero.github.io/hugo-guide/
```

### Modify go.mod

Change the first line from ` module github.com/username/my-site` to e.g.:

```mod
module github.com/kkvero/hugo-guide
```

### Create .gitignore

In project root. With contents:

```{filename=".gitignore"}
node_modules/
public/
resources/
.hugo_build.lock
.vscode/
```

### Create GitHub Actions workflow

Create these directories and file so that it has the path `.github/workflows/pages.yaml` in project root with the content that follows.
<br/>
**What info to customize:**

- hugo version. Get it in your local terminal with:

```bash
hugo version
```

E.g. 0.135.0

- go verison. It is in `go.mod` of your project.
  E.g. go 1.22.7
- If you are deploying to username pages (and not to GitHub Pages Project like we do here) `https://<USERNAME>.github.io/` then modify the `--baseURL`:

```yaml {filename=".github/workflows/pages.yaml"}
run: |
  hugo \
    --gc --minify \
    --baseURL "https://${{ github.repository_owner }}.github.io/"
```

{{% details title=".github/workflows/pages.yaml" closed="true" %}}

```yaml
# Sample workflow for building and deploying a Hugo site to GitHub Pages
name: Deploy Hugo site to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["main"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

# Default to bash
defaults:
  run:
    shell: bash

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.135.0
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0 # fetch all history for .GitInfo and .Lastmod
          submodules: recursive
      - name: Setup Go
        uses: actions/setup-go@v5
        with:
          go-version: "1.22.7"
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v4
      - name: Setup Hugo
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb
      - name: Build with Hugo
        env:
          # For maximum backward compatibility with Hugo modules
          HUGO_ENVIRONMENT: production
          HUGO_ENV: production
        run: |
          hugo \
            --gc --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

{{% /details %}}

### Initialize git

From project directory.

```bash
# Initialize
git init
git add -A
git commit -m "initial commit"
git branch -M main

# Add remote
git remote add origin git@github.com:kkvero/hugo-guide.git
git push -u origin main

# Subsequent
git log --pretty=oneline
git status
git add -A
git commit -m "initial commit"
git push -u origin main

```

### Workflow status

To view the status of your workflow of building the site, go to the repository of your site, choose "Actions".
Should show actions in progress.
NOTE: It does not appear instantaneously, click "All workflows" before starting another workflow manually.

### Continuous integration.

When you push changes to the project with "Subsequent" git commands, site gets rebuilt.

{{% /steps %}}
