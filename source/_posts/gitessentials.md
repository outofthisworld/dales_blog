title: 'Working with GIT, version control system'
tags:
  - 'Git, Github, Version Control'
categories:
  - GitHub
author: Dale Appleby
featured_image: /css/images/gitrepo_0.png
date: 2017-10-21 14:02:00
---
![upload successful](/css/images/pasted-2.png)


## What is git, anyway?
#### For those of you that have been living under a rock for the last little while, or those still using SVN or mercrial or another popular version control system, this post may come in handy. Today we're going to be talking about git, a tool which is used to enable you to easily manage a project across multiple versions and seamesly integrate and work within a team environment. Git was created by Linus Torvalds in 2005 during development of the Linux kernal and has since become one of the most popular version control systems to date.





## Version control respositories
#### There are many websites that use git as the client to interface with repos that are hosted in the cloud. These websites offer tons of features including continious testing, bug tracking, code reviews, access control and of course private and free repos. GitHub is the most popular online version control system, with over 20 million users and over 57 million code repos. Other options include BitBucket...For the purpose of this blog post however we will be focusing on using git with GitHub as it is the most frequently used.

## So what does GitHub offer?
    1. Documentation in form of markdown readme.md file.
    
    2. Issue tracking 

    4. Access control

    5. Wikis

    6. Pull requests with code review and comments

    7. Commits history

    8. Analytics: pulse, contributors, commits, code frequency, punch card, network, members

    9. Difference files

    11. Rollback/reset head

    10. GitHub Pages: small websites can be hosted from public repositories on GitHub.

#### These simple things, on projects of varying size become an invaluable tool to being a productive developer and increasing productivity and workflows.





## Getting started.. creating your first repo!
#### If you haven't already, pop on over to [GitHub](https://www.google.com "GitHub") and create an account. Once your account is created, follow the steps to create your first repository!

![GitHub repo image](/css/images/gitrepo_0.png "Logo Title Text 1")



## Using your repository
#### Great, you now have a github account and a fresh repository, but now what? Well... It's time to make your first push to Github. First we need to create a folder which will house the all of our code.

 If you're on OSX/linux you can run the follwing command in your terminal to create a new project folder on your desktop for the time being:

```Bash
cd ~/Desktop/ && mkdir myfirstgitproject && cd myfirstgitproject && echo "This is my first github project" > readme.md
```

#### On windows (since I don't know the windows command line very well) navigate to your desktop and create a new folder named 'myfirstgitproject' and within this folder create a new file named readme.md and put any content you like within this file.

## Basic commands
#### Wohoo, we have our project folder. Now we can learn about some of the basic GitHub commands before we start using them for on our new project.

### Git init
```Bash
    git init #initializes a new or existing git project.
```
#### git init initalizes the current directory as a git repository. Behind the scenes it creates a hidden .git folder that is used to help git function correctly. You will never need to touch this folder, but every new project folder you create that you want to integrate with git will require you to use this command.

### Git add
```Bash
    git add <file> #adds a file to the staging area
    git add <directory> #adds a directory to the staging area
    git add --all #adds all files to the staging area
```
#### git add is used to prepare content for the next commit. It places files into a staging area, updating the index of the working tree. The index holds a snapshot of the working trees content and git add places files into this index. You can see items within your staging area using the git status command. Note that if you modify a file that has already been added to the staging area using git add, you will have to add it again.

### Git status
```Bash
git status #shows information regarding tracked/untracked files on the current branch
```
```Bash
root@groot:~/Desktop/myfirstgitproject> git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        readme.md

nothing added to commit but untracked files present (use "git add" to track)
```

#### git status shows information regarding the current branch and the files that are tracked and untracked. Untracked files are those files that have not been added to the staging area of the current branch. Untracked files are not pushed to the your projects github repository, first you must add them using the git add <file> command.


### Git commit
```Bash
    git commit -m <message>
```
#### Git commit is essentially a save point during the projects life cycle. Once you are happy with the contents of the staging area (seen using the git status command) you can finalize the snapshot using this command. This will save the snapshot into your projects history and you can easily revert back to that commit in the future.


