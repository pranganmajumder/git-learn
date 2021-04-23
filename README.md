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






