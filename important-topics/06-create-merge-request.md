## PUSH feature BRANCH

```bash
git checkout feature/login
git push origin feature/login
```

## Go to Git Hosting Platform (GitHub, GitLab)

- Navigate to the repo
- find `Create merge request`

Here’s a clear, step-by-step guide to **create a Merge Request (MR)** — perfect for GitLab or similar platforms. Straight to the point, Murad:

---

### Click `Create Merge Request`

- Source branch: `feature/your-branch-name`
- Target branch: usually `main` or `develop`

---

### Fill in MR Details

- **Title**: Clear and descriptive
- **Description**: What this MR does, why it matters
- **Assign reviewers**: If needed
- **Labels**: Bug, feature, etc.

---

### Review Changes

- Check diffs, commits, and CI status

---

### Submit the Merge Request

- Click **“Submit”** or **“Create Merge Request”**

---

### Monitor & Respond

- Address comments
- Push updates if needed:
  ```bash
  git commit -m "Fix review feedback"
  git push
  ```
