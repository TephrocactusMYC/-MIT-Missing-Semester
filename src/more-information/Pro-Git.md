# This is the notes of reading ProGit
[Pro Git](https://git-scm.com/book/en/v2) is an open source book!

# Installing Git
First of all, do not forget to config your git, especailly the editor(In my ubuntu, the default editor is nano).
```shell
git config --global user.name "name"
git config --global user.email example@email.com
git config --global core.editor vim
# then
git config --list
```
# Basic operate
Many basic command to learn!
```shell
# get a repo
git clone 
git init

# git add
git add .
git commit -m "add"

# push
git push

# branch
git checkout mybranch

# log
git log

# status
git status
git diff

# rm
git rm

# mv
git mv 

# tag
git tag
```
# track
Remember that each file in your working directory can be in one of two states: tracked or untracked.

# snapshot
Git doesn’t think of or store its data this way. Instead, Git thinks of its data more like a series of snapshots of a miniature filesystem. With Git, every time you commit, or save the state of your project, Git basically takes a picture of what all your files look like at that moment and stores a reference to that snapshot. To be efficient, if files have not changed, Git doesn’t store the file again, just a link to the previous identical file it has already stored. Git thinks about its data more like a stream of snapshots.

# Three states
Git has three main states that your files can reside in: modified, staged, and committed:

- Modified means that you have changed the file but have not committed it to your database yet.

- Staged means that you have marked a modified file in its current version to go into your next commit snapshot.

- Committed means that the data is safely stored in your local database.

This leads us to the three main sections of a Git project: the working tree, the staging area, and the Git directory.

# branch
The main information:
- Git is a version control system that supports branching. 
- Git's branches are lightweight and easy to create and switch between. 
- Git encourages frequent use of branching and merging. 
- Git saves file snapshots, and when committing, it saves a commit object that includes pointers to the snapshot of staged content and parent objects.
- Git branches are essentially mutable pointers to commit objects, with "master" being the default name.
- Creating a new branch simply requires creating a new branch pointer.
- HEAD is a special pointer that points to the currently active local branch.


# rebase
There is no difference in the end product of the integration, but rebasing makes for a cleaner history. 

# Distributed Workflows
Integration-Manager Workflow is very useful.

# Stashing
Stashing is used when you don't want to commit your current work but have to switch to another branch.


# More
Combined with the Pro-Git pictures, you will have a deeper understanding.



