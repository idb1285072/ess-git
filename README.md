git -> version control system
track and manage changes to files over time

what is git?
history and naming?
who use
git vs GitHub?

```bash
git init
git status

git add file1 file2 -> stage
git add .
git commit -m 'message' -> commit
git log
```

# Topics

- Cloning Project
- Create new Branch
- Stash, Add, Commit and Push
- Pull and Fetch Remote Branch
- Merge Branches
- Create Merge Request
- .gitignore and Git Hooks
- Interactive Rebase (Intro)
- Merge Conflict Resolution

---

- clone

```bash
git clone URL
```

- Create branch

```bash
git branch branch_name #CREATE
git checkout branch_name #NAVIGATE
git checkout -b branch_name #CREATE & NAVIGATE
```

- Code, Add, Commit
- Before Merge must Update main

```bash
git fetch origin
git checkout main
git pull origin main
git checkout main
git merge my_branch
```

- push to GitHub my_branch

```bash
git push origin branch_name
```

- Create Pull Request
- Code Review + feedback
  - Solve Problems, add, commit, push
- Approve = old branch delete + pull updated main

---

Switch remote branch

```bash
git fetch origin #fetch all remote branch
git branch -r #see exiting remote branches
git checkout -b feature/login-page origin/feature/login-page
git switch -t origin/feature/login-page #new syntax
```

b