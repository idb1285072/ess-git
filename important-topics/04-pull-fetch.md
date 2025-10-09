```bash
git fetch --all --prune
```

## Command

```bash
git fetch # = git fetch origin
# default remote = origin
git fetch origin # fetch the origin remote
git fetch upstream # fetch specific (the upstream) remote
git fetch origin feature/login # fetch specific branch
git fetch --all # fetch all remotes
```

```bash
git pull # fetch + merge
git pull origin main # pull origin remote and main branch
git pull --set-upstream origin feature/login #SET_TRACKING
```

```bash
git branch -vv #TRACKING OR UPSTREAM
```

**Note**:

- `git fetch` = `git fetch origin` if default remote = origin
- `git pull` = `git pull origin main` if current branch = main and tracking origin/main

---

#### Tracking vs Upstream

- **main** is tracking **origin/main**.
- **origin/main** is the upstream for **main**.

---

# Summary

Use,

```bash
# first time
git checkout main
git pull --set-upstream origin main
# then
git checkout main
git pull
```

or,

```bash
# everytime
git checkout main
git pull origin main
```

Use,

```bash
git fetch origin # fetch all branches (recomended and common)
git fetch origin main # fetch only main branch (faster)

git checkout main
git merge origin/main
#OR,
git checkout feature/my-feature
git merge origin main
```
