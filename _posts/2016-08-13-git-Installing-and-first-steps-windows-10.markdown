---
layout: post
title: git - Installing and first steps (Windows 10)
categories: git
tags: [git]
date: 2016-08-13
---

### What is GIT?

To summarize, GIT is a distributed version control system (VCS).

### What does GIT do?

A version control system is an application which controls the changes that you make to your files. It can be used for different purposes, even if you want to version your “Word” files, you can do it. However, it is more familiar to developers who want to control their code files and development.

### How to install GIT on Windows 10?

How to install GIT on Windows: Download the appropriate version, [link to download] [git download].

    Execute the “.exe” file.

Choose the option: "Use Git from the Windows Command Prompt" 


### How to use GIT:

1 - Open the “Git Bash”. Using the command line: Navigate to the folder that you want to create a new project. Ex: c:\documents\projects. Execute the command:

    git init newblog
  
    *(Where newblog is the name of the project)

GIT will create a new empty folder named “newblog” and that will be your new repository.
Navigate to the “newblog” folder; See that git shows the folder that you're currently in, and at the end of the line it shows “(master)”;  Master is the branch which controls the changes in the files.

2 -  To add files to be versioned. (Do the test below to see what happens). Navigate to the “newblog” folder and create two new files: document01.txt and document02.txt, come back to the git command line and execute the commands:

    git add document01.txt

    git add document02.txt

    OR

    git add .

    *(to add all the files inside the folder to the repository)

3 – Commit these changes:

    git commit –m”first commit”

4 – To create a new branch execute the command:

    git checkout -b test01

    *(Where test01 is the name of the new branch)

5 – See the git display showing “(test01)

Navigate to the “newblog” folder and delete one of the files and execute the command:

    git status

See that GIT shows you the change you've just made.

6 -  Commit this change:

  git commit –a –m”file deleted”

7 – Navigate to the “newblog” folder, keep your eyes in this folder and execute the command in the git bash:

  git checkout master

    *see what happen

    git checkout test01

    *see what happen

So, this test shows you how to create a new branch, and it is useful to version your changes, you can work in a parallel branches, and keep the master branch running.

8 – When you finish your changes in the parallel branch, you can merge the changes to the master branch:

    git checkout master
    git merge test01

[git download]: https://git-scm.com/downloads
