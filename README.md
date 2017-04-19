# Git Cheat Sheet

## Basic Commands

**Initialize git repo**

`git init`

**Clone existing repo**

If you want to get started with an existing repository, then you need to clone it:

```bash
# clone a repo
git clone [url]

# clone repo into specific directory
git clone https://github.com/libgit2/libgit2 mylibgit
```

**See project state.**

The main tool used to view the project state and the stage that the files are, is:

```bash
# view file status
git status

# view simplified output
git status -s
```

**Making changes**

The different states of the files in a git project are:

- **untracked**   are files not tracked by Git yet - need to be added
- **unstaged**    are files that are tracked by Git, but have changes that have not
                  yet been prepared to be commited
- **staged**      are files are ready to be commited
- **unmodified**  are files that have been commited. Once they are modified, their
                  status becomes unstaged.

<br/>
<img src="images/git-lifecycle.png">
<br/>

```bash
# track a new file
git add [filename]

# dot stands for current dir - add everything in and beneath
git add -A .

# with the * in “” git adds all the .txt files even in subdirectories
git add \*.txt

# remove files from staging area
git reset [filename]

# Commit is a snapshot of our repository - files are now unmodified
git commit -m “name of snapshot”

# goes back to the last commit of the file
git checkout -- octocat.txt

# If you made a small change and want to add it to the last commit, add it via
#git add, and run
git commit --amend
```

**Making the changes available online**

In order to push a local repo to Git Server, we need to add a remote repository

```bash
# view linked remote repos
git remote

# get verbose output
git remote -v

# add remote link - usually named as origin
git remote add origin [link]

# push to a online repo named origin on the master branch (with the -u flag Git
# remembers the params)
git push -u origin master

# to get locally the changes in the remote repo
git pull origin master
```

**Difference between git clone and pull**

- `git clone` is how you get a local copy of an existing repository to work on.
It's usually only used once for a given repository, unless you want to have multiple working copies of it around. (Or want to get a clean copy after messing up your
local one...)
- `git pull` (or `git fetch` + `git merge`) is how you update that local copy with
new commits from the remote repository. If you are collaborating with others, it
is a command that you will run frequently.

**Show file changes**

```bash
# view changes in a file from latest commit
git diff [filename]

# view changes in all files from latest commit (HEAD is pointer to most recent commit)
git diff HEAD

# view the differences that are staged for next commit
git diff --staged

# --staged and --cache are synonyms
git diff --cached
```

**Removing files**

```bash
# remove files (they are not only deleted but also removed from the working tree)
git rm [\*.txt]

# recursively remove all files and folders from the current directory
git rm -r name_of_folder
```

**View the history of commits**

`git log`

**Ignoring files**

Often you will want to prevent git from tracking files such as big size data sources.
To ignore them, list them in a .gitignore file.

```bash
# create .gitignore file
touch .gitignore

# add the files you want to ignore
echo 'data/*' > .gitignore
```


### Branches

To work on a feature or a bug of the project, you create a separate branch and
you make separate commits to it. When done you merge it back to the master branch
(and then push it remotely).

```bash
# show local branches
git branch

# show only remote
git branch -r

# show all (both remote and local)
git branch -a

# viewing branches sorted
git for-each-ref --sort=-committerdate refs/heads/

# create the branch and switch to it
git branch [name of branch]

# switch to a branch
git checkout [name of branch]

# delete the branch
git branch -d [name of branch]

# once in master branch merge the new feature
git merge [name of branch]
```


## Stashing

Sometimes, while in the middle of some uncommitted work, we may want to pull some
new changes or switch to a new branch without having to do a commit of half-done
work. Stashing takes the unfinished work and pushes it to a stack of unfinished
changes.

```bash
# run before pulling new work
git stash

# view stored stashes
git stash list

# apply the stashed worked
git stash apply

# apply an older stash
git stash apply stash@{1}

# once applied stashed work remove from stack
git stash drop
```


## Pull request

Allows the project maintainers to make comments and review any changes you have
made locally before you merge and then push them to remote


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

# alternativelly to automatically initialize and update each submodule in the
# repository
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

## Writing Good Commit Messages

Structure your commit message like this:

From: [http://git-scm.com/book/ch5-2.html](http://git-scm.com/book/ch5-2.html)

> ```
> Short (50 chars or less) summary of changes
>
> More detailed explanatory text, if necessary.  Wrap it to about 72
> characters or so.  In some contexts, the first line is treated as the
> subject of an email and the rest of the text as the body.  The blank
> line separating the summary from the body is critical (unless you omit
> the body entirely); tools like rebase can get confused if you run the
> two together.
>
> Further paragraphs come after blank lines.
>
>   - Bullet points are okay, too
>
>   - Typically a hyphen or asterisk is used for the bullet, preceded by a
>     single space, with blank lines in between, but conventions vary here
> ```

**The seven rules of a great Git commit message**

1. Separate subject from body with a blank line
2. Limit the subject line to 50 characters
3. Capitalize the subject line
4. Do not end the subject line with a period
5. Use the imperative mood in the subject line
6. Wrap the body at 72 characters
7. Use the body to explain what and why vs. how

## Git Resources

- https://git-scm.com

## References

- https://git-scm.com
- https://chris.beams.io/posts/git-commit/
