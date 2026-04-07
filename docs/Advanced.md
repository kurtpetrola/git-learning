# Advanced Git Commands

A deeper look into powerful Git commands for refining commits, managing branches, and handling complex version control workflows.

> **Note:** If you're new to Git, start with [Basics](./Basics.md) before diving into these commands.

---

## Advanced Workflow Overview

     ┌────────────────────────┐
     │      git stash         │
     │ Save work temporarily  │
     └──────────┬─────────────┘
                │
                ▼
     ┌────────────────────────┐
     │      git rebase -i     │
     │ Clean up commit history│
     └──────────┬─────────────┘
                │
                ▼
     ┌────────────────────────┐
     │   git cherry-pick      │
     │ Apply specific commits │
     └──────────┬─────────────┘
                │
                ▼
     ┌────────────────────────┐
     │      git merge         │
     │ Integrate final branch │
     └────────────────────────┘

> **Note:** This diagram illustrates how advanced commands refine, apply, and integrate commits for cleaner, more controlled version histories.

---

## Commit & History Management

A deeper look at tools for rewriting history, fixing mistakes, and cleaning up commit logs.

- **`git commit --amend`** — Modify the most recent commit (message or staged files).
- **`git revert <commit>`** — Create a new commit that undoes the changes of a previous one.

  ```bash
  git revert abc1234
  # creates a new commit reversing abc1234
  ```

- **`git reset [--soft|--mixed|--hard] <commit>`** — Move HEAD to a specific commit with different levels of file/stage reset.

  - `--soft` → Keeps changes staged.
  - `--mixed` → Keeps changes in working directory.
  - `--hard` → Discards all changes.

- **`git reflog`** — Shows the history of all HEAD movements (useful for recovery).
- **`git rebase -i <commit-hash>`** — Interactive Rebase. The master tool for history rewriting. Allows you to **squash**, **edit**, **reword**, **reorder**, and **drop** commits in a range.

```bash
# Opens an editor to modify the last 3 commits before pushing
git rebase -i HEAD~3
```

---

## Branch & Merge Management

- **`git rebase [branch]`** — Reapply commits on top of another base branch (creates a linear history).
- **`git cherry-pick <commit>`** — Apply a specific commit from another branch.
- **`git stash`** — Temporarily save changes without committing.

  - `git stash pop` → Reapply the last stashed changes.
  - `git stash list` → Show all stashes.

- **`git merge --no-ff [branch]`** — Merge a branch while preserving commit history.
- **`git branch -m <new-name>`** — Rename the current local branch.

  ```bash
  # 1. Rename the local branch (e.g., from 'feat/old-bug' to 'feature/fix-bug')
  git branch -m feature/fix-bug

  # 2. Push the new branch and set it as upstream (or use the existing alias -u)
  git push origin -u feature/fix-bug

  # 3. Optional: Delete the old name on the remote
  git push origin --delete feat/old-bug
  ```

- **`git branch --set-upstream-to=origin/<branch> <local-branch>`** — Explicitly configure or change the remote tracking branch for a local branch.

---

## Tagging & Releases

- **`git tag <tag-name>`** — Create a lightweight tag (e.g., version markers).
- **`git tag -a <tag-name> -m "message"`** — Create an annotated tag with a message.
- **`git push origin --tags`** — Push all tags to the remote repository.

---

## Inspecting Changes

- **`git show <commit>`** — Display details and changes of a specific commit.
- **`git diff`** — Compare changes between working directory, staging area, and commits.
  - `git diff HEAD` → Compare current changes with the last commit.
  - `git diff --staged` → Show differences between staged changes and the last commit.
- **`git log -p <file>`** — Shows the commit history and the full patch (diff) for every commit that modified a specific file.

---

## Remote Repository Management

- **`git remote -v`** — List remote connections.
- **`git fetch`** — Download objects and refs from the remote without merging.
- **`git pull --rebase`** — Update local branch while maintaining a cleaner history.
- **`git push --force-with-lease`** — Safely overwrite remote history after a local rebase or amend. This check prevents accidental overwrites of remote work.
- **`git remote prune origin`** — Remove references to remote-tracking branches that no longer exist.

---

## Troubleshooting & Recovery

- **`git restore <file>`** — Restore working directory files to a previous state.

  ```bash
  git restore src/app.js
  # restores app.js to the last committed state
  ```

- **`git bisect`** — Find the commit that introduced a bug by binary search.
- **`git clean -fd`** — Remove untracked files and directories.

---

## Tips

These practical reminders help maintain efficient, safe Git usage in everyday scenarios.

- Use **interactive rebase** (`git rebase -i`) to clean up commits before merging or pushing a feature branch.
- Use **`git push --force-with-lease`** instead of `git push --force` after rewriting history.
- Run **`git stash`** before switching branches to avoid losing uncommitted work.
- Use **annotated tags** for official releases (`git tag -a v1.0.0 -m "First release"`).

---

## Collaboration Workflows

Understanding team-oriented branching models is key for efficient collaboration and maintaining clean histories in shared repositories.

### Feature Branch Workflow

- Create a new branch for each feature or fix:

  ```bash
  git switch -c feature/awesome-feature
  ```

- Push and open a Pull Request (PR) or Merge Request (MR) when ready.
- Keeps `main` or `develop` branch stable and deployable.

### Fork-and-Pull Request Workflow

- Common in open-source projects.
- Developers fork the main repository, make changes in their own copy, and submit a pull request.
- Maintainers review and merge contributions into the main project.

### Release Branch Workflow

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

### Gitflow Model (Hybrid)

- Combines feature, release, and hotfix branches under a structured workflow.
- Branch types:

  - `main` — production-ready code
  - `develop` — integration branch
  - `feature/*` — new features
  - `release/*` — upcoming releases
  - `hotfix/*` — urgent patches

  > Ideal for teams handling multiple parallel development streams.

---

## Common Advanced Workflows

> Practical examples for applying advanced Git commands in real-world scenarios.

### Rebase a Feature Branch onto Main

```bash
git switch feat/new-feature
git fetch origin
git rebase origin/main
# resolve conflicts if any
git push --force-with-lease
```

> **Tip:** Keeps feature history clean and avoids merge clutter.

### Cherry-Pick a Specific Commit

```bash
git switch main
git cherry-pick abc1234
```

> **Tip:** Useful when you need a single fix from another branch without merging the whole thing.

### Stash and Restore Changes

```bash
git stash push -m "wip: refactor UI"
git switch main
git pull --rebase
git switch feat/ui-update
git stash pop
```

> **Tip:** Safely save your work-in-progress before syncing or switching branches.

### Bisect to Find a Bug

```bash
git bisect start
git bisect bad
git bisect good <commit-hash>
# test commits as prompted
git bisect reset
```

> **Note:** Automates debugging by isolating the exact commit that introduced a regression.

---

## See Also

> Explore related Git documentation:

- [Prefixes](./Prefixes.md) — Commit and branch naming conventions
- [Basics](./Basics.md) — Fundamental Git commands and usage
- [Modern](./Modern.md) — Modern Git features and tools
- [Troubleshooting](./Troubleshooting.md) — Common problems and solutions
- [Config](./Config.md) — Useful aliases and configuration examples
- [Cheat Sheet](./CheatSheet.md) — Quick command reference
- [Tips](./Tips.md) — Practical tips and best practices
- [Resources](./Resources.md) — External references and learning materials

---

_This guide expands your Git knowledge beyond the basics, helping you work more efficiently and confidently in real-world scenarios._
