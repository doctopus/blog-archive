
---
title: "Hugo Update Workflow"
date: 2021-05-17T20:50:05-04:00
draft: false
hero: "/images/hero-4.jpg"
excerpt: "Blog Update Workflow"
---

# Hugo Blog Update
Workflow of adding blog posts

1. Run `hugo new post/xpost.md`  or Add xpost.md to doctopus/content/post and modify headers (note that the structure differs from theme to theme) here xpost is the url part of the blog post.
2. In terminal go to within the hugo created blog: cd Documents/dev/work/blog/doctopus (doctopus is the blog created from `hugo new site doctopus`)

3. Create the static content in the public folder by running command `hugo -t hugo-theme-novela` while in the doctopus folder


4. run `hugo server -D` in terminal to see local update in the blog
5. Open http://localhost:1313/ in browser
6. Ctrl C to stop server. Once Everything is ready in local environment. While sever is running everything happens in real time as soon as you save files.


7. Cd inside newly updated public folder, push changes to public folder to its git at doctopus.github.io using `git add .` `git commit -m "message"` `git push origin master`

8. Optionally push contents of blog fodler by moving up to blog folder and pushing to the blog repo using `git add .` `git commit -m "message"` `git push origin main`



To differentiate the masters    
blog git has branch : main    
doctopus.github.io has branch : master  



Note that the hero images are taken from the folder public/images 
Do not directly change content in the public folder rather add content to the theme? folder to have them replicated in the public folder.


