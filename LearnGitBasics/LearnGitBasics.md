
Git Tutorial from Backlog
[Learn the Basics](https://backlog.com/git-tutorial/what-is-git/)

------

# The Git Workflow

A Git project has three components:

- repo
- working tree
- index (staging)

The repo is the container that tracks changes to your files.

The working tree, or working directory, are the files you are currently working on. 

The index is the staging area where commits are prepared. 

Summary of the Git workflow:
- modify a file
- stage the file
- commit the file


# Repositories

Two types of repos:
 - remote
 - local 

 A remote repository is hosted on a site like Github,
 A local repository is the repo on your computer.


 ## Creating a Repo

 There are two ways to create a repo:
- git init
- git clone

Use `git init` if you are creating a brand new repo on your local machine. 

Use `git clone` to copy a remote repo down to your computer.
- By default, `git clone` will set up a local master branch that tracks the remote master branch. 
- A cloned repo maintains the same history as the original repo it was cloned from. 



## Recording Changes

After modifying a file you can add it to the index/staging area but either  adding just the one file, adding all files using the ".", or by using the "-A" flag. 

```git
git add filename.html
git add .
git all -A
```

Once a file is added to the index, it can be committed. A commit is a snapshot of the entire repo at that moment in time.

```git
git commit 
```

This syntax will open the default editor so that you can add a message. Alternately, you can add the message at the same time you commit. 

```git 
git commit -m "Add filename.html to do stuff"
```

## Undoing Changes 

There are two ways to undo changes: 
- git revert
- git reset

The `git revert` command will undo a commit that has been pushed.

The `git reset` and `git rebase -i` commands can also be used but they cause the remote repo to become desynchronized with the local repo. 

Git reset can also discard commits that are no longer needed. There are three reset modes:
- mixed (default)
- soft
- hard 

Mixed mode restores the state of a changed index.
Soft mode undoes a previous commit. 
Hard mode removes all traces of a commit. 

| Mode Name | HEAD position | Index       | Working Tree |
| --------- | ------------- | ------------| -------------|
| soft       | change       | unchanged   | unchanged |
| mixed      | change       | change      | unchanged |
| hard       | change       | change      | change |



## Syncing Repos 

The three commands used for syncing your local repo with the remote repo are: 
- git push
- git pull 
- git merge

Git push - when you push, you are pushing you local changing up to the remote repository. 

Git pull - when you pull, you are pulling any changes on the remote repo down into your local repo. 

Git merge - If you try to push changes and get an error it's usually because there are changes in the remote repo that are not reflected in your local copy. To fix this, you need to merge the remote changes to your local repo. 

### Merge Conflict 

If Git cannot decide how to merge the two changes, it will throw an error so that you can make the changes manually in your text editor. 


## Rewriting History 

There are numerous ways to revise your *local* commit history. 

### Git commit --amend 

The `git commit --amend` command allows you to add files to the commit, or modify the commit message. 


### Git rebase 

Rebasing is the process of taking all the changes that were committed on one branch, and applying them to a new branch. 

Run `git rebase` and add in the `-i` option to rewrite, replace, delete, and merge individual commits in the history. You can also:

Rewrite a past commit message
Squash a group of commits together
Add files that have not been committed

### Git cherry pick 

You can apply an existing commit from another branch to the current branch within the repository by using the git cherry-pick command. Cherry-picking allows you to:

Move a commit that was committed to the wrong branch to the right branch.
Add a commit to the current branch based on an existing commit from another branch.

### Git merge --squash

Squashing is the process of merging multiple commits into a single commit.

If you run git merge and the --squash option, a new commit will group all of the commits from that branch together. The commit will be used to merge into the current branch.


# Learn Git Collaboration
[Learn Git Collaboration](https://backlog.com/git-tutorial/using-branches/)

## Branches 

Branching allows you to "branch out" from the original code and isolate their work. 

Branching enables you to isolate your work from others. Changes in the primary branch or other branches will not affect your branch, unless you decide to pull the latest changes from those branches.

It is a common practice to create a new branch for each task (i.e., a branch for bug fixing, a branch for new features, etc.). This method allows others to easily identify what changes to expect and also makes backtracking simple.

To create a branch, 

```bash
git branch branchname 
```

Switch between branches by using the `git checkout` command. Switching between branches is like switches between different work spaces. 

```bash 
git checkout branchname
```


## Git HEAD

HEAD is used to represent the current snapshot of a branch. For a new repository, Git will by default point HEAD to the master branch. Changing where HEAD is pointing will update your current active branch.

The ~(tilde) and ^(caret) symbols are used to point to a position relative to a specific commit. The symbols are used together with a commit reference, typically HEAD or a commit hash.

`~<n>` refers to the <n>th grandparent. 
`HEAD~1` refers to the commit's first parent. 
`HEAD~2` refers to the first parent of the commit's first parent.

`^<n>` refers to the the <n>th parent. 
`HEAD^1` refers to the commit's first parent. 
`HEAD^2` refers to the commit's second parent. A commit can have two parents in a merge commit.

## Git Stash

When you switch to another branch with uncommitted changes in your working tree, these uncommitted changes will also be carried to the new branch that you switch to. Changes that you commit will be committed to the new switched branch. 

However, if Git finds a conflict between the files from the newly switched branch and the uncommitted changes from the previous branch, you will not be allowed to switch to the other branch. You must commit or stash those changes first before switching branches.

You can think of stash as a drawer to store uncommitted changes temporarily. Stashing allows you to put aside the “dirty” changes in your working tree and continue working on other things in a different branch on a clean slate.

Uncommitted changes that are stored in the stash can be taken out and applied to the original branch and other branches as well.

## Remote Branches 

The remote branch is referred to as `origin/master`.
Your local branch is referred to as just `origin`.

### Fast-forward Commit

When the remote copy, origin/master, is ahead of your local repo, and you have not yet made any changes to your local repo that are not yet in the cloud, then when you run `git pull` it will do a fast-forward merge into your repo. 
In other words, your repo will "fast-forward" to get caught up with the remote repo's changes. 

### Pull

However, if you have local changes that you have not pushed up yet, and you need to pull down changes, Git will try to merge the remote changes into your local repo. 



**Git will always attempt a merge when you use `git pull`.Git must merge and commit before a pull if local branch is different from the remote branch.**

If there are any conflicts between the two branches, you will need to resolve those manually.

Use `git pull` to pull down any changes from the remote repo.

## Git Fetch 

Similar to `git pull`, the `git fetch` command will pull down any changes on the remote repo, but will not attempt to merge them into your local repo. 

Once changes are fetched, you can merge them in by merging FETCH_HEAD or but using `git pull`.

## Push Branch to Remote 

All of your commits are available to you until you push your local branch to the remote repository. That is, you can work on your own local branch at your own pace without affecting other members of the team.

When you push your local branch to remote, Git will do a fast-forward merge to the destination repository.

However, if the push results in a non-fast-forward merge, Git will decline your push to prevent you from overwriting previous commits. In that case, you have to pull the latest remote changes and push again.

## Branching Workflows

A workflow consists of five types of branches:
- master 
- feature, or topic, branch
- release branch
- hotfix branch
- develop branch

### Master Branch

The master, or main, branch is created automatically when you create a repo. 

All commits go under the master branch unless you specifically switch over to a different branch first. 

Codebase residing in the master branch is considered to be production-ready. When it is ready for a specific release, the latest commit will be given a release tag.

### Feature Branch

When you start working on a new feature/bug fix, you should create a feature/topic branch. A feature/topic branch is normally created off a develop/integration branch. This feature/topic branch can reside in your local machine throughout the entire development lifecycle of the feature.

You will push this branch to the remote repository whenever you are ready to merge the change set with the develop/integration branch.


### Release Branch

When you roll out a new release, you create a release branch. A release branch helps you to ensure that the new features are running correctly.


### Hotfix Branch

When you need to add an important fix to your production codebase quickly, you can create a Hotfix branch off the master branch.



### Develop Branch

...

## Rebase 

The `git rebase` command is an alternate to `git merge`. When using rebase, the branches are merged together and the commits  from the secondary branch are appended to the end of the master branch. 

A rebase does not move the position of the master. In any case, you will be able to do a fast-forward or a clean merge from bugfix to master after rebasing.

## Tags 

Tags are often used to indicate release versions. There are two types of tags:
- lightweight tag
- annotated tag 

A lightweight tag is similar to a branch that does not change. It just points directly to a specific commit in the history. Lightweight tags are mainly used temporarily in your local workspace.

An annotated tag is checksummed and often used when you are planning to mark an important commit. You can add comments, a signature, the date, plus the tagger's name and e-mail.

## Pull Requests

A pull request notifies other development team members of changes made in your local repository. Pull requests provide the following functions:

- Notify team members when a review or merge of work is needed
- Display changes made to source code in an easy-to-understand manner
- Provide a platform for communicating about source code


### Development process with pull requests
Here is a simple development workflow with pull requests your team can follow:

- [Developer] Clone or pull the source of the work target.
- [Developer] Create a branch for the work.
- [Developer] Perform development work such as adding and modifying functions.
- [Developer] Push after the task is completed.
- [Developer] Create a pull request.
- [Review / Merge Personnel] Check the changes from the notified pull request and review.
- [Review / Merge Personnel] Judge the work and send a feedback to the developer if necessary.
- [Review / Merge Personnel] Merge if there is no problem as a result of the review.
- [Review / Merge Personnel] Close if the pull request itself becomes unnecessary as a result of the review.



# Work with Git 
[Work with Git](https://backlog.com/git-tutorial/getting-started/install-git/)


Set your global username and email. 

```bash
git config --global user.name "My Name"
git config --global user.email "me@mail.com"
```

Set Git output color.

```bash
git config --global color.ui auto
```

Create aliases for git commands.
This creates an alias of `co` to stand for `checkout`.

```bash
git config --global alias.co checkout
```


## Remote Repos

You can create an alias for your remote repo so that you don't need to type out it's full name every time you push to it.

By default, the remote repo will have an alias of origin. 


If you're starting with an empty repo on Github, and you're not using the clone command, you need to set the path of the remote repo.

```bash
git remote add origin path-to-your-github-repo.git
```

To push to a remote repo:

```bash
git push -u origin master
```
Think of it as push *to* origin *from* the master branch. 





