+++
date = '2019-07-30T18:52:26+05:30'
draft = false
title = 'The Force - Git'
+++

Git is a very popular and efficient Distributed Version Control System used by many contributors for many projects. “Distributed” means that all developers within a team have a complete version of the project. It's free and open source. Most of us dislike Git on the first try even after running the most basic Git commands. Git is complicated at first I agree. But Git is so dear to Programmers.
Sadly programmers life is a mess without Git. Its very helpful for managing projects

### “I know who did what, when, and why.” -Git

There are few commands using which we can make our life easier and let Git to track everything.

### Getting & Creating Projects:

`$ git init:` After creating a new directory, perform git init to create an empty git repository. 

`$ git clone:` By running this command, create a working copy of a repository in your local. There are several ways to clone a repository.
1. https:// clone URLs are available on all repositories, public and private. 
2. SSH URLs provide access to a Git repository via SSH, a secure protocol.

### Basic Snapshotting:

`$ git status:` It simply shows you what's been going on with git add and git commit. The Status messages also include relevant instructions for staging/unstaging files. Sample output showing that on branch “Pluto_Branch” nothing to commit.
```bash
[rayan@localhost foobar]$ git status
On branch Pluto-Branch
nothing to commit, working tree clean
```

`$ git add:` This command adds a change in the working directory to the staging area. It tells Git that you want to include updates to a particular file in the next commit.

`$ git add [file-name.txt]:` This command stage all changes in [file-name.txt] for the next commit.

`$ git add -A:` This command will add all new and modified files to the staging area. Along with unwanted/test files

`$ git commit -m "[commit message]":` This command is used to commit the changes you have added. -m is used for connecting a commit message to your commit.

`$ git rm -r [file-name.txt]:` This command is used to remove a file/directory

### Branching & Merging:

`$ git branch:` List all the branches associated with the repository. (the asterisk points to the current branch)

`$ git branch -a:` List all the branches associated with your repository (local and remote)

`$ git branch [branch name]:` this command is to create a new branch in the current repository

`$ git branch -d [branch name]:` Used to delete mentioned branch.

`$ git push origin --delete [branch name]:` This command is used to delete a remote branch

`$ git checkout -b [branch name]:` Used to create a new branch then switch to it

`$ git checkout [branch name]:` Used to switch to the mentioned branch.

`$ git checkout - :` used to switch to the branch last visited.

`$ git checkout -- [file-name.txt]:` discard all the changes to a file

`$ git merge [branch name]:` This command is used to integrate changes from another branch.

`$ git merge [source branch] [target branch]:` Allows us to merge a the source branch into the target branch.

### Sharing & Updating Projects:

`$ git push origin [branch name]:` Pushes all the modified local objects to the remote repository and advances its branches.

`$ git push -u origin [branch name]:` This command  sets the upstream of the current local branch, so that it tracks [branch name] branch of the remote repository origin.

`$ git push origin --delete [branch name]:` To delete a remote branch we use this command with —delete flag.

`$ git pull:` This command fetches the files from the remote repository and merges it with your local one.

`$ git pull origin [branch name]:` It will fetch the remote branch and merge it into your current local branch.

`$ git remote add origin ssh://git@github.com/[username]/[repository-name].git:` This command is used to add a remote repository.

`$ git remote set-url origin ssh://git@github.com/[username]/[repository-name].git:` To set a repository's origin branch to SSH

### Inspection & Comparison:

`$ git log:` Shows a listing of commits on a branch including author, date, number of commits, current branch, what all things are required to commit, message, content.

`$ git log --summary:` This command will shows the list of commits with more details.

`$ git diff:` This command is used in git to track the difference between the changes made on a file.

