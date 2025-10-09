## What “Cloning” Means in Git

When you **clone** a project from GitHub (or any Git repository), you are:

1. **Copying the entire repository** — not just the files, but the entire history (all commits, branches, tags, etc.).
2. Creating a **local repository** on your computer that is connected to the **remote repository** on GitHub.
3. Git then sets up a link (called a **remote**, usually named `origin`) to the original repo so you can **fetch**, **pull**, and **push** changes later.

So cloning = downloading + linking.

---

## Command

```bash
git clone https://github.com/username/repository.git folder_name #CLONE
git clone -b branch-name https://github.com/user/repo.git #CLONE Branch
git remote -v #check fetch and push
git remote show origin 
git clone --depth 1 https://github.com/username/repository.git #Shallow Cloning (faster) latest version not full history
```
