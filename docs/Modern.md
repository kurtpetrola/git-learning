# 🚀 Modern Git Features

Essential modern Git capabilities and tools for contemporary development workflows.

> 📘 This guide complements [Basics](./Basics.md) and [Advanced](./Advanced.md) with features that have become critical in professional environments.

---

## 🪝 Git Hooks

Automated scripts that run at specific points in Git's execution flow.

### What Are Git Hooks?

Git hooks are scripts that Git executes before or after events such as commits, pushes, and merges. They enable automation of quality checks, testing, and enforcement of standards.

### Common Hook Types

| Hook           | Trigger Event                | Common Use Cases                          |
| :------------- | :--------------------------- | :---------------------------------------- |
| **pre-commit** | Before commit is created     | Linting, formatting, syntax checking      |
| **commit-msg** | After commit message entered | Enforce commit message conventions        |
| **pre-push**   | Before push to remote        | Run tests, check branch protection        |
| **post-merge** | After merge completes        | Dependency updates, rebuild notifications |

### Practical Example: Pre-commit Hook

```bash
# .git/hooks/pre-commit
#!/bin/sh

# Run linter before allowing commit
npm run lint
if [ $? -ne 0 ]; then
  echo "❌ Linting failed. Please fix errors before committing."
  exit 1
fi

echo "✅ Pre-commit checks passed!"
```

### Popular Hook Management Tools

