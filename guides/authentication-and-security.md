# Authentication and security

Authentication lets Git prove which GitHub account is connecting. It is separate from repository authorization: your account must also have permission to read or write the repository.

## Choose an authentication method

For a first workshop exercise, HTTPS is usually the easiest place to begin. SSH is convenient for repeated work once its key is configured. You only need one method for a repository; choose the method that matches your remote URL and follow the current GitHub instructions.

## HTTPS and Personal Access Tokens

An HTTPS remote looks like:

```bash
git remote set-url origin https://github.com/<account>/<repository>.git
```

When GitHub requests a password for Git over HTTPS, use a Personal Access Token (PAT), not your GitHub account password. Create a token only through GitHub's current settings, grant the minimum required access, and store it using a supported credential manager. Never paste a token into source code, a command that will be saved in shell history, an Issue, or a chat message. Revoke a token that is exposed or no longer needed.

If a token stops working, do not keep guessing. Check its expiration and permissions, confirm that you are using the intended GitHub account, and create a replacement through GitHub if needed.

## SSH

SSH avoids entering a token for every push after key setup. Create a key with a modern algorithm, protect the private key with a passphrase, add only the public key to GitHub, and test the connection using GitHub's documented command:

```bash
ssh -T git@github.com
git remote set-url origin git@github.com:<account>/<repository>.git
```

Never upload or share the private key. Use separate keys where your organization's policy requires it.

## `.gitignore`

Example:

```gitignore
# Local environment and secrets
.env
.env.*
!.env.example

# Python cache and virtual environment
__pycache__/
.venv/

# Build output
dist/
build/
```

Patterns vary by project. A `.gitignore` prevents untracked files from being added accidentally; it does not remove a file already tracked. For a tracked file that should no longer be tracked:

```bash
git rm --cached <file>
git commit -m "Stop tracking local file"
```

The `--cached` option removes the file from Git's tracking while leaving your local copy on disk. Check `git status` and `git diff --staged` before committing this change.

## Secure habits

- Review staged changes before every commit.
- Use least privilege for tokens and repository access.
- Do not commit passwords, API keys, certificates, private keys, or personal data.
- Rotate credentials immediately after exposure.
- Treat forks and Pull Requests as code from outside your trusted environment until reviewed.

For current token scopes, SSH guidance, and secret-removal procedures, use the official GitHub security documentation linked in [references](../references.md). The guidance in this section is a workshop introduction, not a substitute for your organization's policy.

