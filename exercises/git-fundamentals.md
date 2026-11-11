# Exercise 1: Git fundamentals

**Level:** beginner | **Suggested approach:** work through the sections in order

Create a temporary practice folder for this exercise so that mistakes do not affect an important project. Replace every placeholder in angle brackets with your own value; do not type the angle brackets.

## Objectives

- Configure Git and identify the current author.
- Create a local repository and make a focused commit.
- Observe the working directory, staging area, local history, and remote.
- Clone a repository and synchronize changes.

## Starting requirements

- Git installed and available in a terminal.
- A GitHub account and permission to create a practice repository.
- A text editor.
- A safe email address for commit attribution.

## Tasks

### A. Configure and inspect

Run `git --version`, set `user.name` and `user.email`, then inspect the configuration. Use an email you are comfortable associating with your GitHub account.

**Checkpoint:** You should be able to identify the configured name and email before continuing.

### B. Create two commits

1. Create a directory and initialize it with `git init`.
2. Add a `README.md` describing a small practice project.
3. Use `git status`, `git diff`, and `git diff --staged` before committing.
4. Commit the README.
5. Add a second file, such as `notes.md`, and commit it separately.
6. Inspect the history with `git log --oneline`.

**Checkpoint:** `git status` should show a clean working tree after each commit, and `git log --oneline` should show at least two commits.

### C. Add a GitHub remote

Create an empty GitHub repository, add it as `origin`, and push the `main` branch:

```bash
git remote add origin <repository-url>
git branch -M main
git push -u origin main
```

**Checkpoint:** Refresh the GitHub repository page and confirm that the README and its commit history are visible.

### D. Clone and update

Clone the repository into a different directory. Make a small change there, commit, and push. In the original directory, fetch and fast-forward the local `main` branch.

For the original directory, the safe sequence is:

```bash
git fetch origin
git switch main
git pull --ff-only origin main
```

## Hints

- `git status` is safe to run at any time.
- Stage only the files for the current commit.
- `git remote -v` shows where pushes and fetches go.
- If authentication fails, consult the authentication guide rather than putting a token in a file.
- If you are unsure what a command changed, stop and run `git status` and `git log --oneline`.

## Expected outcomes

- A repository with at least two meaningful commits.
- A visible difference between unstaged and staged changes.
- A working `origin` remote and a successful push.
- A second clone containing the latest committed change.

## Clean-up

When finished, you may remove only the temporary practice folder using your normal file manager. Keep the GitHub repository if you want to use it for the next exercise.

## Reflection

1. What is the difference between a change in the working directory and a change in the staging area?
2. Why can another person see a commit on your computer but not on GitHub until you push?
3. What information did `git status` provide that `git log --oneline` did not?

