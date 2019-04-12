Guide to git and GitHub in the Schwilk lab
==========================================

In the Schwilk lab, we use [git][git] for version control of data and code with central repositories hosted on [GitHub][github] under the  [schwilkab organization account][schwilklab]. 

Students can also have individual github accounts and set up their repositories under those. In that case, the owner can add the rest of the lab as collaborators on github and designate read or read/write access.

## Using git branches for lab collaboration ##

We use a shared repository workflow. Although that means everyone has the ability to push to the master branch, in general, only the owner/originator of that repository should push directly to master.  Others should instead work in what we call a "private branch" or a "feature branch". Anyone can still push to these branches, but if the creator of the branch names it so that the branch name begins with their name or GitHub ID, then that tells us that is a "private" branch.  The rest of us can read it, clone it, and  pull from it, but only the branch creator is allowed to push to it. This means that the branch "owner" is free to rebase, squash commits, and otherwise rewrite commit history and then do a force push.


Here are some outside references on this style of workflow:

- https://guides.github.com/introduction/flow/
- https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow

Below is a quick reference guide for basic steps involved in our "private branch" workflow. I'll use the [skyisland-climate repository][skyisland-climate] as an example with an example private branch, schwilk-testbranch.

### Set up local copy of the repo ###

```bash

# get local clone of repository (I use ssh, you may use https)
git clone git@github.com:schwilklab/skyisland-climate.git

# move to "root" folder of repo
cd  skyisland-climate

# list branches available (local and remote):
git branch -a 
```

### Create or move to a "private" branch for work ###

#### create new branch with "master" as the parent ####

```bash
# make sure you are in master (git status) or switch to master: git checkout master
# create branch and switch to it in one step:
# git checkout -b [name_of_your_new_branch], eg:

git checkout -b schwilk-testbranch
```

#### If the branch already exists ####

``` bash
git checkout schwilk-testbranch
```

#### What is a detached head state? ####

NOTE: the detached head state happens when you are in a local branch such as master, and check out a *different branch* from a remote. For example, you are in local/master and checkout origin/newbranch. You now need to make a branch called newbranch (or something else) and set up tracking with origin/newbranch.

### Typical private branch workflow ###

#### Before writing new code ####

```bash
# a new day, starting some work, so first, let's make sure our master is up to date with 
# origin (schwilklab/skyisland-climate on github):
git checkout master
git fetch
git merge
# the previous two commands can be combined as git pull 

# Note any changes, look at commits maybe inspect diffs if you want, then switch to 
# your private branch:
git checkout schwilk-testbranch

# optional: bring in changes from master
git merge master 

# or, if you want to "replay" these on your current branch:
git rebase master
```

#### Committing your new code ####

Writing nicely formatted commit messages is easier with a default editor named in your global gitconfig, or through rstudio, emacs, or other interface. 

I'll show how to do this using the command line, but these really common commands are worth accessing through a keyboard shortcut interface, editor, etc.

```bash
# make some changes then check what you have changed
git diff
# or 
git diff [filename]

# then, if satisfied, stage them using git add
git add [modifed file]

# or, to stage all changes in the working directory including deleted files:
git add -A 

# other variants for staging:
git add .   # stages new and modified, without deleted
git add -u # stages modified and deleted, without new

# Check what you have staged before  you commit!
git status
# maybe check a diff to be sure:
git diff --staged

# now commit those staged changes or check and unstage if you made a mistake
git commit # will open up an editor

# to just give a one liner commit message (not good form!):
# git commit -m"Commit message"
```
##### Interactively commit only portions of a changed file #####

Consider also that interactively selecting hunks to commit can be very useful if you've made a bunch of changes and want to commit them as separate commits. This happens a lot: I update some data in one file, then write some related code editing two files, then fix an unrelated typo in a fourth file.  These really should be three separate commits. THese are easy to commit separately if every change is in a separate file but if you want to make two commits out of changes to one file, then you need to be able to commit individual "hunks". 

see `git commit --interactive` and `git commit --patch` (which is shortcut to patch option in interactive commit).


##### Some notes on commit messages: #####

Commit messages have two parts: a first line (50 chars or less), and a body (wrap at 79 chars to be nice).  Some discussion of writing good messages: 
- http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
- http://chris.beams.io/posts/git-commit/

If the commit fixes a github issue include something like "fixes #8" in the commit

#### Pushing commits to the central repository so others can see them ####

Our central repository is usually hosted at github

Push with some frequency.  You don't need to push as often as you commit, but if you are working in a private branch, there is little cost: we can always fix things if you push something messy or even rewrite commit messages, squash commits etc.  Our rule in the lab is if a branch begins with your name or github username, then no one else should push to it. Others can merge from it into their own branches, but should not push to yours.

``` bash

# You've committed changes and the repo is clean, lets check:
git status # we want to see "working directory clean"

# ok, so let's push
git push # THIS WONT WORK THE FIRST TIME

# you'll get an error because git does not know where to push this, not what
# remote, no what branch on that remote. But git will tell you what to do:

git push --set-upstream origin schwilk-testbranch
# next time, a simple "git push" will work
```

#### Pull requests and merging####

We can merge our schwilk-testbranch branch in in one of two ways: 
1. through the GitHub interface (merge happens on github server copy of repo) or
2. By switching to master, and doing `merge schwilk-testbranch`, and then pushing the result.

Regardless of how we actually do the merge, since we use github, go ahead and open up a pull request first through the github interface. See https://help.github.com/articles/using-pull-requests/ The "base branch" would be master and the "head branch" would be schwilk-testbranch.


[git]: https://git-scm.com/
[github]: https://github.com/
[schwilklab]: https://github.com/schwilklab
[skyisland-climate]: https://github.com/schwilklab/skyisland-climate
