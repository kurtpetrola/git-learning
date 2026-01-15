# 💡 Git Tips and Best Practices

> Quick tips, reminders, and useful patterns to help you become more efficient with Git.

---

### 🧠 General Tips

- **Commit often, but with purpose.** Small, meaningful commits make it easier to track changes.
- **Write clear commit messages.** Use the imperative mood and describe _what_ and _why_.
- **Tidy up before sharing.** Use `git rebase -i` to squash, reword, or drop commits before pushing a feature branch.
- **Avoid committing secrets.** Use `.gitignore` to exclude sensitive files like `.env`.
- **Pull before pushing.** Always sync your branch before pushing changes to avoid conflicts.
- **Use branches wisely.** Keep `main` or `master` clean; do experimental work in feature branches.

---

### 🧰 Handy Commands

- **Undo last commit (keep changes):**

  ```bash
  git reset --soft HEAD~1
  ```

- **Undo last commit (discard changes):**

  ```bash
  git reset --hard HEAD~1

  ```

- **Amend the previous commit:**

  ```bash
  git commit --amend
  ```

- **Temporarily save uncommitted work:**

  ```bash
  git stash
  git stash pop
  ```

- **View changes before committing:**

  ```bash
  git diff
  ```

- **View branch history visually:**
  ```bash
  git log --oneline --graph --decorate --all
  ```

---

### 🚀 Workflow Recommendations

- Create a `dev` branch for testing changes before merging to `main`.
- Use **Pull Requests (PRs)** even in solo projects for practice and documentation.
- **Force push safely:** If you rebase or amend a shared branch, use git `push --force-with-lease` instead of `--force` to prevent overwriting someone else's work.
- Tag versions using **semantic versioning**:

  ```bash
  git tag -a v1.0.0 -m "Initial release"

  ```

---

### 🧹 Maintenance Tips

- **Clean up merged branches (local)**:

  ```bash
  git branch --merged | grep -v "main" | xargs git branch -d
  ```

- **Prune remote-tracking branches**:
  ```bash
  git remote prune origin
  ```

---

### 🪄 Pro Tips

Use [GitHub Desktop](https://desktop.github.com/) or [GitKraken](https://www.gitkraken.com/) for visualizing commits when learning Git workflows.

---

### 📝 .gitignore Best Practices

- **Start with a template:** Use [gitignore.io](https://www.toptal.com/developers/gitignore) to generate `.gitignore` for your tech stack.
- **Common patterns:**

  ```gitignore
  # Dependencies
  node_modules/
  vendor/

  # Environment variables
  .env
  .env.local

  # IDE and editor files
  .vscode/
  .idea/
  *.swp
  *~

  # OS files
  .DS_Store
  Thumbs.db

  # Build outputs
  dist/
  build/
  *.log
  ```

- **Don't commit sensitive data:** API keys, passwords, tokens should never be in version control.
- **Global gitignore:** Create `~/.gitignore_global` for personal files:

  ```bash
  git config --global core.excludesfile ~/.gitignore_global
  ```

---

### ✍️ Commit Message Templates

Create a commit message template for consistency:

**1. Create template file `~/.gitmessage`:**

```
# <type>(<scope>): <subject>
# |<----  Using a Maximum Of 50 Characters  ---->|

# Explain why this change is being made
# |<----   Try To Limit Each Line to a Maximum Of 72 Characters   ---->|

# Provide links or keys to any relevant tickets, articles or other resources
# Example: closes #23

# --- COMMIT END ---
# Type can be
#    feat     (new feature)
#    fix      (bug fix)
#    refactor (refactoring code)
#    style    (formatting, missing semi colons, etc)
#    docs     (changes to documentation)
#    test     (adding or refactoring tests)
#    chore    (maintain)
# --------------------
# Remember to:
#   - Capitalize the subject line
#   - Use the imperative mood in the subject line
#   - Do not end the subject line with a period
#   - Separate subject from body with a blank line
#   - Use the body to explain what and why vs. how
#   - Can use multiple lines with "-" or "*" for bullet points in body
```

**2. Configure Git to use it:**

```bash
git config --global commit.template ~/.gitmessage
```

---

### 🪝 Git Hooks Quick Tips

- **Make hooks executable:** `chmod +x .git/hooks/pre-commit`
- **Share hooks with team:** Use tools like [Husky](https://typicode.github.io/husky/) (Node.js) or [pre-commit](https://pre-commit.com/) (Python)
- **Common use cases:**
  - `pre-commit`: Run linters, formatters, tests
  - `commit-msg`: Enforce commit message format
  - `pre-push`: Run full test suite

**Example pre-commit hook (lint check):**

```bash
#!/bin/sh
npm run lint
if [ $? -ne 0 ]; then
  echo "❌ Linting failed. Fix errors before committing."
  exit 1
fi
```

---

### 🔍 Code Review Best Practices

- **Keep PRs small:** Easier to review, less likely to introduce bugs
- **Self-review first:** Review your own changes before requesting review
- **Write descriptive PR descriptions:** Include what, why, and how
- **Use draft PRs:** For work-in-progress that needs early feedback
- **Respond to feedback:** Address comments or explain why you disagree
- **Use conventional comments:**
  - `nit:` - Minor suggestion, not blocking
  - `question:` - Asking for clarification
  - `suggestion:` - Proposing an alternative
  - `blocking:` - Must be addressed before merge

---

### 🧼 Repository Hygiene

- **Delete merged branches:** Keep repository clean

  ```bash
  git branch -d feature/completed-feature
  git push origin --delete feature/completed-feature
  ```

- **Run garbage collection periodically:**

  ```bash
  git gc --aggressive --prune=now
  ```

- **Keep commits atomic:** One logical change per commit
- **Squash fixup commits:** Before merging to main

  ```bash
  git rebase -i main
  ```

- **Use meaningful branch names:** `feat/user-auth`, not `my-branch`

---

## 🔗 See Also

> Explore related Git documentation:

- [📘 Basics](./Basics.md) — Fundamental Git commands and usage
- [🧩 Prefixes](./Prefixes.md) — Commit and branch naming conventions
- [⚙️ Advanced](./Advanced.md) — Advanced Git commands and workflows
- [🚀 Modern](./Modern.md) — Modern Git features and tools
- [🔧 Troubleshooting](./Troubleshooting.md) — Common problems and solutions
- [⚙️ Config](./Config.md) — Useful aliases and configuration examples
- [📋 Cheat Sheet](./CheatSheet.md) — Quick command reference
- [🔗 Resources](./Resources.md) — External references and learning materials

---

_These tips help you maintain clean, efficient, and professional Git workflows every day._