- **[Husky](https://typicode.github.io/husky/)** — Easy Git hooks for Node.js projects
- **[pre-commit](https://pre-commit.com/)** — Multi-language hook framework
- **[lefthook](https://github.com/evilmartians/lefthook)** — Fast and powerful Git hooks manager

> 💡 Make hooks executable: `chmod +x .git/hooks/pre-commit`

---

## 🌳 Git Worktrees

Work on multiple branches simultaneously without switching or stashing.

### What Are Worktrees?

Worktrees allow you to checkout multiple branches at once in separate directories, all connected to the same repository.

### Basic Commands

```bash
# Create a new worktree for a feature branch
git worktree add ../my-feature feature/new-feature

# List all worktrees
git worktree list

# Remove a worktree
git worktree remove ../my-feature

# Prune stale worktree entries
git worktree prune
```

### Practical Use Cases

**1. Parallel Development:**

```bash
# Work on feature in one terminal
cd ~/project
git worktree add ../hotfix hotfix/critical-bug

# Review PR in another terminal
cd ../hotfix
# Make changes, test, commit
```

**2. Testing Different Branches:**

```bash
# Test main branch while developing
git worktree add ../testing-main main
cd ../testing-main
npm test
```

> 🧠 Each worktree has its own working directory but shares the same `.git` repository, saving disk space.

---

## 📦 Git Submodules & Subtrees

Manage external dependencies and nested repositories within your project.

### Submodules vs Subtrees

| Feature        | Submodules                      | Subtrees                                 |
| :------------- | :------------------------------ | :--------------------------------------- |
| **Complexity** | More complex to manage          | Simpler for contributors                 |
| **Repository** | Separate repository references  | Merged into parent repository            |
| **Updates**    | Manual sync required            | Manual merge required                    |
| **History**    | Keeps separate history          | Merges history into parent               |
| **Best For**   | External libs with own workflow | External code you want to modify locally |

### Git Submodules

```bash
# Add a submodule
git submodule add https://github.com/user/repo.git libs/external

# Clone a repository with submodules
git clone --recurse-submodules https://github.com/user/project.git

# Update submodules
git submodule update --remote --merge

# Remove a submodule
git submodule deinit libs/external
git rm libs/external
```

### Git Subtrees

```bash
# Add a subtree
git subtree add --prefix=libs/external https://github.com/user/repo.git main --squash

# Pull updates from subtree
git subtree pull --prefix=libs/external https://github.com/user/repo.git main --squash

# Push changes back to subtree
git subtree push --prefix=libs/external https://github.com/user/repo.git main
```

> ⚠️ Choose submodules for clean separation; choose subtrees for simplified contributor experience.

---

## 💾 Git LFS (Large File Storage)

Efficiently handle large files in Git repositories.

### What Is Git LFS?

Git LFS replaces large files with text pointers inside Git, while storing the actual file contents on a remote server.

### Installation

```bash
# Install Git LFS
# Windows (via Git for Windows installer or)
git lfs install

# macOS
brew install git-lfs
git lfs install

# Linux
sudo apt-get install git-lfs
git lfs install
```

### Basic Usage

```bash
# Track specific file types
git lfs track "*.psd"
git lfs track "*.mp4"
git lfs track "*.zip"

# View tracked patterns
git lfs track

# Add .gitattributes (created by track command)
git add .gitattributes

# Commit and push as normal
git add design.psd
git commit -m "feat: add design mockup"
git push
```

### Migration to LFS

```bash
# Migrate existing files to LFS
git lfs migrate import --include="*.psd,*.mp4" --everything
```

### Common Commands

```bash
# Show LFS files in current repository
git lfs ls-files

# Fetch all LFS objects
git lfs fetch --all

# Check LFS storage usage
git lfs status
```

> 💡 GitHub free tier includes 1GB LFS storage and 1GB bandwidth per month. Paid plans available for larger needs.

---

## 🎯 Sparse Checkout

Clone and work with only specific directories from large repositories.

### What Is Sparse Checkout?

Sparse checkout allows you to populate your working directory with only a subset of files from a repository, ideal for monorepos.

### Cone Mode (Recommended)

```bash
# Clone without checking out files
git clone --no-checkout https://github.com/user/monorepo.git
cd monorepo

# Initialize sparse-checkout in cone mode
git sparse-checkout init --cone

# Specify directories to include
git sparse-checkout set apps/frontend libs/shared

# Checkout the files
git checkout main
```

### Pattern Mode

```bash
# Initialize sparse-checkout
git sparse-checkout init

# Edit sparse-checkout patterns
git sparse-checkout set "apps/frontend/*" "libs/*"

# View current patterns
git sparse-checkout list
```

### Disable Sparse Checkout

```bash
# Return to full checkout
git sparse-checkout disable
```

> 🚀 Sparse checkout can significantly improve clone and checkout times for large monorepos.

---

## 🎨 Git Attributes (.gitattributes)

Control how Git handles specific files in your repository.

### What Are Git Attributes?

Git attributes allow you to define file-specific settings like line endings, diff behavior, merge strategies, and export rules.

### Common Use Cases

**1. Line Ending Normalization:**

```gitattributes
# .gitattributes

# Auto-detect text files and normalize line endings
* text=auto

# Force LF for shell scripts
*.sh text eol=lf

# Force CRLF for Windows batch files
*.bat text eol=crlf

# Binary files (no line ending conversion)
*.png binary
*.jpg binary
*.pdf binary
```

**2. Custom Diff Drivers:**

```gitattributes
# Better diffs for specific file types
*.json diff=json
*.md diff=markdown

# Treat minified files as binary (don't show diffs)
*.min.js binary
*.min.css binary
```

**3. Merge Strategies:**

```gitattributes
# Never merge package-lock.json (always use ours/theirs)
package-lock.json merge=binary

# Use custom merge driver for changelog
CHANGELOG.md merge=union
```

**4. Export and Archive:**

```gitattributes
# Exclude files from git archive
.gitattributes export-ignore
.gitignore export-ignore
tests/ export-ignore
```

### Configuring Custom Diff

```bash
# Set up custom diff driver in Git config
git config diff.json.textconv "jq ."
```

> 🧠 Git attributes are version-controlled, ensuring consistent behavior across all clones.

---

## 🔐 Signed Commits (GPG)

Verify commit authenticity with cryptographic signatures.

### Why Sign Commits?

- **Verification:** Prove commits are from you
- **Security:** Prevent impersonation
- **Trust:** Required by some organizations
- **GitHub Badge:** "Verified" badge on signed commits

### Setup GPG Signing

**1. Generate GPG Key:**

```bash
# Generate new GPG key
gpg --full-generate-key
# Choose RSA and RSA, 4096 bits, expiration as needed

# List GPG keys
gpg --list-secret-keys --keyid-format=long

# Export public key to add to GitHub/GitLab
gpg --armor --export YOUR_KEY_ID
```

**2. Configure Git:**

```bash
# Set your GPG key
git config --global user.signingkey YOUR_KEY_ID

# Enable commit signing by default
git config --global commit.gpgsign true

# Optional: sign tags by default
git config --global tag.gpgsign true
```

**3. Sign Individual Commits:**

```bash
# Sign a specific commit
git commit -S -m "feat: add authentication"

# Sign a tag
git tag -s v1.0.0 -m "Release version 1.0.0"
```

### Verification

```bash
# Verify signatures in log
git log --show-signature

# Verify specific commit
git verify-commit HEAD
```

### Troubleshooting

```bash
# If GPG asks for passphrase every time
export GPG_TTY=$(tty)
# Add to ~/.bashrc or ~/.zshrc

# Windows: Set GPG program path
git config --global gpg.program "C:/Program Files (x86)/GnuPG/bin/gpg.exe"
```

> 💡 Add your GPG public key to GitHub/GitLab under Settings → SSH and GPG keys.

---

## 🧹 Git Maintenance & Optimization

Keep your repository healthy and performant.

### Repository Cleanup

```bash
# Garbage collection (cleanup unreachable objects)
git gc

# Aggressive garbage collection
git gc --aggressive --prune=now

# Remove untracked files and directories
git clean -fd

# Dry run to see what would be removed
git clean -fd --dry-run
```

### Repository Verification

```bash
# Check repository integrity
git fsck

# Verify all objects
git fsck --full
```

### Reduce Repository Size

```bash
# Prune remote-tracking branches
git remote prune origin

# Remove local references to deleted remote branches
git fetch --prune

# Find large files in history
git rev-list --objects --all | \
  git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | \
  awk '/^blob/ {print substr($0,6)}' | \
  sort --numeric-sort --key=2 | \
  tail -n 10
```

### Scheduled Maintenance

```bash
# Enable automatic maintenance
git maintenance start

# Run maintenance tasks manually
git maintenance run

# Stop automatic maintenance
git maintenance stop
```

### Statistics and Analysis

```bash
# Show repository size
git count-objects -vH

# Show who contributed most to a file
git shortlog -sn

# Repository statistics
git log --all --format='%aN' | sort -u | wc -l  # Number of contributors
```

> 🚀 Run `git gc` periodically to optimize repository performance and reclaim disk space.

---

## 🧩 Quick Command Reference

| Command                   | Purpose                         |
| :------------------------ | :------------------------------ |
| `git worktree add`        | Create new worktree             |
| `git lfs track "*.ext"`   | Track files with LFS            |
| `git sparse-checkout set` | Set sparse checkout directories |
| `git commit -S`           | Sign commit with GPG            |
| `git gc --aggressive`     | Aggressive garbage collection   |
| `git submodule update`    | Update submodules               |
| `git maintenance run`     | Run maintenance tasks           |
| `git clean -fd`           | Remove untracked files          |

---

## 🔗 See Also

> Explore related Git documentation:

- [📘 Basics](./Basics.md) — Fundamental Git commands and usage
- [⚙️ Advanced](./Advanced.md) — Advanced Git commands and workflows
- [🧩 Prefixes](./Prefixes.md) — Commit and branch naming conventions
- [🔧 Troubleshooting](./Troubleshooting.md) — Common problems and solutions
- [💡 Tips](./Tips.md) — Practical tips and best practices
- [🔗 Resources](./Resources.md) — External references and learning materials

---

_This guide equips you with modern Git tools essential for professional development workflows and large-scale projects._
