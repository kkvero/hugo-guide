---
title: "Troubleshooting"
date: "2024-10-15T15:04:36+07:00"
draft: false
weight: 3
---

While following along the notes in the previous sections some questions arise. Let's clear some of them.

## Various Issues

### How to start using raw html in markdown files.

#### How to insert a new line in markdown.

(Solving #1 using as an example to solve #2.) </br>
_Goal_ : In markdown the way to insert line breaks (without that horrible sea of white space around) but just want to start from a new line, is to use double space.
<br/>
_Problem_ : The text editor or its plugins might strip the double space to one space, leaving you without a line break.
<br/>
_Solution_ : Use html `<br/>`.
By default Hugo will not allow to use raw html in markdown. To enable, add to `hugo.yaml` (standard practice if you are the only author of your content):

```yaml {filename="hugo.yaml"}
markup:
  goldmark:
    renderer:
      unsafe: true
```

### Getting a specific version of Hugo

1. E.g.getting Hugo v0.121.2 <br/>
   Download this Hugo version binary from [Github releases repository](https://github.com/gohugoio/hugo/releases)
   Downloaded this one e.g.:
   [hugo_extended_0.121.2_Linux-64bit.tar.gz](https://github.com/gohugoio/hugo/releases/download/v0.121.2/hugo_extended_0.121.2_Linux-64bit.tar.gz)

{{< callout type="info">}}
_How to detect your OS architecture._ <br/>
Download files have options for 64bit, amd64, arm64.
To detect yours use `dpkg --print-architecture` in terminal.
{{< /callout >}}

2. Unzip (just double click on it). <br/>
   Unzips into a folder e.g. `~/Downloads/hugo_extended_0.121.2_Linux-64bit`. <br/>
   `cd` into the containing folder. <br/>
   In there there will be three files: license, readme and the executable hugo binary.
3. Rename that binary from `hugo` to name+whatever version you chose to download, e.g. `hugo1212`
4. Move or copy the renamed executable to `/usr/local/bin`. (Check if `/usr/local/bin` is in your path by running `echo $PATH`, but it most likely is.)
   Copying:

```shell
~/Downloads/hugo_extended_0.121.2_Linux-64bit$
sudo cp -i hugo1212 /usr/local/bin/hugo1212
```

(By using `-i` for interactive you will be asked if you would like to replace the file.)

5. That's it, set up your Hugo project as usual and use instead of `hugo server` -> `hugo1212 server` (all other hugo commands likewise).

{{< callout type="info">}}
_Why it works._ <br/>
Hugo binaries do not need to be installed and can be run directly from the bin folder. [source](https://stackoverflow.com/questions/59969577/installing-two-different-versions-of-hugo-ubuntu)
{{< /callout >}}

### To submodule or not to submodule.

**To submodule** <br/>
Using a theme as a submodule is recommended by theme developers in their docs. And it is a good way to go. And that's what was used in the deploy section of this "Hugo Guide". <br/>
But submodules are great if:

- The theme author relentlessly looks after his/her project, i.e. the theme. That is keeps up to date with every new release of Hugo.

**Not to submodule** <br/>
These are open source commercial-free projects and it is often that the theme project authors stop updating their themes to stay inline with Hugo updates. <br/>
Then consider:

- not to submodule a theme
- use a specific version of hugo for this theme

This can be a _fallback_ option. If a theme stops being supported, it is good to know that it will not break your project. Just revert to a specific hugo version when the project worked. (Alternatively you could modify the theme yourself.)

**How submoduling effects deployment with GitHub Actions** <br/>
In no way. <br/>
You specify to use a submodule in `hugo.yaml`. <br/>
`.github/workflows/hugo.yaml` does not care if you use submodules. Submodules will be downloaded when the workflow runs the `hugo` command which builds the `/public` dir of site. And that command either downloads submodules specified in `hugo.yaml` or uses `themes` folder.

### U+003E error

If getting this error `unrecognized character in shortcode action: U+003E '>'` but you did close all the `}}`. Make sure you have in `hugo.yaml`:

```yaml
enableInlineShortcodes: true
```

### Hugo shortcodes execute even if they are inside code blocks.

Use this notation (wrap in `/* */`) to prevent a shortcode from executing (when want to just document):

```
{{</*/* foo */*/>}}
{{%/*/* bar */*/%}}
```

Will render without `/* */`:

```
{{</* foo */>}}
{{%/* bar */%}}
```

- Shortcodes with opening and closing tags too:

```
{{</*/* callout */*/>}}
Some text.
{{</*/* /callout */*/>}}
```

- Note, escaping shortcodes will not work inside another shortcode. E.g. inside hugo theme hextra _callout_ shortcode. Hugo will throw an error.

### Link to a page on the current site

Use Hugo built-in shortcodes (in markdown): <br/>
`[Deploy]({{</* ref "/docs/deploy" */>}})` <br/>
In comparison, to link to an outside page in markdown: <br/>
`[Deploy](https://example.com).`

### CSS

The theme might be perfect but as you start customizing it, things may start to look not so perfect.
<br/>
To fix how your changes look on a webpage, create inside dir `asstet`, dir `css`, file `custom.css` (name of the file might be specific to your chosen theme). And place all your desired CSS fixes there.

#### Fix sticking elements

When creating several badges on the landing page (the home page), they appear to stick together. (In development they show up ok, stick in production.)
<br/>
Add this to `assets/css/custom.css`:

```CSS {filename="assets/css/custom.css"}
#badge_container::after {
  overflow: hidden;
  width: auto;
  display: inline;
  clear: both;
  content: "";
  display: table;
}

.badge_elem {
  float: left;
  margin-right: 0.5em;
}
```

<small>`::after` is to clear the float used in `.badge_elem` (otherwise the badges will float over the text that follows, on narrow screens).</small>

Use the defined CSS in `content/_index.md`:

```md
<div id="badge_container">
    <div class="badge_elem">
    {{</* hextra/hero-badge */>}}
    <!--badge 1 content-->
    {{</* /hextra/hero-badge */>}}
    </div>

    <div class="badge_elem">
    {{</* hextra/hero-badge */>}}
    <!--badge 2 content -->
    {{</* /hextra/hero-badge */>}}
    </div>

</div>
```
