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

## 🔗 See Also

> Explore related Git documentation:

- [📘 Basics](./Basics.md) — Fundamental Git commands and usage
- [🧩 Prefixes](./Prefixes.md) — Commit and branch naming conventions
- [⚙️ Advanced](./Advanced.md) — Advanced Git commands and workflows
- [🚀 Modern](./Modern.md) — Modern Git features and tools
- [🔧 Troubleshooting](./Troubleshooting.md) — Common problems and solutions
- [🔗 Resources](./Resources.md) — External references and learning materials

---

_These tips help you maintain clean, efficient, and professional Git workflows every day._
