```bash
git checkout main
git merge feature/login # linear history if fast forward
git merge --no-ff feature/login # no fast forward. force a merge commit.
git merge -m "Merge login feature" feature/login # merge with commit message
```

for personal small projects use fast forward. for team `--no-ff` is better.

- merge remote branch into local
  ```bash
  git fetch origin
  git merge origin/feature/login
  ```

```bash
git log --oneline --graph --all
```
