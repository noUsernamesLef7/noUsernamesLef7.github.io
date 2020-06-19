---
layout: post
date: 2020-06-18
author: Jason Brown
title: Why Jekyll?
---
I figured a good way to start off my blog would be to write about why I chose to use Jekyll to build my site and publish blog posts. The biggest reason is that I'm using [GitHub Pages](https://pages.github.com) to host and it's *"powered by Jekyll."* Now you could ignore this fact and use GitHub Pages to host html written however you like, but after looking into Jekyll I decided to take the plunge.

### It's Easy to Use
I know myself well enough that if I want to have any hope of publishing regular blog posts, it will have to be as painless as possible. **Jekyll lets me write posts (and all pages for that matter) as plain old Markdown files which it takes and renders as HTML.** Markdown is familiar since I use some version of it for formatting Discord messages, Reddit posts, Trello cards, readme files, among other uses. Markdown is lightweight which means I can write quickly and include formatting without interrupting my stream of conciousness. You can control how the content is rendered on a page by defining layouts that include your basic HTML structure and then use [Liquid](https://github.com/Shopify/liquid/wiki) templating to control where content and variables go.

### It Isn't WordPress
There is no database behind this blog and the site is completely static. I like avoiding unnecessary complexity when I can and this kind of approach certainly achieves that. There are no dependencies that have to be maintained lest they become a CVE infested nightmare, no analytics, no fingerprinting, and taking up so little disk space, it loads super fast.

Instead, I author my posts in a designated location and then when Jekyll is run, it organizes them and renders them as HTML. The blog post index page is generated using a simple for loop in the Liquid template. **Jekyll grants me some of the pros of using a heavy CMS like WordPress but also allows me to still have a fast loading static site.**

### It Allows for Templating
As I mentioned, Jekyll uses the Liquid templating language. **This cuts way down on duplicate code reducing the size of my project and allowing me to *"simulate"* some of the features of a dynamic site.** Right now, I've got a default layout and a post layout that inherits most of it's structure from the default. In addition to layouts, you can also create "includes" for any snippets of code that are frequently reused throughout.

### Conclusion
Using GithHub Pages to host definitely nudged me towards using Jekyll but after having looked into it, I actually think **it's the right balance of content management, templating, and old school static for my use case.** I did check out a few other static site generators including [Hugo](https://gohugo.io) but the simplicity of Jekyll (and the fact that I don't know Go) stuck out to me. If you are looking to try your hand at blogging or want to host a small simple website I would recommend the GitHub Pages/Jekyll combo. Of course, I haven't been using it for very long so my opinion should be taken with a grain of salt and may change over time.