### Git remote
```Bash
    git remote add origin <repo>
```
#### git remote essentially creates an alias to refer to a git repository hosted on a server. When you have finished making changes locally, you can push your code to the server, specifying the remote location that you want to upload to.

### Git branch
```Bash
    git branch <branchname>
```
#### git branch allows you to create a separate local work flow away from the current master branch. When you create a new branch using git branch, the branch is brought to the current place in time of the master. Any changes you make will only be visible within the newly created branch. When you are happy with a branch, you can merge the changes into the master branch or create what is known as a pull request in order for your team to review the changes before it is merged into the main code base. Branches are very useful for working on separate features and and are an essential tool in many git workflows as we will discuss later.

### Git push
```Bash
    git push -u <remote> <branch>
```
#### Pushes all staged files in the specified branch to the specified remote. This will update the repository held on the server.

## Working with our basic command set
#### We now have a good understanding of some of the essential git commands lets put them to good use with the project we created earlier.

#### First make sure you are in the right folder, using the cd command navigate to the root of your project:

```Bash
	cd ~/Desktop/myfirstgitproject
```

#### Next, we would like to initialize the project folder as a git repository. To do this we use the git init command:
```Bash
	git init
```
#### Great! We have our project folder initialized to use git. The next step is to add some files to the staging area, telling git that we want these files within our current working tree. Luckily we have one file to work with named readme.md. readme.md is a markdown file that GitHub renders on a repo page when someone visits it. It is used to, amongst other things, explain what the code in a particular repo does, how people can use/compile/download the code, and how people can contribute to the code. Our readme just says "hello world", but you can specify anything you like. Without further ado, lets add the file to our staging area using the following command:
```Bash
	git add readme.md
```

#### If everything went according to plan, the file should now be within our staging area. We can double check this by checking the output of the git status command. You should see something like this:
```Bash
  On branch master

  Initial commit

  Changes to be committed:
    (use "git rm --cached <file>..." to unstage)

      new file:   readme.md
```

#### Next we need to tell git that we are done with our changes by creating a new commit. Remember commits are essentially save points, you can roll back your source code to any commit point. One thing to note is that commits should be after every logically related change. By this I mean, you shouldn't modify the readme, then work on the front end HTML code, then modify some of the server side code and then jump on over to some of the client side scripts and then commit unless all of these changes are related to one another. Rather, if they are unrelated you would break it down into serveral commits, once for the read me, once for the front end HTML, once for the server side code, and once to the client side scripts. This way, it makes it easier to go back to a certain point, and it also makes it easier for people that look at your repos commits to see what changes have been made and at what point in time. Awesome, now lets create our commit:
```Bash
	git commit -m "Updated readme to say \"hello world\""
```

#### We are now done with our first commit, now all we have to do is send these changes to our server repository! In order to do so, we have to set up our remote so that it points at our GitHub repo. Navigate to your repo and copy the link to it, next run the following command replacing it with the url to your repo (Don't forget to add .git at the end of the url in the command) :
```Bash
	git remote add origin <urltoyourgitrepo>.git
```

#### We now have our remote, and we are almost done. The last thing we have to do is push our changes to the remotes master branch. To do this, we use the following command:
```Bash
	git push -u origin master
```

#### Assuming you're connected to the internet and the push completed succesfully, you should now be able to navigate to your repos URL and see the readme.md file within your repository. Congratulations if you have made it this far, you now have a decent understanding of what is needed to push your code to a remote repository. However, there is still much more to learn about git. We still don't know how to keep our local repo in sync with the server side repo. What if you have a team member working with you and they have made a change while you are working on your code? We also haven't learnt how to merge changes from branches, and how to resolve any conflicts that may occur. We also need to learn about pull requests, and the difference between rebasing and branching. Lastly, we need to understand the fundamental team workflows, that way we have a good understanding of how to use git in a team environment. It's a long road ahead, but we shall get through it!

# To be continued...
