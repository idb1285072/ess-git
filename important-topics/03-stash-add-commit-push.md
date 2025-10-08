# Big picture: three Git areas

Before we dive into commands, keep this in your head:

- **Working directory (worktree)** — the files you edit.
- **Staging area (index)** — where `git add` places the snapshot that will become the next commit.
- **Repository (HEAD / refs / objects)** — saved commits and history.

`git add` moves things from worktree → index.
`git commit` turns the index → commit (in `.git/objects`) and moves a branch pointer.
`git push` publishes commits from your local repo to a remote (e.g., GitHub).
`git stash` temporarily records (saves) worktree + index state so you can get back to a clean working state.

---

# Stash

**What it does:**
Saves your _uncommitted_ changes (staged and unstaged) away so you can get to a clean working tree to switch branches, pull, run tests, etc.

**When to use:**
You’ve started work, need to switch branches quickly, don’t want to commit WIP to the current branch.

**Core commands & behavior**

```bash
# save working changes (staged + unstaged)
git stash push -m "WIP: start login form"

# include untracked files too:
git stash push -u -m "WIP: include untracked files"

# list stashes
git stash list

# view stash diff
git stash show -p stash@{0}

# apply stash but keep it in stash list
git stash apply stash@{0}

# apply and remove from stash (pop)
git stash pop stash@{0}

# create a new branch and apply stash to it (handy)
git stash branch feature/from-stash stash@{0}

# drop or clear
git stash drop stash@{0}
git stash clear
```

**Internals (conceptual):**

- Stash entries are stored in the repo under `refs/stash` (a stack). A stash entry records the **index state** and the **working tree state**; if you include untracked files `-u`, Git stores them as an extra object/commit linked to the stash entry.
- `stash@{0}` is the most recent stash, `stash@{1}` next, etc.

**Practical tip:**
Prefer `git stash push -m "..."` (modern) over the older `git stash save`.

**Common pitfalls**

- `git stash pop` may produce conflicts; resolve like normal merges (`git add` resolved files, then `git reset`? — but usually you `git add` and continue).
- Don’t rely on stash as long-term storage — treat it as temporary. Use a branch for longer WIP (`git stash branch ...` to move stash into a branch).

---

# Add — staging changes


```bash
git add path/to/file
git add .
# stage all changes in the entire repo (including deletions)
git add -A   # recommended when you want everything staged

# stage tracked files that are modified or deleted (no new files)
git add -u

# interactive patch mode (choose hunks)
git add -p

# intent-to-add a new file (record it in index so `git diff --staged` shows a placeholder)
git add -N newfile

# unstage a file (modern)
git restore --staged path/to/file
# or older:
git reset HEAD path/to/file
```

---

# Commit

```bash
# commit staged changes
git commit -m "Short subject line"

# amend last commit (rewrite history)
git commit --amend -m "New message and include newly staged changes"

# sign commit with GPG
git commit -S -m "Signed commit"

# show what will be committed
git diff --staged    # differences between index and HEAD (what commit will contain)
git diff             # differences between worktree and index (what's not staged)
```

**Good commit message style**

- 50-character subject, present imperative: e.g., `Add login validation`
- Blank line
- Body explaining the _why_ and any non-obvious details, wrapped at ~72 chars
- Reference issue IDs or coauthors in trailers when needed

**Amending vs new commit**

- `--amend` replaces the last commit (creates new commit object). If you already pushed the original, you must force-push; prefer not to amend public commits.

**Undoing a commit**

- Keep changes but undo commit:

  - `git reset --soft HEAD^` → moves HEAD back but keeps index as-is (so you can re-commit).

- Uncommit and unstage:

  - `git reset --mixed HEAD^` (default) → keep worktree changes, remove from index.

- Discard commit entirely:

  - `git reset --hard HEAD^` — **dangerous** (data loss if not backed up).

**Important checks**

- `git log --oneline --graph --decorate` to inspect history.
- `git show HEAD` to inspect the most recent commit.

---

# Push — publish commits to GitHub (remote)


```bash
# push the current branch to 'origin' and set upstream (first time)
git push -u origin my-branch

# push a specific branch
git push origin my-branch

# push all branches
git push --all origin

# force update (be careful)
git push --force-with-lease origin my-branch
# safer than --force because it refuses if remote advanced unexpectedly
```

**Publishing a new branch to GitHub**
When you `git push -u origin feature/xyz`, GitHub will create the remote branch. You can then open a PR on GitHub.

**Recovery: if you accidentally forced something**

- Use `git reflog` locally to find lost commits and recover them (`git checkout -b recover <sha>`).
- If remote has been force-pushed and you need to restore remote state, coordinate with team (someone who has the desired commit can re-push).

---

# Putting it together — example real-world flow

Scenario: you’ve modified files, want to stash, then later stage, commit and push.

```bash
# see status
git status

# temporarily stash local changes to switch branch
git stash push -m "WIP: form layout"   # stash staged+unstaged
git switch main
git pull origin main

# return to feature branch
git switch feature/login
git stash pop   # or git stash apply stash@{0}
# resolve conflicts if any, then:
git add -p     # stage logical hunks
git commit -m "Add login form and client-side validation"

# push to GitHub and set upstream
git push -u origin feature/login
```

If you wanted to convert stash to a branch directly:

```bash
git stash branch feature/from-stash stash@{0}
# that creates feature/from-stash at the commit you stashed from, applies stash, and removes the stash
```

---

# Short cheat sheet

```bash
# stash
git stash push -m "msg"
git stash list
git stash apply|pop stash@{0}
git stash branch new-branch stash@{0}

# add
git add file
git add -p
git add -A
git restore --staged file

# commit
git commit -m "Subject"
git commit --amend
git commit -S

# push
git push -u origin branch
git push --force-with-lease origin branch
```
