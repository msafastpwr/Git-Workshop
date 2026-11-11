# Git cheatsheet

Run these commands from inside a project directory. Replace values in `<angle brackets>`.

## The beginner cycle

For most small changes, use this order:

```bash
git status
# edit a file
git diff
git add <file>
git diff --staged
git commit -m "Describe the change"
git push
```

Do not skip the two diff commands while learning. The first shows edits that are not staged; the second shows what the next commit will contain.

## Identity and setup

```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --list --show-origin
```

Use the email associated with your GitHub account when you want commits linked to that account.

## Create or inspect a repository

```bash
git init
git status
git log --oneline --decorate --graph --all
git log -p -2
git show <commit>
git diff
git diff --staged
```

Run `git init` only when creating a new local repository. Do not run it inside an already cloned repository.

- `git log --oneline --decorate --graph --all` shows a compact view of branches and commits.
- `git log -p -2` shows the patch from the two most recent commits.
- `git show <commit>` shows one commit and the files it changed.

## Stage and commit

```bash
git add <file>
git add .
git restore <file>                 # discard unstaged changes in a file
git restore --staged <file>        # unstage without deleting the changes
git commit -m "Describe the change"
git show <commit>
```

Review `git status` and `git diff --staged` before every commit. A commit should represent one understandable change.

## Remotes and synchronization

```bash
git remote -v
git remote add origin <repository-url>
git remote set-url origin <repository-url>
git fetch origin
git pull --ff-only origin main
git push -u origin main
git push
```

`fetch` downloads remote history without changing your files. `pull` fetches and integrates changes; `--ff-only` prevents Git from creating an unexpected merge commit.

## Clone and branches

```bash
git clone <repository-url>
cd <repository-name>
git branch
git switch -c feature/<short-name>
git switch main
git branch --delete feature/<short-name>
git push -u origin feature/<short-name>
git push origin --delete feature/<short-name>
```

`git switch -c` creates a branch and switches to it. `git switch <name>` changes to an existing branch. Confirm the current branch with `git branch --show-current`.

## Merge and inspect history

```bash
git switch main
git pull --ff-only origin main
git merge feature/<short-name>
git log --oneline --graph --decorate --all
git diff main...feature/<short-name>
```

If the feature branch is directly ahead of `main`, Git can make a **fast-forward merge** by moving the `main` label forward. If both branches have new commits, Git creates a **three-way merge** using the two branch tips and their common ancestor. Either type can still require conflict resolution.

If a merge conflicts, edit the marked files, then:

```bash
git add <resolved-file>
git commit                         # finish a merge
git merge --abort                  # abandon the merge
```

## Temporarily set work aside

Use stash for unfinished, uncommitted changes when you need a clean working directory briefly:

```bash
git stash push -m "work in progress"
git stash list
git stash pop
git stash drop stash@{0}
```

`git stash pop` applies the saved changes and removes that stash if successful. Review the result with `git status`; a stash can also produce conflicts.

## Safe undo

```bash
git commit --amend                  # only before sharing the commit
git revert <commit>                 # create a new commit that reverses it
git reset --soft HEAD~1              # undo commit, keep staged changes
git reset HEAD~1                     # undo commit, keep changes unstaged
git restore --source=<commit> -- <file>
```

Avoid rewriting commits already pushed to a shared branch. If rewriting your own remote branch is necessary, prefer `git push --force-with-lease` over `--force` and coordinate first.

## Recovering lost local history

`git reflog` records where local branch and `HEAD` references have pointed recently:

```bash
git reflog
git show <reflog-commit>
git switch -c recovery/<short-name> <reflog-commit>
```

Reflog is mainly for local recovery and is not a permanent copy of shared history. Do not delete or reset anything until you have identified the commit you want to keep.

## Additional learning

`git rebase` can replay local commits onto a new base, but it rewrites commit history. It can be useful on a private feature branch, but do not use it casually on shared branches. Read the official documentation before practicing it.

## What to type for placeholders

If a command contains `feature/<short-name>`, replace it with a real branch name such as `feature/update-readme`. If it contains `<repository-url>`, paste the URL copied from GitHub. Do not include the angle brackets.

