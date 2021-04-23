# Git Cheat Sheet
## Concepts
* `master` Name of the default branch, similar to SVN's trunk.
* `HEAD` The "current branch". E.g. after 'git checkout' HEAD revision changes to point to the tip.of the branch. 
* Ancestry References
   * `^` Parent of that commit. E.g. `git show HEAD^` to show parent of HEAD or `git show d921970^2` means the second parent of d921970.


## Global Git Configuration

```bash
# cache credentials for a day
git config --global credential.helper "cache --timeout=86400"
# Store credentials for https:// (wincred for Windows, gnome-keyring for Linux, osxkeychain for Mac)
git config --global credential.helper wincred
# commits are signed by default
git config --global commit.gpgsign true
```

## Signing



### Undoing Changes

#### Undo Local Change

```bash
git checkout <file>
```

#### Undo Local Commit

```bash
git commit -m "Something terribly misguided" 
git reset --soft HEAD~
```

#### Undo git add

```bash
# remove file from about-to-be-commited index without changing anything else
git reset <file> 
# unstage all due changes
git reset
```


### Show the changes which have been staged

```bash
git diff --cached
```

## Workflows
### Simple Centralized Workflow
Everybody commits to `master` branch.

1. Clone a repository

   ```bash
   # automatically adds shortcut 'origin' back to parent repository
   git clone https://github.com/bitcoin/bitcoin.git
   ```

1. Make local changes

   ```bash
   git status
   git add <some files>
   git commit
   ```

1. Incorporate upstream changes

   ```bash
   # like SVN update: fetches changes and merges them.
   # --rebase: move all local commits to tip of master.
   #  Not strictly necessary, but removes superfluous “merge commit”
   git pull --rebase origin master
   ```

1. Push local `master` to central repository

   ```bash
   git push origin master
   ```

1. Resolve merge conflicts. Repeat until all conflicts resolved.

   ```bash
   # see where the problems are
   git status
   # Now edit files to your liking.
   git add <some files>
   git rebase --continue
   ```
Something bad happens? Go right back to before the pull with `git rebase --abort`

1. Publish features

   ```bash
   git push origin master
   ```



### Feature Branch Workflow
Create a new branch for every new feature. Each branch has a clear, highly focused purpose. Use descriptive names, like `animated-menu-items`. Feature branches should be pushed to the central repository.

1. Checkout a remote branch to begin working on a feature
   ```bash
   git branch -r # gives e.g. origin/feature/make-everything-better
   git checkout -b make-everything-better origin/feature/make-everything-better
   ```
   
1. Make local changes

   ```bash
   git status
   git add <some files>
   git commit
   ```

1. Push local feature branch `animated-menu-items` to central repository

   ```bash
   # -u adds upstream reference to the branch.
   # After that 'git pull' and 'git push' work on that branch.
   git push -u origin animated-menu-items
   ```

1. Make pull request: Let devs have a look at the branch, fix stuff until everybody is happy.
1. Merge the feature into `master`

   ```bash
   # Make sure we are operating on the branch 'master'
   git checkout master
   # make sure we are up to date!
   git pull
   # merge the branch
   git pull origin animated-menu-items
   # finally, push back updated master to origin
   git push
   ```



