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
  4. [Branching](#4-branching)  
    4.1. [Create branch](#41-create-branch)  
    4.2. [Branch switching](#42-branch-switching)  
    4.3. [Listing branches](#43-listing-branches)  
    4.4. [Renaming branch ](#44-renaming-branch)  
    4.5. [Destroy branch](#45-destroy_branch)
  5. [Merging](#5-merging)  
    5.1. [Fast forward merge](#51-fast-forward-merge)  
    5.2. [3-way merge](#52-3-way-merge)  
    5.3. [Resolving Conflicts](#53-resolving-conflicts)

    

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


![Staging](staging_area.png)

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

git checkout works hand-in-hand with git branch. When you want to start a new feature, you create a branch with git
branch,then check it out with git checkout. You can work on multiple features in a single repository by switching
between them with git checkout.


<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 1100">
<style>
.st0{display:none;}
.st1{display:inline;}
.st2{fill:#FFFFFF;}
.st3{fill:none;stroke:#9882CE;stroke-width:4;stroke-miterlimit:10;}
.st4{fill:none;stroke:#404040;stroke-width:4;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;}
.st5{fill:#B3E3FF;stroke:#404040;stroke-width:4;stroke-miterlimit:10;}
.st6{fill:#FFFFFF;stroke:#59AFE1;stroke-width:4;stroke-miterlimit:10;}
.st7{fill:#FFFFFF;stroke:#404040;stroke-width:4;stroke-miterlimit:10;}
.st8{fill:#B18BE8;stroke:#404040;stroke-width:4;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;}
 .st9{fill:#404040;} .st10{fill:#CCCCCC;stroke:#404040;stroke-width:4;stroke-miterlimit:10;}
 .st11{fill:#FFFFFF;stroke:#404040;stroke-width:4;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;}
 .st12{fill:#999999;} .st13{fill:#B3E3FF;stroke:#404040;stroke-width:4;stroke-linejoin:round;stroke-miterlimit:10;}
  .st14{fill:#59AFE1;stroke:#404040;stroke-width:4;stroke-linejoin:round;stroke-miterlimit:10;}
  .st15{fill:none;stroke:#CCCCCC;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;}
  .st16{fill:none;stroke:#404040;stroke-width:4;stroke-miterlimit:10;}
  .st17{fill:#B18BE8;stroke:#404040;stroke-width:4;stroke-miterlimit:10;}
  .st18{fill:#FFFFFF;stroke:#6693ED;stroke-width:4;stroke-miterlimit:10;}
  .st19{fill:#4ED1A1;stroke:#404040;stroke-width:4;stroke-miterlimit:10;}
   .st20{fill:none;stroke:#4D4D4D;stroke-width:4;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;}
    .st21{fill:none;stroke:#59AFE1;stroke-width:4;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;}
     .st22{fill:none;stroke:#59AFE1;stroke-width:4;stroke-miterlimit:10;}
      .st23{fill:none;stroke:#CCCCCC;stroke-width:4;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;}
       .st24{fill:#FFFFFF;stroke:#CCCCCC;stroke-width:4;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;}
       .st25{fill:#FFFFFF;stroke:#404040;stroke-width:4;stroke-linejoin:round;stroke-miterlimit:10;} .st26{fill:#CCCCCC;}
       .st27{fill:#4ED1A1;stroke:#404040;stroke-width:4;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;}
        .st28{fill:#4CD3D6;stroke:#404040;stroke-width:4;stroke-linejoin:round;stroke-miterlimit:10;}
         .st29{fill:#B3E3FF;stroke:#404040;stroke-width:4;stroke-linecap:round;stroke-linejoin:round;stroke-miterlimit:10;}
         </style>
         <path class="st12" d="M320.9,11.4c0-3.6,2.6-5.5,5.3-5.5c2.4,0,4.1,1.3,4.7,3.4l-1.4,0.5c-0.4-1.6-1.6-2.5-3.3-2.5 c-1.9,0-3.8,1.4-3.8,4.2s1.8,4.2,3.8,4.2c1.8,0,3-1.1,3.4-2.5l1.3,0.5c-0.6,2-2.2,3.4-4.7,3.4C323.4,17,320.9,15,320.9,11.4zM334.7,16.7h-1.4V5.9h1.4v4.5c0.5-0.8,1.4-1.1,2.2-1.1c1.7,0,2.6,1.2,2.6,2.9v4.6H338v-4.3 c0-1-0.4-1.8-1.7-1.8c-1.1,0-1.6,0.8-1.7,1.9V16.7zM348.7,14.7c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4h-5.4c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L348.7,14.7z M347.3,12.4c0-1-0.7-1.8-2-1.8c-1.2,0-1.9,0.9-2,1.8 H347.3zM352.2,13.1c0,1.6,1,2.5,2.2,2.5c1.3,0,1.8-0.9,2-1.5l1.2,0.5c-0.3,1-1.4,2.2-3.3,2.2c-2.1,0-3.6-1.6-3.6-3.8 c0-2.2,1.6-3.8,3.6-3.8c1.9,0,2.9,1.2,3.2,2.3l-1.3,0.5c-0.2-0.7-0.7-1.5-1.9-1.5C353.2,10.6,352.2,11.4,352.2,13.1zM363.4,12.6l3.1,4.2h-1.8l-2.4-3.2l-1,1v2.2H360V5.9h1.4v6.8l3.1-3.2h1.9L363.4,12.6zM369.3,5.8c0.6,0,1,0.4,1,1c0,0.6-0.4,1-1,1c-0.6,0-1-0.5-1-1C368.3,6.2,368.8,5.8,369.3,5.8z M368.6,16.7 V9.5h1.4v7.2H368.6zM374.6,16.7h-1.4V9.5h1.4v1c0.5-0.9,1.4-1.2,2.2-1.2c1.7,0,2.6,1.2,2.6,2.9v4.6h-1.4v-4.3 c0-1-0.4-1.8-1.7-1.8c-1.1,0-1.7,0.9-1.7,2V16.7zM383.2,16.8c0.1,1,0.9,1.8,2,1.8c1.5,0,2.2-0.8,2.2-2.3v-1c-0.3,0.7-1.1,1.2-2.2,1.2c-1.9,0-3.3-1.5-3.3-3.5 c0-1.9,1.3-3.5,3.3-3.5c1.1,0,1.9,0.4,2.2,1.1v-1h1.4v6.7c0,1.8-0.9,3.6-3.6,3.6c-1.8,0-3.1-1.1-3.3-2.7L383.2,16.8z M387.4,12.9 c0-1.4-0.8-2.3-2.1-2.3c-1.2,0-2.1,0.9-2.1,2.3c0,1.4,0.8,2.3,2.1,2.3C386.6,15.2,387.4,14.3,387.4,12.9zM401.1,5.9c2.7,0,5.3,2,5.3,5.5c0,3.6-2.7,5.5-5.3,5.5c-2.7,0-5.3-2-5.3-5.5C395.8,7.9,398.4,5.9,401.1,5.9z M401.1,15.6c2,0,3.8-1.4,3.8-4.2s-1.9-4.2-3.8-4.2c-2,0-3.8,1.4-3.8,4.2S399.1,15.6,401.1,15.6zM411.7,17c-1.7,0-2.7-1.3-2.7-2.9V9.5h1.4v4.3c0,1,0.4,1.9,1.6,1.9c1.1,0,1.7-0.8,1.7-1.8V9.5h1.4v5.9 c0,0.6,0,1.1,0.1,1.3h-1.4c0-0.2-0.1-0.6-0.1-0.9C413.4,16.6,412.5,17,411.7,17zM420.2,9.5h1.6v1.3h-1.6v3.8c0,0.7,0.3,1,1,1c0.2,0,0.4,0,0.6-0.1v1.2c-0.1,0-0.5,0.1-1,0.1 c-1.2,0-2-0.8-2-2.1v-4h-1.4V9.5h0.4c0.8,0,1.1-0.5,1.1-1.1V7.2h1.3V9.5zM439.1,16.7V8.5l-3.6,8.3h-1.3l-3.6-8.3v8.3H429V6.1h2l3.7,8.7l3.8-8.7h2v10.6H439.1zM445.5,12.6l1.9-0.3c0.4-0.1,0.6-0.3,0.6-0.5c0-0.7-0.5-1.3-1.6-1.3c-1,0-1.5,0.6-1.6,1.5l-1.4-0.3 c0.2-1.4,1.4-2.3,3-2.3c2.2,0,3,1.2,3,2.6v3.6c0,0.6,0.1,1,0.1,1.2h-1.4c0-0.2-0.1-0.5-0.1-1c-0.3,0.5-1,1.2-2.3,1.2 c-1.5,0-2.4-1-2.4-2.2C443.3,13.5,444.2,12.8,445.5,12.6z M448,13.6v-0.3l-2.2,0.3c-0.6,0.1-1,0.4-1,1.1c0,0.5,0.4,1,1.2,1 C447.1,15.8,448,15.2,448,13.6zM452.9,14.4c0.1,0.8,0.7,1.3,1.7,1.3c0.8,0,1.2-0.4,1.2-1c0-0.4-0.3-0.8-0.9-0.9l-1.2-0.3 c-1.1-0.2-1.8-1-1.8-2c0-1.2,1.2-2.3,2.6-2.3c2,0,2.6,1.3,2.7,1.9l-1.2,0.5c-0.1-0.4-0.4-1.2-1.5-1.2c-0.7,0-1.2,0.5-1.2,1 c0,0.4,0.3,0.8,0.8,0.9l1.2,0.3c1.3,0.3,2,1.1,2,2.1c0,1-0.9,2.2-2.6,2.2c-2,0-2.8-1.3-2.9-2.1L452.9,14.4zM461.8,9.5h1.6v1.3h-1.6v3.8c0,0.7,0.3,1,1,1c0.2,0,0.4,0,0.6-0.1v1.2c-0.1,0-0.5,0.1-1,0.1 c-1.2,0-2-0.8-2-2.1v-4H459V9.5h0.4c0.8,0,1.1-0.5,1.1-1.1V7.2h1.3V9.5zM472.1,14.7c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4h-5.4c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L472.1,14.7z M470.7,12.4c0-1-0.7-1.8-2-1.8c-1.2,0-1.9,0.9-2,1.8 H470.7zM478.7,10.9c-0.2,0-0.4,0-0.6,0c-1.2,0-2,0.6-2,2.2v3.6h-1.4V9.5h1.4v1.3c0.5-1.1,1.4-1.4,2.2-1.4 c0.2,0,0.4,0,0.5,0V10.9z"/><path class="st13" d="M488.8 397.1H585V447.1H488.8z"/><path class="st9" d="M523.5,428.1v-8.3l-3.6,8.3h-1.3l-3.6-8.3v8.3h-1.5v-10.6h2l3.7,8.7l3.8-8.7h2v10.6H523.5zM529.9,423.9l1.9-0.3c0.4-0.1,0.6-0.3,0.6-0.5c0-0.7-0.5-1.3-1.6-1.3c-1,0-1.5,0.6-1.6,1.5l-1.4-0.3 c0.2-1.4,1.4-2.3,3-2.3c2.2,0,3,1.2,3,2.6v3.6c0,0.6,0.1,1,0.1,1.2h-1.4c0-0.2-0.1-0.5-0.1-1c-0.3,0.5-1,1.2-2.3,1.2 c-1.5,0-2.4-1-2.4-2.2C527.7,424.8,528.7,424.1,529.9,423.9z M532.4,425v-0.3l-2.2,0.3c-0.6,0.1-1,0.4-1,1.1c0,0.5,0.4,1,1.2,1 C531.5,427.1,532.4,426.5,532.4,425zM537.4,425.7c0.1,0.8,0.7,1.3,1.7,1.3c0.8,0,1.2-0.4,1.2-1c0-0.4-0.3-0.8-0.9-0.9l-1.2-0.3 c-1.1-0.2-1.8-1-1.8-2c0-1.2,1.2-2.3,2.6-2.3c2,0,2.6,1.3,2.7,1.9l-1.2,0.5c-0.1-0.4-0.4-1.2-1.5-1.2c-0.7,0-1.2,0.5-1.2,1 c0,0.4,0.3,0.8,0.8,0.9l1.2,0.3c1.3,0.3,2,1.1,2,2.1c0,1-0.9,2.2-2.6,2.2c-2,0-2.8-1.3-2.9-2.1L537.4,425.7zM546.2,420.8h1.6v1.3h-1.6v3.8c0,0.7,0.3,1,1,1c0.2,0,0.4,0,0.6-0.1v1.2c-0.1,0-0.5,0.1-1,0.1 c-1.2,0-2-0.8-2-2.1v-4h-1.4v-1.3h0.4c0.8,0,1.1-0.5,1.1-1.1v-1.2h1.3V420.8zM556.6,426c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4h-5.4c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L556.6,426z M555.2,423.7c0-1-0.7-1.8-2-1.8 c-1.2,0-1.9,0.9-2,1.8H555.2zM563.2,422.3c-0.2,0-0.4,0-0.6,0c-1.2,0-2,0.6-2,2.2v3.6h-1.4v-7.2h1.4v1.3c0.5-1.1,1.4-1.4,2.2-1.4 c0.2,0,0.4,0,0.5,0V422.3z"/><path class="st4" d="M536.9 353.6L536.9 377.1M526 362.3L536.9 351.4 547.7 362.3M640.9,226.9M557.9 226.9L515.9 226.9M402.9 308.9L515.9 308.9M444.2,267.9c0,22.6-18.4,41-41,41H286.4h-85.3M444.2,267.9c0-22.6,18.4-41,41-41h30.7"/><circle class="st11" cx="346.6" cy="308.9" r="21"/><circle class="st11" cx="263.4" cy="308.9" r="21"/><circle class="st11" cx="536.9" cy="226.9" r="21"/><circle class="st14" cx="536.9" cy="308.9" r="21"/><circle class="st11" cx="180.1" cy="308.9" r="21"/><path class="st4" d="M536 184.2L536 160.7M546.8 175.5L536 186.4 525.1 175.5"/><path class="st8" d="M466.1 88.7H607.7V138.7H466.1z"/><path class="st9" d="M493.9,112c-0.1-0.8-0.8-1.8-2.2-1.8c-1.2,0-2.1,0.8-2.1,1.8c0,0.8,0.5,1.4,1.4,1.5l1.6,0.3 c1.8,0.4,2.8,1.5,2.8,3c0,1.6-1.4,3.1-3.7,3.1c-2.6,0-3.8-1.6-4-3.2l1.4-0.4c0.1,1.2,0.9,2.3,2.5,2.3c1.5,0,2.2-0.8,2.2-1.7 c0-0.8-0.5-1.4-1.6-1.6l-1.5-0.3c-1.5-0.3-2.6-1.3-2.6-2.9c0-1.7,1.5-3.2,3.5-3.2c2.4,0,3.4,1.5,3.6,2.6L493.9,112zM504.6,116.1c0,2.2-1.5,3.8-3.7,3.8s-3.7-1.6-3.7-3.8c0-2.2,1.5-3.8,3.7-3.8S504.6,113.9,504.6,116.1z M503.1,116.1c0-1.7-1.1-2.6-2.2-2.6s-2.2,0.9-2.2,2.6c0,1.7,1.1,2.6,2.2,2.6S503.1,117.8,503.1,116.1zM507.1,119.7v-7.2h1.3v1c0.5-0.8,1.4-1.2,2.2-1.2c0.9,0,1.8,0.4,2.2,1.4c0.6-1,1.5-1.4,2.4-1.4 c1.3,0,2.5,0.9,2.5,2.7v4.7h-1.4v-4.5c0-0.9-0.5-1.6-1.5-1.6c-1,0-1.7,0.8-1.7,1.8v4.4h-1.4v-4.5c0-0.9-0.4-1.6-1.5-1.6 c-1,0-1.7,0.8-1.7,1.8v4.3H507.1zM527,117.7c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4h-5.4c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L527,117.7z M525.6,115.4c0-1-0.7-1.8-2-1.8 c-1.2,0-1.9,0.9-2,1.8H525.6zM534.3,119.7v-10.6h6.5v1.4h-5v3.4h4.5v1.4h-4.5v4.5H534.3zM548.9,117.7c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4h-5.4c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L548.9,117.7z M547.5,115.4c0-1-0.7-1.8-2-1.8 c-1.2,0-1.9,0.9-2,1.8H547.5zM553.2,115.6l1.9-0.3c0.4-0.1,0.6-0.3,0.6-0.5c0-0.7-0.5-1.3-1.6-1.3c-1,0-1.5,0.6-1.6,1.5l-1.4-0.3 c0.2-1.4,1.4-2.3,3-2.3c2.2,0,3,1.2,3,2.6v3.6c0,0.6,0.1,1,0.1,1.2h-1.4c0-0.2-0.1-0.5-0.1-1c-0.3,0.5-1,1.2-2.3,1.2 c-1.5,0-2.4-1-2.4-2.2C551,116.5,552,115.8,553.2,115.6z M555.7,116.6v-0.3l-2.2,0.3c-0.6,0.1-1.1,0.4-1.1,1.1c0,0.5,0.4,1,1.2,1 C554.8,118.8,555.7,118.2,555.7,116.6zM562,112.5h1.6v1.3H562v3.8c0,0.7,0.3,1,1,1c0.2,0,0.4,0,0.6-0.1v1.2c-0.1,0-0.5,0.1-1,0.1 c-1.2,0-2-0.8-2-2.1v-4h-1.4v-1.3h0.4c0.8,0,1.1-0.5,1.1-1.1v-1.2h1.3V112.5zM568.8,120c-1.7,0-2.7-1.3-2.7-2.9v-4.5h1.4v4.3c0,1,0.4,1.9,1.6,1.9c1.1,0,1.7-0.8,1.7-1.8v-4.4h1.4v5.9 c0,0.6,0,1.1,0.1,1.3H571c0-0.2-0.1-0.6-0.1-0.9C570.5,119.6,569.6,120,568.8,120zM579.4,113.9c-0.2,0-0.4,0-0.6,0c-1.2,0-2,0.6-2,2.2v3.6h-1.4v-7.2h1.4v1.3c0.5-1.1,1.4-1.4,2.2-1.4 c0.2,0,0.4,0,0.5,0V113.9zM587.9,117.7c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4h-5.4c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L587.9,117.7z M586.4,115.4c0-1-0.7-1.8-2-1.8 c-1.2,0-1.9,0.9-2,1.8H586.4z"/><path class="st12" d="M295.9,657.4c0-3.6,2.6-5.5,5.3-5.5c2.4,0,4.1,1.3,4.7,3.4l-1.4,0.5c-0.4-1.6-1.6-2.5-3.3-2.5 c-1.9,0-3.8,1.4-3.8,4.2s1.8,4.2,3.8,4.2c1.8,0,3-1.1,3.4-2.5l1.3,0.5c-0.6,2-2.2,3.4-4.7,3.4C298.4,663,295.9,661,295.9,657.4zM309.6,662.7h-1.4v-10.9h1.4v4.5c0.5-0.8,1.4-1.1,2.2-1.1c1.7,0,2.6,1.2,2.6,2.9v4.6H313v-4.3 c0-1-0.4-1.8-1.7-1.8c-1.1,0-1.6,0.8-1.7,1.9V662.7zM323.7,660.7c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4h-5.4c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L323.7,660.7z M322.3,658.4c0-1-0.7-1.8-2-1.8 c-1.2,0-1.9,0.9-2,1.8H322.3zM327.1,659.1c0,1.6,1,2.5,2.2,2.5c1.3,0,1.8-0.9,2-1.5l1.2,0.5c-0.3,1-1.4,2.2-3.3,2.2 c-2.1,0-3.6-1.6-3.6-3.8c0-2.2,1.6-3.8,3.6-3.8c1.9,0,2.9,1.2,3.2,2.3l-1.3,0.5c-0.2-0.7-0.7-1.5-1.9-1.5 C328.2,656.6,327.1,657.4,327.1,659.1zM338.4,658.6l3.1,4.2h-1.8l-2.4-3.2l-1,1v2.2H335v-10.9h1.4v6.8l3.1-3.2h1.9L338.4,658.6zM344.3,651.8c0.6,0,1,0.4,1,1c0,0.6-0.4,1-1,1c-0.6,0-1-0.5-1-1C343.3,652.2,343.8,651.8,344.3,651.8z M343.6,662.7v-7.2h1.4v7.2H343.6zM349.6,662.7h-1.4v-7.2h1.4v1c0.5-0.9,1.4-1.2,2.2-1.2c1.7,0,2.6,1.2,2.6,2.9v4.6h-1.4v-4.3 c0-1-0.4-1.8-1.7-1.8c-1.1,0-1.7,0.9-1.7,2V662.7zM358.2,662.8c0.1,1,0.9,1.8,2,1.8c1.5,0,2.2-0.8,2.2-2.3v-1c-0.3,0.7-1.1,1.2-2.2,1.2c-1.9,0-3.3-1.5-3.3-3.5 c0-1.9,1.3-3.5,3.3-3.5c1.1,0,1.9,0.4,2.2,1.1v-1h1.4v6.7c0,1.8-0.9,3.6-3.6,3.6c-1.8,0-3.1-1.1-3.3-2.7L358.2,662.8z M362.4,658.9 c0-1.4-0.8-2.3-2.1-2.3c-1.2,0-2.1,0.9-2.1,2.3c0,1.4,0.8,2.3,2.1,2.3C361.6,661.2,362.4,660.3,362.4,658.9zM376.1,651.9c2.7,0,5.3,2,5.3,5.5c0,3.6-2.7,5.5-5.3,5.5c-2.7,0-5.3-2-5.3-5.5 C370.7,653.9,373.4,651.9,376.1,651.9z M376.1,661.6c2,0,3.8-1.4,3.8-4.2s-1.9-4.2-3.8-4.2c-2,0-3.8,1.4-3.8,4.2 S374.1,661.6,376.1,661.6zM386.7,663c-1.7,0-2.7-1.3-2.7-2.9v-4.5h1.4v4.3c0,1,0.4,1.9,1.6,1.9c1.1,0,1.7-0.8,1.7-1.8v-4.4h1.4v5.9 c0,0.6,0,1.1,0.1,1.3h-1.4c0-0.2-0.1-0.6-0.1-0.9C388.4,662.6,387.5,663,386.7,663zM395.2,655.5h1.6v1.3h-1.6v3.8c0,0.7,0.3,1,1,1c0.2,0,0.4,0,0.6-0.1v1.2c-0.1,0-0.5,0.1-1,0.1 c-1.2,0-2-0.8-2-2.1v-4h-1.4v-1.3h0.4c0.8,0,1.1-0.5,1.1-1.1v-1.2h1.3V655.5zM409.5,655c-0.1-0.8-0.8-1.8-2.2-1.8c-1.2,0-2.1,0.8-2.1,1.8c0,0.8,0.5,1.4,1.4,1.5l1.6,0.3 c1.8,0.4,2.8,1.5,2.8,3c0,1.6-1.4,3.1-3.7,3.1c-2.6,0-3.8-1.6-4-3.2l1.4-0.4c0.1,1.2,0.9,2.3,2.5,2.3c1.5,0,2.2-0.8,2.2-1.7 c0-0.8-0.5-1.4-1.6-1.6l-1.5-0.3c-1.5-0.3-2.6-1.3-2.6-2.9c0-1.7,1.5-3.2,3.5-3.2c2.4,0,3.4,1.5,3.6,2.6L409.5,655zM420.1,659.1c0,2.2-1.5,3.8-3.7,3.8s-3.7-1.6-3.7-3.8c0-2.2,1.5-3.8,3.7-3.8S420.1,656.9,420.1,659.1z M418.7,659.1c0-1.7-1.1-2.6-2.2-2.6s-2.2,0.9-2.2,2.6c0,1.7,1.1,2.6,2.2,2.6S418.7,660.8,418.7,659.1zM422.7,662.7v-7.2h1.3v1c0.5-0.8,1.4-1.2,2.2-1.2c0.9,0,1.8,0.4,2.2,1.4c0.6-1,1.5-1.4,2.4-1.4 c1.3,0,2.5,0.9,2.5,2.7v4.7h-1.4v-4.5c0-0.9-0.5-1.6-1.5-1.6c-1,0-1.7,0.8-1.7,1.8v4.4h-1.4v-4.5c0-0.9-0.4-1.6-1.5-1.6 c-1,0-1.7,0.8-1.7,1.8v4.3H422.7zM442.6,660.7c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4h-5.4c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L442.6,660.7z M441.2,658.4c0-1-0.7-1.8-2-1.8 c-1.2,0-1.9,0.9-2,1.8H441.2zM449.8,662.7v-10.6h6.5v1.4h-5v3.4h4.5v1.4h-4.5v4.5H449.8zM464.4,660.7c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4H459c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L464.4,660.7z M463,658.4c0-1-0.7-1.8-2-1.8c-1.2,0-1.9,0.9-2,1.8 H463zM468.8,658.6l1.9-0.3c0.4-0.1,0.6-0.3,0.6-0.5c0-0.7-0.5-1.3-1.6-1.3c-1,0-1.5,0.6-1.6,1.5l-1.4-0.3 c0.2-1.4,1.4-2.3,3-2.3c2.2,0,3,1.2,3,2.6v3.6c0,0.6,0.1,1,0.1,1.2h-1.4c0-0.2-0.1-0.5-0.1-1c-0.3,0.5-1,1.2-2.3,1.2 c-1.5,0-2.4-1-2.4-2.2C466.6,659.5,467.5,658.8,468.8,658.6z M471.3,659.6v-0.3l-2.2,0.3c-0.6,0.1-1.1,0.4-1.1,1.1 c0,0.5,0.4,1,1.2,1C470.4,661.8,471.3,661.2,471.3,659.6zM477.5,655.5h1.6v1.3h-1.6v3.8c0,0.7,0.3,1,1,1c0.2,0,0.4,0,0.6-0.1v1.2c-0.1,0-0.5,0.1-1,0.1 c-1.2,0-2-0.8-2-2.1v-4h-1.4v-1.3h0.4c0.8,0,1.1-0.5,1.1-1.1v-1.2h1.3V655.5zM484.3,663c-1.7,0-2.7-1.3-2.7-2.9v-4.5h1.4v4.3c0,1,0.4,1.9,1.6,1.9c1.1,0,1.7-0.8,1.7-1.8v-4.4h1.4v5.9 c0,0.6,0,1.1,0.1,1.3h-1.4c0-0.2-0.1-0.6-0.1-0.9C486.1,662.6,485.2,663,484.3,663zM495,656.9c-0.2,0-0.4,0-0.6,0c-1.2,0-2,0.6-2,2.2v3.6H491v-7.2h1.4v1.3c0.5-1.1,1.4-1.4,2.2-1.4 c0.2,0,0.4,0,0.5,0V656.9zM503.4,660.7c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4H498c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L503.4,660.7z M502,658.4c0-1-0.7-1.8-2-1.8c-1.2,0-1.9,0.9-2,1.8 H502z"/><path class="st13" d="M488.8 1043.1H585V1093.1H488.8z"/><path class="st9" d="M523.5,1074.1v-8.3l-3.6,8.3h-1.3l-3.6-8.3v8.3h-1.5v-10.6h2l3.7,8.7l3.8-8.7h2v10.6H523.5zM529.9,1069.9l1.9-0.3c0.4-0.1,0.6-0.3,0.6-0.5c0-0.7-0.5-1.3-1.6-1.3c-1,0-1.5,0.6-1.6,1.5l-1.4-0.3 c0.2-1.4,1.4-2.3,3-2.3c2.2,0,3,1.2,3,2.6v3.6c0,0.6,0.1,1,0.1,1.2h-1.4c0-0.2-0.1-0.5-0.1-1c-0.3,0.5-1,1.2-2.3,1.2 c-1.5,0-2.4-1-2.4-2.2C527.7,1070.8,528.7,1070.1,529.9,1069.9z M532.4,1071v-0.3l-2.2,0.3c-0.6,0.1-1,0.4-1,1.1 c0,0.5,0.4,1,1.2,1C531.5,1073.1,532.4,1072.5,532.4,1071zM537.4,1071.7c0.1,0.8,0.7,1.3,1.7,1.3c0.8,0,1.2-0.4,1.2-1c0-0.4-0.3-0.8-0.9-0.9l-1.2-0.3 c-1.1-0.2-1.8-1-1.8-2c0-1.2,1.2-2.3,2.6-2.3c2,0,2.6,1.3,2.7,1.9l-1.2,0.5c-0.1-0.4-0.4-1.2-1.5-1.2c-0.7,0-1.2,0.5-1.2,1 c0,0.4,0.3,0.8,0.8,0.9l1.2,0.3c1.3,0.3,2,1.1,2,2.1c0,1-0.9,2.2-2.6,2.2c-2,0-2.8-1.3-2.9-2.1L537.4,1071.7zM546.2,1066.8h1.6v1.3h-1.6v3.8c0,0.7,0.3,1,1,1c0.2,0,0.4,0,0.6-0.1v1.2c-0.1,0-0.5,0.1-1,0.1 c-1.2,0-2-0.8-2-2.1v-4h-1.4v-1.3h0.4c0.8,0,1.1-0.5,1.1-1.1v-1.2h1.3V1066.8zM556.6,1072c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4h-5.4c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L556.6,1072z M555.2,1069.7c0-1-0.7-1.8-2-1.8 c-1.2,0-1.9,0.9-2,1.8H555.2zM563.2,1068.3c-0.2,0-0.4,0-0.6,0c-1.2,0-2,0.6-2,2.2v3.6h-1.4v-7.2h1.4v1.3c0.5-1.1,1.4-1.4,2.2-1.4 c0.2,0,0.4,0,0.5,0V1068.3z"/><path class="st4" d="M536.9 999.6L536.9 1023.1M526 1008.3L536.9 997.4 547.7 1008.3M640.9,872.9M557.9 872.9L515.9 872.9M402.9 954.9L515.9 954.9M444.2,913.9c0,22.6-18.4,41-41,41H286.4h-85.3M444.2,913.9c0-22.6,18.4-41,41-41h30.7"/><circle class="st11" cx="346.6" cy="954.9" r="21"/><circle class="st11" cx="263.4" cy="954.9" r="21"/><circle class="st14" cx="536.9" cy="872.9" r="21"/><circle class="st11" cx="536.9" cy="954.9" r="21"/><circle class="st11" cx="180.1" cy="954.9" r="21"/><path class="st4" d="M536 830.2L536 806.7M546.8 821.5L536 832.4 525.1 821.5"/><path class="st8" d="M466.1 734.7H607.7V784.7H466.1z"/><path class="st9" d="M493.9,758c-0.1-0.8-0.8-1.8-2.2-1.8c-1.2,0-2.1,0.8-2.1,1.8c0,0.8,0.5,1.4,1.4,1.5l1.6,0.3 c1.8,0.4,2.8,1.5,2.8,3c0,1.6-1.4,3.1-3.7,3.1c-2.6,0-3.8-1.6-4-3.2l1.4-0.4c0.1,1.2,0.9,2.3,2.5,2.3c1.5,0,2.2-0.8,2.2-1.7 c0-0.8-0.5-1.4-1.6-1.6l-1.5-0.3c-1.5-0.3-2.6-1.3-2.6-2.9c0-1.7,1.5-3.2,3.5-3.2c2.4,0,3.4,1.5,3.6,2.6L493.9,758zM504.6,762.1c0,2.2-1.5,3.8-3.7,3.8s-3.7-1.6-3.7-3.8c0-2.2,1.5-3.8,3.7-3.8S504.6,759.9,504.6,762.1z M503.1,762.1c0-1.7-1.1-2.6-2.2-2.6s-2.2,0.9-2.2,2.6c0,1.7,1.1,2.6,2.2,2.6S503.1,763.8,503.1,762.1zM507.1,765.7v-7.2h1.3v1c0.5-0.8,1.4-1.2,2.2-1.2c0.9,0,1.8,0.4,2.2,1.4c0.6-1,1.5-1.4,2.4-1.4 c1.3,0,2.5,0.9,2.5,2.7v4.7h-1.4v-4.5c0-0.9-0.5-1.6-1.5-1.6c-1,0-1.7,0.8-1.7,1.8v4.4h-1.4v-4.5c0-0.9-0.4-1.6-1.5-1.6 c-1,0-1.7,0.8-1.7,1.8v4.3H507.1zM527,763.7c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4h-5.4c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L527,763.7z M525.6,761.4c0-1-0.7-1.8-2-1.8 c-1.2,0-1.9,0.9-2,1.8H525.6zM534.3,765.7v-10.6h6.5v1.4h-5v3.4h4.5v1.4h-4.5v4.5H534.3zM548.9,763.7c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4h-5.4c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L548.9,763.7z M547.5,761.4c0-1-0.7-1.8-2-1.8 c-1.2,0-1.9,0.9-2,1.8H547.5zM553.2,761.6l1.9-0.3c0.4-0.1,0.6-0.3,0.6-0.5c0-0.7-0.5-1.3-1.6-1.3c-1,0-1.5,0.6-1.6,1.5l-1.4-0.3 c0.2-1.4,1.4-2.3,3-2.3c2.2,0,3,1.2,3,2.6v3.6c0,0.6,0.1,1,0.1,1.2h-1.4c0-0.2-0.1-0.5-0.1-1c-0.3,0.5-1,1.2-2.3,1.2 c-1.5,0-2.4-1-2.4-2.2C551,762.5,552,761.8,553.2,761.6z M555.7,762.6v-0.3l-2.2,0.3c-0.6,0.1-1.1,0.4-1.1,1.1c0,0.5,0.4,1,1.2,1 C554.8,764.8,555.7,764.2,555.7,762.6zM562,758.5h1.6v1.3H562v3.8c0,0.7,0.3,1,1,1c0.2,0,0.4,0,0.6-0.1v1.2c-0.1,0-0.5,0.1-1,0.1 c-1.2,0-2-0.8-2-2.1v-4h-1.4v-1.3h0.4c0.8,0,1.1-0.5,1.1-1.1v-1.2h1.3V758.5zM568.8,766c-1.7,0-2.7-1.3-2.7-2.9v-4.5h1.4v4.3c0,1,0.4,1.9,1.6,1.9c1.1,0,1.7-0.8,1.7-1.8v-4.4h1.4v5.9 c0,0.6,0,1.1,0.1,1.3H571c0-0.2-0.1-0.6-0.1-0.9C570.5,765.6,569.6,766,568.8,766zM579.4,759.9c-0.2,0-0.4,0-0.6,0c-1.2,0-2,0.6-2,2.2v3.6h-1.4v-7.2h1.4v1.3c0.5-1.1,1.4-1.4,2.2-1.4 c0.2,0,0.4,0,0.5,0V759.9zM587.9,763.7c-0.4,1.3-1.6,2.3-3.2,2.3c-1.9,0-3.6-1.4-3.6-3.9c0-2.3,1.6-3.8,3.4-3.8c2.2,0,3.5,1.5,3.5,3.8 c0,0.2,0,0.4,0,0.4h-5.4c0,1.3,1,2.2,2.2,2.2c1.2,0,1.8-0.6,2-1.5L587.9,763.7z M586.4,761.4c0-1-0.7-1.8-2-1.8 c-1.2,0-1.9,0.9-2,1.8H586.4z"/>
<path class="st15" d="M129.3 550.1L670.7 550.1"/></svg>

## 4.3. Listing branches

```
 $ git branch
```
List all of the branches in your repository locally.

```
$  git branch -r
```
List all the branches present on remote.

```
$ git branch -a
```
List all the branches from remote as well as local.


## 4.4. Renaming branch

```
$ git branch -m new_name
```

Rename the current branch to  new_name

## 4.5. Destroy branch

```
 $ git branch -d branch_name
```
Delete the specified branch. This is a “safe” operation in that Git prevents you from deleting the branch if it has
unmerged changes.

```
 $ git branch -D branch_name
```
Force delete the specified branch, even if it has unmerged changes. This is the command to use if you want to permanently
throw away all of the commits associated with a particular line of development.

```
 $ git push origin :branch_name
```
where origin is remote_name.
Delete the specific branch from remote.

# 5. Merging

Once you’ve finished developing a feature in an isolated branch, it's important to be able to get it back into the main
 code base,so that everyone can use it. You can do so with the git merge or git pull command.
 
```
 $ git merge <branch>
```

Above command merge the specified branch into the current branch. Git will determine the merge algorithm automatically.

```
 $ git merge --no-ff <branch>
```

Above command merge the specified branch into the current branch, but always generate a merge commit (even if it was a fast-forward 
merge). This is useful for documenting all merges that occur in your repository.

```
 $ git pull <remote_name> <branch> 
```

Above command merge the specified branch into the current branch.

## 5.1. Fast forward merge

A fast-forward merge can occur when there is a linear path from the current branch tip to the target branch. Instead of 
“actually” merging the branches, all Git has to do to integrate the histories is move (i.e., “fast forward”) the current
 branch tip up to the target branch tip. This effectively combines the histories, since all of the commits reachable 
from the target branch are now available through the current one. For example, a fast forward merge of some-feature into
 master would look something like the following:
 
 
![Fast forward merge](ff_merging.svg)


## 5.2. 3-way merge

Now suppose we have not linear path to the target branch i.e, branch is diverged. In this case a fast-forward merge is not 
possible if the branches have diverged. When there is not a linear path to the target branch, Git has no choice but to 
combine them via a 3-way merge. 3-way merges use a dedicated commit to tie together the two histories. The nomenclature 
comes from the fact that Git uses three commits to generate the merge commit: the two branch tips and their common 
ancestor.


![3-way merge](3_way.svg)

In 3-way merge, there is may be occur merging conflicts.

## 5.3. Resolving Conflicts

If the two branches you're trying to merge both changed the same part of the same file, Git won't be able to figure out 
which version to use. When such a situation occurs, it stops right before the merge commit so that you can resolve the 
conflicts manually.

Merge conflicts will only occur in the event of a 3-way merge. It’s not possible to have conflicting changes in a 
fast-forward merge.

To resolve the commit, edit the files to fix the conflicting changes. Then run git add to add the resolved files, and 
run git commit to commit the repaired merge. Git remembers that you were in the middle of a merge, so it sets the 
parents of the commit correctly.




