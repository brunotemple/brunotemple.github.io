---
layout: post
title: Jekyll-Git-GitHub a little sample.
categories: [samples]
tags: [github git jekyll]
---

### How to create your website/blog and host on GitHub.

1 – On GitHub create a new repository called: username.github.io (must user the username)
    Ex: brunotemple.github.io
    
2 – Copy the URL of this repository, usually; it is: https://github.com/username/repositoryname.git
    Ex: https://github.com/brunotemple/brunotemple.github.io.git

3 – Open the Git Bash (previous post), navigate to the folder that you want to create your repository, and execute the command:

    git init *repositoryname

Ex: git init myblog (a new folder will be created)

4 – Navigate to this folder and execute the command:

    git remote add origin *URL of Github

Ex: git remote add origin https://github.com/brunotemple/brunotemple.github.io.git

5 – Create your blog using the Jekyll (previous post)

    Jekyll new myblog

6 – Navigate to this folder to commit and push the changes to GitHub using the command:
    
    git commit –m”First Commit”
    git push -u origin master
    
7 – Open you browser, now you can see your blog on the web: http://username.github.io
    Ex: https://brunotemple.github.io
    
8 - Updating the blog directly on GitHub, it is possible, try it.
In the main folder of your blog, create a file called README.txt, if you have already created while you were creating your repository, just make some changes in the file, including “Hello World” for example. Commit this change.

9 – Get the update on the local machine.
In the “Git Bash” navigate to the folder of the project and execute the command:

    git pull origin master
    
Check the file README.txt.

10 – Updating by the local machine.
Open the README.txt and include the text “testing of version”, close and save.
In the “Git Bash” execute the command:

    git commit –a –m”README changes”
    git push -u origin
    
It is done, you can see the new version on GitHub.

