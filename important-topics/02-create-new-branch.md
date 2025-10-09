## What is a branch (short & precise)

A **branch** is just a **named pointer** to a commit. Creating a branch means creating a new pointer that you can move forward (by committing) without changing other branches. Branches are extremely cheap because they’re just refs (small files) in `.git`.

## Command

```bash
git switch -c feature/123-add-login # Create & switch to new branch
git checkout -b feature/123-add-login # or (older / widely shown)
```

What happens:

- Git creates `.git/refs/heads/feature/123-add-login` with current commit SHA.
- `HEAD` is updated to point to that ref.
- Your working tree stays the same; new commits move that branch forward.

---

Each commit advances the branch pointer.

---

## Push the new branch to GitHub (create remote branch and set tracking)

To push and set the upstream (so `git pull` / `git push` work without extra args):

```bash
git push -u origin feature/123-add-login
```

- This creates `origin/feature/123-add-login` on GitHub.
- `-u` / `--set-upstream` configures your local branch to track that remote branch.

Check status & tracking:

```bash
git branch -vv
```

---

## Create a branch on GitHub (UI) and check it out locally

On GitHub: open repo → branch dropdown → type new name → press Enter/Create branch.

Locally:

```bash
git fetch origin
git switch --track origin/<branch-name>
# or
git checkout --track origin/<branch-name>
```

That creates a local branch that tracks the remote branch.

---

## Common workflows (practical)

### Feature branch workflow (common, simple)

1. Start from main:

   ```bash
   git fetch origin
   git checkout main
   git pull
   git checkout -b feature/ID-description
   ```

2. Work & commit.
3. Push:

   ```bash
   git push -u origin feature/ID-description
   ```

4. Open a Pull Request on GitHub from `feature/ID-description` → `main`.
5. After merge: delete branch locally & remotely.

---

## Updating your branch with upstream changes

Two main approaches:

**A — Merge from main into feature (safe, preserves history)**:

```bash
git fetch origin
git switch feature/123
git merge origin/main
# resolve conflicts if any, commit merge
```

**B — Rebase onto main (linear history, rewrites commits)**:

```bash
git fetch origin
git switch feature/123
git rebase origin/main
# resolve conflicts if asked, then:
git rebase --continue
# afterwards, if branch was pushed earlier, push with:
git push --force-with-lease
```

**Rule of thumb:** Rebase local / private branches; avoid rebasing branches others use (or coordinate).

---

## Merging a PR (on GitHub) — effects explained

GitHub merge options typically:

- **Create a merge commit** — preserves full history, creates one merge commit.
- **Squash and merge** — combines the PR commits into a single commit on the base branch.
- **Rebase and merge** — reapplies commits onto the base branch, producing a linear history.

Which to use depends on team policy.

---

## Deleting branches (cleanup)

After merge:

Locally:

```bash
git branch -d feature/123-add-login    # only deletes if merged
git branch -D feature/123-add-login    # force delete
```

Remote:

```bash
git push origin --delete feature/123-add-login
# or older syntax:
git push origin :feature/123-add-login
```

Prune stale remote-tracking branches locally:

```bash
git fetch --prune
# or
git remote prune origin
```

---

## Recovering deleted branch or lost commits

If you delete a branch but the commits are still referenced in reflog:

```bash
git reflog
# find SHA of last commit on branch
git checkout -b recovered-branch <sha>
```

`git reflog` is your friend — it tracks local HEAD movements.

---

## Advanced / internal bits (short)

- Branch = file with a commit SHA in `.git/refs/heads/`
- `HEAD` is typically `ref: refs/heads/main` — it points to the current branch ref.
- Remote-tracking branch `origin/main` is updated by `git fetch`.
- `git fetch` updates refs but doesn't change working tree; `git pull` = `fetch` + `merge` (or `rebase` if configured).
- Detached HEAD: `git checkout <sha>` — creates no branch; create one with `git switch -c name`.

Useful plumbing commands:

```bash
git show-ref      # list refs
git log --graph --oneline --decorate --all  # view branches & history
```

---

## Quick command cheat-sheet

```bash
# create & switch (local)
git switch -c my-branch
# or
git checkout -b my-branch

# push & set upstream
git push -u origin my-branch

# switch to remote branch that already exists
git fetch origin
git switch --track origin/my-branch

# update branch from main
git fetch origin
git merge origin/main      # or git rebase origin/main

# delete branch local & remote
git branch -d my-branch
git push origin --delete my-branch

# show branches
git branch -a
git branch -vv
```

---

## Quick best-practices summary

- Always branch from the correct base (main/develop).
- Name branches clearly (`type/ID-short-desc`).
- Push early — makes PRs and collaboration easier.
- Prefer `--force-with-lease` if you must force-push.
- Use PRs for code review; choose merge strategy per team.
- Clean up merged branches regularly.

## Command

```bash
git branch branchName # create a new branch
git checkout branchName # switch to an exiting branch
git switch branchName # switch to an exiting branch (modern)
git checkout -b branchName # create and switch to a new branch
git switch -c branchName # create and switch to a new branch (modern)

git branch # list all local branches
git branch -r # list remote branches
git branch -a # list all branches (local + remote)
git status # show current branch and changes

git branch -d branchName # delete a branch (safe: only if merged)
git branch -D branchName # force delete a branch (only if not merged)
git push origin --delete branchName # delete a remote branch
```
