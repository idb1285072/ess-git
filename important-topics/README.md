## Update Your Local Repo

Keep your main branch up-to-date before merging anything.

```bash
git fetch origin
git checkout main
git pull origin main
```

- `git fetch origin` → downloads latest commits from remote.
- `git pull origin main` → merges remote `main` into your local one.

---

## Merge a Feature Branch into Main

Once your feature branch is complete and tested:

```bash
git checkout main
git pull origin main
git merge feature/branch-name
```

- Brings all commits from `feature/branch-name` into `main`.
- If no conflicts → automatic merge commit is created.

---

## Force a Merge Commit (Keep History Clean)

Even if a fast-forward is possible, create a merge commit so your feature stays identifiable.

```bash
git merge --no-ff feature/branch-name -m "Merge feature/branch-name into main"
```

- `--no-ff` forces a merge commit instead of just moving the branch pointer.
- Commonly used in **team workflows** to preserve feature boundaries.

---

## Squash Merge (Clean History)

Combine all commits from the feature branch into one commit on `main`.

```bash
git merge --squash feature/branch-name
git commit -m "Add login functionality (squashed)"
```

- Keeps `main` history neat with one logical commit per feature.
- Common in teams that prefer **linear history**.

---

## Abort or Cancel a Merge

If conflicts or problems occur and you want to undo a merge in progress:

```bash
git merge --abort
```

- Restores your working directory to the state before the merge started.

---

## Resolve Conflicts

When Git can’t auto-merge, you’ll see conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).

After fixing them manually:

```bash
git add conflicted-file.js
git commit
```

- Marks conflicts as resolved and finalizes the merge.

---

## Choose Whose Changes to Keep

If conflicts arise and you want to automatically prefer one side:

```bash
git checkout --ours path/to/file     # Keep current branch version
git checkout --theirs path/to/file   # Keep incoming branch version
git add path/to/file
```

---

## Merge with Strategy Options

To auto-resolve certain conflict types:

```bash
git merge -X ours feature/branch-name
git merge -X theirs feature/branch-name
```

- `-X ours` → prefer your branch’s changes when conflicts happen.
- `-X theirs` → prefer the other branch’s changes.

---

## Merge from Remote Branch

If the remote branch exists but not locally:

```bash
git fetch origin feature/branch-name
git merge origin/feature/branch-name
```

- Merges directly from the remote-tracking branch.

---

## Revert a Merge Commit

Undo a previous merge while keeping history clean:

```bash
git revert -m 1 <merge-commit-sha>
```

- `-m 1` keeps the first parent (usually your main branch).

---

## Clean Up After Merge

After merging a feature branch successfully:

```bash
git branch -d feature/branch-name
git push origin --delete feature/branch-name
```

- Removes the local and remote feature branches.

---

## Helpful Merge Visualization & Inspection

Check what you’re merging before doing it:

```bash
git log --oneline main..feature/branch-name
git diff main..feature/branch-name
git log --graph --oneline --decorate --all
```

- Lets you review commits and changes to avoid mistakes.

---

## Configure Default Merge Style

Some teams prefer merges, others rebases. Configure your behavior:

```bash
git config --global pull.rebase false   # always merge when pulling
git config --global pull.rebase true    # rebase instead of merge
```

---

## Typical Team Merge Workflow Example

```bash
# 1. Get latest main
git checkout main
git pull origin main

# 2. Merge feature branch
git merge --no-ff feature/login-page

# 3. Resolve any conflicts
# (edit, git add, git commit)

# 4. Push merged result
git push origin main

# 5. Clean up
git branch -d feature/login-page
git push origin --delete feature/login-page
```

---

| Command                             | Purpose                           |
| ----------------------------------- | --------------------------------- |
| `git merge branch`                  | Merge another branch into current |
| `git merge --no-ff branch`          | Always create a merge commit      |
| `git merge --squash branch`         | Combine commits into one          |
| `git merge --abort`                 | Cancel a merge in progress        |
| `git merge -X ours/theirs`          | Auto-resolve conflicts            |
| `git revert -m 1 <sha>`             | Undo a merge commit               |
| `git checkout --ours/theirs file`   | Resolve conflict manually         |
| `git branch -d <branch>`            | Delete merged local branch        |
| `git push origin --delete <branch>` | Delete merged remote branch       |
