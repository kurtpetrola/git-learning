# 📋 Git Cheat Sheet

Quick reference for the most commonly used Git commands.

---

## ⚙️ Setup & Configuration

```bash
# Set your name and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default editor
git config --global core.editor "code --wait"

# Set default branch name
git config --global init.defaultBranch main

# View config
git config --list
git config --global --list
```

---

## 🏁 Basic Commands

### Repository Setup

```bash
git init                          # Initialize new repository
git clone <url>                   # Clone remote repository
```

### Staging & Committing

```bash
git status                        # Show working directory status
git add <file>                    # Stage specific file
git add .                         # Stage all changes
git commit -m "message"           # Commit staged changes
git commit -am "message"          # Stage and commit (tracked files only)
git commit --amend                # Amend last commit
```

### Inspection

```bash
git diff                          # Show unstaged changes
git diff --staged                 # Show staged changes
git diff HEAD                     # Show all changes since last commit
```

---

## 🌿 Branching & Merging

### Branch Management

```bash
git branch                        # List local branches
git branch <name>                 # Create new branch
git branch -d <name>              # Delete branch (safe)
git branch -D <name>              # Force delete branch
git branch -m <new-name>          # Rename current branch
```

### Switching Branches

```bash
git switch <branch>               # Switch to branch
git switch -c <branch>            # Create and switch to branch
git checkout <branch>             # (Legacy) Switch to branch
```

### Merging

```bash
git merge <branch>                # Merge branch into current
git merge --no-ff <branch>        # Merge with merge commit
git merge --abort                 # Abort merge
```

---

## 🌐 Remote Operations

### Remote Management

```bash
git remote -v                     # List remotes
git remote add origin <url>       # Add remote
git remote set-url origin <url>   # Change remote URL
git remote prune origin           # Remove stale remote branches
```

### Fetch, Pull, Push

```bash
git fetch                         # Download objects from remote
git fetch --prune                 # Fetch and prune stale branches
git pull                          # Fetch and merge
git pull --rebase                 # Fetch and rebase
git push                          # Upload to remote
git push -u origin <branch>       # Push and set upstream
git push --force-with-lease       # Safe force push
```

### Cloning

```bash
git clone <url>                   # Clone repository
git clone <url> <directory>       # Clone to specific directory
git clone --branch <name> <url>   # Clone specific branch
```

---

## ⏪ Undo & Revert

### Unstage & Restore

```bash
git restore <file>                # Discard changes in file
git restore --staged <file>       # Unstage file
git reset <file>                  # Unstage file (legacy)
git checkout -- <file>            # Restore file (legacy)
```

### Reset

```bash
git reset --soft HEAD~1           # Undo commit, keep changes staged
git reset HEAD~1                  # Undo commit, keep changes unstaged
git reset --hard HEAD~1           # Undo commit, discard changes
```

### Revert

```bash
git revert <commit>               # Create new commit undoing changes
git revert --no-commit <commit>   # Revert without committing
```

### Stash

```bash
git stash                         # Save changes temporarily
git stash push -m "message"       # Stash with message
git stash list                    # List all stashes
git stash pop                     # Apply and remove last stash
git stash apply                   # Apply last stash (keep it)
git stash drop                    # Delete last stash
git stash clear                   # Delete all stashes
```

---

## 🔍 Inspection & History

### Log

```bash
git log                           # Show commit history
git log --oneline                 # Compact log
git log --oneline --graph --all   # Visual branch history
git log -n 5                      # Show last 5 commits
git log --author="name"           # Filter by author
git log --since="2 weeks ago"     # Time-based filter
git log -- <file>                 # History of specific file
```

### Show & Diff

```bash
git show <commit>                 # Show commit details
git show HEAD                     # Show last commit
git diff <commit1> <commit2>      # Compare commits
git diff <branch1> <branch2>      # Compare branches
```

### Blame & Search

```bash
git blame <file>                  # Show who changed each line
git grep "search term"            # Search in repository
```

---

## 🧰 Advanced Operations

### Rebase

```bash
git rebase <branch>               # Rebase current branch
git rebase -i HEAD~3              # Interactive rebase last 3 commits
git rebase --continue             # Continue after resolving conflicts
git rebase --abort                # Cancel rebase
```

### Cherry-Pick

```bash
git cherry-pick <commit>          # Apply specific commit
```

### Tags

```bash
git tag                           # List tags
git tag <name>                    # Create lightweight tag
git tag -a <name> -m "message"    # Create annotated tag
git push origin --tags            # Push tags to remote
```

### Reflog

```bash
git reflog                        # Show reference log
git reflog show <branch>          # Show reflog for branch
```

### Clean

```bash
git clean -n                      # Preview untracked files to remove
git clean -f                      # Remove untracked files
git clean -fd                     # Remove untracked files and directories
```

---

## 🎯 Useful Aliases

Add these to your `.gitconfig` for faster workflow:

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.lg "log --oneline --graph --decorate --all"
git config --global alias.undo "reset HEAD~1 --mixed"
git config --global alias.unstage "reset HEAD --"
git config --global alias.amend "commit --amend --no-edit"
git config --global alias.pushf "push --force-with-lease"
git config --global alias.up "pull --rebase --autostash"
```

---

## 🚨 Emergency Commands

```bash
# Undo last commit (keep changes)
git reset HEAD~1

# Discard all local changes
git reset --hard HEAD
git clean -fd

# Recover deleted commit
git reflog                        # Find commit hash
git cherry-pick <hash>            # Restore commit

# Fix wrong branch
git branch <new-branch>           # Create branch with current commit
git reset --hard HEAD~1           # Remove commit from current branch
git switch <new-branch>           # Switch to new branch

# Abort operations
git merge --abort
git rebase --abort
git cherry-pick --abort
```

---

## 📊 Quick Reference Table

| Command                 | Description           |
| :---------------------- | :-------------------- |
| `git init`              | Initialize repository |
| `git clone <url>`       | Clone repository      |
| `git status`            | Check status          |
| `git add .`             | Stage all changes     |
| `git commit -m "msg"`   | Commit changes        |
| `git push`              | Push to remote        |
| `git pull`              | Pull from remote      |
| `git branch`            | List branches         |
| `git switch <branch>`   | Switch branch         |
| `git merge <branch>`    | Merge branch          |
| `git log`               | View history          |
| `git diff`              | Show changes          |
| `git stash`             | Save work temporarily |
| `git reset --hard HEAD` | Discard all changes   |
| `git reflog`            | Recovery tool         |

---

## 🔗 See Also

> For detailed explanations and examples:

- [📘 Basics](./Basics.md) — Fundamental Git commands and usage
- [⚙️ Advanced](./Advanced.md) — Advanced Git commands and workflows
- [🧩 Prefixes](./Prefixes.md) — Commit and branch naming conventions
- [🚀 Modern](./Modern.md) — Modern Git features and tools
- [🔧 Troubleshooting](./Troubleshooting.md) — Common problems and solutions
- [⚙️ Config](./Config.md) — Useful aliases and configuration examples
- [💡 Tips](./Tips.md) — Practical tips and best practices
- [🔗 Resources](./Resources.md) — External references and learning materials

---

_Print this cheat sheet and keep it nearby for quick reference while learning Git!_
