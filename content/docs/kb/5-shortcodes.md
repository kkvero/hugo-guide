---
title: "Shortcodes"
date: "2024-10-16T15:56:09+07:00"
draft: false
weight: 15
---

## Builtin

[Hugo builtin shortcodes](https://gohugo.io/content-management/shortcodes/#using-shortcodes)

- **Youtube shortcode**

```html
{{</* youtube 0RKpf3rK57I */>}}
```

Where 0RKpf3rK57I is the video id part in the full link `https://www.youtube.com/watch?v=0RKpf3rK57I`

- **Other shortcodes**
  <br/>
  `relref` - returns the permalink of a page on your site:

  ```markdown
  [Post 1]({{%/* relref "/posts/post-1#foo" */%}})
  ```

  ->rendered

  ```html
  <a href="/posts/post-1/#foo">Post 1</a>
  ```

  `ref` - the same but absolute
  <br/>
  `figure` - for images ([figure](https://gohugo.io/content-management/shortcodes/#figure))

## Custom

{{< callout >}}
Consider reading about making custom shortcodes after reading the Partials section.
{{< /callout >}}

Shortcodes = Shortcode templates

{{< callout >}}
**Partials are used in layout templates, shortcodes are used in content files.**
{{< /callout >}}

Two _types of shortcodes_ we can create:

1. a single tag shortcode and a
2. start/end tag shortcode.
   {{< callout >}}
   **Shortcode name is the filename.**
   {{< /callout >}}

#### Shortcode, example 1.

- Create shortcode: `layouts/shortcodes/myshortcode.html` (creating `shortcodes` folder in `layouts`)

```html
This is the shortcode text.
```

Make sure you have `{{.Content}}` in `layouts/_default/single.html`

- Use shortcode in `content/a.md`

```markdown
+++
title = 'A'
date = 2024-10-10T20:37:08+07:00
draft = true
+++

This is a.md
{{</* myshortcode */>}}
```

- Go to `http://localhost:1313/a/`, it should display:

```
This is a.md This is the shortcode text.
```

#### Passing in variables to a shortcode

```markdown {filename="content/a.md"}
{{</* myshortcode color="blue" */>}}
```

```html {filename="layouts/shortcodes/myshortcode.html"}
<p style="color:{{ .Get `color` }}">This is the shortcode text.</p>
```

{{< callout >}}
In CSS use backticks for "".
<br/>
If not used in CSS it would use "" `{{ .Get "color" }}`.
{{< /callout >}}

#### Passing in positional parameters.

```markdown {filename="content/a.md"}
{{</* myshortcode orange */>}}
```

```html {filename="layouts/shortcodes/myshortcode.html"}
<p style="color:{{ .Get 0 }}">This is the shortcode text.</p>
```

#### Shortcode to surround an image with a border.

The .md file would pass in the `img-src` and `caption`.
The `layouts/shortcodes/myshortcode.html` would look like:

```html
<div style="border: 1px solid black">
  <img src="{{ .Get `image-src`}}" />
</div>
<p>{{ .Get “caption” }}</p>
```

#### Shortcodes with closing tags.

```markdown {filename="content/a.md"}
This is a.md
{{</* myshortcode */>}}
Text inside the opening and closing tags.
{{</* / myshortcode */>}}
```

```html {filename="layouts/shortcodes/myshortcode.html"}
<p style="background-color:yellow">{{.Inner}}</p>
```

#### Practical example: lorem

Problem: your website is still in development, but you want to
populate your web pages with text to test it out.
<br/>
Solution: create a shortcode that will generate some Lorem Ipsum text.

In `layouts` create directory `shortcodes`, create a file with the name of your shortcode.

```go-html-template {filename="layouts/shortcodes/lorem.html"}
{{- $count := .Get "count" | default (.Get 0) | default 1 -}}
{{- $loremipsum :=
  slice "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
  tempor incididunt ut labore et dolore magna aliqua." "Ut enim ad minim veniam,
  quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
  consequat." "Duis aute irure dolor in reprehenderit in voluptate velit esse
  cillum dolore eu fugiat nulla pariatur." "Excepteur sint occaecat cupidatat non
  proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
-}}
{{- range seq $count }}
  <p class="loremipsum">
    {{- range $index := seq 1 (index (shuffle (seq 0 3) ) 0 ) -}}
      {{ index
        $loremipsum $index
      }}&nbsp;
    {{- end -}}
  </p>
  {{- $loremipsum = shuffle $loremipsum -}}
{{- end -}}
```

<small>Attribution: the code for the shortcode was suggested on Hugo discourse forum,
[link to the post](https://discourse.gohugo.io/t/lorem-ipsum-shortcode-for-hugo/15604/5?u=kkvero).</small>

Use the shortcode in a markdown file (this will generate 20 paragraphs of Lorem Ipsum text):

```html {filename="content/posts/post1.md"}
{{</* lorem count="20" */>}}
```
