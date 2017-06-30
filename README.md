# git-guide

## Table of Contents
  1. [Setup](#1-basic-setup)  
    1.1. [Installation](#11-git-installation)  
    1.2. [Configurations](#12-git-configurations) 
         
    
 
   
# 1. Setup

This section will be a quick setup guide for installing and using Git and GitHub and how to perform its various functions of creating a user and a repository locally, connecting this repo to the remote host that contains your project to GitHub.

## 1.1. Installation

Install git on an Ubuntu for this you can use the apt package management tools to update your local package index. Afterwards, you can download and install the program:

```
    $ sudo apt-get update
    $ sudo apt-get install git

```

This will download and install git to your system. You will still have to complete the configuration steps that we cover in the next section.

## 1.2. Configurations

Now that you have git installed, you need to do a few things so that the commit messages that will be generated for you will contain your correct information.

The easiest way of doing this is through the git config command. Specifically, we need to provide our name and email address because git embeds this information into each commit we do. We can go ahead and add this information by typing:

```
    $ git config --global user.name "Your Name"
    $ git config --global user.email "youremail@domain.com"
    
```

You can see all of the configuration items from:


```
    $ git config --list
    
```

