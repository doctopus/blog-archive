
---
title: "Hugo Deployment"
date: 2021-04-17T20:55:05-04:00
draft: false
hero: "/images/hero-2.jpg"
excerpt: "Hugo Blog Deployment in Github Pages"
---

# Hugo Blog Deployment

#### Objective: Setup a blog
The following workflow backs up the blog mechanism in github while having the generated static content pointed to the github.io website  

blog (git linked to blog repository)  
blog/doctopus (the site name created by hugo)  
blog/doctopus/public (git linked to github page repository as a submodule)  
blog/doctopus/theme (git linked to theme page repository as a submodule)  

...blog/doctopus    
├── archetypes  
├── config.toml  
├── content  
├── data  
├── layouts  
├── public  
├── static  
└── themes (installed as a submodule)  


   

### Install Hugo
[https://gohugo.io/getting-started/quick-start/](https://gohugo.io/getting-started/quick-start/)

```brew install hugo```

In github create two repos blog and username.github.io   
Clone blog at your local computer

```go
cd blog  
hugo new site doctopus
```

Creates a doctopus folder inside blog/  
Doctopus folder will have the boilerplate folders
Since the blog folder is cloned git is already init in it.

Install the theme of choice as a submodule in the themes folder

`git submodule add https://github.com/xxx/hugo-theme.git themes/hugo-theme`

Notice that this folder was added as a submodule so it can not be deleted. If it needs to be removed it needs to be removed using following process.    

### Removing Submodule in a Main Git Module
If a submodule is wrongly added. Just deleting it will not remove it, instead do the following

```go
git submodule deinit <path_to_submodule>

git rm <path_to_submodule>

git commit-m "Removed submodule "

rm -rf .git/modules/<path_to_submodule>`
```

### Preparing the config
Edit config.toml file to edit baseURL as “https://username.github.io/“  
Add the theme=“hugo-theme-name”

Start the server by `hugo server`  
It shows an empty site with the given theme at http://localhost:1313/

### Create Post
To create a post. Refer to the example site folder inside the theme for the structure. Some themes nest all the blog posts in content/posts and others in content/post

So depending on what the theme follows create a post inside the doctopus/content

`hugo new post/hello.md`

At the top of the created post file there would be format for defining things, such as hero image etc. Again the formatting differs from theme to theme so refer to example site post header codes. So far what has been done lets the blog/doctopus/ folder act as the static site generator that will put its resources in the blog/doctopus/public folder which we will point to the GitHub hosted page.

### Setting public folder as github.io page
To add GitHub.io page website as a submodule it needs to have been committed at least once. To have one commit to the username.github.io repo, first clone it somewhere temporary and create a README.md in it and then commit and push. This repo is now ready to be pulled as a submodule.

While pushing for the first time we can define its master branch.

`git push origin master`

To differentiate the master branches for convenience,    
blog git has branch : main    
doctopus.github.io has branch : master    

To create a submodule within the blog in a folder named public: that is blog/doctopus/public

`git submodule add -b master https://github.com/doctopus/doctopus.github.io.git public`

Note here the master refers to the master branch of the github.io repo. This now creates a new folder in blog/doctopus/public

Again this page being a submodule, it can not be removed by just deleting. Follow the above method to remove a submodule if accidentally created.

The static files generated for the website will be added here automatically and that can be pushed to github for publication in the website.

At this point there will be only the readme.md file that we created while pushing the first commit. Now to fill this folder with the generated static site.

`hugo sever` command serves content created in the content folder to the local host along with the activated theme. However notice that this is getting served from the doctopus folder directly and not from the public folder. To be able to put all the processed static files in the public folder, run the code:  

```go
hugo -t hugo-theme
```

This will put all the generated content in the public folder. If you do a git remote -v in the public folder it can be seen how the public folder points to the github.io repo.

Once we commit and push the contents to the github.io repo it will be live on the username.github.io page.

Every time the `hugo -t hugo-theme` command is run it successively adds static files to the public folder without removing anything. So you may need to manually remove the things that gets added wrongly.

### Adding Static Content
To add static content add content in the doctopus folders without directly adding anything directly in the public folder. Everytime the static site is generated, it pulls the respective content and puts in their place in the subfolders of the public folder.

Every time new content is added, run the `hugo -t hugo-theme` code to generate static content and push the changes to the public folder to username.github.io repository

### Blog sync logic
Pushing changes of the blog as a whole may be ok to keep a back up of the file system of the hugo generated content but to make the site online only the public folder needs to be prepared and pushed. So only pushing the public folder after running the  `hugo -t hugo-theme` command should make the github.io website live.


