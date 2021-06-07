# How to build a hugo site

Install hugo
- https://gohugo.io/getting-started/installing/

Generate site basics dir: https://gohugo.io/getting-started/directory-structure/

```
hugo new site [--force]
```

Set up `archetypes/default.md`

```
---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
category: ""
tags : []
draft: true
---
```

Set up config

Add page

```
$ hugo new about/index.md
/Users/quynhanhpham/github.com/pqa-site/content/about/index.md created
```




