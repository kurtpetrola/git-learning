# 🔧 Git Troubleshooting Guide

Practical solutions to common Git problems and mistakes.

> 💡 This guide helps you diagnose and fix Git issues quickly. Each section follows a problem-solution format with step-by-step instructions.

---

## 🔀 Merge Conflicts

### Understanding Merge Conflicts

Merge conflicts occur when Git can't automatically combine changes from different branches. This happens when the same lines in a file are modified differently in both branches.

### Reading Conflict Markers

When a conflict occurs, Git marks the conflicting sections in your files:

```
<<<<<<< HEAD
Your current branch changes
=======
Incoming branch changes
>>>>>>> feature-branch
```

- **`<<<<<<< HEAD`** — Start of your current branch changes
- **`=======`** — Separator between changes
- **`>>>>>>> branch-name`** — End of incoming branch changes

### Step-by-Step Resolution

**1. Identify Conflicted Files:**

```bash
git status
# Files with conflicts will be listed under "Unmerged paths"
```

**2. Open and Edit Conflicted Files:**

```bash
# Open the file in your editor
# Look for conflict markers (<<<<<<, =======, >>>>>>>)
# Decide which changes to keep:
#   - Keep yours
#   - Keep theirs
#   - Keep both (merge manually)
#   - Write something new
```

**3. Remove Conflict Markers:**

```bash
# After deciding what to keep, remove the markers:
# <<<<<<< HEAD
# =======
# >>>>>>>
```

**4. Stage the Resolved Files:**

```bash
git add <resolved-file>
```

**5. Complete the Merge:**

```bash
git commit
# Git will provide a default merge commit message
```

### Accepting All Changes from One Side

```bash
# Accept all changes from current branch (ours)
git checkout --ours <file>
git add <file>

# Accept all changes from incoming branch (theirs)
git checkout --theirs <file>
git add <file>
```

### Abort a Merge

```bash
# Cancel the merge and return to pre-merge state
git merge --abort
```

### Tools for Conflict Resolution

```bash
# Use Git's built-in merge tool
git mergetool

# Use VS Code (if configured)
code --wait <file>
```

> 🧠 Always test your code after resolving conflicts to ensure everything works correctly.

---

## ⏪ Undo & Recovery

### Undo Last Commit (Keep Changes)

```bash
# Undo commit but keep changes staged
git reset --soft HEAD~1

# Undo commit and keep changes unstaged
git reset HEAD~1
# or
git reset --mixed HEAD~1
```

### Undo Last Commit (Discard Changes)

```bash
# ⚠️ Warning: This permanently deletes changes
git reset --hard HEAD~1
```

### Recover Deleted Commits

If you accidentally deleted commits, use `reflog` to recover them:

```bash
# 1. Find the lost commit
git reflog
# Look for the commit hash you want to recover

# 2. Restore the commit
git checkout <commit-hash>
# or create a branch from it
git branch recovery-branch <commit-hash>

# 3. Merge back if needed
git checkout main
git merge recovery-branch
```

### Restore Deleted Files

```bash
# Restore a file deleted in the last commit
git checkout HEAD~1 -- <file-path>

# Restore from a specific commit
git checkout <commit-hash> -- <file-path>
```

### Discard Uncommitted Changes

```bash
# Discard changes in a specific file
git restore <file>
# or (legacy)
git checkout -- <file>

# Discard all uncommitted changes
git restore .

# Discard changes and untracked files
git reset --hard HEAD
git clean -fd
```

### Undo a Pushed Commit

**Option 1: Revert (Safe - Creates New Commit):**

```bash
# Create a new commit that undoes the changes
git revert <commit-hash>
git push
```

**Option 2: Reset (Risky - Rewrites History):**

```bash
# ⚠️ Only use on branches you own!
git reset --hard <commit-hash>
git push --force-with-lease
```

### Recover from `reset --hard`

```bash
# 1. Find the commit before reset
git reflog

# 2. Reset back to that commit
git reset --hard <commit-hash>
```

> 💡 `reflog` keeps a history of HEAD movements for ~90 days, so you can almost always recover from mistakes.

---

## 🌿 Branch Issues

### Can't Switch Branches (Uncommitted Changes)

**Problem:** `error: Your local changes to the following files would be overwritten by checkout`

**Solution 1: Stash Changes**

```bash
git stash push -m "WIP: description"
git switch <other-branch>
# Later, come back and restore:
git switch original-branch
git stash pop
```

**Solution 2: Commit Changes**

```bash
git add .
git commit -m "wip: temporary commit"
git switch <other-branch>
```

**Solution 3: Force Switch (Discard Changes)**

```bash
# ⚠️ This discards all changes
git switch -f <other-branch>
```

### Accidentally Deleted a Branch

