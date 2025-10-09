## CLONE

```bash
git clone URL
```

## NEW BRANCH

```bash
git checkout -b feature/my-feature
```

## WORK on the BRANCH

```bash
git add .
git commit -m "feat: add login form"
```

---

## UP-TO-DATE BRANCH

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

**When to use:**

- Before merging/rebasing your branch
- To see if the remote main branch has new changes

**Why:** Fetching lets you check remote updates **without touching your current branch**.

---

**When to use:**

- Regularly on `main` to stay synced with the team
- Before merging main into your feature branch

**Why:** Ensures your work is based on the latest main branch — reduces merge conflicts.

## PUSH feature BRANCH

So,

```bash
# frist time
git checkout feature/login
git push -u origin feature/login

# then
git checkout feature/login
git push
```

or,

```bash
# always
git checkout feature/login
git push origin feature/login
```

---

## OPEN a PULL REQUEST

- Use GitHub/GitLab/Bitbucket to merge your feature branch into `main`.

---

### Recommended sequence when contributing

1. `git checkout main`
2. `git pull` → make sure local main is up-to-date
3. `git checkout -b feature/my-feature`
4. Work + commit on your feature branch
5. Periodically:

   - `git fetch origin` → see if main has updates
   - `git merge origin/main` or `git rebase origin/main` → integrate latest changes

6. `git push -u origin feature/my-feature` → open pull request
