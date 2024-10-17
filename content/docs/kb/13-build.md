---
title: "Build"
date: "2024-10-17T13:14:05+07:00"
draft: false
weight: 23
---

```shell
hugo
```

Builds the project, i.e. creates `public` folder.

- Delete the public folder before a re-build (otherwise the files you delete while developing will hang around in the public folder).
- Deploy only the public folder.

This is the simplest way to build a project. Then you "copy/paste" the "public" folder with static files that Hugo generated to your hosting provider of choice.

If you want a more sophisticated approach - continuous integration with git, see the next section [Deploy]({{< ref "/docs/deploy" >}}).