```bash
# 1. Find the deleted branch in reflog
git reflog
# Look for "checkout: moving from deleted-branch"

# 2. Recreate the branch
git branch <branch-name> <commit-hash>
```

### Rename a Branch

**Rename Local Branch:**

```bash
# Rename current branch
git branch -m <new-name>

# Rename any branch
git branch -m <old-name> <new-name>
```

**Rename Remote Branch:**

```bash
# 1. Rename local branch
git branch -m <old-name> <new-name>

# 2. Delete old remote branch
git push origin --delete <old-name>

# 3. Push new branch and set upstream
git push origin -u <new-name>
```

### Branch Diverged from Origin

**Problem:** `Your branch and 'origin/main' have diverged`

**Solution 1: Rebase (Preferred)**

```bash
git fetch origin
git rebase origin/main
# Resolve conflicts if any
git push --force-with-lease
```

**Solution 2: Merge**

```bash
git fetch origin
git merge origin/main
git push
```

**Solution 3: Reset to Origin (Discard Local Changes)**

```bash
# ⚠️ This discards all local commits
git fetch origin
git reset --hard origin/main
```

### Remove Orphaned Branches

```bash
# List branches merged into main
git branch --merged main

# Delete merged branches (excluding main)
git branch --merged main | grep -v "main" | xargs git branch -d

# Windows PowerShell version:
git branch --merged main | Where-Object {$_ -notmatch "main"} | ForEach-Object {git branch -d $_.Trim()}
```

---

## 🌐 Remote Repository Problems

### Push Rejected (Non-Fast-Forward)

**Problem:** `! [rejected] main -> main (non-fast-forward)`

**Cause:** Remote has commits you don't have locally.

**Solution:**

```bash
# 1. Fetch and merge remote changes
git pull --rebase
# or
git fetch origin
git rebase origin/main

# 2. Resolve conflicts if any

# 3. Push changes
git push
```

### Can't Pull (Diverged Histories)

**Problem:** `fatal: Need to specify how to reconcile divergent branches`

**Solution 1: Rebase**

```bash
git pull --rebase
```

**Solution 2: Merge**

```bash
git pull --no-rebase
# or
git config pull.rebase false
git pull
```

**Solution 3: Fast-Forward Only**

```bash
git pull --ff-only
```

### Authentication Failures

**HTTPS Token Issues:**

```bash
# Update credentials (Windows)
git config --global credential.helper manager

# Clear cached credentials
git credential reject
# Enter the URL when prompted

# Set new token
git config --global credential.helper store
git pull  # Enter username and new token
```

**SSH Key Issues:**

```bash
# Test SSH connection
ssh -T git@github.com

# Add SSH key to agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa

# Generate new SSH key if needed
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### Remote Branch Deleted But Still Showing

```bash
# Remove stale remote-tracking branches
git fetch --prune
# or
git remote prune origin

# View remote branches
git branch -r
```

### Wrong Remote URL

```bash
# Check current remote URL
git remote -v

# Change remote URL (HTTPS to SSH)
git remote set-url origin git@github.com:username/repo.git

# Change remote URL (SSH to HTTPS)
git remote set-url origin https://github.com/username/repo.git
```

---

## 📝 Commit History Issues

### Wrong Commit Message

**Last Commit:**

```bash
git commit --amend -m "correct message"
# If already pushed:
git push --force-with-lease
```

**Older Commit:**

```bash
# Interactive rebase
git rebase -i HEAD~3  # Number of commits to go back

# In the editor, change 'pick' to 'reword' for commits to edit
# Save and close, then edit messages as prompted
```

### Committed to Wrong Branch

**Move Last Commit to New Branch:**

```bash
# Create new branch with current commit
git branch <new-branch>

# Remove commit from current branch
git reset --hard HEAD~1

# Switch to new branch
git switch <new-branch>
```

**Move Last Commit to Existing Branch:**

```bash
# 1. Get the commit hash
git log -1

# 2. Switch to correct branch
git switch <correct-branch>

# 3. Cherry-pick the commit
git cherry-pick <commit-hash>

# 4. Switch back and remove from wrong branch
git switch <wrong-branch>
git reset --hard HEAD~1
```

### Remove Sensitive Data from History

**Using git filter-repo (Recommended):**

```bash
# Install git-filter-repo first
pip install git-filter-repo

# Remove specific file
git filter-repo --path <file-to-remove> --invert-paths

# Force push (⚠️ this rewrites history)
git push --force-with-lease --all
```

**Alternative: BFG Repo-Cleaner:**

```bash
# Download BFG from https://rtyley.github.io/bfg-repo-cleaner/

# Remove file from history
bfg --delete-files <filename>

# Clean up
git reflog expire --expire=now --all
git gc --prune=now --aggressive

