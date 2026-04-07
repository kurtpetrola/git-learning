# Git Prefixes

Consistent commit and branch prefixes help maintain clarity, streamline collaboration, and enable automation such as changelog generation and CI/CD triggers.

---

## Git Commit Prefixes

> Based on the [Conventional Commits specification](https://www.conventionalcommits.org/en/v1.0.0/).

| Prefix       | Purpose                                     | Example                                    |
| :----------- | :------------------------------------------ | :----------------------------------------- |
| **feat**     | Introduce a new feature or enhancement      | `feat: add user authentication`            |
| **fix**      | Resolve a bug or issue                      | `fix: correct file upload failure`         |
| **docs**     | Documentation changes only                  | `docs: update README installation guide`   |
| **style**    | Code style or formatting (no logic changes) | `style: apply consistent indentation`      |
| **refactor** | Code restructuring without behavior change  | `refactor: simplify database queries`      |
| **test**     | Add or update tests                         | `test: add unit tests for login feature`   |
| **chore**    | Maintenance (non-code, non-CI, non-build)   | `chore: update dependencies`               |
| **perf**     | Performance improvements                    | `perf: optimize image loading`             |
| **ci**       | CI/CD configuration changes                 | `ci: configure GitHub Actions for testing` |
| **build**    | Build system configuration/packaging        | `build: update Gradle version`             |
| **revert**   | Revert a previous commit                    | `revert: undo login fix`                   |
| **deps**     | Direct dependency version bumps             | `deps: bump firebase version`              |

> **Warning:** **Breaking Change**: Suffix any prefix with `!` (e.g., `feat!`: or `fix!`:). This signals that the change is API-incompatible and requires a major version bump.

> **Tip:** You may combine prefixes for clarity (e.g., `feat+docs: add guide for login feature`), but keep messages concise.

---

## Common Scopes

Scopes define the specific area of the project the change affects.
Use them consistently to make your commit history more meaningful.

| Scope Example | Description                               |
| :------------ | :---------------------------------------- |
| **auth**      | Authentication and authorization logic    |
| **ui**        | User interface components and styles      |
| **api**       | API integrations or backend communication |
| **db**        | Database models, migrations, or queries   |
| **build**     | Build scripts and configurations          |
| **config**    | Environment or project settings           |
| **docs**      | Documentation content or structure        |

> **Note:** Keep scopes short, lowercase, and descriptive — e.g. `feat(ui): add dark mode toggle`

---

## Extended Prefixes (Optional)

| Prefix    | Purpose                                 | Example                                 |
| :-------- | :-------------------------------------- | :-------------------------------------- |
| **wip**   | Work in progress (not ready for review) | `wip: update dashboard layout`          |
| **temp**  | Temporary or experimental change        | `temp: try alternate login method`      |
| **merge** | Merging branches or resolving conflicts | `merge: resolve feature/auth conflicts` |

> **Warning:** Use these sparingly and squash them before merging to keep the main history clean.

---

## Commit Message Format

`type(scope): short-summary`

**Examples:**

- feat(auth): add google sign-in support
- fix(ui): align login button on mobile

> **Tip:** Keep summaries under 72 characters and use the imperative mood (e.g., "add" instead of "added" or "adds").

> **Tip:** Use tools like [Commitizen](https://github.com/commitizen/cz-cli) or [Conventional Changelog](https://github.com/conventional-changelog/conventional-changelog) to enforce these rules automatically.

---

## Commit Message Do's and Don'ts

### Do:

- ✅ Use a clear, concise summary (e.g., `fix(api): handle 404 errors gracefully`)
- ✅ Write in imperative mood ("add", "fix", "update")
- ✅ Include scope when meaningful
- ✅ Group related commits logically
- ✅ Reference issues or PRs when relevant (e.g., `fix(auth): resolve token refresh bug (#42)`)

### Don't:

- ❌ Write vague messages like "update", "fix stuff", or "misc changes"
- ❌ Use past tense or third person ("added feature", "adds login page")
- ❌ Combine unrelated changes in one commit
- ❌ Use emojis or decorative text in commit subjects
- ❌ Leave long details in the subject — use the body for explanations instead

> **Note:** Think of your commit message as a changelog entry for your future self (and teammates).

### Good vs Bad Examples

| ✅ Good Commit                                 | ❌ Bad Commit         |
| :--------------------------------------------- | :-------------------- |
| `feat(auth): add google sign-in support`       | `added login feature` |
| `fix(ui): align login button on mobile`        | `fixed ui`            |
| `docs(readme): clarify installation steps`     | `update docs`         |
| `refactor(api): simplify error handling logic` | `cleanup code`        |
| `chore(deps): bump react version to 18.2.0`    | `update react`        |

> **Note:** Notice how good commits are structured, specific, and action-oriented, while bad ones are vague or inconsistent.

## Git Branch Prefixes

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

> **Note:** Use **lowercase** and **hyphens** for branch names (e.g., `feat/add-login-screen`).

---

## Benefits of Using Prefixes

- Organized and readable commit history
- Easier changelog generation
- Clear branch purpose and ownership
- Streamlined CI/CD automation
- Professional and consistent project structure

---

## See Also

> Explore related Git documentation:

- [Basics](./Basics.md) — Fundamental Git commands and usage
- [Advanced](./Advanced.md) — Advanced Git commands and workflows
- [Modern](./Modern.md) — Modern Git features and tools
- [Troubleshooting](./Troubleshooting.md) — Common problems and solutions
- [Config](./Config.md) — Useful aliases and configuration examples
- [Cheat Sheet](./CheatSheet.md) — Quick command reference
- [Tips](./Tips.md) — Practical tips and best practices
- [Resources](./Resources.md) — External references and learning materials

---

_This guide ensures your repository remains consistent, maintainable, and professional across all stages of development._
