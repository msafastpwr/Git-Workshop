# Git workflow

Git keeps several states separate. Understanding that separation makes the commands predictable.

```text
working directory  --git add-->  staging area  --git commit-->  local repository
       ^                                                            |
       |                                                            | git push
       |                                                            v
       +---------------------- git checkout/fetch/pull -------- remote repository
```

## The four places

1. **Working directory:** the files currently checked out on your computer. Edits here are not yet part of the next commit.
2. **Staging area (index):** the exact snapshot selected for the next commit. Stage only the files and hunks that belong together.
3. **Local repository:** the `.git` database containing commits, branches, and history on your computer.
4. **Remote repository:** a shared copy hosted on a service such as GitHub. `origin` is the conventional name for the main remote.

Think of the staging area as a review desk: Git does not automatically include every file you changed in the next commit. You choose the snapshot with `git add`, inspect it, and then commit it.

## A repeatable local cycle

```bash
git status
# edit files
git diff
git add <files>
git diff --staged
git commit -m "Explain the completed change"
```

Use `git status` often. It tells you which files are modified, staged, untracked, or ahead/behind a remote.

### Reading `git status`

- **Untracked files** are new files Git has not been told to track.
- **Changes not staged for commit** are edits that will not be in the next commit yet.
- **Changes to be committed** are already staged.
- **Your branch is ahead of `origin/main`** means you have local commits that have not been pushed.

## A repeatable remote cycle

Before starting work on a shared branch, update it:

```bash
git switch main
git pull --ff-only origin main
git switch -c feature/meaningful-name
```

After making and testing a focused commit:

```bash
git push -u origin feature/meaningful-name
```

Open a Pull Request on GitHub so the change can be discussed and reviewed before it reaches `main`.

If `git pull` reports conflicts, pause and use the conflict steps in [branching and merging](branching-and-merging.md). Do not delete files or force-push just to make the message disappear.

## Commit guidance

Good commit messages are short, specific, and written as an action:

```text
Add validation for empty repository names
Document SSH key setup
Fix navigation link in workshop README
```

Avoid mixing unrelated formatting, generated files, and feature work in one commit.

