# Troubleshooting

Start with `git status`; it usually identifies the current state and the next safe action.

## A simple troubleshooting routine

1. Read the complete error message.
2. Run `git status`.
3. Check the current branch with `git branch --show-current`.
4. Confirm the remote with `git remote -v`.
5. Make one small fix, then run the command again.

Do not delete the `.git` directory or use a force-push as a first response.

## “Nothing to commit”

Git cannot find a change to record. Check that you saved the file, that you are in the expected directory, and that the file is not ignored. Run `git status` and `git diff`. If the change is already committed, use `git log --oneline` to confirm it.

## “Not a git repository”

You are outside a repository, or the repository was not initialized. Move into the project directory or run `git init` when creating a new local repository.

## “Please tell me who you are”

Configure the identity used in commits:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## Authentication failed or permission denied

GitHub does not accept an account password for Git over HTTPS. Use a Personal Access Token (PAT) through a credential manager, or configure an SSH key. See [authentication and security](../guides/authentication-and-security.md). Confirm that the remote URL points to the intended repository and that your account has access.

## “Updates were rejected” on push

The remote has commits you do not have:

```bash
git fetch origin
git log --oneline HEAD..origin/main
git pull --ff-only origin main
```

If fast-forwarding is impossible, inspect the history and resolve the merge deliberately. Do not force-push a shared branch.

## “Your branch is ahead of `origin/main`”

Your local branch has commits that are not on GitHub yet. Review them with `git log --oneline origin/main..HEAD`, then use `git push` when they are ready to share.

## “Your branch is behind `origin/main`”

The remote has commits your local branch does not have. Save or commit your work, then update safely with `git pull --ff-only origin main` when fast-forwarding is possible.

## Merge conflict

Run `git status`, edit every conflicted file, remove conflict markers, test, `git add` the resolutions, and finish the merge. Use `git merge --abort` if you need to return to the pre-merge state.

## Accidentally staged a file

```bash
git restore --staged <file>
```

The file's edits remain in the working directory.

## Accidentally committed locally

If the commit is not shared, `git commit --amend` can correct its message or contents. To remove the last commit while keeping its changes, use `git reset --soft HEAD~1`. If the commit is already shared, prefer `git revert <commit>`.

## Forgot to add a file to a commit

If the commit has not been pushed yet, stage the missing file and amend the commit:

```bash
git add <forgotten-file>
git commit --amend --no-edit
```

Only amend a commit that nobody else is depending on. If it has already been shared, make a new commit instead.

## Recovering a commit with reflog

If a local reset or branch change seems to hide a commit, inspect the local reference history:

```bash
git reflog
git switch -c recovery/<short-name> <commit-from-reflog>
```

Create the recovery branch before attempting further cleanup. Reflog helps with local references; it does not recover a secret that was pushed to GitHub or replace credential rotation.

## Accidentally committed a secret

Revoke or rotate the exposed credential immediately. Removing it in a later commit does not remove it from history. Stop pushing, notify the repository owner, and follow the repository's secret-removal procedure.

