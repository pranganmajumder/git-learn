
# Git Command Basics

git branch -r   to see remote branch

git remote -v to see remote 

git remote add origin url   to add remote repo

git pull <repo-url>
ex : git pull origin git@github.com:pranganmajumder/git-learn.git master

to change last commit message (warning : you have to change it before push to remote branch)
git commit  ---amend -m <message>

git branch    to see the branch and pointed branch
git checkout <branch_name> go to the branch
git checkout - go to previous branch
git checkout -b <branch_name>   to build and checkout branch simultaneously
git add <file> track a new file and staged to be commited

git restore <file>  to discard changes in working directory/ file
git restore --staged <file>  to unstage/untrack a file before commit



Untracked basically means that Git sees a file you didn’t have in the previous snapshot (commit);

