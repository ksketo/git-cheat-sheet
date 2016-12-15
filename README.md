# Git Cheat Sheet

## Basic Commands

**Initialize git repo**

`git init`

**See project state.**
If a new file was created then this command will show that the file is untracked and needs to be added, to include in the project what will be committed.

`git status`

**Making changes**

Staging area is the place where you group files together before you commit them to Git. Type of files are:
- staged (files are ready to be commited-added to the project)
- unstaged (files with changes that have not yet been prepared to be commited - added to the project)
- untracked (files not tracked by Git yet - need to be added)
- deleted (file has been deleted and is waiting to be removed from Git).

```bash
# make a file tracked
git add [filename]
# dot stands for current dir - add everything in and beneath
git add -A .
# with the * in “” git adds all the .txt files even in subdirectories
git add \*.txt
# remove files from staging area
git reset [filename]
# Commit is a snapshot of our repository.
git commit -m “name of snapshot”
```


**View the history of commits**

`git log`

**Making the changes available online**

In order to push a local repo to Git Server, we need to add a remote repository

```bash
# first do that to check if remote exists
git ls-remote
# it is good to name remotes as origin
git remote add origin [link]
# push to a default remote branch with name (with the -u flag Git remembers the params)
git push - u origin master
# to get locally the changes in the remote repo
git pull origin master
```

Sometimes we may want to pull first and then commit the changes
```bash
# run before pulling
git stash
# run that to commit changes after having pulled
git stash apply
```

When we pull from remote repo, some things will have changed. To see what is different from our last commit. Looks for changes at files that have already been staged. Note: the HEAD is the pointer that by default points to the most recent commit (it can be used as a quick way to reference that commit).

```bash
git diff HEAD
# use that to see the differences just staged
git diff --staged
```

**Difference between git clone and pull**

- git clone is how you get a local copy of an existing repository to work on. It's usually only used once for a given repository, unless you want to have multiple working copies of it around. (Or want to get a clean copy after messing up your local one...)
- git pull (or git fetch + git merge) is how you update that local copy with new commits from the remote repository. If you are collaborating with others, it is a command that you will run frequently.

**Removing files**

```bash
# To remove files (this way they are not only deleted but also removed from the working tree)
git rm [\*.txt]

# to recursively remove all files and folders from the current directory
git rm -r name_of_folder
```

### Branches

If you are working on a branch and you want to switch to a different one
```bash
git checkout [name of branch]
# goes back to the last commit of the file
git checkout -- octocat.txt
```

To work on a feature or a bug of the project, you create a separate branch and you make separate commits to it. When done you merge it back to the master branch (and then push it remotely).

```bash
# show local branches
git branch

# show all
git branch -a

# show only remote
git branch -r

# viewing branches sorted
git for-each-ref --sort=-committerdate refs/heads/

# create the branch and switch to it
git branch [name of branch]

# delete the branch
git branch -d [name of branch]
```

When we are on master branch and we want to merge another branch into it

`git merge [name of branch]`


## Pull request

Allows the project maintainers to make comments and review any changes you have made locally before you merge and then push them to remote

## Submodules

**Add a new submodule in existing repo**

`git submodule add [url]`

**Cloning a project with submodules**

```bash
# first clone the project with the included submodules
git clone [main-project-url]

# change dir
cd [project-dir]

# initialize submodule config file
git submodule init

# fetch all data from submodule project
git submodule update

# alternativelly to automatically initialize and update each submodule in the repository
git clone --recursive [main-project-url]
```

**To commit changes in a submodule**

The submodule is its own repo/work-area, with its own .git directory. So:

``` bash
# first commit/push your submodule's changes

cd path/to/submodule
git checkout master
git add <stuff>
git commit -m "comment"
git push submodule_origin master

# then tell your main project to track the updated version

cd /main/project
git add path/to/submodule
git commit -m "updated my submodule"
git push origin master
```

## Git Resources

- https://git-scm.com
