## Command

```bash
# CREATE and SWITCH
git branch branchName # create a new branch
git checkout branchName # switch to an exiting branch
git switch branchName # switch to an exiting branch (modern)
git checkout -b branchName # create and switch to a new branch
git switch -c branchName # create and switch to a new branch (modern)

# LOG
git branch # list all local branches
git branch -r # list remote branches
git branch -a # list all branches (local + remote)
git branch -vv
git status # show current branch and changes
git log --oneline --graph --decorate --all # branch history
git show-ref # branch ref
git reflog # commit ref

# EDIT and DELETE
git branch -d branchName # delete a branch (safe: only if merged)
git branch -D branchName # force delete a branch (even if not merged)
git push origin --delete branchName # delete a remote branch
git push origin :feature/123-add-login # delete a remote branch (old syntax)
git branch -m oldName newName #RENAME

git push -u origin branchName # push new branch to remote --set-upstream
git push origin branchName # push new branch to remote
```

# Switch remote branch

```bash
git fetch origin #fetch all remote branch
git branch -r #see exiting remote branches
git checkout -b feature/login-page origin/feature/login-page
git switch -t origin/feature/login-page #new syntax
git switch --track origin/feature/login-page #new syntax
```

TODO

## Recovering deleted branch or lost commits

If you delete a branch but the commits are still referenced in reflog:

```bash
git reflog
# find SHA of last commit on branch
git checkout -b recovered-branch <sha>
```

`git reflog` is your friend — it tracks local HEAD movements.