* [stackoverflow](http://stackoverflow.com/a/5343146/48181)
* [git-credential-store](https://git-scm.com/docs/git-credential-store)
* [centralized workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/centralized-workflow)
* [feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)
* [git-push](https://git-scm.com/docs/git-push)
* [head](http://stackoverflow.com/a/2304106/48181)
* [Ancestry](https://git-scm.com/book/en/v2/Git-Tools-Revision-Selection#Ancestry-References)
* [Undoing Changes](https://www.atlassian.com/git/tutorials/undoing-changes)
* [50 commands to know freecodecamp]( https://www.freecodecamp.org/news/git-cheat-sheet/)

Sources: [feature branch workflow], [git-push] , [Martinux]( https://github.com/martinus)

| Command               |    Use    |
| ------------------ | ----------- |
|`git push --delete origin <branch_name_here>`|`remove a remote branch in Git`|




# GIT Cheatsheet


## Git Configuration

`$ git config --global user.name "username"`

`$ git config --global user.email "email"`

`$ git config --list`


## Git Initializaion
`$ git clone <repo-url> <local-new-directory>` Clones the repository creating a new folder


#### Locally initialize and pull from remote repository
`$ git init` 

`$ git pull <repo-url>` "git fetch + git merge" - fetch and merge with the local file.


#### add, rename, remove, replace remote url
`$ git remote add <short-name> <url>`

`$ git remote rename <old-name> <new-name>`

`$ git remote remove <short-name>`

`$ git remote set-url <short-name> <new.git.url>`



## Stage changes to commit
`$ git add .`

`$ git add *`

`$ git add -all`

`$ git add -A` Stage all files including deleted ones

`$ git add <file-name>`

`$ git add *.<extension>` Supports regular expressions

## Renaming files
`$ git mv <old-name> <new-name>`


## Commit changes
`$ git commit -m "message"` usual message format - "C1:branch-name message"

`$ git commit --amend -m "message"` `--amend / -a` modify or replace last commit if not pushed

`$ git push origin <branch-name>`


## History
`$ git status` status of files

`$ git log` history of commits

`$ git log -p` history of commits with changes

`$ git log -p <number-of-logs>` certain number of commit history

`$ git diff`  shows the differences with previous commit


## Show names of changed files in a particular commit
`$ git show --pretty="" --name-only <commit-hash>`


## Branching 
`$ git branch <branch-name>` create new branch

`$ git checkout <branch-name>` moves HEAD to the branch

`$ git checkout -b <branch-name>` create and checkout at a time

`$ git checkout -` toggle with previous branch

`$ git branch` show local branches

`$ git branch -r` show remote branches

`$ git branch -a` show all branches

`$ git branch -v` show all branches along with last commit

`$ git branch -d <branch-name>` delete branch

`$ git branch -D <branch-name>` force delete branch

## Rename branch
`$ git branch -m <new-name>` rename current branch to <new-name>
 
`$ git branch -m <old-name> <new-name>` rename branch named <old-name> to <new-name> while in another branch
 

## Delete branch
`$ git push --delete <remote-name> <branch-name>` deleting remote branch - in most cases `remote` name is `origin`

`$ git branch -d <branch-name>` deleting local branch `-D` for force delete


#### Move branches using refs
`$ git checkout HEAD~2` only move head

`$ git branch -f master HEAD~3` move branch to third ancestor.



## Stashing 
`$ git stash save 'message'` save dirty works along with a message

`$ git stash list` shows the list of stash

`$ git stash apply` get back last stash

`$ git stash aplly stash@{1}` get second last stash

`$ git stash drop` remove the stash from the list

`$ git stash drop stash@{1}`

`$ git stash pop` get back the last stash & remove from the list


#### Unmodifying a Modified file
`$ git checkout --<file>` dangerous command :p. any changes made are completely gone. use with caution


## Reset branch
`$ git reset --<mode> HEAD~<number>` works in local - deletes history

mode : 
 - soft : commit is reset but files remain staged

 - hard : everything is deleted along with directory

 - mixed: files becomes unstaged


`$ git revert HEAD` works in both by commiting a new commit with invert of HEAD

`$ git revert <commit-hash>` same


## cherry-pick, merge, rebase
`$ git cherry-pick <hash1> <hash2> ...` copies commits with the provided hash and place it under current HEAD

`$ git merge <branch-name>` merge the provided branch with the current branch

`$ git rebase <branch-name>` merge the provided branch with the current branch in which provided branch-name is deleted as it never existed

`$ git rebase -i HEAD~<number>` interactive way - reorder or drop upto provided parent


## Tags

`$ git tag` show all tags

`$ git tag -a <tag name> -m "<tag message>"` annotated tag

`$ git tag <tag name>` lightweight tag

`$ git show <tag name>` show info about the tag

`$ git tag -a <tag name> <commit hash>` tag previous commit

`$ git push origin --tags` push all tags to remote

`$ git push origin <tag name>` push specific tag to remote

`$ git tag -d <tag name>` delete tag

`$ git push origin :refs/tags/<tag name>` update deletion in remote

`$ git checkout -b <branch name> <tag name>` to make change to a previous tag make a branch first


## Alias
It's like #define in C programming

`$ git config --global alias.ci commit`

`$ git config --global alias.last 'log -1 HEAD'` After this `git last` shows the log of last commit.