# Force push
git push --force-with-lease --all
```

> ⚠️ **Important:** Notify all collaborators before rewriting history. They'll need to re-clone or reset their repositories.

### Split a Large Commit

```bash
# 1. Reset to before the commit (keep changes)
git reset HEAD~1

# 2. Stage and commit changes in smaller chunks
git add <file1>
git commit -m "feat: add feature part 1"

git add <file2>
git commit -m "feat: add feature part 2"
```

### Reorder Commits

```bash
# Interactive rebase
git rebase -i HEAD~5

# In the editor, reorder the lines to reorder commits
# Save and close
```

---

## 📋 Staging & Working Directory

### Unstage Files

```bash
# Unstage specific file
git restore --staged <file>
# or (legacy)
git reset HEAD <file>

# Unstage all files
git restore --staged .
# or
git reset HEAD
```

### Staged Wrong Files

```bash
# Remove from staging but keep changes
git restore --staged <wrong-file>

# Check what's staged
git diff --staged
```

### Discard Changes to Specific Files

```bash
# Discard unstaged changes in a file
git restore <file>

# Discard staged changes
git restore --staged <file>
git restore <file>
```

### Remove Untracked Files

```bash
# Preview what will be removed
git clean -n

# Remove untracked files
git clean -f

# Remove untracked files and directories
git clean -fd

# Remove ignored files too
git clean -fdx
```

### Accidentally Staged All Files

```bash
# Unstage everything
git reset

# Or unstage everything except certain files
git reset HEAD
git add <files-to-keep-staged>
```

---

## 🔐 Authentication & Access

### HTTPS Authentication Issues

**Update Credentials:**

```bash
# Windows (Credential Manager)
git config --global credential.helper manager-core

# macOS (Keychain)
git config --global credential.helper osxkeychain

# Linux (Store)
git config --global credential.helper store
```

**Remove Cached Credentials:**

```bash
# Windows
cmdkey /list | findstr git
cmdkey /delete:LegacyGeneric:target=git:https://github.com

# macOS
git credential-osxkeychain erase
# Enter: protocol=https, host=github.com

# Linux
rm ~/.git-credentials
```

### SSH Key Problems

**Generate New SSH Key:**

```bash
# Generate key
ssh-keygen -t ed25519 -C "your_email@example.com"

# Start SSH agent
eval "$(ssh-agent -s)"

# Add key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard
# Windows
clip < ~/.ssh/id_ed25519.pub
# macOS
pbcopy < ~/.ssh/id_ed25519.pub
# Linux
cat ~/.ssh/id_ed25519.pub
```

**Test SSH Connection:**

```bash
ssh -T git@github.com
# Should see: "Hi username! You've successfully authenticated..."
```

### Permission Denied Errors

**Wrong SSH Key:**

```bash
# Check which key is being used
ssh -vT git@github.com

# Specify key explicitly
ssh-add -D  # Remove all keys
ssh-add ~/.ssh/id_ed25519  # Add correct key
```

**Wrong Permissions:**

```bash
# Fix SSH directory permissions
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```

### Token Expiration

**GitHub Personal Access Token:**

```bash
# 1. Generate new token at https://github.com/settings/tokens
# 2. Update stored credentials:
git credential reject
# Enter protocol, host, path

# 3. Next push will prompt for new credentials
git push
# Username: your-username
# Password: your-new-token
```

---

## 🧩 Quick Problem Finder

Can't find your issue? Use this quick reference:

| Problem                   | See Section                                                 |
| :------------------------ | :---------------------------------------------------------- |
| Files show `<<<<<<< HEAD` | [Merge Conflicts](#-merge-conflicts)                        |
| Need to undo last commit  | [Undo & Recovery](#-undo--recovery)                         |
| Lost commits after reset  | [Recover Deleted Commits](#recover-deleted-commits)         |
| Can't switch branches     | [Branch Issues](#-branch-issues)                            |
| Push rejected             | [Remote Problems](#-remote-repository-problems)             |
| Wrong commit message      | [Commit History Issues](#-commit-history-issues)            |
| Files stuck in staging    | [Staging & Working Directory](#-staging--working-directory) |
| Authentication failed     | [Authentication & Access](#-authentication--access)         |

---

## 🔗 See Also

> Explore related Git documentation:

- [📘 Basics](./Basics.md) — Fundamental Git commands and usage
- [⚙️ Advanced](./Advanced.md) — Advanced Git commands and workflows
- [🧩 Prefixes](./Prefixes.md) — Commit and branch naming conventions
- [🚀 Modern](./Modern.md) — Modern Git features and tools
- [💡 Tips](./Tips.md) — Practical tips and best practices
- [🔗 Resources](./Resources.md) — External references and learning materials

---

_This guide helps you recover from mistakes and solve common Git problems quickly and safely._
