# Git and GitHub guide

This guide is written for a first practice session. Read the short explanation before running each command, and run commands one at a time. If a command produces an error, do not immediately repeat it; read the message and check the [troubleshooting guide](../resources/troubleshooting.md).

## Git and GitHub

Git is a distributed version-control system. It records snapshots of a project and lets you compare, restore, and combine changes. GitHub hosts Git repositories and adds collaboration features such as Issues, Pull Requests, reviews, and forking.

### A few words you will see often

- A **repository** (or repo) is a project managed by Git.
- A **commit** is a saved snapshot with a message.
- A **branch** is a named line of work.
- A **remote** is a copy of the repository somewhere else, usually GitHub.
- `main` is a common name for the default branch. A project may use another name.

## Install and configure Git

Check whether Git is installed:

```bash
git --version
```

Install Git using the instructions for your operating system in the official [Git installation documentation](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git). Then configure an author identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

Inspect configuration with `git config --list --show-origin`.

The `--global` option applies the setting to your user account on this computer. Your name and email are written into future commits; they are not a GitHub password.

## Create a repository and commit

```bash
mkdir hello-git
cd hello-git
git init
printf "# Hello Git\n" > README.md
git status
git add README.md
git diff --staged
git commit -m "Add project README"
```

What each important command does:

- `git init` starts Git tracking in the current directory. Run it once for a new project.
- `git status` reports what is new, changed, or staged.
- `git add README.md` selects the file for the next commit.
- `git diff --staged` lets you review exactly what will be committed.
- `git commit -m "..."` records the selected snapshot in your local repository.

The file moves from untracked or modified in the working directory, to staged in the index, to recorded in the local repository. `git log --oneline` shows the resulting history. A commit is local until you push it.

## Connect to GitHub

Create an empty repository on GitHub, then add it as a remote:

```bash
git remote add origin https://github.com/<account>/<repository>.git
git branch -M main
git push -u origin main
```

Here, `origin` is the nickname for the GitHub repository and `main` is the branch being published. The first push uses `-u` to remember the connection, so later `git push` commands can be shorter. If GitHub created a README or other files in the new repository, it may not be empty; follow the repository's displayed instructions or use the collaboration workflow rather than overwriting work.

For an existing project, `git clone <url>` downloads the repository, its history, and a working copy:

```bash
git clone https://github.com/<account>/<repository>.git
cd <repository>
```

`git fetch` downloads remote updates; `git pull` fetches and integrates them; `git push` publishes local commits.

Before using a URL, copy it from the repository's GitHub **Code** button. Use HTTPS or SSH consistently with the authentication method in the [authentication guide](authentication-and-security.md).

## GitHub Issues and contributions

Issues are used to discuss bugs, tasks, and improvements. A contribution normally starts from an Issue or a clearly described change, continues on a feature branch, and reaches the project through a Pull Request. Forking creates your GitHub-owned copy when you do not have direct write access.

## Branch, merge, and review

```bash
git switch main
git pull --ff-only origin main
git switch -c feature/hello-message
# edit and test
git add .
git commit -m "Add hello message"
git push -u origin feature/hello-message
```

Open a Pull Request into `main`. Explain what changed and how it was tested. Reviewers can comment on lines, request changes, and approve. Resolve conflicts when branches changed the same lines; see [branching and merging](../resources/branching-and-merging.md).

### Why not work directly on `main`?

`main` is usually the shared, dependable branch. A feature branch gives you a safe place to experiment, makes the change easier to review, and keeps unfinished work away from the shared branch.

## Working safely

Use `.gitignore` for files that should not be tracked, such as build output, local environment files, and editor metadata. It is not a security boundary: do not place secrets in the repository at all. Review `git diff --staged` before committing and keep commits focused.

The [Git cheatsheet](../resources/git-cheatsheet.md), [Git workflow](../resources/git-workflow.md), and [troubleshooting guide](../resources/troubleshooting.md) provide command-level support.

