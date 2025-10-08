## What “Cloning” Means in Git

When you **clone** a project from GitHub (or any Git repository), you are:

1. **Copying the entire repository** — not just the files, but the entire history (all commits, branches, tags, etc.).
2. Creating a **local repository** on your computer that is connected to the **remote repository** on GitHub.
3. Git then sets up a link (called a **remote**, usually named `origin`) to the original repo so you can **fetch**, **pull**, and **push** changes later.

So cloning = downloading + linking.

---

## Command

```bash
git clone https://github.com/username/repository.git
```

Git does the following under the hood:

1. **Creates a new folder** with the same name as the repo.
2. **Initializes** a new `.git` folder (this is your local Git database).
3. **Downloads all objects and refs** (commits, branches, tags).
4. **Checks out** the default branch (usually `main` or `master`).
5. **Sets the remote** named `origin` to the GitHub URL.

### Check Remote Connection

```bash
git remote -v
```

You’ll see something like:

```bash
origin  https://github.com/username/repository.git (fetch)
origin  https://github.com/username/repository.git (push)
```

This means your local repo is linked to the GitHub repo.

---

### Verify Branches

```bash
git branch -a
```

- `* main` — current branch.
- `remotes/origin/main` — remote branch.

If you want to switch branches:

```bash
git checkout branch_name
```

---

## Shallow Cloning (Faster Option)

If you only want the latest version (not the full history), use:

```bash
git clone --depth 1 https://github.com/username/repository.git
```

