# ⚙️ Git Config Examples

Practical Git configurations, aliases, and settings to boost your productivity.

> 💡 Copy these configurations to enhance your Git workflow. Apply them using `git config --global` or add directly to your `~/.gitconfig` file.

---

## 🎯 Useful Aliases

Shortcuts and enhanced commands to speed up your workflow.

### Basic Shortcuts

```bash
# Status
git config --global alias.st status

# Checkout
git config --global alias.co checkout

# Branch
git config --global alias.br branch

# Commit
git config --global alias.ci commit

# Add all
git config --global alias.aa "add --all"
```

**`.gitconfig` format:**

```ini
[alias]
    st = status
    co = checkout
    br = branch
    ci = commit
    aa = add --all
```

### Enhanced Log Aliases

```bash
# Beautiful one-line log
git config --global alias.lg "log --oneline --graph --decorate --all"

# Detailed log with stats
git config --global alias.ll "log --pretty=format:'%C(yellow)%h%C(reset) - %C(cyan)%an%C(reset) %C(green)(%ar)%C(reset) %s' --abbrev-commit"

# Log with file changes
git config --global alias.ls "log --stat --abbrev-commit"

# Last 10 commits
git config --global alias.last "log -10 --oneline --decorate"
```

**`.gitconfig` format:**

```ini
[alias]
    lg = log --oneline --graph --decorate --all
    ll = log --pretty=format:'%C(yellow)%h%C(reset) - %C(cyan)%an%C(reset) %C(green)(%ar)%C(reset) %s' --abbrev-commit
    ls = log --stat --abbrev-commit
    last = log -10 --oneline --decorate
```

### Workflow Aliases

```bash
# Undo last commit (keep changes)
git config --global alias.undo "reset HEAD~1 --mixed"

# Unstage all files
git config --global alias.unstage "reset HEAD --"

# Amend last commit
git config --global alias.amend "commit --amend --no-edit"

# Show changes in last commit
git config --global alias.last-changes "diff HEAD^ HEAD"

# List all aliases
git config --global alias.aliases "config --get-regexp ^alias\."
```

**`.gitconfig` format:**

```ini
[alias]
    undo = reset HEAD~1 --mixed
    unstage = reset HEAD --
    amend = commit --amend --no-edit
    last-changes = diff HEAD^ HEAD
    aliases = config --get-regexp ^alias\.
```

### Advanced Power Aliases

```bash
# Interactive rebase last 5 commits
git config --global alias.reb "rebase -i HEAD~5"

# Find branches containing commit
git config --global alias.fb "!f() { git branch -a --contains \$1; }; f"

# Delete merged branches
git config --global alias.cleanup "!git branch --merged | grep -v '\\*\\|main\\|master\\|develop' | xargs -n 1 git branch -d"

# Stash with message
git config --global alias.save "!git stash push -m"

# Create branch and switch
git config --global alias.cob "checkout -b"

# Show contributors
git config --global alias.contributors "shortlog -sn"
```

**`.gitconfig` format:**

```ini
[alias]
    reb = rebase -i HEAD~5
    fb = "!f() { git branch -a --contains $1; }; f"
    cleanup = "!git branch --merged | grep -v '\\*\\|main\\|master\\|develop' | xargs -n 1 git branch -d"
    save = "!git stash push -m"
    cob = checkout -b
    contributors = shortlog -sn
```

### Safety Aliases

```bash
# Force push safely
git config --global alias.pushf "push --force-with-lease"

# Pull with rebase
git config --global alias.up "pull --rebase --autostash"

# Show what would be pushed
git config --global alias.ready "log @{u}.. --oneline"
```

**`.gitconfig` format:**

```ini
[alias]
    pushf = push --force-with-lease
    up = pull --rebase --autostash
    ready = log @{u}.. --oneline
```

---

## 🌐 Global Configuration

Essential global settings for a better Git experience.

### User Information

```bash
# Set your name and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

**`.gitconfig` format:**

```ini
[user]
    name = Your Name
    email = your.email@example.com
```

### Default Editor

```bash
# VS Code
git config --global core.editor "code --wait"

# Vim
git config --global core.editor "vim"

# Nano
git config --global core.editor "nano"

# Notepad (Windows)
git config --global core.editor "notepad"
```

**`.gitconfig` format:**

```ini
[core]
    editor = code --wait
```

### Default Branch Name

```bash
# Use 'main' as default branch name
git config --global init.defaultBranch main
```

**`.gitconfig` format:**

```ini
[init]
    defaultBranch = main
