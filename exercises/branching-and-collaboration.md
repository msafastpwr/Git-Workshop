# Exercise 2: Branching and collaboration

**Level:** beginner to intermediate | **Prerequisite:** complete [Git fundamentals](git-fundamentals.md)

Use a practice repository or a repository where you have permission to create branches and Pull Requests. Never experiment on an important production repository.

## Objectives

- Develop a feature on a branch instead of directly on `main`.
- Publish a branch and describe its work in a Pull Request.
- Practice review, merging, and conflict resolution.
- Use an Issue and a safe collaboration workflow.

## Starting requirements

- A completed Git fundamentals exercise or equivalent experience.
- A GitHub repository where you can create branches and Pull Requests.
- At least one teammate for the review and conflict portions.
- A small text file or README section that both collaborators can edit.

## Tasks

### A. Create an Issue and feature branch

In a practice repository, create an Issue for a small documentation or code improvement. Update local `main`, then create a branch named `feature/<short-description>`.

**Checkpoint:** Run `git branch --show-current` and confirm that the result is your feature branch, not `main`.

### B. Make and publish the change

Make the smallest useful change, inspect the staged diff, commit it, and push the branch:

```bash
git switch main
git pull --ff-only origin main
git switch -c feature/<short-description>
# make and test the change
git add <relevant-files>
git commit -m "Describe the feature"
git push -u origin feature/<short-description>
```

Open a Pull Request linked to the Issue. Include what changed and how you tested it.

**Checkpoint:** The Pull Request should show only the files and lines related to your Issue.

### C. Review a teammate

Read a teammate's Pull Request. Leave one specific, actionable comment or approve it if it is ready. If changes are requested, the author should add a follow-up commit and push it to the same branch.

### D. Resolve a controlled conflict

Two collaborators should edit the same small section differently on separate branches. Open a Pull Request or merge locally until Git reports a conflict. Inspect `git status`, choose the correct combined result, remove markers, test, stage, and finish the merge. If the result is unclear, stop and ask the authors rather than guessing.

Do not intentionally create a conflict in an important project. A small heading or sentence in a practice README is enough.

### E. Finish and clean up

After the Pull Request is merged, update local `main` and delete the obsolete local and remote feature branches.

```bash
git switch main
git pull --ff-only origin main
git branch --delete feature/<short-description>
git push origin --delete feature/<short-description>
```

## Hints

- Pull before creating a new branch.
- Do not resolve a conflict by blindly choosing “ours” or “theirs”; understand both edits.
- Keep review comments about behavior, correctness, maintainability, or missing documentation.
- Use `git merge --abort` if a local merge should be abandoned.
- Before deleting a branch, confirm that its Pull Request was merged and that you no longer need unpushed work.

## Expected outcomes

- A feature branch with a focused commit and an open or completed Pull Request.
- At least one meaningful review interaction.
- A conflict resolved with no conflict markers left in the files.
- A clean local `main` branch after integration.

## Reflection

Write down one difference between working directly on `main` and working on a feature branch. Also note which command helped you understand the repository state most clearly.

1. Why is updating from `main` before creating a feature branch useful?
2. What information should a reviewer receive in a Pull Request description?
3. What did Git need you to decide during the conflict?

