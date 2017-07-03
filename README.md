# git-guide

## Table of Contents
  1. [Setup](#1-setup)  
    1.1. [Installation](#11-installation)  
    1.2. [Configurations](#12-configurations)
  2. [Repository](#2-repository)   
    2.1. [Create Git Repository](#21-create-git-repository)  
    2.2. [Create Remote Repository](#22-create-remote-repository)  
    2.3. [Add Remote Repository](#23-add-remote-repository)  
    2.4. [Clone Existing Repository](#24-clone-existing-repository)
  3. [Commands](#3-commands)     
    3.1. [git status](#31-git-status)  
    3.2. [git add](#32-git-add)  
    3.3. [git diff](#33-git-diff)  
    3.4. [git commit](#34-git-commit)  
    3.5. [git log](#35-git-log)  
  4. [Branching](#3-branching)  
    4.1. [Create Branch](#41-create-branch)  
    4.2. [Branch switching](#42-branch-switching)

    

# 1. Setup

This section will be a quick setup guide for installing and using Git and GitHub and how to perform its various functions
of creating a user and a repository locally, connecting this repo to the remote host that contains your project to GitHub.

## 1.1. Installation

Install git on an Ubuntu for this you can use the apt package management tools to update your local package index.
Afterwards, you can download and install the program:

```
    $ sudo apt-get update
    $ sudo apt-get install git

```

This will download and install git to your system. You will still have to complete the configuration steps that we cover
in the next section.

## 1.2. Configurations

Now that you have git installed, you need to do a few things so that the commit messages that will be generated for you 
will contain your correct information.

The easiest way of doing this is through the git config command. Specifically, we need to provide our name and email 
address because git embeds this information into each commit we do. We can go ahead and add this information by typing:

```
    $ git config --global user.name "Your Name"
    $ git config --global user.email "youremail@domain.com"
    
```

You can see all of the configuration items from:


```
    $ git config --list
    
```

# 2. Repository

The purpose of Git is to manage a project, or a set of files, as they change over time. Git stores this information in a
data structure called a repository.

A git repository contains, among other things, the following:

    
* A set of commit objects.
* A set of references to commit objects, called heads.
    
    
The Git repository is stored in the same directory as the project itself, in a subdirectory called .git. Note differences
from central-repository systems like CVS or Subversion:
    
* There is only one .git directory, in the root directory of the project.
* The repository is stored in files alongside the project. There is no central server repository.


## 2.1. Create Git Repository
     
Goto in your project's directory or create, make sure it is not an empty directory.After that run the following command:
    
```
    $ git init   

```
This will create a .git directory in your project directory.
        

## 2.2. Create Remote Repository

We will create a repository on github for this you have to create an account on [github](#https://github.com/).

To put your project up on GitHub, you'll need to create a repository for it to live in. 
You can follow this [github article](#https://help.github.com/articles/create-a-repo/).

```
$ git remote add origin git@github.com:username/new_repo

```

# 2.4. Clone Existing Repository

git clone is primarily used to point to an existing repo and make a clone or copy of that repo at in a new directory, at
 another location. The git clone command copies an existing Git repository.
 
```
$ git clone my-project-url.git

$ cd my-project

``` 
Cloning automatically creates a remote connection called "origin" pointing back to the original repository. 

# 3. Commands

Let's start with basic commands that are used commonly.

## 3.1. git status

```
$ git status
```
git status shows which files have changed between the current project state and HEAD. Files are put in one of three 
categories: new files that haven’t been added (with git add), modified files that haven’t been added, and files that
have been added.

## 3.2. git add
```
$ git add "filename"
```
This command add the specified filename to git.

```
$ git add .
```
If you want to add all the files in your local repository 


![GitHub Logo](staging_area.png)

## 3.3. git diff

```
$ git diff
```
git diff shows the diff between HEAD and the current project state.

```
$ git diff --cached
```
With the --cached option it compares added files against HEAD; otherwise it compares files not yet added.*

```
$ git diff "filename"
```

To see the difference of a particular file between current HEAD and the current file state.


## 3.4. git commit 

``` 
$ git commit -m "Your message"
```
git commit to create the commit object.The new commit object will have the current HEAD as its parent.

-m option is used to give commit message.

```
$ git commit -a
```
This will automatically add all modified files but leave new files.


## 3.5. git log

```
$ git log
```

git log shows a log of all commits starting from HEAD back to the initial commit.


# 4. Branching

When you want to add a new feature or fix a bug—no matter how big or how small—you should work on a new branch to 
encapsulate your changes. This makes sure that unstable code is never committed to the main code base, and it gives you 
the chance to clean up your feature’s history before merging it into the main branch. 

## 4.1. Create Branch

```
$ git branch <branch>

```

Above command will create a new branch called <branch>. This does not check out the new branch.

Now, suppose git repository has structure like this:

```
(A) -- (B) -- (C)
               |
             master
               |
              HEAD


```

where (B) was the version you sent to the conference and (C) is your new revision state. (I’m dropping the arrowheads 
because they always point to the left.)

To jump back to commit (B) and start new work from there, you first need to know how to reference the commit. You could 
either use git log to get the SHA1 name of (B), or you could use HEAD^ to retrieve it (as you will remember from the 
previous page, HEAD^ means the parent of the HEAD commit).

```
$ git branch [new-head-name] [reference-to-(B)]

```
This command will create a new head with the given name, and point that head at the requested commit object. If the 
commit object is left out, it will point to HEAD. 

After that repository commit tree looks like this: 

```
(A) -- (B) ------- (C)
        |           |
   fix-headers    master
                    |
                   HEAD
                   
```

## 4.2. Branch switching

```
 $ git checkout existing_branch_name
```

The git checkout command lets you navigate between the branches created by git branch. Checking out a branch updates the
files in the working directory to match the version stored in that branch, and it tells Git to record all new commits on
that branch. Think of it as a way to select which line of development you’re working on.
In order to start working on the headers, you need to set the fix-headers head to be the current head.

Above command does the following:
* Points HEAD to the commit object specified by [head-name]
* Rewrites all the files in the directory to match the files stored in the new HEAD commit.

```
         +-------------- (D)
        /                 |
(A) -- (B) -- (C)         |
               |          |
             master  fix-headers
                          |
                         HEAD

```

You can see now why it’s called “branching”: the commit tree has grown a new branch. Note that the angle of the line
connecting (B) and (D) is irrelevant; pointers do not store whether they are horizontal or slanted.

if there are any uncommitted changes when you run git checkout, Git will behave very strangely. The strangeness is
predictable and sometimes useful, but it is best to avoid it. All you need to do, of course, is commit all the new
changes before checking out the new head.

```
 $ git checkout  -b new_branch_name
```

-b option allows to create and switch to a new branch.


