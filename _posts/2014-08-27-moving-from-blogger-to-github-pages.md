---
title: Moving from Blogger to GitHub Pages
tags:
  - Blog
description: >
    Migrate your blog from Blogger to GitHub Pages to gain full control on your content.
---

This is a **meta post**. Yes, this post traits about its own creation, infact I am moving from Blogger to Github Pages.

I started looking these examples:

* [Bootstrap](http://getbootstrap.com/): [repo](hettps://github.com/twbs/bootstrap)
* [Perfection Kills](http://perfectionkills.com/): [repo](https://github.com/kangax/perfectionkills.com)
* [ESLint](http://eslint.org/): [repo](https://github.com/eslint/eslint.github.io)

See here more [sites using Jekyll](http://jekyllrb.com/docs/sites/).

## Pros

* Can edit locally using my favourite editor (vim, of course :^).
* Can edit online using GitHub editor.
* Easier web design: editing Blogger template is horrible! Now I can use Bootstrap 3.
* Can easily embed a GitHub Gist, see [Jekyll documentation about gists](http://jekyllrb.com/docs/templates/#gist).

## Cons

* Loose out of the box Google Ads integration: it is ok for me, cause I will remove ads.
* Loose comments feature: I will implement it with disqus or facebook. By the way I got three type of comments while my blog was on Blogger: spam, that I had to moderate; hints, that I would like to redirect to a collaboration via GitHub, maybe using the site's repo issues tracker; thanks, that I would like to redirect to donations.

## Steps

### Basic structure

```bash
├── _config.yml
├── index.html
├── _includes/
|   ├── _includes/footer.html
|   └── _includes/header.html
├── _layouts/
|   ├── _layouts/default.html
|   └── _layouts/post.html
└── _posts/
    └── _posts/2014-08-27-moving-from-blogger-to-github-pages.md
```

### Porting a post

I will focus on post [How to install DBD::Oracle](http://g14n.info/2013/07/how-to-install-dbdoracle), that is the most visited of my blog.

See [Jekyll docs about how to write a post](http://jekyllrb.com/docs/posts/).

To preserve blogger urls, edit _config.yml and add

```
permalink: ./:year/:month/:title.html
```

Note that filename should start with yyyy-mm-dd and post title should be lowercase and separated by dashes, file extension is *.md*, for instance, I will create a file

```
_posts/2013-07-02-how-to-install-dbdoracle.md
```

Don't forget to insert a [YAML frontmatter](http://jekyllrb.com/docs/frontmatter/)

```
---
layout: post
title: Moving from Blogger to GitHub Pages
tags:
  - Blog
---
```

## Extras

### Naked domain and SSL

I used [Cloudfare](https://www.cloudflare.com/) to get a naked domain and SSL: it was really easy and took no more than 30 minutes. Now my homepage is **https://g14n.info**.

### Comments

On blogger you have comments and moderation out of the box. To achieve the same feature in a modular way, I chose [Disqus](https://disqus.com/).

Basically I added an `{{ "{% include disqus.html " }}%}` to my *_layouts/posts.html* and created an *_include/disqus.html* with all the code required.

Read how to [embed Disqus code][2] as a reference.

A good tip is to add the *disqus_shortname* variable into the *_config.yml*

```
disqus:
  shortname: g14n
```

and to use [Jekyll variables][3] to set [Disqus Javascript configuration variables][4] like this

```js
var disqus_shortname  = '{{ site.disqus.shortname }}';
var disqus_identifier = '{{ page.id }}';
var disqus_title      = '{{ page.title }}';
var disqus_url        = '{{ site.url }}/{{ page.url }}';
```

## See also

* [Dependencies and versions used by GitHub Pages][1]

  [1]: https://pages.github.com/versions/ "Dependencies and versions used by GitHub Pages"
  [2]: https://help.disqus.com/customer/portal/articles/472097-universal-embed-code "Disqus Universal Embed Code"
  [3]: http://jekyllrb.com/docs/variables/ "Jekyll Variables"
  [4]: https://help.disqus.com/customer/portal/articles/472098-javascript-configuration-variables "Disqus JavaScript configuration variables"