```

### Diff and Merge Tools

```bash
# VS Code as diff tool
git config --global diff.tool vscode
git config --global difftool.vscode.cmd "code --wait --diff \$LOCAL \$REMOTE"

# VS Code as merge tool
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd "code --wait \$MERGED"
```

**`.gitconfig` format:**

```ini
[diff]
    tool = vscode
[difftool "vscode"]
    cmd = code --wait --diff $LOCAL $REMOTE

[merge]
    tool = vscode
[mergetool "vscode"]
    cmd = code --wait $MERGED
```

---

## 🎨 UI/UX Improvements

Enhance Git's visual output and user experience.

### Color Configuration

```bash
# Enable colors
git config --global color.ui auto

# Custom colors for status
git config --global color.status.added "green bold"
git config --global color.status.changed "yellow bold"
git config --global color.status.untracked "red bold"

# Custom colors for branch
git config --global color.branch.current "yellow reverse"
git config --global color.branch.local "yellow"
git config --global color.branch.remote "green"
```

**`.gitconfig` format:**

```ini
[color]
    ui = auto

[color "status"]
    added = green bold
    changed = yellow bold
    untracked = red bold

[color "branch"]
    current = yellow reverse
    local = yellow
    remote = green
```

### Pager Settings

```bash
# Use less as pager with better options
git config --global core.pager "less -FRX"

# Disable pager for certain commands
git config --global pager.branch false
git config --global pager.tag false
```

**`.gitconfig` format:**

```ini
[core]
    pager = less -FRX

[pager]
    branch = false
    tag = false
```

### Autocorrect

```bash
# Auto-correct typos after 1 second (10 = 1 second)
git config --global help.autocorrect 10
```

**`.gitconfig` format:**

```ini
[help]
    autocorrect = 10
```

### Better Status Output

```bash
# Show short status format
git config --global status.short true

# Show branch info in status
git config --global status.branch true

# Show stash info in status
git config --global status.showStash true
```

**`.gitconfig` format:**

```ini
[status]
    short = true
    branch = true
    showStash = true
```

---

## ⚡ Performance Settings

Optimize Git's performance for faster operations.

### Credential Caching

```bash
# Cache credentials for 1 hour (3600 seconds)
git config --global credential.helper "cache --timeout=3600"

# Windows: Use Windows Credential Manager
git config --global credential.helper manager-core

# macOS: Use macOS Keychain
git config --global credential.helper osxkeychain
```

**`.gitconfig` format:**

```ini
# Linux/Unix
[credential]
    helper = cache --timeout=3600

# Windows
[credential]
    helper = manager-core

# macOS
[credential]
    helper = osxkeychain
```

### Parallel Processing

```bash
# Use multiple threads for pack operations
git config --global pack.threads 0  # 0 = auto-detect CPU cores

# Parallel fetch submodules
git config --global submodule.fetchJobs 4
```

**`.gitconfig` format:**

```ini
[pack]
    threads = 0

[submodule]
    fetchJobs = 4
```

### Filesystem Monitoring

```bash
# Enable filesystem monitor for large repos
git config --global core.fsmonitor true

# Untracked cache for faster status
git config --global core.untrackedCache true
```

**`.gitconfig` format:**

```ini
[core]
    fsmonitor = true
    untrackedCache = true
```

---

## 💻 Platform-Specific Configurations

Settings tailored for Windows, macOS, and Linux.

### Windows-Specific

```bash
# Handle line endings (CRLF on checkout, LF on commit)
git config --global core.autocrlf true

# Symlink support
git config --global core.symlinks true

# Credential manager
git config --global credential.helper manager-core

# Long paths support
git config --global core.longpaths true
```

**`.gitconfig` format:**

```ini
[core]
    autocrlf = true
    symlinks = true
    longpaths = true

[credential]
    helper = manager-core
```

### macOS-Specific

```bash
# Preserve file mode
git config --global core.fileMode true

# Use macOS Keychain for credentials
git config --global credential.helper osxkeychain

# Ignore .DS_Store
git config --global core.excludesfile ~/.gitignore_global
# Then create ~/.gitignore_global with:
# .DS_Store
```

**`.gitconfig` format:**

```ini
[core]
    fileMode = true
    excludesfile = ~/.gitignore_global

[credential]
    helper = osxkeychain
```

### Linux-Specific

```bash
# Preserve file mode and permissions
git config --global core.fileMode true

# Use credential cache
git config --global credential.helper cache
```

**`.gitconfig` format:**

```ini
[core]
    fileMode = true

[credential]
    helper = cache
