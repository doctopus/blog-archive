---
title: "Hello"
date: 2021-04-17T18:55:05-04:00
draft: false
header:
  image: "/images/hero-1.jpg"
  caption: "Yay! It works!"
---
![alt text](https://i.imgur.com/0xnhLwg.jpg)
TRying to add a picture

Install from the command line
The images are already in images folder


If you don’t want to use the starter, you can start from scratch and just install this theme from the command line.

Create a new Hugo site and initialize your project as a Hugo module:

hugo new site my-awesome-blog
cd my-awesome-blog
hugo mod init

Edit your config.toml to add the theme settings:

# Novela settings
theme = "github.com/forestryio/hugo-theme-novela"

paginate = 6

[social]
twitter= "https://twitter.com/forestryio"
github= "https://github.com/forestryio/novela-hugo-starter"
linkedin= "https://www.linkedin.com/company/forestry.io"
instagram = "#"
dribbble = "#"
youtube = "#"

[taxonomies]
author = "authors"

Create your first draft post and preview it locally:

hugo new post/my-first-post.md
hugo server -D

You’re good to go!
Customization
Logo

Override /themes/novela/layouts/partials/icons/ui/logo.html with your own file at /layouts/partials/icons/ui/logo.html; include your logo in SVG format for desktop and mobile formats.

Novela supports light and dark mode. To have your logo respond in kind, add class="change-fill" to the svg path(s).

In order for the Socials to be surfaced in Forestry, you should copy the theme’s config/_default/social.yaml to your project.
Authors

You should register authors as a taxonomy in your project’s `config.yaml``

taxonomies:
  author: authors
