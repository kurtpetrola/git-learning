# 🧩 Git Prefixes

Consistent commit and branch prefixes help maintain clarity, streamline collaboration, and enable automation such as changelog generation and CI/CD triggers.

---

## 🪶 Git Commit Prefixes

> Based on the [Conventional Commits specification](https://www.conventionalcommits.org/en/v1.0.0/).

| Prefix       | Purpose                                     | Example                                    |
| :----------- | :------------------------------------------ | :----------------------------------------- |
| **feat**     | Introduce a new feature or enhancement      | `feat: add user authentication`            |
| **fix**      | Resolve a bug or issue                      | `fix: correct file upload failure`         |
| **docs**     | Documentation changes only                  | `docs: update README installation guide`   |
| **style**    | Code style or formatting (no logic changes) | `style: apply consistent indentation`      |
| **refactor** | Code restructuring without behavior change  | `refactor: simplify database queries`      |
| **test**     | Add or update tests                         | `test: add unit tests for login feature`   |
| **chore**    | Maintenance or build-related tasks          | `chore: update dependencies`               |
| **perf**     | Performance improvements                    | `perf: optimize image loading`             |
| **ci**       | CI/CD configuration changes                 | `ci: configure GitHub Actions for testing` |
| **build**    | Build system or dependency updates          | `build: update Gradle version`             |
| **revert**   | Revert a previous commit                    | `revert: undo login fix`                   |
| **deps**     | Dependency-specific updates                 | `deps: bump firebase version`              |

> 💡 You may combine prefixes for clarity (e.g., `feat+docs: add guide for login feature`), but keep messages concise.

---

## 🧭 Commit Message Format

`type(scope): short-summary`

**Examples:**

- feat(auth): add google sign-in support
- fix(ui): align login button on mobile

> ✅ Keep summaries under 72 characters and use the imperative mood (e.g., “add” instead of “added” or “adds”).

---

## 🌿 Git Branch Prefixes

| Prefix                 | Purpose                           | Example                          |
| :--------------------- | :-------------------------------- | :------------------------------- |
| **feature/** (`feat/`) | New feature development           | `feature/user-authentication`    |
| **fix/** (`bugfix/`)   | Bug fixes                         | `fix/login-error`                |
| **hotfix/**            | Urgent production fixes           | `hotfix/security-vulnerability`  |
| **release/**           | Release preparation               | `release/v1.2.0`                 |
| **develop/** (`dev/`)  | Development or staging branches   | `dev/staging`                    |
| **chore/**             | Maintenance or build-related work | `chore/update-dependencies`      |
| **refactor/**          | Code refactoring                  | `refactor/database-optimization` |
| **test/**              | Testing branches                  | `test/integration-tests`         |
| **docs/**              | Documentation updates             | `docs/api-documentation`         |
| **style/**             | Styling or UI changes             | `style/css-redesign`             |

> ✏️ Use **lowercase** and **hyphens** for branch names (e.g., `feat/add-login-screen`).

---

## ⚙️ Benefits of Using Prefixes

- 🧭 Organized and readable commit history
- 🪄 Easier changelog generation
- 🌱 Clear branch purpose and ownership
- ⚡ Streamlined CI/CD automation
- 🧑‍💻 Professional and consistent project structure

---

_This guide ensures your repository remains consistent, maintainable, and professional across all stages of development._
