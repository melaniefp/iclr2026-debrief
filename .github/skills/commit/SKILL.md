---
name: commit
description: Guide for safely committing changes. Use this skill when you are about to make a git commit.
---

# Commit

This skill guides you through safely committing changes to the repository. It ensures you are on the correct branch, selectively stage only relevant files, pass quality checks, and handle pre-commit hook issues.

## When to use this skill

You are about to create a git commit.

## Step 1: Determine the current branch

Run `git branch --show-current` to check which branch you are on.

### If you are on the `main` branch

1. Stash your working changes: `git stash --include-untracked`.
2. Pull latest from remote: `git pull origin main`.
3. Create and switch to a new feature branch: `git checkout -b <branch-name>`.
   - Use `copilot/<descriptive-name>` naming convention (e.g., `copilot/add-feature`).
4. Pop the stash: `git stash pop`.

### If you are on a non-main branch

Decide whether your changes belong to the current branch's feature or are unrelated:

**Adding to the current feature** (e.g., the user asked you to iterate on existing work on this branch):
- No branch switch needed. Proceed directly to Step 2.

**Working on an unrelated feature**:
1. Stash your working changes: `git stash --include-untracked`.
2. Switch to main and pull latest: `git checkout main && git pull origin main`.
3. Create and switch to a new feature branch from the updated main: `git checkout -b <branch-name>`.
   - Use `copilot/<descriptive-name>` naming convention.
4. Pop the stash: `git stash pop`.

> **Note**: If `git stash pop` produces merge conflicts, resolve them before proceeding.

## Step 2: Selectively stage files

**Never run `git add .` or `git add -u`**. The working tree often contains untracked files and unrelated modifications that should not be included in the commit.

1. Run `git status` to review the working tree.
2. Identify which changed files are relevant to the commit you are making.
3. Stage only the relevant files: `git add <file1> <file2> ...`.
4. After staging, run `git diff --cached --stat` to double-check the staged changes.

## Step 3: Run quality checks on changed files

Before committing, verify that your changes pass type checking and tests.

### Pyright

Run pyright on the staged files:

```bash
uv run pyright <file1> <file2> ...
```

If there are errors:
- Fix genuine type issues in the code.
- For false positives or unavoidable cases, prefer `# type: ignore[<rule>]` over convoluted workarounds (e.g., casting to `Any`) — readability matters more.
- Re-run pyright to confirm fixes.

### Pytest

Run relevant tests:

```bash
uv run pytest <relevant-test-files-or-directories>
```

- If your changes are in `projects/foo/src/`, run `uv run pytest projects/foo/tests/`.
- If you can identify the specific test file(s), run those directly.

## Step 4: Commit with pre-commit checks

Run the commit:

```bash
git commit -m "<conventional commit message>"
```

The pre-commit hooks will run automatically. Common issues and how to handle them:

### Trailing whitespace / formatting

Pre-commit hooks (e.g., `trailing-whitespace`, `ruff-format`) will auto-fix formatting issues. If the commit fails due to these:
1. Review the auto-fixed changes with `git diff`.
2. Stage the fixes: `git add <fixed-files>`.
3. Re-run the commit.

### Codespell

The codespell hook checks for common misspellings. **Do not blindly accept codespell suggestions** — it can misfire on technical terms, variable names, or domain-specific words that are not in its dictionary.

If codespell flags a false positive:
1. Verify that the flagged word is intentionally spelled that way.
2. If it is a legitimate technical term, add it to the `ignore-words-list` in `.codespellrc`.
3. Only fix genuinely misspelled words.

### Other pre-commit failures

- **check-json5**: Validates JSON5 files. Fix any syntax errors.
- **end-of-file-fixer**: Ensures files end with a newline. Accept the auto-fix.
- **ruff check**: Linting issues. Fix the flagged issues or add targeted `# noqa:` comments if justified.

After all pre-commit checks pass and the commit succeeds, verify the commit with `git log --oneline -1`.

## Commit message conventions

Use conventional commit format:

```
type(scope): description
```

- **Types**: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`, `ci`
- **Scope**: Optional, e.g., `core`, `evolution`, `logging`
- **Examples**:
  - `feat(evolution): add crossover mutation support`
  - `fix(core): resolve database connection leak`
  - `docs: update installation instructions`

Always include the co-authorship trailer:

```
Co-authored-by: Copilot <223556219+Copilot@users.noreply.github.com>
```
