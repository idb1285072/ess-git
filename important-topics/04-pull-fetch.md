## `git fetch` — Get Updates _Safely_

### What it does:

- Contacts the remote (e.g. `origin`).
- Updates the remote-tracking branches like `origin/main`, `origin/feature-x`.
- Does **not** touch your local branches or working directory.

### Example:

```bash
git fetch origin
```

Now:

- Your local repo knows the newest commits on the server.
- You can inspect before merging:

  ```bash
  git log origin/main --oneline
  git diff main..origin/main
  ```

If you want to update your branch after fetching:

```bash
git merge origin/main
# or, for a cleaner history
git rebase origin/main
```

### Fetch a specific branch:

```bash
git fetch origin feature/login
```

This updates `origin/feature/login` locally, but doesn’t create or switch to a branch.

To work on it:

```bash
git switch --track origin/feature/login
```

---

## `git pull` — Fetch + Merge (or Rebase)

### What it does:

`git pull` = `git fetch` + `git merge` (or rebase, depending on config).

It:

1. Downloads remote changes.
2. Merges (or rebases) them into your current branch.
3. Updates your working directory immediately.

### Example:

```bash
git pull origin main
```

This will:

- Fetch new commits from `origin/main`
- Merge them into your current `main` branch.

If your repo is configured to rebase instead of merge:

```bash
git config --global pull.rebase true
```

Then:

```bash
git pull
```

will **fetch + rebase** instead of merge.

---

## Common Scenarios

### Update your local main

```bash
git switch main
git fetch origin
git merge origin/main
# or simply
git pull origin main
```

### Get a new remote branch

```bash
git fetch origin feature/login
git switch --track origin/feature/login
```

### Refresh all remote branches

```bash
git fetch --all --prune
```

- `--all`: fetch from all remotes
- `--prune`: remove deleted remote branches locally

## Command

```bash
git fetch origin # fetch the origin remote
git fetch origin feature/login # fetch specific branch
git pull # fetch + merge
```
