---
title: "Shortcodes"
date: "2024-10-16T15:56:09+07:00"
draft: false
weight: 15
---

#### Builtin

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
