---
title: 博客模板指南
published: 2025-12-25
description: "如何使用这个博客模板?"
cover: "./cover.webp"
pinned: true
tags: []
category: Guides
draft: false
---


提示：对于本指南中未提及的内容，你可以在[天文文档]中找到答案。(https://docs.astro.build/).


## 帖子前言

```yaml
---
title: 我的第一篇博客文章
published: 2025-12-25
description: 这是我Astro博客的第一篇文章。
cover: ./cover.webp
tags: [Foo, Bar]
category: Front-end
draft: false
---
```


| 属性 | 描述                                                                                                          |
|---------------|-------------------------------------------------------------------------------------------------------------|
| `title`       | 帖子标题。                                                                                                       |
| `published`   | 帖子发布的日期。                                                                                                    |
| `pinned`      | 这篇帖子是否置顶在帖子列表顶部。                                                                                            |
| `description` | 简要介绍一下帖子。显示在索引页。                                                                                            |
| `cover`       | 帖子的封面图片路径。 <br/>1. 以 `http://` or `https://`开头: 网页图像 <br/>2.以 `/`开头: `public` 文件夹图片 <br/>3. 不使用任何前缀：相对于标记文件 |
| `tags`        | 帖子标签。                                                                                                       |
| `category`    | 帖子分类。                                                                                                       |
| `licenseName` | 帖子内容的授权名称。                                                                                                  |
| `author`      | 帖子作者。                                                                                                       |
| `sourceLink`  | 帖子内容的来源链接或参考资料。                                                                                             |
| `draft`       | 如果这篇帖子还是草稿，那就不会显示出来。                                                                                        |


## Post 文件的放置位置

你的帖子文件应该放在`src/content/posts/`， 你还可以创建子目录，更好地组织帖子和资源。

```
src/content/posts/
├── post-1.md
└── post-2/
    ├── cover.png
    └── index.md
```