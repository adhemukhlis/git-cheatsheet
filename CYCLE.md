# Git Development Cycle

This document describes the lifecycle of working on a single task or feature, divided into four main phases.

---

## 1. Initial Start (Once per Cycle)

This phase is done only once when you start a new task. It ensures your workspace is clean, updated, and that your branch follows standard naming conventions.

### Step 1: Update the Main Branch

Before creating your new branch, always get the latest code from the remote repository.

```bash
git checkout main
git pull origin main
```

### Step 2: Create a New Branch

Create and switch to your task branch. Use a prefix based on Conventional Commit tags.

**Branch Naming Pattern:** `<tag>/<task-description>` or `<tag>/<task-id>-<description>`

```bash
git checkout -b feat/login-page
```

### Conventional Commit Tags

Use these tags to prefix your branch name and commit messages:

| Tag        | Description                                      | Example Branch Name         |
| :--------- | :----------------------------------------------- | :-------------------------- |
| `feat`     | Adding a new feature                             | `feat/user-login`           |
| `fix`      | Fixing a bug                                     | `fix/button-alignment`      |
| `hotfix`   | Fixing an urgent bug directly in production      | `hotfix/crash-on-boot`      |
| `refactor` | Restructuring code without changing its behavior | `refactor/api-client`       |
| `chore`    | Routine maintenance tasks (dependencies, tools)  | `chore/update-dependencies` |
| `test`     | Adding or updating tests                         | `test/auth-validation`      |
| `docs`     | Documentation updates                            | `docs/api-guide`            |

---

## 2. Repetitive Cycle (Daily Development)

This phase repeats daily or multiple times a day until the task is complete.

### Syncing with Main (Start of the Day)

Keep your feature branch up-to-date with the remote `main` branch to avoid complex merge conflicts later.

> still on feat/login-page

```bash
# 1. Fetch latest changes from remote
git fetch origin

# 2. Rebase your branch onto the latest origin/main
git rebase origin/main
```

#### Handling Rebase Conflicts

If Git reports conflicts during the rebase:

1. Open the conflicted files and resolve the issues.
2. Stage the resolved files:
   ```bash
   git add <file-name>
   ```
3. Continue the rebase process:
   ```bash
   git rebase --continue
   ```
   _(Repeat these steps if there are multiple commits being rebased)._

### Committing Your Work (Throughout the Day)

Commit your changes incrementally. Use clear commit messages following Conventional Commits format.

```bash
git add .
git commit -m "feat: implement login form UI"
```

---

## 3. Ready to Complete (Pre-Push & Pull Request)

Perform these steps when your task is complete and you are ready to share it with your team.

### Step 1: Final Sync with Main

Perform one final rebase to ensure your branch integrates cleanly with the latest changes on `origin/main`.

```bash
git fetch origin
git rebase origin/main
```

### Step 2: Push to Remote Repository

Push your branch to the remote repository.

- **First-time Push:** Set the upstream tracking branch.

  ```bash
  git push -u origin feat/login-page
  ```

- **Subsequent Pushes (After Rebase):** Since rebasing rewrites commit history, you must safely force-push to update the remote branch.
  ```bash
  git push --force-with-lease
  ```

Once pushed, open a Pull Request (PR) or Merge Request (MR) for review.

---

## 4. Closing / Cleanup (End of Cycle)

Once your Pull Request has been approved, merged into the `main` branch, and the task is fully closed, perform these cleanup steps.

### Step 1: Sync Local Main

Get the merged changes onto your local `main` branch.

```bash
git checkout main
git pull origin main
```

### Step 2: Delete Local Branch

Delete your local feature branch since it is no longer needed.

```bash
git branch -d feat/login-page
```

### Step 3: Clean Up Remote Tracking Branches (Optional)

Remove references to remote branches that have been deleted from the server.

```bash
git fetch --prune
```
