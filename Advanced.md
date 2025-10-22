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
- **`git prune`** : Remove references to remote-tracking branches that no longer exist.

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

_This guide expands your Git knowledge beyond the basics, helping you work more efficiently and confidently in real-world scenarios._