```

---

## 🔒 Safety & Best Practices

Configurations to prevent common mistakes and protect your work.

### Auto-Stash on Rebase

```bash
# Automatically stash before rebase
git config --global rebase.autoStash true
```

**`.gitconfig` format:**

```ini
[rebase]
    autoStash = true
```

### Push Behavior

```bash
# Only push current branch
git config --global push.default current

# Automatically set upstream on push
git config --global push.autoSetupRemote true

# Require force with lease instead of force
git config --global push.useForceIfIncludes true
```

**`.gitconfig` format:**

```ini
[push]
    default = current
    autoSetupRemote = true
    useForceIfIncludes = true
```

### Pull Strategy

```bash
# Use rebase by default when pulling
git config --global pull.rebase true

# Or use merge (explicit)
git config --global pull.rebase false

# Only fast-forward merges
git config --global pull.ff only
```

**`.gitconfig` format:**

```ini
[pull]
    rebase = true
    # or
    # rebase = false
    # ff = only
```

### Prune on Fetch

```bash
# Automatically prune remote branches
git config --global fetch.prune true
```

**`.gitconfig` format:**

```ini
[fetch]
    prune = true
```

### Commit Signing

```bash
# Sign all commits by default
git config --global commit.gpgsign true

# Set GPG key
git config --global user.signingkey YOUR_GPG_KEY_ID
```

**`.gitconfig` format:**

```ini
[commit]
    gpgsign = true

[user]
    signingkey = YOUR_GPG_KEY_ID
```

---

## 📋 Complete Example `.gitconfig`

Here's a ready-to-use configuration combining the best settings:

```ini
[user]
    name = Your Name
    email = your.email@example.com

[core]
    editor = code --wait
    autocrlf = input  # Use 'true' on Windows
    pager = less -FRX
    excludesfile = ~/.gitignore_global

[init]
    defaultBranch = main

[color]
    ui = auto

[alias]
    # Shortcuts
    st = status
    co = checkout
    br = branch
    ci = commit
    aa = add --all

    # Logs
    lg = log --oneline --graph --decorate --all
    ll = log --pretty=format:'%C(yellow)%h%C(reset) - %C(cyan)%an%C(reset) %C(green)(%ar)%C(reset) %s' --abbrev-commit
    last = log -10 --oneline --decorate

    # Workflow
    undo = reset HEAD~1 --mixed
    unstage = reset HEAD --
    amend = commit --amend --no-edit
    save = "!git stash push -m"
    cob = checkout -b

    # Advanced
    pushf = push --force-with-lease
    up = pull --rebase --autostash
    cleanup = "!git branch --merged | grep -v '\\*\\|main\\|master\\|develop' | xargs -n 1 git branch -d"

[push]
    default = current
    autoSetupRemote = true

[pull]
    rebase = true

[fetch]
    prune = true

[rebase]
    autoStash = true

[help]
    autocorrect = 10

# Platform-specific (uncomment as needed)

# Windows
# [core]
#     longpaths = true
# [credential]
#     helper = manager-core

# macOS
# [credential]
#     helper = osxkeychain

# Linux
# [credential]
#     helper = cache --timeout=3600
```

---

## 🚀 Quick Setup

Copy and paste to apply the recommended configuration:

```bash
# User info
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Editor
git config --global core.editor "code --wait"

# Default branch
git config --global init.defaultBranch main

# Essential aliases
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

# Safety
git config --global push.default current
git config --global push.autoSetupRemote true
git config --global pull.rebase true
git config --global fetch.prune true
git config --global rebase.autoStash true

# UI
git config --global color.ui auto
git config --global help.autocorrect 10
```

---

## 🔍 View Your Config

```bash
# View all global configuration
git config --global --list

# View specific config value
git config --global user.name

# View all aliases
git config --get-regexp ^alias\.

# Open config file in editor
git config --global --edit
```

---

## 🔗 See Also

> Explore related Git documentation:

- [📘 Basics](./Basics.md) — Fundamental Git commands and usage
- [⚙️ Advanced](./Advanced.md) — Advanced Git commands and workflows
- [🧩 Prefixes](./Prefixes.md) — Commit and branch naming conventions
- [🚀 Modern](./Modern.md) — Modern Git features and tools
- [🔧 Troubleshooting](./Troubleshooting.md) — Common problems and solutions
- [💡 Tips](./Tips.md) — Practical tips and best practices
- [🔗 Resources](./Resources.md) — External references and learning materials

---

_These configurations will supercharge your Git workflow and make everyday operations faster and safer._
