# Collaboration workflow

This workflow combines Git branches with GitHub Issues and Pull Requests.

The short version is: **discuss → branch → change → review → merge → clean up**. The steps below explain what to do at each stage.

## 1. Discuss the work

Use an Issue to describe a bug, improvement, or learning task. Include the problem, useful context, and a clear completion condition. Search existing Issues before opening a duplicate.

## 2. Start from current code

Before changing anything, make sure you know which repository and branch you are using. `origin` normally means your copy; `upstream` normally means the original project.

For an existing repository:

```bash
git clone <repository-url>
cd <repository-name>
git switch main
git pull --ff-only origin main
git switch -c feature/<issue-summary>
```

For someone else's repository, create a fork on GitHub, clone your fork, and add the original repository as `upstream` if you need to keep your fork current:

```bash
git clone <your-fork-url>
cd <repository-name>
git remote add upstream <original-repository-url>
git fetch upstream
git switch main
git merge --ff-only upstream/main
```

## 3. Make and publish a focused change

Edit only the files needed for the Issue. Then review before committing:

```bash
git status
git diff
git add <relevant-files>
git diff --staged
git commit -m "Implement the issue change"
git push -u origin feature/<issue-summary>
```

Do not commit passwords, tokens, private keys, or unrelated local files. Check the staged diff first.

## 4. Open and review a Pull Request

The Pull Request should explain the problem, the solution, how it was tested, and any limitations. Link the Issue where appropriate. Reviewers should check correctness, clarity, tests, documentation, and accidental files—not just formatting.

Authors should respond to feedback with new commits, keep the discussion clear, and update the branch if `main` changes. Reviewers should leave actionable comments and approve only when the change is ready.

If you are unsure what to write, answer four questions: **What changed? Why was it needed? How was it tested? Is anything still unfinished?**

## 5. Integrate and clean up

After approval and required checks, merge according to the repository's policy. Then remove the merged feature branch locally and remotely:

```bash
git switch main
git pull --ff-only origin main
git branch --delete feature/<issue-summary>
git push origin --delete feature/<issue-summary>
```

