
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

```git 
git branch branchname 
```

Switch between branches by using the `git checkout` command. Switching between branches is like switches between different work spaces. 


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