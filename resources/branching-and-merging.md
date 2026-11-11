# Branching and merging

A branch is a movable name pointing to a line of commits. Branches let people work on changes without changing the shared default branch directly.

The branch name describes the work, not the person doing it. Examples include `feature/add-search`, `docs/fix-setup`, and `bugfix/incorrect-link`.

## Feature branch flow

```bash
git switch main
git pull --ff-only origin main
git switch -c feature/update-readme
# edit, test, stage, and commit
git push -u origin feature/update-readme
```

Open a Pull Request from `feature/update-readme` into `main`. After review and required checks, merge it through GitHub. Delete the branch when it is no longer needed.

## Which branch am I on?

```bash
git branch --show-current
git status
```

The second command also shows whether your branch is ahead of or behind its remote. Always confirm the branch name before committing or pushing.

## Local merge

For a local merge, first update the target branch:

```bash
git switch main
git pull --ff-only origin main
git merge feature/update-readme
git push origin main
```

In a team repository, use the repository's Pull Request process instead of pushing directly to a protected branch.

## Fast-forward and three-way merges

Suppose `main` has not changed since a feature branch was created:

```text
A---B---C main
         \
          D---E feature
```

A fast-forward merge moves `main` to `E`; there is no separate merge commit. If both branches continue independently:

```text
A---B---C---F main
         \
          D---E feature
```

Git uses the common ancestor `B`, the `main` tip `F`, and the feature tip `E` for a three-way merge. The result may be a new merge commit, and competing edits may cause a conflict.

## Resolving a conflict

Conflicts occur when Git cannot combine competing edits automatically.

Do not panic: a conflict is a request for a human decision, not a damaged repository. Make a copy of important uncommitted work before attempting a complicated resolution.

1. Run `git status` to see the conflicted files.
2. Open each file and choose the correct final content between the conflict markers:

   ```text
   <<<<<<< HEAD
   version on the current branch
   =======
   version being merged
   >>>>>>> feature/update-readme
   ```

3. Remove all markers and test the result.
4. Stage each resolved file: `git add <file>`.
5. Finish with `git commit` or continue the Pull Request's conflict-resolution flow.

To abandon a local merge before committing:

```bash
git merge --abort
```

Resolve the cause, not just the markers: retain the behavior both sides need, and ask the contributors when the intended result is unclear.

