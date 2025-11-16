# 🧰 Git Basics

Essential Git commands for initializing, managing, and collaborating on repositories.

---

## 🗺️ Git Workflow Overview

     ┌──────────────────────────┐
     │        git init          │
     │   Create a repository    │
     └────────────┬─────────────┘
                  │
                  ▼
        ┌──────────────────┐
        │  git add .       │
        │  git commit -m ""│
        │  Track changes   │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │ git branch /     │
        │ git switch       │
        │ Manage branches  │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │ git push / pull  │
        │ Sync with remote │
        └────────┬─────────┘
                 │
                 ▼
        ┌──────────────────┐
        │ git merge        │
        │ Integrate changes│
        └──────────────────┘

> 💡 This flow captures the typical Git lifecycle: initialize → track → branch → sync → merge.

---

## ⚙️ Repository Setup

- **`git init`** — Initialize a new Git repository in the current directory.
- **`git clone <url>`** — Create a local copy of a remote repository.
  > 💡 Tip: Run `git status` right after initializing or cloning to check your repo’s state.

---

## 🪶 Staging & Committing

- **`git add <file>`** — Stage changes for the next commit.
  - **`git add .`** — Stage all modified files in the current directory.
- **`git commit -m "commit message"`** — Save staged changes as a new commit.
- **`git status`** — Show the current state of the working directory and staging area.
  > 🧠 Use concise, descriptive commit messages to maintain a clean history.

---

## 🚀 Synchronizing with Remote

- **`git remote add origin <url>`** — Connect your local repository to a remote host.
- **`git push`** — Upload local commits to the remote repository.
- **`git pull`** — Fetch and merge changes from the remote repository.
  > ⚡ Run `git pull --rebase` for cleaner, linear commit histories in personal projects.

---

## 🌿 Branching & Merging

- **`git branch`** — List all local branches.
  - **`git branch <branch-name>`** — Create a new branch.
- **`git switch <branch-name>`** — Switch to another branch (recommended over `checkout`).
- **`git merge <branch-name>`** — Merge the specified branch into the current one.
- **`git branch -d <branch-name>`** — **Delete the local branch (safe)**. Only deletes if the branch has been fully merged into its upstream.
  - Use **`git branch -D <branch-name>`** to **forcefully** delete the branch, even if it has unmerged changes.
    > 🪄 Keep your `main` branch stable; use feature branches for development and experimentation.

---

## 🧭 Viewing History

- **`git log`** — Display the commit history of the repository.
  - **`git log --oneline --graph --decorate`** — Show a simplified visual history.
- **`git diff`** — Compare working directory changes with the last commit.

---

## 🧹 Undoing Changes

- **`git restore <file>`** — Revert unstaged changes in a file.
- **`git reset <file>`** — Unstage a file without discarding changes.
- **`git checkout -- <file>`** — (Legacy) Restore file to last committed state.
  > 🧩 Learn the difference between `reset`, `restore`, and `revert` in the [Advanced](./Advanced.md) guide.

---

## 🧩 Common Workflows

> These examples combine basic commands into simple, real-world sequences you’ll use often.

### 🏗️ Start a New Project

```bash
git init
git add .
git commit -m "chore: initial project setup"
git branch -M main
git remote add origin <url>
git push -u origin main
```

### 🌿 Create a New Feature Branch

```bash
git switch -c feat/new-feature
# make changes
git add .
git commit -m "feat: implement new feature"
git push -u origin feat/new-feature
```

### 🔄 Sync and Update Your Local Repository

```bash
git switch main
git pull --rebase
```

### 🚢 Merge and Clean Up

```bash
git merge feat/new-feature
git branch -d feat/new-feature
git push origin --delete feat/new-feature
```

> 🧠 These workflows provide a solid foundation before exploring [Advanced Git Commands](./Advanced.md) like `rebase`, `stash`, and `cherry-pick`.

---

## 🔗 See Also

> Explore related Git documentation:

- [🧩 Prefixes](./Prefixes.md) — Commit and branch naming conventions
- [⚙️ Advanced](./Advanced.md) — Advanced Git commands and workflows
- [💡 Tips](./Tips.md) — Practical tips and best practices
- [🔗 Resources](./Resources.md) — External references and learning materials

---

_This guide serves as a quick reference for essential Git commands to keep your workflow efficient and organized._
