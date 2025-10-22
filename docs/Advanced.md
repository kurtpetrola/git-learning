# ⚙️ Advanced Git Commands

A deeper look into powerful Git commands for refining commits, managing branches, and handling complex version control workflows.

---

## 🧠 Commit & History Management

- **`git commit --amend`** : Modify the most recent commit (message or staged files).
- **`git revert <commit>`** : Create a new commit that undoes the changes of a previous one.
- **`git reset [--soft|--mixed|--hard] <commit>`** : Move HEAD to a specific commit with different levels of file/stage reset.

  - `--soft` → Keeps changes staged.
  - `--mixed` → Keeps changes in working directory.
  - `--hard` → Discards all changes.

- **`git reflog`** : Shows the history of all HEAD movements (useful for recovery).

---

## 🌿 Branch & Merge Management

- **`git rebase [branch]`** : Reapply commits on top of another base branch (creates a linear history).
- **`git cherry-pick <commit>`** : Apply a specific commit from another branch.
- **`git stash`** : Temporarily save changes without committing.

  - `git stash pop` → Reapply the last stashed changes.
  - `git stash list` → Show all stashes.

- **`git merge --no-ff [branch]`** : Merge a branch while preserving commit history.

---

## 🏷️ Tagging & Releases

- **`git tag <tag-name>`** : Create a lightweight tag (e.g., version markers).
- **`git tag -a <tag-name> -m "message"`** : Create an annotated tag with a message.
- **`git push origin --tags`** : Push all tags to the remote repository.

---

## 🔍 Inspecting Changes

- **`git show <commit>`** : Display details and changes of a specific commit.
- **`git diff`** : Compare changes between working directory, staging area, and commits.
  - `git diff HEAD` → Compare current changes with the last commit.
  - `git diff --staged` → Show differences between staged changes and the last commit.

---

## 🌐 Remote Repository Management

- **`git remote -v`** : List remote connections.
- **`git fetch`** : Download objects and refs from the remote without merging.
- **`git pull --rebase`** : Update local branch while maintaining a cleaner history.
- **`git remote prune origin`** : Remove references to remote-tracking branches that no longer exist.

---

## 🧩 Troubleshooting & Recovery

- **`git restore <file>`** : Restore working directory files to a previous state.
- **`git bisect`** : Find the commit that introduced a bug by binary search.
- **`git clean -fd`** : Remove untracked files and directories.

---

## 🚀 Tips

- Use **rebase** instead of merge for a cleaner, linear history in personal branches.
- Run **`git stash`** before switching branches to avoid losing uncommitted work.
- Use **annotated tags** for official releases (`git tag -a v1.0.0 -m "First release"`).

---

## 🌐 Collaboration Workflows

Understanding team-oriented branching models is key for efficient collaboration and maintaining clean histories in shared repositories.

### 🔀 Feature Branch Workflow

- Create a new branch for each feature or fix:
  ```bash
  git checkout -b feature/awesome-feature
  ```
- Push and open a Pull Request (PR) or Merge Request (MR) when ready.
- Keeps `main` or `develop` branch stable and deployable.

### 🍴 Fork-and-Pull Request Workflow

- Common in open-source projects.
- Developers fork the main repository, make changes in their own copy, and submit a pull request.
- Maintainers review and merge contributions into the main project.

### 🚢 Release Branch Workflow

- Used for managing releases and bug fixes separately.
- Create a release branch from `develop`:

```bash
  git checkout -b release/v1.0.0 develop
```

- Fix bugs or finalize documentation before merging into both `main` and `develop`.
- Tag final versions:

```bash
  git tag -a v1.0.0 -m "Version 1.0.0 release"
```

### 🧩 Gitflow Model (Hybrid)

- Combines feature, release, and hotfix branches under a structured workflow.
- Branch types:
  - `main` — production-ready code
  - `develop` — integration branch
  - `feature/*` — new features
  - `release/*` — upcoming releases
  - `hotfix/*` — urgent patches

> Ideal for teams handling multiple parallel development streams

---

## 🔗 See Also

> Explore related Git documentation:

- [🧩 Prefixes](./Prefixes.md) — Commit and branch naming conventions
- [📘 Basics](./Basics.md) — Fundamental Git commands and usage
- [💡 Tips](./Tips.md) — Practical tips and best practices
- [🔗 Resources](./Resources.md) — External references and learning materials

---

_This guide expands your Git knowledge beyond the basics, helping you work more efficiently and confidently in real-world scenarios._
