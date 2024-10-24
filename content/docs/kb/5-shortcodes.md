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

- _Partials are used in layout template, shortcodes are used in content files._
- Two types of shortcodes we can create:

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
