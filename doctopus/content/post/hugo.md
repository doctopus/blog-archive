
---
title: "Hugo Deployment"
date: 2021-04-17T20:55:05-04:00
draft: false
hero: "/images/hero-2.jpg"
excerpt: "Hugo Blog Deployment in Github Pages"
---

# Hugo Blog Deployment

blog(git linked to blog repository)

——doctopus (any site name; created by hugo)

\-boilerplate folders    
      -themes    
         —hugo-theme (installed as a submodule)    
      -config.toml    

\-public (git linked to github page repository as a submodule)    

*Install Hugo* [https://gohugo.io/getting-started/quick-start/](https://gohugo.io/getting-started/quick-start/)

`brew install hugo`

In github create repos blog and username.github.io

Clone blog at your local computer

hugo new site doctopus

Creates a doctopus folder in blog/

Since the blog folder is cloned git is already init in it.

Install the theme of choice as a submodule in the themes folder

`git submodule add https://github.com/xxx/hugo-theme.git themes/hugo-theme`

Notice that this folder was added as a submodule so if it needs to be removed it needs to be removed using following process.    


*Removing Submodule in a Main Git Module*
If a submodule is wrongly added. Just deleting it will not help. Instead do the following

`git submodule deinit <path_to_submodule>

git rm <path_to_submodule>

git commit-m "Removed submodule "

rm -rf .git/modules/<path_to_submodule>`


Edit config.toml file to edit baseURL as “https://username.github.io/“

And add the theme=“hugo-theme-name”

start the server by hugo server

It shows an empty site with the given theme

To create a post. Refer to the example site folder inside the theme for the structure. Some themes nest all the blog posts in content/posts and others in content/post

So depending on what the theme follows create a post inside the doctopus/content

`hugo new post/hello.md`

At the top of the post file, there would be format for defining things, such as hero image etc. Again the formatting differs from theme to theme so refer to example site post header codes.

So far what has been done in the blog/doctopus   folder will serve as the static site generator that will put its resources in the public folder which we will point to the GitHub hosted page.

To add GitHub page website as a submodule it needs to have been committed at least once. To have one commit to the username.github.io repo, first clone it somewhere temporary and create a README.md in it and then commit and push. This repo is now ready to be pulled as a submodule.

While pushing for the first time we can define its master branch.

`git push origin master`

To differentiate the masters    
blog git has branch : main    
doctopus.github.io has branch : master    

To create a submodule within the blog in a folder named public: that is blog/doctopus/public

`git submodule add -b master https://github.com/doctopus/doctopus.github.io.git public`

Note here the master refers to the master branch of the github.io repo. This now creates a new folder in blog/doctopus/public

Again this page being a submodule, it can not be removed by just deleting. Follow the above method to remove a submodule if accidentally created.

The static files generated for the website will be added here automatically and that can be pushed to github for publication in the website.

At this point there will be only the readme.md file that we created while pushing the first commit. Now to fill this folder with the generated static site.

If we activate the surver by command hugo sever then the post created in the content folder should be visible along with the activated theme. However this is getting served from the doctopus folder directly. To be able to put all the processed files in one folder.

To generate the static content run the code.

`hugo -t hugo-theme`

This will put all the generated content in the public folder. If you do a git remote -v in the public folder it can be seen how the public folder points to the github.io repo.

Once we commit and push the contents to the github.io repo it will be live on the username.github.io page.

Every time the Hugo -t Hugo-theme command is run it successively adds static files to the public folder without removing anything. So you may need to remove the things that gets added wrongly.

To add static content add content in the doctopus folders without directly adding anything directly in the public folder. Everytime the static site is generated, it pulls the respective content and puts in their place in the subfolders of the public folder.

Every time new content is added, run the `hugo -t hugo-theme` code to generate static content and push the changes to the public folder to username.github.io repository
Pushing changes of the blog as a whole may be ok to keep a back up but to make the site online only the public folder needs to be prepared and pushed.


